<div align="center">
  <table style="margin-left:auto; margin-right:auto; border-collapse: collapse">
    <tr>
      <td align="left" style="border: none">
        <img src="images/SHLogo.jpg" alt="Image Description" width="150" height="150">
      </td>
      <td align="center" style="border: none">
        <h1>FOOD PRICES ANALYSIS IN NIGERIA<br>(CASE STUDY: 2002-2023)</h1>
      </td>
    </tr>
  </table>
</div>

<div align="center"> <img src="images/foodprices%20cover.jpg" width=730> </div>

## <p align="center"/> **TABLE OF CONTENTS** </p>
1. [Project Overview](#project-overview)
2. [Project Objectives](#project-objectives)
4. [Tools & Technologies Used](#tools--technologies)
5. [Project Structure](#project-structure)
7. [Data Collection](#data-collection)
8. [Data Cleaning & Preprocessing](#data-cleaning--data-preprocessing)
9. [Methodology](#methodology)
10. [Results & Discussions](#results--discussions)
11. [Recommendations](#recommendations)    
12. [Future Work](#future-work)
13. [References](#references)
14. [Contact Information](#contact-information)
15. [Acknowledgements](#acknowledgements)

## PROJECT OVERVIEW
This project, my second capstone endeavor at the SkillHarvest Data Analytics Bootcamp, involves analyzing food price data for Nigeria sourced from the World Food Programme Price Database. As a group project where I serve as the team lead, our goal is to delve into trends, disparities, and factors influencing food prices. Ultimately, we aim to provide valuable insights for stakeholders and policymakers

## PROJECT OBJECTIVES
- Identify regional variations in food prices within Nigeria and analyze the factors contributing to these disparities.
- Provide insights for policymakers
- Evaluate food affordability and accessibility
- Compare inflation rates of food commodities of year to year

## TOOLS & TECHNOLOGIES
- Power BI for data cleaning, analysis and visualization

## PROJECT STRUCTURE
- /datasets: Contains the raw and processed data files
- /visualizations: Contains Power BI visualization files
- /images: Contains images used for creating Github documentations
- /videos: Contains video demonstration of the project dashboard capabilities

## DATA COLLECTION
The dataset used for this project contains food prices data for various commodities and regions in Nigeria [Check Datasource](https://data.humdata.org/dataset/wfp-food-prices-for-nigeria). It covers foods such as maize, rice, beans, fish, and sugar for different markets across the country.

<div align="center">
  <img src="images/dataset%20snapshot.PNG" alt="Image Description">
</div>

## DATA CLEANING & DATA PREPROCESSING
This section outlines the data preprocessing techniques employed to clean and prepare the dataset for analysis. Each technique addresses specific issues such as data formatting and data type standardization.

### <p align="center"> Data Formatting & Data Standardisation </p>
- Promoted the first row as header and deleted the next row immediately after it
- Renamed all the columns using sentence case
- Changed the data type for the "Date" column to a datetime type
- Renamed the second column, "admin 1" to "State"
- Renamed the third column, "admin 2" to "LGA"
- Changed the data type for the "Latitude" and "Longitude" columns to float
- Formatted the last column, "USD price" to 2 decimal places.
- Replaced every value of "Beans (niebe)" in the "Commodity" column with "Beans (white)"

<div align="center">
  <img src="images/dataformatting.PNG" alt="Image Description">
</div>

## METHODOLOGY
### <p align="center">Data Analysis</p>
- Identified factors influencing food prices, including market dynamics, supply chain disruptions, and economic factors.
- Utilized DAX measures to calculate key metrics such as average prices, same period last year comparisons, year-over-year growth, and average price for year-over-year comparisons.

**You will find below, some of the DAX measures that I created:**
```
DAX QUERY
**1. TO CALCULATE THE AVERAGE PRICE OF ALL THE FOOD ITEMS ACROSS THE YEARS**

Average Price of Food Item(s) = AVERAGE(wfp_food_prices_nga[Price])
```
```
DAX QUERY
2. TO CALCULATE THE YEAR OVER YEAR AVERAGE PRICE OF FOOD ITEMS

AvgPrice YoY% = 
VAR __PREV_YEAR = CALCULATE([Average Price of Food Item(s)], DATEADD('CALENDAR'[Date], -1, YEAR))
RETURN
	DIVIDE([Average Price of Food Item(s)] - __PREV_YEAR, __PREV_YEAR)
```
```
DAX QUERY
3. TO CALCULATE THE THE PREVIOUS YEAR AVERAGE PRICE BASED ON THE SELECTED(CURRENT) YEAR

SamePeriod LY = CALCULATE([Average Price of Food Item(s)],SAMEPERIODLASTYEAR('CALENDAR'[Date]))
```
```
DAX QUERY
5. CALCULATE YEAR OVER YEAR PERCENTAGE GROWTH OF AVERAGE PRICE OF FOOD ITEMS

YoY Growth = 
var _uparrow = UNICHAR(129129)
var _downarrow = UNICHAR(129131)
var _variancee = [Variance]
var _varpercent = [AvgPrice YoY%]*100
var _blank = isblank([AvgPrice YoY%])
return
if (_blank,"NIL",
if (_variancee>0, ROUND(_varpercent,2)&"% "&_uparrow, ROUND(_varpercent,2)&"% "& _downarrow))
```
```
DAX QUERY
4. TO CALCULATE THE DIFFERENCE BETWEEN THE AVERAGE PRICE OF FOOD ITEMS AS COMAPRED TO THE PREVIOUS YEAR

Variance = [Average Price of Food Item(s)]-[SamePeriod LY]
```

### <p align="center">Visualization Creation</p>
- Created visualizations to effectively communicate key findings and insights.
- Utilized charts, graphs, and other visual elements to present trends, patterns, and disparities in food prices.

**First, find below some of the report visualizations: However, for more details, [Watch the video here](https://drive.google.com/file/d/1RJsscFydDBy3Q3KyBYPrChOIvWu4rbVY/view?usp=drive_link)**
<div align="center">
  <img src="visualizations/foodprices%20report.PNG" alt="FoodPrices">
</div>
#
<div align="center">
  <img src="visualizations/metrics%20report.PNG" alt="Metrics">
</div>
#
<div align="center">
  <img src="visualizations/marketprod%20report.PNG" alt="MarketProduction">
</div>
#

## RESULTS & DISCUSSIONS
<div align="center">
  <img src="visualizations/Count%20of%20Prod%20States%20&%20Commodities%20by%20Date.PNG" alt="Image Description">
</div>

1. The number of states engaging in food production or agriculture saw a significant increase starting from 2015, with a 50% rise observed within 7 months
2. This surge in agricultural activity led to a subsequent increase in food production across the nation, highlighting the direct correlation between state involvement in agriculture and the availability of diverse food items.

<div align="center">
  <img src="visualizations/States%20Producing%20Power%20&%20Market%20Count.PNG" alt="Image Description">
</div>

3. Yobe and Borno states emerged as leaders with the highest count of markets, correlating with their status as top producers of unique food commodities. Each state experienced an impressive 82% increase in market count and food commodity production compared to others.

<div align="center">
  <img src="visualizations/Food%20Prices%20by%20Market%20&%20States.PNG" alt="Image Description">
</div>

4. Despite being among the least prolific states in terms of food production and market presence, Abia stands out for for its relatively expensive food items compared to other producing states, underscoring its market influence despite limited production volume

## RECOMMENDATIONS

|RECOMMENDATIONS|
|---------------|
|1. Conduct further analysis to understand the factors contributing to Abia's high average food prices despite its lower production and market presence. This insight can inform strategies to address affordability challenges and improve access to essential food items in the region.|
|2. Provide targeted support and resources to states like Yobe and Borno, which have emerged as leaders in market count and food commodity production. This can help maximize their potential and further strengthen their contributions to the agricultural sector.|
|3. Implement policies and initiatives that foster agricultural development and investment to sustain the surge in agricultural activity and subsequent food production growth.|


## FUTURE WORK
- Create a model to forecast prices of food items in Nigeria
- Refine project visualizations for better insights
- Explore additional datasets for broader analysis
- Collaborate with domain experts for deeper insights

## REFERENCES
- [World Food Programme Price Database](https://www.wfp.org/prices)

## CONTACT INFORMATION
For inquiries, please contact [Email](sunmolaadeyanju@gmail.com) or connect on [LinkedIn](https://www.linkedin.com/in/sunmolaadeyanju/).

## ACKNOWLEDGEMENTS
- Special thanks to [Mr. Temidayo](https://www.linkedin.com/in/temidayoayeni/) for his invaluable support and guidance.

