---
title: "San Francisco building emissions"
date: "2022-05-07"
menu:
  main:
    title: "Home"
    weight: 1
  
---
# Building energy usage in San Francisco and how to use data science and machine learning to explore solutions to reduce them
{{< load-plotly >}}
{{< plotly json="../../plotly/Commercial_benchmark_status.json" height="800px" width="800px" modebar="false">}}

{{< load-plotly >}}
{{< plotly json="../../plotly/Commercial_benchmark_by_year.json" height="800px" width="800px" modebar="false">}}

{{< load-plotly >}}
{{< plotly json="../../plotly/correlation_matrix.json" height="800px" width="800px" modebar="false">}}

{{< load-plotly >}}
{{< plotly json="../../plotly/log_source_eui_by_industry.json" height="800px" width="800px" modebar="false">}}

{{< load-plotly >}}
{{< plotly json="../../plotly/median_eui_by_industry_by_year.json" height="800px" width="800px" modebar="false">}}

{{< load-plotly >}}
{{< plotly json="../../plotly/missing_data.json" height="800px" width="800px" modebar="false">}}

{{< load-plotly >}}
{{< plotly json="../../plotly/source_eui_treemap.json" height="800px" width="800px" modebar="false">}}

{{< load-plotly >}}
{{< plotly json="../../plotly/sum_of_eui_by_year_and_industry.json" height="800px" width="800px" modebar="false">}}

{{< load-plotly >}}
{{< plotly json="../../plotly/yearly_total_emissions.json" height="800px" width="800px" modebar="false">}}

The global pandemic has only just released its grip on much of the world, but while the world was distracted, another threat to humanity tightened its grip: global warming. While the pandemic has had surprising effects[1] upon the climate, global warming is still as large a threat to the long-term future of civilization. With oceans rising, increasing amounts of extreme weather and rising temperatures, it is clear that we must reduce carbon emissions and that we should encourage any reductions, however small they may be. We have therefore decided to explore how the city of San Francisco can analyze their building energy usage intensity (EUI) and where an increased effort is needed, based on the results of the analysis. We aim to do this by observing the building EUI for different industries from the city of San Francisco and provide thorough explanations to what we do and why we do it, such that other cities will be able to replicate the steps we have taken and thus make informed decisions regarding where they can reduce their own building EUI. We do this by first introducing our steps to preprocess our data, then we explore which industries' have the largest EUI and lastly, provide a framework for how to evaluate the results of the analysis and make informed decisions, backed by data. 

---
**NOTE**

It works with almost all markdown flavours (the below blank line matters).

---

## You have your dataset, now what?

An important step towards creating meaningful results from data analysis is to first take a step backwards and consider the data at your disposal. Do you have some columns that are irrelevant the problem at hand or are you missing key data values or do you wish to create new columns based on the existing ones to provide context to the dataset? In any case, you will likely need to do some data preprocessing to ensure that your dataset is sanitized and ready to be processed. Preprocessing is an activity that is largely individual for each dataset, as what needs to be done is entirely dependant on the dataset itself and the aim of the data analysis. 

### Our approach to preprocessing the San Francisco dataset

At a first glance, the dataset contains a lot of missing data, which needs to preprocessed before diving into an analysis.
We limited the dataset to a subset of attributes for the analysis as step before remov

 and removed the records with missing values.

#THOMAS WRITE PREPROCESSING

## Identifying interesting patterns

Now for the fun parts of data analysis, exploring the nooks and crannies of your dataset! The first part of this journey is to take a step backwards (again) and try to process your dataset in your mind by asking the right questions; what are you trying to do with your dataset and can this intuitively be explained by any of the features in your dataset? If you cannot answer these questions, that's completely fine and you can still follow the same structure, but instead of targeting your search on specific features, you should examine every available feature. 

### Controlled pattern exploration

These questions helps you define your objective (if any) and provide you with hypothesis that you can explore by creating specific visualizations or plots related to the hypothesis. Our objective was to reduce overall building emissions in San Francisco by reducing the overall EUI. We then explored the current trends in our dataset, which shows that the overall EUI of San Francisco is currently trending downwards. 

As we are looking to reduce building EUI in the future, we are looking for features that can be shown to be correlated with building EUI. When going through the features in our dataset, we identified three candidate features that could be correlated with building EUI: 

 - Floor area
 - Year Built
 - Property type - self-reported%%%%%%%%%%WRITE CORRECT HERE, DONT REMEMBER

