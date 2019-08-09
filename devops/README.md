#
## The Issue of Development/Debugging:

During the development phase the developer accesses the dependent components locally which is easily achievable by `docker`. However, few issues which are discovered in the `hosted system` do not repoduced on local stack. For debugging such an issue, the components that needs debugging are executed locally and rest on the `hosted system`.

## Approach

The idea is to device a methodology to easily setup the stack to execute selected components locally and rest on the `hosted system`. The dev will follow below steps:

* __Use `GNU Make`__
```bash
# select your components
$ HOST_SYS=http://myhost.com/ ./configure --with-ui-dev

# build docker containers
$ make build

# bring containers up
$ make up
```

* __How Stack is Setup__

The the components to be debugged runs locally along with an `nginx` in a `docker` container which works as a `reverse proxy`.
      
```text
                                                         +------------+
                                                         |  HOST_SYS  |
                                                         |            |
                                                +------> |    api     |
                                                |        |            |
                                                |        |  database  |
                                            +---+----+   |            |
                                            | DOCKER |   |    auth    |
 developer --> http://localhost:1234/ui --> |        |   +------------+
                                            | nginx  |
                                            +---+----+
                                                |        +------------+
                                                |        |   DOCKER   |
                                                +------> |            |
                                                         |     ui     |
                                                         +------------+
```

We can make use of parameterized `docker-compose.yml` & `dockerfile` to wireup the dependencies

Each component should have a `dev` & `deploy` version of the `dockerfile`
- component_dev.docker-composer.build.yml
- component_dev.docker-composer.up.yml
- component_dev.dockerfile.yml
