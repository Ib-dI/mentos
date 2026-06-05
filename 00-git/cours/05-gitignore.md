# Leçon 5 — Le fichier .gitignore

Tous les fichiers d'un projet ne doivent **pas** être suivis par Git. Le fichier
`.gitignore` est la liste de ceux que Git doit **ignorer complètement**.

## 🤔 Pourquoi ignorer des fichiers ?

Trois grandes catégories de fichiers à ignorer :

1. **Les dépendances téléchargées** — ex. le dossier `node_modules/` (au Module 1).
   Il peut peser des **centaines de Mo** et se régénère tout seul. On ne le versionne jamais.
2. **Les secrets** — fichiers `.env` contenant mots de passe et clés API. ☠️ **Jamais** sur GitHub.
3. **Les fichiers temporaires / système** — logs (`*.log`), fichiers d'OS (`.DS_Store`), caches.

## 🔧 Comment ça marche

Tu crées un fichier nommé **exactement** `.gitignore` (avec le point au début) à la
racine du projet, et tu y mets une règle par ligne :

```
node_modules/      # ignore tout le dossier node_modules
.env               # ignore ce fichier précis
*.log              # ignore TOUT fichier finissant par .log
.DS_Store          # fichier système macOS
```

| Syntaxe | Signification |
|---------|---------------|
| `nom.txt` | ignore le fichier `nom.txt` |
| `dossier/` | ignore tout le dossier `dossier` |
| `*.log` | le `*` est un joker : ignore tout nom finissant par `.log` |
| `!important.log` | le `!` fait une **exception** : ne pas ignorer celui-là |

## 🧪 Vérifier que ça marche

Crée un fichier `test.log`, puis :
```
git status
```
`test.log` ne doit **pas** apparaître : il est ignoré. ✅

## 😏 Le piège classique

> **Pourquoi `.gitignore` lui-même apparaît dans `git status` ?**
>
> Parce que `.gitignore` n'ignore pas **lui-même** — il liste les **autres** fichiers
> à ignorer. C'est un fichier de configuration normal qu'on **veut** versionner et
> partager, pour que toute l'équipe ignore les mêmes choses. Un fichier qui décrit
> l'invisible, mais qui reste visible. 🧙

## 🔒 Le point sécurité (important !)

Des développeurs débutants poussent leur `.env` sur GitHub **par accident chaque jour**,
et des bots automatisés volent leurs clés en quelques minutes. La règle d'or :

> **Un secret ne va JAMAIS sur GitHub.** `.gitignore` est ta première ligne de défense.

⚠️ Attention : `.gitignore` n'agit que sur les fichiers **pas encore suivis**. Si tu as
déjà committé un secret par erreur, l'ajouter au `.gitignore` ne suffit pas — il reste
dans l'historique. Il faut alors le retirer du suivi *et* changer le secret.

## ✅ Ce qu'il faut retenir

`.gitignore` = la liste des fichiers que Git doit oublier. Dépendances, secrets, temporaires.

➡️ Suite : [Leçon 6 — Les Pull Requests](06-pull-requests.md)
