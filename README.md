This repo demonstrates how to write an easily-tested JSON web service in
Go, with a PostgreSQL database. [It's a companion to a blog post I wrote](http://nerdyc.com/blog/2016/06/16/testing-web-apps-end-to-end-in-go/).

Tests in this project run against a local PostgreSQL server, and make
real HTTP calls to ensure that it works from end-to-end.

## Overview

Here's the gist of how tests work:

* The `test` sub-package contains shared test setup and helpers.

* The `test.Env` type manages setting up and tearing down global test state, like the connection to PostgreSQL.

* PostgreSQL is run locally (I use [Postgres.app](http://postgresapp.com)), and located via the `DATABASE_URL` environment variable.

* The [`migrate`](https://github.com/mattes/migrate) package is used to create a clean database before each test.

* The standard [`net/http/httptest`](https://golang.org/pkg/net/http/httptest/) package provides a test HTTP server that runs the API code.

* Test requests are made using standard HTTP.

Dive in and look at the tests, or [read the blog post for more detail](http://nerdyc.com/blog/2016/06/16/testing-web-apps-end-to-end-in-go/).
 
## Running the Tests

Tests are run via `go test`, just like any other Go project. However, the tests require a PostgreSQL database. The database URL is passed in via the `DATABASE_URL` environment variable, like this:

```bash
DATABASE_URL="postgres://username@localhost:5432/service_test?sslmode=disable" go test
```

## Contact Me!

I'd love to know if this helps you! I'm [@nerdyc](https://twitter.com/nerdyc) on Twitter.