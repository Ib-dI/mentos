# Leçon 8 — Les conflits de fusion

Le conflit fait peur aux débutants. Pourtant, **ce n'est ni une erreur ni une
catastrophe** : c'est Git qui te demande poliment de l'aider à choisir.

## 🤔 C'est quoi un conflit ?

Un conflit de fusion survient quand **deux branches modifient la même ligne du même
fichier différemment**, et qu'on essaie de les fusionner. Git sait fusionner tout seul
des changements sur des lignes/fichiers différents — mais sur **la même ligne**, il ne
peut pas deviner laquelle garder. Il s'arrête et te passe la main.

```
master:   ...A───B (rouge)──┐
                 \          │ merge → 💥 CONFLIT (même ligne, valeurs différentes)
branche:          C (bleu)──┘
```

## 🧭 Lire les marqueurs de conflit

Quand un conflit éclate, Git **modifie le fichier** et y insère des marqueurs :

```
<<<<<<< HEAD
Couleur préférée : rouge
=======
Couleur préférée : bleu
>>>>>>> couleur-bleu
```

| Marqueur | Signification |
|----------|---------------|
| `<<<<<<< HEAD` | Début de **ta** version (branche actuelle) |
| `=======` | La frontière entre les deux versions |
| `>>>>>>> couleur-bleu` | Fin de la version de **l'autre** branche |

## 🔧 Résoudre un conflit, étape par étape

1. `git merge autre-branche` → Git annonce `CONFLICT`.
2. `git status` → te dit **quels fichiers** sont en conflit.
3. Ouvre chaque fichier concerné. Décide quoi garder :
   - ta version, OU
   - l'autre version, OU
   - un mélange / une nouvelle ligne.
4. **Supprime les 3 lignes de marqueurs** (`<<<<<<<`, `=======`, `>>>>>>>`). Il ne doit
   rester que le contenu propre que tu veux.
5. `git add <fichier>` → ça signifie à Git « ce fichier est résolu ».
6. `git commit` → Git propose un message de merge tout prêt, valide-le.

## ⚠️ Le piège n°1 du débutant

**Oublier de supprimer un marqueur**, puis committer un fichier qui contient encore
`<<<<<<<` ou `=======`. Le fichier reste cassé et le bug part en production.

> ✅ **Réflexe de sécurité** : avant le `git add`, relis le fichier (ou fais `git diff`)
> et assure-toi qu'il reste **zéro marqueur**. Cherche `<<<<<<<` partout.

## 🛡️ Comment limiter les conflits ?

On ne les supprime jamais à 100 %, mais on réduit beaucoup leur fréquence :

1. **Petites branches, fusionnées souvent** — moins une branche diverge longtemps, moins ça risque.
2. **`git pull` régulièrement** — reste à jour avec le travail des autres.
3. **Bien découper le code** — chacun sur des fichiers/zones différents.
4. **Communiquer** — « je touche au fichier X » évite les réécritures parallèles.

## 💡 Tips du mentor

- Un conflit **n'est pas ta faute** ni un signe que tu as mal fait. C'est la vie normale d'un projet à plusieurs.
- En cas de panique totale pendant un merge, tu peux **tout annuler** et repartir propre : `git merge --abort`.
- Beaucoup d'éditeurs (VS Code) colorent les conflits et proposent des boutons « Accept Current / Incoming / Both ». Pratique, mais comprends d'abord la version manuelle.

## ✅ Ce qu'il faut retenir

Conflit = Git te demande de choisir entre deux versions d'une même ligne. Tu édites,
tu enlèves les marqueurs, `git add`, `git commit`. Calme et méthode. ⚔️

⬅️ Retour au [sommaire des cours](README.md)
