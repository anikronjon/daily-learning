## build
build can be specified either as a string containing a path to the build context:
```yml
version: "3.9"
services:
  webapp:
    build: ./dir
```
Or, as an object with the path specified under context and optionally Dockerfile and args
```yml
version: "3.9"
services:
  webapp:
    build:
      context: ./dir
      dockerfile: Dockerfile-alternate
      args:
        buildno: 1
```

### context
The value of context will be either a path of a directory containing a Dockerfile, or a url of a git repository 
```yml
build:
  context: ./dir
```

### dockerfile
Alternate Dockerfile
```yml
build:
  context: .
  dockerfile: Dockerfile-alternate
```

## container_name
Specify a custom container name, rather than a generated default name.

Note: 
- Docker container names must be unique,
- You cannot scale a service beyond 1 container if you have specified a custom name. 
- Attempting to do so results in an error.
```yml
build: ./dir
container_name: my-web-container

```

## command
Override the default command.
```yml
build: ./dir
container_name: my-web-container
command: bundle exec thin -p 3000
```
or
```yml
build: ./dir
container_name: my-web-container
command: ["bundle", "exec", "thin", "-p", "3000"]
```

## depends_on
Express dependency between services. Service dependencies cause the following behaviors:

- docker-compose up starts services in dependency order. In the following example, db and redis are started before web.
- docker-compose up SERVICE automatically includes SERVICE’s dependencies. In the example below, docker-compose up web also creates and starts db and redis.
- docker-compose stop stops services in dependency order. In the following example, web is stopped before db and redis.
```yml
version: "3.9"
services:
  web:
    build: .
    depends_on:
      - db
      - redis
  redis:
    image: redis
  db:
    image: postgres
```

## ports
```yml
ports:
  - "3000"
  - "3000-3005"
  - "8000:8000"
  - "9090-9091:8080-8081"
  - "49100:22"
  - "127.0.0.1:8001:8001"
  - "127.0.0.1:5000-5010:5000-5010"
  - "127.0.0.1::5000"
  - "6060:6060/udp"
  - "12400-12500:1240"
```

## volumes [..]([volumes](https://docs.docker.com/compose/compose-file/compose-file-v3/#volumes)
```yml
version: "3.9"
services:
  web:
    image: nginx:alpine
    volumes:
      - type: volume
        source: mydata
        target: /data
        volume:
          nocopy: true
      - type: bind
        source: ./static
        target: /opt/app/static

  db:
    image: postgres:latest
    volumes:
      - "/var/run/postgres/postgres.sock:/var/run/postgres/postgres.sock"
      - "dbdata:/var/lib/postgresql/data"

volumes:
  mydata:
  dbdata:
```
