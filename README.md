# SLURM Cluster

This repository contains scripted deployment methods for the [SLURM](https://slurm.schedmd.com/documentation.html) cluster resource manager.

Notably, this repo demonstrates how to build SLURM from source, and set up a cluster on CentOS 7 (RHEL 7 equivalent), in order to replicate the production configuration that would be used on a High Performance Compute cluster (HPC).

These SLURM deployments are meant to be used as a testing ground for working with and developing software that interacts with SLURM.

## Build Methods

Several build methods are included, in order to demonstrate the usage of different technologies. Choose the method that works best for your intended usage. As much as possible, the final deployed SLURM cluster will be the same between all methods.

### Vagrant

A cluster deployment method that uses Vagrant in order to provision CentOS 7 virtual machines. This is intended to be used from a host system running an operating system such as macOS.

### LXC

(in progress)

### Docker

SLURM cluster deployment is not recommended with Docker due to incompatibilites with the `systemctl` system inside Docker containers. Docker is not supported here, though a template `Dockerfile` is included to get you started if you want to try it yourself.

# Software

Tested on macOS 10.12

- SLURM 18.08.8

- Vagrant 2.0.1

- CentOS 7

- GNU `make`, `bash`

# Notes

A method of building a demo SLURM cluster using Vagrant with Ubuntu pre-built packages can be found here: https://github.com/stevekm/slurm-cluster-vagrant
