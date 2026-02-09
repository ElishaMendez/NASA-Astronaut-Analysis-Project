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
This practice project allowed me to apply SQL fundamentals to a real-world dataset. I calculated summary statistics on spaceflight hours, grouped astronauts by their graduate majors to explore experience patterns, and created a custom ranking system based on total flight hours.
Key techniques practiced:
- Using AVG, MAX, and MIN to understand data ranges
- Applying GROUP BY with HAVING to filter aggregated results
- Building CASE statements to create new categorical variables
- Combining AND/OR logic for complex filtering

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

# Recommendations



