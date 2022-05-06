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
├── cs
│   └── dev
│       └── cluster-1-dev
│           └── dev -> ../../../cs-src/dev
└── cs-src
    └── dev
        ├── all-clusters
        ├── cluster-1-dev
        │   ├── base
        │   └── team-a
        └── security
            ├── constraint-templates
            └── constraints
```
