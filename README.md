PGMongo experimental driver
===========================

An experimental driver that makes a PostgreSQL database appear like a MongoDB database to its customers.



Usage
-----
		java -jar pgmongo.jar

1. Connect to PostgreSQL DB:

		connect -u [user name] -p [password] -url [url_to_db] -debug
			Options:
		-u			user name
		-p			password
		-url		url to db
		-debug		debug mod on
			
			
2. Write requests:

		db.[collection_name].[query_name]([query_json]);

3. ...

4. PROFIT!


Move data from mongoDB to PostgreSQL:
-------------------------------------

1. Export collections to json:

		mongoexport --db [db_name] --collection [collection_name] --out [name_output_file].json
 
 (In order to connect to a mongod that enforces authorization with the --auth option, 
 you must use the --username and --password options.)

2. Import json to PostgreSQL:

 		CREATE TABLE [table_name](json_data jsonb);
		\copy [table_name] FROM '[json_file_name]'
		VACUUM ANALYZE [table_name];

3. Create column '_id', make it primary key:

		alter table [table_name] add column _id text;
		update [table_name] set _id = json_data->[json_path_to_id]->'_id';
		alter table [table_name] add primary key (_id);    


