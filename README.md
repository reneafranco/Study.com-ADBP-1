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
    userid SERIAL PRIMARY KEY,
    name VARCHAR(255),
    username VARCHAR(20),
    address VARCHAR(255),
    city VARCHAR(255),
    state CHAR(2),
    zip INTEGER,
    CONSTRAINT unique_username UNIQUE (username)
);

CREATE TABLE locations (
    itemid SERIAL PRIMARY KEY,
    type INTEGER,
    description VARCHAR(255),
    lng REAL,
    lat REAL
);

CREATE TABLE photographs (
    photoid SERIAL PRIMARY KEY,
    locationid INTEGER
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
