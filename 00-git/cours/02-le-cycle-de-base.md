# Leçon 2 — Le cycle de base : les 3 zones

C'est **la** notion à comprendre pour ne plus jamais être perdu avec Git. Tout
fichier voyage à travers **3 zones**.

## 🗺️ Les 3 zones

```
   Répertoire de travail          Zone de transit            Dépôt (historique)
   (working directory)            (staging area)             (repository)
   ┌──────────────────┐           ┌──────────────┐           ┌──────────────┐
   │  tes fichiers    │ git add   │  fichiers     │ git commit│  commits      │
   │  tels que tu les │ ────────► │  prêts à être │ ────────► │  enregistrés  │
   │  modifies        │           │  enregistrés  │           │  pour toujours│
   └──────────────────┘           └──────────────┘           └──────────────┘
```

1. **Répertoire de travail** : les fichiers sur ton disque, ceux que tu modifies dans ton éditeur.
2. **Zone de transit** (*staging area*) : une salle d'attente. Tu y mets les fichiers
   que tu veux inclure dans ta prochaine photo.
3. **Dépôt** : l'historique. Une fois *committé*, c'est gravé.

> 🧠 **Analogie** : tu prépares un colis 📦.
> - `git add` = tu mets les objets choisis **dans le carton** (staging).
> - `git commit` = tu **fermes et scelles** le carton avec une étiquette (le message).
> Pourquoi deux étapes ? Pour choisir **précisément** ce qui entre dans chaque commit.

## 🔧 Les commandes

### `git status` — ta boussole 🧭
À taper **tout le temps**. Il te dit dans quelle zone sont tes fichiers.
```
git status
```

### `git add` — mettre dans la zone de transit
```
git add notes.md        # un fichier précis
git add .               # tout ce qui a changé (le point = "ici et en dessous")
```

### `git commit` — enregistrer la photo
```
git commit -m "Ajout des notes du module 0"
```
Le `-m` permet d'écrire le **message** directement. Un bon message décrit ce que
fait le commit.

### `git log` — voir l'historique
```
git log --oneline       # version courte, une ligne par commit
```

## 💡 Tips du mentor

- **`git status` est ton meilleur ami.** Avant et après chaque commande, regarde-le.
- **Un commit = une idée.** Ne mélange pas 10 changements sans rapport dans un seul commit.
- **Messages clairs.** « fix » ou « update » ne disent rien. « Corrige le calcul du total » est utile.
- La staging area déroute au début. Retiens juste : `add` puis `commit`, toujours dans cet ordre.

## ✅ Ce qu'il faut retenir

`modifier` → `git add` → `git commit`. C'est le battement de cœur de Git. 💓

➡️ Suite : [Leçon 3 — Le dépôt distant](03-depot-distant.md)