We started by examining the floor area and year built features by plotting these against the EUI in separate scatter plots and visualizing the trend:

{{< plotly json="../../plotly/correlation_matrix.json" height="800px" width="800px" modebar="false">}}

We found that, while both correlate with EUI to a small degree, they are not entirely able to explain the large variations in EUI between various buildings. 

Next, we decided to examine the self reported property type by exploring which industries' had the highest building EUI. This proved to be a hard task, as not all industries are equally represented and as some industries simply need a larger power consumption to function, thereby inflating it's building EUI. We noticed the Offices and Data center industries as extreme examples of this. Offices are extremely overrepresented in the dataset, but each individual office does not have a high building EUI. In contrast, there are very few data centers, but each data center has a very high building EUI, as they inherently consume a lot of energy to power all the computing units. As we can observe that different industries have vastly differing building EUI values, we concluded industries are correlated with building EUI, but we could not entirely explain the correlation. 

As we could not explain the correlation between industry and EUI, we decided to take a closer look on their relationship. As we have observed that overall EUI in San Francisco is currently trending downwards, we are interested in exploring which different industries follow this trend and, more importantly, those that don't. We have done this by observing the relative change for each year for every industry, from the benchmark in 2012:

%INSERT PLOT REGARDING PERCENTAGE CHANGE FROM 2012
{{< plotly json="../../plotly/yearly_total_emissions.json" height="800px" width="800px" modebar="false">}}
%EXPLAIN WHAT WE OBSERVE

%MOTIVATE MACHINE LEARNING

## Creating predictions

As we deal with an immense amount of data, we must unfortunately (for some) venture into the uncharted lands of Machine Learning to make any relevant predictions for the future. Luckily, it has never been easier to enter these uncharted lands, as libraries and online guides make it as easy to create a machine learning model as it is to fill out an online form: just input the variables and you're off! Of course, some online forms are complicated and require information that is not readily available to you and you therefore need to do some digging to find it. Likewise, you sometimes need to tweak small details regarding your machine learning model to ensure that the results are adequate. We will briefly discuss our machine learning model and how we use the model's predictions as a basis for our suggestions for San Francisco to reduce building EUI. 

We can observe that building EUI is seemingly dependant on the industry connected to the building and that some industries have seemingly taken steps to reduce their building EUI, while others have not. We therefore decided to explore how the industries' building EUI could develop in the future, if current trends hold. To do this, we developed a machine learning model, using linear regression, to predict the building EUI of each industry for the next two years. The initial model, let's call it Emel, is just a linear regression model %THOMAS PLEASE WRITE

## Exploring industries' effect on building EUI in the future

Based on Emel's predictions, we can now explore how the different industries' building EUI project into the future and based on this we can explore the different avenues that San Francisco has to reduce their building EUI to reduce their overall emissions. To contextualize this, we first recap the current trends for each industry:

%INSERT CURRENT INDUSTRY TRENDS LINE PLOT (WITHOUT ML PREDS)(OR MAYBE BOTH, SWITCHING BY BUTTON??)

%INSERT ML PREDICTIONS

%DESCRIBE THESE

## Results and recommendations

Throughout our exploratory analysis of the dataset, we could observe a correlation between features such as floor area or year built and building EUI. These features are not entirely responsible for a larger EUI, but both positively correlate with a larger EUI. We could, however, observe a slight correlation between industry and building EUI, which intuitively also makes sense, as different activities consume different amounts of power. Furthermore, we explored some industries that had a low contribution to overall building EUI, but had a very large median EUI, such as the data centers. There are relatively few data centers in San Francisco and they therefore do not show up when you only account for total industry EUI. We also discovered that only accounting for median EUI for an industry also has issues, as it allowed industries that had a large proportion of total EUI of San Francisco to slip through unnoticed. As there was no clear way to get an overview of industry EUI, we decided to explore the degree to which different industries improve their building EUI throughout the years recorded in the dataset. Using the initial value in 2012, we created a rolling improvement variable, which proved that not all industries improve at equal pace, even when accounting for relative size. 


%THEN DESCRIBE WHICH INDUSTRIES ARE GOOD AND BAD AND GIVE RECOMMENDATION

test