## MySQL Database Design

### Table: patients
- id: INT, Primary Key, AUTO_INCREMENT
- name: VARCHAR(100), NOT NULL
- email: VARCHAR(100), UNIQUE, NOT NULL
- phone: VARCHAR(15)
- date_of_birth: DATE
- gender: VARCHAR(10)

### Table: doctors
- id: INT, Primary Key, AUTO_INCREMENT
- name: VARCHAR(100), NOT NULL
- specialization: VARCHAR(100)
- email: VARCHAR(100), UNIQUE, NOT NULL
- phone: VARCHAR(15)
- availability: TEXT  -- stores JSON of available time slots

### Table: appointments
- id: INT, Primary Key, AUTO_INCREMENT
- doctor_id: INT, Foreign Key → doctors(id)
- patient_id: INT, Foreign Key → patients(id)
- appointment_time: DATETIME, NOT NULL
- status: INT (0 = Scheduled, 1 = Completed, 2 = Cancelled)

### Table: admin
- id: INT, Primary Key, AUTO_INCREMENT
- username: VARCHAR(50), UNIQUE, NOT NULL
- password_hash: VARCHAR(255), NOT NULL
- role: VARCHAR(20)

### Table: payments (optional)
- id: INT, Primary Key, AUTO_INCREMENT
- appointment_id: INT, Foreign Key → appointments(id)
- amount: DECIMAL(10,2)
- payment_method: VARCHAR(50)
- payment_date: DATETIME

---

## MongoDB Collection Design

### Collection: prescriptions

```json
{
  "_id": "ObjectId('64abc123456')",
  "appointmentId": 51,
  "patientId": 12,
  "medications": [
    {
      "name": "Paracetamol",
      "dosage": "500mg",
      "instructions": "Take 1 tablet every 6 hours"
    }
  ],
  "doctorNotes": "Patient reported mild fever and body ache.",
  "createdAt": "2025-07-17T10:00:00Z",
  "pharmacy": {
    "name": "Guardian Woodlands",
    "location": "Causeway Point, SG"
  }
}
