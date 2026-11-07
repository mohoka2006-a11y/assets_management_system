# Project Workflow
## Asset Management System

## Phase 1 – Project Organization
1. Confirm the selected system: Asset Management System.
2. Confirm the seven approved tables.
3. Assign responsibilities to six team members.
4. Create the GitHub repository.
5. Create the project folder structure.
6. Maintain Database_Specification.md as the source of truth.

## Phase 2 – Database Design
1. Design the ERD.
2. Review all entities and attributes.
3. Identify primary keys.
4. Identify foreign keys.
5. Confirm relationship cardinality.
6. Prepare the relational mapping diagram.
7. Review both diagrams against the database specification.

## Phase 3 – SQL Server Database Creation
1. Create the database using Microsoft SQL Server.
2. Configure at least one primary MDF data file.
3. Configure at least one secondary NDF data file.
4. Configure at least two LDF transaction log files.
5. Define SIZE, MAXSIZE, and FILEGROWTH for every file.
6. Verify that the database is created successfully.

## Phase 4 – Table Creation
1. Create Categories.
2. Create Locations.
3. Create Employees.
4. Create Assets.
5. Create AssetAssignments.
6. Create Maintenance.
7. Create Disposals.
8. Verify all primary and foreign key relationships.

## Phase 5 – Constraints
1. Add UNIQUE constraints.
2. Add CHECK constraints.
3. Add DEFAULT constraints.
4. Verify NOT NULL requirements.
5. Test the constraints with valid and invalid records.

## Phase 6 – Testing
1. Insert sample data.
2. Verify table relationships.
3. Test primary keys.
4. Test foreign keys.
5. Test UNIQUE constraints.
6. Test CHECK constraints.
7. Test DEFAULT values.
8. Test NOT NULL columns.
9. Record the results.
10. Capture screenshots.

## Phase 7 – Final Submission
1. Review the database.
2. Review the ERD.
3. Review the mapping diagram.
4. Verify all SQL scripts.
5. Prepare the final integrated SQL script.
6. Prepare the final report.
7. Check all required files.
8. Submit the project.

## GitHub Collaboration Workflow

### Main Branch
The main branch contains the approved project version.

### Working Branches
Each member should work on a separate branch.

Suggested branch names:
- project-setup
- member-2-erd
- member-3-mapping
- member-4-sql-tables
- member-5-constraints
- member-6-testing

### Pull Request Process
1. Create or switch to your assigned branch.
2. Make your changes.
3. Save and test your work.
4. Commit your changes.
5. Push your branch to GitHub.
6. Open a Pull Request targeting main.
7. Review the changes for consistency.
8. Merge the Pull Request when ready.

The repository is configured to require Pull Requests before merging. Mandatory approving reviews are not required.

### Important Git Rules
- Do not work directly on main.
- Do not force-push to main.
- Do not commit SQL Server database files (.mdf, .ndf, .ldf).
- Commit SQL scripts, diagrams, documentation, and relevant screenshots.
- Pull the latest main branch before starting new work.
- Keep all deliverables organized in their designated folders.

## Individual Discussion Preparation

Every team member should be able to:
- Explain the purpose of the seven tables.
- Identify primary keys and foreign keys.
- Explain one-to-many relationships.
- Explain the many-to-many relationship.
- Explain the linking table.
- Create a table.
- Add or remove a constraint.
- Alter a column.
- Explain the database file structure.
