# Hospital Management Database System - Project Overview

## **Project Structure**

This is a comprehensive **Hospital Management Database System** built using MySQL that manages the core operations of a healthcare facility. The project is designed to handle patient registration, doctor management, room allocation, billing, and appointment scheduling.

## **Database Schema Overview**

### **Core Tables (6 Main Tables)**

1. **`hospital_departments`** - Department management
2. **`patients`** - Patient registration and medical records
3. **`doctors`** - Doctor information and specializations
4. **`RoomsInfo`** - Room allocation and management
5. **`appointments`** - Appointment scheduling system
6. **`billing`** - Financial transactions and payment tracking

### **Supporting Tables**
- **`backup`** - Audit trail for deleted patients

## **Key Features Implemented**

### **1. Multi-language Support**
- Patient data stored in **Bengali (বাংলা)** language
- Names, addresses, and medical conditions in Bengali script
- Demonstrates internationalization capabilities

### **2. Data Integrity & Constraints**
- **Primary Keys**: AUTO_INCREMENT for all tables
- **Foreign Key Relationships**: Maintaining referential integrity
- **Check Constraints**: Rating validation (0-5), experience validation
- **ENUM Types**: Gender, doctor status with predefined values
- **UNIQUE Constraints**: Doctor email addresses

### **3. Automated Backup System**
````sql
CREATE TRIGGER before_patient_delete
BEFORE DELETE ON patients
FOR EACH ROW
BEGIN
    INSERT INTO backup (first_name, last_name, phone_number)
    VALUES (OLD.first_name, OLD.last_name, OLD.phone_number);
END$$
````

### **4. Comprehensive Room Management**
- Different room types: Single, Double, ICU, Suite
- Status tracking: Available, Occupied
- Department-wise room allocation
- Daily rate management

## **Database Relationships**

```
hospital_departments (1) ──→ (M) doctors
hospital_departments (1) ──→ (M) RoomsInfo
patients (1) ──→ (M) billing
patients (1) ──→ (M) appointments
doctors (1) ──→ (M) appointments
RoomsInfo (1) ──→ (M) appointments
```

## **Sample Data Insights**

### **Departments (10 Departments)**
- Emergency Department, Cardiology, Orthopedics
- Pediatrics, Radiology, Surgery
- OB-GYN, Internal Medicine, Psychiatry, Oncology

### **Patients (15 Records)**
- Bengali names and addresses (Dhaka-based)
- Comprehensive medical conditions in Bengali
- Age range: 1965-1995 (30-60 years old)
- Contact information and emergency contacts

### **Rooms (15 Rooms)**
- Room numbers: 201-215
- Daily rates: ৳150-৳520
- Mixed occupancy status
- Department-wise distribution

## **Advanced Features**

### **1. Audit Trail System**
- Automatic backup of deleted patient records
- Timestamp tracking for all operations
- Data recovery capabilities

### **2. Data Validation**
- Doctor rating system (0-5 scale)
- Experience validation (must be positive)
- Status management with ENUM constraints

### **3. Financial Management**
- Decimal precision for monetary values
- Payment status tracking
- Amount paid vs total amount comparison

## **Technical Specifications**

### **Data Types Used**
- **INT AUTO_INCREMENT**: Primary keys
- **VARCHAR**: Names, contact info
- **TEXT**: Descriptions, addresses
- **DATE/DATETIME**: Dates and timestamps
- **DECIMAL(10,2)**: Financial values
- **ENUM**: Status and category fields

### **Constraints Implemented**
- **NOT NULL**: Critical fields
- **UNIQUE**: Email addresses
- **CHECK**: Rating and experience validation
- **FOREIGN KEY**: Referential integrity
- **ON DELETE RESTRICT**: Prevent accidental deletions

## **Use Cases Supported**

1. **Patient Management**: Registration, medical history, contact tracking
2. **Doctor Management**: Specialization, availability, rating system
3. **Room Management**: Allocation, pricing, occupancy tracking
4. **Appointment Scheduling**: Patient-doctor-room coordination
5. **Billing System**: Payment tracking and financial management
6. **Department Management**: Organizational structure
7. **Data Recovery**: Backup and restore functionality

## **Project Strengths**

### **1. Real-world Application**
- Bengali language support for local healthcare
- Comprehensive medical condition tracking
- Emergency contact management

### **2. Database Design Excellence**
- Proper normalization (3NF)
- Strong referential integrity
- Efficient data organization

### **3. Business Logic Implementation**
- Automated backup triggers
- Status management systems
- Financial tracking capabilities

### **4. Scalability Features**
- Room capacity management
- Department-wise organization
- Extensible table structure

## **Potential Enhancements**

1. **User Authentication System**: Role-based access control
2. **Appointment Time Slots**: Detailed scheduling
3. **Medical History Tracking**: Treatment records
4. **Inventory Management**: Medical supplies
5. **Reporting System**: Analytics and insights

This project demonstrates a solid understanding of database design principles, real-world application development, and comprehensive healthcare management system implementation using MySQL.
