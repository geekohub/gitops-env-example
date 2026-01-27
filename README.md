┌─── gitops-env-example┌────────┐
│        Platform Team          │
│   (Defines Golden Path)       │
└──────────────┬───────────────┘
               │ Git (Fleet)
               ▼
┌──────────────────────────────────────────┐
│        Rancher Fleet (GitOps)            │
│  - Environment targeting (dev / prod)    │
│  - Drift detection & auto-heal           │
│  - Auditable change history              │
└──────────────┬───────────────┬───────────┘
               │               │
               ▼               ▼
┌──────────────────────┐   ┌────────────────────────┐
│   SUSE Security      │   │   SUSE Observability   │
│   (NeuVector)        │   │   (StackState)         │
│                      │   │                        │
│ • Image scanning     │   │ • Topology mapping     │
│ • Runtime protection │   │ • Change intelligence  │
│ • Admission control  │   │ • Events & SLOs        │
│ • Policy enforcement │   │ • Root cause analysis  │
└───────────┬──────────┘   └───────────┬────────────┘
            │                          │
            └───────────┬──────────────┘
                        ▼
            ┌──────────────────────────┐
            │   Kubernetes Cluster     │
            │  (Any distro, any cloud) │
            └──────────────────────────┘
