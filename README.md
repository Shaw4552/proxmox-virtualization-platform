# Proxmox Virtualization Platform & DNS Infrastructure

> **Portfolio Progression Project**
>
> This repository documents an earlier stage of my virtualization and infrastructure engineering work, focused on Proxmox VE, VM deployment, storage design, segmentation, and DNS integration.
>
> The current integrated multi-site environment is documented here:
> [Enterprise-Style Homelab Infrastructure](https://github.com/Shaw4552/homelab-public)

## Overview

This project documents the design and deployment of a virtualized infrastructure platform using Proxmox VE, including a segmented network architecture and a production-style DNS stack.

The goal of this environment is to simulate real-world infrastructure practices with a focus on:

- Security (least privilege, segmentation)
- Reliability (redundant services)
- Observability and validation
- Infrastructure-as-documented systems

---

## Architecture Summary

### Virtualization Layer
- Proxmox VE (single-node deployment)
- QEMU/KVM virtual machines
- LVM-backed storage + NVMe high-performance storage

### Network Design (Abstracted)

| VLAN | Purpose        |
|------|--------------|
| VLAN 10 | Management |
| VLAN 20 | Clients    |
| VLAN 30 | IoT        |
| VLAN 40 | Servers    |
| VLAN 50 | VPN        |

- Default-deny inter-VLAN routing
- Explicit allow rules for required services only

---

## DNS Infrastructure

### Primary DNS Stack
- Pi-hole (DNS filtering)
- Unbound (recursive resolver)
- Caddy (internal TLS reverse proxy)

### Secondary DNS Planning
- Replicated Pi-hole instance
- Planned synchronization between DNS nodes

### Features
- Centralized DNS resolution
- Domain-level filtering policies
- Internal service resolution (split DNS)
- DNS over VPN support

---

## Security Design

- Least-privilege firewall rules
- Segmentation between IoT, clients, and servers
- VPN-restricted management access
- No direct exposure of internal services to WAN

---

## Storage Design

- Proxmox host storage (LVM)
- Dedicated NVMe storage for VM workloads
- Separation of OS disk vs workload storage

---

## Virtual Machines Deployed

### Ubuntu Server (Docker Host)
- Base system for containerized services
- QEMU guest agent enabled
- Managed via SSH

### Planned
- Windows VM (for recovery and desktop use)
- Additional service nodes (monitoring, automation)

---

## Key Lessons Learned

- Importance of proper repository configuration (Proxmox subscription vs non-subscription)
- Storage planning impacts performance significantly
- DNS design must account for failover and consistency
- Network segmentation must be intentional from the start

---

## Improvements Identified at This Stage

- Automated configuration deployment (CI/CD for infrastructure)
- DNS synchronization between nodes
- Load-balanced reverse proxy layer
- Monitoring and alerting stack (Uptime Kuma / Prometheus)
- Infrastructure diagrams

---

## Notes on Sanitization

All IP addresses, hostnames, and identifiers have been modified or generalized to avoid exposing sensitive network details while preserving architectural accuracy.

---

## Why This Matters

This project demonstrates:

- Real-world infrastructure design thinking
- Secure network segmentation practices
- Virtualization and service orchestration
- Documentation-driven engineering

This project represents an early effort to apply structured infrastructure design and operational decision-making in a controlled lab environment.