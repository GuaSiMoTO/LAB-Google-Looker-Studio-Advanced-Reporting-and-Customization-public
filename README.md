# LAB-Google-Looker-Studio-Advanced-Reporting-and-Customization

## Introduction

Hello guys! This is the second lab of Looker Studio. Here we will design and develop more advanced reports, and we will use more complex tools that Google Looker Studio provide.

## Initial Setup

### Requirements
Start by forking the provided GitHub repository to your account and then clone it locally. This will be your workspace for completing the lab exercises.

- [Learn how to fork this repo](https://guides.github.com/activities/forking/)
- Clone this repo into your `code/labs` folder

### Scenario

This time we will work with the Earthquake data of Central Asia. We got this data from this link "Harmonized Earthquacke Catalogue for Central Asia --> [Central Asia Earthquake Catalogue](https://datacatalog.worldbank.org/search/dataset/0064167/Central-Asia-earthquake-catalogue)

This dataset contains all the earthquakes that happened in Central Asia (at this point I think is obvious, right? 😁). Pay attention to this variable types:
- Latitude and Longitude.
- Dates variables.

### Starter File

You can download the SFRARR_Earthquake_Catalogue.csv file in this repository. This CSV contains all the data for this project.

### Iteration 0: Create a Data Source with the SFRARR_Earthquake_Catalogue.csv file.

Go to your looker studio and create a Data Source with the CSV contained in this repository.

### Iteration 1: Start tunning the Data Source dates

Modify the date fields, and make them fit into their corresponding format. For example, "Day" field must be "Day of Month" type.

Warning: There are no data type for "Second" or "Year". We will fix them in next iteration.

### Iteration 2: Little trick for the year and second field

As we said in the theory session, Looker Studio parser sometimes fail. This is one of this cases. We have to prepare the year field to make him understand it. So lets do the next steps:
- Change the "Year" field name to "Year_categorical", and change it to Numeric data type.
- Create a calculated field named "Year" that uses this formula --> year(DATE(Year_raw,1,1)).
- Hide the "Year_raw" field, so it doesnt appear in the reports (in the three dots, click on it and select "Hide").

As you see in the formula, we create a fake date with our year, and then  we extract the year. This generates a year Data Type.

Sadly, the "Second" field doesn't have a specific type, so just convert it to "Numeric".

### Iteration 3: Latitude & Longitude

This two fields have an important information, but Looker can't use them properly in Map charts if they are not correctly formated. We have to combine them. Follow the next steps:
- Create a Calculated field that concatenate both fields into one.
- Name it "Location".
- Hide the "Latitude" and "Longitude" fields
- Hint 1 --> an example of ("Latitude Longitude")[https://support.google.com/looker-studio/answer/9843174?hl=en#latitude-longitude&zippy=%2Cin-this-article] Data type is "51.5074,-0.1278". Your calculated field must create this.
- Hint 2 --> use one of this functions (Text Functions)[https://support.google.com/looker-studio/topic/7041728?hl=en&ref_topic=7019880&sjid=6090106204308859891-EU]

### Iteration 4: Some small fixes on Default Aggregation

Now, we will analyze the default aggregations in the numeric fields. We have two numeric fields: "Depth" and "MagSize". In this case, to represent the reality we should apply an Averange/Max/Min in both. This is because it doesnt make sense to Sum the depth of multiple earthquakes.

### Iteration 5: Start creating a Map Report

Our crativity session starts now! Lets begin with a Bubble Map. We have two interesting variables here to plot in the Map: The "Depth" and the "MagSize". Set the next parameters on your bubble map:
- Size --> Depth
- Color Metric --> MagSize
- Go to Style and tune the color, so the progresion is (Green, yellow, red). For non data metrics, use grey.

  WARNING: because of the huge amount of data, the map could be non centered. You will have to drag and zoom to the zone where the data is.

### Iteration 6: Add some control to your data

The map is colorfoul and full of information, right? Well, maybe too much information that is hard to know what happened... Lets add some Sliders and DropDown list to the report, so we can focus our vision to some point of the data. Add the follow controls:
- Slider for "MagSize".
- Fixed List for "Year_categorical".
- An advanced filter with "Id".

Do not forget to prettify them!

### Iteration 7: Drilling down into the dates.

In this step we will need a new Calculated field. It will be the "MagSize" with no decimals. For this, use the mathematical round function that Looker provide, and create a new Calculated field named "Rounded_MagSize".

After this, create a stacked Column chart, with:
- Drill down enabled.
- "Year_categorical" and "Month" as Dimension.
- "Rounded_MagSize" as Breakdown Dimension.
- "Record count" as metric.
- Sort by "Year_categorical" in descending mode.
- Secondary sort, use "Rounded_MagSize".

### Iteration 8: Use Versioning to save your data.

To finish, do not forget to save your version!. First, Save a version named "Final Report" and mthen ake a screenshot of your Version History. Save it for us!

### Bonues 3



### Bonus 2

Nice job! Now lets try something harder. There is a dataset with the Welfare of the countries here --> (Poverty And Inequality Platform)[https://datacatalog.worldbank.org/search/dataset/0063646/-Poverty-and-Inequality-Platform--PIP---Percentiles]

Download the "Survey-years percentiles - 2017 PPP values" CSV, and design a report that shows us the world welfare. The report needs to have this characteristics:
- It has to be interactive. The user should be able to choose a country and analyze it (use a Map, so the user can select a country with the map)
- It has to show the averange welfare evolution through the percentile.
- There should be a Chart where we can compare the averange welfare of all countries.

Tip: The "percentile" field and the "avg_welfare" are the most important ones.


# Submission
Once you have completed your analysis and visualizations, make a PDF of your reports and push them to your forked GitHub repository. Ensure that your final submission includes narratives explaining your visualizations and insights.

```bash
$ git add .
$ git commit -m "done"
$ git push origin main
```

Then create a Pull Request!!

# Additional Resources

- [Google Looker Studio Documentation](https://support.google.com/lookerstudio/)
- [Google Looker Studio Visualization types](https://cloud.google.com/looker/docs/visualization-types)
- [Looker Charts Reference](https://support.google.com/looker-studio/topic/7059081)
- [Downloading your report as PDF](https://support.google.com/looker-studio/answer/9125317)
