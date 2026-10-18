# Calibre

Site de nutrition sur mesure : calories, macronutriments, micronutriments, menu du jour et liste de courses, calculés selon le profil, l'activité et l'objectif de chacun (sèche, recomposition, maintien, prise de masse).

## Ouvrir le site

Ouvre `index.html` dans un navigateur. Rien à installer.

Pour tester comme en ligne (polices, manifeste, page 404) : `python3 -m http.server` dans ce dossier, puis http://localhost:8000.

## Mettre en ligne

Le site est prévu pour GitHub Pages, à l'adresse https://ylanmartingorsse-beep.github.io/Calibre/.

1. Le dépôt doit être public.
2. Sur GitHub : Settings → Pages → Source « Deploy from a branch » → branche `main`, dossier `/ (root)`.
3. Après une ou deux minutes, le site est en ligne. `404.html` est utilisé automatiquement pour les pages introuvables.

## Structure

- `index.html` : le site complet (structure, styles et logique de calcul).
- `mentions-legales.html`, `confidentialite.html`, `404.html` : pages secondaires, style commun dans `pages.css`.
- `fonts/` : polices Barlow hébergées sur le site (licence OFL).
- `favicon.svg`, `apple-touch-icon.png`, `icons/`, `manifest.webmanifest`, `og-image.png` : icônes et aperçu de partage.
- `CLAUDE.md` : la fiche projet que Claude Code lit au début de chaque session (règles de calcul, design, méthode de travail).

## Avertissement

Calibre fournit des estimations destinées aux adultes en bonne santé, sur la base des références de l'ANSES et de l'EFSA. Il ne remplace pas un avis médical.
