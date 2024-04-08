# Data-Science


import sqlite3

# Connect to the SQLite database 
conn = sqlite3.connect('my_database.db')

# Create a cursor object to interact with the database
cursor = conn.cursor()

# Create the Ages table if not exists
cursor.execute('''
CREATE TABLE IF NOT EXISTS Ages (
  name VARCHAR(128),
  age INTEGER
)
''')

# Delete any existing rows in the Ages table
cursor.execute('DELETE FROM Ages')

# Insert the provided rows into the Ages table
rows_to_insert = [
    ('Mara', 28),
    ('Otto', 33),
    ('Fyn', 31),
    ('Neshawn', 17)
]
cursor.executemany('INSERT INTO Ages (name, age) VALUES (?, ?)', rows_to_insert)

# Commit changes to the database
conn.commit()

# Run the SQL command to concatenate name and age, convert to hexadecimal, and order the results
cursor.execute('SELECT hex(name || age) AS X FROM Ages ORDER BY X')

 # Fetch all rows from the result set
result_rows = cursor.fetchall()

# Find and print the first row
if result_rows:
    first_row = result_rows[0][0]
    print("The first row in the resulting record set:", first_row)

# Close the cursor and the connection
cursor.close()
conn.close()