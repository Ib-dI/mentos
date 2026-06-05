# Leçon 7 — Inspecter et annuler des changements

Savoir **avancer** avec Git, c'est bien. Savoir **regarder ce qu'on a fait** et
**revenir en arrière**, c'est ce qui te sauve le jour où tu casses quelque chose.

## 🔍 Inspecter : qu'est-ce qui a changé ?

### `git diff` — voir les modifications non encore ajoutées
```
git diff
```
Affiche, ligne par ligne, ce que tu as modifié dans le **répertoire de travail** mais
pas encore mis en zone de transit. Les lignes **vertes** (`+`) sont ajoutées, les
**rouges** (`-`) supprimées.

```
git diff --staged
```
La variante : montre ce qui est **déjà dans la zone de transit** (après un `git add`).

> 🧠 Réflexe : **toujours `git diff` avant de `git add`** pour relire ce que tu vas committer.

### `git log` — explorer l'historique
```
git log                       # complet, avec auteur, date, message
git log --oneline             # condensé, une ligne par commit
git log --oneline --graph     # + représentation visuelle des branches/merges
```

Le `--graph` dessine les fusions :
```
*   a371dd0 Merge pull request #1
|\
| * 79d0ff1 Création de notre journal
|/
* 37cbdab Ajout du programme détaillé
```

## ↩️ Annuler : revenir en arrière

On distingue **où** se trouve ce qu'on veut annuler — encore nos 3 zones (Leçon 2) !

### Annuler une modif dans le répertoire de travail
```
git restore mon-fichier.md
```
Le fichier revient à son **dernier état committé**. Tes modifications non sauvegardées
sont **jetées**.

> ⚠️ **DANGER** : c'est **irréversible**. Ce que tu n'avais pas committé est perdu pour
> de bon. Vérifie **toujours** avec `git diff` avant de restaurer.

### Sortir un fichier de la zone de transit (annuler un `git add`)
```
git restore --staged mon-fichier.md
```
Le fichier sort de la salle d'attente, **mais ta modification reste** dans le répertoire
de travail. Tu n'as rien perdu, tu as juste « dé-stagé ».

### Tableau récap

| Situation | Commande | Effet |
|-----------|----------|-------|
| J'ai modifié, pas encore `add` → je veux annuler | `git restore <fichier>` | jette la modif (⚠️ irréversible) |
| J'ai fait `git add` → je veux le retirer du staging | `git restore --staged <fichier>` | dé-stage, garde la modif |
| Je veux juste **voir** ce que j'ai changé | `git diff` | affiche les différences |

## 🆚 `restore` vs `revert` (à ne pas confondre)

- **`git restore`** : annule des changements **non committés** (dans le travail / staging).
- **`git revert <commit>`** : annule un commit **déjà enregistré** en créant un **nouveau
  commit** qui fait l'inverse. L'historique est préservé (on ne réécrit rien). On le
  verra en exercice.

## 💡 Tips du mentor

- `git diff` est gratuit et sans danger : utilise-le sans modération.
- Avant tout `git restore`, demande-toi : *« suis-je sûr de vouloir perdre ça ? »*
- Tant qu'un travail n'est pas committé, Git ne peut pas toujours te le rendre. **Committe tôt, committe souvent.**

## ✅ Ce qu'il faut retenir

`diff` pour regarder, `restore` pour annuler le non-committé, `restore --staged` pour
dé-stager. Et on retrouve **toujours** les 3 zones. 🔗

⬅️ Retour au [sommaire des cours](README.md)
