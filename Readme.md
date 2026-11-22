
# EXPERIMENT 06: Stored Procedures, Validation Triggers, and Audit Logging

## Aim
To create a stored procedure `transfer_employee(emp_id, new_dept_id)` with validation and error handling, and to implement triggers for salary validation and audit logging, including testing of edge cases.

## Technologies Used
- MySQL
- MySQL Workbench / MySQL Command Line Client
- SQL Stored Procedures
- SQL Triggers

## Database Details
**Database Name:** `CompanyDB_Exp06`

### Tables Created

1. **Department**
   - `Dept_ID` – Primary Key
   - `Dept_Name` – Department Name

2. **Employee**
   - `Emp_ID` – Primary Key
   - `Emp_Name` – Employee Name
   - `Salary` – Employee Salary
   - `Dept_ID` – Foreign Key referencing Department

3. **Salary_Audit**
   - `Audit_ID` – Auto Increment Primary Key
   - `Emp_ID` – Employee ID
   - `Old_Salary` – Previous Salary
   - `New_Salary` – Updated Salary
   - `Changed_At` – Timestamp of salary change

## Features Implemented

### 1. Stored Procedure: `transfer_employee()`
Transfers an employee from one department to another.

**Validations:**
- Checks whether the employee exists.
- Checks whether the target department exists.
- Updates the employee's department if both validations pass.
- Generates a custom error using `SIGNAL SQLSTATE '45000'` if validation fails.

### 2. Before Update Trigger: `before_employee_salary_update`
Validates employee salary before updating.

**Functionality:**
- Prevents negative salary values.
- Raises a custom error if the new salary is less than zero.

### 3. After Update Trigger: `after_employee_salary_update`
Maintains a history of salary changes.

**Functionality:**
- Checks whether the salary has actually changed.
- Stores the employee ID, old salary, and new salary in `Salary_Audit`.
- Automatically records the timestamp of the change.

## Initial Sample Data

### Departments

| Dept_ID | Dept_Name |
|---|---|
| 1 | Sales |
| 2 | Engineering |

### Employee

| Emp_ID | Emp_Name | Salary | Dept_ID |
|---|---|---|---|
| 1 | Alex | 60000.00 | 1 |

## Execution Steps

1. Create and select the database.
2. Drop existing procedures, triggers, and tables if they exist.
3. Create the Department, Employee, and Salary_Audit tables.
4. Insert initial department and employee records.
5. Create the `transfer_employee()` stored procedure.
6. Create the salary validation trigger.
7. Create the salary audit trigger.
8. Execute the stored procedure and verify department transfer.
9. Update the employee's salary and verify the audit log.
10. Test error cases individually.

## Testing and Expected Results

| Test Case | Operation | Expected Result |
|---|---|---|
| 1 | Transfer employee 1 to department 2 | Successful transfer |
| 2 | Update salary from 60000 to 65000 | Salary updated and audit record created |
| 3 | Transfer employee 999 | Employee does not exist |
| 4 | Transfer to department 999 | Department does not exist |
| 5 | Update salary to -5000 | Salary cannot be negative |

**Note:** Error test cases are commented out in the SQL script. Uncomment and execute each test individually.

## Expected Output

- Employee Alex is successfully transferred from Sales to Engineering.
- Employee salary is updated from 60000 to 65000.
- The Salary_Audit table stores the old and new salary.
- Invalid employee and department IDs generate custom errors.
- Negative salary updates are rejected.

## Important Concepts Used

- `CREATE PROCEDURE`
- `CREATE TRIGGER`
- `BEFORE UPDATE`
- `AFTER UPDATE`
- `SIGNAL SQLSTATE '45000'`
- `OLD` and `NEW` keywords
- `DELIMITER`
- Primary Key and Foreign Key
- Audit Logging
- Error Handling

## Conclusion

Successfully implemented a stored procedure for employee department transfer with validation and error handling. Also implemented triggers to prevent negative salary updates and automatically maintain salary change history in the audit table.
