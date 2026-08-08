# Data Science Salary Calculator

<img width="1102" height="422" alt="Screenshot 2026-07-14 115523" src="https://github.com/user-attachments/assets/a6371934-ce32-4174-a0a4-85abadda8133" />


## Introduction

This data science salary calculator was created to help job seekers investigate expected salaries for their desired roles and ensure they are being adequately compensated. Users can select a job title, country, and employment type to instantly see the matching job count, median salary, and how that role compares to similar roles, work types, and locations.

The data is from my Excel course, which provides a foundation in analyzing data using this powerful tool. The dataset contains detailed information on job titles, salaries, countries, and employment types that are presented here.



### Excel Skills Used

The following Excel skills were utilized for analysis:

- **📉 Charts**
- **🧮 Formulas and Functions**
- **❎ Data Validation**
- **🔎 Lookup Functions (XLOOKUP)**
- **🔄 Dynamic Arrays (SORT, FILTER)**
- **📐 Statistical Functions (COUNT, MEDIAN)**

### Data Jobs Dataset

The dataset used for this project contains real-world data science job information. The dataset is available via my Excel course, which provides a foundation for analyzing data using Excel. It includes detailed information on:

- **👨‍💼 Job titles**
- **💰 Salaries**
- **🌍 Countries**
- **⏰ Employment types**

## Dashboard Build

### 📉 Charts

#### 📊 Job Title - Bar Chart

<img width="336" height="240" alt="Screenshot 2026-07-14 115658" src="https://github.com/user-attachments/assets/e108578e-f786-475b-94e4-0ec5a3238546" />


- 🛠️ **Excel Features:** Utilized bar chart feature (with formatted salary values) and optimized layout for clarity.
- 🎨 **Design Choice:** Horizontal bar chart comparing median salaries across related roles, with the selected title highlighted.
- 📉 **Data Organization:** Job titles listed alongside their median salaries for quick comparison.
- 💡 **Insights Gained:** Enables quick identification of salary trends — Machine Learning Engineer and Data Scientist roles command noticeably higher median salaries than Data Analyst roles.

#### 🗺️ Country - Map Chart

<img width="366" height="238" alt="Screenshot 2026-07-14 115817" src="https://github.com/user-attachments/assets/2364dabe-9a8e-488b-8a1a-70a72fc6e646" />


- 🛠️ **Excel Features:** Utilized Excel's Bing Maps chart feature to highlight the selected country.
- 🎨 **Design Choice:** Color-coded map to visually differentiate the selected country from others.
- 📊 **Data Representation:** Highlights the selected country geographically for instant context.
- 💡 **Insights Gained:** Enables quick understanding of how the same role is compensated differently depending on location.

#### ⏰ Type - Bar Chart

<img width="362" height="241" alt="Screenshot 2026-07-14 115851" src="https://github.com/user-attachments/assets/b0a83364-0163-4990-bc04-aa15d28f3432" />


- 🛠️ **Excel Features:** Utilized bar chart feature comparing median salary across employment types.
- 🎨 **Design Choice:** Horizontal bar chart with the selected employment type highlighted.
- 📉 **Data Organization:** Employment types (Full-time, Part-time, Contractor, Internship, Temp work) listed alongside their median salaries.
- 💡 **Insights Gained:** Full-time roles show the highest median pay compared to Part-time, Contractor, Internship, and Temp work — quantifying the trade-off between flexibility and compensation.

### 🧮 KPI Cards

<img width="1054" height="138" alt="Screenshot 2026-08-08 120410" src="https://github.com/user-attachments/assets/ab11640e-44c1-4002-896c-f70fc9446769" />


- 💰 **Median Salary:** The calculated median salary for the exact combination of Job Title + Country + Type selected.
- 🏢 **Top Job Platform:** The platform where this type of job is most frequently posted.
- 🔢 **Job Count:** The number of postings matching the selected criteria.
- 🔗 **Interactivity:** All three cards recalculate instantly whenever the Job Title, Country, or Type dropdown changes.

