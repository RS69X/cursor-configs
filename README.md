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
│   │   ├── typescript.mdc
│   │   ├── python.mdc
│   │   ├── react-nextjs.mdc
│   │   ├── fastapi.mdc
│   │   ├── tests.mdc
│   │   └── components.mdc
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
   cp .cursor/rules/typescript.mdc /chemin/vers/votre/projet/.cursor/rules/
   # Répéter pour chaque règle nécessaire
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

### Par Stack Technologique

- `typescript.mdc` - Règles TypeScript strictes
- `python.mdc` - Règles Python avec type hints
- `react-nextjs.mdc` - React 19 + Next.js 15 App Router
- `fastapi.mdc` - FastAPI avec Pydantic v2

### Par Type de Fichier

- `tests.mdc` - Conventions pour les tests
- `components.mdc` - Patterns pour les composants UI

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
