# Mount CephFS using Kernel Driver {#cephfs-mount-using-kernel-driver}

The CephFS kernel driver is part of the Linux kernel. It allows mounting
CephFS as a regular file system with native kernel performance. It is
the client of choice for most use-cases.

:::: note
::: title
Note
:::

CephFS mount device string now uses a new (v2) syntax. The mount helper
(and the kernel) is backward compatible with the old syntax. This means
that the old syntax can still be used for mounting with newer mount
helpers and kernel. However, it is recommended to use the new syntax
whenever possible.
::::

## Prerequisites

### Complete General Prerequisites

Go through the prerequisites required by both, kernel as well as FUSE
mounts, in [Mount CephFS: Prerequisites](../mount-prerequisites) page.

### Is mount helper present?

`mount.ceph` helper is installed by Ceph packages. The helper passes the
monitor address(es) and CephX user keyrings, saving the Ceph admin the
effort of passing these details explicitly while mounting CephFS. If the
helper is not present on the client machine, CephFS can still be mounted
using the kernel driver, but only by passing these details explicitly to
the `mount` command. To check whether `mount.ceph` is present on your
system, run the following command:

::: prompt
bash \#

stat /sbin/mount.ceph
:::

### Which Kernel Version?

Because the kernel client is distributed as part of the linux kernel
(not as part of packaged ceph releases), you will need to consider which
kernel version to use on your client nodes. Older kernels are known to
include buggy ceph clients, and may not support features that more
recent Ceph clusters support.

Remember that the \"latest\" kernel in a stable linux distribution is
likely to be years behind the latest upstream linux kernel where Ceph
development takes place (including bug fixes).

As a rough guide, as of Ceph 10.x (Jewel), you should be using a least a
4.x kernel. If you absolutely have to use an older kernel, you should
use the fuse client instead of the kernel client.

This advice does not apply if you are using a linux distribution that
includes CephFS support, as in this case the distributor will be
responsible for backporting fixes to their stable kernel: check with
your vendor.

## Synopsis

In general, the command to mount CephFS via kernel driver looks like
this:

    mount -t ceph {device-string}={path-to-mounted} {mount-point} -o {key-value-args} {other-args}

## Mounting CephFS

On Ceph clusters, CephX is enabled by default. Use `mount` command to
mount CephFS with the kernel driver:

    mkdir /mnt/mycephfs
    mount -t ceph <name>@<fsid>.<fs_name>=/ /mnt/mycephfs

`name` is the username of the CephX user we are using to mount CephFS.
`fsid` is the FSID of the ceph cluster which can be found using
`ceph fsid` command. `fs_name` is the file system to mount. The kernel
driver requires MON\'s socket and the secret key for the CephX user,
e.g.:

    mount -t ceph cephuser@b3acfc0d-575f-41d3-9c91-0e7ed3dbb3fa.cephfs=/ -o mon_addr=192.168.0.1:6789,secret=AQATSKdNGBnwLhAAnNDKnH65FmVKpXZJVasUeQ==

When using the mount helper, monitor hosts and FSID are optional.
`mount.ceph` helper figures out these details automatically by finding
and reading ceph conf file, .e.g:

    mount -t ceph cephuser@.cephfs=/ -o secret=AQATSKdNGBnwLhAAnNDKnH65FmVKpXZJVasUeQ==

:::: note
::: title
Note
:::

Note that the dot (`.`) still needs to be a part of the device string.
::::

A potential problem with the above command is that the secret key is
left in your shell\'s command history. To prevent that you can copy the
secret key inside a file and pass the file by using the option
`secretfile` instead of `secret`:

    mount -t ceph cephuser@.cephfs=/ /mnt/mycephfs -o secretfile=/etc/ceph/cephuser.secret

Ensure the permissions on the secret key file are appropriate
(preferably, `600`).

Multiple monitor hosts can be passed by separating each address with a
`/`:

    mount -t ceph cephuser@.cephfs=/ /mnt/mycephfs -o mon_addr=192.168.0.1:6789/192.168.0.2:6789,secretfile=/etc/ceph/cephuser.secret

In case CephX is disabled, you can omit any credential related options:

    mount -t ceph cephuser@.cephfs=/ /mnt/mycephfs

:::: note
::: title
Note
:::

The ceph user name still needs to be passed as part of the device
string.
::::

To mount a subtree of the CephFS root, append the path to the device
string:

    mount -t ceph cephuser@.cephfs=/subvolume/dir1/dir2 /mnt/mycephfs -o secretfile=/etc/ceph/cephuser.secret

## Backward Compatibility

The old syntax is supported for backward compatibility.

To mount CephFS with the kernel driver:

    mkdir /mnt/mycephfs
    mount -t ceph :/ /mnt/mycephfs -o name=admin

The key-value argument right after option `-o` is CephX credential;
`name` is the username of the CephX user we are using to mount CephFS.

To mount a non-default FS `cephfs2`, in case the cluster has multiple
FSs:

    mount -t ceph :/ /mnt/mycephfs -o name=admin,fs=cephfs2

    or

    mount -t ceph :/ /mnt/mycephfs -o name=admin,mds_namespace=cephfs2

:::: note
::: title
Note
:::

The option `mds_namespace` is deprecated. Use `fs=` instead when using
the old syntax for mounting.
::::

## Unmounting CephFS

To unmount the Ceph file system, use the `umount` command as usual:

    umount /mnt/mycephfs

:::: tip
::: title
Tip
:::

Ensure that you are not within the file system directories before
executing this command.
::::

## Persistent Mounts

To mount CephFS in your file systems table as a kernel driver, add the
following to `/etc/fstab`:

    {name}@.{fs_name}=/ {mount}/{mountpoint} ceph [mon_addr={ipaddress},secret=secretkey|secretfile=/path/to/secretfile],[{mount.options}]  {fs_freq}  {fs_passno}

For example:

    cephuser@.cephfs=/     /mnt/ceph    ceph    mon_addr=192.168.0.1:6789,noatime,_netdev    0       0

If the `secret` or `secretfile` options are not specified then the mount
helper will attempt to find a secret for the given `name` in one of the
configured keyrings.

See [User Management](../../rados/operations/user-management/) for
details on CephX user management and
[mount.ceph](../../man/8/mount.ceph/) manual for more options it can
take. For troubleshooting, see
`kernel_mount_debugging`{.interpreted-text role="ref"}.