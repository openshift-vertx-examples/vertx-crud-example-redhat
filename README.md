https://appdev.openshift.io/docs/vertx-runtime.html#example-crud-vertx

## Running the application locally

To run the application locally, you need to start a local PostgreSQL instance. For example, you can use Docker as follows:

```bash
docker run --name some-postgres -e POSTGRES_USER=user -e POSTGRES_PASSWORD=password -e POSTGRES_DB=my_data -p 5432:5432 -d postgres
```

By default (for local development) the application uses:

* `localhost` as host
* `5432` as port
* `user` as username
* `password` as password
* `my_data` as database name

Then run the application using: `mvn compile vertx:run`. The application runs on: http://localhost:8080.

## Running the application on Openshift

To run the application on Openshift, you need to start a PostgreSQL instance. For example:

```bash
oc new-app -e POSTGRESQL_USER=luke -ePOSTGRESQL_PASSWORD=secret -ePOSTGRESQL_DATABASE=my_data registry.access.redhat.com/rhscl/postgresql-10-rhel7 --name=my-database
```

Wait and ensure the database pod is running, then:

```bash
mvn clean oc:deploy -Popenshift
```

## Integration tests

Run integrations test using:

```bash
mvn clean verify -Popenshift,openshift-it
```
