[![npm version](https://badge.fury.io/js/get-free-port.svg)](https://badge.fury.io/js/get-free-port)

# GET-FREE-PORT

BEFORE:

```sh
# Project 1
$ next -p 3004

# Project 2
$ gatsby develop -p 3005

# Project 3
$ node expressapp.js -p 3006

# A week later, starting a new project...
# Project 4
# Did I already use port 3005? Or was the next one 3006?
$ ./koaapp.js --port 3006 # oops!

# Open another terminal, want to run second instance, up arrow + enter, and...
$ ./koaapp.js --port 3006 # guaranteed EADDRINUSE!
```

AFTER:

```sh
# Install GNP in your path
$ npm install -g get-next-port

# Project 1
$ next -p `get-free-port proj1` # port A

# Project 2
$ gatsby develop -p `get-free-port proj2` # port B

# Project 3
$ node expressapp.js -p `npx get-free-port proj3` # Or don't install GNP at all!

# A week later, starting a new project...
# Project 4
$ ./koaapp.js --port `get-free-port proj4` # port D

# And in another window, we want to start another dev instance without problems
$ ./koaapp.js --port `get-free-port proj4` # will run on the next available port
```

This tool takes in an identifier (`id`) and spits out a mapped port number.
Hence, subsequent calls using the same `id` will get the same port number again
and again. The only exception is when the mapped port is being used by another
process, in which case this tool temporarily returns the next least unused port
number using [detect-port](https://github.com/node-modules/detect-port). Once
the originally mapped port is no longer in use, later calls with the same `id`
will return it.

Port numbers start at 3000. You can change/delete your port mappings in the
`_portmap.json` file at `~/.config/_portmap.json`.

This is useful if, like me, you're running any dozen dev servers off the same
rig and like to have consistent port numbers for your projects with the added
flexibility of temporary port assignments.

## Installation and Usage

```sh
npm install -g get-next-port
get-next-port ident
```

This tool can also be used via NPX without installing anything:

```sh
$ echo `npx get-free-port ident`
```