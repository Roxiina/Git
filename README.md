# 🧭 Sujet de veille : Les Workflows Git, Pull Requests et CI/CD

## 🎯 Objectif

Comprendre comment les **workflows Git** organisent le travail collaboratif dans les projets de développement, et comment les **Pull Requests** et le **CI/CD** assurent la **qualité**, la **fiabilité** et la **livraison continue** du code.

---

## 🧩 1. Les principaux Workflows Git

Git permet de gérer différentes façons de collaborer sur un projet.  
Chaque équipe choisit le workflow adapté à sa taille et à son rythme de développement.

---

### 🧱 a) Workflow de branches (Feature Branch Workflow)

**Principe :**  
Chaque nouvelle fonctionnalité est développée dans une **branche distincte** à partir de la branche principale (`main` ou `develop`).

**Étapes typiques :**
```bash
# 1. Se placer sur la branche principale
git checkout main

# 2. Mettre à jour la branche principale
git pull origin main

# 3. Créer une nouvelle branche
git checkout -b feature/nouvelle-fonctionnalite

# 4. Ajouter et valider les changements
git add .
git commit -m "Ajout de la nouvelle fonctionnalité"

# 5. Envoyer la branche sur le dépôt distant
git push origin feature/nouvelle-fonctionnalite
```
---

## Avantages :
- Organisation claire des tâches.
- Permet la revue de code.

## Inconvénients :
- Peut ralentir si beaucoup de branches ouvertes en parallèle.

---

## 🧭 b) Git Flow

**Principe :**
Workflow complet basé sur plusieurs branches permanentes :
- main → code en production
- develop → code de développement
- feature/* → nouvelles fonctionnalités
- release/* → préparation de version
- hotfix/* → correction d’urgence

**Commandes typiques :**
```bash
# Initialiser Git Flow
git flow init

# Créer une nouvelle feature
git flow feature start nom-feature

# Terminer la feature (fusionne dans develop)
git flow feature finish nom-feature

# Créer une release
git flow release start 1.0.0
git flow release finish 1.0.0
```

---

## Avantages :
- Très structuré, adapté aux cycles de release longs.
- Idéal pour des équipes nombreuses.

## Inconvénients :
- Complexe à gérer pour des projets rapides ou CI/CD.

---

## 🌳 c) Trunk Based Development

**Principe :**
- Tout le monde travaille sur une seule branche (main ou trunk).
- Les branches sont courtes et fusionnées très vite.
- Tests automatiques obligatoires avant fusion.

**Avantages :**
- Intégration continue fluide.
- Compatible avec CI/CD.

**Inconvénients :**
- Nécessite une grande discipline et des tests solides.

---

## 🔄 d) Workflow de Fork

**Principe :**
Chaque contributeur forke (duplique) le dépôt principal sur son propre compte, travaille dessus, puis propose une Pull Request vers le dépôt d’origine.

**Commandes typiques :**
```bash
# Cloner le fork
git clone https://github.com/mon-compte/nom-du-projet.git

# Ajouter le dépôt principal comme "upstream"
git remote add upstream https://github.com/original/nom-du-projet.git

# Synchroniser son fork
git fetch upstream
git merge upstream/main
```

---

## Avantages :
- Idéal pour projets open-source.
- Sécurisé : pas d’accès direct au dépôt principal.

---

## Inconvénients :
- Moins fluide pour les équipes internes.

---

## 💬 2. Les Pull Requests (PR)
Une Pull Request (PR) est une demande de fusion de code vers la branche principale.

## 🔧 Étapes d’une PR

**Tu pushes ta branche sur le dépôt distant :**
- git push origin feature/nouvelle-fonctionnalite
- Sur GitHub ou GitLab → cliquer sur “New Pull Request”.

**Rédiger un titre et une description claire :**
- Ce que fait la modification
- Pourquoi elle est utile
- Comment la tester
- Un collègue relit et commente ton code.
- Une fois validée → fusion dans main.
- GitHub peut ensuite lancer un pipeline CI/CD.

---

## ✅ Bonnes pratiques
- Une PR = une seule fonctionnalité.
- Rédiger des messages de commit clairs.
- Exiger au moins une review avant fusion.
- Automatiser les tests et le linting sur les PR.

---

## ⚙️ 3. Le CI/CD (Intégration Continue / Déploiement Continu)
## 🔁 CI – Continuous Integration
À chaque commit ou PR, les tests sont lancés automatiquement.
Le code doit être toujours intégrable et fonctionnel.

**Exemple avec GitHub Actions :**
```bash
name: CI
on: [push, pull_request]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Installer Python
        uses: actions/setup-python@v4
        with:
          python-version: 3.10
      - name: Installer les dépendances
        run: pip install -r requirements.txt
      - name: Lancer les tests
        run: pytest
```
---

## 🚀 CD – Continuous Delivery / Deployment
Automatisation du déploiement après succès des tests.

**Peut être :**
- Continuous Delivery → déploiement prêt mais manuel.
- Continuous Deployment → déploiement automatique après validation.

**Exemples d’outils :**

| 🧰 **Outil** | ⚙️ **Fonction principale** |
|---------------|----------------------------|
| **GitHub Actions** | Automatisation CI/CD intégrée à GitHub |
| **GitLab CI/CD** | Pipelines puissants et simples à configurer |
| **Jenkins** | Serveur open-source pour automatiser builds/tests |
| **Azure DevOps** | Pipelines professionnels intégrés à Azure |
| **CircleCI / Travis CI** | Automatisation cloud simple et rapide |


---
## 🎯 Enjeux
- Qualité du code : revues + tests automatisés.
- Fiabilité : éviter les régressions.
- Collaboration efficace : chacun travaille sans bloquer les autres.
- Livraison rapide : moins d’attente entre le code et la production.

---

## 🔍 Pistes de recherche
- Étudier un pipeline complet CI/CD sur GitHub Actions.
- Comparer Git Flow vs Trunk Based Development.
- Lire la documentation officielle de GitLab CI/CD.
- Tester une Pull Request réelle sur un dépôt d’exercice.

--- 

## 📘 Ressources utiles

- [📖 Git - Documentation officielle](https://git-scm.com/docs)
- [🐙 GitHub Docs - Pull Requests](https://docs.github.com/fr/pull-requests)
- [🧰 GitLab CI/CD Guide](https://docs.gitlab.com/ci//)
- [🚀 Trunk Based Development](https://trunkbaseddevelopment.com/)

---