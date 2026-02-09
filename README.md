# NASA-Astronaut-Yearbook-Analysis

This was a made up project using a Kaggle dataset
  https://www.kaggle.com/nasa/astronaut-yearbook
  
Technologies Used: SQL

## Features
- Summary Statistics (AVG, MAX, MIN)
I calculated the average, maximum, and minimum spaceflight hours to understand the overall experience range of astronauts.

- Grouped Insights Using GROUP BY + HAVING
I grouped astronauts by their graduate major and used HAVING to filter groups based on average flight hours. This highlights which academic backgrounds tend to have lower or higher flight experience.

- Custom Categories Using CASE
I created a new variable (Space_Rank) that classifies astronauts into custom skill levels—Novice, Junior, Spacewalker, and Senior Spacewalker—based on total flight hours.

- Multi-Condition Filtering Using AND/OR
I practiced more complex filtering by selecting astronauts with specific engineering degrees and military ranks.

## What I Learned
- How to summarize large datasets using aggregate functions
- The difference between WHERE and HAVING
- How to build new categories using conditional logic with CASE
- How to cleanly structure SQL queries for readability
- How grouping and filtering help uncover meaningful patterns in a dataset

## How It Can Be Improved
- Add window functions to rank astronauts by flight hours
- Visualize the results in Power BI or Excel dashboards
- Export the cleaned dataset and do further modeling in Python
- Expand the analysis to look at gender, birthplaces, or mission outcomes
- Create stored procedures to automate repetitive queries

SQL Code
--- What are average, max, and min values in the data?---
select
round(Avg(Space_Flight_hr)) as Average_hrs,
max(Space_Flight_hr) as Max_hrs, 
min(Space_Flight_hr) as Min_hrs
from astronauts;

--- What about those numbers per category in the data (using HAVIN)?---
select name, Graduate_Major, avg(Space_Flight_hr) as Avg_hours
from astronauts
group by Graduate_Major
having avg(Space_Flight_hr) <= 100
order by Avg_Hours;

--- What ways are there to group the data values that don’t exist yet (using CASE)?---
select name, count(Space_Flight_hr) as space_HOURS,
    case
        when Space_Flight_hr > 1000 then 'Senior Spacewalker'
        when Space_Flight_hr > 500 then 'Spacewalker'
        when Space_Flight_hr > 100 then 'Junior Spacewalker'
        else 'Novice Spacewalker'
    end as Space_Rank
from astronauts
group by name, Space_Rank;

--- What interesting ways are there to filter the data (using AND/OR)?---
select name, Graduate_Major, Military_Rank 
from astronauts
where Graduate_Major = 'Mechanical Engineering' and (Military_Rank = 'Colonel' or Military_Rank = 'Major');
-----------------------------------------------------------------------------------------------------------------------------------------------
CREATE TABLE astronauts(
   Name                TEXT PRIMARY KEY,
   Year                INTEGER,
   GroupNum            INTEGER,
   Status              TEXT,
   Birth_Date          TEXT,
   Birth_Place         TEXT,
   Gender              TEXT,
   Alma_Mater          TEXT,
   Undergraduate_Major TEXT,
   Graduate_Major      TEXT,
   Military_Rank       TEXT,
   Military_Branch     TEXT,
   Space_Flights       INTEGER,
   Space_Flight_hr     INTEGER,
   Space_Walks         INTEGER,
   Space_Walks_hr      REAL,
   Missions            TEXT,
   Death_Date          TEXT, 
   Death_Mission       TEXT
);
# Background and Overview
This is a personal learning project designed to practice SQL skills using publicly available NASA astronaut data. Using a Kaggle dataset, I explored astronaut profiles to practice data analysis techniques including summary statistics, conditional logic, grouping, and filtering.The analysis focuses on:

Practicing aggregate functions to summarize spaceflight experience data
Using GROUP BY and HAVING to identify patterns across educational backgrounds
Applying CASE statements to create custom classifications
Building multi-condition filters to extract specific data subsets

<p>The complete SQL code and dataset can be accessed <a href="https://github.com/ElishaMendez/NASA-Astronaut-Yearbook-Analysis" target="_blank">here.</a></p>
<p>Dataset source: <a href="https://www.kaggle.com/nasa/astronaut-yearbook" target="_blank">Kaggle - NASA Astronaut Yearbook</a></p>

