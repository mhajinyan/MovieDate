# MovieDate

# Project Overview

**In this data analysis project, I examine movie performance and trends from 2012 to 2016. By reviewing multiple variables, my goal is to uncover patterns, generate data-informed recommendations, and gain a deeper understanding of the film industry's dynamics.**

 - [Tools](#tools)
 - [Data Overview](#data-overview)
 - [Data Source](#data-cleaning-and-preparation)
 - [Results and Findings](#results-and-findings)
 - [Using M Language](#using-m-language)

## Data Overview
Movie Data: The primary dataset used for this analysis is the "Movie Data.xmls" file, containing detailed information about each movie's performance, actors, directors, and other relevant details. The results are in the new file that has a new spreadsheet "Dashboard" with the charts and slicers representing data analysis: [Movies Data and Dashboard.xlsx](https://github.com/user-attachments/files/20746857/Movies.Data.and.Dashboard.xlsx)

## Tools

Excel Power Query for Data Cleaning.
Excel Pivot Tables for Data Analysis, Creating Reports, and Visualizations.

## Data Cleaning and Preparation
In the initial data preparation phase, we performed the following tasks:

  Data loading and inspection.
  Handling errors, handling missing values.
  Data cleaning and formatting. 

## Results and Findings

As an example, I identified the best and the worst movies by ROI: 
![image](https://github.com/user-attachments/assets/6dcecf6f-4935-4ab4-9fc7-e8f4cec1102d)

The dashboard features slicers that enable users to view information on revenues generated by actors in specific genres for a particular year.
![image](https://github.com/user-attachments/assets/98f0dce7-2a2c-4a32-b139-a844d8848769)

## Using M Language

In my Power Query work, I faced several technical challenges.

First, after grouping data, I needed to add an index column within each subgroup. Since Power Query does not natively support adding an index inside grouped tables, I had to write a custom M function to extract, transform, and re-expand each nested table with its local indexing. This operation required a precise understanding of the Table. Group and Table.AddIndexColumn functions.

`= Table.Group(#"Removed Columns3", {"owner_name"}, {{"Count", each Table.AddIndexColumn(_, "Index", 1,1)}})`

Second, I needed to extract a datetime value and convert it into a readable text string that combined the weekday name, date, and time. This required using DateTime.ToText with custom formatting, and ensuring consistency across time zones and data types. These tasks highlighted the complexity of the M language when handling advanced transformations.

` = Table.TransformColumns(#"Duplicated Column", {{"appointment_datetime - Copy", each Text.Combine({DateTime.ToText(_, "dddd"), DateTime.ToText(_, "MMMM d, yyyy h:mm tt")}, ", "), type text}})`

