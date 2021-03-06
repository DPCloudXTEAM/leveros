![Lever OS](https://raw.githubusercontent.com/leveros/leveros/master/doc/images/leveros-logo-full-white-bg-v0.2.png "Lever OS")
============================================================================

leveros - Node client library for Lever OS
==========================================

The `leveros` Node client library can be used to invoke Lever methods either from within a Lever service or from outside Lever altogether.

[![ReadMe.io](https://img.shields.io/badge/ReadMe.io-docs-blue.svg)](https://leveros.readme.io/) [![npm version](https://badge.fury.io/js/leveros.svg)](https://badge.fury.io/js/leveros) [![Join the chat at https://gitter.im/leveros/leveros](https://badges.gitter.im/leveros/leveros.svg)](https://gitter.im/leveros/leveros?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge) [![License](https://img.shields.io/badge/license-Apache--2.0-blue.svg)](http://www.apache.org/licenses/LICENSE-2.0) [![Analytics](https://ga-beacon.appspot.com/UA-77293003-2/github.com/leveros/leveros/js/leveros?pixel)](https://github.com/igrigorik/ga-beacon)

Documentation
-------------

See [ReadMe.io](https://leveros.readme.io/docs/node-client-api).

Installation
------------

Installation for use outside Lever

```bash
$ npm install leveros
```

Installation for use within Lever

```bash
$ docker run --rm -it --user=root -v "$PWD":/leveros/custcode leveros/levercontainer:latest npm install leveros
```

The installation procedure is special for Lever because the library depends on `grpc` which contains C++ extensions for node. These need to be compiled on the OS it will run on. As Lever containers are Docker containers (namely containers based on the `ubuntu` image), the above command installs the library while running in the same container it will run on Lever.

To use the library, simply

```javascript
require('leveros');
```

Quick example
-------------

```javascript
var leveros = require('leveros');

var client = new leveros.Client();
client.forceHost = process.env.LEVEROS_IP_PORT;
var service = client.service('dev.lever', 'helloService');
service.invoke('sayHello', "world", function (error, reply) {
    console.log(reply);
});
```

```bash
# Without docker-machine
$ LEVEROS_IP_PORT="127.0.0.1:8080" node client.js

# With docher-machine
$ LEVEROS_IP_PORT="$(docker-machine ip default):8080" node client.js
```

Setting `LEVEROS_IP_PORT` is necessary so that you can invoke the `dev.lever` environment without adding an entry for it in `/etc/hosts` and setting the listen port to `80`.
