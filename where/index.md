---
layout: page
status: publish
published: true
title: Where
author:
  display_name: abarna
date: '2012-02-05 23:05:04 -0800'
date_gmt: '2012-02-06 09:05:04 -0800'
categories: []
tags: []
comments: []
---
    {% for member in site.static_files %}
    {{ member.path }}
    {% endfor %}
<div class="map_container">
</div>
<script src="//code.jquery.com/jquery-1.11.3.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/d3/3.5.6/d3.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/topojson/1.6.19/topojson.min.js"></script>
<script>
var width = 960,
    height = 650;

  var projection = d3.geo.mercator()
  .scale(153)
  .translate([width / 2, height / 2])
.rotate([160,0])
  .precision(.1);

var path = d3.geo.path()
  .projection(projection);

  var graticule = d3.geo.graticule();

  var svg = d3.select(".map_container").append("svg")
  .attr("preserveAspectRatio", "xMinYMin meet")
  .attr("viewBox", "0 0 " + width + " " + height );

  var features = svg.append("g")

  features.append("path")
.datum(graticule)
  .attr("class", "graticule")
  .attr("d", path);

  d3.json("/where/data/world-50m.json", function(error, world) {
      features.insert("path", ".graticule")
      .datum(topojson.feature(world, world.objects.land))
      .attr("class", "land")
      .attr("d", path);
      });

load_track("/where/data/2010-CCE2.geojson", "cce2");
//load_track("/static/data/cruises/KM1102_1min.r2rnav.bz2.json", "exits2");
//load_track("/static/data/cruises/MV1305_1min.r2rnav.bz2.json", "p02_1");
//load_track("/static/data/cruises/MV1306_1min.r2rnav.bz2.json", "p02_2");
//load_track("/static/data/cruises/NBP1403.nav.bz2.json", "p16s");

$(svg).width("100%");
$(".map_container").height($(".map_container").width() * 0.6777);
$(window).resize(function(){
    $(".map_container").height($(".map_container").width() * 0.6777);
    });

function load_track(f_path, t_class){
d3.json(f_path, function(collection) {
    tracks = features.selectAll()
    .data(collection.features).enter().append("g")
    .attr("class", t_class);
    tracks.append("svg:path")
    .attr("d", path);
    });
}

function zoom_to(x, y, k) {
  x = -x;
  y = -y;
  k = k * 153;
  projection.rotate([x,y])
    .scale(k);
  features.selectAll("path").transition()
    .duration(10)
    .attr("d", path);
}

function show_all(){
    d3.select(".cce2").transition().duration(1000).style("stroke-width", "3px").style("stroke", "#000");
    d3.select(".exits2").transition().duration(1000).style("stroke-width", "3px").style("stroke", "#000");
    d3.select(".p02_1").transition().duration(1000).style("stroke-width", "3px").style("stroke", "#000");
    d3.select(".p02_2").transition().duration(1000).style("stroke-width", "3px").style("stroke", "#000");
    d3.select(".p16s").transition().duration(1000).style("stroke-width", "3px").style("stroke", "#000");
}
function hide_all_but(cls){
  if (cls != "cce2"){
    d3.select(".cce2").transition().duration(1000).style("stroke-width", "0px").style("stroke", "#000");
  }
  if (cls != "exits2"){
    d3.select(".exits2").transition().duration(1000).style("stroke-width", "0px").style("stroke", "#000");
  }
  if (cls != "p02_1"){
    d3.select(".p02_1").transition().duration(1000).style("stroke-width", "0px").style("stroke", "#000");
  }
  if (cls != "p02_2"){
    d3.select(".p02_2").transition().duration(1000).style("stroke-width", "0px").style("stroke", "#000");
  }
  if (cls != "p16s"){
    d3.select(".p16s").transition().duration(1000).style("stroke-width", "0px").style("stroke", "#000");
  }
}

function show_full_map(){
  //zoom_to(160,0,1);
  svg.transition().duration(1000).attr("viewBox", "0 0 " + width + " " + height );
  show_all();
}
function show_p02_1(){
  //zoom_to(166,30,5);
  svg.transition().duration(1000).attr("viewBox", "270 180 225 152" );
  d3.select(".p02_1").transition().duration(1000).style("stroke-width", "1px").style("stroke", "#00f");
  hide_all_but("p02_1");
}
function show_p02_2(){
  //zoom_to(166,30,5);
  svg.transition().duration(1000).attr("viewBox", "420 180 225 152" );
  d3.select(".p02_2").transition().duration(1000).style("stroke-width", "1px").style("stroke", "#00f");
  hide_all_but("p02_2");
}
function show_cce2(){
  //zoom_to(-118,33,34);
  svg.transition().duration(1000).attr("viewBox", "550 205 73 50" );
  d3.select(".cce2").transition().duration(1000).style("stroke-width", "0.2px").style("stroke", "#00f");
  hide_all_but("cce2");
}
function show_exits2(){
  //zoom_to(-162,20,25);
  svg.transition().duration(1000).attr("viewBox", "430 250 73 50" );
  d3.select(".exits2").transition().duration(1000).style("stroke-width", "0.2px").style("stroke", "#00f");
  hide_all_but("exits2");
}
function show_p16s(){
  //zoom_to(166,30,5);
  svg.transition().duration(1000).attr("viewBox", "270 350 400 270" );
  d3.select(".p16s").transition().duration(1000).style("stroke-width", "2px").style("stroke", "#00f");
  hide_all_but("p16s");
}
</script>
