# Leçon 6 — Les Pull Requests (PR)

La Pull Request est le **cœur de la collaboration moderne** sur GitHub. C'est ce qui
distingue « utiliser Git tout seul » de « travailler comme une équipe pro ».

## 🎯 C'est quoi une Pull Request ?

Une PR est une **demande de fusion** que tu fais **sur GitHub** (pas en ligne de
commande). Tu dis : *« Voici les changements sur ma branche, je propose de les
fusionner dans `master` »*.

La PR ouvre un espace pour :
- **relire** le code (le tien ou celui d'un collègue),
- **discuter**, commenter ligne par ligne,
- **valider**, puis seulement **fusionner**.

> 🧠 **Analogie** : une PR, c'est une **porte avec un vigile**. 🛡️ Personne n'entre
> dans `master` sans passer le contrôle. Ça protège la branche principale.

## 🤝 Pourquoi s'imposer ça plutôt que merger direct ?

En entreprise, **personne ne merge directement sur `master`**. Tout passe par une PR
relue par quelqu'un d'autre. Raisons :

1. **Revue de code** : un second regard repère les bugs avant qu'ils n'entrent.
2. **Qualité** : on discute des choix techniques avant de figer.
3. **Montée en compétence** : toute l'équipe apprend en lisant le code des autres.
4. **Traçabilité** : chaque changement a une discussion archivée.

## 🔄 Le cycle complet d'une PR

```
   LOCAL                          GITHUB
   ┌─────────────────┐
   │ git switch -c   │  branche de travail
   │ (modifs+commit) │
   │ git push -u     │ ──────►   La branche apparaît sur GitHub
   └─────────────────┘
                                 ┌─────────────────────────┐
                                 │ "Compare & pull request"│
                                 │ → titre + description    │
                                 │ → relire "Files changed" │
                                 │ → Merge pull request     │
                                 └─────────────────────────┘
   ┌─────────────────┐                      │
   │ git switch master│ ◄────────────────────┘
   │ git pull         │  ← ÉTAPE CLÉ : récupère le merge fait en ligne
   │ git branch -d    │  ← nettoyage de la branche
   └─────────────────┘
```

## ⚠️ Le piège à ne pas oublier

La fusion d'une PR se fait **sur GitHub** (en ligne). Donc juste après, ton dépôt
**local est en retard** d'un commit (le commit de merge). Tu **dois** faire :

```
git switch master
git pull
```

Beaucoup de débutants oublient ce `git pull` et se retrouvent désynchronisés.

## 💡 Tips du mentor

- **Titre + description clairs** : explique *quoi* et *pourquoi*, pas juste « update ».
- **Prends 10 secondes pour relire « Files changed »** avant de merger, même seul. C'est le réflexe pro.
- **Petites PR > grosses PR.** Une PR qui change 3 000 lignes est impossible à relire correctement.
- Même en solo, t'entraîner aux PR vaut le coup : c'est exactement ce qu'on te demandera en équipe.

## ✅ Ce qu'il faut retenir

PR = proposer un merge sur GitHub, le faire relire, fusionner, puis `git pull` en local.

⬅️ Retour au [sommaire des cours](README.md)
