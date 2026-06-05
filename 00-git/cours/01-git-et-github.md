# Leçon 1 — Git et GitHub, c'est quoi ?

## 🎯 L'idée en une phrase

**Git** est un outil qui sauvegarde l'historique de ton projet.
**GitHub** est un site web où tu héberges tes projets Git pour les sauvegarder en ligne et collaborer.

Ce ne sont **pas** la même chose. On peut utiliser Git sans GitHub. GitHub a juste
besoin de Git.

## 🕰️ Git : la machine à remonter le temps

Imagine que tu écris un mémoire. Tu fais des copies de sauvegarde :
`memoire.doc`, `memoire-v2.doc`, `memoire-final.doc`, `memoire-final-VRAI.doc`…
C'est le chaos. 😅

Git résout ça. Il enregistre des **photos** (on dit des *commits*) de ton projet à
des moments précis. Tu peux :

- voir **qui** a changé **quoi** et **quand**,
- revenir à n'importe quelle version passée,
- travailler à plusieurs sans s'écraser le travail.

> 🧠 **Analogie** : Git, c'est le bouton « historique » de Google Docs, mais en
> beaucoup plus puissant et que **tu** contrôles.

## ☁️ GitHub : le cloud de tes projets

GitHub est un **service en ligne** qui stocke tes dépôts Git. Il sert à :

- **sauvegarder** ton travail ailleurs que sur ton PC (si ton disque crashe, tout est sauvé),
- **partager** ton code (portfolio pour un futur emploi 👀),
- **collaborer** : plusieurs personnes travaillent sur le même projet.

> Il existe des alternatives (GitLab, Bitbucket), mais GitHub est le plus utilisé.

## 📦 Le vocabulaire de base

| Terme | Définition simple |
|-------|-------------------|
| **Dépôt** (*repository*, *repo*) | Le dossier de ton projet, suivi par Git |
| **Commit** | Une photo enregistrée de ton projet à un instant T |
| **Local** | Ce qui est sur **ton ordinateur** |
| **Distant** (*remote*) | Ce qui est sur **GitHub** |
| **Pousser** (*push*) | Envoyer tes commits du local vers GitHub |

## ✅ Ce qu'il faut retenir

1. Git = l'outil d'historique (sur ta machine).
2. GitHub = l'hébergement en ligne (le cloud).
3. On travaille en **local**, puis on **pousse** vers le **distant**.

➡️ Suite : [Leçon 2 — Le cycle de base](02-le-cycle-de-base.md)
