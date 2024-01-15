+++
title = 'Authentification in spa 🔐'
date = 2024-01-15T04:35:46+03:00
+++

How authentication process work in Single Page Application (SPA)

<!--more-->

## 🌍 General concept

```js
// Hook de Navigation : Exécuté avant chaque navigation
router.beforeEach((to, from, next) => {
  // Étape 1: Accéder aux informations de l'utilisateur authentifié
  const authUser = store.getters["auth/authUser"];

  // Étape 2: Vérifier si la route nécessite une authentification
  const reqAuth = to.matched.some((record) => record.meta.requiresAuth);

  // Étape 3: Préparer l'objet de requête de redirection vers la page de connexion
  const loginQuery = { path: "/login", query: { redirect: to.fullPath } };

  if (reqAuth && !authUser) {
    // Étape 4: La route nécessite une authentification, mais l'utilisateur n'est pas authentifié
    // Étape 5: Dispatch de l'action pour obtenir les informations d'authentification de l'utilisateur
    store.dispatch("auth/getAuthUser").then(() => {
      // Vérifier à nouveau si l'utilisateur est authentifié après la résolution de l'action asynchrone
      if (!store.getters["auth/authUser"]) 
        // Étape 6: Redirection vers la page de connexion avec la redirection préparée
        next(loginQuery);
      else 
        // Étape 7: Utilisateur authentifié, permettre la continuation de la navigation
        next();
    });
  } else {
    // Étape 8: La route ne nécessite pas d'authentification, permettre la continuation de la navigation
    next(); // Assurez-vous toujours d'appeler next()!
  }
});
```

## ⚠️ Notabene

Using this approch can costs a lot of request if we test for a token validity everytime we use it. Instead we can just check for a variable in our `localstorage`

Our variable in `localstorage` will be updated when:

- users loged in
- users loged out
- token has expired and refresh token is no longer valide
