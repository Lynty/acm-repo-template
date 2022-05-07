# Configuring namespace specific policies

With this SADA opinionated ACM repository, we can configure multi-environment, multi-cluster, and multi-tenancy. For multi-tenancy, the namespaces used by different teams should have different policies according to the best practices for multi-tenancy.

- **[automated rendering](automated-rendering/README.md)**:
  Config Sync supports rendering Kustomize configurations in version 1.9.0 or later.
  You can check in the Kustomize configurations to your Git repository,
  and Config Sync will render and sync them to your clusters.

## Source Kustomize configurations

The directory `configsync-src` contains the configuration in Kustomize format. Each cluster uses `./cs/<ENV>/<CLUSTER_NAME>` as its Config Sync policy directory.

The folder directory: 
```
.
├── README.md
├── cs
│   └── dev
│       ├── cluster-1-dev
│       │   ├── dev -> ../../../cs-src/dev
│       │   └── kustomization.yaml
│       └── cluster-2-dev
│           ├── dev -> ../../../cs-src/dev
│           └── kustomization.yaml
└── cs-src
    └── dev
        ├── all-clusters
        │   ├── kustomization.yaml # updates to all clusters
        │   ├── pod.yaml
        │   ├── team-a
        │   │   └── kustomization.yaml # updates to all team-a namespaces
        │   └── team-b
        │       ├── kustomization.yaml # updates to all team-b namespaces
        │       └── nginx_web_deployment.yaml
        ├── cluster-1-dev
        │   ├── base
        │   │   ├── kustomization.yaml # updates to all namespaces in cluster-1-dev
        │   │   ├── namespace.yaml
        │   │   └── role.yaml
        │   ├── team-a
        │   │   └── kustomization.yaml # updates to team-a namespace in cluster-1-dev
        │   └── team-b
        │       └── kustomization.yaml # updates to team-b namespace in cluster-1-dev
        ├── cluster-2-dev
        │   ├── base
        │   │   ├── kustomization.yaml # updates to all namespaces in cluster-2-dev
        │   │   ├── namespace.yaml
        │   │   └── role.yaml
        │   └── team-b
        │       └── kustomization.yaml # updates to team-b namespace in cluster-2-dev
        └── security
            ├── constraint-templates
            │   ├── k8srestrictnamespaces.yaml
            │   └── kustomization.yaml
            ├── constraints
            │   ├── K8sRestrictNamespaces.yaml
            │   └── kustomization.yaml
            └── kustomization.yaml
```
