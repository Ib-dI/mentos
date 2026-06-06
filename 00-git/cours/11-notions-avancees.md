# Leçon 11 — Notions avancées (survol) : `reset`, `reflog`, `rebase`, tags

⚠️ **Fiche "comprendre et se méfier".** Ces commandes sont **puissantes et certaines
sont dangereuses**. Le but ici n'est pas de les maîtriser, mais de **savoir qu'elles
existent, à quoi elles servent, et quels pièges éviter**.

---

## 1️⃣ `git reset` — reculer la branche en arrière

`reset` déplace ta branche sur un commit antérieur. La grande question : **que
deviennent les modifications entre les deux ?** → 3 modes.

| Mode | Historique | Staging | Tes fichiers | Danger |
|------|-----------|---------|--------------|--------|
| `--soft` | reculé | gardé (staged) | **gardés** | 🟢 sûr |
| `--mixed` *(défaut)* | reculé | vidé | **gardés** (non staged) | 🟢 sûr |
| `--hard` | reculé | vidé | **SUPPRIMÉS** | 🔴 destructeur |

```bash
git reset --soft HEAD~1    # annule le dernier commit, garde tout en staging
git reset HEAD~1           # (--mixed) annule le commit, travail à re-committer
git reset --hard HEAD~1    # annule le commit ET jette le travail 💀
```

- `HEAD~1` = un commit en arrière, `HEAD~2` = deux, etc.
- Usage sain typique : `--soft` pour refaire un commit fait trop tôt.

> 🔴 **`git reset --hard` est la commande la plus dangereuse de Git** : c'est l'une des
> rares qui peut détruire du travail définitivement. Réfléchis à deux fois.

---

## 🛟 `git reflog` — le filet de sécurité (À RETENIR)

Git garde une trace de **tous** les déplacements de `HEAD`, même vers des commits
"supprimés" par un `reset --hard` (pendant ~30 jours).

```bash
git reflog                 # liste tout l'historique de tes déplacements de HEAD
git reset --hard <hash>    # reviens sur un commit que tu croyais perdu
```

> 🧠 **Réflexe de survie** : après un `reset`/`rebase` raté, **`git reflog` AVANT de
> paniquer**. Tes commits y sont presque toujours encore.

---

## 2️⃣ `git rebase` — réécrire l'histoire en ligne droite

Même but que `merge` (intégrer une branche), méthode différente :

```
MERGE (garde la vraie histoire) :       REBASE (réécrit, tout droit) :
A───B───C (master)                       A───B───C (master)
     \       \                                    \
      D───E───M (merge commit)                     D'──E' (rejoués au bout)
```

`rebase` **rejoue tes commits par-dessus** la branche cible → historique linéaire,
**sans commit de merge**.

- `git rebase master` (depuis ta branche) → rejoue ta branche sur master.
- `git rebase -i HEAD~3` → **interactif** : fusionner (squash), renommer, réordonner
  tes 3 derniers commits avant de les partager. Outil de pro pour nettoyer une branche.

> 🔴 **Même piège que `--amend`** : `rebase` **change les hash** → **JAMAIS sur une
> branche déjà poussée/partagée.** Uniquement sur ta branche locale perso.

---

## 🔁 Le principe à retenir : NE PAS réécrire l'histoire partagée

`git commit --amend`, `git reset` et `git rebase` ont un point commun :
ils **réécrivent l'historique → ils changent les hash des commits**.

Or, dès qu'un commit est **poussé**, les autres l'ont avec son hash. Si tu le réécris,
ton historique et le leur **divergent** → tu casses le dépôt partagé.

> ✅ **Règle d'or** : réécriture (`amend` / `reset` / `rebase`) **uniquement sur des
> commits locaux non poussés**. Ce qui est partagé est gravé dans le marbre — pour le
> corriger proprement, on utilise `git revert` (qui crée un *nouveau* commit qui annule,
> sans réécrire — voir leçon 7).

---

## 3️⃣ Tags & releases — marquer les versions

Un **tag** = une étiquette posée sur un commit important (une version livrée).

```bash
git tag v1.0.0                          # tag léger
git tag -a v1.0.0 -m "Première version" # tag annoté (recommandé : daté, auteur, message)
git tag                                 # lister les tags
git show v1.0.0                         # voir le commit pointé par le tag

git push origin v1.0.0                  # ⚠️ un push normal n'envoie PAS les tags
git push origin --tags                  # pousser tous les tags
```

> 💡 Sur GitHub, un tag peut devenir une **Release** : une page avec notes de version et
> fichiers à télécharger. C'est ce qui produit les `v1.0.0`, `v2.3.1`… des logiciels.
> Lié au **versioning sémantique** (voir leçon 10 : `fix`=patch, `feat`=mineure, etc.).

---

## 🎁 Quelques commandes bonus pour être complet

```bash
git cherry-pick <hash>   # copier UN commit précis d'une autre branche vers la tienne
git show <hash>          # voir le détail complet d'un commit (message + diff)
git blame <fichier>      # qui a écrit chaque ligne et dans quel commit (enquête)
git commit --amend       # corriger le DERNIER commit local (voir leçon 10)
git revert <hash>        # annuler un commit en en créant un nouveau (sûr, voir leçon 7)
```

---

## 💡 Tips du mentor

- **90 % du temps**, tu n'as besoin que des bases (`add`, `commit`, `push`, `pull`,
  branches, `merge`). `reset`/`rebase` sont des outils ponctuels, pas le quotidien.
- En cas de doute sur une commande qui touche l'historique : **fais une branche de
  sauvegarde avant** (`git branch sauvegarde`). Tu pourras toujours y revenir.
- `git revert` vs `git reset` : `revert` est l'option **sûre et partageable** (il ajoute
  un commit) ; `reset` réécrit et se réserve au local.

## ✅ Ce qu'il faut retenir

`reset --hard` détruit → méfiance. `reflog` est ton filet de sécurité. `rebase` rend
l'historique linéaire mais réécrit les hash → local seulement. Les tags marquent les
versions. **Règle suprême : on ne réécrit jamais l'histoire déjà partagée.** 🏁

⬅️ Retour au [sommaire des cours](README.md)
