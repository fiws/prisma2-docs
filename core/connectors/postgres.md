# PostgreSQL data source connector

The PostgreSQL data source connector connects Prisma to a PostgreSQL database server.

## Example

To connect to a PostgreSQL database server, you need to configure a [`datasource`](../../prisma-project-file.md#data-sources) block in your [project file](../../prisma-project-file.md):

```groovy
datasource pg {
  provider = "postgres"
  url      = env(POSTGRES_URL)
}

// ... the file should also contain a data model definition and (optionally) generators
```

The fields passed to the `datasource` block are:

- `provider`: Specifies the `postgres` data source connector.
- `url`: Specifies the [connection string](#connection-string) for the PostgreSQL database server. In this case, we're [using an environment variable](../../prisma-project-file.md#using-environment-variables) to provide the connection string.

Find more information on the `datasource` fields [here](../../prisma-project-file.md#data-sources).

## Data model mapping

The PostgreSQL connector maps the [scalar types](../../data-modeling.md#scalar-types) from the [data model](../../data-modeling.md#scalar-types) as follows to native column types:

| Data model  | PostgreSQL  |
| -------- | --------- | 
| `String`   | `text`      | 
| `Boolean`  | `boolean`   |
| `Int`      | `integer`   |
| `Float`    | `real`      |
| `Datetime` | `timestamp` |

## Connection details

### Connection string

PostgreSQL offers also two styles of connection strings. See the [official documentation](https://www.postgresql.org/docs/current/libpq-connect.html#LIBPQ-CONNSTRING) for details.

- Key-value string: `host=localhost port=5432 dbname=mydb connect_timeout=10`
- Connection URI:
  ```
  postgresql://
  postgresql://localhost
  postgresql://localhost:5433
  postgresql://localhost/mydb
  postgresql://user@localhost
  postgresql://user:secret@localhost
  postgresql://other@localhost/otherdb?connect_timeout=10&application_name=myapp
  postgresql://host1:123,host2:456/somedb?target_session_attrs=any&application_name=myapp
  ```

The connection URI needs to follow the [official format](https://www.postgresql.org/docs/10/libpq-connect.html#id-1.7.3.8.3.6) for PostgreSQL connection strings:

```
postgresql://[user[:password]@][netloc][:port][,...][/dbname][?param1=value1&...]
```

### Configuration options

- **Host**: The IP address/domain of your database server, e.g. `localhost`.
- **Post**: The port on which your database server listens, e.g. `5432`.
- **Database**: The name of the database target schema. 
- **Schema**: The name of the target schema. 
- **User**: The database user, e.g. `admin`.
- **Password**: The password for the database user.
- **SSL**: Whether or not your database server uses SSL.
