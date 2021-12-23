# Surfs Up

## Overview
Analysis was done on the temperature in Oahu during the months of June and December. The weather stats for these months were collected from stations in Oahu then summarized and presented. The study was performed to provide information that would help determine whether or not a opening an ice cream and surf shop is an advisable business plan.

## Results: 

- ### June Temperature

<img src = "https://github.com/AaronAKTX/surfs_up/resources/JuneTemps.PNG">

- ### Decemeber Temperature
The table above clearly shows a very high number of Senior level Engineers and Staff members are at retirement age.


## Summary

### How many roles will need to be filled as the "silver tsunami" begins to make an impact?
Based on the data in the retiring_titles table, a total of 90,398 roles will need to be filled.
After filtering out titles that had already ended and recalculating, 74,458 jobs will need to be filled.

### Are there enough qualified, retirement-ready employees in the departments to mentor the next generation of Pewlett Hackard employees?
If we go by the mentoring search in the challenge, there is not near enough retirement-ready employees to mentor the next generation. If we include every employee, not just employees born in 1965, there may be enough to get a good number of people mentored. It's also notable that there are many non-senior level positions that are the retirement age as well so, senior-level positions won't all be able to be filled internally. For example, looking at currently employed Senior Engineers in Production, 10189 are retiring. 3611 Engineers in Production are retiring as well, which will leave less than 9000 Engineers in Production. 9000 is less than 10,000+ Senior engineers retiring. Below is a table with current employee counts, retiring age employee counts, pct of title retiring broken down by department and title.

<img src = "https://github.com/AaronAKTX/Pewlett-Hackard-Analysis/blob/main/Data/retiring_per_dept_title.PNG">

- Below is the query used to create the table above. The complete CSV is also included in this repository.


        WITH emp_counts AS(
        SELECT  count(e1.emp_no) as count_current_emp, t1.title, d.dept_name, coalesce(e2.retiring_current_emp,0) as count_of_retiring_age_emp
        FROM 
        employees e1
        INNER JOIN titles t1 ON e1.emp_no = t1.emp_no
        INNER JOIN dept_emp de1 ON e1.emp_no = de1.emp_no 
        INNER JOIN departments d ON de1.dept_no =d.dept_no
        LEFT JOIN(
        SELECT  count(e.emp_no) AS retiring_current_emp, t.title, d.dept_name
        FROM 
        employees e
        INNER JOIN titles t on e.emp_no = t.emp_no
        INNER JOIN dept_emp de on e.emp_no = de.emp_no 
        INNER JOIN departments d on de.dept_no =d.dept_no
        WHERE t.to_date = '9999-01-01' and de.to_date = '9999-01-01'
        AND e.birth_date <= '1955-12-31'
        GROUP BY  t.title, d.dept_name) AS e2 
        ON d.dept_name = e2.dept_name AND t1.title = e2.title

        WHERE t1.to_date = '9999-01-01' AND de1.to_date = '9999-01-01'

        GROUP BY  t1.title, d.dept_name,e2.retiring_current_emp
        ORDER BY d.dept_name, t1.title
        )
        SELECT count_current_emp, count_of_retiring_age_emp, round(cast((count_of_retiring_age_emp/count_current_emp::float) * 100.00 as numeric),2) as pct_workforce_retiring,           title, dept_name
        --INTO current_employed_counts_per_dept_title	
        FROM emp_counts
