---
layout: default
title: Welcome
permalink: /
---

<style type="text/css">
.container{
    display: flex;
}
.fixed{

}
.flex-item{
    flex-grow: 0.5;
}
</style>

<script type="text/javascript">
images_dictionary={
     dogs:["/resources/welcome_dogs.jpg","dogwalker on the waterfront <br /> Hoboken, NJ summer 2016"],
     ferns1:["/resources/welcome_ferns1.jpg","<i>Athyrium filix-femina</i> near Peavey Arboretum <br />  Corvallis, OR spring 2016"],
     ferns2:["/resources/welcome_ferns2.jpg", "<i>Athyrium filix-femina</i> near Peavey Arboretum <br />  Corvallis, OR spring 2016"],
     flowers:["/resources/welcome_flowers.jpg", "<i>Penstemon strictus</i> at Chip Ross park <br /> Corvallis, OR summer 2016"],
     lamppost:["/resources/welcome_lamppost.jpg", "sunset at NW Mirador Pl<br /> Corvallis, OR summer 2016"],
     road:["/resources/welcome_road.jpg", "NW Soap Creek Road <br /> Corvallis, OR summer 2016"],
     strawberries:["/resources/welcome_strawberries.jpg", "<i>Fragaria × ananassa</i> at USDA ARS HCRL<br /> Corvallis, OR summer 2016"],
     sunrisemoonset:["/resources/welcome_sunrisemoonset.jpg", "moonset at sunrise near Chip Ross park <br /> Corvallis, OR summer 2016"],
     thistle:["/resources/welcome_thistle.jpg", "<i>Cirsium vulgare</i> at Owens Farm <br />  Corvallis, OR summer 2016"]
};

  var image_keys = [
    "dogs",
    "ferns1",
    "ferns2",
    "flowers",
    "lamppost",
    "road",
    "strawberries",
    "sunrisemoonset",
    "thistle"
  ];

  function getImageHTML() {
    var html_code = '<img src=\"';
    var randomIndex = Math.floor(Math.random() * image_keys.length);
    html_code += images_dictionary[image_keys[randomIndex]][0];
    html_code += '\"  style=\"max-width:100vw; max-height:60vh;\" alt=\"have you tried ~refreshing~?!\"/>';
    html_code += "<br /><span align=\"left;\">"
    html_code += images_dictionary[image_keys[randomIndex]][1];
    html_code += "</span>"

    return html_code;
  }
</script>

<div class="container">
  <div class="flex-item">
  </div>

  <div class="fixed">
  <script type="text/javascript">
    document.write(getImageHTML());
  </script>
  </div>

  <div class="flex-item">
  </div>
</div>
