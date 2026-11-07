# Database Specification
## Asset Management System

## 1. Introduction
The Asset Management System is designed to manage an organization's physical assets and their related information.

The database stores information about asset categories, organizational locations, employees, assets, asset assignments, maintenance activities, and disposals.

## 2. Database Management System
Microsoft SQL Server.

## 3. Database Storage Requirements
The database must use multiple physical files:

- One primary data file (.mdf).
- At least one secondary data file (.ndf).
- At least two transaction log files (.ldf).

Every database file must have explicitly configured:
- Initial SIZE.
- MAXSIZE.
- FILEGROWTH.

A separate filegroup may be used for the secondary data file.

Physical file paths must be configured according to the SQL Server installation environment.

## 4. Database Tables

### Table 1: Categories
Stores the categories used to classify organizational assets.

| Column | Data Type | Constraints |
|---|---|---|
| CategoryID | INT IDENTITY(1,1) | Primary Key |
| CategoryName | NVARCHAR(100) | NOT NULL, UNIQUE |
| Description | NVARCHAR(255) | NULL |

### Table 2: Locations
Stores the physical locations where assets are registered.

| Column | Data Type | Constraints |
|---|---|---|
| LocationID | INT IDENTITY(1,1) | Primary Key |
| LocationName | NVARCHAR(100) | NOT NULL |
| Building | NVARCHAR(100) | NULL |
| RoomNumber | NVARCHAR(30) | NULL |

### Table 3: Employees
Stores employee information.

| Column | Data Type | Constraints |
|---|---|---|
| EmployeeID | INT IDENTITY(1,1) | Primary Key |
| FullName | NVARCHAR(150) | NOT NULL |
| Email | VARCHAR(150) | NOT NULL, UNIQUE |
| Phone | VARCHAR(20) | NULL |
| JobTitle | NVARCHAR(100) | NULL |

### Table 4: Assets
Stores the organization's registered assets.

| Column | Data Type | Constraints |
|---|---|---|
| AssetID | INT IDENTITY(1,1) | Primary Key |
| AssetName | NVARCHAR(150) | NOT NULL |
| SerialNumber | VARCHAR(100) | NOT NULL, UNIQUE |
| CategoryID | INT | NOT NULL, Foreign Key |
| LocationID | INT | NOT NULL, Foreign Key |
| PurchaseDate | DATE | NOT NULL |
| PurchaseCost | DECIMAL(12,2) | NOT NULL, CHECK >= 0 |
| Status | VARCHAR(30) | NOT NULL, DEFAULT 'Available', CHECK |

Allowed asset statuses:
- Available
- Assigned
- Under Maintenance
- Disposed

### Table 5: AssetAssignments
Records the assignment history between assets and employees.

| Column | Data Type | Constraints |
|---|---|---|
| AssignmentID | INT IDENTITY(1,1) | Primary Key |
| AssetID | INT | NOT NULL, Foreign Key |
| EmployeeID | INT | NOT NULL, Foreign Key |
| AssignedDate | DATE | NOT NULL |
| ReturnDate | DATE | NULL |
| Notes | NVARCHAR(255) | NULL |

Business rule:
ReturnDate must not be earlier than AssignedDate.

### Table 6: Maintenance
Stores maintenance records for assets.

| Column | Data Type | Constraints |
|---|---|---|
| MaintenanceID | INT IDENTITY(1,1) | Primary Key |
| AssetID | INT | NOT NULL, Foreign Key |
| TechnicianID | INT | NOT NULL, Foreign Key to Employees |
| MaintenanceDate | DATE | NOT NULL |
| Description | NVARCHAR(255) | NOT NULL |
| Cost | DECIMAL(12,2) | NOT NULL, CHECK >= 0 |
| Status | VARCHAR(30) | NOT NULL, DEFAULT 'Pending', CHECK |

Allowed maintenance statuses:
- Pending
- In Progress
- Completed

### Table 7: Disposals
Stores information about assets that have been disposed of.

| Column | Data Type | Constraints |
|---|---|---|
| DisposalID | INT IDENTITY(1,1) | Primary Key |
| AssetID | INT | NOT NULL, Foreign Key, UNIQUE |
| ApprovedByEmployeeID | INT | NOT NULL, Foreign Key to Employees |
| DisposalDate | DATE | NOT NULL |
| Reason | NVARCHAR(255) | NOT NULL |
| DisposalValue | DECIMAL(12,2) | NOT NULL, CHECK >= 0 |

