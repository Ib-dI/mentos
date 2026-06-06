# Leçon 10 — Des messages de commit clairs et conventionnels

Un projet, c'est des **centaines de commits**. Si chaque message est vague (`fix`,
`update`, `truc`), l'historique devient illisible. Bien écrits, tes commits racontent
l'**histoire du projet** comme un livre.

---

## 😱 Le problème

```
fix
truc
ça marche enfin
update
asdfgh
```
Impossible de savoir ce qui a changé ni pourquoi. Maintenant compare :
```
feat(auth): ajoute la connexion par Google
fix(panier): corrige le total quand la quantité est à zéro
docs(readme): explique l'installation sous Windows
```
On lit l'histoire d'un coup d'œil. C'est ça, les **Conventional Commits**.

---

## 📐 Le format

```
<type>(<portée optionnelle>): <description courte à l'impératif>
```

### Les types courants

| Type | Quand l'utiliser |
|------|------------------|
| `feat` | une **nouvelle fonctionnalité** |
| `fix` | une **correction de bug** |
| `docs` | de la **documentation** uniquement |
| `style` | mise en forme (espaces, indentation…) sans changer le code |
| `refactor` | réécriture du code **sans changer le comportement** |
| `test` | ajout/modif de **tests** |
| `chore` | tâches diverses (config, dépendances, ménage) |

### La portée (scope) — optionnelle

Entre parenthèses, **un seul mot court** (ou `kebab-case`), qui dit **où** ça touche :
`feat(auth)`, `fix(panier)`, `docs(commits-conventionnels)`.
> ⚠️ Pas d'espaces dans la portée : `(commits)` ✅, `(commit conventionnel)` ❌.

---

## ✍️ Les règles d'or de la description

1. **À l'impératif présent** : « ajoute », « corrige », « explique »
   (pas « ajouté », ni « j'ai ajouté », ni le nom « ajout »).
   - Astuce : la phrase doit compléter *« Si j'applique ce commit, il va… »*
     → « …**ajoute** la page contact ».
2. **Précise** : on doit comprendre **quoi** sans ouvrir le code.
   - ❌ `fix(bouton): corrige le bug du bouton`
   - ✅ `fix(bouton): corrige le plantage au double-clic`
3. **Courte** (~50 caractères), **minuscule** après les deux-points, **pas de point final**.
4. **Soignée** : un message est un livrable lu par toute l'équipe. On y corrige même
   les fautes d'orthographe.

---

## 🚀 Pourquoi c'est pas juste cosmétique

Des outils **lisent** ces préfixes pour automatiser :
- **générer le changelog** automatiquement,
- décider du **numéro de version** (versioning sémantique) :
  - `fix` → version **patch** (1.2.3 → 1.2.**4**)
  - `feat` → version **mineure** (1.2.3 → 1.**3**.0)
  - un changement cassant (noté `feat!` ou `BREAKING CHANGE`) → version **majeure**
    (1.2.3 → **2**.0.0)

---

## 🔧 Corriger le dernier message : `git commit --amend`

Tu viens de committer et tu repères une faute dans le message ? Tant qu'il n'est **pas
encore poussé**, tu peux le réécrire :

```bash
git commit --amend -m "docs(commits): explique le fonctionnement des commits conventionnels"
# ou sans -m : ouvre l'éditeur sur le dernier commit
git commit --amend
```

`--amend` sert aussi à **ajouter un fichier oublié** au dernier commit :
```bash
git add fichier-oublie.txt
git commit --amend --no-edit   # garde le message tel quel
```

### ⚠️ Le piège mortel de `--amend`

`--amend` **ne modifie pas** le commit : il en **crée un nouveau** qui remplace
l'ancien → **le hash change**.
```
avant :  1236c00 docs(...)
amend :  14864b8 docs(...)   ← hash différent = commit différent
```
Conséquence : **JAMAIS de `--amend` sur un commit déjà poussé/partagé.** Les autres ont
encore l'ancien hash dans leur historique ; tu créerais une divergence et tu casserais
leur dépôt. Règle simple :

> ✅ `--amend` uniquement sur un commit **local, non poussé**.

(On reverra cette règle « ne réécris pas l'histoire partagée » avec `reset` et `rebase`
en leçon 11.)

---

## 💡 Tips du mentor

- En anglais ou en français ? Peu importe, mais **reste cohérent** dans tout le projet.
  Beaucoup d'équipes écrivent les messages en anglais : `feat`, `fix`… sont anglais.
- Le **type** dépend du contexte, pas du mot employé : « ça marche enfin » peut être un
  `fix` (j'ai réparé) ou un `feat` (ma feature marche). À toi de qualifier l'intention.
- Un commit = **une intention**. Si ton message contient « et », tu mélanges peut-être
  deux changements → fais deux commits.

## ✅ Ce qu'il faut retenir

`type(scope): description à l'impératif, précise et minuscule`. Ça rend l'historique
lisible et ça alimente des outils automatiques. Et `--amend` répare le **dernier**
commit **local** — jamais un commit déjà partagé. 📝

⬅️ Retour au [sommaire des cours](README.md)
