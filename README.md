# pg_queries

Shows 
- amount of active, idle, idle in transaction, and max connections
- current active queries 
  - amount of query time (estimated, with a resolution relating our polling interval)
  - colored by query type
- recent queries (based on our on memory, not idle state in an unused worker)


Can filter out things that are done very quickly - because it's aimed at finding clients that could use a little work - more efficient queries, less idle in transaction, that kind of thing.

Some of these are things I'd like to see in pg_top, or are just a little easier than setting log_min_duration_statement and checking logs.


# connecting

Connects to user and database 'postgres' on localhost (defaults on most systems), and should work transparently when aliased like `sudo -u postgres pg_queries` or not.

If you want anything else, read up on pg_hba.conf   (`local all all trust`   will work -- but know its security implications!)

Not sure whether this can be cleverer, haven't studied it enough.


# TODO
- make compatible with multiple postgres servers (the table it queries has seen changes over time)

  
