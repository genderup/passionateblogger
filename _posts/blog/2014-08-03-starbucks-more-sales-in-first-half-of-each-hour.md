---
layout: post
title:  "Starbucks: More Sales In First Half Of Each Hour"
date:   2014-07-27 15:54:21
categories: 
- blog
- culture
---

<img class="image-center" src="/starbucks2.png">

 <!--more--> 

How does Starbucks measure success?  

According to <a href="https://dl.dropboxusercontent.com/u/10328969/Sales%20By%20Period%20Daily%20Report.pdf" target="_blank">its</a><i> Sales By Period Daily Report</i>, Starbucks breaks its day down into half hour periods and calculates the number of customers (i.e. transactions) and total sales for each half hour. Naturally, the period with the greatest number of transactions might not be the period with the highest total sales, and that's how it was Wednesday July 30, 2014 at one of the local Starbucks in my neighbourhood.  

As you can see on the first chart, the period ending at 9:30 a.m. had the greatest number of customers (47), but the total sales were lower than the period ending at 10:30 a.m. (Sales for each period become visible by moving the mouse over the graph, or compare the first graph with the second directly below it.) The total average sale for the period ending at 9:30 a.m. is $3.67 while the average sale for the period ending at 10:30 a.m (when customers are perhaps a little  hungrier) is $5.26. 

<div id="graph">

</div>




<div id="graph2">

</div>


The most interesting takeaway from the report is that, during business hours, there is less traffic in the store during the second half of each hour. From 8 to 8:30 a.m., there were 32 customers in the store, but only 24 from 8:30 to 9 a.m.  From 9 to 9:30 a.m. there were 47 customers in the store, but only 27 from 9:30 to 10 a.m.  And from 10 to 10:30 a.m., there were 40 customers in the store, but only 29 from 10:30 to 11 a.m. 

Is this an anomaly or do people generally prefer to get coffee early in the hour to then <del> spend </del> waste the whole hour consuming it?  What insight would this type of data on a larger scale into workplace productivity?

Starbucks uses customer count to determine when to open and close as well as to decide how many staff to have on the floor at any given time.  The Starbucks where <a href="https://dl.dropboxusercontent.com/u/10328969/Sales%20By%20Period%20Daily%20Report.pdf" target="_blank">this</a>  report comes from has two employees open the store at 5:30 a.m. From 7:30 to 11:30 a.m. there are four employees in the store, for a total of 33 staff hours for the periods covered by the report.  Total sales for the period were $1384.54, meaning that each staff hour generated $41.93 in sales.   <a href="http://www.glassdoor.ca/Salary/Starbucks-Toronto-Salaries-EI_IE2202.0,9_IL.10,17_IM976.htm">Glassdoor</a> has Starbucks baristas in Toronto earning $10.86 per hour, with shift supervisors earning a little more ($11.89 per hour) but minimum wage rose to $11 in May, 2014. At the most, it would likely cost this Starbucks around $396 (33 times $12) in wages to generate the $1384.54 in sales. 

Retail space is relatively expensive at this location (in North Toronto). According to several landlords on the street, rents (with taxes and insurance and utilities) vary between $5,000 and $7,000 per month. As Starbucks has one of the larger and best locations (in terms of visibility), I assume it would be $7000 per month, meaning it would cost about $233 per day. 

By 11:30 a.m. on a Wednesday July 30, 2014, my local Starbucks had already generated $1384.54 in total sales, paid $396 in wages, and covered its basic property costs for the day, leaving it approximately $755 to cover the cost of everything else (coffee, cups, wifi, corporate costs etc). It was also open to 11 p.m. during the summer, leaving it another 11.5 hours for more sales and syrupy sweet service.


<pre id="csvdata">
zeit,count,total,avg
5:30,0,0,0
6:00,14,41.1, $2.94 
6:30,19,52, $2.74 
7:00,21,74, $3.52 
7:30,28,143.25, $5.12 
8:00,30,141.3, $4.71 
8:30,32,124.28, $3.88 
9:00,24,74.8, $3.12 
9:30,47,172.35, $3.67 
10:00,27,119.77, $4.44 
10:30,40,210.44, $5.26 
11:00,29,150.95, $5.21 
11:30,14,80.3, $5.74 
</pre>



