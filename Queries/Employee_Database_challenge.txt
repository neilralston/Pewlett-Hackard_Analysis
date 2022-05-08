--DELIVERABLE 1
SELECT employees.emp_no,
	employees.first_name,
	employees.last_name,
	titles.title,
	titles.from_date,
	titles.to_date
--INTO retirement_info_title
FROM employees
LEFT JOIN titles
ON employees.emp_no = titles.emp_no
WHERE (birth_date BETWEEN '1952-01-01' AND '1955-12-31')
ORDER BY emp_no;

-- Use Dictinct with Orderby to remove duplicate rows
SELECT DISTINCT ON (retirement_info_title.emp_no) retirement_info_title.emp_no,
	retirement_info_title.first_name,
	retirement_info_title.last_name,
	retirement_info_title.title
INTO unique_titles
FROM retirement_info_title
WHERE retirement_info_title.to_date = ('9999-01-01')
ORDER BY emp_no, to_date DESC;

SELECT COUNT (unique_titles.emp_no), unique_titles.title
INTO retiring_titles
FROM unique_titles
GROUP BY title
ORDER BY COUNT (title) DESC;

--DELIVERABLE 2
SELECT DISTINCT ON (employees.emp_no) employees.emp_no,
	employees.first_name,
	employees.last_name,
	dept_employees.from_date,
	dept_employees.to_date,
	titles.title
INTO mentor_elig
FROM employees
LEFT JOIN dept_employees
ON employees.emp_no = dept_employees.emp_no
LEFT JOIN titles
ON employees.emp_no = titles.emp_no
WHERE dept_employees.to_date = ('9999-01-01')
AND (employees.birth_date BETWEEN '1965-01-01' AND '1965-12-31')
ORDER BY emp_no;