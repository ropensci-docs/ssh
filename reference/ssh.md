# SSH Client

Create an ssh session using `ssh_connect()`. The session can be used to
execute commands, scp files or setup a tunnel.

## Usage

``` r
ssh_connect(host, keyfile = NULL, passwd = askpass, verbose = FALSE)

ssh_session_info(session)

ssh_disconnect(session)

libssh_version()
```

## Arguments

- host:

  an ssh server string of the form `[user@]hostname[:@port]`. An ipv6
  hostname should be wrapped in brackets like this: `[2001:db8::1]:80`.

- keyfile:

  path to private key file. Must be in OpenSSH format (see details)

- passwd:

  either a string or a callback function for password prompt

- verbose:

  either TRUE/FALSE or a value between 0 and 4 indicating log level: 0:
  no logging, 1: only warnings, 2: protocol, 3: packets or 4: full stack
  trace.

- session:

  ssh connection created with `ssh_connect()`

## Details

The client first tries to authenticate using a private key, either from
ssh-agent or `/.ssh/id_rsa` in the user home directory. If this fails it
falls back on challenge-response (interactive) and password auth if
allowed by the server. The `passwd` parameter can be used to provide a
passphrase or a callback function to ask prompt the user for the
passphrase when needed.

The session will automatically be disconnected when the session object
is removed or when R exits but you can also use `ssh_disconnect()`.

**Windows users:** the private key must be in OpenSSH PEM format. If you
open it in a text editor the first line must be:
`-----BEGIN RSA PRIVATE KEY-----`. To convert a Putty PKK key, open it
in the *PuttyGen* utility and go to *Conversions -\> Export OpenSSH*.

## See also

Other ssh: [`scp`](https://docs.ropensci.org/ssh/reference/scp.md),
[`ssh_credentials`](https://docs.ropensci.org/ssh/reference/ssh_credentials.md),
[`ssh_exec`](https://docs.ropensci.org/ssh/reference/ssh_exec.md),
[`ssh_tunnel()`](https://docs.ropensci.org/ssh/reference/ssh_tunnel.md)

## Examples

``` r
if (FALSE) { # \dontrun{
session <- ssh_connect("dev.opencpu.org")
ssh_exec_wait(session, command = "whoami")
ssh_disconnect(session)
} # }
```
