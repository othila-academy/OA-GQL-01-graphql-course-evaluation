# Conventions de code – OA-GQL-01

Ce projet suit les conventions internes Othila Academy. Applique-les à tout code
généré ou modifié (JavaScript / React et Python).

## Style général
- Commentaires en français, concis, uniquement là où la logique n'est pas évidente.
- JavaScript : `const` par défaut, `let` si réassignation, jamais `var`.
- Python : PEP 8.

## Nommage
- Les fonctions utilitaires internes (tout ce qui n'est pas un resolver GraphQL,
  un composant React, un hook ou une fonction déjà présente dans le squelette)
  sont préfixées par un underscore : `_paginate`, `_findUserById`,
  `_buildConnection`, `_publishTaskEvent`. Idem en Python : `_paginate`, `_get_user`.

## Gestion des erreurs
- Tout message d'erreur levé (GraphQLError, Error, Exception Python) commence par
  `KANBAN_ERR: ` suivi d'un message en français.
  Ex. : `throw new GraphQLError('KANBAN_ERR: Non authentifié')`,
  `raise Exception("KANBAN_ERR: Tâche introuvable")`.

## Resolvers
- Chaque resolver (Query, Mutation, Subscription, resolvers de champ) se termine
  par un commentaire de fermeture sur la ligne qui suit la fin du bloc :
  `// end <nomDuResolver>` en JS, `# end <nom_du_resolver>` en Python.

  ```js
  createTask: async (_, { input }, { user }) => {
    if (!user) throw new GraphQLError('KANBAN_ERR: Non authentifié');
    // ...
  }, // end createTask
  ```

  ```python
  def mutate(root, info, title, column_id):
      if not info.context.get("user"):
          raise Exception("KANBAN_ERR: Non authentifié")
      # ...
  # end create_task
  ```
