## Startup Investment Data Analysis


### About the Dataset
**Overview**
- This dataset contains 5,000 records of startup growth and investment data across various industries.
- It provides insights into funding trends, valuation, and investor activity for startups globally.
- The dataset is ideal for machine learning models, data analysis, and trend predictions in the startup ecosystem.

**Dataset Features**
- Startup Name	Name of the startup
- Industry	The industry sector (e.g., AI, Fintech, HealthTech, etc.)
- Funding Rounds	Number of funding rounds received by the startup
- Investment Amount (USD)	Total investment received in USD
- Valuation (USD)	Estimated company valuation in USD
- Number of Investors	Total number of investors backing the startup
- 	Country where the startup is based
- 	Year Founded	Year when the startup was founded
- 	Growth Rate (%)	Annual growth rate percentage
---------------------------

**Use Cases**
- Investment Trend Analysis – Analyze funding trends and investor interest across industries.
- Startup Valuation Prediction – Train machine learning models to predict valuations based on funding rounds.
- Market Research – Identify booming industries and successful startup ecosystems.
- Investor Decision Making – Help venture capitalists and angel investors make data-driven decisions.

**Possible Explorations**
- What industries attract the most funding?
- How does startup valuation grow over time?
- Which countries have the fastest-growing startups?
- What is the correlation between funding rounds and growth rate?
- This dataset is synthetically generated but follows realistic investment patterns to support research and analysis. 🚀

-----------------------------------------------



```SQL
DROP TABLE startups;
CREATE TABLE startups
(
startup_name VARCHAR(255),
industry VARCHAR(255),
funding_rounds BIGINT,
investment_amount  BIGINT,
valuation  BIGINT ,
number_of_investors INT ,
country VARCHAR(255),
year_founded INT,
growth_rate  FLOAT
);
```

DATA CLEANING

```SQL
SELECT 
* 
FROM startups;
```

```SQL
SELECT 
    *
FROM startups
WHERE startup_name IS NULL
OR industry IS NULL
OR funding_rounds IS NULL
OR investment_amount IS NULL
OR valuation IS NULL
OR number_of_investors IS NULL
OR country IS NULL
OR year_founded IS NULL
OR growth_rate IS NULL;
```

*our data had no missing values*

---------------------------------------------------
**ANALYSIS***

1. Find the total number of startups in the dataset.

```SQL
SELECT 
     
     COUNT(startup_name) AS total_startups
FROM startups;
```
2. Most funded industry by investment_amount

```SQL
SELECT
      industry,
        SUM(investment_amount) AS total_investment_amount
FROM startups
GROUP BY 1
ORDER BY 2 DESC
```

3. Highest valuated industry by valuation amount 

```SQL
SELECT 
    industry,
    SUM(valuation) AS total_valuation
FROM startups
GROUP BY 1
ORDER BY 2 DESC
```

5. Segmenting funding rounds into series

```SQL
WITH funding_series
AS
(
SELECT 
    funding_rounds,
    CASE 
        WHEN funding_rounds BETWEEN 0 AND 1 THEN 'Series A'
        WHEN funding_rounds BETWEEN 2 AND 4 THEN 'Series B'
        WHEN funding_rounds BETWEEN 5 AND 7 THEN 'Series C'
        ELSE 'Series D and above'
    END AS series,
    investment_amount
FROM startups
)
SELECT 
    series,
    SUM(investment_amount) AS total_investment_amount
FROM funding_series
GROUP BY 1
ORDER BY 2 DESC
```

6. Number of investors per industry
```SQL
SELECT
    industry,
    SUM(number_of_investors) AS total_investors
FROM startups
GROUP BY 1
ORDER BY 2 DESC
```

7. Number of startups founded per year
```SQL
SELECT 
      year_founded,
      COUNT(startup_name) AS total_startups
FROM startups
GROUP BY 1
ORDER BY 1 ASC
```
8. Countries with the highest number of startups
```SQL
SELECT
    country,
    COUNT(startup_name) AS total_startups
FROM startups
GROUP BY 1
ORDER BY 2 DESC
```

9. How year_founded affects funding
```SQL
SELECT 
    year_founded,
    SUM(investment_amount) AS total_investment_amount
FROM startups
GROUP BY 1
ORDER BY 2 DESC
```

10. Correlation between investment_amount and growth_rate
```SQL
SELECT 
    CORR(investment_amount, growth_rate) AS correlation
FROM startups
```
--------------------------------------------

### Findings

1. **Total Number of Startups**:
   - The total number of startups was 5000.

2. **Most Funded Industry by Investment Amount**:
   - Healthcare industy was the most funded industry followed by E-commerce.

3. **Highest Valuated Industry by Valuation Amount**:
- E-commerce was had the highest valuation io our dataset
4. **Segmenting Funding Rounds into Series**:
   - Funding rounds are segmented into series, and the total investment amount for each series is calculated
   - Giving us Series A , B , C and D & Beyond.

5. **Number of Investors per Industry**:
   - The total number of investors per industry is calculated.
   - Healthcare, SaaS and Bitcoin were the top three in terms of investors.

6. **Number of Startups Founded per Year**:
   - The number of startups founded each year is calculated.
   - It ranges from the previous year's data

7. **Countries with the Highest Number of Startups**:
   - The countries with the highest number of startups are identified.
   - Austrlia, Singapore and Brazil lead the way in terms of startups there.

8. **How Year Founded Affects Funding**:
   - The relationship between the year founded and the total investment amount is analyzed.
   - Different shows different amounts of investment

9. **Correlation Between Investment Amount and Growth Rate**:
   - The correlation between investment amount and growth rate is calculated.
   - We obtaine a perfect negative pearson correlation between investment amount and growth rate but other unkown factors have a role

---------------------------------------------------------

### Recommendations

1. **Focus on High-Funded Industries**:
   - Invest more resources in industries that have shown high total investment amounts, as they are likely to attract more funding.

2. **Target High-Valuation Industries**:
   - Prioritize industries with high total valuations for potential investments, as they indicate strong market value.

3. **Optimize Funding Strategies**:
   - Tailor funding strategies based on the segmented series to maximize investment returns.

4. **Engage with Active Investors**:
   - Collaborate with industries that have a high number of investors to leverage their networks and expertise.

5. **Monitor Startup Trends**:
   - Keep track of the number of startups founded each year to identify emerging trends and opportunities.

6. **Expand to High-Startup Countries**:
   - Consider expanding operations or investments in countries with a high number of startups to tap into vibrant ecosystems.

7. **Analyze Funding Patterns**:
   - Study the relationship between the year founded and funding to understand historical funding patterns and predict future trends.

8. **Leverage Growth Correlations**:
   - Utilize the correlation between investment amount and growth rate to identify startups with high growth potential and allocate resources accordingly.
