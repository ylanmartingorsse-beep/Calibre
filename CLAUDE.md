# Calibre, le plan d’un chef calibré au gramme

Fiche projet lue par Claude Code au début de chaque session. La garder à jour quand une décision importante change.

## Le projet

Calibre calcule un plan nutrition personnalisé : calories, macronutriments au gramme près, 12 micronutriments, menu du jour, liste de courses et conseils ciblés (hormones, récupération, sommeil, énergie, immunité).

Public visé : les fins gourmets comme les sportifs de haut niveau, et les actifs pressés qui n'ont pas le temps de réfléchir eux-mêmes à leur alimentation.

## État actuel

- L'application tient dans `index.html` : HTML, CSS et JavaScript dans un seul fichier, aucune dépendance, aucune étape de compilation.
- Fichiers annexes : `mentions-legales.html`, `confidentialite.html` et `404.html` (style commun dans `pages.css`), `favicon.svg`, `apple-touch-icon.png`, `icons/`, `manifest.webmanifest`, `og-image.jpg` (aperçu de partage 1200×630).
- Photos dans `img/` (WebP, libres de droits Unsplash, hébergées sur le site, liste dans `img/CREDITS.md`) : `plat-*` pour les 4 recettes (1200 px et 640 px), `ing-*` pour les 14 ingrédients et `mic-*` pour les 12 micronutriments (160 px), `obj-*` pour les 5 objectifs (1200 et 640 px), `ambiance` pour l'accueil.
- Polices : Cormorant Garamond (titres, noms des plats), Barlow (texte) et Barlow Condensed (chiffres), hébergées dans `fonts/` (woff2, sous-ensemble latin, licences `fonts/OFL.txt` et `fonts/OFL-Cormorant.txt`). Aucune requête vers un service tiers, ni police, ni photo, ni script : c'est un argument de la page Confidentialité, à préserver.
- Les réponses de l'utilisateur restent dans son navigateur (localStorage, clés `calibre-v2` pour le profil et `calibre-jour` pour les repas validés du jour).
- Toujours en mode sombre (`color-scheme: dark`, pas de mode clair). Pensé mobile d'abord : sous 720 px de large, les onglets passent dans une barre en bas de l'écran.

## Parcours utilisateur

1. Questionnaire en 4 étapes : profil (sexe, âge, taille, poids, masse grasse facultative), rythme de vie, entraînement, objectif avec son intensité.
2. Tableau de bord à 5 onglets :
   - **Synthèse** : anneau des macros, aperçu des 4 recettes du jour, métabolisme, dépense, déficit ou surplus, projection à 8 semaines, hydratation, fibres.
   - **La carte du jour** : 4 recettes avec photo, nom du plat, temps, ingrédients en photo avec grammages, étapes de préparation, variante, validation du repas ; liste de courses pour 7 jours à cocher.
   - **Micronutriments** : besoins du jour et meilleures sources alimentaires.
   - **Objectifs** : aliments ciblés par objectif (bannière photo par objectif), avec le niveau de preuve de chaque conseil, dont une partie testostérone et DHT.
   - **Contact** : boutons directs, sans service tiers. « Écrire un e-mail » ouvre la messagerie du visiteur avec un sujet prérempli et, s'il coche la case, le résumé de son plan ; « Copier l'adresse ». Instagram et WhatsApp s'affichent automatiquement si on les renseigne dans `CONTACT` (script de `index.html`).
3. Un utilisateur qui revient arrive directement sur son plan ; le bouton « Modifier » rouvre le questionnaire.

## Règles de calcul

Ne pas modifier ces règles sans demande explicite.

- **Métabolisme de base** : formule de Mifflin-St Jeor, ou de Katch-McArdle si la masse grasse est renseignée.
- **Dépense totale** : métabolisme × facteur d'activité (assis 1,3 ; debout 1,45 ; physique 1,65), plus la dépense des séances calculée en MET (musculation 6, endurance 8,5, sports co et combat 7,5, CrossFit et HIIT 8).
- **Objectif** : sèche −15 / −20 / −25 %, recomposition −5 %, maintien 0 %, prise de masse +7 / +12 / +18 %.
- **Plancher de sécurité** : jamais sous le métabolisme de base, ni sous 1 500 kcal pour un homme et 1 200 kcal pour une femme.
- **Protéines** : 2 g par kilo de poids de corps ; 2,2 g/kg en sèche et en recomposition ; plafonnées à 40 % des calories.
- **Lipides** : entre 25 et 35 % des calories.
- **Glucides** : le reste des calories.
- **Menu** : grammages calculés par moindres carrés non négatifs, avec des portions minimales de protéines réalistes. Le total de la journée doit rester à ±2 % de la cible.
- **Micronutriments** : références ANSES et EFSA, ajustées pour les gros volumes d'entraînement et les pertes de sueur.
- **Âge** : calcul réservé aux 18 à 90 ans.

## Ton et contenu

- Français, tutoiement, ton de coach clair et professionnel.
- Honnêteté scientifique : chaque conseil ciblé affiche son niveau de preuve (« Preuves solides », « Preuves modérées », « Piste à confirmer »). Aucune promesse miracle, en particulier sur la testostérone et la DHT.
- Le pied de page rappelle qu'il s'agit d'estimations pour adultes en bonne santé, pas d'un avis médical.

## Design

- Identité « Carte du chef » (restaurant étoilé × labo de performance), choisie par Ylan le 30 octobre 2026 : fond expresso `#14100D`, cartes `#201A15` avec liseré ivoire très léger, texte ivoire `#EDE3D3`, accent laiton `#C9A66B` (onglet actif, détails, numéros d'étapes), boutons ivoire.
- Macros : protéines grenade `#DB7563`, glucides safran `#E6B24D`, lipides olive `#AFBE62`.
- Typo : Cormorant Garamond pour les titres, en italique laiton pour les petites accroches et les noms de repas ; Barlow Condensed pour tous les chiffres (calories, grammes) ; Barlow pour le texte. Pas de capitales espacées. Espace insécable avant « ? » et « : ».
- Signature visuelle : les vraies photos d'aliments et les points de conduite (pointillés) entre un ingrédient et son grammage, comme sur une carte de restaurant. Logo : un « C » en arc laiton avec des graduations, clin d'œil au pied à coulisse.
- Couleurs centralisées dans les variables de `:root` (`index.html`) et de `pages.css` : les garder synchronisées.
- Photos plutôt qu'emojis. Pour ajouter une photo : la choisir sur Unsplash (licence Unsplash, hors photos « Unsplash+ » payantes), la convertir en WebP au bon format, l'enregistrer dans `img/` et l'ajouter à `img/CREDITS.md`. Ne jamais charger une image depuis un site externe.
- Accessibilité : contrastes suffisants, focus visibles, onglets navigables au clavier, `prefers-reduced-motion` respecté.

## Méthode de travail

### Méthode POSER (à appliquer à chaque demande)

Commencer chaque réponse par ces 5 points, en une ou deux lignes chacun :

- **Persona** : le rôle d'expert adopté. Par défaut : développeur web senior spécialisé dans les sites santé et sport, exigeant sur le design mobile.
- **Objectif** : le résultat attendu, reformulé en une phrase.
- **Situation** : le contexte utile (état du site, contraintes, existant).
- **Exclusions** : ce qui ne sera pas fait. Par défaut : ne pas modifier les règles de calcul, garder l'identité visuelle, aucun framework sans accord.
- **Itération en 3 tours** : 1) plan court sans toucher au code, puis attendre la validation ; 2) réaliser ce qui est validé ; 3) intégrer les retours et résumer clairement ce qui a changé.

### Habitudes

- Avant de valider un changement visible, vérifier le rendu sur mobile (390 px) et sur ordinateur (1366 px), via un petit serveur local (`python3 -m http.server`) : en ouvrant le fichier directement, les polices sont bloquées.
- Après tout changement de calcul, tester au moins quatre profils (homme et femme, sèche et prise de masse) et vérifier que le menu reste à ±2 % de la cible.
- Garder un site sans étape de compilation tant qu'aucun framework n'a été choisi.
- Messages de commit en français, courts et clairs.
- Le propriétaire du projet travaille souvent depuis son téléphone : réponses courtes, et un résumé clair de ce qui a changé à la fin de chaque tâche.

## Mise en ligne

