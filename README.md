# postgres
Bastille Template for PostgreSQL Jail

 STATUS:  Testing

Once this is installed you need to edit the config files.

	sudo vim /var/db/postgres/data11/postgresql.conf

Uncomment the listen_address and line and change to look like below.

	listen_addresses = '*'
	The wilcard * tells PostregreSQL service to listen on all 
	interfaces. But you can limit to specific IP address.

	listen_addresses = '192.168.1.20'


Then
	service postgresql restart

You can check that it is bound to all interfaces with the following command:

	sockstat -4 -6 | grep 5432

postgres user and group is created by default when you install PostgreSQL server. You’ll need to reset the password for this user to one you can remember.

	# passwd  postgres
	Changing local password for postgres
	New Password:
	Retype New Password:

You can also use

	$ su - postgres
	$ psql -c "alter user postgres with password 'StrongPassword'"
	ALTER ROLE

Test PostgreSQL 11 database functionality
Add a test database user:

	su - postgres
	createuser test_dbuser

	Grant created user an ownership to test_db:

	createdb test_db -O test_dbuser

Login to test_db database:

	# psql test_db
 	psql (11.1)
 	Type "help" for help
	test_db=#

Set user password:

	test_db=# alter user test_dbuser with password 'MyDBpassword';
	ALTER ROLE

Create a table and add some dummy data.

	test_db=# create table test_table ( id int,first_name text, last_name text ); 
	CREATE TABLE
	test_db=# insert into test_table (id,first_name,last_name) values (1,'John','Doe'); 
	INSERT 0 1
	Show table data

	test_db=#  select * from test_table;
	  id | first_name | last_name 
	 ----+------------+-----------
	   1 | John       | Doe
	 (1 row)
	Drop the test table

	test_db=# DROP TABLE test_table;
	DROP TABLE

Drop the test database

	$ dropdb test_db;

Should be ready to use now.
