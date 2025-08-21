Based on your actual DBMS project code, here are the answers to all the viva questions:

## **Database Design & Schema Questions**

**1. What is the primary purpose of your hospital management database?**
The database manages core hospital operations including patient registration, department management, room allocation, doctor information, billing, and appointments. It maintains comprehensive records for healthcare delivery with proper relationships between entities.

**2. Explain the relationship between hospital_departments and doctors tables.**
One-to-many relationship where one department can have multiple doctors. The `department_id` in doctors table is a foreign key referencing `hospital_departments(department_id)`.

**3. Why did you use AUTO_INCREMENT for primary keys?**
AUTO_INCREMENT ensures unique, sequential IDs are automatically generated, eliminating duplicate key issues and simplifying record insertion without manual ID management.

**4. What are the foreign key constraints in your database and why are they important?**
- `doctors.department_id` → `hospital_departments.department_id`
- `billing.patient_id` → `patients.patient_id`
- `appointments.patient_id` → `patients.patient_id`
- `appointments.doctor_id` → `doctors.id`
- `appointments.room_id` → `roomsinfo.RoomID`
- `RoomsInfo.DepartmentID` → `hospital_departments.department_id`

They maintain referential integrity and prevent orphaned records.

**5. Explain the referential integrity maintained in your appointments table.**
Appointments table uses `ON DELETE RESTRICT` to prevent deletion of patients, doctors, or rooms that have active appointments, ensuring data consistency.

**6. Why did you choose ENUM data type for gender in patients table?**
ENUM restricts values to predefined options ('Male', 'Female', 'Other'), ensuring data consistency and preventing invalid entries.

**7. What is the significance of the ON DELETE RESTRICT constraint in appointments table?**
Prevents deletion of referenced records (patients, doctors, rooms) if they have dependent appointment records, maintaining data integrity.

## **Table Structure & Data Types**

**8. Explain the difference between VARCHAR and TEXT data types in your schema.**
- VARCHAR: Fixed maximum length (e.g., VARCHAR(100) for names) - faster for shorter strings
- TEXT: Variable length for longer content (descriptions, medical conditions) - no length limit

**9. Why did you use DECIMAL(10,2) for monetary values instead of FLOAT?**
DECIMAL provides exact precision for financial calculations, avoiding floating-point rounding errors. Format: 10 total digits, 2 after decimal point.

**10. What is the purpose of TIMESTAMP fields with DEFAULT CURRENT_TIMESTAMP?**
Automatically records creation time (`created_at`) and update time (`updated_at ON UPDATE CURRENT_TIMESTAMP`), providing audit trail functionality.

**11. Explain the CHECK constraint on the rating field in doctors table.**
`CHECK (rating >= 0 AND rating <= 5)` ensures doctor ratings are within valid range (0-5 scale), preventing invalid rating values.

**12. Why did you use different data types for phone numbers in different tables?**
All use VARCHAR(20) consistently, which accommodates international formats, extensions, and special characters while maintaining flexibility.

**13. What is the maximum length you've allocated for email addresses and why?**
VARCHAR(100) - sufficient for most email addresses while preventing excessively long inputs that could cause storage issues.

## **Normalization & Database Design**

**14. What normal form is your database in? Justify your answer.**
The database is in 3NF (Third Normal Form):
- 1NF: All attributes are atomic
- 2NF: No partial dependencies (all non-key attributes depend on complete primary key)
- 3NF: No transitive dependencies (no non-key attribute depends on another non-key attribute)

**15. Are there any denormalization techniques you've applied? Why?**
Yes, storing `active_patients` count in doctors table for performance optimization, avoiding complex COUNT queries for frequent operations.

**16. Explain how you've avoided data redundancy in your design.**
- Separate tables for distinct entities
- Foreign key relationships instead of duplicate data
- Normalization principles followed
- Department information stored once and referenced

**17. Could you identify any potential anomalies in your current design?**
Minor update anomaly: If `active_patients` count becomes inconsistent with actual appointments, manual synchronization would be needed.

**18. How would you improve the database design for better performance?**
- Add indexes on frequently queried fields (email, phone, appointment_datetime)
- Consider partitioning large tables by date
- Add composite indexes for multi-column searches

