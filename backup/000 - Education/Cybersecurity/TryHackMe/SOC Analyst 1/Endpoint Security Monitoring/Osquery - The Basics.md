# Osquery: Interactive Mode

One of the ways to interact with Osquery is by using the interactive mode. Open the terminal and run `osqueryi`. To understand the tool, run the `.help` command in the interactive terminal, as shown below:

```Powershell
root@analyst$ osqueryi
Using a virtual database. Need help, type '.help'
osquery> .help
Welcome to the osquery shell. Please explore your OS!
You are connected to a transient 'in-memory' virtual database.

.all [TABLE]     Select all from a table
.bail ON|OFF     Stop after hitting an error
.connect PATH    Connect to an osquery extension socket
.disconnect      Disconnect from a connected extension socket
.echo ON|OFF     Turn command echo on or off
.exit            Exit this program
.features        List osquery's features and their statuses
.headers ON|OFF  Turn display of headers on or off
.help            Show this message
.mode MODE       Set output mode where MODE is one of:
                   csv      Comma-separated values
                   column   Left-aligned columns see .width
                   line     One value per line
                   list     Values delimited by .separator string
                   pretty   Pretty printed SQL results (default)
.nullvalue STR   Use STRING in place of NULL values
.print STR...    Print literal STRING
.quit            Exit this program
.schema [TABLE]  Show the CREATE statements
.separator STR   Change separator used by output mode
.socket          Show the local osquery extensions socket path
.show            Show the current values for various settings
.summary         Alias for the show meta command
.tables [TABLE]  List names of tables
.types [SQL]     Show result of getQueryColumns for the given query
.width [NUM1]+   Set column widths for "column" mode
.timer ON|OFF      Turn the CPU timer measurement on or off
```

> [!NOTE] 
> As per documentation, meta=commands are prefixed with a `.`

## List the Tables

To list all the tables that can be queried, use the `.tables` meta-command.

For example, if you wish to check what tables are associated with processes, you can use `.tables process`.

```Powershell
root@analyst$ osqueryi 
Using a virtual database. Need help, type '.help' 
osquery> .table  
=> appcompat_shims   
	=> arp_cache   
	=> atom_packages   
	=> authenticode   
	=> autoexec   
	=> azure_instance_metadata   
	=> azure_instance_tags   
	=> background_activities_moderator   
	=> bitlocker_info
	=> carbon_black_info   
	=> carves   
	=> certificates   
	=> chassis_info   
	=> chocolatey_packages`
```

To list all the tables with the term `user` in them, we will use the `.tables user` as shown below:

```powershell
root@analyst$ osqueryi 
Using a virtual database. Need help, type '.help' 
osquery> .table user   
	=> user_groups   
	=> user_ssh_keys   
	=> userassist   
	=> users`
```

> In the above example, four tables are returned that contain the word `user`. 

## Understanding the Table Schema

Table names are not enough to know what information it contains without actually querying it. Knowledge of columns and types (known as **schema**) for each table is also helpful. 

We can list a table's schema with the following meta-command: `.schema table_name`

Here, we are interested in understanding the columns in the user's table.

```powershell
root@analyst$ osqueryi
Using a virtual database. Need help, type '.help'
osquery> .schema users
CREATE TABLE users(`uid` BIGINT, `gid` BIGINT, `uid_signed` BIGINT, `gid_signed` BIGINT, `username` TEXT, `description` TEXT, `directory` TEXT, `shell` TEXT, `uuid` TEXT, `type` TEXT, `is_hidden` INTEGER HIDDEN, `pid_with_namespace` INTEGER HIDDEN, PRIMARY KEY (`uid`, `username`, `uuid`, `pid_with_namespace`)) WITHOUT ROWID;
```

> The above result provides the column names like username, description, PID followed by the respective datatypes like BIGINT, TEXT, INTEGER, etc. Let's pick a few columns from this schema and use SQL query to ask osquery to display the columns from the user table using the following syntax:

