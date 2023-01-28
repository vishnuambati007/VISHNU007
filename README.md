CREATE TABLE EmployeeDetails (
  EmpId INT PRIMARY KEY,
  FullName VARCHAR(255) NOT NULL,
  ManagerId INT,
  DateOfJoining DATE NOT NULL,
  City VARCHAR(255)
);
CREATE TABLE EmployeeSalary (
  EmpId INT PRIMARY KEY,
  Project VARCHAR(255) NOT NULL,
  Salary DECIMAL(10,2) NOT NULL,
  Variable DECIMAL(10,2) NOT NULL,
  FOREIGN KEY (EmpId) REFERENCES EmployeeDetails(EmpId)
);
INSERT INTO EmployeeDetails (EmpId, FullName, ManagerId, DateOfJoining, City)
VALUES (1, 'John Smith', 3, '2022-05-01', 'New York'),
       (2, 'Jane Doe', 3, '2022-06-01', 'Los Angeles'),
       (3, 'Bob Johnson', NULL, '2022-07-01', 'Chicago'),
       (4, 'Samantha Williams', 2, '2022-08-01', 'Houston'),
       (5, 'Michael Davis', 1, '2022-09-01', 'Phoenix');
INSERT INTO EmployeeSalary (EmpId, Project, Salary, Variable)
VALUES (1, 'Project A', 50000, 10000),
       (2, 'Project B', 55000, 12000),
       (3, 'Project C', 60000, 15000),
       (4, 'Project D', 65000, 20000),
       (5, 'Project E', 70000, 25000);
  1 /*SELECT *
FROM EmployeeDetails
WHERE NOT EXISTS (SELECT 1 FROM EmployeeSalary WHERE EmployeeDetails.EmpId = EmployeeSalary.EmpId);
*/

  2/*SELECT * FROM employees WHERE NOT EXISTS (SELECT * FROM projects WHERE projects.employee_id = employees.id);

  3/*SELECT * FROM EmployeeDetails WHERE YEAR(joining_date) = 2020;

  4/*SELECT EmployeeDetails.* FROM EmployeeDetails
JOIN EmployeeSalary ON EmployeeDetails.employee_id = EmployeeSalary.employee_id;

  5/*SELECT project_name, COUNT(employee_id) as 'Number of Employees'
FROM projects
GROUP BY project_name;

  6/*SELECT EmployeeDetails.employee_name, EmployeeSalary.salary
FROM EmployeeDetails
LEFT JOIN EmployeeSalary ON EmployeeDetails.employee_id = EmployeeSalary.employee_id;

  7/*SELECT EmployeeDetails.* FROM EmployeeDetails
JOIN Managers ON EmployeeDetails.employee_id = Managers.manager_id;

 8/*SELECT employee_name, COUNT() as count
FROM EmployeeDetails
GROUP BY employee_name
HAVING COUNT() > 1;

9/*SELECT * FROM EmployeeDetails
WHERE (employee_id % 2) <> 0;

10/*WITH cte AS (
SELECT salary, ROW_NUMBER() OVER (ORDER BY salary DESC) as row_num
FROM EmployeeSalary
)
SELECT salary FROM cte
WHERE row_num = 3;
