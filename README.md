# 📁 Excel Data Analytics Portfolio

*Two Excel projects built on a data-related job postings dataset*

> **Project 1** — an interactive salary calculator powered by array formulas
> **Project 2** — a Power Pivot / DAX analysis of skills vs. salary

## 📑 Contents

- [Project 1: Data Science Salary Calculator](#project-1-data-science-salary-calculator--interactive-excel-dashboard)
- [Project 2: Salary vs. Skills Analysis](#project-2-salary-vs-skills-analysis--power-pivot--dax-dashboard)

---
---

# 🧮 Project 1: Data Science Salary Calculator
### Interactive Excel Dashboard

## 🎯 Project Overview

An **interactive salary lookup tool** that helps data professionals estimate expected compensation based on **job title, country, and employment type**.

> 🧩 **Business problem:** Job seekers often can't easily find salary data broken down by role, location, and work type together.
>
> 🚀 **Goal:** Let a user pick a job title, country, and work type from dropdowns and instantly see the matching job count, median salary, and how that role compares to similar roles, work types, and locations.

## 🗂️ Dataset

Data lives in a table named `jobs` with (at minimum):

| Column | Description |
|:--|:--|
| `job_title_short` | Standardized job title (e.g., "Data Scientist") |
| `job_country` | Country of the job posting |
| `job_schedule_type` | Employment type (Full-time, Part-time, Contractor, Internship, Temp work, or combinations) |
| `salary_year_avg` | Annualized average salary |

The dataset contains thousands of individual job postings (counts like `5,638` and `6,480` appear in the calculations), likely aggregated from online job platforms.

> 💡 Only columns visible in the formulas are documented; the raw dataset may contain additional fields.

## 📊 Dashboard & Visualizations

The `Salary_Calculator` sheet is a three-input control panel with outputs beneath each control.

**🔽 Input controls** *(Data Validation dropdowns)*
`Job Title` · `Country` · `Type` — these drive every chart and KPI on the sheet.

**📈 Visualizations**

| Chart | What it shows |
|:--|:--|
| **Job Title bar chart** | Median salary across related roles, selected title highlighted |
| **Country map** *(Bing Maps chart)* | Highlights the selected country geographically |
| **Type bar chart** | Median salary by employment type, selected type highlighted |

**🧮 KPI cards**
`Median Salary` · `Top Job Platform` · `Job Count` — all recalculated for the selected combination.

**🔗 How it works together**
The three dropdowns are the single source of truth. Changing any of them recalculates the underlying array formulas, which update the KPI cards and re-render all three charts — a fully interactive salary explorer.

## 🛠️ Excel Features & Skills Demonstrated

| Skill | How it was used |
|:--|:--|
| **Data Validation** | Dropdown lists for Job Title, Country, Type drive the dashboard |
| **Array Formulas** | `COUNT(IF(...))` and `MEDIAN(IF(...))` evaluate multiple conditions across the table |
| **Logical Functions** | Boolean conditions multiplied together to simulate AND logic inside array formulas |
| **Text Functions** | `SEARCH()` + `ISNUMBER()` to match employment type within combined text values |
| **Statistical Functions** | `COUNT()`, `MEDIAN()` inside array formulas |
| **Lookup Functions** | `XLOOKUP()` to retrieve values based on selection |
| **Dynamic Arrays** | `SORT(FILTER(...))` to remove errors and rank results |
| **Sorting & Filtering** | Helper columns sort titles, countries, and types with their counts/salaries |
| **Excel Tables** | Structured references (`jobs[job_title_short]`) |
| **Charts** | Dynamic bar charts and a geographic map chart |
| **Dashboard Design** | Linked charts, KPI cards, and controls in one cohesive layout |
| **Multi-sheet Structure** | `Data`, `Salary_Calculator`, `Data_Validation`, `country` sheets |

## 💡 Key Insights

- 📌 Machine Learning Engineer and Data Scientist roles pay noticeably more than Data Analyst roles.
- 📌 Full-time work pays the most compared to Part-time, Contractor, Internship, and Temp work.
- 📌 Salary varies meaningfully by country, visible instantly via the map.
- 📌 Useful for benchmarking offers or deciding between full-time vs. contractor work.

## 🏷️ Skills Highlighted

`Data Validation` · `Array Formulas` · `COUNT` · `MEDIAN` · `IF` · `SEARCH` · `ISNUMBER` · `SORT` / `FILTER` · `XLOOKUP` · `Excel Tables` · `Formula-Driven Charts` · `Dashboard Design` · `Multi-Sheet Workbook`

---
---

# 🧠 Project 2: Salary vs. Skills Analysis
### Power Pivot & DAX Dashboard

## 🎯 Project Overview

Analyzes the relationship between **job skills, job titles, countries, and salaries** using a **Power Pivot** data model and **DAX**.

> 🧩 **Business problem:** Which skills are most in-demand, which pay the most, and does knowing more skills actually correlate with higher pay?
>
> 🚀 **Goal:** Build a relational data model (jobs ↔ skills) and use DAX measures with PivotTables/PivotCharts to explore U.S. vs. non-U.S. pay, the skills–salary relationship, skill demand, and pay per skill.

## 🗂️ Dataset

A **Power Pivot Data Model** with two related tables:

| Table | Key Columns |
|:--|:--|
| `data_jobs_salary` | `job_id`, `job_title_short`, `job_title`, `job_location`, `job_via`, `job_schedule_type`, `search_location`, `job_posted_date`, `job_country`, `salary_rate`, `salary_year_avg`, `salary_hour_avg`, and others |
| `data_jobs_skills` | `job_id`, `job_skills` (one row per skill per job posting) |

**🔗 Relationship:** One-to-many on `job_id` *(one job can require many skills)*.

## 📊 Dashboard & Visualizations

**🔽 Slicers:** `Country` and `Job Title`, shared across all visuals.

| Visual | What it shows |
|:--|:--|
| **PivotTable** — *Median Salary by Job Title (USA vs. Non-USA)* | Median Salary USA, Median Salary Non-USA, and overall Median salary side by side; U.S. pay is consistently higher |
| **Scatter chart** — *"Do more skills mean more money for data nerds?"* | Median salary vs. average skills requested per role, with a trendline showing a positive relationship · filterable by Country |
| **Bar chart** — *"What are the top skills of Data Nerds?"* | Top 10 skills ranked by frequency in postings (SQL ~53%, Excel ~41% lead) · filterable by Job Title and Country |
| **Combo chart** — *"What's the pay of top 10 skills?"* | Bars for median salary per skill, markers for skill likelihood — shows the most in-demand skills aren't always the highest paid · filterable by Job Title and Country |

**🔗 How it's organized**
All visuals share the same data model and slicers, so filtering by role or country updates the salary table, scatter plot, and both skills charts together.

## 🛠️ Excel Features & Skills Demonstrated

| Skill | How it was used |
|:--|:--|
| **Power Pivot / Data Model** | Two tables related via `job_id` |
| **Table Relationships** | One-to-many between salary and skills tables |
| **DAX — `CALCULATE()`** | Country-conditional median salary measure |
| **DAX — `CROSSFILTER()`** | Bidirectional filtering across the relationship for skill-based salary measure |
| **DAX — `COUNT()`** | Base "Skill count" measure |
| **Calculated Measures** | "Skills per job" and "Skill likelihood" |
| **PivotTables & PivotCharts** | Salary comparisons, scatter chart with trendline, bar and combo charts |
| **Slicers** | Country and Job Title, synchronized across visuals |
| **Data Model Diagram View** | Used to design/verify relationships |
| **Dashboard Design** | Multiple cross-filtered visuals answering related questions |

## 💡 Key Insights

- 📌 U.S. salaries consistently exceed non-U.S. salaries across every job title.
- 📌 More required skills correlates with higher salary (positive trendline).
- 📌 SQL and Excel are the most in-demand skills, but Python and Oracle pay the most among the top 10 — demand and pay aren't the same thing.
- 📌 Useful for prioritizing which skills to learn next: foundational skills for employability, higher-value skills for pay.

## 🏷️ Skills Highlighted

`Power Pivot` · `Data Model` · `One-to-Many Relationships` · `DAX` · `CALCULATE` · `CROSSFILTER` · `COUNT` · `PivotTables` · `PivotCharts` · `Slicers` · `Trendlines` · `Combo Charts` · `Dashboard Design`