**SQL Query Syntax**: `select column1, column2, column3 from table;`

```
root@analyst$ osqueryi
Using a virtual database. Need help, type '.help'
osquery>select gid, uid, description, username, directory from users;
+-----+------+------------------------------------------------------------+----------------------+-------------------------------------------+
| gid | uid  | description                                                | username           | directory                                   |
+-----+------+-------------------------------------------------------------------------------------------------------------------------------+
| 544 | 500  | Built-in account for administering the computer/domain     | Administrator      |                                             |
| 581 | 503  | A user account managed by the system.                      | DefaultAccount     |                                             |
| 546 | 501  | Built-in account for guest access to the computer/domain   | Guest              |                                             |
| 544 | 1002 |                                                            | James              | C:\Users\James                              |
| 18  | 18   |                                                            | SYSTEM             | %systemroot%\system32\config\systemprofile  |
| 19  | 19   |                                                            | LOCAL SERVICE      | %systemroot%\ServiceProfiles\LocalService   |
| 20  | 20   |                                                            | NETWORK SERVICE    | %systemroot%\ServiceProfiles\NetworkService |
+-----+------+------------------------------------------------------------+--------------------+---------------------------------------------+
```

## Display Mode

Osquery comes with multiple display modes to select from. Use the `.help` option to list the available modes or choose 1 of them as shown below.

```
root@analyst$ osqueryi 
Using a virtual database. Need help, type '.help' 
osquery>.help Welcome to the osquery shell. Please explore your OS! You are connected to a transient 'in-memory' virtual database. 
. 
. 
. 
.mode MODE       Set output mode where MODE is one of:                    
	csv      Comma-separated values                    
	column   Left-aligned columns see .width                    
	line     One value per line                    
	list     Values delimited by .separator string                    
	pretty   Pretty printed SQL results (default) . . .`
```

# Schema Documentation

For this task, go to the schema [documentation](https://osquery.io/schema/5.5.1/) of Osquery version 5.5.1, the latest version. The schema documentation looks like the image shown below:

![](https://i.imgur.com/zkud8rn.png)

## Breakdown

Let's breakdown the important information we could find in this schema documentation:

1. A dropdown lists various versions of osquery. Choose the version you wish to see table schemas for. 
2. The number of tables within the selected version of Osquery. (In the above image, 106 tables are available).
3. The list of tables is listed in alphabetical order for the selected version of osquery. This is the same result we got when we used the `.table` command in the interactive mode. 
4. The name of the table and a brief description. 
5. A detailed chart showing each table's **column**, **type**, and **description**.
6. Information to which Operating System table applies. (In the above image, the **account_policy_data** table is available only for **macOS**)
7. A dropdown menu to select the operating system of choice. We can choose multiple OS, which will display the tables available for those OS.

# Creating SQL Queries

The SQL language implemented by Osquery is not an entire SQL language that you might be accustomed to, but rather it's a superset of **SQLite**. 

Realistically all your queries will start with a **SELECT** statement. This makes sense because, with Osquery, you are only querying information on an endpoint. You won't be updating or deleting any information/data on the endpoint.

**The exception to the rule**: Using other SQL statements, such as **UPDATE** and **DELETE**, is possible, but only if you're creating run-time tables (views) or using an extension if the extension supports them. 

Your queries will also include a **FROM** statement and end with a **semicolon**.

## Exploring Installed Programs

IF you wish to retrieve all the information about the installed programs on the endpoint, first understand the table schema either using the `.schema programs` command in the interactive mode or use the documentation [here](https://osquery.io/schema/5.5.1/#programs).

**Query**: `SELECT * FROM programs LIMIT 1;`

```powershell
root@analyst$ osqueryi 
Using a virtual database. Need help, type '.help' 
osquery>select * from programs limit 1;               
			name = 7-Zip 21.07 (x64)            
			version = 21.07   
			install_location = C:\Program Files\7-Zip\     
			install_source =           
			language =          
			publisher = Igor Pavlov   
			uninstall_string = "C:\Program Files\7-Zip\Uninstall.exe"       
			install_date = 
			identifying_number =`
```

