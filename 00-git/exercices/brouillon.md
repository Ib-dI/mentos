C'est un brouillon qui 📐 La règle des Conventional Commits

  Format :
  <type>(<portée optionnelle>): <description courte à l'impératif>

  Les types les plus courants :

  ┌──────────┬───────────────────────────────────────────────────────────────┐
  │   Type   │                       Quand l'utiliser                        │
  ├──────────┼───────────────────────────────────────────────────────────────┤
  │ feat     │ une nouvelle fonctionnalité                                   │
  ├──────────┼───────────────────────────────────────────────────────────────┤
  │ fix      │ une correction de bug                                         │
  ├──────────┼───────────────────────────────────────────────────────────────┤
  │ docs     │ de la documentation uniquement                                │
  ├──────────┼───────────────────────────────────────────────────────────────┤
  │ style    │ mise en forme (espaces, point-virgules…) sans changer le code │
  ├──────────┼───────────────────────────────────────────────────────────────┤
  │ refactor │ réécriture du code sans changer le comportement               │
  ├──────────┼───────────────────────────────────────────────────────────────┤
  │ test     │ ajout/modif de tests                                          │
  ├──────────┼───────────────────────────────────────────────────────────────┤
  │ chore    │ tâches diverses (config, dépendances, ménage)                 │
  └──────────┴───────────────────────────────────────────────────────────────┘

  Règles d'or de la description :
  - à l'impératif présent : « ajoute », « corrige » (et pas « ajouté » / « j'ai
  ajouté »)
  - courte (~50 caractères), pas de point final
  - en minuscule après les deux-points