## Set postgresql on an external disk drive on MACOS

1. Open Disk Utility, select the external drive and use the option 'Erase'.

2. Select the format 'Mac OS Extended (Journaled)' because with 'exFAT' the initdb doesn't work(1).

3. Create a directory on your external hard drive where PostgreSQL will store its data.

    ```
    mkdir /Volumes/<external_drive_name>/pgsql_data
    ```

4. PostgreSQL needs to have ownership of the directory. Change the ownership of the directory:
    
    ```
    sudo chown -R $(whoami) /Volumes/<external_drive_name>/pgsql_data
    ```

5. Before making changes, stop the PostgreSQL service if it’s running:
    
    ```
    brew services stop postgresql@15
    ```

6. Initialize the new data directory on the external hard drive:
    
    ```
    initdb -D /Volumes/<external_drive_name>/pgsql_data 
    ```

7. If you have this error:

    ```
    initdb: error: invalid locale settings; check LANG and LC_* environment variables
    ```

    Add the following lines to the '.zshrc' file:
    
    ```
    export LANG=en_US.UTF-8
    export LC_ALL=en_US.UTF-8
    ```

    And then:

    ```
    source ~/.zshrc
    ```

8. Edit the PostgreSQL configuration to point to the new data directory. This can be done by modifying the PostgreSQL service script or directly starting PostgreSQL with the new data directory.

    To modify the service script, you may need to edit the Homebrew service file:

    ```
    nano /opt/homebrew/opt/postgresql@15/homebrew.mxcl.postgresql@15.plist 
    ```

    Look for the following section:
    
    ```
    <array>
		<string>/opt/homebrew/opt/postgresql@15/bin/postgres</string>
		<string>-D</string>
		<string>/opt/homebrew/var/postgresql@15</string>
	</array>
    ```

    and change the data directory path:

    ```
    <array>
		<string>/opt/homebrew/opt/postgresql@15/bin/postgres</string>
		<string>-D</string>
		<string>/Volumes/<external_drive_name>/pgsql_data</string>
	</array>
    ```

9. Start the PostgreSQL service again with the new configuration:

    ```
    brew services start postgresql@15
    ```

10. Create a database with your username:

    ```
    createdb <username>
    ```

11. Ensure that PostgreSQL is using the new data directory. You can do this by connecting to the PostgreSQL server and checking the data directory:

    ```
    psql -U <username> -c 'SHOW data_directory;'
    ```

    This should return the external drive directory:

    ```
    /Volumes/<external_drive_name>/pgsql_data 
    ```

(1) Error with initdb:

    ```
    % initdb -D pgsql_data
    The files belonging to this database system will be owned by user "claurelb".
    This user must also own the server process.

    The database cluster will be initialized with locale "en_US.UTF-8".
    The default database encoding has accordingly been set to "UTF8".
    The default text search configuration will be set to "english".

    Data page checksums are disabled.

    fixing permissions on existing directory pgsql_data ... ok
    creating subdirectories ... ok
    selecting dynamic shared memory implementation ... posix
    selecting default max_connections ... 100
    selecting default shared_buffers ... 128MB
    selecting default time zone ... America/Lima
    creating configuration files ... ok
    running bootstrap script ... 2024-05-20 19:40:47.443 -05 [97014] LOG:  could not link file "pg_wal/xlogtemp.97014" to "pg_wal/000000010000000000000001": Operation not supported
    2024-05-20 19:40:47.445 -05 [97014] FATAL:  could not open file "pg_wal/000000010000000000000001": No such file or directory
    child process exited with exit code 1
    initdb: removing contents of data directory "pgsql_data"
    ```