# Leçon 9 — Mettre de côté (`stash`) et cloner (`clone`)

Deux outils du quotidien : l'un pour **ranger ton travail en cours** quand on te
dérange, l'autre pour **copier un dépôt entier** sur ta machine.

---

## 📦 Partie A — `git stash` : la poche temporaire

### Le scénario

Tu es en plein milieu d'une modif **pas finie**. Ton lead débarque : « urgence,
corrige autre chose tout de suite ». Tu ne veux ni committer du travail à moitié fait,
ni le perdre. Solution : tu le **ranges dans une poche**, ton plan de travail
redevient propre, tu fais l'urgence, puis tu **ressors** ton travail.

### Les commandes

| Commande | À quoi ça sert |
|----------|----------------|
| `git stash` | range les modifs **suivies** (tracked) et nettoie le dossier |
| `git stash -u` | …**+ les fichiers non suivis** (nouveaux fichiers) ⚠️ |
| `git stash list` | affiche toutes tes poches |
| `git stash apply` | ressort le travail **mais garde** la poche |
| `git stash pop` | ressort le travail **et vide** la poche |
| `git stash drop` | jette **une** poche précise |
| `git stash clear` | jette **toutes** les poches (irréversible) |

### ⚠️ Piège n°1 — `stash` ignore les fichiers non suivis

Un `git stash` tout simple ne met de côté **que ce que Git suit déjà**. Si tu viens de
créer un **nouveau** fichier (jamais `git add`), il est *untracked* → `git stash` le
**laisse en place**. Beaucoup croient l'avoir rangé… et le retrouvent là.

> ✅ **Réflexe** : un nouveau fichier à ranger ? Utilise `git stash -u`
> (ou `--include-untracked`).

### ⚠️ Piège n°2 — `apply` vs `pop`

```
git stash apply   → recopie le contenu   ❌ garde la poche dans la liste
git stash pop     → recopie le contenu   ✅ supprime la poche de la liste
```

Si tu fais `apply`, ta poche **reste** dans `git stash list`. À force, tu accumules des
stashes fantômes que tu oublies. 90 % du temps, ce que tu veux c'est `pop`.

> 💡 `apply` est utile pour appliquer **le même stash sur plusieurs branches**.

### Cycle type

```bash
# je crée un nouveau fichier en cours de travail
git status              # il apparaît en "untracked"
git stash -u            # rangé dans la poche, dossier propre
git stash list          # stash@{0}: WIP on master: ...
# ... je fais mon urgence ...
git stash pop           # mon travail revient, la poche se vide
git stash list          # (vide)
```

---

## 🌍 Partie B — `git clone` : copier un dépôt

### À quoi ça sert

Un collègue te partage un dépôt (ou tu récupères un projet sur GitHub). `git clone` en
fait une **copie locale complète**.

```bash
git clone https://github.com/Ib-dI/mentos.git
# ou avec un autre nom de dossier :
git clone https://github.com/Ib-dI/mentos.git mentos-clone
```

### Ce que `clone` fait pour toi (la magie)

Contrairement à `git init` où tu configures tout à la main, `clone` ramène d'un coup :

1. **Tous les fichiers** du projet.
2. **Tout l'historique** (`.git` complet → `git log` te montre tous les commits).
3. **Le lien remote déjà configuré** sous le nom `origin`.

Quand tu fais `git log --oneline` juste après, tu vois :
```
57c3cab (HEAD -> master, origin/master, origin/HEAD) ...
```
`origin/master` est déjà là → tu peux `pull` / `push` immédiatement, rien à brancher.

### `clone` vs `init`

| | `git init` | `git clone` |
|---|---|---|
| Crée un dépôt vide | ✅ | — |
| Récupère un dépôt existant | — | ✅ |
| Historique | aucun | complet |
| Remote `origin` | à configurer à la main | déjà branché |

---

## 💡 Tips du mentor

- `git stash` est un sauveur de vie, mais c'est une poche **temporaire** : ce qu'on
  range, on le ressort vite. Ne stocke pas du travail des semaines dedans.
- Un stash n'est lié à **aucune branche** : tu peux le `pop` sur une autre branche que
  celle où tu l'as créé (très pratique « zut, je code sur la mauvaise branche »).
- Après un `clone`, fais toujours un `git log --oneline` et un `git remote -v` : tu
  vérifies que l'historique et le lien GitHub sont bien là.

## ✅ Ce qu'il faut retenir

`stash` = ranger/ressortir du travail en cours (pense `-u` pour les nouveaux fichiers,
et `pop` pour vider la poche). `clone` = copier un dépôt entier, historique et remote
inclus, prêt à l'emploi. 🚀

⬅️ Retour au [sommaire des cours](README.md)
