# Distributed CTF management scripts

## Scoreboard

Setting up the scoreboard is as simple as running the
`scoreboard/mellivora-install` script as root on a box running Debian or
Ubuntu.  It is recommended to do this on a VM or EC2 instance as this
script will install fresh copied of MySQL, Apache 2, PHP.

# Challenges

To set up the challenges, 
you will need to set up a host run the challenges on. 
You will need to make sure that this host has `docker` installed.

In the `ctf-master` script, set:

* `SERVER` to be the name of the host the challenges will run from,
* `LOGIN` to be the full user in the `docker` group to connect to the
  host with (you will need to set up SSH keys for this user),

# Creating Challenges

Each challenge consists of a few key elements:

* The `Dockerfile` which ensures the correct requirements are installed
  and configured on the server.
  This may include installing a web server for web challenges (see the
  `web-sample` and `web-template`),
  building a source file and setting up `xinetd` for a binary exploit
  challenge (see `net-sample` and `net-template`.
* The challenge content in the `content` directory, and
* `ctf.sh` containing the configuration of the challenge.

**NOTE**: Network services must expose on the port 9091. This is then
used by the `ctf-master` script to map the port to an externally visible
port.

Firstly, the `Dockerfile` is used to build the container that will host
the challenge. This will install the necessary software, copy in the
challenge content, and build any necessary dependancies.

Then, the container can then be run.

Challenges must be copied or linked into the `challenges` directory. The
**challenge id** is the name of the directory under `challenges`.

# Managing Challenges

Managing challenges is easy with the `ctf-master` script. Use
`ctf-master -h` to see how to use it.
