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



