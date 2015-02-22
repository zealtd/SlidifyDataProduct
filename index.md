---
title       : Data Product Pitch
subtitle    : Predicting and visualizing Profits on Fruit over time
author      : Ahsan Ijaz
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Synopsis

1. The purpose of this project is to explore the Fruits data set that comes with Google Visualization library.
2. Google Motion chart is used to provide an interactive display to do so.
3. Prediction using a linear model is made on the profits provided by fruits based on type, time and location of the fruit.


--- 

## Google Motion Visualization
The Google visualization plot is used to check how different variables in the Fruits data set vary with time.

```r
 Motion=gvisMotionChart(Fruits,timevar = "Year",idvar = "Fruit")
Motion
```

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
  "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<title>MotionChartIDb4f31e5f1c0</title>
<meta http-equiv="content-type" content="text/html;charset=utf-8" />
<style type="text/css">
body {
  color: #444444;
  font-family: Arial,Helvetica,sans-serif;
  font-size: 75%;
  }
  a {
  color: #4D87C7;
  text-decoration: none;
}
</style>
</head>
<body>
 <!-- MotionChart generated in R 3.1.2 by googleVis 0.5.7 package -->
<!-- Mon Feb 23 03:36:39 2015 -->


<!-- jsHeader -->
<script type="text/javascript">
 
// jsData 
function gvisDataMotionChartIDb4f31e5f1c0 () {
var data = new google.visualization.DataTable();
var datajson =
[
 [
 "Apples",
2008,
"West",
98,
78,
20,
"2008-12-31" 
],
[
 "Apples",
2009,
"West",
111,
79,
32,
"2009-12-31" 
],
[
 "Apples",
2010,
"West",
89,
76,
13,
"2010-12-31" 
],
[
 "Oranges",
2008,
"East",
96,
81,
15,
"2008-12-31" 
],
[
 "Bananas",
2008,
"East",
85,
76,
9,
"2008-12-31" 
],
[
 "Oranges",
2009,
"East",
93,
80,
13,
"2009-12-31" 
],
[
 "Bananas",
2009,
"East",
94,
78,
16,
"2009-12-31" 
],
[
 "Oranges",
2010,
"East",
98,
91,
7,
"2010-12-31" 
],
[
 "Bananas",
2010,
"East",
81,
71,
10,
"2010-12-31" 
] 
];
data.addColumn('string','Fruit');
data.addColumn('number','Year');
data.addColumn('string','Location');
data.addColumn('number','Sales');
data.addColumn('number','Expenses');
data.addColumn('number','Profit');
data.addColumn('string','Date');
data.addRows(datajson);
return(data);
}
 
// jsDrawChart
function drawChartMotionChartIDb4f31e5f1c0() {
var data = gvisDataMotionChartIDb4f31e5f1c0();
var options = {};
options["width"] =    600;
options["height"] =    500;
options["state"] = "";

    var chart = new google.visualization.MotionChart(
    document.getElementById('MotionChartIDb4f31e5f1c0')
    );
    chart.draw(data,options);
    

}
  
 
// jsDisplayChart
(function() {
var pkgs = window.__gvisPackages = window.__gvisPackages || [];
var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
var chartid = "motionchart";
  
// Manually see if chartid is in pkgs (not all browsers support Array.indexOf)
var i, newPackage = true;
for (i = 0; newPackage && i < pkgs.length; i++) {
if (pkgs[i] === chartid)
newPackage = false;
}
if (newPackage)
  pkgs.push(chartid);
  
// Add the drawChart function to the global list of callbacks
callbacks.push(drawChartMotionChartIDb4f31e5f1c0);
})();
function displayChartMotionChartIDb4f31e5f1c0() {
  var pkgs = window.__gvisPackages = window.__gvisPackages || [];
  var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
  window.clearTimeout(window.__gvisLoad);
  // The timeout is set to 100 because otherwise the container div we are
  // targeting might not be part of the document yet
  window.__gvisLoad = setTimeout(function() {
  var pkgCount = pkgs.length;
  google.load("visualization", "1", { packages:pkgs, callback: function() {
  if (pkgCount != pkgs.length) {
  // Race condition where another setTimeout call snuck in after us; if
  // that call added a package, we must not shift its callback
  return;
}
while (callbacks.length > 0)
callbacks.shift()();
} });
}, 100);
}
 
// jsFooter
</script>
 
<!-- jsChart -->  
<script type="text/javascript" src="https://www.google.com/jsapi?callback=displayChartMotionChartIDb4f31e5f1c0"></script>
 
<!-- divChart -->
  
<div id="MotionChartIDb4f31e5f1c0" 
  style="width: 600; height: 500;">
</div>
 <div><span>Data: Fruits &#8226; Chart ID: <a href="Chart_MotionChartIDb4f31e5f1c0.html">MotionChartIDb4f31e5f1c0</a> &#8226; <a href="https://github.com/mages/googleVis">googleVis-0.5.7</a></span><br /> 
<!-- htmlFooter -->
<span> 
  R version 3.1.2 (2014-10-31) 
  &#8226; <a href="https://developers.google.com/terms/">Google Terms of Use</a> &#8226; <a href="https://google-developers.appspot.com/chart/interactive/docs/gallery/motionchart">Documentation and Data Policy</a>
</span></div>
</body>
</html>
---


## Prediction Mechanism

1. Prediction is done for completion of server calculation requirement and is ill advised.
2. It is ill-advised since the data set is too small and the model too simple.
3. Moreover, the variables used are intentionally chosen as year, type and location so that it throws somewhat ludicrous predictions and also is able to demonstrate the selection of inputs.
4. The model chosen is shown as follows.


```r
 fit<-lm(Profit~ Location + Fruit + Year,data= Fruits)
fit$coefficients
```

```
##   (Intercept)  LocationWest  FruitBananas  FruitOranges          Year 
##  4.699333e+03  1.000000e+01  2.477748e-15            NA -2.333333e+00
```
---

## Navigation Bar

A navigation bar is provided that moves from visualization to prediction to help file of the product.

---

## Final Thoughts

1. It is ill advised to take any predictions of the product seriously.
2. The purpose was to learn slidify and shiny apps, and the student in question has gotten some idea of how to use them.

---


