# SLURM Cluster with Vagrant

This deployment demonstration is meant to run on your local desktop with Vagrant, designed under macOS but should run on Linux as well.

## Usage

The cluster should be initialized from the recipe in the `Makefile`:

```
make setup
```

It will take 5-30mins to build all the VMs. An internet connection is required.

Once they are built, you can test with

```
make test
```

This will submit a compute job to SLURM. The job's stdout log will be written to `/mnt/nfs/var/nfsshare` on the compute node, which corresponds to `/var/nfsshare` on the head node using NFS sharing.

If you need to reset the VM's after they have been built (e.g. to initialize Vagrant settings or simulate a reboot, etc.), you can use the following commands

```
# reboot the VMs
vagrant reload

# start all the services
make reload
```

## Extra Commands

Some extra Vagrant commands that are helpful for managing the cluster setup:

Check VM statuses

```
vagrant status
```

Build VMs with

```
vagrant up
```

Enter a VM

```
vagrant ssh headnode
```

Stop VM with

```
vagrant halt
```

Remove with

```
vagrant destroy -f
```

Re-sync the `/vagrant/` directory inside each VM with the host directory (this directory)

```
vagrant rsync
```
