---
layout: post
title: "Example"
modified:
categories: blog
excerpt:
date: 2015-08-10T08:08:50-04:00
---

[MathJax](http://www.mathjax.org/) is a simple way of including Tex/LaTex/MathML based mathematics in HTML webpages. To get up and running you need to include the MathJax script in the header of your github pages page, and then write some maths. For LaTex, there are two delimiters you need to know about, one for block or displayed mathematics `\[ ... \]`, and the other for inline mathematics `\( ... \)`.

## Usage

To enable MathJax support be sure Kramdown is your Markdown flavor of choice and MathJax is set to true in your `_config.yml` file.

<!-- <iframe src="http://bl.ocks.org/mbostock/raw/4061502/0a200ddf998aa75dfdb1ff32e16b680a15e5cb01/" width="600" height="400" marginwidth="0" marginheight="0" scrolling="no"></iframe> -->

<!-- <script src="http://d3js.org/d3.v3.min.js"></script> -->
<!--
<style>

div.example {
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
}

.box {
  font: 10px sans-serif;
}

.box line,
.box rect,
.box circle {
  fill: #fff;
  stroke: #000;
  stroke-width: 1.5px;
}

.box .center {
  stroke-dasharray: 3,3;
}

.box .outlier {
  fill: none;
  stroke: #ccc;
}

</style>

<script>

var margin = {top: 10, right: 50, bottom: 20, left: 50},
    width = 120 - margin.left - margin.right,
    height = 500 - margin.top - margin.bottom;

var min = Infinity,
    max = -Infinity;

var chart = d3.box()
    .whiskers(iqr(1.5))
    .width(width)
    .height(height);

d3.csv("/morley.csv", function(error, csv) {
  var data = [];

  csv.forEach(function(x) {
    var e = Math.floor(x.Expt - 1),
        r = Math.floor(x.Run - 1),
        s = Math.floor(x.Speed),
        d = data[e];
    if (!d) d = data[e] = [s];
    else d.push(s);
    if (s > max) max = s;
    if (s < min) min = s;
  });

  chart.domain([min, max]);

  var svg = d3.select("div#example").selectAll("svg")
      .data(data)
    .enter().append("svg")
      .attr("class", "box")
      .attr("width", width + margin.left + margin.right)
      .attr("height", height + margin.bottom + margin.top)
    .append("g")
      .attr("transform", "translate(" + margin.left + "," + margin.top + ")")
      .call(chart);

  setInterval(function() {
    svg.datum(randomize).call(chart.duration(1000));
  }, 2000);
});

function randomize(d) {
  if (!d.randomizer) d.randomizer = randomizer(d);
  return d.map(d.randomizer);
}

function randomizer(d) {
  var k = d3.max(d) * .02;
  return function(d) {
    return Math.max(min, Math.min(max, d + k * (Math.random() - .5)));
  };
}

// Returns a function to compute the interquartile range.
function iqr(k) {
  return function(d, i) {
    var q1 = d.quartiles[0],
        q3 = d.quartiles[2],
        iqr = (q3 - q1) * k,
        i = -1,
        j = d.length;
    while (d[++i] < q1 - iqr);
    while (d[--j] > q3 + iqr);
    return [i, j];
  };
}


<div id="example"></div>
-->

<select>
<option value="div0" selected>resnet-preact</option>
<option value="div1">resnet-preact-1x1</option>
<option value="div2">resnet</option>
</select>

<div id="wrap">
  <div id="div0" class="svg"></div>
  <div id="div1" class="svg"></div>
  <div id="div2" class="svg"></div>
</div>

<style>
#wrap {
  height: 200px;
  text-align: center;
}

#div0, #div1, #div2 {
  height: 0px;
  text-align: center;
}

#div1, #div2 {
  display: none;
}
</style>

<script src="https://d3js.org/d3.v4.js"></script>

<script>

var svg0 = "/resnet-preact.svg";
var svg1 = "/resnet-preact-1x1.svg";
var svg2 = "/resnet.svg";
var div0 = d3.select("div#div0");
var div1 = d3.select("div#div1");
var div2 = d3.select("div#div2");

var createSvg = function(div, dataset) {
    d3.xml(dataset).mimeType("image/svg+xml").get(function(error, xml) {
      if(error) throw error;
      div.node().append(xml.documentElement);
    });
}

var prev = "div0";
d3.select("select").on("change", function() {
    var curr = d3.select("select").property("value");
    var div_show = d3.select('#' + curr);
    var div_hide = d3.select('#' + prev);
    prev = curr;
    div_hide.style('display', 'inherit');
    div_show.style('display', 'inherit');
    div_hide.select('svg')
        .transition()
        .duration(200)
        .style('opacity', 0);
    div_show.select('svg')
        .transition()
        .duration(200)
        .style('opacity', 1);
  });

createSvg(div0, svg0);
createSvg(div1, svg1);
createSvg(div2, svg2);

</script>

<!--

$(function() {
  $('#svg1').slideDown();
  $('select').change(function() {
      var val = $(this).val();
      if (val) {
          $('div.svg:not(#svg' + val + ')').slideUp();
          $('#svg' + val).slideDown();
      }
  });
});

-->

<!--
<script>

var one = "/resnet-preact-1x1.svg";
var two = "/resnet-preact.svg";
var div1 = d3.select("div#example1");
var div2 = d3.select("div#example2");

var createSvg = function(div, dataset) {
    d3.xml(dataset).mimeType("image/svg+xml").get(function(error, xml) {
      if(error) throw error;
      div.node().append(xml.documentElement);
      console.log(dataset + ' LOADED!!!!');
    });
}

