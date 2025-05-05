Snowflake SQL Development Environment with VS Code & Git
This guide walks you through setting up a local development environment to write, execute, and version-control Snowflake SQL queries using Visual Studio Code, Git, and the Snowflake extension.

Step-by-Step Setup
1. Setup Repository in VS Code
Install VS Code

Go to the official site: Visit https://code.visualstudio.com

Download the installer: Click on the "Download for Windows" button to get the .exe installer.

Run the installer: Double-click the downloaded .exe file.

Follow setup instructions:

Accept the license agreement.
Choose install location.
Optional: Check boxes for “Add to PATH”, “Add ‘Open with Code’ to context menu”.
Click ‘Install’, then ‘Finish’.

Launch VS Code: Use the Start menu or desktop shortcut.

Create or Clone a Git Repository

Open Terminal in VS Code (ctrl+`) and execute below commands:

git clone https://github.com/your-username/snowflake-dwh-queries.git
cd snowflake-dwh-queries
Create folder structure

mkdir queries
touch README.md
2. Install Snowflake Extension for VS Code
Open the Extensions tab in VS Code (Ctrl + Shift + X)
Search for "Snowflake" link to Extension
Click Install
This extension allows you to connect to Snowflake and execute SQL queries directly within VS Code.

3. Authenticate Snowflake in VS Code
Press Ctrl+Shift+P (Command Palette), then search for:

Snowflake: Edit Connection File
This can be done using Snowflake extension user interface too.

Provide the required connection details:

Account: xy12345.east-us-2.azure (replace with your Snowflake account locator)
Username/Password: Your Snowflake credentials
Warehouse: COMPUTE_WH (or your configured warehouse)
Database: DEMO_DB
Schema: PUBLIC
Role (optional): SYSADMIN
Save the connection as a named profile (e.g., my_snowflake).

A .toml file will be auto-generated at location : C:\Users\your_user\.snowflake\connections.toml

[connections.my_snowflake]
account = "xy12345.east-us-2.azure"
user = "your_username"
password = "your_password"
role = "SYSADMIN"
warehouse = "COMPUTE_WH"
database = "DEMO_DB"
schema = "PUBLIC"
4. Write and Execute SQL Queries
Create SQL files inside the queries/ folder:

touch queries/01_create_tables.sql
Example content:

CREATE OR REPLACE TABLE employees (
  id INT,
  name STRING,
  department STRING,
  hire_date DATE
);
To run the query:

Open the .sql file
Right-click anywhere inside the editor
Select "Execute Query in Snowflake"
The output appears in the Results tab within VS Code.

5. Commit SQL Code and Push to Git Repository
Add changes:

git add .
Commit with a message:

git commit -m "Added initial SQL table creation script"
Push to remote:

git push origin main
Use GitHub/GitLab/Bitbucket as the remote to store and collaborate on your SQL codebase.

Example Project Structure
snowflake-dwh-queries/
│
├── queries/
│   ├── 01_create_tables.sql
│   ├── 02_insert_data.sql
│   └── ...
└── README.md              # This documentation
Use Cases of Version Control
1. Version Control for DWH Logic
Track changes to:

DDL scripts (create/alter tables, views)
DML scripts (insert/update/delete)
Business logic (stored procedures, UDFs, views)
Comment history, rollback, and code reviews
2. Team Collaboration
Collaborate on query development using Git branches and pull requests
Perform peer code reviews for data quality and logic validation
Enforce standards with pre-commit hooks or linters
3. Release Management / CI-CD
Automate deployment of SQL changes via Git workflows (e.g., GitHub Actions, Azure DevOps)
Use tools like SchemaChange, Liquibase, or Flyway for managing schema migrations
Tag and release versions of your data models
4. Development-Test-Prod Promotion
Maintain separate folders or branches for dev, staging, and production environments
Use environment-specific Snowflake connections in .toml profiles
Automate promotion using scripts
5. Metadata & Data Lineage Tracking
Document table-level metadata
Use consistent naming and folder conventions
Integrate with data catalog tools (e.g., Alation, Atlan) using SQL codebase
6. Audit & Compliance
Maintain audit trails of who changed what, when, and why
Prove compliance with change management policies in regulated environments (e.g., HIPAA, GDPR, SOX)
7. Template and Boilerplate Scripts
Share reusable SQL templates for creating standard tables, SCD patterns, CDC patterns, etc.
Onboard new developers with starter kits
8. Testing SQL Logic
Store test datasets as insert scripts
Write SQL unit tests using tools like dbt tests or manual assertions
