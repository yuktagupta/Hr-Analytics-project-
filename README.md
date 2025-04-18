HR ANALYTICS PROJECT

Preview of Projects
Project Overview
Preview of Projects:

Power BI HR Analytics Dashboard:
https://github.com/yuktagupta/Hr-Analytics-project-/blob/main/blue%20sn.png
https://github.com/yuktagupta/Hr-Analytics-project-/blob/main/power%20bi%20snap.png

Tableau HR Analytics Project: HR Analytics Dashboard
https://github.com/yuktagupta/Hr-Analytics-project-/blob/main/tableau%20snap%20.png

SQL Queries:
Create Table
create table hrdata
(
	emp_no int8 PRIMARY KEY,
	gender varchar(50) NOT NULL,
	marital_status varchar(50),
	age_band varchar(50),
	age int8,
	department varchar(50),
	education varchar(50),
	education_field varchar(50),
	job_role varchar(50),
	business_travel varchar(50),
	employee_count int8,
	attrition varchar(50),
	attrition_label varchar(50),
	job_satisfaction int8,
	active_employee int8
)

Import Data in Table Using Query
COPY hrdata FROM 'D:\hrdata.csv' DELIMITER ',' CSV HEADER;

Employee Count:
select sum(employee_count) as Employee_Count from hrdata;

Attrition Count:
select count(attrition) from hrdata where attrition='Yes';
Attrition Rate:
select 
round (((select count(attrition) from hrdata where attrition='Yes')/ 
sum(employee_count)) * 100,2)
from hrdata;

Active Employee:
select sum(employee_count) - (select count(attrition) from hrdata  where attrition='Yes') from hrdata;
OR
select (select sum(employee_count) from hrdata) - count(attrition) as active_employee from hrdata
where attrition='Yes';

Average Age:
select round(avg(age),0) from hrdata;

Attrition by Gender
select gender, count(attrition) as attrition_count from hrdata
where attrition='Yes'
group by gender
order by count(attrition) desc;

Department wise Attrition:
select department, count(attrition), round((cast (count(attrition) as numeric) / 
(select count(attrition) from hrdata where attrition= 'Yes')) * 100, 2) as pct from hrdata
where attrition='Yes'
group by department 
order by count(attrition) desc;


No of Employee by Age Group
SELECT age,  sum(employee_count) AS employee_count FROM hrdata
GROUP BY age
order by age;

Education Field wise Attrition:
select education_field, count(attrition) as attrition_count from hrdata
where attrition='Yes'
group by education_field
order by count(attrition) desc;

Attrition Rate by Gender for different Age Group
select age_band, gender, count(attrition) as attrition, 
round((cast(count(attrition) as numeric) / (select count(attrition) from hrdata where attrition = 'Yes')) * 100,2) as pct
from hrdata
where attrition = 'Yes'
group by age_band, gender
order by age_band, gender desc;

Job Satisfaction Rating
-Run this query first to activate the cosstab() function in postgres
CREATE EXTENSION IF NOT EXISTS tablefunc;

-Then run this to get o/p-
SELECT *
FROM crosstab(
  'SELECT job_role, job_satisfaction, sum(employee_count)
   FROM hrdata
   GROUP BY job_role, job_satisfaction
   ORDER BY job_role, job_satisfaction'
	) AS ct(job_role varchar(50), one numeric, two numeric, three numeric, four numeric)
ORDER BY job_role;
SQl output :-
https://github.com/yuktagupta/Hr-Analytics-project-/blob/main/sql%20snap%20.png
Excel HR Analytics Dashboard: HR Analytics Excel Dashboard
https://github.com/yuktagupta/Hr-Analytics-project-/blob/main/HR%20Analytics%20Dashboard%20Excel%20Project.xlsx


Project Overview

This project utilized four essential data analysis tools: Power BI, Tableau Desktop, SQL, and Excel.

Data

HR Data 2022 of a medical components manufacturing company (open source)

Problem Statement

Within the organization, the HR department bears the responsibility of monitoring and overseeing diverse facets of employee data to ensure the maintenance of a healthy workforce. Nevertheless, a notable deficiency exists in terms of well-defined performance indicators to systematically track and analyze critical HR metrics. To address this challenge, the project was structured around several pivotal components, meticulously designed to offer invaluable insights and hands-on experience.

Analysis

A set of KPIs that can greatly benefit the HR department has been designed to address the following points:

Employee Count: With this KPI in place, the HR department can gain clear visibility into the total number of employees. This would enable effective workforce assessment, aiding in future growth or downsizing planning.

Attrition Count: By implementing a standardized method for tracking employee attrition, the HR department can obtain reliable and comprehensive data on the number of employees who have left the organization.

Attrition Rate: The introduction of a clear measure for attrition rate offers the opportunity to assess turnover levels. This can be instrumental in comparing these rates with industry benchmarks and gaining insights into employee satisfaction and engagement levels.

Active Employees: The ability to differentiate between active and inactive employees provides the HR department with a valuable tool to assess workforce productivity and capacity accurately.

Average Age: By incorporating the average age KPI, the HR department can delve into workforce demographics. This insight can inform effective succession planning and enhance the organization's ability to attract and retain younger talent.

The HR department's challenges in understanding attrition patterns based on gender, department-wise attrition rates, employee age distribution, job satisfaction ratings, education field-wise attrition, and attrition rates by gender for different age groups have all been successfully addressed through visualizations:

Attrition by Gender: Insightful visualizations that enable a comprehensive understanding of attrition patterns based on gender. This newfound clarity aids in identifying any gender-related disparities and facilitates the implementation of targeted retention strategies.

Department-wise Attrition: Visualizations have been deployed to showcase attrition rates across different departments. This enhancement empowers the HR department to easily identify departments with higher attrition rates, allowing them to promptly address any underlying issues or concerns.

Number of Employees by Age Group: Visual representations have been established to analyze the distribution of employees across various age groups. This data supports the assessment of workforce demographics and facilitates the identification of age-related gaps or imbalances, informing the implementation of targeted HR policies or programs.

The HR department can benefit from visualizations representing job satisfaction ratings, providing an effective means to measure employee engagement and overall job satisfaction levels.

Education Field-wise Attrition: Visual representations have been implemented to analyze attrition rates based on education fields. This allows for the identification of specific educational backgrounds associated with higher attrition, enabling tailored retention strategies. ** Attrition Rate by Gender for Different Age Groups:** Visualizations display attrition rates based on gender and different age groups. This enables the HR department to identify age and gender-related attrition trends, facilitating the implementation of targeted retention strategies for specific employee segments.

Project Phases

Power BI

Constructed a dynamic and interactive dashboard. The emphasis was on data integration and the creation of visually appealing, informative visualizations.

Tableau

Created the dashboard in Tableau with custom charts. Developed complex calculations and insightful trend analyses.

SQL

Employed SQL queries to extract key metrics. Created test documents to demonstrate data validation data in Tableau and Power Bi using SQL queries

Excel

Created an interactive Excel dashboard incorporating pivot tables and visually compelling charts.

Conclusion

This portfolio project serves as a testament to the ability to harness data effectively, transforming it into actionable insights. It showcases the technical prowess and dedication to providing invaluable solutions through data analysis.
