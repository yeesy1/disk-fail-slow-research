# Experimental Plan

## Phase 1: Environment Preparation

Provision at least three bare-metal nodes with local SSDs and deploy a Ceph storage cluster.

Verify storage topology, device access permissions, network connectivity, and monitoring availability.

## Phase 2: Baseline Measurement

Generate representative block, file, and object storage workloads.

Collect disk-level I/O metrics without fault injection to establish baseline performance.

## Phase 3: Fail-Slow Fault Injection

Introduce controlled I/O latency and investigate device performance degradation.

Record affected devices, injection start/end times, fault parameters, and system behavior.

## Phase 4: Data Collection and Analysis

Collect time-series performance metrics, synchronize timestamps, and associate fault injection records with affected devices.

Compare normal and degraded devices to investigate workload-dependent fail-slow behavior.

## Phase 5: Detection Evaluation

Construct labeled datasets and evaluate fail-slow detection methods using disk-level performance metrics.

The evaluation will focus on detection effectiveness under varying workloads and degradation severities.
