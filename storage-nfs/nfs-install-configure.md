**On NFS Server:**

**Update Package Repositories:**
This command updates the package repositories on your Ubuntu system to ensure you have the latest package information.

```bash
sudo apt update
```
**Install NFS Server Package:**

This command installs the NFS server package (nfs-kernel-server) on your Ubuntu system, which allows your system to act as an NFS server and share directories over the network.
```bash
sudo apt install nfs-kernel-server
```
**Create Directory to Share:**

This command creates a directory (/nfs/share) on your system that you want to share via NFS. You can replace /nfs/share with the path to the directory you want to share.

```bash
sudo mkdir -p /nfs/share
```
**Configure NFS Exports:**

This command opens the exports file (/etc/exports) in the Nano text editor, allowing you to specify which directories to share and define the access permissions for NFS clients.

```bash
sudo vi /etc/exports
```

**Add a line in the following format:**

Add a line in the following format to the exports file:
/path/to/directory client_IP(options)

 In the exports file, you need to specify the directory you want to share (/nfs/share in this example), followed by the IP address or network range of the NFS clients allowed to access the share (* allows access from any IP), and the access permissions and options for the share (rw for read-write access, sync for synchronous writes, no_subtree_check to disable subtree checking).
```bash
/nfs/share *(rw,sync,no_subtree_check)
```
**Restart NFS Server:**
After making changes to the exports file, you need to restart the NFS server service (nfs-kernel-server) for the changes to take effect and the shared directories to become available to NFS 
clients.
```bash
sudo systemctl restart nfs-kernel-server
```

**Configuring NFS Client on Client Machine:**

**Install NFS Client Package:**

These commands update the package repositories and then install the NFS client package (nfs-common) on the client machine, which allows it to mount NFS shares from remote servers.
```bash
sudo apt update
sudo apt install nfs-common
```
**Create Directory to Mount NFS Share:**

This command creates a directory (/shared/data) on the client machine where the NFS share will be mounted.
```bash
sudo mkdir -p /shared/data
```

**Mount NFS Share:**

This command mounts the NFS share from the NFS server (identified by server_IP) to the directory you created on the client machine (/shared/data). Replace server_IP with the IP address of the NFS server and /nfs/share with the path to the shared directory on the server.
```bash
sudo mount -t nfs nfs_server_IP:/nfs/share /shared/data
```
**Access NFS Share:**

The NFS share is now mounted on the client machine at /shared/data, allowing you to read from and write to the shared directory /nfs/share as if it were a local directory on the client machine.
