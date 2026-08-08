# Salary vs. Skills Analysis

<img width="1298" height="357" alt="Screenshot 2026-08-07 195220" src="https://github.com/user-attachments/assets/eddacc52-b7f7-434c-ae4d-7ffd38c156fd" />


## Introduction

This salary vs. skills analysis was created to help job seekers and learners understand which skills are most in-demand for data roles, which skills pay the most, and whether acquiring more skills actually correlates with a higher salary. Users can filter the analysis by job title and country to instantly see how skill demand and pay shift across different markets.

The data is from my Excel course, which provides a foundation in analyzing data using this powerful tool. The dataset contains detailed information on job postings and their required skills, modeled as a relational data set connected through Power Pivot.

### Excel Skills Used

The following Excel skills were utilized for analysis:

- **🗃️ Power Pivot / Data Model**
- **🔗 Table Relationships**
- **🧮 DAX Measures (CALCULATE, CROSSFILTER, COUNT)**
- **📊 PivotTables**
- **📉 PivotCharts**
- **🔎 Slicers**

### Data Jobs Dataset

The dataset used for this project contains real-world data science job information, modeled as two related tables in Power Pivot. The dataset is available via my Excel course, which provides a foundation for analyzing data using Excel. It includes detailed information on:

- **👨‍💼 Job titles**
- **💰 Salaries**
- **🌍 Countries**
- **🛠️ Required skills**

**Relationship:** The two tables (`data_jobs_salary` and `data_jobs_skills`) are linked in a one-to-many relationship on `job_id` — one job can have many associated required skills.

## Dashboard Build

### 🗃️ Data Model

<img width="626" height="477" alt="Screenshot 2026-08-07 195443" src="https://github.com/user-attachments/assets/4d294cc0-4d4d-411c-b9eb-eefe8755e419" />


- 🛠️ **Excel Features:** Utilized Power Pivot's Diagram View to visually design and verify the relationship between the two tables.
- 🔗 **Relationship:** One-to-many relationship configured between `data_jobs_salary` and `data_jobs_skills` on `job_id`.
- 🎯 **Purpose:** Allows salary data and skills data to be analyzed together despite living in separate tables.

### 📉 Charts

#### 📈 Scatter Chart - "Do more skills mean more money for data nerds?"

<img width="1222" height="354" alt="Screenshot 2026-08-07 195008" src="https://github.com/user-attachments/assets/9b60c63a-350f-415a-8219-f67e38bebcb5" />


- 🛠️ **Excel Features:** Utilized a PivotChart (scatter) with a linear trendline.
- 🎨 **Design Choice:** X-axis shows median salary, Y-axis shows average skills requested per job title.
- 📉 **Data Organization:** Each data point represents a job title, plotted by salary and skill count.
- 💡 **Insights Gained:** Confirms a positive relationship — roles that request more skills on average also tend to pay more, with Senior Data Engineer and Data Engineer requiring the most skills and paying among the highest.
- 🔎 **Interactivity:** Filterable by the Country slicer.

#### 📊 Bar Chart - "What are the top skills of Data Nerds?"

<img width="1099" height="323" alt="Screenshot 2026-08-07 194834" src="https://github.com/user-attachments/assets/8de3c115-a07e-4ba7-b3e2-0274e6399e5b" />


- 🛠️ **Excel Features:** Utilized a PivotChart (horizontal bar chart) ranking skills by frequency.
- 🎨 **Design Choice:** Top 10 skills ranked by "Skill Count in Job Postings" (likelihood a posting requires that skill).
- 📉 **Data Organization:** Skills sorted in descending order of demand.
- 💡 **Insights Gained:** SQL (~53%) and Excel (~41%) are the most frequently requested skills, far ahead of the rest.
- 🔎 **Interactivity:** Filterable by both Job Title and Country slicers.

#### 📊 Combo Chart - "What's the pay of top 10 skills?"

<img width="515" height="327" alt="Screenshot 2026-08-07 195142" src="https://github.com/user-attachments/assets/3953b840-de33-40e4-b1d8-b5df71dbc32f" />

