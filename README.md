# WHR Happiness Corruption COVID19
 Attempt to analyze World Happiness Report Data in Python and identify stories

## Background
- The World Happiness Report is an annual publication produced by the the Sustainable Development Solutions Network (SDSN) and The Center for Sustainable Development at Columbia University.
- It was first produced as a reponse to a UN General Assembly 2011 Resolution which invited national governments to “give more importance to happiness and well-being in determining how to achieve and measure social and economic development.” 
- Data is collected in partnership with the Gallup World Poll team
- Data sources used to develop the WHR include:
- Gallup World Poll
- World Risk Poll (Lloyd's Register Foundation)
- Covid Data Hub (Imperial College London // YouGov)

## Methodology
1. Accessed the World Happiness Report (https://worldhappiness.report/) to review methodology and types of data included
2. Downloaded dataset from Kaggle
3. The Happiness Index includes questions about perceptions about corruption, social support, healthy life expectancy, generousity, and freedom. So I sought to address the following questions:
- how do perceptions of corruptions by the public compare with expert opinions on global corruption (via Transparency International Corruption Perception Index)?
- how do these elements compare between countries with questionably lower numbers of COVID deaths and COVID cases? 
- if data is available, this analysis could be supplemented with information about levels of restriction in each country

## Datasets:
- World Happiness Report: https://www.kaggle.com/ajaypalsinghlo/world-happiness-report-2021
- Transparency International Corruption Index: https://www.transparency.org/en/cpi/2020/index/nzl
- Novel Coronavirus (COVID-19) Cases and Deaths (JHU CSSE): https://github.com/CSSEGISandData/COVID-19
- World Bank Population Estimates and Projections: https://datacatalog.worldbank.org/dataset/population-estimates-and-projections


## Methods:

I mapped the country names across the different datasets. In the instances where country names differed, I mapped the following:

| Base                    | Alternative Spellings               |
|-------------------------|-------------------------------------|
| Czech Republic          | Czechia                             |
| United States           | US                                  |
| United States           | United States of America            |
| Taiwan                  | Taiwan*                             |
| Taiwan                  | Taiwan Province of China            |
| South Korea             | Korea, South                        |
| South Korea             | Korea                      |
| North Korea             | Korea, North                        |
| North Cyprus            | Turkish Republic of Northern Cyprus |
| North Cyprus            | Northern Cyprus                     |
| Ivory Coast             | Cote d'Ivoire                       |
| Hong Kong               | Hong Kong S.A.R. of China           |
| Palestinian Territories | West Bank and Gaza                  |
| Myanmar                 | Burma                               |
| Eswatini                | Swaziland                           |
| Congo (Brazzaville)     | Republic of Congo                   |
| Congo (Kinshasa)        | Democratic Republic of Congo        |
| Slovaka    | Slovak Republic                   |
| Russia     | Russian Federation       |
| Egypt  | Egypt, Arab Rep                   |
| Gambia     | Gambia, The       |

I extracted cumulative case and death data as of 31 December 2020 from Novel Coronavirus (COVID-19) Cases and Deaths (JHU CSSE) and the 2021 Corruption Perception Index (CPI) Score from Transparency International Corruption Index and added them to the a new combined file containg World Happiness Report 2021 indicators

I mapped CPI scores to WHR Perception of Corruption Scores (100-cpi_score/100) and added them to the combined file
- <i>NOTE: This is my rough mapping - not an evidence-based method to compare these scores</i>

I added World Bank 2020 Population estimates and used them, in conjuction with CCSE data, to derive cases and deaths per 100k population, as of 31 Dec 2020 (e.g. number of cases/population *100000), and added them to the combined file
- <i>NOTE: World Bank data did not include population data on Taiwan or North Cyprus. Taiwanese population data was taken from UN Population division estimates (https://population.un.org/wpp/) and North Cyprus data was taken from https://www.ticaret.gov.tr/</i>

I extracted a list of OECD countries and matched countries to their OECD status in the combined file. 
  
In the combined file, I removed data irrelevant to this analysis including:                         
- Standard error of ladder score            
- upperwhisker                                
- lowerwhisker
- Explained by: Log GDP per capita
- Explained by: Social support
- Explained by: Healthy life expectancy
- Explained by: Freedom to make life choices
- Explained by: Generosity
- Explained by: Perceptions of corruption
- Dystopia + residual  
    
####Data Notes:
- North Cyprus is only recognized by Turkey, and thus excluded from the analysis. 
- Turkmenistan was not included in the JHU CSSE because it claims no COVID-19 cases or deaths, and thus do not report. Thus, in the combined dataset, I mark it as 0 deaths and 0 cases to compare '0' reporting with perception of corruption scores in this analysis.
- North Korea was not included in the World Happiness Report
- Palestinian Territories were not included in the Transparency International Corruption Index 

## Limitations
- I attempted to do the entire project, from cleaning to analysis, in Python (see notebook happiness-2021-cleaning attempt); however, I had several challenges trying to reformat the data in the time frame given using my current python skillset. So, I combined the various elements needed for analysis and made the necessary calculations in excel first. I then imported the csv file into my analysis workbook (happiness-2021-analysis).
- Technically, Transparency International does not provide full rights to modify and re-analyze the data in the way I've done in this analysis. Thus, this story and its findings, where relevant to TI's data, should be considered illustrative.
- I was not able to do a time-series analysis yet, but it would be interesting to see if corruption perceptions shifted pre-/post-COVID - noting that perception of corruption is influenced by several factors
- With additional time, I'd like to see how happiness compares between island nations
 
## Key Findings
- Despite being the 4th happiest country in the world, Iceland has the highest corruption perception score amongst all Nordic countries. It is ranked 6th most corrupt based on public perception and 10th most corrupt based on expert opinion in Western Europe.
- Of the top 50 countries reporting the lowest COVID cases and deaths, Singapore (0.082) and New Zealand (0.242) have the lowest corruptions scores. The average public perception of corruption for this group is 0.722.
- Using New Zealand as a comparator (7 deaths/100k and 43 cases/100k):
    - 65% (n=23) countries reporting less than 7 deaths/100k population and have higher than average corruption score across both public and expert opinions are in Sub-Saharan Africa.
    - 50% (n=7) of countries reporting less than 44 cases/100k population and have higher than average corruption score across both public and expert opinions are in Sub-Saharan Africa.
    - Turkmenistan reported 0 cases and 0 deaths. It has the 17th highest perceived corruption score in the world.
    - Of the 20 most corrupt countries in the world, based on public perception, 40% are in Central and East Europe.