The UNIQUE constraint on AssetID ensures that an asset has no more than one disposal record.

## 5. Primary Keys
Every table has one primary key:

- Categories.CategoryID
- Locations.LocationID
- Employees.EmployeeID
- Assets.AssetID
- AssetAssignments.AssignmentID
- Maintenance.MaintenanceID
- Disposals.DisposalID

## 6. Foreign Keys

The database contains eight foreign key relationships:

1. Assets.CategoryID references Categories.CategoryID.
2. Assets.LocationID references Locations.LocationID.
3. AssetAssignments.AssetID references Assets.AssetID.
4. AssetAssignments.EmployeeID references Employees.EmployeeID.
5. Maintenance.AssetID references Assets.AssetID.
6. Maintenance.TechnicianID references Employees.EmployeeID.
7. Disposals.AssetID references Assets.AssetID.
8. Disposals.ApprovedByEmployeeID references Employees.EmployeeID.

## 7. Relationships and Cardinality

### One-to-Many Relationships
- Categories (1) → Assets (Many).
- Locations (1) → Assets (Many).
- Assets (1) → AssetAssignments (Many).
- Employees (1) → AssetAssignments (Many).
- Assets (1) → Maintenance (Many).
- Employees (1) → Maintenance (Many).
- Employees (1) → Disposals (Many).

### One-to-Zero-or-One Relationship
- Assets (1) → Disposals (0..1).

The UNIQUE constraint on Disposals.AssetID enforces the maximum of one disposal record per asset.

### Many-to-Many Relationship
Employees and Assets have a Many-to-Many relationship.

This relationship is resolved using the linking table AssetAssignments:

- One employee can have multiple asset assignments.
- One asset can have multiple assignment records over time.

## 8. Constraints Requirements

The implementation must include:

| Constraint | Minimum Requirement | Planned Implementation |
|---|---:|---|
| PRIMARY KEY | Every table | 7 |
| FOREIGN KEY | 4 | 8 |
| UNIQUE | 2 columns | CategoryName, Email, SerialNumber, Disposals.AssetID |
| CHECK | 3 columns | PurchaseCost, Cost, Status, ReturnDate, DisposalValue |
| DEFAULT | 2 columns | Assets.Status, Maintenance.Status |
| NOT NULL | Mandatory columns | All required fields |

All constraints should use descriptive names.

## 9. Business Rules

1. Every asset must belong to one category.
2. Every asset must have one registered location.
3. Every asset assignment must reference an existing employee and asset.
4. An asset may have multiple assignment records over time.
5. An asset must not have overlapping active assignments.
6. A disposed asset must not receive a new assignment.
7. ReturnDate cannot be earlier than AssignedDate.
8. An asset may have at most one disposal record.
9. Every maintenance record must reference an existing asset and technician.
10. Asset and maintenance statuses must use the permitted values.

Important implementation note:
Some business rules, such as preventing overlapping active assignments and preventing assignments of disposed assets, require additional enforcement through triggers or application logic. They are not guaranteed by ordinary CHECK constraints alone.

## 10. Diagrams

The project requires:

### Entity Relationship Diagram (ERD)
Must include:
- Seven entities.
- Attributes.
- Primary keys.
- Foreign keys.
- Relationships.
- Cardinality.

### Relational Mapping Diagram
Must include:
- Seven relational tables.
- Columns and data types.
- Primary keys.
- Foreign keys.
- Relationship arrows.

Both diagrams must be prepared digitally using draw.io and also hand-drawn on paper, according to the project instructions.

## 11. SQL Script Organization

00_Create_Database.sql
Creates the database and configures its physical files.

01_Create_Tables.sql
Creates the seven tables.

02_Add_Constraints.sql
Adds the required constraints.

03_Insert_Sample_Data.sql
Inserts test records.

04_Test_Constraints.sql
Tests the database constraints and relationships.

## 12. Scope
This document defines the approved database structure for Phase 1. Any structural changes must be discussed with the team and reflected consistently in the diagrams and SQL scripts.