### 🧮 Formulas and Functions

#### 🔢 Count of Matching Job Postings
=COUNT(
IF(
(jobs[job_title_short]=A2)*
(jobs[job_country]=country)*
(ISNUMBER(SEARCH(type,jobs[job_schedule_type]))),
jobs[salary_year_avg]
)
)
- 🔍 **Multi-Criteria Filtering:** Checks job title, country, and schedule type simultaneously.
- 📊 **Array Formula:** Utilizes `COUNT()` function with a nested `IF()` statement to evaluate an array of conditions.
- 🎯 **Tailored Insights:** Returns the number of job postings matching the exact combination selected.
- **🔢 Formula Purpose:** This formula powers the Job Count KPI card.

🍽️ Background Table

<img width="616" height="403" alt="Screenshot 2026-07-14 120855" src="https://github.com/user-attachments/assets/ae314e07-91fe-4d92-bf0d-84d931468623" />


#### 💰 Median Salary by Job Title, Country, and Type
=MEDIAN(
IF(
(jobs[job_title_short]=title_ex)*
(jobs[job_country]=A2)*
(ISNUMBER(SEARCH(type,jobs[job_schedule_type])))*
(jobs[salary_year_avg]<>0),
jobs[salary_year_avg]
)
)
- 🔍 **Multi-Criteria Filtering:** Checks job title, country, schedule type, and excludes blank salaries.
- 📊 **Array Formula:** Utilizes `MEDIAN()` function with nested `IF()` statement to analyze an array.
- 🎯 **Tailored Insights:** Provides specific salary information for job titles, countries, and schedule types.
- **🔢 Formula Purpose:** This formula powers the Median Salary KPI card.

🍽️ Background Table

<img width="451" height="202" alt="Screenshot 2026-07-14 120059" src="https://github.com/user-attachments/assets/f3f673f0-6177-4983-98dd-2360348c799e" />


#### 🔎 XLOOKUP for Median Salary Retrieval
=XLOOKUP(title_ex,D2:D10,E2:E10,"No Results")
- 🔍 **Lookup Logic:** Searches for the selected job title within a reference table and returns its corresponding median salary.
- 📊 **Error Handling:** Returns "No Results" if no match is found, preventing broken references.
- **🔢 Formula Purpose:** This formula retrieves the Median Salary KPI value based on the selected job title.


#### 🔄 Sorting and Filtering Results
=SORT(FILTER(A2:B112,ISNUMBER(B2:B112)),2,-1)
- 🔍 **Dynamic Filtering:** The `FILTER()` function removes rows with errors or invalid (non-numeric) values.
- 📊 **Dynamic Sorting:** The `SORT()` function ranks the remaining results in descending order.
- **🔢 Formula Purpose:** This formula populates a clean, ranked reference table used to support the dashboard's dropdowns and charts.

<img width="630" height="156" alt="Screenshot 2026-07-14 120711" src="https://github.com/user-attachments/assets/5ed73051-3683-4b24-b91f-cca50d1d1c2c" />


### ❎ Data Validation

#### 🔍 Filtered Lists

- 🔒 **Enhanced Data Validation:** Implementing filtered lists as data validation rules under the `Job Title`, `Country`, and `Type` dropdowns ensures:
    - 🎯 User input is restricted to predefined, validated values
    - 🚫 Incorrect or inconsistent entries are prevented
    - 👥 Overall usability of the dashboard is enhanced

<img width="1228" height="479" alt="Screenshot 2026-08-08 122358" src="https://github.com/user-attachments/assets/2fb52e2f-b47c-4503-a008-614e9d66419c" />


## Conclusion

I created this dashboard to showcase insights into salary trends across various data-related job titles. Utilizing data from my Excel course, this dashboard allows users to make informed decisions about their career paths by exploring how job title, country, and employment type influence salaries.
