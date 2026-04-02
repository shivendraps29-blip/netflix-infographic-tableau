# netflix-infographic-tableau
Tableau infographic dashboard on 8,807 Netflix titles —  genre, cast, ratings &amp; country analysis with Python  preprocessing for data cleaning before visualization.


# 🎬 Netflix Infographic | Tableau + Python Project

## About This Project

This started from a simple question — what does Netflix's 
content library actually look like when you break it down 
properly? Not just "how many shows are there" but which 
countries are producing the most, who keeps showing up 
in the cast across multiple titles, which genres dominate 
by year, and how content volume has shifted over time.

The dataset had 8,807 rows and 12 columns covering both 
movies and TV shows. Before anything went into Tableau, 
I had to fix two major structural problems in the data 
using Python — which is why this repo has both a 
Tableau file and a preprocessing notebook.

---

## The Data Problem I Had to Solve First

Two columns in the raw dataset were the main issue:

**Genre column** — every title had multiple genres 
crammed into one cell as a comma-separated string. 
Something like "Dramas, International Movies, Thrillers" 
all in one field. You can't count genre frequency 
meaningfully when the data is structured like that.

Fixed it by splitting the listed_in column and using 
pandas explode() to give each genre its own row. 
Then grouped by Genre and counted unique titles — 
so a title with 3 genres contributes once to each, 
not inflating any single genre count.

**Cast column** — exact same problem. Multiple actors 
in one cell. Exploded that too, then grouped by cast 
member and counted how many unique titles each 
person appeared in — which is what drives the 
Top Cast Members chart in the dashboard.

Both fixes were done separately for Movies and TV Shows 
so the dashboards could filter independently by type.

The cleaned file was exported as 
updated_netflix_titles.csv and fed into Tableau.

---

## What the Dashboard Shows

Two separate dashboards — one for Movies, one for TV Shows — 
both filterable by year using a Select Year parameter.

**Total Content KPI**
A sparkline showing total count for the selected year 
with percentage difference vs the previous year. 
So you can instantly see if Netflix added more or 
fewer titles compared to last year.

**Country Filmed Map**
Bubble map showing where content was produced globally. 
The US dominates but India, UK, Japan and South Korea 
have notable presence — visible clearly on the map.

**Most Frequent Genres**
Horizontal bar chart of top genres for the selected year. 
International content consistently ranks high which 
reflects Netflix's global content strategy.

**Top 10 Cast Members**
Bar chart of actors/actresses with the most title 
appearances. This only works cleanly because of the 
cast explosion done in preprocessing — without that 
step the data would be unusable for this chart.

**Content Rating Breakdown**
Bar chart comparing rating distribution 
(TV-MA, TV-14, R, PG-13 etc.) for the selected year 
vs the previous year.

---

## Tableau Calculated Fields Used

**Movies Dashboard**
- CY Movies — distinct movie count for selected year
- PY Movies — distinct movie count for previous year
- % Diff Movies — percentage change between CY and PY
- Min/Max Movies — window functions for sparkline bounds

**TV Shows Dashboard**
- CY TV Shows — distinct TV show count for selected year
- PY TV Shows — distinct count for previous year
- % Diff TV Shows — percentage change CY vs PY
- Min/Max TV Shows — window functions for sparkline bounds

---

## Python Preprocessing — What I Did

Libraries used: pandas only

Steps in order:
1. Read netflix_titles.csv into a DataFrame
2. Split listed_in column on ', ' and exploded into rows
3. Reset index after explosion
4. Grouped by Genre, counted unique titles per genre
5. Separated into Movies and TV Shows DataFrames
6. Repeated genre count for each type separately
7. Exploded cast column the same way
8. Grouped by cast member, counted unique title appearances
9. Exported cleaned data to updated_netflix_titles.csv

The key decision was counting unique titles per genre/cast 
rather than raw row counts — otherwise titles with many 
genres or large casts would inflate the numbers unfairly.

---

## Tools Used

- **Tableau Desktop** — dashboard design, calculated 
  fields, parameters, map visualization, sparklines
- **Python (pandas)** — data preprocessing, 
  column explosion, groupby aggregations
- **Jupyter Notebook** — preprocessing workflow

---

## Dataset

Netflix titles dataset from Kaggle — 8,807 rows, 
12 columns covering show_id, type, title, director, 
cast, country, date_added, release_year, rating, 
duration, listed_in, and description.

## Screenshots

![nt](https://github.com/user-attachments/assets/0f414d87-e342-4e73-bdd2-9c34538f0b49)

![nt2](https://github.com/user-attachments/assets/1366df2c-d8e1-49c0-aaff-cf1a5c6b31c4)

![nt3](https://github.com/user-attachments/assets/887eae72-0327-448c-a192-f400ffa23c97)