## **Triggers & Stored Procedures**

**19. Explain the purpose of the before_patient_delete trigger.**
```sql
CREATE TRIGGER before_patient_delete
BEFORE DELETE ON patients
FOR EACH ROW
BEGIN
    INSERT INTO backup (first_name, last_name, phone_number)
    VALUES (OLD.first_name, OLD.last_name, OLD.phone_number);
END$$
```
Automatically backs up essential patient information before deletion for audit trail and potential recovery.

**20. What happens when a patient record is deleted from your database?**
1. The trigger fires before deletion
2. Patient's name and phone are saved to backup table
3. Original record is deleted
4. Backup maintains timestamp of deletion

**21. Why did you use DELIMITER $$ before creating the trigger?**
Changes the statement delimiter from `;` to `$$` to allow semicolons within the trigger body without terminating the CREATE TRIGGER statement.

**22. What are the advantages and disadvantages of using triggers?**
Advantages: Automatic execution, data integrity, audit trails
Disadvantages: Hidden business logic, debugging difficulty, performance impact

**23. How would you create an AFTER INSERT trigger for logging new appointments?**
```sql
DELIMITER $$
CREATE TRIGGER after_appointment_insert
AFTER INSERT ON appointments
FOR EACH ROW
BEGIN
    INSERT INTO appointment_log (appointment_id, action, timestamp)
    VALUES (NEW.appointment_id, 'CREATED', NOW());
END$$
DELIMITER ;
```

## **Sample Query Questions**

**29. Write a query to find all available doctors in the Cardiology department.**
```sql
SELECT d.* FROM doctors d
JOIN hospital_departments hd ON d.department_id = hd.department_id
WHERE hd.department_name = 'Cardiology' AND d.status = 'Available';
```

**30. How would you find the total number of patients per department?**
```sql
SELECT hd.department_name, COUNT(DISTINCT a.patient_id) as patient_count
FROM hospital_departments hd
LEFT JOIN doctors d ON hd.department_id = d.department_id
LEFT JOIN appointments a ON d.id = a.doctor_id
GROUP BY hd.department_id, hd.department_name;
```

**31. Write a query to get all appointments for a specific date range.**
```sql
SELECT * FROM appointments 
WHERE appointment_datetime BETWEEN '2024-01-01' AND '2024-12-31';
```

**32. How would you calculate the average room rate by department?**
```sql
SELECT hd.department_name, AVG(r.DailyRate) as avg_rate
FROM hospital_departments hd
JOIN RoomsInfo r ON hd.department_id = r.DepartmentID
GROUP BY hd.department_id, hd.department_name;
```

**33. Find all patients who have emergency contacts with missing phone numbers.**
```sql
SELECT * FROM patients 
WHERE emergency_contact_phone IS NULL OR emergency_contact_phone = '';
```

## **Data Integrity & Constraints**

**34. What constraints ensure data integrity in your billing table?**
- PRIMARY KEY on bill_id
- FOREIGN KEY to patients table
- NOT NULL constraints on essential fields
- DECIMAL precision for monetary values

**35. How do you prevent duplicate email addresses in the doctors table?**
`email VARCHAR(100) NOT NULL UNIQUE` constraint ensures no duplicate emails are allowed.

**36. Explain the importance of NOT NULL constraints in your design.**
Ensures critical fields (names, IDs, dates) always have values, preventing incomplete records and maintaining data quality.

**37. What happens if you try to insert an invalid status in doctors table?**
The ENUM constraint will reject the insertion and throw an error since only 'Available', 'Not Available', 'Busy' are allowed.

**38. How would you ensure that appointment dates are not in the past?**
Add a CHECK constraint:
```sql
ALTER TABLE appointments 
ADD CONSTRAINT chk_future_date 
CHECK (appointment_datetime > NOW());
```

## **Backup & Recovery**

**39. Explain your backup strategy for deleted patient records.**
The `before_patient_delete` trigger automatically saves deleted patient information (name, phone) to the backup table with deletion timestamp.

**40. How would you restore accidentally deleted patient data?**
```sql
SELECT * FROM backup WHERE deleted_at > '2024-01-01';
-- Manual restoration would require recreating patient record with backed up data
```

