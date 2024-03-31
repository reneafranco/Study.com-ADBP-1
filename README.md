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
