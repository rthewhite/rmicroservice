# RMicroservice
This package aims to help you build "simple" microservices in Typescript.

The Connect team at Schuberg Philis is building microservices which use [Protobuf](https://github.com/google/protobuf) and [GRPC](https://grpc.io) as a basis and bolt REST on top of that for web usage. This package aims to use the proto as the basis for the service and make it simple to bolt REST on top of that.

It will help you setup health checks, do input validation etc. So that you can focus on implementing the actual business logic.

## Getting started
There is an example service in the [repo](https://github.com/rthewhite/rmicroservice/tree/master/example).

You can run this example using ts-node for example: 

``` ts-node service.ts ```

This will start a really simple service based on the [proto](https://github.com/rthewhite/rmicroservice/blob/master/example/proto/hello.proto) file. It will expose the HTTP server on the default 8000 port and the GRPC server on port 9000.

## Concepts
This package is working based on a couple of concepts:
- [service](https://github.com/rthewhite/rmicroservice/blob/master/docs/services.md) actual implementation of the GRPC services defined in the proto. The logic of mapping these to a REST endpoint is also contained in them.
- [managers](https://github.com/rthewhite/rmicroservice/blob/master/docs/managers.md) managers contain logic used by the services to accomplish their goal.
- [providers](https://github.com/rthewhite/rmicroservice/blob/master/docs/providers.md) providers provide an service mostly used by the managers to be able to do their job. Think of a database connections for example. Usually they register themselves with the [healthmanager](https://github.com/rthewhite/rmicroservice/blob/src/health.ts) to be incorporated into the service healthcheck


## Dependency injection
This framework relies heavily on dependency injection and uses [inversify](https://github.com/inversify/InversifyJS) for that. Whenever you need an dependency in your services or managers you should use the constructor to inject it.

You can see an example in the [helloservice](https://github.com/rthewhite/rmicroservice/blob/master/example/services/hello.ts) which gets the HelloManager injected. Notice the ```@injectable``` decorator on the [manager](https://github.com/rthewhite/rmicroservice/blob/master/example/managers/hellomanager.ts) don't forget this otherwise an error will be thrown.
