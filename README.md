# Study.com-ADBP-1

Prompt 1 - Create the Schema/Database
  - Let's call it 'finalproject'. Type the name in and then click the Apply button at the lower-right corner of the window.

  - From the finalproject schema, create a new table and label it users. The following fields should be created:

      userid
      name
      username
      address
      city
      state
      zip
      We must also think about the data types of each of these attributes in the users table. We can make the data types to be:
      
      userid - numeric, integer, not null, primary key, unique, auto-increment
      name - alphanumeric
      username - alphanumeric (20 characters)
      address - alphanumeric
      city - alphanumeric
      state - alphanumeric (2 characters)
      zip - numeric (integer, 5 digits)
      The second table we will need is the one to hold the locations for people and locations where the photos were taken. This table will be called locations. It needs to contain two items for identification and another two items for the actual location.
      
      itemid - numeric, integer, not null, auto-increment
      type - numeric, integer
      description - alphanumeric
      lng, real
      lat, real


    Name this table photographs.

    photoid - numeric, integer
    locationid - numeric , integer



    CREATE TABLE users (
    userid SERIAL PRIMARY KEY,// serial es especificamenete para PostgreSQL
    name VARCHAR(255),
    username VARCHAR(20),
    address VARCHAR(255),
    city VARCHAR(255),
    state CHAR(2),
    zip INTEGER,
    CONSTRAINT unique_username UNIQUE (username)
);

CREATE TABLE users (
    userid INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255),
    username VARCHAR(20),
    address VARCHAR(255),
    city VARCHAR(255),
    state CHAR(2),
    zip INT(5),
    CONSTRAINT unique_username UNIQUE (username)
); 

CREATE TABLE locations (
    itemid INT AUTO_INCREMENT PRIMARY KEY,
    type INT,
    description VARCHAR(255),
    lng REAL,
    lat REAL
);

CREATE TABLE photographs (
    photoid INT AUTO_INCREMENT PRIMARY KEY,
    locationid INT
);


users: Contains information about users of the database. It has fields for userid, name, username, address, city, state, and zip. The userid is a primary key and auto-incremented. The username is also set to be unique.

locations: Stores information about the locations, whether it's for a person or a photograph. It includes fields for itemid, type, description, lng (longitude), and lat (latitude). Itemid is a primary key and auto-incremented.

photographs: Holds information about photographs, linking them to their respective locations. It has fields for photoid (unique identifier for each photograph) and locationid (which refers to the itemid in the locations table).


Prompt 3 - Alter Tables


ALTER TABLE users MODIFY userid INT NOT NULL;
This will change the field userid in the table users so that this field cannot have NULL values. You will have to modify your own code to match the requirements of the following:

Create a new SQL statement and modify the following fields so that they are not null.

Table	Field(s)
locations	type, description, lng, lat
users	name, username
photograph	photoid, locationid


-- Disable safe update mode
SET SQL_SAFE_UPDATES = 0;

-- Update existing NULL values with appropriate defaults
UPDATE locations SET type = 0 WHERE type IS NULL;
UPDATE locations SET description = '' WHERE description IS NULL;
UPDATE locations SET lng = 0.0 WHERE lng IS NULL;
UPDATE locations SET lat = 0.0 WHERE lat IS NULL;

-- Alter the columns to NOT NULL
ALTER TABLE locations MODIFY COLUMN type INT NOT NULL;
ALTER TABLE locations MODIFY COLUMN description VARCHAR(255) NOT NULL;
ALTER TABLE locations MODIFY COLUMN lng REAL NOT NULL;
ALTER TABLE locations MODIFY COLUMN lat REAL NOT NULL;

ALTER TABLE users MODIFY COLUMN name VARCHAR(255) NOT NULL;
ALTER TABLE users MODIFY COLUMN username VARCHAR(20) NOT NULL;

ALTER TABLE photographs MODIFY COLUMN photoid INT NOT NULL;
ALTER TABLE photographs MODIFY COLUMN locationid INT NOT NULL;

-- Re-enable safe update mode
SET SQL_SAFE_UPDATES = 1;


