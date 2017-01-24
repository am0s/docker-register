docker-register sets up a container running [docker-gen][1].  docker-gen dynamically generate a
python script when containers are started and stopped.  This generated script registers the running
containers host IP, port and domains in etcd with a TTL.  It works in tandem with haproxy-discover which
generates haproxy routes on the host to forward requests to registered containers.

### Usage

To run it:

    $ docker run -d -e HOST_IP=1.2.3.4 -e ETCD_HOST=1.2.3.4:4001 -v /var/run/docker.sock:/var/run/docker.sock -t am0s/docker-register

Then start any containers you want to be discoverable and publish their exposed port to the host.

    $ docker run -d -P -t ...

If you run the container on multiple hosts, they will be grouped together automatically.

### Acknowledgements

This code is based on [jwilder/docker-register](https://github.com/jwilder/docker-register) but heavily modified.

### License

MIT
