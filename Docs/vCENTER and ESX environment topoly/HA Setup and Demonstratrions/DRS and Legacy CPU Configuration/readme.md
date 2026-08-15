# DRS and CPU Compatibility — EVC Considerations

## Purpose

This document describes how **Enhanced vMotion Compatibility (EVC)** could be used within the KLM VMware lab environment to improve CPU compatibility between hosts with different processor generations.

**EVC is not currently enabled in the environment.**

This document therefore describes EVC as a potential design option rather than an active configuration.

The purpose is to document the reasoning behind the design and provide a reference for future hardware changes, cluster expansion, or migration requirements.

---

## Current Environment

The lab contains multiple ESXi hosts with different hardware generations and ESXi versions.

| Host | ESXi Version | Connection State | CPU / Memory |
|---|---|---|---|
| KLMESX01 | 7.0.3 | Connected | 4 CPU / 12 GB RAM |
| KLMESX02 | 6.5.0 | Connected | 4 CPU / 12 GB RAM |
| KLMESX03 | 7.0.3 | Offline | 2 CPU / 4 GB RAM |
| KLMESX04 | 7.0.3 | Offline | 2 CPU / 4 GB RAM |

The environment is primarily a **lab / test environment**, rather than a production workload.

Because the hosts are not identical, CPU compatibility should be considered when planning features such as:

- vMotion
- DRS
- Cluster expansion
- Hardware replacement
- Host migration
- VM mobility between different CPU generations

---

## What is EVC?

**Enhanced vMotion Compatibility (EVC)** is a VMware vSphere feature that establishes a common CPU feature baseline for virtual machines running within a cluster.

Different generations of CPUs can expose different instruction sets and CPU capabilities.

For example:

```text
Newer CPU
    |
    |  exposes additional CPU instructions
    v
+-----------------------+
| New CPU feature set   |
+-----------------------+

Older CPU
    |
    |  does not support some newer instructions
    v
+-----------------------+
| Older CPU feature set |
+-----------------------+
