# HospitalManagementSystem
SQL Database Model of an example Hospital management System (MySQL)


This project was inspired by https://github.com/hrishikeshathalye/Hospital-Management-System-DBMS. It uses similar ER structure; although, I've added, manipulated, and
altered the structure to create my own mock database. Below is the majority of the code used to create this system

Note: I used auto_increment with my INT ID's because MySQL doesn't use sequences. I have included the Sequences I would have used for the ID's in [], although they 
were not used in this model.

Hospital Management System Database:
CREATE TABLE Patient (
Patient_Id INT AUTO_INCREMENT Primary Key,
Email VARCHAR(50) NOT NULL,
P_Password VARCHAR(30) NOT NULL,
P_Name VARCHAR(50) NOT NULL,
Gender VARCHAR(6) NOT NULL CHECK (Gender IN ('Male' , 'Female'))
);

CREATE TABLE Address (
ID INT AUTO_INCREMENT Primary Key,
Street_Number VARCHAR(10) NOT NULL,
Address_Line_1 VARCHAR(30) NOT NULL,
Address_Line_2 VARCHAR(20),
City VARCHAR(25) NOT NULL,
Postal_Code VARCHAR(5) NOT NULL,
Country VARCHAR(30) NOT NULL);

CREATE TABLE Patient_Address (
Patient_ID INT,
Address_ID INT,
foreign key (patient_id) REFERENCES patient(patient_id) ON DELETE CASCADE,
foreign key (address_id) references address(ID) ON DELETE SET NULL
);

CREATE TABLE Doctor (
Doctor_ID INT AUTO_INCREMENT Primary Key,
Email VARCHAR(50) NOT NULL,
Name VARCHAR(50) NOT NULL,
Password VARCHAR(30) NOT NULL,
Gender VARCHAR(6)
);

CREATE TABLE Appointments (
Appointment_ID INT AUTO_INCREMENT PRIMARY KEY,
DATE DATE NOT NULL,
Start_Time TIME  NOT NULL,
End_Time Time NOT NUll,
Status VARCHAR(10)
);

CREATE TABLE Medical_History (
History_ID INT AUTO_INCREMENT Primary Key,
Date Date NOT NULL,
Conditions VARCHAR(50) NOT NULL,
Surgeries VARCHAR(50) NOT NULL,
Medications VARCHAR(50) NOT NULL
);

CREATE TABLE Diagnose (
 Appointment_ID INT Primary Key,
 Doctor_ID INT Primary Key,
 Diagnosis VARCHAR(50) NOT NULL,
 Prescription varchar(50) NOT NULL,
 foreign key (Appointment_ID) references Appointments(Appointment_ID) ON DELETE SET NULL,
 foreign key (Doctor_ID) references Doctor(Doctor_ID) ON DELETE SET NULL
 );

CREATE TABLE Schedules (
Doctor_ID INT NOT NULL,
Date Date NOT NULL,
Start_Time Time NOT NULL,
End_Time Time NOT NULL,
Break_Time Time Not NULL
);

ALTER TABLE schedules 
ADD PRIMARY KEY(Doctor_ID, Date);

ALTER TABLE schedules 
ADD foreign key (Doctor_ID) references Doctor(Doctor_ID) ON DELETE CASCADE;

CREATE TABLE PatientAttendAppointments (
Patient_ID INT,
Appointment_ID INT,
Concerns VARCHAR(80),
Symptoms VARCHAR(50),
foreign key (patient_id) references Patient(Patient_ID) ON DELETE CASCADE,
foreign key (appointment_id) references Appointments(Appointment_ID) ON DELETE SET NULL
);

ALTER TABLE PatientAttendAppointments 
ADD primary key (patient_id, appointment_id);

ALTER TABLE Medical_History
ADD Doctor_ID INT;

ALTER TABLE Medical_History
ADD foreign key (doctor_id) references Doctor(Doctor_ID) ON DELETE SET NULL;

CREATE TABLE PatientHistoryIndex (
Patient INT,
History_ID INT,
foreign key (patient) references Patient(Patient_ID) ON DELETE CASCADE,
foreign key (history_ID) references Medical_History(History_ID) ON DELETE SET NULL
);

ALTER TABLE PatientHistoryIndex
ADD primary key (history_id)

[
CREATE SEQUENCE Patient_Id_Sequence
START WITH 100000
INCREMENT BY 1
MINVALUE 100000
MAXVALUE 199999
NOCYCLE

CREATE SEQUENCE Doctor_Id_Sequence
START WITH 200000
INCREMENT BY 1
MINVALUE 200000
MAXVALUE 299999
NOCYCLE

CREATE SEQUENCE History_Id_Sequence
START WITH 300000
INCREMENT BY 1
MINVALUE 300000
MAXVALUE 399999
NOCYCLE

CREATE SEQUENCE Appointment_ID_Sequence
START WITH 400000
INCREMENT BY 1
MINVALUE 400000
MAXVALUE 499999
NOCYCLE

CREATE SEQUENCE Address_Id_Sequence
START WITH 500000
INCREMENT BY 1
MINVALUE 500000
MAXVALUE 599999
NOCYCLE
]

Thank you!
