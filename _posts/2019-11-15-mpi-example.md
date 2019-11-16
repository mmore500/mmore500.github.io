---
layout: post
title:  "MPI Code Example: Latency-hiding Variable-length Messages on a Toroidal Grid"
date:   2019-11-15
no_toc: true
---

<iframe width="560" height="315" src="https://www.youtube.com/embed/-MqlC0PLS9A" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

In preparation for parallelizing our evolution-of-multicellularity research code (a.k.a. [SignalGP DISHTINY](https://osf.io/g58xk/)), I threw together some starter C++ code with the key [MPI](https://en.wikipedia.org/wiki/Message_Passing_Interface) functionality we'll need: sending and receiving variable-length messages on a toroidal grid.
Without further ado...

## The Toy Problem

Arrange available MPI processes in a square 2D toroidal grid.
Assume the number of available MPi processes is a perfect square.

<p><a href="https://commons.wikimedia.org/wiki/File:2d_torus.png#/media/File:2d_torus.png"><img width="100%" src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/cc/2d_torus.png/1200px-2d_torus.png" alt="2d torus.png"></a><br>By <a href="//commons.wikimedia.org/w/index.php?title=User:Yli47&amp;action=edit&amp;redlink=1" class="new" title="User:Yli47 (page does not exist)">Yixuan Li</a> <span class="img-responsive" class="int-own-work" lang="en">Own work</span>, <a href="https://creativecommons.org/licenses/by-sa/4.0" title="Creative Commons Attribution-Share Alike 4.0">CC BY-SA 4.0</a>, <a href="https://commons.wikimedia.org/w/index.php?curid=53610657">Link</a></p>

Every MPI process selects a unique character (e.g., `A`) based on their MPI rank and then sends messages containing their to unique character to all four grid neighbors.
Messages are variable-length:
* send a 1 character message to the North neighbor (e.g., `A`),
* send a 2 character message to the South neighbor (e.g., `AA`),
* send a 3 character message to the East neighbor (e.g., `AAA`), and
* send a 4 character message to the West neighbor (e.g., `AAAA`).

Wait for all messages to be received then print out own location, ID, and received messages so we know everything worked!


## The Algorithm

Each MPI process performs the following steps.

1. for each neighbor `n`
    1.  post a non-blocking send message to `n`
2. perform (hypothetical) computational work
    * because the sends were non-blocking, we can take care of unrelated beep-boop business while messages are en route
    * this is known as "overlapping communication with computation" or "latency-hiding"
3. do number of neighbors times
    1. blocking probe for *any* incoming message
    2. reserve enough space to copy down the message
        * (we don't know message size before the blocking probe)
    3. blocking receive to copy down incoming message
4. wait for all non-blocking sends to complete
5. print out who I am and what messages I got
    * all on one line to prevent interleaved output messages

## The Code Snippet

Note: MPI API calls are somewhat byzantine and cryptic.
(Hello, out params.)
However, their names are usually kind of descriptive at a high level.
If you're new to MPI, I'd recommend just focusing on the big picture while reading the code below.
But if you really want to dig in to the details, here's the [API reference](https://www.mpich.org/static/docs/latest/www3/) for all of the MPI calls made in the code.

`main.cc`:
```c++
#include <iostream>
#include <sstream>
#include <vector>
#include <unordered_map>
#include <cmath>
#include <algorithm>

#include "mpi.h"

// some slick book-keeping for cardinal directionality
struct Cardi {

  // cardinal directions
  enum Dir { N, S, E, W, NumDirs };

  // transforms
  static constexpr Dir Opp[] { S, N, W, E };
  static constexpr Dir Cw[] { E, W, S, N };
  static constexpr Dir Ccw[] { W, E, N, S };
  static constexpr int Dim[] { 1, 1, 0, 0 };
  static constexpr int Dx[] { 0, 0, 1, -1 };
  static constexpr int Dy[] { 1, -1, 0, 0 };
  static constexpr int Dd[] { 1, -1, 1, -1 };

};

int main(int argc, char* argv[])
{

  MPI_Init(&argc, &argv);

  // make a square grid out of available processes
  MPI_Comm comm_grid;
  const int ndim = 2;
  const int nprocs = [&](){
    int res;
    MPI_Comm_size(
      MPI_COMM_WORLD,
      &res
    );
    return res;
  }(); // use immediately-invoked lambda for consty goodness
  const std::array<int, ndim> dimension{ {
    static_cast<int>(std::sqrt(nprocs)),
    static_cast<int>(std::sqrt(nprocs))
  } };
  const std::array<int, ndim> periodic{ {1, 1} }; // toroidal wraparound

  MPI_Cart_create(
    MPI_COMM_WORLD,
    ndim,
    dimension.data(),
    periodic.data(),
    1, // allow reordering of world ranks
    &comm_grid
  );

  // get world rank info
  // which MPI proc am I in the ?
  const int w_rank = [&](){
    int res;
    MPI_Comm_rank(
      MPI_COMM_WORLD,
      &res
    );
    return res;
  }(); // use immediately-invoked lambda for consty goodness

  // get comm_grid info
  // where am I (x,y) in the grid?
  const std::array<int, ndim> coords = [&](){
    std::array<int, ndim> res;
    MPI_Cart_coords(
      comm_grid,
      w_rank,
      ndim,
      res.data()
    );
    return res;
  }(); // use immediately-invoked lambda for consty goodness
  // what is my rank in the grid?
  const int g_rank = [&](){
    int res;
    MPI_Cart_rank(
      comm_grid,
      coords.data(),
      &res
    );
    return res;
  }();

  // calculate neighboring ranks
  // store in array, indexed by cardinal direction
  const std::array<int, Cardi::Dir::NumDirs> neighs = [&](){
    std::array<int, Cardi::Dir::NumDirs> res;
    for (size_t i = 0; i < Cardi::Dir::NumDirs; ++i) {
      MPI_Cart_shift(
        comm_grid,
        Cardi::Dim[i],
        Cardi::Dd[i],
        const_cast<int *>(&g_rank),
        &res[i]
      );

    }
    return res;
  }(); // use immediately-invoked lambda for consty goodness

  // GOAL:
  // everyone broadcasts a unique character to each cartesian neighbor
  // send 1 byte North, 2 bytes South, 3 bytes East, and 4 bytes West
  const unsigned char id = 65 + g_rank;

  // prepare for sends
  const std::vector<unsigned char> send_data(Cardi::Dir::NumDirs, id);
  std::array<MPI_Request, Cardi::Dir::NumDirs> send_requests;

  // post non-blocking send requests to each neighbor
  for (size_t i = 0; i < Cardi::Dir::NumDirs; ++i) {
    MPI_Isend(
      send_data.data(),
      i + 1, // message length
      MPI_BYTE, // message data type
      neighs[i], // message destination
      i, // tag represents outgoing direction
      comm_grid, // use the grid communicator group
      &send_requests[i] // use later to check up if send completed
    );
  }

  // whee!
  // DO COMPUTE WORK HERE
  // while messages are en route

  // data structure to store incoming message data
  // incoming direction -> result
  std::unordered_map<int, std::vector<unsigned char>> received;

  // receive messages from each neighbor, in any order
  for (size_t i = 0; i < Cardi::Dir::NumDirs; ++i) {

    // block until we get any message
    MPI_Status status;
    MPI_Probe(
      MPI_ANY_SOURCE,
      MPI_ANY_TAG,
      comm_grid,
      &status
    );

    // how long is the message, who sent it, and from what direction
    const int msg_len = [&](){
      int res;
      MPI_Get_count(
        &status,
        MPI_BYTE,
        &res
      );
      return res;
    }(); // use immediately-invoked lambda for consty goodness
    const int msg_source = status.MPI_SOURCE;
    const int msg_tag = status.MPI_TAG;
    const int incoming_direction = Cardi::Opp[msg_tag];

    // make space for incoming data
    received.emplace(
      std::piecewise_construct,
      std::forward_as_tuple(incoming_direction),
      std::forward_as_tuple(msg_len)
    );

    // copy down data from message
    MPI_Recv(
      received.at(incoming_direction).data(), // where to put it
      msg_len, // how long is the message
      MPI_BYTE, // message data type
      msg_source, // who sent it, makes sure we grab the right message!
      msg_tag, // what it's tagged, makes sure we grab the right message!
      comm_grid, // use the grid communicator group
      MPI_STATUS_IGNORE // yup
    );

  }

  // wait for all sends to complete
  MPI_Waitall(
    send_requests.size(),
    send_requests.data(),
    MPI_STATUSES_IGNORE
  );

  // print my results!
  std::ostringstream oss;
  // who am I...
  oss << "rank " << g_rank << ", id " << id
    << " @ (" << coords[0] << ", " << coords[1] << ")";
  // ..and what did I get?
  for (const auto & [k, v] : received) {
    oss << " [" << k << ": ";
    std::for_each(
      std::begin(v),
      std::end(v),
      [&oss](auto c){ oss << c; }
    );
    oss << "]";
  }
  // print out my info on one line in one go!
  std::cout << oss.str() << std::endl;

  MPI_Finalize();

  return 0;
}
```

"Go Go Gadget!":
```bash
# load dependencies on our MSU iCER SLURM/CentOS 7 cluster
module purge; module load GCC/8.2.0-2.31.1 OpenMPI/3.1.3;
# compile
mpic++ -std=c++17 main.cc
# run with 9 (or any other square number) of MPI procs
mpiexec -n 9 ./a.out
```

output:
```
rank 7, id H @ (1, 1) [2: BBBB] [0: II] [3: EEE] [1: G]
rank 2, id C @ (2, 2) [0: AA] [1: B] [2: FFFF] [3: III]
rank 4, id E @ (0, 1) [2: HHHH] [1: D] [3: BBB] [0: FF]
rank 5, id F @ (0, 2) [3: CCC] [0: DD] [1: E] [2: IIII]
rank 1, id B @ (2, 1) [1: A] [3: HHH] [2: EEEE] [0: CC]
rank 6, id G @ (1, 0) [0: HH] [2: AAAA] [1: I] [3: DDD]
rank 0, id A @ (2, 0) [1: C] [2: DDDD] [3: GGG] [0: BB]
rank 8, id I @ (1, 2) [2: CCCC] [1: H] [3: FFF] [0: GG]
rank 3, id D @ (0, 0) [3: AAA] [2: GGGG] [0: EE] [1: F]
```

## References

1. Victor Eijkhout's textbook [*Parallel Programming for Science and Engineering*](https://bitbucket.org/VictorEijkhout/parallel-computing-book/src/default/)
2. Wes Kendall's blog post [*Dynamic Receiving with MPI Probe (and MPI Status)*](https://mpitutorial.com/tutorials/dynamic-receiving-with-mpi-probe-and-mpi-status/)

## Let's Chat

I would love to chat about your thoughts, questions, and comments RE: the code!!!

I started a twitter thread (right below) so we can chat :phone: :phone: :phone:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">blogged an annotated <a href="https://twitter.com/hashtag/cpp?src=hash&amp;ref_src=twsrc%5Etfw">#cpp</a> <a href="https://twitter.com/hashtag/MPI?src=hash&amp;ref_src=twsrc%5Etfw">#MPI</a> snippet w/ latency-hiding variable-length msg passing on a toroidal grid... buckle up for some nifty beep boop biz!<a href="https://t.co/jNiDkS5HrF">https://t.co/jNiDkS5HrF</a><br><br>it&#39;s the starter kit for my evolve-multicells-w/-hella-distributed-computaz project! cool things ahead 😎🛣️</p>&mdash; Matthew A Moreno (@MorenoMatthewA) <a href="https://twitter.com/MorenoMatthewA/status/1195474712576614402?ref_src=twsrc%5Etfw">November 15, 2019</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
Pop on there and drop me a line :fishing_pole_and_fish:, make a comment :raising_hand_woman:, or leave your own cool MPI snippets and/or memes :heart:
