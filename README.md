# h4ckm4ch1n3
A contenerized pentesting environement for recreational CTF using OpenVPN.

## Usage
> ⚠️ Your docker engine must not be in swarm mode

There's 2 main tools included :

### The Hackmachine
It's a [parrotsec container](https://hub.docker.com/r/parrotsec/security) you
can run it with :

`docker-compose run --rm hackmachine`

You'll be dropped in a root shell with full access to the tools included, if
you need more, first update apt repositories with `apt update` and then install
whatever you need.

For convinience, you can add hostsnames to the network with the `extra_hosts`
parameter of the `vpn` service.

### The Browser
In some of those CTF you might need to access webpages with a browser, to avoid
connecting your main machine to the VPN, you can use this container to get a
browser with vpn access in you browser. Run it with :

`docker-compose run --rm -d browser`

You can then access it at [http://localhost:8080](http://localhost:8080)

If the window seems too small click on the "maximize" button in the top right
corner.

### Under the hood™
Under the hood there's two utilities containers :

### The VPN
It's an OpenVPN client container, it reads your `*.ovpn` files from the `./vpn`
directory.
It's configured to allow an access to the internet via the host network if the
vpn network you're connected to doesn't allow it.

### The Proxy
Any container connected to the VPN won't be accessible via the host network, to
circumvent this, there is a proxy container allowing you to access `http`
traffic only, the syntax to add a new one :

`-w "http://<service>[:port];/<route>"`
