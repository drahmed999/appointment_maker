# Database Layout for Dental Appointment System

---

## 1. Patients Table
- **Table Name**: `Patients`
- **Primary Key**: `ContactNumber` (Unique for each patient)
- **Columns**:
  - `ContactNumber` (Primary Key, NVARCHAR(50)): The patient's unique contact number.
  - `PatientName` (NVARCHAR(100)): Full name of the patient.
  - `DateOfBirth` (DATE): Date of birth of the patient.
  - `Age` (INT): Age of the patient.
  - `Gender` (NVARCHAR(10)): Gender of the patient (e.g., Male, Female, Other).
  - `Email` (NVARCHAR(100)): The patient's email address.
  - `Address` (NVARCHAR(250)): Home address of the patient.
  - `Notes` (NVARCHAR(500)): Additional notes (e.g., allergies, special considerations).

### Example Patients Table

| **ContactNumber** | **PatientName** | **DateOfBirth** | **Age** | **Gender** | **Email**            | **Address**         | **Notes**               |
|-------------------|-----------------|-----------------|---------|------------|----------------------|---------------------|-------------------------|
| 123-456-7890      | John Doe         | 1980-04-15      | 44      | Male       | johndoe@example.com  | 123 Main St          | No known allergies      |
| 987-654-3210      | Jane Smith       | 1990-08-22      | 34      | Female     | janesmith@example.com| 456 Elm St           | Allergic to penicillin  |

---

## 2. Dentists Table
- **Table Name**: `Dentists`
- **Primary Key**: `DentistName` (Assumed to be unique for simplicity)
- **Columns**:
  - `DentistName` (Primary Key, NVARCHAR(100)): The full name of the dentist.
  - `ContactNumber` (NVARCHAR(50)): The contact number for the dentist.
  - `Email` (NVARCHAR(100)): The email address of the dentist.
  - `Specialty` (NVARCHAR(100)): Dentist’s area of expertise (e.g., orthodontist, endodontist).
  - `Notes` (NVARCHAR(500)): Additional notes related to availability or qualifications.

### Example Dentists Table

| **DentistName**  | **ContactNumber** | **Email**             | **Specialty**  | **Notes**              |
|------------------|-------------------|-----------------------|----------------|------------------------|
| Dr. Smith        | 123-456-7890       | dr.smith@clinic.com   | Orthodontist   | Available on weekdays  |
| Dr. Johnson      | 987-654-3210       | dr.johnson@clinic.com | Endodontist    | Available in mornings  |

---

## 3. Procedures Table (with ProcedureName as Primary Key)
- **Table Name**: `Procedures`
- **Primary Key**: `ProcedureName` (Unique for each procedure)
- **Columns**:
  - `ProcedureName` (Primary Key, NVARCHAR(100)): Name of the dental procedure.
  - `Description` (NVARCHAR(500)): A detailed description of the procedure.
  - `Cost` (DECIMAL(10,2)): The cost of the procedure.

### Example Procedures Table

| **ProcedureName**  | **Description**                               | **Cost** |
|--------------------|-----------------------------------------------|----------|
| Teeth Cleaning      | Routine cleaning to remove plaque and tartar. | 100.00   |
| Teeth Whitening     | Cosmetic procedure to whiten teeth.           | 200.00   |
| Filling             | Restoring cavities with dental materials.     | 150.00   |
| Root Canal          | Endodontic treatment to save an infected tooth.| 500.00  |
| Dental Crown        | Cap placed over a damaged tooth.              | 800.00   |
| Tooth Extraction    | Removal of a damaged or decayed tooth.        | 250.00   |

---

## 4. Appointments Table
- **Table Name**: `Appointments`
- **Primary Key**: `AppointmentID` (Automatically generated)
- **Foreign Keys**:
  - `PatientContactNumber` references `Patients.ContactNumber`
  - `DentistName` references `Dentists.DentistName`
  - `ProcedureName` references `Procedures.ProcedureName`
- **Columns**:
  - `AppointmentID` (Primary Key, INT): Unique identifier for each appointment.
  - `PatientContactNumber` (Foreign Key, NVARCHAR(50)): References the patient's unique contact number.
  - `DentistName` (Foreign Key, NVARCHAR(100)): References the dentist's name.
  - `ProcedureName` (Foreign Key, NVARCHAR(100)): References the procedure name.
  - `AppointmentDateTime` (DATETIME): Date and time of the appointment.
  - `AppointmentStatus` (NVARCHAR(50)): Status of the appointment (e.g., Scheduled, Completed, Canceled).
  - `Notes` (NVARCHAR(500)): Additional notes related to the appointment (e.g., special instructions).

### Example Appointments Table

| **AppointmentID** | **PatientContactNumber** | **DentistName** | **ProcedureName** | **AppointmentDateTime** | **AppointmentStatus** | **Notes**              |
|-------------------|--------------------------|-----------------|-------------------|-------------------------|-----------------------|------------------------|
| 1                 | 123-456-7890             | Dr. Smith       | Teeth Cleaning     | 2024-09-22 10:00:00      | Scheduled              | First-time patient     |
| 2                 | 987-654-3210             | Dr. Johnson     | Root Canal         | 2024-09-23 11:30:00      | Scheduled              | Needs anesthesia       |

---

## Relationships Between Tables:
- **Patients** (`ContactNumber`) and **Appointments** (`PatientContactNumber`): Links a patient to an appointment.
- **Dentists** (`DentistName`) and **Appointments** (`DentistName`): Links a dentist to an appointment.
- **Procedures** (`ProcedureName`) and **Appointments** (`ProcedureName`): Links a specific dental procedure to an appointment.

---



## Summary of Table Layout:
- **Patients Table**: Contains patient information with **ContactNumber** as the primary key.
- **Dentists Table**: Stores dentist details with **DentistName** as the primary key.
- **Procedures Table**: Contains dental procedures with **ProcedureName** as the primary key.
- **Appointments Table**: Links patients, dentists, and procedures, and stores the appointment-specific details.