**41. What is the purpose of the backup table in your design?**
Maintains audit trail of deleted patients with essential contact information and deletion timestamps for compliance and recovery purposes.

## **Advanced SQL Concepts**

**47. Write a query using JOINs to get patient details with their doctor information.**
```sql
SELECT p.first_name, p.last_name, p.phone_number,
       d.first_name as doctor_fname, d.last_name as doctor_lname,
       hd.department_name
FROM patients p
JOIN appointments a ON p.patient_id = a.patient_id
JOIN doctors d ON a.doctor_id = d.id
JOIN hospital_departments hd ON d.department_id = hd.department_id;
```

**48. How would you use subqueries to find the busiest department?**
```sql
SELECT department_name FROM hospital_departments
WHERE department_id = (
    SELECT d.department_id 
    FROM doctors d
    JOIN appointments a ON d.id = a.doctor_id
    GROUP BY d.department_id
    ORDER BY COUNT(*) DESC
    LIMIT 1
);
```

## **Practical Scenario Questions**

**51. How would you handle double-booking of rooms?**
Add unique constraint on room_id and appointment_datetime, or implement application-level checking before insertion.

**52. What would happen if a department is deleted that has active doctors?**
Foreign key constraint would prevent deletion, maintaining referential integrity.

**64. What would happen if you try to delete a doctor with active appointments?**
The `ON DELETE RESTRICT` constraint would prevent the deletion and throw an error.

**65. How would you handle invalid date entries?**
Use DATE data type validation and add CHECK constraints for reasonable date ranges.

This comprehensive answer set covers all aspects of your hospital management database system based on your actual SQL code.







Based on your actual DBMS project code, here are comprehensive query-related questions for your viva:

## **Basic SELECT Queries**

**1. Write a query to display all patients whose first name starts with 'র'.**
```sql
SELECT * FROM patients WHERE first_name LIKE 'র%';
```

**2. Find all departments that have 'ology' in their name.**
```sql
SELECT * FROM hospital_departments WHERE department_name LIKE '%ology%';
```

**3. List all available rooms with their daily rates.**
```sql
SELECT RoomNumber, Type, DailyRate FROM RoomsInfo WHERE Status = 'Available';
```

**4. Display patients born after 1990.**
```sql
SELECT first_name, last_name, date_of_birth FROM patients 
WHERE date_of_birth > '1990-01-01';
```

## **JOIN Operations**

**5. Show all rooms with their department names.**
```sql
SELECT r.RoomNumber, r.Type, r.Status, hd.department_name 
FROM RoomsInfo r
JOIN hospital_departments hd ON r.DepartmentID = hd.department_id;
```

**6. List all doctors with their department information.**
```sql
SELECT d.first_name, d.last_name, d.specialization, hd.department_name
FROM doctors d
JOIN hospital_departments hd ON d.department_id = hd.department_id;
```

**7. Find all appointments with patient names and doctor names.**
```sql
SELECT p.first_name AS patient_name, p.last_name AS patient_surname,
       d.first_name AS doctor_name, d.last_name AS doctor_surname,
       a.appointment_datetime, a.reason
FROM appointments a
JOIN patients p ON a.patient_id = p.patient_id
JOIN doctors d ON a.doctor_id = d.id;
```

**8. Show billing information with patient details.**
```sql
SELECT p.first_name, p.last_name, b.billing_date, b.total_amount, b.payment_status
FROM billing b
JOIN patients p ON b.patient_id = p.patient_id;
```

## **Aggregate Functions**

**9. Count the number of patients by gender.**
```sql
SELECT gender, COUNT(*) as patient_count FROM patients GROUP BY gender;
```

**10. Find the average daily rate for each room type.**
```sql
SELECT Type, AVG(DailyRate) as average_rate FROM RoomsInfo GROUP BY Type;
```

**11. Calculate total capacity by department.**
```sql
SELECT hd.department_name, SUM(r.Capacity) as total_capacity
FROM RoomsInfo r
JOIN hospital_departments hd ON r.DepartmentID = hd.department_id
GROUP BY hd.department_id, hd.department_name;
```

