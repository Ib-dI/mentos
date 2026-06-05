# Leçon 3 — Le dépôt distant (GitHub)

Tes commits vivent pour l'instant sur ta machine. Pour les sauvegarder en ligne et
collaborer, on les envoie vers un **dépôt distant** (*remote*) — typiquement sur GitHub.

## 🔗 `git remote` — connecter local et distant

Un *remote* est juste un **raccourci nommé** vers l'adresse de ton dépôt GitHub.
Par convention, on l'appelle **`origin`**.

```
git remote add origin https://github.com/ton-pseudo/ton-repo.git
git remote -v          # vérifie : affiche les remotes enregistrés
```

> `origin` n'est pas un mot magique, c'est juste le nom habituel. Tu pourrais
> l'appeler autrement, mais tout le monde utilise `origin`, garde-le.

## ⬆️ `git push` — envoyer vers GitHub

```
git push                       # envoie les commits de ta branche actuelle
git push -u origin master      # la 1re fois : lie ta branche locale à origin
```

Le `-u` (pour *upstream*) crée le lien entre ta branche locale et sa jumelle sur
GitHub. Après ça, un simple `git push` suffit.

## ⬇️ `git pull` — récupérer depuis GitHub

Quand le dépôt distant a des commits que tu n'as pas (parce qu'un collègue a poussé,
ou parce que **toi-même** tu as fusionné une PR sur le site), tu te resynchronises :

```
git pull
```

> 🧠 `git pull` = `git fetch` + `git merge`. Il **télécharge** les nouveautés puis
> les **intègre** dans ta branche, en une commande.

## 🔍 `git fetch` — juste regarder, sans intégrer

```
git fetch
```
`fetch` télécharge les nouveautés du distant **sans** modifier ton travail. Utile
pour voir « ce qui se passe sur GitHub » avant de décider de fusionner. Plus prudent
que `pull` quand tu n'es pas sûr.

## 📥 `git clone` — copier un dépôt existant

Pour récupérer un projet qui existe déjà sur GitHub (le tien sur un autre PC, ou
celui de quelqu'un d'autre) :

```
git clone https://github.com/un-pseudo/un-repo.git
```
Ça crée le dossier, télécharge tout l'historique et configure `origin` automatiquement.

## 🧭 Le schéma mental

```
   TON PC (local)                         GITHUB (distant / origin)
   ┌───────────────┐    git push  ──►     ┌───────────────┐
   │  tes commits  │                      │  tes commits  │
   │               │   ◄── git pull       │  sauvegardés  │
   └───────────────┘   ◄── git fetch      └───────────────┘
            ▲                                      
            └──────────── git clone (la 1re copie) ┘
```

## 💡 Tips du mentor

- **Pousse souvent.** Un commit non poussé n'est pas sauvegardé en ligne.
- **`git pull` avant de commencer à travailler** quand tu collabores : tu pars de la dernière version.
- Choisis **HTTPS** comme adresse au début (plus simple sur Windows que SSH).

## ✅ Ce qu'il faut retenir

`origin` = ton GitHub. `push` = envoyer, `pull` = recevoir, `clone` = copier la 1re fois.

➡️ Suite : [Leçon 4 — Les branches](04-les-branches.md)
