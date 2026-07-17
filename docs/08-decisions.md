# Architecture Decision Records (ADR)

This document records the most important architectural and technical decisions made throughout the project lifecycle.

---

# ADR-001

## Title

Use Ubuntu Server 24.04 LTS

## Status

Accepted

## Context

A lightweight, stable, and production-ready operating system is required.

## Decision

Use Ubuntu Server 24.04 LTS.

## Rationale

- Long-Term Support (LTS)
- Low resource consumption
- Excellent Docker compatibility
- Large community support
- Widely adopted in production environments

---

# ADR-002

## Title

Use Docker Compose

## Status

Accepted

## Context

The platform will initially run on a single virtual machine.

## Decision

Use Docker Compose for container orchestration.

## Rationale

- Simple deployment
- Easy maintenance
- Fully reproducible environment
- Appropriate for a DevOps portfolio project

---

# ADR-003

## Title

Prometheus-Based Monitoring Stack

## Status

Accepted

## Context

The platform requires infrastructure and container monitoring.

## Decision

Use:

- Prometheus
- Grafana
- Node Exporter
- cAdvisor
- Alertmanager

## Rationale

- Industry standard
- Open-source ecosystem
- Excellent integration
- Highly scalable

---

# ADR-004

## Title

Use Nginx as Reverse Proxy

## Status

Accepted

## Context

Multiple web services must be exposed through a single entry point.

## Decision

Deploy Nginx as a reverse proxy.

## Rationale

- Lightweight
- High performance
- Easy configuration
- Production-ready

---

# ADR-005

## Title

SSH Commit Signing

## Status

Accepted

## Context

Every commit should be authenticated and verifiable.

## Decision

Use SSH-based commit signing for the entire repository.

## Rationale

- Verified commits on GitHub
- Improved repository trust
- Industry best practice

---

# ADR-006

## Title

Continuous Documentation

## Status

Accepted

## Context

Most personal projects only document the final result.

## Decision

Document every phase, configuration, incident, and architectural decision throughout the project.

## Rationale

- Improves reproducibility
- Demonstrates engineering methodology
- Serves as technical documentation
- Increases portfolio value

---

# ADR-007

## Title

Reproducible Infrastructure

## Status

Accepted

## Context

The entire environment should be deployable from scratch.

## Decision

Store all infrastructure configuration in Git and automate deployment through scripts.

## Rationale

- Infrastructure as Code (IaC)
- Reproducibility
- Automation
- Simplified deployment

---

# ADR-008

## Title

Self-Healing Architecture

## Status

Accepted

## Context

The objective is to build more than a traditional monitoring platform.

## Decision

Implement automatic recovery capabilities using Python, Docker Engine API, and infrastructure automation.

## Rationale

- Simulates real-world SRE environments
- Demonstrates automation skills
- Adds significant value to the project

---

# ADR-009

## Title

Documentation-Driven Development

## Status

Accepted

## Context

Every infrastructure change should be traceable and reproducible.

## Decision

Documentation will be written immediately after implementing each feature or configuration.

## Rationale

- Prevents knowledge loss
- Improves maintainability
- Simplifies troubleshooting
- Keeps repository synchronized with implementation

---

# Future Decisions

Every significant architectural or technical decision must be documented using the same ADR format.