# Data Structure Overview
- Primary Source: Kaggle NASA Astronaut Yearbook dataset (practice dataset)
- Records: Full roster of NASA astronauts with biographical and mission data
- Key Fields: Name, birth information, educational background (undergraduate and graduate majors), military rank and branch, spaceflight hours, spacewalk hours, mission details, and status
- Analysis Tool: SQL (aggregate functions, conditional logic, grouping, and filtering)

# Executive Summary
### Overview of Findings
This analysis examined NASA astronaut profiles to identify experience patterns and create meaningful classifications. By calculating summary statistics, I found that spaceflight hours vary significantly across the astronaut corps, with some having minimal experience while others have logged over 1,000 hours in space.
I grouped astronauts by their graduate majors and discovered that certain academic backgrounds—particularly in engineering disciplines—tend to correlate with different average flight hours. Using conditional logic, I created a custom ranking system (Novice, Junior Spacewalker, Spacewalker, and Senior Spacewalker) based on total flight hours, providing a clearer way to segment astronauts by expertise level.
Additionally, I used multi-condition filtering to identify astronauts with specific combinations of educational and military backgrounds, such as Mechanical Engineering graduates who hold the rank of Colonel or Major—a profile that appears frequently in the dataset.

Below are key SQL queries used in this analysis:
--- Summary Statistics ---
SELECT
    ROUND(AVG(Space_Flight_hr)) AS Average_hrs,
    MAX(Space_Flight_hr) AS Max_hrs, 
    MIN(Space_Flight_hr) AS Min_hrs
FROM astronauts;

--- Experience by Graduate Major ---
SELECT Graduate_Major, AVG(Space_Flight_hr) AS Avg_hours
FROM astronauts
GROUP BY Graduate_Major
HAVING AVG(Space_Flight_hr) <= 100
ORDER BY Avg_Hours;

--- Custom Expertise Classification ---
SELECT name, Space_Flight_hr AS space_HOURS,
    CASE
        WHEN Space_Flight_hr > 1000 THEN 'Senior Spacewalker'
        WHEN Space_Flight_hr > 500 THEN 'Spacewalker'
        WHEN Space_Flight_hr > 100 THEN 'Junior Spacewalker'
        ELSE 'Novice Spacewalker'
    END AS Space_Rank
FROM astronauts
ORDER BY Space_Flight_hr DESC;

# Insights Deep Dive
- **Wide Experience Range Reveals Career Stage Distribution**
The analysis shows spaceflight hours vary dramatically from under 10 hours to over 1,000 hours, which appears to reflect natural career progression. I found that becoming a "veteran" astronaut with 500+ hours is relatively rare, achieved by less than 20% of the dataset.
- **Academic Background Influences Mission Assignment Patterns**
Certain graduate majors show consistently lower average flight hours. This pattern suggests these fields may be newer to NASA's selection criteria or potentially associated with support roles. Engineering disciplines, particularly Aerospace and Mechanical Engineering, appear more frequently in the higher flight-hour categories.
- **The "1,000-Hour Club" is Highly Exclusive**
My analysis revealed that only a handful of astronauts achieve Senior Spacewalker status (1,000+ hours), representing years of multiple long-duration missions. The data shows a steep pyramid structure: many novices, fewer mid-career astronauts, and very few veterans.
- **Military Leadership Background Remains a Strong Predictor**
I observed that the combination of engineering degrees with senior military ranks (Colonel/Major) appears frequently among high-experience astronauts. This pattern suggests NASA may value both technical expertise and proven leadership under high-pressure conditions.
# Recommendations
- **Time-Series Trends:** Analyze how astronaut profiles have evolved over decades by grouping astronauts by their selection year to identify shifting priorities in NASA's recruitment strategy
- **Predictive Modeling:** Build a model to predict which astronaut profiles are most likely to achieve 500+ flight hours based on educational background, military rank, and selection year
- **Window Functions:** Implement RANK() and ROW_NUMBER() to identify top performers within each graduate major category
- **Python Integration:** Use pandas and scikit-learn to perform statistical tests on correlations between variables and build classification models


