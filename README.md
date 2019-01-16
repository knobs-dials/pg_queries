# pg_queries

Shows current queries in postgresql server, amount of query time, colored by query type, and mentions amount of idle queries.


Which are basically the things I'd like to see in pg_top, so even I only use this
when pg_top isn't informative enough, e.g. when I want to see 
idle-in-transaction messiness, or the specific queries that dominate
even when not indiviually crossing log_min_duration_statement.



Connects to user and database 'postgres' on localhost.
This should work transparently when su'd to postgres.

If you want it on other users, edit your pg_hba.conf
(local all all trust   will work -- but know its security implications!)

Not sure whether this can be cleverer, haven't studied it enough.


TODO:
- option parsing instead of hardcoded things
- remember last query per PID, so we can get a better indication of *what* is causing idle in transaction


  