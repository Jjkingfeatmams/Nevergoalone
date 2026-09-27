# Publier le nouveau prototype live sur Netlify

Cette version conserve les profils intéressés en direct avec Netlify Blobs.
Elle commence par l'histoire de Never Go Alone, puis propose un onboarding
local (prénom, nom, âge, sexe et centres d'intérêt). Les centres d'intérêt
priorisent le catalogue sans masquer les autres sorties ; le thème sombre est
actif par défaut.

## Publication

1. Créer un **nouveau projet Netlify** depuis ce dossier Git. Ne pas publier
   seulement `index.html`, car les Functions ne seraient pas publiées.
2. Laisser le **Base directory** vide si le contenu de ce dossier est à la
   racine du dépôt. Netlify utilisera `netlify.toml`, la commande
   `npm run build` et le dossier publié `dist`.
3. Déclencher le déploiement. La commande est `npm run build` et le dossier
   publié est `dist`.
4. Dans **Site configuration → Environment variables**, ajouter de préférence
   `INTEREST_HASH_SECRET` avec une longue valeur aléatoire privée. Ne pas
   modifier cette valeur après les premières inscriptions, car elle protège
   les liens de retrait des profils.

Le dossier `dist` est généré automatiquement par la commande de build et est
volontairement ignoré par Git : il n'est pas nécessaire de l'ajouter au dépôt.

Les routes `/api/*` sont traitées par `netlify/functions/live-interest.mjs`.
Elles enregistrent seulement le prénom, l'âge, la nationalité, l'activité,
la courte description, les passions et un avatar illustré qui peuvent être
affichés publiquement.
Le genre choisi peut aussi être affiché publiquement après consentement.
L'e-mail et le nom ne sont pas conservés dans le stockage partagé.

Pour protéger l'accès au prototype, activer la protection du site dans les
réglages Netlify plutôt que de mettre un mot de passe dans le code source.
