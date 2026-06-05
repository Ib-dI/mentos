# Leçon 4 — Les branches

Les branches sont **la** fonctionnalité qui rend Git si puissant. C'est ce qui permet
de travailler sur une nouvelle idée **sans casser** le code qui marche.

## 🌿 C'est quoi une branche ?

Une branche est une **ligne de développement indépendante**. La branche principale
s'appelle souvent `master` (ou `main`). Quand tu veux ajouter une fonctionnalité, tu
crées une branche à part, tu y travailles tranquillement, puis tu **fusionnes** dans
la principale quand c'est prêt.

> 🧠 **Analogie** : `master` est le tronc de l'arbre. Une branche, c'est une vraie
> branche : elle pousse à part, et si elle est bonne, on la greffe au tronc (*merge*).
> Pendant ce temps, le tronc reste intact.

```
master:   A───B───C────────────E   (merge)
                    \          /
branche:             D────────/
```

## 🔧 Les commandes

### Créer une branche et basculer dessus
```
git switch -c ma-fonctionnalite      # méthode moderne (-c = create)
git checkout -b ma-fonctionnalite    # ancienne méthode, équivalente
```

### Lister les branches / voir où on est
```
git branch        # l'étoile * indique ta branche actuelle
```

### Changer de branche
```
git switch master
```

> ⚠️ **Le déclic à comprendre** : quand tu changes de branche, **les fichiers sur ton
> disque changent réellement**. Un fichier créé sur une branche « disparaît » du dossier
> quand tu reviens sur `master` (il n'est pas perdu : il vit dans l'autre branche).

### Fusionner une branche dans la branche actuelle
```
git switch master           # 1. on se place sur la branche qui reçoit
git merge ma-fonctionnalite # 2. on y fusionne l'autre
```

### Supprimer une branche fusionnée
```
git branch -d ma-fonctionnalite   # -d refuse si non fusionnée (garde-fou)
git branch -D ma-fonctionnalite   # -D force (à utiliser en connaissance de cause)
```

## ⏩ Le « fast-forward »

Si `master` n'a **pas bougé** pendant que tu travaillais sur ta branche, le merge est
un **fast-forward** : Git n'a pas besoin de créer un commit de fusion, il fait juste
**avancer le pointeur** de `master` jusqu'à ta branche.

Si au contraire `master` a reçu d'autres commits entre-temps, les deux branches ont
**divergé** : Git crée alors un vrai **commit de merge** qui réunit les deux histoires.

## 💥 Et si les deux branches modifient la même ligne ?

C'est un **conflit de fusion** (*merge conflict*). Git ne sait pas quelle version
garder et te demande de choisir à la main. On verra ça en exercice — pas de panique,
c'est moins effrayant qu'il n'y paraît.

## 💡 Tips du mentor

- **Ne travaille jamais directement sur `master`** pour une nouvelle fonctionnalité. Une branche par tâche.
- **Nomme tes branches clairement** : `ajout-login`, `correction-bug-total`, pas `test2`.
- **Supprime tes branches après merge.** Un dépôt propre = un esprit clair.

## ✅ Ce qu'il faut retenir

Le cycle : `switch -c` → travailler → `commit` → `switch master` → `merge` → `branch -d`.

➡️ Suite : [Leçon 5 — Le fichier .gitignore](05-gitignore.md)
