# Veterinary Clinic Management System 🐾

A Python-based desktop application designed to manage veterinary clinic operations through Object-Oriented Programming (OOP) and a layered software architecture.

The system provides an integrated solution for managing pet owners, veterinarians, pets, and veterinary visits, with centralized data validation, relationship management, and persistent data storage.

---

## Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [Technologies](#technologies)
- [System Architecture](#system-architecture)
- [Business Rules & Workflow](#business-rules--workflow)
- [Installation](#installation)
- [Execution](#execution)
- [Project Structure](#project-structure)
- [Validation Rules](#validation-rules)
- [Data Persistence](#data-persistence)
- [Testing](#testing)
- [License](#license)

---

## Overview

The Veterinary Clinic Management System aims to simplify the organization and management of essential veterinary clinic information.

The application consists of four main management modules:

| Module | Description |
|:---|:---|
| Owners | Manages pet owner profiles and contact information. |
| Veterinarians | Stores veterinarian profiles and professional details. |
| Pets | Maintains pet records and owner relationships. |
| Visits | Manages veterinary visits, including scheduling, status, diagnosis, and treatment. |

The application is designed with a focus on modularity, data integrity, maintainability, and separation of responsibilities.

---

## Key Features

**Entity Management**
- Register and manage pet owners.
- Register and manage veterinarians.
- Create and maintain pet records.
- Schedule and manage veterinary visits.

**Data Integrity**
- Enforce unique identifiers.
- Validate user inputs through dedicated validation methods.
- Verify relationships between dependent records.
- Prevent references to non-existing entities.
- Support optional fields such as email, microchip number, diagnosis, and treatment.

**Graphical Interface**
- Desktop GUI developed with Tkinter.
- Dedicated management sections.
- Structured table views for displaying records.

**Data Management**
- Object serialization using Pickle.
- Separate storage files for each entity.
- Retrieval of previously saved records.

---

## Technologies

| Technology | Purpose |
|:---|:---|
| Python | Core programming language |
| Tkinter | Graphical User Interface |
| Object-Oriented Programming | Application design |
| Pickle | Object serialization and data persistence |
| Regular Expressions | Input validation |
| Git & GitHub | Version control |
| PyCharm | Development environment |

---

## System Architecture

The project follows a layered architecture to separate application responsibilities and improve code organization.

| Layer | Responsibility |
|:---|:---|
| Model | Defines application entities and their attributes. |
| Data Access | Handles data storage and retrieval. |
| Business Logic | Implements business rules, validation, and entity relationships. |
| Controller | Coordinates communication between the GUI and business logic. |
| View | Provides the graphical user interface. |
| Tools | Contains reusable validation utilities. |
| Test | Includes test modules for application classes. |

### Architecture Principles

- **Separation of Concerns:** Each layer has a clearly defined responsibility.
- **Modularity:** Components are organized into independent modules.
- **Reusability:** Shared functionality is implemented in reusable methods.
- **Maintainability:** The layered structure makes modifications easier.
- **Data Integrity:** Business rules ensure valid relationships between records.

---

## Business Rules & Workflow

The application enforces dependencies between entities to maintain data consistency.

### Entity Relationships

- One Owner can be associated with multiple Pets.
- Each Pet must belong to an existing Owner.
- One Veterinarian can manage multiple Visits.
- Each Visit must reference an existing Pet and Veterinarian.

### Required Registration Order

Records must be registered in the following order:

```text
Owners ─────────┐
                ├──> Pets ───> Visits
Vets ───────────┘
```

| Step | Entity | Requirement |
|:---:|:---|:---|
| 01 | Owners | Register owners with unique IDs. |
| 02 | Vets | Register veterinarians with unique IDs. |
| 03 | Pets | Reference an existing Owner ID. |
| 04 | Visits | Reference existing Pet and Vet IDs. |

**Important:** The application validates entity relationships before accepting dependent records.

---

## Installation

### Clone the Repository

```bash
git clone https://github.com/ReyhanehMahmoudabadi/Veterinary_Clinic_Management_System.git
```

### Navigate to the Project Directory

```bash
cd Veterinary_Clinic_Management_System
```

### Configure the Environment

Open the project in PyCharm or another Python IDE and ensure that Python is properly installed and configured.

No additional third-party packages are required.

---

## Execution

Run the following command from the project root directory:

```bash
python main.py
```

The main application window provides access to four management modules:

- Owners
- Vets
- Pets
- Visits

Follow the required registration workflow before creating dependent records.

---

## Project Structure

```text
Veterinary_Clinic_Management_System/
│
├── business_logic/
│   ├── __init__.py
│   ├── owner_bl.py
│   ├── pet_bl.py
│   ├── vet_bl.py
│   └── visit_bl.py
│
├── controller/
│   ├── __init__.py
│   ├── owner_controller.py
│   ├── pet_controller.py
│   ├── vet_controller.py
│   └── visit_controller.py
│
├── data_access/
│   ├── __init__.py
│   ├── owner_da.py
│   ├── pet_da.py
│   ├── vet_da.py
│   ├── visit_da.py
│   │
│   └── data/
│       ├── owner.dat
│       ├── pet.dat
│       ├── vet.dat
│       └── visit.dat
│
├── model/
│   ├── __init__.py
│   ├── person.py
│   ├── owner.py
│   ├── pet.py
│   ├── vet.py
│   └── visit.py
│
├── test/
│   ├── __init__.py
│   ├── person_test.py
│   ├── owner_test.py
│   ├── pet_test.py
│   ├── vet_test.py
│   └── visit_test.py
│
├── tools/
│   ├── __init__.py
│   └── validation.py
│
├── view/
│   ├── __init__.py
│   ├── owner_view.py
│   ├── panel_view.py
│   ├── pet_view.py
│   ├── vet_view.py
│   └── visit_view.py
│
├── main.py
│
└── README.md
```

---

## Validation Rules

Input validation is centralized in the `Validator` class, located in:

`tools/validation.py`

The application implements the following validation rules:

| Field | Validation |
|:---|:---|
| Names | Valid English letters and defined length limits |
| National ID | Exactly 10 digits |
| Phone Number | Defined mobile number format |
| Email | Valid email format (optional) |
| Owner ID / Vet ID | Positive integers |
| Pet ID | 1–10 English letters or digits |
| Gender | Male, Female, or Unknown |
| Birth Date | Valid date; cannot be in the future |
| Weight | Positive number |
| Microchip Number | Exactly 15 digits when provided |
| Visit ID | `VIS-` prefix followed by digits |
| Visit Date | Valid datetime; cannot be in the past |
| Visit Status | Scheduled, Completed, Cancelled, or Rescheduled |

Additional validation methods cover addresses, specializations, license numbers, species, breeds, visit reasons, diagnoses, and treatments.

---

## Data Persistence

The application uses Python's built-in `pickle` module to serialize and store application objects.

Each entity has a dedicated binary storage file:

| File | Description |
|:---|:---|
| `owner.dat` | Owner records |
| `vet.dat` | Veterinarian records |
| `pet.dat` | Pet records |
| `visit.dat` | Veterinary visit records |

All data files are located in:

```text
data_access/data/
```

The Data Access layer handles saving and retrieving records.

**Note:** Keep the `.dat` files in their original directory to preserve access to previously stored information.

---

## Testing

The `test/` directory contains individual test modules for the application's classes and functionality.

Available test modules:

- `person_test.py`
- `owner_test.py`
- `pet_test.py`
- `vet_test.py`
- `visit_test.py`

Each module can be executed independently to test its corresponding classes.

---

## License

No license has currently been specified for this project.

---

<p align="center">
  <b>Developed by Nazanin Montazeri</b>
</p>

<p align="center">
  Python | OOP | Tkinter | Layered Architecture
</p>