**12. Count available and occupied rooms by department.**
```sql
SELECT hd.department_name, r.Status, COUNT(*) as room_count
FROM RoomsInfo r
JOIN hospital_departments hd ON r.DepartmentID = hd.department_id
GROUP BY hd.department_name, r.Status;
```

## **Subqueries**

**13. Find patients who have no billing records.**
```sql
SELECT * FROM patients 
WHERE patient_id NOT IN (SELECT patient_id FROM billing);
```

**14. Find the department with the highest average room rate.**
```sql
SELECT department_name FROM hospital_departments
WHERE department_id = (
    SELECT DepartmentID FROM RoomsInfo 
    GROUP BY DepartmentID 
    ORDER BY AVG(DailyRate) DESC 
    LIMIT 1
);
```

**15. List patients older than the average age.**
```sql
SELECT first_name, last_name, date_of_birth 
FROM patients 
WHERE date_of_birth < (
    SELECT DATE_SUB(CURDATE(), INTERVAL AVG(DATEDIFF(CURDATE(), date_of_birth))/365 YEAR) 
    FROM patients
);
```

## **Complex WHERE Clauses**

**16. Find patients with diabetes or hypertension in their medical condition.**
```sql
SELECT first_name, last_name, medical_condition 
FROM patients 
WHERE medical_condition LIKE '%ডায়াবেটিস%' OR medical_condition LIKE '%রক্তচাপ%';
```

**17. List rooms that are ICU type and available.**
```sql
SELECT * FROM RoomsInfo WHERE Type = 'ICU' AND Status = 'Available';
```

**18. Find patients registered in the last 30 days.**
```sql
SELECT * FROM patients 
WHERE registration_date >= DATE_SUB(CURDATE(), INTERVAL 30 DAY);
```

## **Date and Time Functions**

**19. Calculate age of all patients.**
```sql
SELECT first_name, last_name, date_of_birth,
       FLOOR(DATEDIFF(CURDATE(), date_of_birth)/365) AS age
FROM patients;
```

**20. Find patients born in specific months (e.g., June).**
```sql
SELECT first_name, last_name, date_of_birth 
FROM patients 
WHERE MONTH(date_of_birth) = 6;
```

**21. Show appointments scheduled for today.**
```sql
SELECT * FROM appointments 
WHERE DATE(appointment_datetime) = CURDATE();
```

## **String Functions**

**22. Concatenate patient full names.**
```sql
SELECT CONCAT(first_name, ' ', last_name) AS full_name, phone_number 
FROM patients;
```

**23. Find patients whose email domain is 'email.com'.**
```sql
SELECT first_name, last_name, email 
FROM patients 
WHERE email LIKE '%@email.com';
```

**24. Get the length of department descriptions.**
```sql
SELECT department_name, LENGTH(description) as description_length 
FROM hospital_departments;
```

## **ORDER BY and LIMIT**

**25. List top 5 most expensive rooms.**
```sql
SELECT RoomNumber, Type, DailyRate 
FROM RoomsInfo 
ORDER BY DailyRate DESC 
LIMIT 5;
```

**26. Show patients ordered by registration date (newest first).**
```sql
SELECT first_name, last_name, registration_date 
FROM patients 
ORDER BY registration_date DESC;
```

**27. Find the 3 oldest patients.**
```sql
SELECT first_name, last_name, date_of_birth 
FROM patients 
ORDER BY date_of_birth ASC 
LIMIT 3;
```

## **HAVING Clause**

**28. Find departments with more than 2 rooms.**
```sql
SELECT hd.department_name, COUNT(r.RoomID) as room_count
FROM hospital_departments hd
JOIN RoomsInfo r ON hd.department_id = r.DepartmentID
GROUP BY hd.department_id, hd.department_name
HAVING COUNT(r.RoomID) > 2;
```

**29. Show room types with average rate above 300.**
```sql
SELECT Type, AVG(DailyRate) as avg_rate
FROM RoomsInfo
GROUP BY Type
HAVING AVG(DailyRate) > 300;
```

## **CASE Statements**

