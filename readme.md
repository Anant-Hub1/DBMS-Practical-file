# Experiment 5: Views, View Updatability, and Recursive CTEs

## Aim

Create SQL views for department salary summaries and employee reporting relationships,
test view updatability, and use a recursive Common Table Expression (CTE) to display
the organizational hierarchy.

## Software Requirements

- MySQL Server 8.0 or later
- MySQL Workbench or another SQL client

## Database and Tables

The SQL script creates a database named `CompanyDB_Exp05` and uses two tables:

| Table | Description |
|---|---|
| `Department` | Stores department IDs and department names |
| `Employee` | Stores employee details, salary, department, job title, and manager ID |

The database contains 5 departments and 30 employees with a manager hierarchy.

## Views Created

### Department Salary Summary

`Department_Salary_Summary` combines department and employee data to display:

- Total number of employees
- Average salary
- Maximum salary
- Minimum salary

This is an aggregate view and is not updatable.

### Employee Hierarchy

`Employee_Hierarchy` uses a self-join to display each employee together with the name
of their manager.

This simple view can reflect changes made to the underlying `Employee` table.

## Operations Performed

1. Created department and employee tables with foreign-key relationships.
2. Created an aggregate department salary summary view.
3. Created an employee-manager hierarchy view using a self-join.
4. Updated a salary in the base table and verified that the view data reflected the change.
5. Demonstrated that aggregate views cannot be updated directly.
6. Used a recursive CTE to list reporting chains and organizational levels.

## Recursive CTE

The recursive CTE works in two parts:

- The **anchor member** selects employees with no manager.
- The **recursive member** finds employees whose `Manager_ID` matches an employee
  already in the CTE.

It also assigns a level to each employee to show their distance from the root manager.

## How to Run

1. Open MySQL Workbench or another SQL client.
2. Connect to MySQL Server.
3. Open `exp-5.sql`.
4. Execute the complete script.
5. Review the view outputs, updatability demonstration, and recursive CTE result.

The script drops existing views and tables before recreating the database objects.