ALTER TABLE locations ALTER COLUMN type SET NOT NULL;
ALTER TABLE locations ALTER COLUMN description SET NOT NULL;
ALTER TABLE locations ALTER COLUMN lng SET NOT NULL;
ALTER TABLE locations ALTER COLUMN lat SET NOT NULL;

ALTER TABLE users ALTER COLUMN name SET NOT NULL;
ALTER TABLE users ALTER COLUMN username SET NOT NULL;

ALTER TABLE photographs ALTER COLUMN photoid SET NOT NULL;
ALTER TABLE photographs ALTER COLUMN locationid SET NOT NULL;


Prompt 4 - Create Index

CREATE UNIQUE INDEX id ON users (userid);

This statement creates an index called id where each KEY will be unique (different from any other). The table users will be used and the index will be based on the first named userid.

Now that the index is created on the users table, add an index for the photograph table. Be sure to use an index identifier that is unique but meaningful (e.g., not xddkrer).

CREATE INDEX idx_locationid ON photographs (locationid);

CREATE UNIQUE INDEX idx_userid ON users (userid);
CREATE INDEX idx_locationid ON photographs (locationid);




Prompt 5 - Enter Data

Now let's enter some data into the database.

We will enter data for the following four individuals.

Userid	name	username	address	city	state	zip
1	Bonnie Buntcake	bbunt	6709 Wonder Street	Wonderbread	OH	46106
2	Sam Smarf	ssmarf	356 A Street	Beefy	PA	19943
3	Wendy Grog	wgrog	900 Star Street	Mary	MD	21340
4	Joe Jogger	jjogger	183713 N North Street	Norther	WV	51423
To enter data into a table you can use the INSERT statement.

INSERT INTO table_name (column1, column2, …)

INSERT INTO users VALUES ('Bonnie Buntcake', 'bbunt', '6709 Wonder Street', 'Wonderbread', 'OH', 46105);


truncate users;

INSERT INTO users (name, username, address, city, state, zip) VALUES 
('Bonnie Buntcake', 'bbunt', '6709 Wonder Street', 'Wonderbread', 'OH', 46105),
('Sam Smarf', 'ssmarf', '356 A Street', 'Beefy', 'PA', 19943),
('Wendy Grog', 'wgrog', '900 Star Street', 'Mary', 'MD', 21340),
('Joe Jogger', 'jjogger', '183713 N North Street', 'Norther', 'WV', 51423);

SELECT * FROM users;




Prompt 6 - Count Rows
If you want to determine the number of rows in a table you can enter the query

SELECT count(*) from users;

Execute this command and paste the results under Prompt 6.

SELECT COUNT(*) FROM users;


Prompt 7 - Add Column
In the photograph table we accounted for the id of the location and the id of the photo in the photo library, but we did not include the location of the photographer. We need to add a field to this table to allow this data to be stored. The field will be called userid.

We used the following statement to make this modification to the table. Use the ALTER command with the following syntax:

ALTER TABLE {table name} ADD COLUMN {column} {data type} AFTER {column}

Paste the SQL code in the Word document under Prompt 7.

Next, Inspect the new table, clicking on the Columns tab. Take a screen capture, and place it in the word file that will contain all of your screen captures. Label this screen capture Prompt 7.

ALTER TABLE photographs ADD COLUMN userid INT AFTER locationid;



Prompt 8 - Issue with New Column
The new column is still incorrect. Can you say how? Hint: How did we modify our columns earlier to ensure data integrity? What data integrity issues will arise if we do not update the column?

Take screen print(s) of any updates you make, and type an answer (100 to 200 words) into the word file containing your screen captures and label this answer Prompt 8.

The issue with the new column userid in the photographs table is that it lacks constraints to ensure data integrity. Specifically, it lacks a FOREIGN KEY constraint, which would enforce referential integrity between the userid column in the photographs table and the userid column in the users table.

Without this constraint, data integrity issues may arise, such as the possibility of inserting userid values into the photographs table that do not correspond to existing userid values in the users table. This could lead to inconsistencies and orphaned records.

