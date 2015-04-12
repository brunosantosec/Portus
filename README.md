Portus: a user interface for the [next generation of Docker registry](https://github.com/docker/distribution).

Portus targets [version 2](https://github.com/docker/distribution/blob/master/docs/spec/api.md)
of the Docker registry API. It aims to act both as
an authoritzation server and as a user interface for the next generation of the
Docker registry.

## Specs

Portus implements the [token based authentication system](https://github.com/docker/distribution/blob/master/docs/spec/auth/token.md)
described by the new ersion of the Docker registry.


## Development environment

This project contains a Vagrant based development environment which consists of
three nodes:

  * `registry.test.lan`: this is the node running the next generation of the
    Docker registry.
  * `portus`: this is the node running portus itself.
  * `client`: a node where latest version of Docker is installed

All the nodes are based on openSUSE 13.2 x86_64. VirtualBox is the chosen
provisioner.

### Intercepting all the traffic sent to the registry

On the client node execute:

```
docker run -ti --rm --add-host=registry.test.lan:192.168.1.2 -p 5000:5000 jess/mitmproxy -p 5000 -R http://registry.test.lan:5000
```

Now on the client node do:

```
docker tag busybox localhost:5000/busybox
docker push localhost:5000/busybox
```
