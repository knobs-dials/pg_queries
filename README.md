# pg_queries

Shows 
- current queries
  - amount of query time (estimated, with a resolution relating our polling interval)
  - colored by query type
- amount of idle connections (and ignores their details, like the most recent query)
- recent queries (not based on idle state but on our own memory)


Some of these are things I'd like to see in pg_top, so even I only use this when pg_top isn't informative enough, 
e.g. when I want to see idle-in-transaction messiness, or the specific queries that dominate even when not indiviually crossing log_min_duration_statement.


Connects to user and database 'postgres' on localhost (defaults on most systems), and should work transparently when aliased like `sudo -u postgres pg_queries` or not.

If you want anything else, read up on pg_hba.conf   (`local all all trust`   will work -- but know its security implications!)

Not sure whether this can be cleverer, haven't studied it enough.


TODO:
- option parsing instead of hardcoded things
- make compatible with multiple postgres servers (the table it queries has seen changes over time)

  
