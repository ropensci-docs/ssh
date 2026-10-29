# SCP (Secure Copy)

Upload and download files to/from the SSH server via the scp protocol.
Directories in the `files` argument are automatically traversed and
uploaded / downloaded recursively.

## Usage

``` r
scp_download(session, files, to = ".", verbose = TRUE)

scp_upload(session, files, to = ".", verbose = TRUE)
```

## Arguments

- session:

  ssh connection created with
  [`ssh_connect()`](https://docs.ropensci.org/ssh/reference/ssh.md)

- files:

  path to files or directory to transfer

- to:

  existing directory on the destination where `files` will be copied
  into

- verbose:

  print progress while copying files

## Details

Note that the syntax is slightly different from the `scp` command line
tool because the `to` parameter is always a target *directory* where all
`files` will be copied **into**. If `to` does not exist, it will be
created.

The `files` parameter in `scp_upload()` is vectorised hence all files
and directories will be recursively uploaded **into** the `to`
directory. For `scp_download()` the `files` parameter must be a single
string which may contain wildcards.

The default path `to = "."` means that files get downloaded to the
current working directory and uploaded to the user home directory on the
server.

## See also

Other ssh:
[`ssh_connect()`](https://docs.ropensci.org/ssh/reference/ssh.md),
[`ssh_credentials`](https://docs.ropensci.org/ssh/reference/ssh_credentials.md),
[`ssh_exec`](https://docs.ropensci.org/ssh/reference/ssh_exec.md),
[`ssh_tunnel()`](https://docs.ropensci.org/ssh/reference/ssh_tunnel.md)

## Examples

``` r
if (FALSE) { # \dontrun{
# recursively upload files and directories
session <- ssh_connect("dev.opencpu.org")
files <- c(R.home("doc"), R.home("COPYING"))
scp_upload(session, files, to = "~/target")

# download it back
scp_download(session, "~/target/*", to = tempdir())

# delete it from the server
ssh_exec_wait(session, command = "rm -Rf ~/target")
ssh_disconnect(session)
} # }
```
