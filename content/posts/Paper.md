---
title: "Examining San Francisco building energy usage intensity"
date: "2022-05-10"
plotly: true
menu:
  main:
    title: "Home"
    weight: 1
  
---
{{< loadImage >}}

# Building energy usage in San Francisco and how to use data science and machine learning to explore solutions to reduce them

The global pandemic has only just released its grip on much of the world, but while the world was distracted, another threat to humanity tightened its grip: global warming. While the pandemic has had surprising effects[1] upon the climate, global warming is still as large a threat to the long-term future of civilization. With oceans rising, increasing amounts of extreme weather and rising temperatures, it is clear that we must reduce carbon emissions and that we should encourage any reductions, however small they may be. We have therefore decided to explore how the city of San Francisco can analyze their building energy usage intensity (EUI) and where an increased effort is needed, based on the results of the analysis. We aim to do this by observing the building EUI for different industries from the city of San Francisco and provide thorough explanations to what we do and why we do it, such that other cities will be able to replicate the steps we have taken and thus make informed decisions regarding where they can reduce their own building EUI. We do this by first introducing our steps to preprocess our data, then we explore which industries' have the largest EUI and lastly, provide a framework for how to evaluate the results of the analysis and make informed decisions, backed by data. 

***What is EUI***

Energy use intensity (EUI) is an indicator of the energy efficiency of a building's design and/or operations[2].  EUI is expressed as thousands of British thermal units used per square foot per year (kBtu/sq. ft./year)


## You have your dataset, now what?

An important step towards creating meaningful results from data analysis is to first take a step backwards and consider the data at your disposal. Do you have some columns that are irrelevant the problem at hand or are you missing key data values or do you wish to create new columns based on the existing ones to provide context to the dataset? In any case, you will likely need to do some data preprocessing to ensure that your dataset is sanitized and ready to be processed. Preprocessing is an activity that is largely individual for each dataset, as what needs to be done is entirely dependant on the dataset itself and the aim of the data analysis. 

### Our approach to preprocessing the San Francisco dataset

At a first glance, the dataset contains a lot of missing data, which needs to preprocessed before diving into an analysis.
We limited the dataset to a subset of attributes for the analysis as a step before removing missing values.
One of the attributes in the dataset describes the compliance in reporting a building's Site EUI.
While the dataset does differentiate between commercial sites, residential housing and other, it is only the commercial data where compliance is high and the data is sufficient for an analysis. 
As the heart of the analysis concerns the Energy Usage Intensity (EUI), we filter for commercial properties and top off the preprocessing by removing any missing values.


## Identifying interesting patterns

Now for the fun parts of data analysis, exploring the nooks and crannies of your dataset! The first part of this journey is to take a step backwards (again) and try to process your dataset in your mind by asking the right questions; what are you trying to do with your dataset and can this intuitively be explained by any of the features in your dataset? If you cannot answer these questions, that's completely fine and you can still follow the same structure, but instead of targeting your search on specific features, you should examine every available feature. 

### Controlled pattern exploration

These questions helps you define your objective (if any) and provide you with hypothesis that you can explore by creating specific visualizations or plots related to the hypothesis. Our objective was to recommend focus areas to reduce overall building emissions in San Francisco by reducing the overall EUI. We then explored the current trends in our dataset, which shows that the overall EUI of San Francisco is currently trending downwards. 

{{< plotly json="../../plotly/yearly_total_emissions.json" height="600px" width="800px">}}

As we are looking to reduce building EUI in the future, we are looking for features that can be shown to be correlated with building EUI. When going through the features in our dataset, we identified three candidate features that could be correlated with building EUI: 

 - Floor area
 - Year Built
 - Industry

We have also identified areas as another candidate feature that could be correlated to the building EUI. We started by examining the floor area and year built features by visualizing these against the EUI:

{{< plotly json="../../plotly/correlation_matrix.json" height="600px" width="600px">}}

We found that, while both correlate with EUI to a small degree, they are not entirely able to explain the large variations in EUI between various buildings. 

Next, we decided to examine the industries by exploring which industries' had the highest building EUI. 

{{< plotly json="../../plotly/log_source_eui_by_industry.json" height="800px" width="800px">}}

This proved to be a hard task, as not all industries are equally represented and some industries simply have a higher energy usage to function, thereby inflating its building EUI. 
We observe from the figure how the data center has a high median EUI, but in comparison to the following plot, we observe how the data center industry as a whole emits less than many other industries. 

{{< plotly json="../../plotly/source_eui_treemap.json" height="1200px" width="800px">}}

We noticed the Data center industry as an extreme example of the skewed representation. Offices are extremely overrepresented in the dataset, but each individual office does not have a high building EUI (kBtu/ft2). In contrast, there are very few data centers, but each data center has a very high building EUI (kBtu/ft2), as they inherently consume a lot of energy to power all the computing units in a relatively small space. 

{{< plotly json="../../plotly/median_eui_by_industry_by_year.json" height="600px" width="800px">}}

As we can observe, different industries have vastly differing building EUI values, we concluded industries are correlated with building EUI, but we could not entirely explain the correlation. 

As we could not explain the correlation between industry and EUI, we decided to take a closer look on their relationship. As we have observed that overall EUI in San Francisco is currently trending downwards, we are interested in exploring which different industries follow this trend and, more importantly, those that don't. We have done this by observing the relative change for each year for every industry, from the benchmark in 2012:

