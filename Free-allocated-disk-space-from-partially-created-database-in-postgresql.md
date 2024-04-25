## Free allocated disk space from partially created database in postgresql

This happened when I run out of disk space when creating a new database with the command ```CREATE DATABASE newdb WITH TEMPLATE db;```.

1. To find the directory where the tables data is stored, run the following command in psql:
    
    ```
    SHOW DATA_DIRECTORY;
    ```
   
   I got the following output:

    ```
            data_directory          
    ---------------------------------
     /opt/homebrew/var/postgresql@15
    ```

2. In a terminal, go to the directory with the following command:
    
    ```
    cd /opt/homebrew/var/postgresql@15/base
    ```

    If you check the content of that folder, you will find something like this:

    ```
    % ls
    1		    15027527	18364955	18449535	4		pgsql_tmp
    12045865	16388		18370020	18460132	5
    ```

3. To find what folders belong to the existing databases, run in psql the following command:
   
    ```
    user=# SELECT oid, datname FROM pg_database;
        oid    |              datname              
     ----------+-----------------------------------
             5 | postgres
         16388 | user
             1 | template1
             4 | template0
      12045865 | db1
      15027527 | db2
      18370020 | db3
      18449535 | db4
    ```

4. Delete the folders whose name is not in the result from the previous step, excluding the ```pgsql_tmp``` folder

   In the example shown, the folders to delete would be 18364955 and 18460132.

   You can use the command ```du -sh folder_name``` to find the size of the folder.