---
layout: post
title:  "Logistical Lessons Learned about Administering Workshop Applications"
date:   2020-05-12
---

We're in the process of wrapping up participant selection for our upcoming [Workshop for Avida-ED Software Development (WAVES)](https://mmore500.com/waves).
This workshop will team up early-career participants with mentors to help build the software foundation that will underly the next version of Avida-ED (as well as more broadly supporting web-based scientific apps and digital evolution research).

So far, almost everything's been turning up roses.
At least, the important things have: soliciting quality applications and thoughtful group discussion and decisions on admission.
Behind the scenes, we've been racing to put all the pieces in place in time for our expected start date in two weeks, a build-the-plane-as-you-fly-it sort of situation.
(We started planing the workshop only about a month ago, in part due to funding unexpectedly becoming available due to the ongoing situation with COVID-19.)

Lets go ahead and jump into what worked well and what we'd like to change up next time.

## Soliciting Applications

This point seems obvious in retrospect, but in order to effectively recruit you need to put together a written job description or call for participants.
Sitting down to write up a call for participants, in my view, is where our planning for the workshop really started to gain traction.
Prior to this point, we had discussed the scope of newly available funding and the kinds of activities we would like to spend it on in broad terms.
Writing down a call for participants made the workshop much easier to explain to potential applicants we approached in person and --- because it was so easy to share --- opened the door to a much broader pool of applicants.
Plus, the text forced stakeholders to make our vision for the workshop concrete and explicit.
More than anything else, engaging with each other over the call for participants brought us stakeholders all together onto the same page.

