# Periodic Table Database

A clean-up and restructuring of an existing PostgreSQL database of chemical elements, plus a Bash script that looks up any element by atomic number, symbol or name. The script was developed in a Git repository using conventional commits.

## Tech used

PostgreSQL · SQL · Bash · Git

## Files

| File | Description |
|---|---|
| `element.sh` | Element lookup script |
| `periodic_table.sql` | Database dump of the cleaned-up database |

## Database clean-up

The starting database had several problems. I fixed them by:

- Renaming unclear columns (e.g. `weight` to `atomic_mass`)
- Adding `NOT NULL`, `UNIQUE` and foreign key constraints
- Normalising element types into a separate `types` table, linked by `type_id`
- Capitalising element symbols consistently
- Removing trailing zeros from atomic masses by converting the column to `DECIMAL`
- Deleting an invalid element record
- Adding two new elements (Fluorine and Neon)

## Example

```bash
./element.sh H
```
```
The element with atomic number 1 is Hydrogen (H). It's a nonmetal, with a mass of 1.008 amu. Hydrogen has a melting point of -259.1 celsius and a boiling point of -252.9 celsius.
```

The script also accepts `1` or `Hydrogen`, and handles missing or unknown input:

```bash
./element.sh
# Please provide an element as an argument.

./element.sh xyz
# I could not find that element in the database.
```

## How to run it

```bash
psql -U postgres < periodic_table.sql
./element.sh Neon
```

## What I learned

- Fixing and restructuring an existing database with `ALTER TABLE`
- Normalising data into a separate lookup table
- Cleaning inconsistent data with SQL string functions
- Joining three tables in one query
- Using Git with conventional commit messages (`feat:`, `fix:` and so on)