{{< loadIframe link="https://dtu-nst.github.io/SocialDataExam/plotly/percentage_change_by_industry_relative_2012.html" >}}

From this, we can observe that while most industries are clearly trending towards a lower building EUI as indicated by the negative percentage change, a few are not. These industries include: 

- Automobile Dealerships
- Distribution centers
- Non-refrigerated warehousing
- Laboratories
- Retail stores

We are interested to predict whether these trends are projected to continue, before we feel comfortable making suggestions to improve building EUI in San Francisco. To do this, we must enter realm of machine learning.


## Creating predictions

As we deal with a reasonably sized dataset, we must unfortunately (for some) venture into the uncharted lands of machine learning to make any relevant predictions for the future. Luckily, it has never been easier to enter these uncharted lands, as libraries and online guides make it as easy to create a machine learning model as it is to fill out an online form: just input the variables and you're off! Of course, some online forms are complicated and require information that is not readily available to you and you therefore need to do some digging to find it. Likewise, you sometimes need to tweak small details regarding your machine learning model to ensure that the results are adequate. We will briefly discuss our machine learning model and how we use the model's predictions as a basis for our suggestions for San Francisco to reduce building EUI. 

We can observe that building EUI is seemingly dependant on the industry connected to the building and that some industries have seemingly taken steps to reduce their building EUI, while others have not. We therefore decided to explore how the industries' building EUI could develop in the future, if current trends hold. To do this, we applied a very simple linear model, using a robust variant of linear regression called "TheilSenRegressor"[3] to predict the percentage change in EUI of each industry for the next two years. 

## Exploring industries' effect on building EUI in the future

Based on the predictions obtained from the model, we can now explore how the different industries' building EUI project into the future and based on this we can explore the different avenues that San Francisco has to reduce their building EUI to reduce their overall emissions. To contextualize this, we first recap the current trends for each industry:

{{< plotly json="../../plotly/yearly_percentage_change_in_eui_by_industry.json" height="600px" width="800px">}}

This shows that many industries follow the overall trend of building EUI, while others don't. We are therefore interested in using our model to predict what will happen for the foreseeable future: 

{{< plotly json="../../plotly/yearly_percentage_change_in_eui_by_industry_with_predictions.json" height="600px" width="800px">}}

We can now observe that the list of industries with the least projected improvement change:

- Strip mall
- Automobile Dealership
- Enclosed mall
- Data center
- Distribution centers

While some industries remain, such as automobile dealership, other have now emerged as front runners, such as strip malls amd data centers. Due to the large amount of uncertainty in the future, we have decided to only suggest those that are on both short-lists of least improvement, which leaves us with two industries:

- Automobile Dealership
- Distribution centers

These industries are the ones we suggest the city of San Francisco take a look at, as they do not seem to follow the downwards trend of building EUI. These industries should be held accountable for their inaction and surveys should be conducted to map the sources of their building EUI. 

## A geographical view of the EUI
As we observe a general downwards trend in EUI we motivate a look at the geographical distribution of the industries' EUI.

{{< loadIframe link="https://dtu-nst.github.io/SocialDataExam/plotly/source_eui_by_postal_code_animated.html" >}}

Luckily, the trend is generally the same across the different areas of San Francisco.

We invite the reader to exercise a further investigation into the location of industries for which we observe a positive percentage change, meaning an increase in EUI.

## Results and recommendations

Throughout our exploratory analysis of the dataset, we could observe a correlation between features such as floor area or year built and building EUI. These features are not entirely responsible for a larger EUI, but both positively correlate with a larger EUI. We could, however, observe a slight correlation between industry and building EUI, which intuitively also makes sense, as different activities consume different amounts of power. Furthermore, we explored some industries that had a low contribution to overall building EUI, but had a very large median EUI, such as the data centers. There are relatively few data centers in San Francisco and they therefore do not show up when you only account for total industry EUI. We also discovered that only accounting for median EUI for an industry also has issues, as it allowed industries that had a large proportion of total EUI of San Francisco to slip through unnoticed. As there was no clear way to get an overview of industry EUI, we decided to explore the degree to which different industries improve their building EUI throughout the years recorded in the dataset. Using the initial value in 2012, we created a rolling improvement variable, which proved that not all industries improve at equal pace, even when accounting for relative size. To further support our suggestions, we developed a simple machine learning model to predict the projected building EUI improvement for each industry. 

Based on our rolling improvement variable and our projections for the different industries, we found two key industries that are not improving at the pace of the rest of San Francisco: automobile dealership and distribution centers. We suggest that the city of San Francisco focus on these two industries to decrease their overall building EUI. 

## References
The following are links to the data sources used in this project:
 - [San Francisco Building Emissions](https://data.sfgov.org/Energy-and-Environment/Existing-Buildings-Energy-Performance-Ordinance-Re/j2j3-acqj)

The following references were used in the creation of this project:
 - [1. Emission Reductions From Pandemic Had Unexpected Effects on Atmosphere ](https://climate.nasa.gov/news/3129/emission-reductions-from-pandemic-had-unexpected-effects-on-atmosphere/)
 - [2. What is EUI? ](https://aiacalifornia.org/energy-use-intensity-eui/)
 - [3. TheilSenRegressor ](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.TheilSenRegressor.html)


## Link to work
[Github link to work](https://github.com/DTU-NST/SocialDataExamCode)
