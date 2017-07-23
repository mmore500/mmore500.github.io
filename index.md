---
layout: widecontent
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

     thistle:["/resources/welcome_thistle.jpg", "<i>Cirsium vulgare</i> at Owens Farm <br />  Corvallis, OR summer 2016"],

     beachsunset:["/resources/welcome_beachsunset.jpg", "an oil rig at sunset <br />  Santa Barbara, CA fall 2016"],

     grain:["/resources/welcome_grain.jpg", "sunset on Lester Ave <br />  Corvallis, OR summer 2016"],

     island:["/resources/welcome_island.jpg", "the view from Cook's Look <br />  Lizard Island National Park, AUS winter 2016"],

     islandfern:["/resources/welcome_islandfern.jpg", "life on the island <br />  Lizard Island National Park, AUS winter 2016"],

     jungle:["/resources/welcome_jungle.jpg", "life in the jungle <br /> Mount Hypipamee National Park, AUS winter 2016"],

     nyc:["/resources/welcome_nyc.jpg", "New York City skyline <br />  Hoboken, NJ summer 2016"],

     peavey:["/resources/welcome_peavey.jpg", "sunrise at Peavey Arboretum <br />  Corvallis, OR spring 2017"],

     serratedleaves:["/resources/welcome_serratedleaves.jpg", "serrated leaves at Peavey Arboretum <br />  Corvallis, OR summer 2016"],

     spiderweb:["/resources/welcome_spiderweb.jpg", "spider web at the University of Puget Sound <br />  Tacoma, WA fall 2016"],

     bee:["/resources/welcome_bee.jpg", "<i>Bombus pennsylvanicus</i> at work <br />  Corvallis, OR summer 2016"],

     moss:["/resources/welcome_moss.jpg", "mosssy branch on Vineyard Mountain <br />  Corvallis, OR spring 2017"],

     translucent:["/resources/welcome_translucent.jpg", "translucent leaf at sunset <br />  Corvallis, OR winter 2016"],

     window:["/resources/welcome_window.jpg", "dog in the window <br />  Columbus, OH summer 2016"],

     airport:["/resources/welcome_airport.jpg", "sunset at Hartsfield-Jackson Atlanta International Airport <br /> Atlanta, GA winter 2017"],

     firehydrant:["/resources/welcome_firehydrant.jpg", "broken fire hydrant <br /> Newark, NJ summer 2016"],

     foliage:["/resources/welcome_foliage.jpg", "foliage at Peavey Arboretum <br /> Corvallis, OR spring 2016"],

     ladybug:["/resources/welcome_ladybug.jpg", "ladybug in the garden <br /> Corvallis, OR spring 2016"],

     lizardsunset:["/resources/welcome_lizardsunset.jpg", "inbetween day and night from Cook's Look <br /> Lizard Island National Park, AUS winter 2016"],

     oppfern:["/resources/welcome_oppfern.jpg", "fern near Oppenheimer cafe <br /> Tacoma, WA spring 2017"],

     plantlife:["/resources/welcome_plantlife.jpg", "spring life near theme row <br /> Tacoma, WA spring 2017"],

     puddles:["/resources/welcome_puddles.jpg", "puddle at sunset <br /> Tacoma, WA spring 2017"],

     snake:["/resources/welcome_snake.jpg", "snake near Chip Ross Park <br /> Corvallis, OR summer 2016"],

     waterfallleaf:["/resources/welcome_waterfallleaf.jpg", "leaves and waterfall near Waldo Lake <br /> Willamette National Forest, OR summer 2015"]

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
    "thistle",
    "beachsunset",
    "grain",
    "island",
    "islandfern",
    "jungle",
    "nyc",
    "peavey",
    "serratedleaves",
    "spiderweb",
    "bee",
    "moss",
    "translucent",
    "window",
    "airport",
    "firehydrant",
    "foliage",
    "ladybug",
    "lizardsunset",
    "oppfern",
    "plantlife",
    "puddles",
    "snake",
    "waterfallleaf"
  ];

  function getImageHTML() {
    var html_code = '<img src=\"';
    var randomIndex = Math.floor(Math.random() * image_keys.length);
    html_code += images_dictionary[image_keys[randomIndex]][0];
    html_code += '\"  style=\"max-width:90vw; max-height:60vh;\" alt=\"have you tried ~refreshing~?!\"/>';
    html_code += "<br /><p align=\"left\">"
    html_code += images_dictionary[image_keys[randomIndex]][1];
    html_code += "</p>"

    return html_code;
  }
</script>

<div style="text-align:center">
  <div style="display: inline-block;">
  <script type="text/javascript">
    document.write(getImageHTML());
  </script>
  </div>
</div>
