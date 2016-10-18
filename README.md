# Droid Module: nfs-client

Install and configure an NFS client and mount a share. For more information on
Droid, please see [droidphp.com](http://droidphp.com).

The steps involved are:-

1. Install the nfs-common package.
2. Create a mount-point for an NFS share.
3. Restart the NFS Common service.
4. Mount an NFS share.


## Assumptions

1. The platform is Debian-based.
2. An NFS server is running, exporting the desired share and permits the client
   machine to connect.


## Limitations

1. Only one NFS share may be mounted.
2. Any host configured to statically assign a port number to the lockd daemon
   (see Optional Information, below) will require a reboot.


## Configuration files managed by the module

Configuration files managed by the module will be overwritten each time the
module is run.

1. The following existing configuration files are overwritten:-

    - /etc/hosts.allow
    - /etc/hosts.deny

2. The following configuration files are installed by their respective platform
   packages during the execution of the module and then overwritten:-

    - /etc/default/nfs-common

3. The following new configuration files are written:-

    - /etc/modprobe.d/lockd.conf


## Information required by the module

1. Values for the following variables:-

        module_nfs_client:
          share:
            host: <string> # NFS Server host name or IP address
            path: <string> # The path of the share being served
          mount:
            path: <string> # Path to the client's mount-point
            mode: <string || number> # File mode of the mount-point
            opts: <string> # Mount options, see manpages mount(8) and nfs(5)

## Optional information

1. Per-host entries in hosts.allow and hosts.deny to secure access to NFS
   related daemons by way of tcpwrappers:-

        hosts:
          nfs_client:
            variables:
              hosts_deny:
                - <string> # suggest: "lockd: ALL"
                           #          "mountd: ALL"
                           #          "rpcbind: ALL"
                           #          "rquotad: ALL"
                           #          "statd: ALL"
              hosts_allow:
                - <string> # suggest: "lockd: 127.0.0.1"
                           #          "mountd: 127.0.0.1"
                           #          "rpcbind: 127.0.0.1"
                           #          "rquotad: 127.0.0.1"
                           #          "statd: 127.0.0.1"

2. Per-host default options in /etc/default/nfs-common to statically assign
   port numbers to the statd daemon:-

        hosts:
          nfs_client:
            variables:
              statd_opts:
                port: <integer>
                outgoing_port: <integer>

3. Per-host kernel options to statically assign TCP and UDP ports to the lockd
   daemon:-

        hosts:
          nfs_client:
            variables:
              lockd_opts:
                port: <integer>
