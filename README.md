# Surfs Up

## Overview
Analysis was done on the temperature in Oahu during the months of June and December. The weather stats for these months were collected from stations in Oahu then summarized and presented. The study was performed to provide information that would help determine whether or not a opening an ice cream and surf shop is an advisable business plan.

## Results: 

### June Temperatures                    
 <img src = "https://github.com/AaronAKTX/surfs_up/blob/main/Resources/JuneTemps.PNG">

### Decemeber Temperatures
<img src = "https://github.com/AaronAKTX/surfs_up/blob/main/Resources/DecTemps.PNG">

### Temperature observations
- The average temperature in June is 75 degrees fahrenheit.
  - 75 percent of the temperatures taken in the month of June are 73 degrees fahrenheit or higher - That is both great surfing and great ice cream weather.
- The average temperature in December is 71 degrees fahrenheit.
  - 75 percent of the temperatures taken in the month of December are 69 degrees fahrenheit or higher - That is both great surfing and great ice cream weather.
- The temperature in two opposite times of year both average a nice temperature for ice cream and surfing and aren't that different from each other which seems to indicate that a year round ice cream/surf shop would be a great business.


## Summary

### Ice Cream and Surfing = the PERFECT combination
Based on the temperature data, the ice cream/surf shop is a great idea. People who surf, can pretty much surf year round looking at the temperature. People who enjoy ice cream can eat year round without getting too cold. People who eat ice cream and surf will be in paradise with this combination.




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
