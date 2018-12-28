# Vertica SQL to CSV

Outputs vertica query results as proper CSV.

Uses python's `csv` library to properly format CSV to one's liking. Outputs the result to stdout, can be piped to any other process.

Tries to mimic the command line arguments of `vsql`, but had to make some changes to keep it simple and versatile for csv.

## Installation
* Clone the repo and change to that directory
```bash
git clone https://github.com/kfzteile24/vertica-csv.git
cd vertica-csv
```
* Initialize the virtual environment (developed and tested on Python 3.7, but should work fine with Python 3.5 as well). Depending on the OS you might have to specify whether it's `-p python3` or `-p python3.6` or omit it entirely.
```bash
python -m vitualenv -p python3 .venv
.venv/bin/pip install -r requirements.txt
```


## Example usage

```bash
# Simplest command - execute on localhost with the current user and no password
./vsqlcsv db_name -c "SELECT * FROM public.sales LIMIT 10;"

# Remote connection, with user and password specification
./vsqlcsv --host 192.168.56.20 -U dbadmin -w letmein db_name --header -quoting all -c "SELECT * FROM public.sales LIMIT 10;"

# Piping command and sending output to file
cat query.sql | ./vsqlcsv --host 192.168.56.20 -U dbadmin db_name --header -quoting all > results.csv
```

You could also copy it to `/usr/local/bin/` and thus make it available regardless of `pwd`.
