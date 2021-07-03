# pg_queries
![screenshot](https://raw.githubusercontent.com/scarfboy/pg_queries/master/screenshot.png "screenshot")

Show current and recent postgresql queries, in a linux shell, based on pg_stat_activity table.

Yes, much like pg_top, but aimed more at finding clients that could use a little work, in that it shows:
- most recent query for idle-in-transaction connections
- current active queries 
  - amount of query time (estimated, with a resolution related to our polling interval)
  - colored by query type
  - (experiment:) what each is waiting on, like locks or WAL (I'm still working on how to present wait_event, wait_event_type)
- recent queries (based on us having seen them, not on idle state in an unused workers) so they don't disappear in a flash
- amount of active, idle, idle in transaction, and max connections

Can filter out things that are done quickly 


# arguments

```
Usage: pg_queries [options]

Options:
  -h, --help            show this help message and exit
  -i POLLINTERVAL, --poll-interval=POLLINTERVAL
                        Poll interval, in seconds. Defaults to 0.4 so you have
                        some chance to read.
  -t SHORTTHRESH, --worktime-threshold=SHORTTHRESH
                        Show only active/recent queries that took at least
                        this many seconds. Higher will show only slower
                        queries. Lower, like 0, shows most (but not all,
                        because we're polling). Defaults to 0.05.
  -f FORGETTIME, --forget-time=FORGETTIME
                        Forget recent queries after this many seconds.
                        Defaults to 30
  -r MAXRECENT, --max-recent=MAXRECENT
                        Show at most this-many recent queries, e.g. to help
                        avoid scrolling off the active ones. Defaults to 3.
  -A, --as-is-query     Default is to truncate to at most a line. This instead
                        leaves the query formatted as reported to us
  -R, --reformat-query  Default is to truncate to at most a line. This instead
                        inserts newlines on the major parts (SELECT, FROM, 
                        WHERE, and such)
  -T, --no-truncate-query
                        Put as much of the query that fits on a single line,
                        truncate the rest, so that we have some hope of
                        showing all on a screen. Currently the default.
  -I, --dont-ignore-boring
                        By default we ignore things like COMMIT, BEGIN, and
                        ROLLBACK. This shows them.
```

# connecting

Connects to user and database 'postgres' on localhost (defaults on most systems), and should work transparently when aliased like `sudo -u postgres pg_queries` if not.

If you want anything else, read up on pg_hba.conf   (`local all all trust`   will often work -- but can be too permissive, so know its security implications!)

Not sure whether this can be cleverer, haven't studied it enough.


# TODO
- check a lot of counting logic, for correctness and whether it does what I want
- make compatible with multiple postgres servers (the table it queries has seen changes over time, current code is since 10ish?)

  
