# Guide d'Utilisation - Cursor Configuration Templates

Ce guide détaille comment utiliser ce dépôt de configurations Cursor dans vos projets.

## 📦 Installation Rapide

### Option 1 : Copie Manuelle

1. Clonez ou téléchargez ce dépôt
2. Copiez les fichiers nécessaires dans votre projet :

```bash
# Fichiers de base (obligatoires)
cp .cursorrules /chemin/vers/votre/projet/
cp .cursorignore /chemin/vers/votre/projet/
cp .cursorindexignore /chemin/vers/votre/projet/

# Créer le dossier pour les règles modulaires
mkdir -p /chemin/vers/votre/projet/.cursor/rules

# Copier les règles selon votre stack
cp .cursor/rules/typescript.mdc /chemin/vers/votre/projet/.cursor/rules/
cp .cursor/rules/react-nextjs.mdc /chemin/vers/votre/projet/.cursor/rules/
# ... etc
```

### Option 2 : Script d'Installation (à créer)

Vous pouvez créer un script shell pour automatiser l'installation :

```bash
#!/bin/bash
# install-cursor-config.sh

PROJECT_PATH=$1

if [ -z "$PROJECT_PATH" ]; then
    echo "Usage: ./install-cursor-config.sh /chemin/vers/projet"
    exit 1
fi

# Copier les fichiers de base
cp .cursorrules "$PROJECT_PATH/"
cp .cursorignore "$PROJECT_PATH/"
cp .cursorindexignore "$PROJECT_PATH/"

# Créer la structure
mkdir -p "$PROJECT_PATH/.cursor/rules"
mkdir -p "$PROJECT_PATH/.cursor/docs"

echo "Configuration Cursor installée dans $PROJECT_PATH"
```

## 🎯 Personnalisation

### 1. Adapter le fichier `.cursorrules`

Le fichier `.cursorrules` principal doit être adapté à votre contexte :

1. **Modifier le Persona** : Ajustez le rôle selon votre expertise

   ```markdown
   Tu es un Ingénieur Senior Full-Stack, spécialisé en [votre domaine]
   ```

2. **Ajouter des règles spécifiques au projet** :

   - Conventions de nommage spécifiques
   - Patterns architecturaux utilisés
   - Outils et bibliothèques spécifiques

3. **Référencer les règles modulaires activées** :
   ```markdown
   Les règles suivantes sont disponibles dans `.cursor/rules/` :

   - `typescript.mdc` - Règles TypeScript strictes
   - `react-nextjs.mdc` - React 19 + Next.js 15
   ```

### 2. Sélectionner les Règles Modulaires

Copiez uniquement les règles pertinentes pour votre stack :

- **Frontend TypeScript/React** : `typescript.mdc` + `react-nextjs.mdc` + `components.mdc`
- **Backend Python/FastAPI** : `python.mdc` + `fastapi.mdc`
- **Tests** : `tests.mdc` (applicable à tous les projets)

### 3. Créer un fichier PROJECT.md

Copiez le template et personnalisez-le :

```bash
cp .cursor/docs/PROJECT.md.template /chemin/vers/votre/projet/PROJECT.md
```

Puis remplissez les sections :

- Vue d'ensemble architecturale
- Glossaire métier
- État du projet
- Points d'attention

## 🔧 Activation des Règles

### Activation Automatique

Les règles avec un **Scope** défini s'activent automatiquement :

```markdown
**Scope**: `**/*.ts`, `**/*.tsx`
```

Quand vous travaillez sur un fichier `.ts` ou `.tsx`, la règle `typescript.mdc` sera automatiquement chargée.

### Activation Manuelle

Pour activer une règle manuellement dans le chat Cursor :

```
@typescript Explique-moi cette fonction
```

Ou pour une règle sans scope :

```
@nom-regle Analyse ce code
```

## 📝 Workflow Recommandé

### Pour un Nouveau Projet

1. **Initialisation** :

   ```bash
   # Installer la configuration de base
   cp .cursorrules .cursorignore .cursorindexignore /nouveau-projet/
   ```

2. **Sélection des règles** :

   ```bash
   # Créer le dossier
   mkdir -p .cursor/rules

   # Copier les règles pertinentes
   cp cursor-configs/.cursor/rules/typescript.mdc .cursor/rules/
   cp cursor-configs/.cursor/rules/react-nextjs.mdc .cursor/rules/
   ```

3. **Personnalisation** :

   - Modifier `.cursorrules` avec le contexte du projet
   - Créer `PROJECT.md` avec l'architecture
   - Adapter `.cursorignore` si nécessaire

4. **Versionner** :
   ```bash
   git add .cursorrules .cursorignore .cursorindexignore .cursor/
   git commit -m "Add Cursor configuration"
   ```

### Pour un Projet Existant

1. **Audit** : Vérifier s'il existe déjà des configurations Cursor
2. **Migration** : Fusionner les règles existantes avec les nouvelles
3. **Test** : Tester avec quelques prompts pour valider le comportement
4. **Itération** : Ajuster les règles selon les besoins

## 🎨 Exemples d'Utilisation

### Exemple 1 : Créer un Composant React

Avec les règles `react-nextjs.mdc` et `components.mdc` activées :

```
Crée un composant Button réutilisable avec les variants primary, secondary, et danger.
Utilise Zod pour valider les props et Tailwind avec cn().
```

L'IA générera automatiquement :

- Un Server Component par défaut (ou Client Component si nécessaire)
- Validation Zod des props
- Classes Tailwind organisées avec `cn()`
- Accessibilité (a11y) intégrée

### Exemple 2 : Créer un Endpoint FastAPI

Avec les règles `python.mdc` et `fastapi.mdc` activées :

```
Crée un endpoint POST /users qui accepte un email et un nom.
Utilise Pydantic v2 pour la validation.
```

L'IA générera automatiquement :

- Modèles Pydantic v2 avec `Field()` et validations
- Endpoint async avec gestion d'erreurs
- Pattern RORO pour la scalabilité

## 🔍 Dépannage

### Les règles ne s'activent pas

1. Vérifier que le fichier `.mdc` est dans `.cursor/rules/`
2. Vérifier que le scope correspond aux fichiers travaillés
3. Redémarrer Cursor si nécessaire

### Trop de règles chargées

Si le contexte devient trop lourd :

- Réduire le nombre de règles modulaires
- Utiliser des scopes plus spécifiques
- Déplacer certaines règles vers l'activation manuelle

### Conflits entre règles

Si deux règles se contredisent :

- La règle la plus spécifique (scope plus étroit) prend le dessus
- Modifier les règles pour résoudre les conflits
- Utiliser l'activation manuelle pour les cas spéciaux

## 📚 Ressources

- [Documentation Cursor](https://cursor.sh/docs)
- [Awesome CursorRules](https://github.com/jxnl/cursorrules) - Exemples de règles communautaires

## 🤝 Contribution

Pour améliorer ce dépôt de configurations :

1. Tester les règles sur vos projets
2. Identifier les patterns manquants
3. Proposer des améliorations via des issues ou PRs

## 📄 Licence

[À définir selon vos préférences]
