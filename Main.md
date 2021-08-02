# Narrative_Vizualization Project
CS 513 Narrative Visualization Project


<html>
<script src='https://d3js.org/d3.v5.min.js'></script>
<style> circle {fill: lightblue; stroke: black;} </style>
<body onload='init()'>
<svg width=300 height=300>
</svg>
<script>
async function init() {

scaleL = d3.scaleLog().domain([10,150]).range([0,200]) 
scaleY = d3.scaleLog().domain([10,150]).range([200,0]) 
const data = await d3.csv(
        'https://flunky.github.io/cars2017.csv');
    d3.select("svg")
      .append("g")
        .attr("transform","translate(50,50)")
      .selectAll('circle')
      .data(data)
      .enter()
      .append('circle')
         .attr("cx", function(d,i) { return scaleL(d["AverageCityMPG"]); })
         .attr("cy", function(d,i) { return 200 -
                                         scaleL(d["AverageHighwayMPG"]);})
         .attr("r", function(d,i) { return (2 + +d["EngineCylinders"]);});

d3.select("svg").append("g")
   .attr("transform","translate(50,50)")
   .attr("fill","none")
   .attr("font-size","10")
   .attr("font-family","sans-serif")
   .attr("text-anchor","end")
.call(d3.axisLeft(scaleY).tickFormat(d3.format("~s")).tickValues([10,20,50,100]));

d3.select("svg").append("g")
   .attr("transform","translate(50,250)")
   .attr("fill","none")
   .attr("font-size","10")
   .attr("font-family","sans-serif")
   .attr("text-anchor","end")
   .call(d3.axisBottom(scaleL).tickFormat(d3.format("~s")).tickValues([10,20,50,100]));
  
  }
</script>
</body>
</html>
  
  
  

  

