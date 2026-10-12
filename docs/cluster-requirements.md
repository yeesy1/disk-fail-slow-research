# Experimental Cluster Requirements

## Cluster Architecture

This project requires a distributed storage testbed consisting of at least three interconnected Linux nodes.

Each node will participate in a Ceph storage cluster and host one or more physical SSDs or NVMe SSDs.

## Hardware Requirements

| Resource | Requirement |
|---|---|
| Nodes | At least 3 bare-metal servers |
| Storage | At least one local physical SSD/NVMe SSD per node |
| Access | Root/sudo privileges |
| Network | Inter-node IP connectivity |
| Operating System | Linux with suitable kernel support |
| Storage Software | Ceph |

## Why Bare-Metal Servers?

The experiments require access to physical storage devices for controlled fail-slow fault injection.

Specifically, the project investigates:

- Artificial delays in the Linux block I/O path.
- NVMe SSD performance degradation using supported device controls.
- The propagation of disk-level latency abnormalities through a distributed storage system.

Virtualized disks or managed cloud block volumes may conceal underlying device behavior and restrict low-level operations.

## Cluster Deployment

The planned cluster consists of three storage nodes:

- Node 1: Ceph storage services and fault injection target.
- Node 2: Ceph storage services and peer comparison.
- Node 3: Ceph storage services and peer comparison.

All nodes will be monitored during baseline, fault injection, and recovery experiments.

Fault injection will be restricted to authorized experimental devices, with device identities verified before testing.
