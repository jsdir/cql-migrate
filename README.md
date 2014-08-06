cql-migrate
===========

Derives deltas and migrates between output schemas from datastored's cassandra adapter

Installation
------------

`npm install -g cql-migrate`

Usage
-----

### Saving migrations

To save a new migration, pipe in the new schema to `cql-migrate add`.

```sh
$ # Use an automatic script.
$ node ./generate_schema.js | cql-migrate add -n "first migration"
$ # Or use a file.
$ cql-migrate | schema.json
```

If the nme parameter `-n` is not given, you will be prompted for the migration name.

Migrations will be saved in the same naming format used by [ActiveRecord](http://guides.rubyonrails.org/migrations.html):

`YYYYMMDDHHMMSS_migration_name.json`

The migration name will have spaces replaced with underscores, and the entire name will be made lowercase. 

### Applying migrations

To migrate to the latest unapplied migration, just run the command by itself:

```sh
$ cql-migrate
```

To migrate to a specific migration, give the schema filename:

```sh
$ cql-migrate 20000101010101_happy_new_year.json
```

A state file is saved in the migration state directory. This will let future migrations know the state of the database and will determine what delta to apply. Since the schema of the latest migration is also saved as state, migrations can be reversed without having to find the last migration. It will already be available in state.
