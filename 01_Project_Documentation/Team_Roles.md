# Team Roles and Responsibilities
## Asset Management System – Six Members

## 1. Project Manager and Database Integration
Responsibilities:
- Coordinate the six team members.
- Maintain the approved database specification.
- Monitor project progress.
- Create and configure the SQL Server database.
- Configure the MDF, NDF, and LDF files.
- Integrate SQL scripts from the team.
- Validate the final database.
- Prepare the final submission.

Main deliverables:
- Database creation script.
- Final integrated SQL script.
- Project coordination and final validation.

## 2. ERD Designer
Responsibilities:
- Design the Entity Relationship Diagram.
- Represent all seven entities.
- Add attributes and primary keys.
- Identify foreign keys and relationships.
- Show correct cardinality.
- Prepare the digital diagram using draw.io.
- Prepare the hand-drawn version.

Main deliverables:
- ERD.drawio
- ERD.pdf
- Hand-drawn ERD image.

## 3. Mapping Diagram Designer
Responsibilities:
- Create the relational mapping diagram based on the approved ERD.
- Represent all seven relational tables.
- Show columns, primary keys, and foreign keys.
- Draw relationship arrows.
- Verify consistency with the database specification.
- Prepare the digital and hand-drawn versions.

Main deliverables:
- Mapping.drawio
- Mapping.pdf
- Hand-drawn mapping diagram image.

## 4. SQL Tables Developer
Responsibilities:
- Create the seven SQL Server tables.
- Use the approved column names and data types.
- Configure identity columns where required.
- Define primary keys.
- Define foreign key relationships.
- Test table creation.

Main deliverable:
- 01_Create_Tables.sql

## 5. Constraints Developer
Responsibilities:
- Define descriptive constraint names.
- Implement UNIQUE constraints.
- Implement CHECK constraints.
- Implement DEFAULT constraints.
- Ensure mandatory columns use NOT NULL.
- Verify the foreign key and primary key definitions.
- Test constraint behavior.

Main deliverable:
- 02_Add_Constraints.sql

## 6. Testing and Documentation Member
Responsibilities:
- Prepare realistic sample data.
- Verify relationships between tables.
- Test valid and invalid insertions.
- Test UNIQUE, CHECK, DEFAULT, and NOT NULL constraints.
- Capture screenshots of successful tests.
- Prepare the testing report.

Main deliverables:
- 03_Insert_Sample_Data.sql
- 04_Test_Constraints.sql
- Testing_Report.md
- Testing screenshots.

## Team Collaboration Rules

1. All members must follow Database_Specification.md.
2. No one should independently rename or add approved database columns without team agreement.
3. Diagrams and SQL scripts must use identical table and column names.
4. Each member is responsible for understanding the complete database design.
5. Every member should be able to explain their own work during the TA discussion.
6. Each member should also understand the primary keys, foreign keys, relationships, and constraints.
7. All work must be committed to GitHub using the agreed workflow.
