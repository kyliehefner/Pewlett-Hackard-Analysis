# Pewlett-Hackard-Analysis
## Overview of Analysis
### Purpose
Pewlett Hackard is a large company of thousands of employees. The purpose of this analysis is to examine the employees that will be retiring in the next few years. Specifically I was tasked with determining the retiring employees by their job title, and identifying employees who are eligible for the mentorship program.

## Results
### Count of retiring employees by title
![image](https://user-images.githubusercontent.com/102445183/169455906-33b71dcc-c2e8-49fa-8ed5-ec77e7b83062.png)
- The title with the most positions opening will be Senior Engineer, with 25,916 employees retiring soon. That's 36% of all retiring employees.
- The title with the least positions opening will be Manager, with only 2 employees retiring soon. The next lowest count is Assistant Engineer with 1,090 employees retiring.

### Employees eligible for mentorship program
![image](https://user-images.githubusercontent.com/102445183/169456346-aa973f08-39a6-4e54-859f-a80a1937cbd0.png)
- There are 1,549 employees eligible for the mentorship program (retiring soon and born in 1965). That's 2% of all retiring employees.
- These eligible employees cover a range of titles and experience levels. Next steps for the mentorship program analysis could be separating these employees by title and limiting by length of time working at Pewlett Hackard.

## Summary
### Analysis
- 72,458 roles will need to be filled as baby boomers reaching retirement age begins to take an impact on Pewlett Hackard.
- Since there are 1,549 employees eligible for the mentorship program, that accounts for 1 experienced mentor employee per 47 opening positions. This appears like enough experienced employees to mentor the new generation of Pewlett Hackard employees, but additional analysis should confirm if that ratio varies greatly for different departments.

### Additional Insights
```sql
-- Mentorship eligible counts by title
SELECT COUNT(title), title
FROM mentorship_eligibility
GROUP BY title
ORDER BY COUNT(title) DESC;
```
![image](https://user-images.githubusercontent.com/102445183/169458163-93036851-f258-4546-bb0a-4333f0c3132f.png)
- Comparing the counts of job titles of the employees eligible for the mentorship program with the counts of all positions that are opening soon due to retirements, we can see that the ratio of potential mentors per opening positions varies slightly between positions. For example, Senior Engineers have a 153:1 opening positions to mentors ratio, while Engineers have a 19:1 ratio. Some mentor Engineers may need to mentor positions for new Senior Engineers instead of new Engineers to make up for this difference.
- We can also see that there are no eligible mentors for new managers, although 2 positions are opening up. Pewlett Hackard will have to broaden their mentorship search range to find mentors for these new managers.

```sql
-- Count of mentor eligible by beginning year in role
SELECT date_part('year', from_date) AS beginning_year, COUNT(emp_no)
FROM mentorship_eligibility
GROUP BY beginning_year
ORDER BY COUNT(emp_no) DESC;

-- Count of mentor eligible by beginning decade in role
SELECT date_part('decade', from_date) AS beginning_decade, COUNT(emp_no)
FROM mentorship_eligibility
GROUP BY beginning_decade
ORDER BY beginning_decade DESC;
```
![image](https://user-images.githubusercontent.com/102445183/169462690-e4f48ae7-0729-4784-9c27-476f77af9e89.png)
![image](https://user-images.githubusercontent.com/102445183/169463192-08b37ca0-2bd7-4e65-8bbf-83f3be476b71.png)
- We can see from the number of eligible mentors by their year and decade starting in their current role that we have sufficient mentors with many years of experience. The majority of our mentors started working in their current role in the 90s, and the smallest number started in the 2000s.
