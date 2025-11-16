---
name: Homework 5
tools: [Python, HTML, vega-lite]
image: [assets/pngs/homework_5_plot_1.png, assets/pngs/homework_5_plot_2.png]
description: Plots for homework 5
custom_js:
  - vega.min
  - vega-lite.min
  - vega-embed.min
  - justcharts
---


# Plot 1

Plot 1 Write-Up 

Plot 1: Most common license types in Fall 2022.

For my first visualization, I examined which business license types were most frequently issued during Fall 2022. The dataset contains application records including license descriptions, business names, and application dates. I transformed the application date column into a timestamp, removed missing values, and counted how many times each LICENSE_DESCRIPTION appeared. I selected the top 15 most common categories to keep the visualization readable. Using Altair, I encoded the license type as a nominal variable on the y-axis and the number of applications as a quantitative value on the x-axis. I added a continuous color encoding on the count variable to reinforce which categories were most prevalent. This horizontal bar chart makes it easier to compare business types and highlights which categories have more licensing activity.

<vegachart schema-url="{{ site.baseurl }}/assets/json/licenses_top_types.json" style="width: 100%"></vegachart>

# Plot 2 

Plot 2 Write-Up 

Plot 2: Monthly licensing trends linked to license types
The second visualization explores how licensing activity changes throughout the year and which kinds of businesses contribute to these trends. I first converted APPLICATION_RECEIVED_DATE into a timestamp, then extracted the month and year components in Python. The top chart shows a bar chart of the number of applications per month. The bottom chart shows counts of license types, but only for the months the user selects. Both charts draw from the same cleaned dataset, but the lower chart updates dynamically based on the user’s selected time window. 

To add meaningful interactivity, I used an interval brush selection (alt.selection_interval) along the x-axis of the month histogram. When the user drags to select a range of months, the bottom bar chart automatically filters to show only license types submitted during that range. This makes it easy to explore patterns—such as seasonal spikes, restaurant-heavy months, or months dominated by construction permits. The interactivity helps users quickly investigate temporal patterns without cluttering the view with multiple faceted or small-multiple charts. 

<vegachart schema-url="{{ site.baseurl }}/assets/json/licenses_month_linked.json" style="width: 100%"></vegachart>


## Search The Data & Methods

<div class="left">
{% include elements/button.html link="https://github.com/UIUC-iSchool-DataViz/is445_data/raw/main/licenses_fall2022.csv" text="The Data" %}
</div>

<div class="right">
{% include elements/button.html link="https://github.com/garcia9810/garcia9810.github.io/tree/main/python_notebooks/Workbook.ipynb" text="The Analysis" %}
</div>

