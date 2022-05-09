---
title: "San Francisco building emissions"
date: "2022-05-07"
menu:
  main:
    title: "Home"
    weight: 1
  
---

# Building emissions in San Francisco and how to use data science and machine learning to explore solutions to reduce them

The global pandemic has only just released it's grip on much of the world, but while the world was distracted, another threat to humanity tightened it's grip: global warming. While the pandemic has had surprising effects(INSERT REF TO REFERENCE 1) upon the climate, global warming is still as large a threat to the long-term future of civilization. With oceans rising, increasing amounts of extreme weather and rising temperatures, it is clear that we must reduce carbon emissions and that we should encourage any reductions, however small. We have therefore decided to explore how cities can analyse their building emissions and which steps they can take, based on the results of the analysis. We aim to do this by observing the building emissions for different industries from the city of San Francisco and provide thorough explanations to what we do and why we do it, such that other cities will be able to replicate the steps we have taken and thus make informed decisions regarding how they can reduce their own building emissions. We do this by first introducing our steps to preprocess our data, then we explore which industries' are the largest contributors to the emissions and lastly, provide a framework for how to evaluate the results of the analysis and make informed decisions, backed by data. 

%noget med machine learning?

## You have your dataset, now what?

An important step towards creating meaningful results from data analysis is to first take a step backwards and consider the data at your disposal. Do you have some columns that are irrelevant the problem at hand or are you missing key data values or do you wish to create new columns based on the existing ones to provide context to the dataste? In any case, you will likely need to do some data preprocessing to ensure that your dataset is sanitized and ready to be processed. Preprocessing is an activity that is largely individual for each dataset, as what needs to be done is entirely dependant on the dataset itself and the aim of the data analysis. 

### Our approach to the San Francisco dataset

%Thomas skriv? idk

## Exploring industries' effect on emissions

Next, we must explore the emissions of the different industries within the city by first identifying the largest offenders and then exploring how these compare to each other and what effect reducing their individual emissions could have upon the overall building emissions of the city. We do this by grouping the data of the different industries and then creating different plots to illustrate their relationships with different features of the dataset to identify correlations between these. These correlations help us contextualize the emissions from different industries.
{{< load-plotly >}}
{{< plotly json="/plotly/compliance.json" modebar="false">}}
{{< plotly json="/plotly/Benchmark.json" modebar="false">}}

{{< plotly json="/plotly/Map1.json" height="800px" width="800px" modebar="false">}}

test