**30. Categorize patients by age groups.**
```sql
SELECT first_name, last_name,
    CASE 
        WHEN FLOOR(DATEDIFF(CURDATE(), date_of_birth)/365) < 18 THEN 'Minor'
        WHEN FLOOR(DATEDIFF(CURDATE(), date_of_birth)/365) BETWEEN 18 AND 65 THEN 'Adult'
        ELSE 'Senior'
    END AS age_category
FROM patients;
```

**31. Classify rooms by price range.**
```sql
SELECT RoomNumber, DailyRate,
    CASE 
        WHEN DailyRate < 200 THEN 'Budget'
        WHEN DailyRate BETWEEN 200 AND 400 THEN 'Standard'
        ELSE 'Premium'
    END AS price_category
FROM RoomsInfo;
```

## **UPDATE and DELETE Operations**

**32. Update room status from 'Occupied' to 'Available' for room 201.**
```sql
UPDATE RoomsInfo SET Status = 'Available' WHERE RoomNumber = '201';
```

**33. Increase daily rates by 10% for all Suite rooms.**
```sql
UPDATE RoomsInfo SET DailyRate = DailyRate * 1.10 WHERE Type = 'Suite';
```

**34. Delete a specific patient (this will trigger the backup).**
```sql
DELETE FROM patients WHERE patient_id = 1;
```

## **Advanced Queries**

**35. Find departments with no occupied rooms.**
```sql
SELECT hd.department_name 
FROM hospital_departments hd
WHERE hd.department_id NOT IN (
    SELECT DISTINCT DepartmentID FROM RoomsInfo WHERE Status = 'Occupied'
);
```

**36. Calculate occupancy rate by department.**
```sql
SELECT hd.department_name,
    COUNT(CASE WHEN r.Status = 'Occupied' THEN 1 END) as occupied_rooms,
    COUNT(*) as total_rooms,
    ROUND((COUNT(CASE WHEN r.Status = 'Occupied' THEN 1 END) * 100.0 / COUNT(*)), 2) as occupancy_rate
FROM hospital_departments hd
LEFT JOIN RoomsInfo r ON hd.department_id = r.DepartmentID
GROUP BY hd.department_id, hd.department_name;
```

**37. Find patients with the longest medical condition descriptions.**
```sql
SELECT first_name, last_name, medical_condition, LENGTH(medical_condition) as condition_length
FROM patients 
WHERE medical_condition IS NOT NULL
ORDER BY LENGTH(medical_condition) DESC 
LIMIT 5;
```

## **View Creation**

**38. Create a view for patient summary.**
```sql
CREATE VIEW patient_summary AS
SELECT patient_id, CONCAT(first_name, ' ', last_name) as full_name,
       FLOOR(DATEDIFF(CURDATE(), date_of_birth)/365) AS age,
       gender, phone_number, email
FROM patients;
```

**39. Create a view for room availability.**
```sql
CREATE VIEW room_availability AS
SELECT r.RoomNumber, r.Type, r.Status, r.DailyRate, hd.department_name
FROM RoomsInfo r
JOIN hospital_departments hd ON r.DepartmentID = hd.department_id
WHERE r.Status = 'Available';
```

## **Index Optimization Queries**

**40. Show query execution plan for patient search by phone.**
```sql
EXPLAIN SELECT * FROM patients WHERE phone_number = '01712345678';
```

**41. Create index on frequently searched columns.**
```sql
CREATE INDEX idx_patient_phone ON patients(phone_number);
CREATE INDEX idx_room_status ON RoomsInfo(Status);
```

## **Data Validation Queries**

**42. Find patients with invalid phone number formats.**
```sql
SELECT * FROM patients 
WHERE phone_number NOT REGEXP '^[0-9]{11}$' AND phone_number IS NOT NULL;
```

**43. Check for duplicate email addresses.**
```sql
SELECT email, COUNT(*) as count 
FROM patients 
WHERE email IS NOT NULL 
GROUP BY email 
HAVING COUNT(*) > 1;
```

## **Backup and Recovery Queries**

**44. View all backed up patient records.**
```sql
SELECT * FROM backup ORDER BY deleted_at DESC;
```

**45. Count how many patients were deleted in the last month.**
```sql
SELECT COUNT(*) as deleted_count 
FROM backup 
WHERE deleted_at >= DATE_SUB(CURDATE(), INTERVAL 30 DAY);
```
