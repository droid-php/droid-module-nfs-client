# Droid Module: droid/nfs-client

Install and configure an NFS client and mount a share. For more information on
Droid, please see [droidphp.com](http://droidphp.com).

The steps involved are:-

1. Update platform packages.
2. Install the nfs-common package.
3. Create a mount-point for an NFS share.
4. Mount an NFS share.


## Assumptions

1. The platform is Debian-based.
2. An NFS server is running, exporting the desired share and permits the client
   machine to connect.


## Limitations

1. Only one NFS share may be mounted.


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

None.
