# emptyhammock-role-database

This is an Ansible role that, in conjunction with a number of other Emptyhammock
roles, handles provisioning and deployment of Django applications.

It is oriented closely to Emptyhammock projects, but you may find some useful
snippets here.

## Configuration

### Required Ansible variables

* Set `pg_user` to the database user name.
* Set `DB_PASSWORD` to the database password.
* Set `project_db` to the name of the project database.

### Optional Ansible variables

* `database_encoding` (default `UTF-8`)
* `database_lc_collate` (default `en_US.UTF-8`)
* `database_lc_ctype` (default `en_US.UTF-8`)
* `database_template`: (default `template0`)

### Manual configuration

The default PostgreSQL user setup has proved sufficient for Django applications
using PostgreSQL versions up through 14.

With PostgreSQL 16 (15 wasn't tested), additional manual configuration was
required to allow the database user to create tables (for running Django
migrations) and access tables and sequences at runtime.

Rough notes:

```
Run `psql` as the Ubuntu `postgres` user.
Connect to the target database:  \c my_database
GRANT ALL ON SCHEMA public TO my_database_user;
GRANT ALL PRIVILEGES ON DATABASE my_database TO my_database_user;
```