We chose to publish our call for participants as a website.
This made it even easier to share --- we just had to distribute a url --- and allowed us to push our announcement out quickly with the confidence that we would be able to  make minor corrections as needed (fixing typos, updating contact information, etc.).
You can see what the site looked like to applicants [here](https://web.archive.org/web/20200513004954/http://mmore500.com/waves//).
Under the hood, the site is built with [Jekyll](https://jekyllrb.com/) and hosted with [GitHub Pages](https://pages.github.com/).
You can view (and fork!) the website's source at [https://github.com/mmore500/waves](https://github.com/mmore500/waves).
As the workshop progresses, we are looking forward to using the workshop website to host week-to-week organizational information as well as showcase our participants and their projects.

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">we&#39;re recruiting participants (esp. undergrads) for a ten-week, funded ($6k), full-time, fully-remote software development workshop this summer! 🌞💻<br><br>help build C++/JS tools for digital evolution &amp; interactive science web apps<br><br>details &amp; application -&gt; <a href="https://t.co/uTuX5HIKMG">https://t.co/uTuX5HIKMG</a></p>&mdash; Matthew A Moreno (@MorenoMatthewA) <a href="https://twitter.com/MorenoMatthewA/status/1253777310567682048?ref_src=twsrc%5Etfw">April 24, 2020</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Once we had the call for participants put together, we threw it out into the world!
Instead of assigning a particular stakeholder to distribute (or manage distributing) the call for participants, we simply had everyone distribute it where they saw fit.
Dr. Ofria and I shared the call for participants with the [Advanced C++ Seminar](http://mmore500.com/cse-491/) students we had last semester.
Various stakeholders forwarded information to department secretaries and mentors at previous institutions and acquaintainces who managed email lists at MSU.
(We prepared a condensed ASCII summary of our call for proposals, [included at the end](#appendix-a-ascii-call-for-participants),
I put a tweet up that got shared a few times.
Dr. Ofria threw [a post up](https://www.reddit.com/r/msu/comments/g7bwk8/seeking_cjavascript_developers_to_participate_in/) on the [MSU reddit](https://www.reddit.com/r/msu).
Dr. Blackwood put an announcement up on [the school-endorsed job board](https://www.joinhandshake.com/).

This shotgun approach worked well for us.
Over the week and a half we circulated our call for participants, we received 92 applications for the workshop.

Receiving too many applicants is, generally speaking, a much better problem than receiving too few.
However, even with eleven sets of hands on deck, sorting through nearly a hundred applications was a big task.
In future years, we might give some consideration to the signal-to-noise ratio that our different dissemination mechanisms yielded.
Anecdotally, the school-endorsed job board (Handshake) seemed to perform poorly in this regard.
When making future decisions about where to advertise, though, we will have to seriously consider questions of equity and inclusion.

## Application Materials

The lesson learned here: make your ask very specific.

Here's what we asked for from applicants.

> Applications should consist of:
>
> 1. a curriculum vitae or resume,
> 2. a brief (appox. 500 to 1000 words) statement that describes
>   * your personal background and career goals,
>   * your interest in the program, and
>   * an interesting coding project you’ve tackled.
>      * in any setting: school, hackathon, personal project, research, work, etc.
>      * as possible, link us to the code, the deployment, the project website, a writeup, and/or presentation!
>   * and, optionally, two references for your coding ability (include name, email, and relationship).
>
> Applications should be submitted to avida-waves@googlegroups.com with the subject line “WAVES Application” no later than May 4, 2020.
>
> We will announce participant selection no later than May 11, 2020.

First things first: ask for PDF files.
You should probably be prepared to deal with the Word documents that will inevietably roll in, but cutting the number of misformatted resumes you end up digging through by even half counts as a win in my book.

Next, in our case, we should have said what *not* to submit.
We ended up with a veritable zoo of files submitted: `.zip` archives of code, loose `.java` files, PDFs of term papers, PowerPoints, and more.
(Oh my!)
Clarifying what we did (and didn't) mean by "link" would have saved us some headaches.

The rationale behind asking for a specific subject line was to make harvesting emailed-in applications easier.
However, there is no universe in which every single application comes in with the subject line "WAVES Application" so this pipe dream is basically useless.
Instead, ask applicants to put their names as the subject line.
This will make organizing applications much easier and, unlike the process of gathering applications where some might fall through the cracks, erroneous names are straightforward to spot and fix up later on.
Asking applicants to submit applications from their school email would have made sorting through applications easier later on, too.

We had a applicant follow up with us after we had announced our workshop admission decisions to ask what criteria we had used to evaluate applications.
We said we were looking for applicants with C++ and/or JavaScript experience (or strong experience in other programming languages) right above the instructions for application materials.
However, in addition to programming experience, we also evaluated how applicants' statements aligned with the workshop objectives we laid out at the very top of the call for proposals.
Although our evaluation criteria were all directly rooted in our call for proposals, this applicants' inquiry highlighted how these criteria might not be entirely obvious to all applicants, particularly those from backgrounds that have not trained them to pick up on such implicit cues.
Laying out point-by-point exactly what we will be looking for in a strong application seems the best way to ensure that _every_  applicants' materials most clearly reflect their potential.

The WAVES workshop stakeholders strongly and unanimously believe in the importance of supporting inclusion and equity within our fields, particularly with respect to underrepresented groups.
Recruiting mentees and hiring colleagues who demonstrate a similar commitment provides key means toward this goal.
In a significant oversight, however, we failed to ask applicants to describe their perspective on and enterprise for inclusion and equity.
This failure deprived applicants, particularly those who have prioritized action to promote inclusion and equity, of the opportunity to showcase their commitment.
Because applicants from underrepresented backgrounds are often some of the strongest champions for inclusion and equity, failing to ask for a diversity statement hinders our own efforts to recruit in a manner that promotes equity and inclusion.
Finally, this oversight also represented a lost opportunity to further cement consideration of inclusion and equity as a norm in our fields.
In any future calls for participants, we plan to correct this mistake.

## Accepting Applications

We accepted applications by email.
This method was easy to set up, easy for applicants to use, flexible, and robust.
The major downside to accepting applications by email was organizing applications after we had received them.
(We did discover some tools, covered in the next section, that made this downside mostly manageable.)
Much larger-scale solicitations should probably consider setting up something like a [Google Form](https://www.google.com/forms/about/) or paying for a pre-built software-as-a-service solution.

We set up a private [Google Groups](https://groups.google.com/) group, which comes with its own email address, to receive applications.
After distributing our call for participants, we came to the stomach-turning realization that only registered group members could send email to the group.
Luckily, we found an obscure configuration switch to toggle to turn the group into a "Shared Inbox," which fixed our problem.
The takeaway lesson here: test your means for accepting applications before you share it!
After we had it set up correctly, the Google groups shared inbox automatically forwarded all applications to several workshop stakeholders.
This was actually quite handy.

We had originally also planned to also use the Google group to coordinate workshop logistics among stakeholders.
A slack channel is turning out to serve this purpose better.
Having intra-workshop emails interspersed with applications turned out to be a huge headache, making double-checking that no application slipped through the cracks much more difficult than it needed to be.
If you do use a Google group to receive applications, be sure to set one up that exclusively serves that purpose.

Another minor pain point was Handshake's proprietary application submission system.
I would wholeheartedly recommend choosing one pipe for *all* applications to go through and then strictly ensuring *all* applications end up going through that pipe.
One might disable alternate submission options as possible or follow up with applicants to ask them to resubmit through the preferred pipe.
Although making accommodations for a few cases doesn't take much time or effort up front, it makes final validation that no applications fell through the cracks much more difficult.

Similarly, we would have benefited from planning how to handle late applications.
We should have made the text of our call for proposals more explicit.
If you plan to consider late applications, the text of the call for applications should say so with language like "for full consideration" or "rolling deadline."
Similarly, if you don't plan to consider late applications, the text should probably explicitly say so with language like "strict deadline."
If you do plan to consider late applications, be sure to have a plan about how they will fit into the review process, especially if it is already underway.

Finally, as packets came in we replied to applicants individually to confirm we had received their materials.
An auto-reply would have accomplished this task much more efficiently.

## Organizing Applications

The lynchpin to bulk processing emailed-in applications was [CloudHQ's](https://cloudhq.net) GMail-to-PDF tool.
This tool allowed me to bulk select emails from inside of the GMail web client then click a "Convert to PDF" button.
After a few minutes of running behind the scenes, I was able to open up my Google Drive to find PDF files corresponding to the email thread for each applicant.
Not only were entire email conversations converted to individual PDFs, but attachments were appended on automatically (including `.doc` files).
CloudHQ provided several options to name the PDFS, including with the email address of the sender and the subject line of the email.
I ended up buying a one month subscription for $19.99 because I exceeded the free tier cap of 50 emails, but it was well worth the money.

Tip: do not rename files in Google Drive.
How ever Google Drive manages file names is a Big, Bad Lie.
I spent about an hour running on a hampster wheel where I was renaming files that were silently reverting back to their original names.
Download files from Google Drive and use some quick scripting to tidy everything up on a Real File System.
The `rename` utility command is your friend here.
I tidied up the downloaded emails to name them based on the sender's email address (e.g., `johnnyappleseed@example.com.pdf`).

I chose to distribute the application packets to reviewers as a single PDF booklet.
Organizing applications into one document obviated the need for me to host the files in a directory where they could be downloaded individually or reviewers to unzip an archive and organize the files.
Also, because we assigned reviewers contiguous subsets of applicants, it made moving from one packet to the next as easy as scrolling to the next page.

This yielded section heading pages titled as `johnyappleseedd@example.com.pdf.pdf`.

Then, after tagging `.pdf.pdf` onto the file extension of the actual packets to ensure that packets were alphabetically ordered after their corresponding section header documents, [PDFtk](https://www.pdflabs.com/tools/pdftk-the-pdf-toolkit/) made stitching the files together a breeze.

```
pdfk *.pdf cat output packet.pdf
```

Then, [a little one-job web app](https://smallpdf.com/add-page-numbers-to-pdf) slapped some page numbers on the booklet before I distributed it.

## Reviewing Applications

We reviewed candidates on
* programming experience,
* the programming project they chose to discuss,
* the effectiveness of their written statement, and
* how candidate interests aligned with workshop objectives.

We had a robust discussion among reviewers as to how to assess applicants projects in an equitable manner.
Extracurricular programming projects aren't just a function of applicants' proficiency and initiative: they also stem from conditioning, opportunity, and encouragement.
We decided to avoid appraising open-ended programming projects as inherently less than just because they took place in a classroom context.
We will certainly revisit the role of programming projects in our application process in preparation for next year's workshop, if we do hold it.

We rated candidates on each of these criteria as either
* Concern,
* Neutral,
* Adequate,
* Strong, or
* Outstanding.

This system sufficed, but in future years we might consider switching to a numerical system.
Numerical ratings avoid burdening reviewers with implicit value judgements associated with the categorical descriptors we used.
The numerical system could also allow for more granular ratings.
Several reviewers mentioned difficulty rating candidates that they felt fell between categories and that being able to mark categories "plus" or "minus" would have made the process much easier.

To ensure reviewers provided comparable ratings, we put together a rubric and discussed it as a group before performing reviews.

|             | Experience          | Statement                         | Project                                | Interest                          | Recommendation |
|-------------|---------------------|-----------------------------------|----------------------------------------|-----------------------------------|------------------|
| Concern     | red flags           | red flags or missing              | red flags                              | red flags                         | do not support   |
| Neutral     | no experience       | insufficient content or quality   | not mentioned                          | no evidence                       | neutral          |
| Adequate    | coursework only     | adequate                          | basic proficiency and initiative       | expresses interest                | support          |
| Strong      | significant project | effective, engaging, and detailed | strong proficiency and initiative      | demonstrates interest             | strongly support |
| Outstanding | exceptional         | exceptional                       | exceptional proficiency and initiative | demonstrates exceptional interest | want to mentor   |

<br/>
<br/>

For some categories, allowing the "Concern" marking seemed superfluous.
However, a few edge cases did arise where it proved a useful tool (such as applicants who described a project that appeared to be the work of others).

## Organizing Reviews

We used a Google Sheets page to organize application reviews.
We used input validation to ensure reviewers' ratings stuck to our defined categories.
This turned individual cells into drop-down boxes, which made recording reviews convenient.
We found that having record reviews on their own sheets in the document and then, once all reviews were in, having a single stakeholder take care of pasting them into the main sheet worked well.

## Selecting Participants

Our review process began with a pass through the spreadsheet to create a shortlist.
For each application packet, we had reviewers give a brief oral recap and then decided as a group whether to shortlist.
This helped reviewers double check with each other that they had similar impressions of applications packet.
It also helped the rest of us double check the reviewers' subjective interpretation of the application packet.

Then, we sorted through the shortlist to advance the strongest applications to a finalist list.
Final selections were based on alignment with individual mentors' projects.

This process took place over the course of several Zoom meetings.
The number of strong applications we had made selecting participants very difficult.
If we had the seats available, we could have filled a dramatically larger workshop with exceptional participants.

We got through the process, though, and ended up with final decisions based on broad consensus.
Although we are pleased with the outcome, the process could have been made more efficient and less stressful by explicitly defining objectives before or at the very beginning of meetings instead of just trying to work through as much of the process as possible.

## Announcing Decisions

We announced decisions by email.
We simply sorted email addresses into groups based on application decisions and sent a bcc message to each group.

* [acceptance email](#appendix-b-acceptance-email-text)
* [waitlist email](#appendix-c-waitlist-email-text)
* [unable to accept email](#appendix-d-unable-to-accept-text)

We put some effort into emphasizing our appreciation for the quality of applications we had received and the effort that went into them.
Sending emails individually (by hand or with a [mail merge](https://en.wikipedia.org/wiki/Mail_merge)) would have provided a more personal touch.
However, I would rather invest time and effort elsewhere in the process.

In future years, we might avoid waitlisting by reaching out to first-round recruits well before the decision deadline then reaching out to more recruits as needed to fill spots before sending out an unable to accept email.

## Providing Feedback to Participants

The applicant who followed up with us about how we had evaluated applications was specifically interested in feedback on how strengthen their future applications.
Their inquiry raised up a valuable point we had not considered yet: how to better provide detailed, actionable feedback to all applicants.
Applicants invest time and energy preparing their materials, so it only seems fair that we do our very best to make the application process worth their while.
If we continue the workshop next year, we should consider how to design evaluation criteria for reviewers that not just help us sort through applications but also prove useful to applicants themselves.
We might design the process from the beginning with the intent to return all reviews, including any written-out reviewer notes, to applicants.
This would require some logistical considerations, but seems within the realm of possibility with the assistance of some clever scripting.

## Let's Chat!

What nuts and bolts have worked well in your efforts to recruit and review applications for academic positions?
Not so well?

I started a twitter thread (right below) so we can chat :phone: :phone: :phone:
... I know y'all got stories!!!

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">WAVES workshop call had an amazing response: 92 applications in all 🌟💻😸<br><br>we&#39;re proud of the crew we assembled but (as always) things could have gone a little smoother behind the scenes... 🙄 🤷<br><br>blog post on Logistical Lessons Learned 💪<a href="https://t.co/zH0aSdNs9U">https://t.co/zH0aSdNs9U</a></p>&mdash; Matthew A Moreno (@MorenoMatthewA) <a href="https://twitter.com/MorenoMatthewA/status/1262152205924134913?ref_src=twsrc%5Etfw">May 17, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

## Appendix A: ASCII Call for Participants

```
  Workshop for Avida-ED Software Development (WAVES)
======================================================


Call for Participants
---------------------

We are looking to recruit five to ten participants for a ten-week, funded,
full-time, fully-remote software development workshop between May 25, 2020 and
July 31, 2020. To accommodate multiple U.S. time zones, all group meetings will
be held over videoconference between 1pm and 4pm EST (GMT-4).

A $6,000 stipend will be disbursed to participants in five bi-weekly
installments of $1,200. All U.S. citizens/permanent residents are eligible to
apply, as are international students already enrolled at Michigan State
University. The workshop will be aimed at upper-level undergraduates in
computer science, but graduate students or other early-career computer
scientists are also welcome to apply.

We are seeking participants with prior practical experience in computer
science: writing and running software of some sort. Prior experience with C++
and/or JavaScript is expected, but not strictly required. We especially
encourage applications from members of underrepresented groups in computer
science.


Workshop Information
--------------------

The WAVES workshop is organized in conjunction with the Avida-ED project.
Avida-ED extends the full-fledged Avida software, originally developed for
digital evolution research, as a freely-available, interactive web application.
This web application enables laboratory activities that teach evolution through
experiments with self-replicating computer programs.

The goal of the workshop is four-fold:
1. to help participants advance their careers by skillbuilding through hands-on
   C++ and/or JavaScript software development in an academic setting,
2. to catalyze effective science communication and science pedagogy by helping
   participants develop the know-how to showcase their research through
interactive web applications,
3. to jumpstart software development on web framework and core digital
   evolution tools in support of the next version of the Avida-ED scientific
and educational software, and
4. to yield software that broadly enriches the digital evolution, scientific,
   education, and open-source communities.

Each WAVES workshop participant will collaborate with an assigned mentor on a
software development project related to Avida-ED or the underlying scientific
software tools that power it. We will help participants choose projects based
on their personal interests and background during the first week of the
workshop. To demonstrate their software, participants will build their own
prototype scientific web application/mini research project or contribute to an
existing web application/research project.


Applications
------------

Applications should consist of:
1. a curriculum vitae or resume,
2. a brief (appox. 500 to 1000 words) statement that describes
   a. your personal background and career goals,
   b. your interest in the program, and
   c. an interesting coding project you’ve tackled.
	  * in any setting: school, hackathon, personal project, research, work,
	    etc.
	  * as possible, link us to the code, the deployment, the project website,
	    a writeup, and/or presentation!
3. and, optionally, two references for your coding ability (include name,
   email, and relationship).

Applications should be submitted to avida-waves@googlegroups.com with the
subject line “WAVES Application” no later than May 4, 2020.

We will announce participant selection no later than May 11, 2020.


Further Information
-------------------
Example project descriptions, a listing of workshop organizers and project
mentors, and more details about workshop logistics are available at
https://mmore500.com/waves.
```

## Appendix B: Acceptance Email Text

> Thank you for applying to become a participant in the WAVES workshop.
> We are delighted to inform you that you have been accepted as a workshop participant.
> We received 92 applications, most of which were excellent, and needed to make tough decisions.
> You are one of 19 participants who we have offered a position in the workshop.
>
> Please let us know as soon as possible --- at the latest by Friday, May 15 --- if you accept this offer; if not we want to be able to offer your place to one of the other applicants.
>
> The workshop will officially start Tuesday, May 26th with a welcome session and orientation from 1pm to 4pm EST.
> After we hear back from you, we will follow up in the next couple of weeks to provide additional details about the workshop and ask for information in order to set up computer accounts and your stipend.
>
> Congratulations and welcome to WAVES!


## Appendix C: Waitlist Email Text

> Thank you for applying to become a participant in the WAVES workshop.
> At this time we cannot yet admit you as a workshop participant.
> However, you did make the short list and we have put you on our waiting list in case we have someone else decline or are able to further grow the workshop.
> We will update you by Monday, May 18 about whether we are able to add you.
> If you are no longer interested in participating, please let us know as soon as possible.
>
> We received 92 applications, many more than the workshop capacity.
> In the end, we had to make tough decisions.
> You had one of the strongest applications and we really want to do our best to include you.


## Appendix D: Unable to Accept Text

> Thank you for applying to become a participant in the WAVES workshop.  We appreciate the time and energy you put in to applying, but unfortunately we are not able to offer you a place in the workshop. We received 92 applications, many more than the workshop capacity.  In the end, we had to make tough decisions and were unable to accept many exceptionally talented participants.
>
> We are tentatively planning to hold another WAVES workshop next summer. If you are interested in receiving our call for participants next year, click here to add your name to our email list. Thank you!
