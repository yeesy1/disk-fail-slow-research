# disk-fail-slow-research
Research on disk fail-slow fault injection and detection in distributed storage systems.
# Disk Fail-Slow Fault Injection and Detection in Distributed Storage Systems

## Overview

This project investigates **disk fail-slow failures in distributed storage systems**, with a particular focus on NVMe SSDs.

Unlike fail-stop failures, where a storage device becomes completely unavailable, fail-slow failures allow the device to continue processing I/O requests while exhibiting degraded performance. Such failures may cause elevated I/O latency, throughput fluctuations, and performance degradation across distributed storage nodes.

The goal of this project is to establish a reproducible experimental environment for studying disk fail-slow behavior through controlled fault injection, performance monitoring, and anomaly detection.

The research builds upon previous experiments involving fail-slow fault injection and detection in a three-node Ceph storage environment.

## Research Objectives

The project focuses on three research objectives:

1. **Fault Injection:** Reproduce different types and severities of disk fail-slow failures through controlled NVMe SSD fault injection.
2. **Performance Characterization:** Investigate how disk-level performance degradation affects I/O latency, throughput, queue depth, and distributed storage performance.
3. **Fail-Slow Detection:** Collect labeled performance traces and evaluate detection methods under different workloads and fault conditions.

## Experimental Environment

The planned experimental environment consists of a distributed storage cluster with at least three Linux nodes.

The cluster will use Ceph as the distributed storage platform, with local physical SSDs or NVMe SSDs serving as storage devices.

### Infrastructure Requirements

| Component | Requirement |
|---|---|
| Cluster size | At least 3 physical or bare-metal nodes |
| Operating system | Linux |
| Storage system | Ceph |
| Storage devices | Local physical SSDs / NVMe SSDs |
| Permissions | Root/sudo access |
| Networking | Inter-node network connectivity |
| Workloads | Block, file, and object storage I/O |

**Physical storage access is essential** because the experiments require controlled fault injection at the Linux block I/O or NVMe device level. Virtual disks and cloud-managed block volumes may not expose the necessary device-level interfaces.

## Fault Injection Methodology

The experiments investigate two main fault injection mechanisms, based on previous research.

### 1. I/O Delay Injection

I/O delay injection simulates a degraded storage device by introducing additional latency into I/O request processing.

Previous experiments used an NVMe hijacking kernel module to intercept selected device I/O requests and introduce configurable delays.

Representative delay configurations include:

- 4 ms
- 5 ms
- 15 ms

Different delay intensities and injection durations can be used to investigate persistent and transient performance degradation.

### 2. NVMe Power-State Degradation

Power-state-based fault injection aims to simulate SSD performance degradation by modifying supported NVMe power-management settings or limiting device performance.

This method can be used to examine reduced I/O processing capacity without intentionally disconnecting the storage device.

Its applicability depends on the capabilities of the physical SSD, its firmware, and the operating system.

## Workload Generation

Experiments will evaluate the effects of injected faults under different storage access patterns.

The planned workloads include:

- **Block storage:** Random and mixed read/write I/O workloads.
- **File storage:** File read/write workloads using CephFS.
- **Object storage:** Object read/write workloads with different object sizes.

Workload parameters such as I/O size, read/write ratio, and concurrency will be varied to investigate the interaction between normal workload fluctuations and disk fail-slow behavior.

## Performance Monitoring

The experiments will collect disk-level performance metrics before, during, and after fault injection.

Primary metrics include:

| Metric | Description |
|---|---|
| r_await | Average read request latency |
| w_await | Average write request latency |
| rMB/s | Read throughput |
| wMB/s | Write throughput |
| aqu-sz | Average I/O queue depth |
| %util | Device utilization |

Fault injection timestamps, affected devices, and injection parameters will be recorded to construct labeled time-series datasets for subsequent analysis.

## Experimental Workflow

The planned experimental workflow consists of the following stages:

1. Provision a three-node Ceph storage cluster with physical NVMe SSDs.
2. Configure workloads and collect baseline I/O performance metrics.
3. Inject controlled fail-slow faults into selected storage devices.
4. Collect performance metrics throughout the injection period.
5. Remove the injected fault and verify recovery.
6. Construct labeled datasets and evaluate fail-slow detection methods.

The experiments will be conducted in an isolated research environment using designated test devices.

## Current Status

**Project status: Research planning and experimental environment preparation.**

Previous academic work established a foundation for studying fail-slow behavior using a three-node Ceph cluster, NVMe delay injection, power-state degradation, and multi-metric performance monitoring.

The current project focuses on extending this work through reproducible experiments on physical SSDs.

The implementation and experiment scripts will be added as the experimental environment becomes available.

## Resource Request

We are seeking access to a research testbed, such as CloudLab or Emulab, providing at least three interconnected bare-metal nodes equipped with local physical SSDs or NVMe SSDs.

The required environment should support administrative access and device-level fault injection experiments.

The requested resources will be used exclusively for academic research on distributed storage reliability and fail-slow fault detection.

## Keywords

Distributed Storage, Ceph, NVMe SSD, Fail-Slow, Fault Injection, Performance Degradation, Anomaly Detection