> In the above example `LIMIT` was used followed by the number to limit the results to display.

> [!NOTE]
> **Note**: Your results will be different if you run this query in the attached VM or your local machine (if Osquery is installed). Here line mode is used to display the result.

The number of columns returned might be more than what we need. You can select specific columns rather than retrieve every column from the table.

**Query**: `SELECT name, version, install_location, install_date from programs limit 1;`

```
root@analyst$ osqueryi 
Using a virtual database. Need help, type '.help' 
osquery>select name, version, install_location, install_date from programs limit 1;             name = 7-Zip 21.07 (x64)          
		   version = 21.07 install_location = C:\Program Files\7-Zip\     
           install_date =`
```

The above query will list the name, version, install location, and installed date of the programs on the endpoint. This will still return many results, depending on how busy the endpoint is. 

## Count

> To see how many programs or entries in any table are returned, we can use the `count()` function as shown below:

**Query**: `SELECT count(*) from programs;`

```shell
root@analyst$ osqueryi Using a virtual database. Need help, type '.help' osquery>select count(*) from programs; 
count(*) = 160`
```

## WHERE Clause

> Optionally, you can use a `WHERE` clause to narrow down the list of results returned based on specified criteria. The following query will first get the user table and only display the result of the user James, as shown below:

**Query**: `SELECT * FROM users WHERE username='James';`

```powershell
root@analyst$ osqueryi Using a virtual database. Need help, type '.help' osquery>SELECT * FROM users WHERE username='James';         
uid = 1002         
gid = 544  
uid_signed = 1002  
gid_signed = 544    
username = James 
description =   
directory = C:\Users\James       
shell = C:\Windows\system32\cmd.exe        
uuid = S-1-5-21-605937711-2036809076-574958819-1002        
type = local`
```

The equal sign is not the only filtering option in a **WHERE** clause. Below are filtering operators that can be used in a **WHERE** clause:

- `=` [equal]
- `<>`  [not equal]
- `>`, `>=` [greater than, greater than, or equal to]
- `<`, `<=` [less than or less than or equal to] 
- `BETWEEN` [between a range]
- `LIKE` [pattern wildcard searches]
- `%` [wildcard, multiple characters]
- `_` [wildcard, one character]

## Matching Wildcard Rules

Below is a screenshot from the Osquery [documentation](https://osquery.readthedocs.io/en/stable/deployment/file-integrity-monitoring/) showing examples of using wildcards when used in folder structures:  

- `%`: Match all files and folders for one level.
- `%%`: Match all files and folders recursively.
- `%abc`: Match all within-level ending in "abc".
- `abc%`: Match all within-level starting with "abc".

## Matching Examples

- - `/Users/%/Library`: Monitor for changes to every user's Library folder, _but not the contents within_.
- `/Users/%/Library/`: Monitor for changes to files _within_ each Library folder, but not the contents of their subdirectories.
- `/Users/%/Library/%`: Same, changes to files within each Library folder.
- `/Users/%/Library/%%`: Monitor changes recursively within each Library.
- `/bin/%sh`: Monitor the `bin` directory for changes ending in `sh`.

> Some tables _require_ a **WHERE** clause, such as the **file** table, to return a value. If the required **WHERE** clause is not included in the query, then you will get an error.

```powershell
root@analyst$ osqueryi Using a virtual database. Need help, type '.help' osquery>select * from file; 
W1017 12:38:29.730041 45744 virtual_table.cpp:965] Table file was queried without a required column in the WHERE clause 
W1017 12:38:29.730041 45744 virtual_table.cpp:976] Please see the table documentation: https://osquery.io/schema/#file 
Error: constraint failed`
```

## Joining Tables using JOIN Function  

OSquery can also be used to join two tables based on a column that is shared by both tables. Let's look at two tables to demonstrate this further. Below is the schema for the **user's** table and the **processes** table.

