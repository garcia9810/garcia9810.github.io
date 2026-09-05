---
name: Crime in Chicago 2025
tools: [Python, Streamlit, Pandas, Altair, Docker]
image: assets/pngs/chicago_crimes.png
description: Interactive Streamlit data story exploring 2025 Chicago crime patterns, long-term citywide trends, and how neighborhood hardship relates to reported incidents.
---

# Crime in Chicago 2025: The Patterns Within The Story

An interactive data story built with Streamlit that uses open data from the City of Chicago
to look past individual headlines and examine the larger patterns behind reported crime.

<p class="text-center">
{% include elements/button.html link="https://crimeinchicago2025-d6eond6bajvcyk3edgbns5.streamlit.app/" text="Launch the App" %}
{% include elements/button.html link="https://github.com/garcia9810/Crime_in_Chicago_2025" text="View on GitHub" style="outline-secondary" %}
</p>

![Crime in Chicago 2025 app](/assets/pngs/chicago_crimes.png)

## What the App Does

- **Where are crimes happening in 2025?** An Altair scatter map of reported incidents, filterable
  by offense type, month, and whether an arrest was made. The map samples down past 5,000 points
  so it stays responsive under broad filters.
- **How does 2025 compare to previous years?** A citywide line chart of yearly incident totals
  from 2001 to the present, pre-aggregated through the open data API to keep the payload small.
- **Crime and hardship across community areas.** 2025 incidents joined to census socioeconomic
  indicators at the community-area level, plotted against the hardship index.

## Technical Notes

Data is pulled live from the City of Chicago Socrata API rather than checked-in CSVs, so the app
never falls out of sync with the source. Each dataset load is wrapped in `st.cache_data` to avoid
re-fetching on every interaction, and the app ships as a Docker image for deployment.

## Data Sources

- [Crimes – 2025](https://data.cityofchicago.org/Public-Safety/Crimes-2025/t7ek-mgzi/about_data), City of Chicago Open Data Portal
- [Crimes – 2001 to Present](https://data.cityofchicago.org/Public-Safety/Crimes-2001-to-Present/ijzp-q8t2), City of Chicago Open Data Portal
- [Census Data – Selected Socioeconomic Indicators in Chicago, 2008–2012](https://data.cityofchicago.org/dataset/Census-Data-Selected-socioeconomic-indicators-in-Chicago-2008-2012/kn9c-c2s2), City of Chicago Open Data Portal
