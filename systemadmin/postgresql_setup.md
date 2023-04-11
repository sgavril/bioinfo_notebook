# postgreSQL set up notes

## Accessing psql terminal
Access as the default postgres user using: 
`psql -U postgres`  

If doing this gives an error: FATAL: Peer authentication failed for user "postgres" then edit the `pg_hba.conf` typically located at `/etc/postgresql/[version]/main/pg_hba.conf` or `/var/lib/pgsql/data/pg_hba.conf` . 

Change the following line from: 

`local   all             postgres                                peer`

to:

`local   all             postgres                                md5`

and restart the service:
`sudo systemctl restart postgresql`.



## Creating a database with sufficient privileges 
First create a database using `CREATE DATABASE <db_name>;`

Then for that database run the following:

`GRANT ALL PRIVILEGES ON DATABASE <db_name> TO <username>;`

`GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO <username>;`

`ALTER DATABASE <db_name> OWNER TO <username>; `


## Sources
- Peer authentication error
    - https://stackoverflow.com/questions/18664074/getting-error-peer-authentication-failed-for-user-postgres-when-trying-to-ge
    - https://stackoverflow.com/questions/18664074/getting-error-peer-authentication-failed-for-user-postgres-when-trying-to-ge
- Getting permissions for Django to access database: https://stackoverflow.com/questions/38944551/steps-to-troubleshoot-django-db-utils-programmingerror-permission-denied-for-r