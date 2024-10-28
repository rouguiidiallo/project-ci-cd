# project-ci-cd

# CI/CD Pipeline Documentation

Ce dépôt utilise GitHub Actions pour automatiser un pipeline CI/CD avec les étapes de **build**, **test** et **déploiement**. Voici un aperçu des étapes et de leurs fonctions.

## Pipeline YAML : `.github/workflows/ci.yml`

### Étapes du Pipeline

1. **Build** :
   - **Environnement** : Exécution dans un conteneur Docker avec une image `node:16`.
   - **Actions** :
     - **Checkout repository** : Récupère le code source.
     - **Cache CHANGELOG.md** : Stocke `CHANGELOG.md` pour réutilisation.
     - **Build application** : Simule la construction de l’application.

2. **Test** :
   - **Environnement** : Exécution sur un environnement Ubuntu.
   - **Conditions** : Le job de test dépend du job `build` et commence une fois que celui-ci est terminé.
   - **Actions** :
     - **Checkout repository** : Récupère le code source.
     - **Restore CHANGELOG.md cache** : Utilise le cache de `CHANGELOG.md` depuis `build`.
     - **Run tests** : Simule l’exécution de tests.

3. **Deploy** :
   - **Environnement** : Exécution sur un environnement Ubuntu.
   - **Conditions** : Le job de déploiement dépend du job `test`.
   - **Actions** :
     - **Checkout repository** : Récupère le code source.
     - **Restore CHANGELOG.md cache** : Utilise le cache de `CHANGELOG.md`.
     - **Deploy application** : Simule un déploiement en utilisant une variable d'environnement.

### Variables d'Environnement

- `MY_VARIABLE` : Utilisée dans l'étape de déploiement pour personnaliser la commande simulée de déploiement.

### Caches et Artefacts

- **Cache de `CHANGELOG.md`** : Le cache permet de stocker le fichier `CHANGELOG.md` entre les étapes du pipeline pour gagner en efficacité et éviter une reconstruction inutile.