<style> 

/* set the CSS */

 
/*body { font: 12px Arial;}*/
#csvdata {
    display: none;
}

#graph2{
    font: 12px Arial;
    width:800px;
    height:260px;
}
 
#graph{
    font: 12px Arial;
    width:800px;
    height:260px;
}
path { 
    stroke: steelblue;
    stroke-width: 2;
    fill: none;
}
 
.axis path,
.axis line {
    fill: none;
    stroke: grey;
    stroke-width: 1;
    shape-rendering: crispEdges;
}
 
</style>
<script src="http://d3js.org/d3.v3.min.js"></script>


 
<script>
 
 (function() {
// Set the dimensions of the canvas / graph
var margin = {top: 30, right: 100, bottom: 50, left: 40},
    width = 800 - margin.left - margin.right,
    height = 270 - margin.top - margin.bottom;
 
// Parse the date / time
var parseDate = d3.time.format("%H:%M").parse,
    formatDate = d3.time.format("%H:%M"),
    bisectDate = d3.bisector(function(d) { return d.zeit; }).left;
 
// Set the ranges
var x = d3.time.scale().range([0, width]);
var y = d3.scale.linear().range([height, 0]);
 
// Define the axes
var xAxis = d3.svg.axis().scale(x)
    .orient("bottom").ticks(12);
 
var yAxis = d3.svg.axis().scale(y)
    .orient("left").ticks(12);
 
// Define the line
var valueline = d3.svg.line()
    .x(function(d) { return x(d.zeit); })
    .y(function(d) { return y(d.count); });

// var valueline2 = d3.svg.line()
//     .x(function(d) { return x(d.zeit); })
//     .y(function(d) { return y(d.total); });
    
// Adds the svg canvas
var svg = d3.select("#graph")
    .append("svg")
        .attr("width", width + margin.left + margin.right)
        .attr("height", height + margin.top + margin.bottom)
    .append("g")
        .attr("transform", 
              "translate(" + margin.left + "," + margin.top + ")");
 
var lineSvg = svg.append("g"); 
 
var focus = svg.append("g") 
    .style("display", "none");
 
// Get the data
var raw = d3.select("#csvdata").text();
console.log("raw vag",raw);
var data = d3.csv.parse(raw);
// console.log("bata after parse", bata);
// // console.log("parsed", parsed);
// d3.csv("https://dl.dropboxusercontent.com/u/10328969/report.csv", function(error, data) {
// // d3.csv.parse(raw, function(error, data) {
// console.log("data", data);
    data.forEach(function(d) {
         // console.log("data in raw", d);
        d.zeit = parseDate(d.zeit);
        d.total = +d.total;
        d.count = d.count;
    });
 
    // Scale the range of the data
    x.domain(d3.extent(data, function(d) { return d.zeit; }));
    y.domain([0, d3.max(data, function(d) { 

        return d.count; 
        // return  Math.max(d.count, d.total);

    })]);
 
    // Add the valueline path.
    lineSvg.append("path")
        .attr("class", "line")
        .attr("d", valueline(data));

    // lineSvg.append("path")
    //     .attr("class", "line")
    //     .style("stroke", "red")
    //     .attr("d", valueline2(data));
 
    // Add the X Axis
    svg.append("g")
        .attr("class", "x axis")
        .attr("transform", "translate(0," + height + ")")
        .call(xAxis);
       
 
    // Add the Y Axis
    svg.append("g")
        .attr("class", "y axis")
        .call(yAxis);

    svg.append("text")             // text label for the x axis
        .attr("x", width /2 )
        .attr("y",  height + margin.bottom )
        .style("text-anchor", "middle")
        .text("Time Period");
    svg.append("text")
        .attr("x", (width / 2))             
        .attr("y", 0 - (margin.top / 2))
        .attr("text-anchor", "middle")  
        .style("font-size", "16px") 
        .style("text-decoration", "underline")  
        .text("Time Period vs Customer Count - Starbucks Sales By Period Daily Report");

    svg.append("text")
        .attr("transform", "rotate(-90)")     
        .attr("y", 0 - margin.left)
        .attr("x", 0 - (height / 2))
        .attr("dy", "1em")
        .style("text-anchor", "middle")
        .text("Customer Count");
 
   // append the x line
    focus.append("line")
        .attr("class", "x")
        .style("stroke", "blue")
        .style("stroke-dasharray", "3,3")
        .style("opacity", 0.5)
        .attr("y1", 0)
        .attr("y2", height);
 
    // append the y line
    focus.append("line")
        .attr("class", "y")
        .style("stroke", "blue")
        .style("stroke-dasharray", "3,3")
        .style("opacity", 0.5)
        .attr("x1", width)
        .attr("x2", width);
 
    // append the circle at the intersection
    focus.append("circle")
        .attr("class", "y")
        .style("fill", "none")
        .style("stroke", "blue")
        .attr("r", 4);
 
    // place the value at the intersection
    focus.append("text")
        .attr("class", "y1")
        .style("stroke", "white")
        .style("stroke-width", "3.5px")
        .style("opacity", 0.8)
        .attr("dx", 8)
        .attr("dy", "-.3em");
    focus.append("text")
        .attr("class", "y2")
        .attr("dx", 8)
        .attr("dy", "-.3em");
    // place the date at the intersection
    focus.append("text")
        .attr("class", "y3")
        .style("stroke", "white")
        .style("stroke-width", "3.5px")
        .style("opacity", 0.8)
        .attr("dx", 8)
        .attr("dy", "1em");
    focus.append("text")
        .attr("class", "y4")
        .attr("dx", 8)
        .attr("dy", "1em");
    
    // append the rectangle to capture mouse
    svg.append("rect")
        .attr("width", width)
        .attr("height", height)
        .style("fill", "none")
        .style("pointer-events", "all")
        .on("mouseover", function() { focus.style("display", null); })
        .on("mouseout", function() { focus.style("display", "none"); })
        .on("mousemove", mousemove);
 
    function mousemove() {
        var x0 = x.invert(d3.mouse(this)[0]),
            i = bisectDate(data, x0, 1),
            d0 = data[i - 1],
            d1 = data[i],
            d = x0 - d0.zeit > d1.zeit- x0 ? d1 : d0;

                    focus.select("circle.y")
            .attr("transform",
                  "translate(" + x(d.zeit) + "," +
                                 y(d.count) + ")");
 
        focus.select("text.y1")
            .attr("transform",
                  "translate(" + x(d.zeit) + "," +
                                 y(d.count) + ")")
            .text("$" + d.total + " total");
 
        focus.select("text.y2")
            .attr("transform",
                  "translate(" + x(d.zeit) + "," +
                                 y(d.count) + ")")
            .text("$" + d.total + " total");
 
        focus.select("text.y3")
            .attr("transform",
                  "translate(" + x(d.zeit) + "," +
                                 y(d.count) + ")")
            .text(d.avg + "avg per customer ");
 
        focus.select("text.y4")
            .attr("transform",
                  "translate(" + x(d.zeit) + "," +
                                 y(d.count) + ")")
            .text(d.avg + "avg per customer");
 
        focus.select(".x")
            .attr("transform",
                  "translate(" + x(d.zeit) + "," +
                                 y(d.count) + ")")
                       .attr("y2", height - y(d.count));
 
        focus.select(".y")
            .attr("transform",
                  "translate(" + width * -1 + "," +
                                 y(d.count) + ")")
                       .attr("x2", width + width);
 
       
    }
 
// });


})();

 (function() {

 var margin = {top: 30, right: 100, bottom: 50, left: 40},
    width = 800 - margin.left - margin.right,
    height = 270 - margin.top - margin.bottom;
 
// Parse the date / time
var parseDate = d3.time.format("%H:%M").parse,
    formatDate = d3.time.format("%H:%M"),
    bisectDate = d3.bisector(function(d) { return d.zeit; }).left;
 
// Set the ranges
var x = d3.time.scale().range([0, width]);
var y = d3.scale.linear().range([height, 0]);
 
// Define the axes
var xAxis = d3.svg.axis().scale(x)
    .orient("bottom").ticks(12);
 
var yAxis = d3.svg.axis().scale(y)
    .orient("left").ticks(12);
 
// Define the line
var valueline = d3.svg.line()
    .x(function(d) { return x(d.zeit); })
    .y(function(d) { return y(d.total); });
    
// Adds the svg canvas
var svg = d3.select("#graph2")
    .append("svg")
        .attr("width", width + margin.left + margin.right)
        .attr("height", height + margin.top + margin.bottom)
    .append("g")
        .attr("transform", 
              "translate(" + margin.left + "," + margin.top + ")");
 
var lineSvg = svg.append("g"); 
 
var focus = svg.append("g") 
    .style("display", "none");
 
// Get the data
d3.csv("https://dl.dropboxusercontent.com/u/10328969/report.csv", function(error, data) {
    data.forEach(function(d) {
        d.zeit = parseDate(d.zeit);
        d.total = +d.total;
        d.count = d.count;
    });
 
    // Scale the range of the data
    x.domain(d3.extent(data, function(d) { return d.zeit; }));
    y.domain([0, d3.max(data, function(d) { return d.total; })]);
 
    // Add the valueline path.
    lineSvg.append("path")
        .attr("class", "line")
        .attr("d", valueline(data));
 
    // Add the X Axis
    svg.append("g")
        .attr("class", "x axis")
        .attr("transform", "translate(0," + height + ")")
        .call(xAxis);
        
        
    // Add the Y Axis
    svg.append("g")
        .attr("class", "y axis")
        .call(yAxis);

    svg.append("text")             // text label for the x axis
        .attr("x", width /2 )
        .attr("y",  height + margin.bottom )
        .style("text-anchor", "middle")
        .text("Time Period");
    svg.append("text")
        .attr("x", (width / 2))             
        .attr("y", 0 - (margin.top / 2))
        .attr("text-anchor", "middle")  
        .style("font-size", "16px") 
        .style("text-decoration", "underline")  
        .text("Time Period vs Total Sales - Starbucks Sales By Period Daily Report");

    svg.append("text")
        .attr("transform", "rotate(-90)")     
        .attr("y", 0 - margin.left)
        .attr("x", 0 - (height / 2))
        .attr("dy", "1em")
        .style("text-anchor", "middle")
        .text("Total Sales");

    
   // append the x line
    focus.append("line")
        .attr("class", "x")
        .style("stroke", "blue")
        .style("stroke-dasharray", "3,3")
        .style("opacity", 0.5)
        .attr("y1", 0)
        .attr("y2", height);
       

 
    // append the y line
    focus.append("line")
        .attr("class", "y")
        .style("stroke", "blue")
        .style("stroke-dasharray", "3,3")
        .style("opacity", 0.5)
        .attr("x1", width)
        .attr("x2", width);
 
    // append the circle at the intersection
    focus.append("circle")
        .attr("class", "y")
        .style("fill", "none")
        .style("stroke", "blue")
        .attr("r", 4);
 
    // place the value at the intersection
    focus.append("text")
        .attr("class", "y1")
        .style("stroke", "white")
        .style("stroke-width", "3.5px")
        .style("opacity", 0.8)
        .attr("dx", 8)
        .attr("dy", "-.3em");
    focus.append("text")
        .attr("class", "y2")
        .attr("dx", 8)
        .attr("dy", "-.3em");
 
    // place the date at the intersection
    focus.append("text")
        .attr("class", "y3")
        .style("stroke", "white")
        .style("stroke-width", "3.5px")
        .style("opacity", 0.8)
        .attr("dx", 8)
        .attr("dy", "1em");
    focus.append("text")
        .attr("class", "y4")
        .attr("dx", 8)
        .attr("dy", "1em");
    
    // append the rectangle to capture mouse
    svg.append("rect")
        .attr("width", width)
        .attr("height", height)
        .style("fill", "none")
        .style("pointer-events", "all")
        .on("mouseover", function() { focus.style("display", null); })
        .on("mouseout", function() { focus.style("display", "none"); })
        .on("mousemove", mousemove);
 
    function mousemove() {
        var x0 = x.invert(d3.mouse(this)[0]),
            i = bisectDate(data, x0, 1),
            d0 = data[i - 1],
            d1 = data[i],
            d = x0 - d0.zeit > d1.zeit- x0 ? d1 : d0;

                    focus.select("circle.y")
            .attr("transform",
                  "translate(" + x(d.zeit) + "," +
                                 y(d.total) + ")");
 
        focus.select("text.y1")
            .attr("transform",
                  "translate(" + x(d.zeit) + "," +
                                 y(d.total) + ")")
            .text( d.count + " persons");
 
        focus.select("text.y2")
            .attr("transform",
                  "translate(" + x(d.zeit) + "," +
                                 y(d.total) + ")")
            .text(d.count + " persons");
 
        focus.select("text.y3")
            .attr("transform",
                  "translate(" + x(d.zeit) + "," +
                                 y(d.total) + ")")
            .text(d.avg + "avg per");
 
        focus.select("text.y4")
            .attr("transform",
                  "translate(" + x(d.zeit) + "," +
                                 y(d.total) + ")")
            .text(d.avg + "avg per");
 
        focus.select(".x")
            .attr("transform",
                  "translate(" + x(d.zeit) + "," +
                                 y(d.total) + ")")
                       .attr("y2", height - y(d.total));
 
        focus.select(".y")
            .attr("transform",
                  "translate(" + width * -1 + "," +
                                 y(d.total) + ")")
                       .attr("x2", width + width);
 
       
    }
 
});


})();


