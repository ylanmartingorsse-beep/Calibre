# Calibre, ton plan nutrition sur mesure

Fiche projet lue par Claude Code au début de chaque session. La garder à jour quand une décision importante change.

## Le projet

Calibre calcule un plan nutrition personnalisé : calories, macronutriments au gramme près, 12 micronutriments, menu du jour, liste de courses et conseils ciblés (hormones, récupération, sommeil, énergie, immunité).

Public visé : les sportifs, et surtout les actifs pressés qui n'ont pas le temps de réfléchir eux-mêmes à leur alimentation.

## État actuel

- L'application tient dans `index.html` : HTML, CSS et JavaScript dans un seul fichier, aucune dépendance, aucune étape de compilation.
- Fichiers annexes : `mentions-legales.html`, `confidentialite.html` et `404.html` (style commun dans `pages.css`), `favicon.svg`, `apple-touch-icon.png`, `icons/`, `manifest.webmanifest`, `og-image.png` (aperçu de partage 1200×630).
- Polices : Barlow et Barlow Condensed, hébergées dans `fonts/` (woff2, sous-ensemble latin, licence `fonts/OFL.txt`). Aucune requête vers un service tiers : c'est un argument de la page Confidentialité, à préserver.
- Les réponses de l'utilisateur restent dans son navigateur (localStorage, clés `calibre-v2` pour le profil et `calibre-jour` pour les repas validés du jour).
- Toujours en mode sombre (`color-scheme: dark`, pas de mode clair). Pensé mobile d'abord : sous 720 px de large, les onglets passent dans une barre en bas de l'écran.

## Parcours utilisateur

1. Questionnaire en 4 étapes : profil (sexe, âge, taille, poids, masse grasse facultative), rythme de vie, entraînement, objectif avec son intensité.
2. Tableau de bord à 4 onglets :
   - **Synthèse** : anneau des macros, métabolisme, dépense, déficit ou surplus, projection à 8 semaines, hydratation, fibres.
   - **Menu** : 4 repas avec grammages, validation des repas, liste de courses pour 7 jours à cocher.
   - **Micronutriments** : besoins du jour et meilleures sources alimentaires.
   - **Objectifs** : aliments ciblés par objectif, avec le niveau de preuve de chaque conseil, dont une partie testostérone et DHT.
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

- Identité « Sport premium sombre » : fond noir `#0B0B0C`, cartes `#151517` avec liseré `#2A2A2F`, accent néon citron vert `#C6FF3D` (boutons, onglet actif, progression, logo).
- Macros : protéines en bleu `#6E8BFF`, glucides en ambre `#FFB020`, lipides en vert `#2FD4A0`.
- Typo : Barlow Condensed 800 en capitales pour les titres et les chiffres, étiquettes espacées en capitales ; Barlow pour le texte.
- Signature visuelle : la jauge segmentée (barres en tirets façon compte-tours, via le masque `--seg`) pour les macros, l'anneau, la progression et le suivi des repas. Logo : un « C » en arc segmenté néon.
- Couleurs centralisées dans les variables de `:root` (`index.html`) et de `pages.css` : les garder synchronisées.
- Emojis pour illustrer les aliments, les repas et les objectifs.
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

- Avant de valider un changement visible, vérifier le rendu sur mobile (390 px) et sur ordinateur (1366 px), en mode clair et en mode sombre.
- Après tout changement de calcul, tester au moins quatre profils (homme et femme, sèche et prise de masse) et vérifier que le menu reste à ±2 % de la cible.
- Garder un site sans étape de compilation tant qu'aucun framework n'a été choisi.
- Messages de commit en français, courts et clairs.
- Le propriétaire du projet travaille souvent depuis son téléphone : réponses courtes, et un résumé clair de ce qui a changé à la fin de chaque tâche.

## Mise en ligne

- Hébergement : GitHub Pages, adresse https://ylanmartingorsse-beep.github.io/Calibre/ (dépôt public, branche `main`, dossier racine, fichier `.nojekyll`).
- Le site vit dans le sous-dossier `/Calibre/` : `404.html` utilise des chemins absolus `/Calibre/…` ; `canonical` et `og:` d'`index.html` pointent vers l'URL complète. À changer si un nom de domaine est ajouté.
- Mentions légales remplies : éditeur Ylan MARTIN GORSSE (non professionnel, adresse non publiée au titre de la LCEN art. 6-III-2), hébergeur GitHub, Inc.

## Idées pour la suite

- Page d'accueil vitrine avant le questionnaire.
- Options alimentaires : végétarien, sans porc, sans poisson, sans lactose.
- Nom de domaine personnalisé (le site est déjà prêt pour GitHub Pages).
- Comptes utilisateurs pour retrouver son plan sur tous ses appareils.
