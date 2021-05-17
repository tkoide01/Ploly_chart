# Belly Button Biodiversity Ploly-chart
Utilize Ploly-chart, JavaScript and HTML to deploy visualized data.

## Overview of the Project
Using JavaScript, HTML, D3.js, Plotly.js, and CSS style sheet to visualize JSON file data to Bar Chart, Gauge Chart and Bubble Chart along with customizing HTML file taking below steps:

- Deliverable 1: Create a Horizontal Bar Chart
- Deliverable 2: Create a Bubble Chart
- Deliverable 3: Create a Gauge Chart
- Deliverable 4: Customize the Dashboard

## Resources
- Data Source: samples.json
- Software: Chrome Blowser, Visual Code Stuido, and Anaconda Prompt
- Image Source: <https://m.facebook.com/Belly-Button-Biodiversity-141859419220981/>

## Results
  Based on the two technical analysis, we can infer below information.
  
  1. Deliverable 1: Create a Horizontal Bar Chart
  ```
  function buildCharts(sample) {
  // 2. Use d3.json to load and retrieve the samples.json file 
  d3.json("static/data/samples.json").then((data) => {
    // 3. Create a variable that holds the samples array. 
    var samplesData = data.samples;
    // 4. Create a variable that filters the samples for the object with the desired sample number.
    var filteredData = samplesData.filter(sampleObj => sampleObj.id == sample);
    //  5. Create a variable that holds the first sample in the array.
    var firstSample = filteredData[0];

    // 6. Create variables that hold the otu_ids, otu_labels, and sample_values.
    var ids  = firstSample.otu_ids;
    var labels = firstSample.otu_labels.slice(0,10).reverse();
    var values = firstSample.sample_values.slice(0,10).reverse();

    var bubbleLabels = firstSample.otu_labels;
    var bubbleValues = firstSample.sample_values;
    // 7. Create the yticks for the bar chart.
    // Hint: Get the the top 10 otu_ids and map them in descending order  
    //  so the otu_ids with the most bacteria are last. 

    var yticks = ids.map(sampleObj => "OTU " + sampleObj).slice(0,10).reverse();
    console.log(yticks);

    // 8. Create the trace for the bar chart. 
    var trace = [{
        x: values,
        y: yticks,
        type: "bar",
        orientation: "h",
        text: labels
    }];
    // 9. Create the layout for the bar chart. 
    var barLayout = {
     title: "Top 10 Bacteria Cultures Found"
    };
    // 10. Use Plotly to plot the data with the layout. 
    Plotly.newPlot("bar", trace, barLayout);
  
  ```
  
   ![](static/images/deliverable1_output.png)
     
  2.  Total 
  
      ![](static/images/deliverable2_output.png)
  
  - While, 
  
## Summary
   Based on the results, we can draw followings three business recommendations to the CEO.

  1. Plan special promotions for both Drivers and Riders to improve the supply and demand balance of ride based on the trend we see in the multiple-line chart.
    
     + Given Urban and Rural are experiencing the dip in their Total Fare around the beginning of the April, we should plan special discount or benefit system based on the number of ride a rider utilize to boost the demand during this time period.

     + Also, in order to maintain the supply of driver during the peak time, we should encourage drivers to drive more around the end of February by giving bonus based on the number of ride they provide during this time period to maximize the Total Fare.
  
  2. Decrease the number of drivers in Urban area to avoid cannibalizing its demand amont other drivers.
    
     + Based on the ride-sharing summary DataFrame, we see that Average Fare per Driver in Urban city type is $16.57 and critically lower compared to Suburban and Rural city types. In addition, while other two city types have less number of Total Drivers compared to their Total Rides number, the Total Drivers outnumbers the Total Rides in Urban. This suggets that demand of ride-sharing in Urban city type is not high enough to meet the current number of Drivers we have there. 

     + In order to avoid cannibalization of demand and inneficient use of personnel budget in having excess number of Drivers, we should decrease the number of drivers we hire in the Urban.

  3. Increase the number of drivers in Rural area to cover the missing opportunity in potential riders.
    
     + Based on the ride-sharing summary DataFrame, we see that both Average Fare per Ride and Average Fare per Driver are both highest in the rural area. The fact that Rural's Average Fare per Ride is higher than the other two city types means that each driver is driving longer distance and also longer time for each ride. Which means, the drivers in Rural are more likely to be occupied when there is potential rider seeking for a ride in Rural. 

     + Therefore, we should increase the number of driver in rural area by 1.4 so that Average Fare per Driver will not decline below the Suburban's Average Fare per Driver and see if increasing the supply in driver may lead to increase in the Total Rides and also the Total Fares from Rural city type.
