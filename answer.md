'''
### add new employee record to employee table with id = 168, firstname = 'John', lastname = 'Doe', initials = 'JD', job = 'Programmer', hire_date = today's date.
'''
today = datetime.now()

sql = "INSERT INTO employee(emp_num, emp_lname, emp_fname, emp_initial, emp_job, emp_hiredate) VALUES (%s, %s, %s, %s, %s, %s)"
value = (168, "Doe", "John", "JD", 'Programmer', today)

cursor.execute(sql, value)

DB.commit()

'''
### query the new created employee (id=168) from employee table, with information of employee id, firstname, lastname, initials, job description (join with job), charge per hour (join with job) and hire_date.
'''

sql = """
SELECT 
    e.emp_num,
    e.emp_fname,
    e.emp_lname,
    e.emp_initial,
    j.job_desc,
    j.charge_per_hour,
    e.emp_hiredate
FROM 
    employee AS e
JOIN 
    job AS j ON e.emp_job = j.job_id
WHERE 
    e.emp_num = 168;
"""

cursor.execute(sql)

'''
### update the new created employee (id=168) job, from 'Programmer' to 'Database Designer'.
'''

sql = """
UPDATE employee
SET emp_job = 'Database Designer'
WHERE emp_num = 168;
"""

cursor.execute(sql)

DB.commit()

'''
### query all project that has "Programmer" assigned to, with information of project id, project name and program manager (join with employee).
'''

sql = """
SELECT 
    p.proj_id,
    p.proj_name,
    e.emp_fname,
    e.emp_lname
FROM 
    project AS p
JOIN 
    employee AS e ON p.proj_manager = e.emp_num
WHERE 
    e.emp_job = 'Programmer';
"""

cursor.execute(sql)

'''
### delete the new created employee (id=168) from employee table.
'''

sql = """
DELETE FROM employee
WHERE emp_num = 168;
"""

cursor.execute(sql)

DB.commit()