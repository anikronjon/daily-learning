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
