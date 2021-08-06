-Hi, I’m Maxwell Grant!
I am actively seeking opportunities in data science, data engineering, and business intelligence. In June of 2021, I achieved a MS in Information Systems with a concentration in Data Analytics from Baruch College while working 40 hours a week in construction management. Please take a moment to view my portfolio. Feel free to contact me if I am a good fit for an open position.
I can be reached at maxwell.grant90@gmail.com

Repository link: https://github.com/MaxwellGrant90/MaxwellGrant90.git

LinkedIn link: https://www.linkedin.com/in/maxwell-grant/


<h1>Project 1 - My Construction Story</h1>
<h2>- An annotated time series graph with Matplotlib in a Jupyter Notebook about companies I worked for. The dataset was extracted from a NYC Department of Buildings public database with over 3.7M rows.</h2>

-Jupyter Notebook: A step by step commentary about retreiving a SoQL query from an Socrates API to a clean and ready to plot dataframe. A short story about my career is included as well.

![MyConstructionStory](https://user-images.githubusercontent.com/88124878/127779601-3fc71140-9660-46fb-bc5a-06b522f9cbe8.png)

<h1>Project 2 - World Happiness Reports 2005-2020</h1>
<h2>- A Tableau dashboard and a linear regression in a Jupyter Notebook with exploratory data analysis and feature importance.</h2>

<h3>- Tableau dashboard</h3>
-Link to the dashboard: https://public.tableau.com/app/profile/maxwell.grant/viz/WorldHappinessReportDashboard_16211719322600/Dashboard1

-Regions, longitude, and latitude added to the dataset.

![World Happiness Dashboard](https://user-images.githubusercontent.com/88124878/127759660-bc014a4f-9cd0-4e93-aea0-32e6aa0dfd38.png)



<h3>- Exploratory data analysis and feature importance</h3>
-Jupyter Notebook: includes evaluation metrics.

![World Happiness EPA](https://user-images.githubusercontent.com/88124878/127779616-f9edf24b-5c56-4967-a8b1-42b3989d4820.png)
![World Happiness EPA regplot](https://user-images.githubusercontent.com/88124878/127758741-538e366b-5181-49a3-801e-c9ba63733711.png)
![World Happiness corr](https://user-images.githubusercontent.com/88124878/127779610-2bede530-e348-448b-9184-a4e8ea0067dc.png)
![World Happiness Feature Importance](https://user-images.githubusercontent.com/88124878/127758744-1d8b7371-5d91-4966-81ec-497f5d5c7962.png)


<h1>Project 3 - Entity-Relationship Model</h1>
<h2>- A database schema of a human resource system with SQL</h2>
-SQL statement (Oracle syntax) to query first name, last name, job title, department, performance score, and salary; ordered by performance score: <br><br>
SELECT e.firstname, e.lastname, t.title, t.department, p.score, s.salary<br>
FROM title t INNER JOIN<br>
performance p ON t.title = p.title<br>
INNER JOIN employee e USING (employeeid)<br>
INNER JOIN salary s USING (employeeid)<br>
WHERE s.active__ = 'TRUE' AND p.active_ = 'TRUE'<br> 
ORDER BY p.score DESC<br><br>
-Table create and insert into statements with mock data are in a .txt file.

![Entity-Relationship Model](https://user-images.githubusercontent.com/88124878/127951189-8b6599ac-1d8f-4516-aa79-6d3f53a3c659.png)
-This database focuses on entity relationships and normalization. It does not contain detailed information. 

MORE PROJECTS COMING SOON!








<!---
MaxwellGrant90/MaxwellGrant90 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
