# Cursor Configuration Templates

Dépôt de configurations modulaires et réutilisables pour Cursor, suivant la philosophie "Configuration as Code".

## 📋 Structure

```
.
├── .cursorrules              # Règles globales (point d'entrée principal)
├── .cursorignore             # Exclusion totale (sécurité)
├── .cursorindexignore        # Exclusion de l'indexation (optimisation)
├── .cursor/
│   ├── rules/                # Règles modulaires scopées (.mdc)
│   │   ├── argocd-core.mdc
│   │   ├── kubernetes-resources.mdc
│   │   ├── kubernetes-security.mdc
│   │   ├── environments-infrastructure.mdc
│   │   ├── secrets-vault.mdc
│   │   ├── operations.mdc
│   │   ├── databases-storage.mdc
│   │   └── ci-cd-pipelines.mdc
│   └── docs/                 # Documentation pour l'IA (optionnel)
│       └── PROJECT.md.template
└── README.md
```

## 🚀 Utilisation

### Installation dans un nouveau projet

1. **Copier les fichiers de base** :

   ```bash
   cp .cursorrules .cursorignore .cursorindexignore /chemin/vers/votre/projet/
   ```

2. **Copier les règles modulaires nécessaires** :

   ```bash
   mkdir -p .cursor/rules
   cp .cursor/rules/argocd-core.mdc /chemin/vers/votre/projet/.cursor/rules/
   # Répéter pour chaque règle nécessaire (kubernetes-resources.mdc, etc.)
   ```

3. **Adapter le fichier `.cursorrules`** :
   - Modifier le persona selon votre contexte
   - Ajouter les références aux règles modulaires activées
   - Personnaliser les contraintes spécifiques au projet

### Activation des règles modulaires

Les règles dans `.cursor/rules/` peuvent être activées de plusieurs façons :

- **Automatique** : Via les patterns glob dans le fichier de règle (ex: `**/*.ts`)
- **Manuelle** : En référençant `@nom-regle` dans le chat Cursor

## 📚 Règles Disponibles

### Infrastructure et DevOps (ArgoCD & Kubernetes)

Les règles Kubernetes et ArgoCD sont organisées en modules spécialisés pour une meilleure maintenabilité :

- `argocd-core.mdc` - Fonctionnalités ArgoCD (ApplicationSets, Projects, RBAC, Notifications, CLI, Sync Waves, Hooks, Rollouts)
- `kubernetes-resources.mdc` - Ressources Kubernetes (Deployments, StatefulSets, Jobs, CronJobs, Init Containers, Persistent Volumes, HPA, Ingress)
- `kubernetes-security.mdc` - Sécurité Kubernetes (NetworkPolicies, PodSecurityStandards, RBAC, Admission Controllers, Image Security)
- `environments-infrastructure.mdc` - Environnements (dev/test/prod) et infrastructure (MetalLB, Cloudflare, Node Management)
- `secrets-vault.mdc` - Gestion des secrets (Vault, External Secrets Operator, Sealed Secrets, Dynamic Secrets)
- `operations.mdc` - Opérations (Monitoring, Logging, Backup, Troubleshooting, Helm, Kustomize, Compliance)
- `databases-storage.mdc` - Bases de données et storage (PostgreSQL, MySQL, MongoDB, Redis, Persistent Volumes, StorageClasses)
- `ci-cd-pipelines.mdc` - Pipelines CI/CD (GitOps workflows, Docker builds, déploiements automatisés)

## 🔧 Personnalisation

Chaque fichier de règle suit la hiérarchie d'instruction recommandée :

1. **Persona** - Définition du rôle expert
2. **Contexte Technique** - Stack précise avec versions
3. **Contraintes Négatives** - Ce qu'il ne faut pas faire
4. **Exemples Few-Shot** - Patterns et anti-patterns

## 🔒 Sécurité

- Les fichiers `.cursorignore` excluent les secrets et données sensibles
- Le mode Privacy de Cursor doit être activé pour les projets sensibles
- Ne jamais commiter de secrets dans les fichiers de configuration
