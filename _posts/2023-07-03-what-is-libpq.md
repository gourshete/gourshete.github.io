---
layout: post
title:  "What is libpq?"
date:   2023-07-03
keywords: "ruby rails github learning ruby_on_rails postgres libpq activerecord"
image: assets/images/libpq.png
categories: [ Postgres]
---

You might have heard about libpq while installing/operating `postgresql`. But what is `libpq`? Let's understand.

<br>

<!--- Define -->

## What is libpq?
libpq is a library that helps app to communicate with postgresql backend server. It is C application programmer's interface. It helps in passing on queries and returning the result.


### Also
As per Postgresql docs -


libpq is also the underlying engine for several other PostgreSQL application interfaces, including those  written for C++, Perl, Python, Tcl and ECPG. So some aspects of libpq behavior will be important to you if you use one of those packages. In particular, Section 34.15, Section 34.16 and Section 34.19 describe behavior that is visible to the user of any application that uses libpq.


<!-- Layman words explaination, if possible -->

## When it is used?
If you have Postgresql on your setup, then libpq will be needed and used as underlying interface to communicate with Postgresql backend server.



### How to install libpq?
1. On Mac OS
```bash
brew install libpq
```

2. On Ubuntu
```bash
sudo apt-get install libpq-dev
```

<br>

### Issues if not installed
<img src="{{ '/assets/images/libpq-error.png' | prepend: site.baseurl }}" alt="libpq-error-image">

-> Installation of `libpq` should resolve this error. If you are still facing an issue, you might need to add libpq to path. Following is example for command terminal which uses zshrc.

```bash
echo 'export PATH="/usr/local/opt/libpq/bin:$PATH"' >> ~/.zshrc
```

<br>
<br>

### Code Example to connect and print hello world
Code example -

```c
#include <stdio.h>
#include <stdlib.h>
#include <libpq-fe.h>

static void
exit_nicely(PGconn *conn)
{
    PQfinish(conn);
    exit(1);
}

int
main(int argc, char **argv)
{
    const char *conninfo;
    PGconn     *conn;
    PGresult   *res;

    if (argc > 1)
        conninfo = argv[1];
    else
        conninfo = "dbname=postgres";

    /* Connect to the database */
    conn = PQconnectdb(conninfo);

    /* Verify success of database connection */
    if (PQstatus(conn) != CONNECTION_OK)
    {
        fprintf(stderr, "Connection to database failed: %s",
                PQerrorMessage(conn));
        exit_nicely(conn);
    }

    /* Execute a simple query and display the results */
    res = PQexec(conn, "SELECT 'Hello World'");
    printf("%s\n", PQgetvalue(res, 0, 0));

    PQclear(res);

    /* close the connection to the database and cleanup */
    PQfinish(conn);

    return 0;
}
```

---

<br>

  References - 
 
- [Postgresql libpq documentation](https://www.postgresql.org/docs/current/libpq.html)
- [Code reference](https://pgpedia.info/l/libpq.html)