update = function(div_show, div_hide) {
  div_hide.style('display', 'inherit')
  div_show.style('display', 'inherit');
  div_hide.select('svg')
      .transition()
      .duration(100)
      .style("opacity", 0)
      .style("display", "none");
  div_show.select('svg')
      .transition()
      .duration(100)
      .style("opacity", 1)
      .style("display", "block");
}

createSvg(div1, one);
createSvg(div2, two);

d3.select("#one").on("click", function() { update(div1, div2); });
d3.select("#two").on("click", function() { update(div2, div1); });

</script>
-->

<!--
      div_svg.node()
          .append(xml.documentElement
                     .transition()
                     .style("opacity", 0)
                     .duration(200)
                     .style("opacity", 1));
-->

<!--
<style>

.node {
  stroke: #fff;
  stroke-width: 1.5px;
}

.node .selected {
  stroke: red;
}

.link {
  stroke: #999;
}

.brush .extent {
  fill-opacity: .1;
  stroke: #fff;
  shape-rendering: crispEdges;
}
</style>

<script src="//d3js.org/d3.v3.min.js"></script>
<script src="http://bl.ocks.org/mbostock/raw/4061502/0a200ddf998aa75dfdb1ff32e16b680a15e5cb01/box.js"></script>
<script>
var width = 960,
    height = 500,
    shiftKey;

var svg = d3.select("div#example2")
    .attr("tabindex", 1)
    .on("keydown.brush", keydown)
    .on("keyup.brush", keyup)
    .each(function() { this.focus(); })
  .append("svg")
    .attr("width", width)
    .attr("height", height);

var link = svg.append("g")
    .attr("class", "link")
  .selectAll("path");

var brush = svg.append("g")
    .datum(function() { return {selected: false, previouslySelected: false}; })
    .attr("class", "brush");

var node = svg.append("g")
    .attr("class", "node")
  .selectAll("circle");

d3.json("/graph.json", function(error, graph) {
  console.log(graph)
  graph.links.forEach(function(d) {
    console.log(d)
    d.source = graph.nodes[d.source];
    d.target = graph.nodes[d.target];
  });

  link = link.data(graph.links).enter().append("path")
      .attr("x1", function(d) { return d.source.x; })
      .attr("y1", function(d) { return d.source.y; })
      .attr("x2", function(d) { return d.target.x; })
      .attr("y2", function(d) { return d.target.y; });

  brush.call(d3.svg.brush()
        .x(d3.scale.identity().domain([0, width]))
        .y(d3.scale.identity().domain([0, height]))
        .on("brushstart", function(d) {
          node.each(function(d) { d.previouslySelected = shiftKey && d.selected; });
        })
        .on("brush", function() {
          var extent = d3.event.target.extent();
          node.classed("selected", function(d) {
            return d.selected = d.previouslySelected ^
                (extent[0][0] <= d.x && d.x < extent[1][0]
                && extent[0][1] <= d.y && d.y < extent[1][1]);
          });
        })
        .on("brushend", function() {
          d3.event.target.clear();
          d3.select(this).call(d3.event.target);
        }));

  node = node.data(graph.nodes).enter().append("circle")
      .attr("r", 4)
      .attr("cx", function(d) { return d.x; })
      .attr("cy", function(d) { return d.y; })
      .on("mousedown", function(d) {
        if (!d.selected) { // Don't deselect on shift-drag.
          if (!shiftKey) node.classed("selected", function(p) { return p.selected = d === p; });
          else d3.select(this).classed("selected", d.selected = true);
        }
      })
      .on("mouseup", function(d) {
        if (d.selected && shiftKey) d3.select(this).classed("selected", d.selected = false);
      })
      .call(d3.behavior.drag()
        .on("drag", function(d) { nudge(d3.event.dx, d3.event.dy); }));
});

function nudge(dx, dy) {
  node.filter(function(d) { return d.selected; })
      .attr("cx", function(d) { return d.x += dx; })
      .attr("cy", function(d) { return d.y += dy; })

  link.filter(function(d) { return d.source.selected; })
      .attr("x1", function(d) { return d.source.x; })
      .attr("y1", function(d) { return d.source.y; });

  link.filter(function(d) { return d.target.selected; })
      .attr("x2", function(d) { return d.target.x; })
      .attr("y2", function(d) { return d.target.y; });

  d3.event.preventDefault();
}

function keydown() {
  if (!d3.event.metaKey) switch (d3.event.keyCode) {
    case 38: nudge( 0, -1); break; // UP
    case 40: nudge( 0, +1); break; // DOWN
    case 37: nudge(-1,  0); break; // LEFT
    case 39: nudge(+1,  0); break; // RIGHT
  }
  shiftKey = d3.event.shiftKey || d3.event.metaKey;
}

function keyup() {
  shiftKey = d3.event.shiftKey || d3.event.metaKey;
}

</script>
-->


```yaml
markdown: kramdown
mathjax: true
```

```
Here is an example MathJax inline rendering \\( 1/x^{2} \\), and here is a block rendering:
\\[ \frac{1}{n^{2}} \\]
```

Here is an example MathJax inline rendering \\( 1/x^{2} \\), and here is a block rendering:
\\[ \frac{1}{n^{2}} \\]

\\[ \sum_{i=0}^n i^2 = \frac{(n^2+n)(2n+1)}{6} \\]

The only thing to look out for is the escaping of the backslash when using markdown, so the delimiters become `\\[ ... \\]` and `\\( ... \\)` for inline and block maths respectively.
