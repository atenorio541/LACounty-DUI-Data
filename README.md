# DUI Crash  Data Across Los Angeles County
##
Background of Los Angeles County

Dataset 

import pandas as pd
import plotly.express as px

# Extracting day of the week from 'COLLISION_DATE' (Monday=0, Sunday=6)
df['DayOfWeek'] = df['COLLISION_DATE'].dt.dayofweek

# Filtering data for alcohol-involved accidents
alcohol_df = df[df['ALCOHOL_INVOLVED'] == 'Y']

# Counting alcohol-involved accidents by day of the week
day_of_week_counts = alcohol_df['DayOfWeek'].value_counts().sort_index()

# Creating a Plotly bar chart for alcohol-involved accidents by day of the week
fig_alcohol_day = px.bar(x=day_of_week_counts.index, y=day_of_week_counts.values,
                         labels={'x': 'Day of Week', 'y': 'Accident Frequency'},
                         title='Alcohol-Involved Accidents by Day of the Week')
fig_alcohol_day.update_layout(xaxis={'tickmode': 'array', 'tickvals': [0, 1, 2, 3, 4, 5, 6],
                                     'ticktext': ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']},
                              yaxis_title='Accident Frequency')
fig_alcohol_day.show()