To address this, we need to add a FOREIGN KEY constraint to the userid column in the photographs table, referencing the userid column in the users table. This constraint will ensure that only valid userid values from the users table can be inserted into the photographs table.

After adding the FOREIGN KEY constraint, it's crucial to inspect the table to confirm that the constraint has been applied correctly.


ALTER TABLE photographs ADD CONSTRAINT fk_userid FOREIGN KEY (userid) REFERENCES users(userid);

ALTER TABLE photographs 
ADD CONSTRAINT fk_userid 
FOREIGN KEY (userid) 
REFERENCES users(userid);

Prompt 9 - Location and Photograph Table Updates
Next we will define some data for the remaining tables. The locations table and the photographs table still require some data to be defined for them.

The locations table will contain the following data.

itemid	type	description	lng	lat
N/A, will be auto-numbered	1	Independence Hall	794.35	651.43
N/A, will be auto-numbered	2	6709 Wonder Street	323.41	412.22
N/A, will be auto-numbered	1	Sunrise	221.45	132.43
N/A, will be auto-numbered	2	356 A Street	123.32	222.43
N/A, will be auto-numbered	1	Mountains	34.12	87.99
N/A, will be auto-numbered	2	900 Star Street	1071.9	206.45
N/A, will be auto-numbered	1	Moonrise	816.2	111.2
N/A, will be auto-numbered	2	183714 N North Street	176.11	11.176
The photograph table will contain the following data. Be sure the locationid entered matches a location that you created earlier!

photoid	locationid	userid
1	?	1
2	?	1
3	?	3
4	?	4
Execute the proper SQL command(s). Paste both the SQL commands and screen captures of each table under Prompt 9.


INSERT INTO locations (type, description, lng, lat) VALUES
(1, 'Independence Hall', 794.35, 651.43),
(2, '6709 Wonder Street', 323.41, 412.22),
(1, 'Sunrise', 221.45, 132.43),
(2, '356 A Street', 123.32, 222.43),
(1, 'Mountains', 34.12, 87.99),
(2, '900 Star Street', 1071.9, 206.45),
(1, 'Moonrise', 816.2, 111.2),
(2, '183714 N North Street', 176.11, 11.176);


SELECT * FROM locations;

INSERT INTO photographs (locationid, userid) VALUES
(1, 1),
(2, 1),
(3, 3),
(4, 4);


Prompt 10 - Users
Now you've created and populated the three tables that make up your database. The next step is to see what we can find out from this database.

First, let's see who is taking pictures. We can do this by selecting the names from the users table.

SELECT name FROM users;

Execute these command(s). When the new screen appears, capture it and place it in the word file that will contain all of your screen captures. Label this screen capture Prompt 10.


Prompt 11 - Who's Taking Pictures?
Now let's see who's actually taken a photo by comparing the list of users to those who have an entry in the photographs table.

SELECT name FROM users, photographs WHERE {where condition}

Complete the WHERE statement, ensuring that you are returning users that have taken pictures (which field(s) are related between the tables?

Execute these command. When the new screen appears, capture it and place it in the word file that will contain all of your screen captures. Be sure to copy the SQL statement as well. Label this screen capture Prompt 11.


SELECT name FROM users, photographs WHERE users.userid = photographs.userid;

SELECT DISTINCT users.name
FROM users
INNER JOIN photographs ON users.userid = photographs.userid;



Prompt 12 - Unique Names
Notice that this query has told us that Bonnie Buntcake, Wendy Grog, and Joe Jogger all have photos in the photographs table. In the case of Bonnie Buntcake though, she has taken two photos.

Supposing we only want names that are unique, i.e., we are not interested in duplicates - only those who have taken photos. We can add the DISTINCT keyword to the SELECT statement.

Update the SQL statement to only show distinct names.

Execute these command. When the new screen appears, capture it and place it in the word file that will contain all of your screen captures. Be sure to copy the SQL statement as well. Label this screen capture Prompt 12.


SELECT DISTINCT users.name 
FROM users 
JOIN photographs ON users.userid = photographs.userid;
