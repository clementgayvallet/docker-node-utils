# docker-node-utils
This repository contains a set of docker based on node. I use these dockers to limit `npm install` and always know what I really have.

## Supported tags and respective `Dockerfile` links

* `latest` [(Dockerfile)](https://github.com/Joxit/docker-node-utils/blob/master/Dockerfile)
* `carto` [(carto/Dockerfile)](https://github.com/Joxit/docker-node-utils/blob/master/carto/Dockerfile)

## Usage

There are some shortcuts you can use thanks to your bashrc or bash_aliases.

- Your source code should be in the current directory tree. 
- You can configure your own user ID with `USER` variable (this is to avoid all new files created by docker are owned by root).
- You can add more options to your docker with the `NODE_OPTS` variable

```sh
# This will let you use node repl or start a node program.
alias node="docker run -ti --rm -e USER=1000 -v $(pwd):/usr/src/app ${NODE_OPTS} joxit/node node"
# This will let you use npm install etc (-g option will not work as you want).
alias npm="docker run -ti --rm -e USER=1000 -v $(pwd):/usr/src/app ${NODE_OPTS} joxit/node npm"
# This will let you use more than one command at the time.
alias node_bash="docker run -ti --rm -e USER=1000 -v $(pwd):/usr/src/app ${NODE_OPTS} joxit/node bash"

# Use cartoCSS utilities 
alias carto="docker run -ti --rm -e USER=1000 -v $(pwd):/usr/src/app ${NODE_OPTS} joxit/node:carto carto"
alias cartocc="docker run -ti --rm -e USER=1000 -v $(pwd):/usr/src/app ${NODE_OPTS} joxit/node:carto cartoymlcc"
```

## Example

```sh
# This will save node_modules in my directory with my source code and node_modules will be owned by root
NODE_OPTS="-e USER=0" npm install
# I use NODE_OPTS var to add new options to the docker (such as port for a server).
NODE_OPTS="-p 3000:3000" node server/index.js
```

## carto

Carto is a fast CSS-like map stylesheets https://github.com/mapbox/carto/blob/master/docs/latest.md

This docker contains [carto](https://github.com/mapbox/carto), [cartocc](https://github.com/yohanboniface/CartoCC) and [cartoymlcc](https://github.com/Joxit/docker-node-utils/blob/master/carto/bin/cartoymlcc).

- **carto** will transform your cartoCSS (.mml) project to a mapnik xml.
- **cartocc** will customize a cartoCSS (.mml) project (such as change database connection).
- **cartoymlcc** will transfom your yaml to a cartoCSS (.mml) project and customize it with cartocc.
