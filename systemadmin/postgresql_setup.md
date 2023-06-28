# postgreSQL set up and usage notes

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

## Making a backup of the database
Can just do `pg_dump <DB_NAME> > backup.sql` , or can compress output: `pg_dump  <DB_NAME> --format=custom > backup.pgdump`

From https://mattsegal.dev/postgres-backup-and-restore.html, below is a script adapted to backup a database using .env file as input.
```
#!/bin/bash
# Backs up mydatabase to a file.
if [ $# -eq 0 ]
    then
        echo "No .env file provided. Usage: ./scripts/backup_database.sh <path_to_.env_file>"
        exit 1
fi

source $1 

mkdir -p ../database_backups

TIME=$(date "+%s")
BACKUP_FILE="database_backups/postgres_${DB_NAME}_${TIME}.pgdump"
echo "Backing up $DB_NAME to $BACKUP_FILE"
pg_dump $DB_NAME --format=custom > $BACKUP_FILE
echo "Backup completed"
```

## Restoring the database
TODO

## Reset the database
Irreversible: `python manage.py reset_db` then confirm yes. Requires `django-extensions` which should be installed and added to Django settings `INSTALLED_APPS`.

## Automating database backups
TODO: https://mattsegal.dev/postgres-backup-automate.html

## Sources
- Peer authentication error
    - https://stackoverflow.com/questions/18664074/getting-error-peer-authentication-failed-for-user-postgres-when-trying-to-ge
    - https://stackoverflow.com/questions/18664074/getting-error-peer-authentication-failed-for-user-postgres-when-trying-to-ge
- Getting permissions for Django to access database: https://stackoverflow.com/questions/38944551/steps-to-troubleshoot-django-db-utils-programmingerror-permission-denied-for-r
- Backing up postgres database: https://mattsegal.dev/postgres-backup-and-restore.html 
- Completely reset db: https://mattsegal.dev/reset-django-local-database.html 