# Execute Remote Command

Run a command or script on the host while streaming stdout and stderr
directly to the client.

## Usage

``` r
ssh_exec_wait(
  session,
  command = "whoami",
  std_out = stdout(),
  std_err = stderr()
)

ssh_exec_internal(session, command = "whoami", error = TRUE)
```

## Arguments

- session:

  ssh connection created with
  [`ssh_connect()`](https://docs.ropensci.org/ssh/reference/ssh.md)

- command:

  The command or script to execute

- std_out:

  callback function, filename, or connection object to handle stdout
  stream

- std_err:

  callback function, filename, or connection object to handle stderr
  stream

- error:

  automatically raise an error if the exit status is non-zero

## Details

The `ssh_exec_wait()` function is the remote equivalent of the local
[`sys::exec_wait()`](https://jeroen.r-universe.dev/sys/reference/exec.html).
It runs a command or script on the ssh server and streams stdout and
stderr to the client to a file or connection. When done it returns the
exit status for the remotely executed command.

Similarly `ssh_exec_internal()` is a small wrapper analogous to
[`sys::exec_internal()`](https://jeroen.r-universe.dev/sys/reference/exec.html).
It buffers all stdout and stderr output into a raw vector and returns it
in a list along with the exit status. By default this function raises an
error if the remote command was unsuccessful.

## See also

Other ssh: [`scp`](https://docs.ropensci.org/ssh/reference/scp.md),
[`ssh_connect()`](https://docs.ropensci.org/ssh/reference/ssh.md),
[`ssh_credentials`](https://docs.ropensci.org/ssh/reference/ssh_credentials.md),
[`ssh_tunnel()`](https://docs.ropensci.org/ssh/reference/ssh_tunnel.md)

## Examples

``` r
if (FALSE) { # \dontrun{
session <- ssh_connect("dev.opencpu.org")
ssh_exec_wait(session, command = c(
  'curl -O https://cran.r-project.org/src/contrib/jsonlite_1.5.tar.gz',
  'R CMD check jsonlite_1.5.tar.gz',
  'rm -f jsonlite_1.5.tar.gz'
))
ssh_disconnect(session)} # }
```
