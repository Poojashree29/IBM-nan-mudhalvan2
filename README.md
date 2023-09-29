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
