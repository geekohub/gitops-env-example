# Rancher Golden Path: Secure & Observable Kubernetes

This repository defines a **Rancher Fleet–based golden path** that automatically deploys **SUSE Security (NeuVector)** and **SUSE Observability (StackState)** to Kubernetes clusters.

The goal is to ensure that **every cluster onboarded into Rancher is secure and observable by default**, with behavior controlled entirely through Git.

---

## 🚀 What This Golden Path Provides

- Zero-touch installation on cluster registration
- Environment-aware configuration (dev vs prod)
- GitOps-driven security enforcement
- Unified observability and security context
- Auditable, repeatable, and scalable platform delivery

---

## 🧱 Architecture Overview

```text
┌──────────────────────────────────────────────┐
│                Platform Team                 │
│   (Defines policy, standards, golden paths)  │
└──────────────────────┬───────────────────────┘
                       │ Git (Fleet)
                       ▼
┌──────────────────────────────────────────────────────────┐
│                    Rancher Prime                         │
│                                                          │
│  • Centralized cluster lifecycle management              │
│  • Fleet-based GitOps at scale                           │
│  • Identity & access (SSO, RBAC, compliance)             │
│  • Policy-driven governance                              │
│  • Enterprise support & lifecycle assurance              │
└───────────────┬──────────────────────┬───────────────────┘
                │                      │
                ▼                      ▼
┌──────────────────────────┐   ┌──────────────────────────┐
│   SUSE Security          │   │   SUSE Observability     │
│   (NeuVector)            │   │   (StackState)           │
│                          │   │                          │
│ • Image & runtime security│  │ • Topology & dependencies│
│ • Admission control       │  │ • Change intelligence    │
│ • Policy enforcement      │  │ • Events & SLOs          │
└───────────────┬──────────┘   └───────────────┬──────────┘
                │                              │
                └──────────────┬───────────────┘
                               ▼
               ┌────────────────────────────────┐
               │        Kubernetes Clusters     │
               │   (Any cloud, any distribution)│
               └────────────────────────────────┘

```

## 🎯 Environment Behavior

This golden path supports different behavior per environment without forking charts.

### Dev Clusters

SUSE Security: Monitor mode

Lower resource consumption

Short observability retention

No external ingress

### Prod Clusters

SUSE Security: Enforce mode

HA controllers and receivers

Longer data retention

External ingress enabled

Capability	Dev	Prod
Security mode	Monitor	Enforce
Controllers	1	3 (HA)
Observability retention	3 days	30 days
GitOps enforcement	✅	✅

---

## 🏷️ Cluster Targeting

Fleet applies configurations based on cluster labels.

Required labels:

env=dev   # Development clusters
env=prod  # Production clusters


Optional labels (for canary testing):

canary=true

---

## 🔄 Version Management Strategy

* A single Helm chart is used for all environments

* SUSE Security versions are controlled via Helm values

* Dev clusters may run newer or pre-release versions

* Prod clusters are pinned to approved versions

* Promotion happens through Git pull requests

This provides:

* Safe validation in dev

* Predictable behavior in prod

* Full audit history

---

## 🛡️ Security Model

* Privileged components are deployed intentionally (NeuVector design)

* Admission control is environment-specific

* All policy changes are Git-reviewed

* No manual changes are allowed in-cluster

---

## 📊 Observability Model

* Full cluster topology is collected automatically

* Security and platform events are correlated

* Changes are tracked and attributed

* Multi-cluster visibility is supported

---

## 📦 Installation

Add this repository in Rancher:

Continuous Delivery → Git Repositories

Point to the repository URL

Select branch (e.g. main)

Deploy

Clusters matching the label selectors will be reconciled automatically.

---

## 🧪 Rollback & Recovery

* Rollbacks are performed via Git revert

* Fleet will automatically reconcile clusters

* No manual Helm operations are required

---

## 🧠 Design Principles

* One repo per platform capability

* One chart per product

* Values control intent, not structure

* Git is the source of truth

* Fleet is the execution engine