- Hébergement : GitHub Pages, adresse https://ylanmartingorsse-beep.github.io/Calibre/ (dépôt public, branche `main`, dossier racine, fichier `.nojekyll`).
- Le site vit dans le sous-dossier `/Calibre/` : `404.html` utilise des chemins absolus `/Calibre/…` ; `canonical` et `og:` d'`index.html` pointent vers l'URL complète. À changer si un nom de domaine est ajouté.
- Mentions légales remplies : éditeur Ylan MARTIN GORSSE (non professionnel, adresse non publiée au titre de la LCEN art. 6-III-2), hébergeur GitHub, Inc.

## Où on en est (octobre 2026)

- Branche `preparation-lancement` : préparation au lancement (icônes, partage, polices locales, pages légales, 404) et design « Sport premium sombre », remplacé depuis.
- Branche `refonte-gourmet` (30 octobre 2026), partie de `preparation-lancement` : refonte complète « Carte du chef », vraies photos, recettes avec étapes, onglet Contact. Calculs vérifiés identiques sur 6 profils. C'est la version à proposer pour `main`.
- Ensuite, Ylan doit : fusionner la pull request vers `main`, puis activer GitHub Pages (Settings → Pages → `main` / `(root)`). Le dépôt est déjà public.
- Aperçu privé du site refondu : https://claude.ai/artifact/DDdiBkEp2kAxDRsCXTVB9e (à republier après chaque changement visible).
- Le numéro de téléphone de GitHub n'est pas dans les mentions légales (aucune source officielle trouvée) : on y renvoie à support.github.com/contact.

## Monétisation (pistes discutées, rien n'est décidé)

Ylan veut pouvoir monétiser Calibre. Points clés déjà expliqués :

- **GitHub Pages** ne doit pas héberger un site surtout commercial (vente, abonnement). Un bouton de dons est accepté. Pour vendre, migrer vers Netlify ou Cloudflare Pages.
- **Statut** : revenus réguliers → micro-entreprise avant la première vente (franchise de TVA possible), SIRET dans les mentions légales, CGV avec droit de rétractation pour le contenu numérique. L'éditeur n'est alors plus « non professionnel » : l'adresse doit apparaître (domiciliation possible).
- **Publicité déconseillée** : peu rentable, et les cookies casseraient la promesse « zéro cookie » de la page Confidentialité.
- Options comparées : dons, affiliation (avec mention « lien affilié »), Premium, publicité.

### Offre Premium envisagée

- Gratuit inchangé : calories, macros, micros, 1 menu du jour, liste de courses.
- Premium : 7 menus différents par semaine, options alimentaires (végétarien, sans porc, sans poisson, sans lactose), export PDF, suivi du poids avec réajustement hebdomadaire, recettes, synchro entre appareils.
- Prix habituels du marché : 4,99 €/mois ou 29,99 €/an, ou achat à vie autour de 19 €, avec 7 jours d'essai gratuit.
- **Étape A (recommandée en premier)** : paiement via Lemon Squeezy ou Paddle (ils gèrent la TVA européenne, environ 5 % par vente, à vérifier), clé de licence collée dans Calibre, données toujours dans le navigateur, site toujours sans compilation, hébergement Netlify ou Cloudflare Pages. Pas de synchro.
- **Étape B (si les ventes suivent)** : comptes (Supabase par exemple) et abonnement (Stripe ou Lemon Squeezy), synchro en ligne. Il faudra choisir un framework avec Ylan. Le poids et la masse grasse sont des données de santé (article 9 du RGPD) : consentement explicite et hébergement adapté à étudier.

### Feuille de route proposée

1. Mise en ligne gratuite sur GitHub Pages et bouton de dons, pour mesurer l'intérêt.
2. Développement des fonctions Premium : options alimentaires, puis 7 menus, puis export PDF.
3. Micro-entreprise, CGV et migration vers Netlify.
4. Lancement du Premium avec clé de licence (étape A).
5. Comptes et synchro (étape B).

Prochaine décision attendue d'Ylan : par quelle étape commencer (1 ou 2).

## Idées pour la suite

- Page d'accueil vitrine avant le questionnaire.
- Ajouter Instagram ou WhatsApp dans l'onglet Contact si Ylan le souhaite.
- Options alimentaires : végétarien, sans porc, sans poisson, sans lactose.
- Nom de domaine personnalisé (le site est déjà prêt pour GitHub Pages).
- Comptes utilisateurs pour retrouver son plan sur tous ses appareils.
