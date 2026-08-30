# Create SSH tunnel

Opens a port on your machine and tunnel all traffic to a custom target
host via the SSH server, for example to connect with a database server
behind a firewall.

## Usage

``` r
ssh_tunnel(session, port = 5555, target = "rainmaker.wunderground.com:23")
```

## Arguments

- session:

  ssh connection created with
  [`ssh_connect()`](https://docs.ropensci.org/ssh/reference/ssh.md)

- port:

  integer of local port on which to listen for incoming connections

- target:

  string with target host and port to connect to via ssh tunnel

## Details

This function blocks while the tunnel is active. Use the tunnel by
connecting to `localhost:5555` from a separate process. Each tunnel can
only be used once and will automatically be closed when the client
disconnects. It is intended to tunnel a single connection, not as a long
running proxy server.

## See also

Other ssh: [`scp`](https://docs.ropensci.org/ssh/reference/scp.md),
[`ssh_connect()`](https://docs.ropensci.org/ssh/reference/ssh.md),
[`ssh_credentials`](https://docs.ropensci.org/ssh/reference/ssh_credentials.md),
[`ssh_exec`](https://docs.ropensci.org/ssh/reference/ssh_exec.md)