```powershell
root@analyst$ osqueryi
Using a virtual database. Need help, type '.help'
osquery>.schema users
CREATE TABLE users(`uid` BIGINT, `gid` BIGINT, `uid_signed` BIGINT, `gid_signed` BIGINT, `username` TEXT, `description` TEXT, `directory` TEXT, `shell` TEXT, `uuid` TEXT, `type` TEXT, `is_hidden` INTEGER HIDDEN, `pid_with_namespace` INTEGER HIDDEN, PRIMARY KEY (`uid`, `username`, `uuid`, `pid_with_namespace`)) WITHOUT ROWID;

osquery>.schema processes
CREATE TABLE processes(`pid` BIGINT, `name` TEXT, `path` TEXT, `cmdline` TEXT, `state` TEXT, `cwd` TEXT, `root` TEXT, `uid` BIGINT, `gid` BIGINT, `euid` BIGINT, `egid` BIGINT, `suid` BIGINT, `sgid` BIGINT, `on_disk` INTEGER, `wired_size` BIGINT, `resident_size` BIGINT, `total_size` BIGINT, `user_time` BIGINT, `system_time` BIGINT, `disk_bytes_read` BIGINT, `disk_bytes_written` BIGINT, `start_time` BIGINT, `parent` BIGINT, `pgroup` BIGINT, `threads` INTEGER, `nice` INTEGER, `elevated_token` INTEGER, `secure_process` INTEGER, `protection_type` TEXT, `virtual_process` INTEGER, `elapsed_time` BIGINT, `handle_count` BIGINT, `percent_processor_time` BIGINT, `upid` BIGINT HIDDEN, `uppid` BIGINT HIDDEN, `cpu_type` INTEGER HIDDEN, `cpu_subtype` INTEGER HIDDEN, `translated` INTEGER HIDDEN, `cgroup_path` TEXT HIDDEN, `phys_footprint` BIGINT HIDDEN, PRIMARY KEY (`pid`)) WITHOUT ROWID;
```

Looking at both schemas, `uid` in `users` table is meant to identify the user record, and in the processes table, the column `uid` represents the user responsible for executing the particular process. We can join both tables using this `uid` field as shown below:

**Query1:** `select uid, pid, name, path from processes;`

**Query2:** `select uid, username, description from users;`

**Joined Query:** `select p.pid, p.name, p.path, u.username from processes p JOIN users u on u.uid=p.uid LIMIT 10;`

```Powershell
root@analyst$ osqueryi
Using a virtual database. Need help, type '.help'
osquery>select p.pid, p.name, p.path, u.username from processes p JOIN users u on u.uid=p.uid LIMIT 10;
+-------+-------------------+---------------------------------------+----------+
| pid   | name              | path                                  | username |
+-------+-------------------+---------------------------------------+----------+
| 7560  | sihost.exe        | C:\Windows\System32\sihost.exe        | James    |
| 6984  | svchost.exe       | C:\Windows\System32\svchost.exe       | James    |
| 7100  | svchost.exe       | C:\Windows\System32\svchost.exe       | James    |
| 7144  | svchost.exe       | C:\Windows\System32\svchost.exe       | James    |
| 8636  | ctfmon.exe        | C:\Windows\System32\ctfmon.exe        | James    |
| 8712  | taskhostw.exe     | C:\Windows\System32\taskhostw.exe     | James    |
| 9260  | svchost.exe       | C:\Windows\System32\svchost.exe       | James    |
| 10168 | RuntimeBroker.exe | C:\Windows\System32\RuntimeBroker.exe | James    |
| 10232 | RuntimeBroker.exe | C:\Windows\System32\RuntimeBroker.exe | James    |
| 8924  | svchost.exe       | C:\Windows\System32\svchost.exe       | James    |
+-------+-------------------+---------------------------------------+----------+
```

Note: Please refer to the Osquery [documentation](https://osquery.readthedocs.io/en/stable/introduction/sql/) for more information regarding SQL and creating queries specific to Osquery.

