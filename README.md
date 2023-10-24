# IBM-nan-mudhalvan2
import ibm_db

# Replace these values with your IBM Db2 Warehouse credentials
dsn_hostname = "your-hostname"
dsn_uid = "your-username"
dsn_pwd = "your-password"
dsn_database = "your-database-name"
dsn_port = "your-port"

# Create a connection string
dsn = (
    "DRIVER={{IBM DB2 ODBC DRIVER}};"
    "DATABASE={0};"
    "HOSTNAME={1};"
    "PORT={2};"
    "PROTOCOL=TCPIP;"
    "UID={3};"
    "PWD={4};".format(dsn_database, dsn_hostname, dsn_port, dsn_uid, dsn_pwd)
)

# Connect to the database
conn = ibm_db.connect(dsn, "", "")

# Execute a SQL query
sql = "SELECT * FROM your_table"
stmt = ibm_db.exec_immediate(conn, sql)

# Fetch and print the results
while ibm_db.fetch_row(stmt):
    result = ibm_db.result(stmt, "COLUMN_NAME")
    print(result)

# Close the connection
ibm_db.close(conn)
CREATE DATABASE MYDB;

-- Connect to the new database
CONNECT TO MYDB;

-- Create a new table
CREATE TABLE Employee (
    EmployeeID INT,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    Department VARCHAR(50)
);

-- Insert data into the Employee table
INSERT INTO Employee (EmployeeID, FirstName, LastName, Department)
VALUES
    (1, 'John', 'Doe', 'HR'),
    (2, 'Alice', 'Smith', 'Marketing'),
    (3, 'Bob', 'Johnson', 'Finance');

-- Retrieve data from the Employee table
SELECT * FROM Employee;

-- Update data
UPDATE Employee
SET Department = 'Sales'
WHERE EmployeeID = 1;

-- Delete data
DELETE FROM Employee WHERE EmployeeID = 3;

-- Disconnect from the database
DISCONNECT;

-- Drop the database (be cautious with this command)
DROP DATABASE MYDBS;
import pandas as pd
import psycopg2

# Extract data from a database
connection = psycopg2.connect(database="mydb")
data = pd.read_sql("SELECT * FROM Sales", connection)

# Transform data
data['TotalAmount'] = data['Quantity'] * data['Price']

# Load data into another database
data.to_sql("SalesSummary", connection, if_exists='replace')