- 🛠️ **Excel Features:** Utilized a dual-axis PivotChart (bars + markers).
- 🎨 **Design Choice:** Bars show median salary per skill, diamond markers show skill likelihood.
- 📉 **Data Organization:** Top 10 skills displayed side by side for salary comparison.
- 💡 **Insights Gained:** The most frequently requested skills (SQL, Excel) aren't necessarily the highest paid — Python and Oracle show the highest median salaries (~$97,000) despite lower/moderate demand.
- 🔎 **Interactivity:** Filterable by both Job Title and Country slicers.

### 📋 PivotTable: Median Salary by Job Title (USA vs. Non-USA)

<img width="882" height="299" alt="Screenshot 2026-08-07 195055" src="https://github.com/user-attachments/assets/6c6208a1-28e5-4100-9128-6cf747d86c5f" />


- 🛠️ **Excel Features:** PivotTable with three DAX measures placed side by side in the Values area.
- 🎯 **Tailored Insights:** Shows Median Salary USA, Median Salary Non-USA, and overall Median salary for each job title.
- 💡 **Insights Gained:** U.S. salaries consistently exceed non-U.S. salaries across every job title (e.g., Cloud Engineer: $115,000 USA vs. $89,100 Non-USA).
- 🔎 **Interactivity:** Filterable by the Country slicer.

### 🧮 DAX Measures

#### 🌍 Median Salary USA
=CALCULATE([Median salary],data_jobs_salary[job_country]="United States")
- 🔍 **Conditional Aggregation:** Uses `CALCULATE()` to filter the base Median salary measure to only U.S.-based postings.
- 🎯 **Formula Purpose:** Powers the "Median Salary USA" column in the comparison PivotTable.

🍽️ Background Screenshot

<img width="542" height="425" alt="Screenshot 2026-08-07 195908" src="https://github.com/user-attachments/assets/ddcf5ce6-9595-420c-bb1d-acd921436a51" />


#### 🔗 Median Salary by Skill
=CALCULATE([Median salary],CROSSFILTER(data_jobs_salary[job_id],data_jobs_skills[job_id],Both))
- 🔍 **Cross-Table Filtering:** Uses `CROSSFILTER()` to allow the skills table to filter the salary table in both directions across the relationship.
- 📊 **Purpose:** Enables the median salary to be recalculated per skill, even though salary and skills live in separate tables.
- 🎯 **Formula Purpose:** Powers the "Median Salary_skills" column used in the top 10 skills pay chart.

🍽️ Background Screenshot

<img width="548" height="429" alt="Screenshot 2026-08-07 200016" src="https://github.com/user-attachments/assets/d21e58e3-8da2-4e08-b790-3a77da7cf39b" />


#### 🔢 Skill Count
=COUNT(data_jobs_skills[job_skills])
- 🔍 **Base Measure:** Counts the number of skill entries in the skills table.
- 🎯 **Formula Purpose:** Serves as the foundation for the derived "Skills per job" and "Skill likelihood" measures.

🍽️ Background Screenshot

<img width="1229" height="700" alt="Screenshot 2026-08-07 195545" src="https://github.com/user-attachments/assets/2a43e235-4fa5-4319-b510-6917eae8f6ab" />

<img width="342" height="427" alt="Screenshot 2026-08-07 195714" src="https://github.com/user-attachments/assets/3ba6092c-ec5f-434b-aea4-21b2e47ebdec" />


### 🔎 Slicers

<img width="730" height="314" alt="Screenshot 2026-08-08 131518" src="https://github.com/user-attachments/assets/d5833b48-409d-458f-bdaa-23fdea285675" />


- 🔒 **Interactive Filtering:** Country and Job Title slicers are connected across multiple PivotTables and PivotCharts, ensuring:
    - 🎯 A single selection updates every visual simultaneously
    - 👥 A consistent, cross-filtered view of the labor market from multiple angles
    - 🔗 Synchronized filtering between the salary comparison table, scatter plot, and skills charts

## Conclusion

I created this analysis to showcase how skills, job titles, and countries interact to shape salary outcomes in the data industry. Utilizing Power Pivot and DAX with data from my Excel course, this dashboard reveals that U.S. salaries consistently outpace non-U.S. salaries, that more required skills correlate with higher pay, and that skill demand and skill value are not always the same thing — helping learners prioritize which skills to develop next.