</script>



 
<div style="width: 700px; margin-left: auto; margin-right:auto">
    <table>
    <caption style="color: #083095; font-size: 18px">Sales By Period Daily Report</caption>
<tr>
  <th>Time</th>
  <th>Customer Count</th>
  <th>Period Total</th>
 
</tr>
<tr>
  <td>5:30 to 6:00</td>
  <td>12</td> 
  <td>$41</td> 
  
</tr>
<tr>

 <td>6:00 to 6:30</td>
  <td>19</td> 
  <td>$52</td> 
 
</tr>

<tr>

 <td>6:30 to 7:00</td>
  <td>21</td> 
  <td>$74</td> 
 
  
</tr>
<tr>

 <td>7:00 to 7:30</td>
  <td>28</td> 
  <td>$143.25</td> 
 
  
</tr>
<tr>

 <td>7:30 to 8:00</td>
  <td>30</td> 
  <td>$141.30</td> 

  
</tr>
<tr>

 <td>8:00 to 8:30</td>
  <td>32</td> 
  <td>$124.80</td> 

</tr>

<tr>

 <td>8:30 to 9:00</td>
  <td>24</td> 
  <td>$74.80</td> 
 
  
</tr>
<tr>

 <td>9:00 to 9:30</td>
  <td>47</td> 
  <td>$172.35</td> 
 
  
</tr>
<tr>

 <td>9:30 to 10:00</td>
  <td>27</td> 
  <td>$119.77</td> 
 
  
</tr>
<tr>
<tr>

 <td>10:00 to 10:30</td>
  <td>40</td> 
  <td>$210.44</td> 
 
  
</tr>
<tr>
<tr>

 <td>10:30 to 11:00</td>
  <td>20</td> 
  <td>$150.95</td> 
 
  
</tr>
<tr>

 <td>11:00 to 11:30</td>
  <td>12</td> 
  <td>$80.30</td> 
 
  
</tr>
<tr>

 <td>total</td>
  <td>325</td> 
  <td>$1384.54</td> 
 
  
</tr>

</table>
</div>





<h4> Unrelated Posts</h4>
<a href="http://discussthetimes.com/blog/twitter/Ten-Women-Is-There-A-Common-Thread/">10 Women: Is There A Common Thread?</a>

<img class="image-center" src="/10women.png">

<h4> Related Posts</h4>

<a href="http://discussthetimes.com/blog/politics/Hard-Choices-Hillary-Clinton-Thought-Iraq-War-Was-Over/">Bad Choices: Hillary Clinton Wrote Too Soon About the Iraq War</a>

<img class="image-center" src="/hardchoices.png">


