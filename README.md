# Calibre

Site de nutrition sur mesure : calories, macronutriments, micronutriments, menu du jour et liste de courses, calculés selon le profil, l'activité et l'objectif de chacun (sèche, recomposition, maintien, prise de masse).

## Ouvrir le site

Ouvre `index.html` dans un navigateur. Rien à installer.

Pour tester comme en ligne (polices, manifeste, page 404) : `python3 -m http.server` dans ce dossier, puis http://localhost:8000.

## Mettre en ligne

Le dossier se publie tel quel sur n'importe quel hébergeur de site statique (Netlify, Cloudflare Pages, GitHub Pages…). `404.html` est reconnu automatiquement par ces hébergeurs. Avant la mise en ligne, compléter les champs `[…]` des pages légales et mettre le domaine dans les balises de partage d'`index.html`.

## Structure

- `index.html` : le site complet (structure, styles et logique de calcul).
- `mentions-legales.html`, `confidentialite.html`, `404.html` : pages secondaires, style commun dans `pages.css`.
- `fonts/` : polices Barlow hébergées sur le site (licence OFL).
- `favicon.svg`, `apple-touch-icon.png`, `icons/`, `manifest.webmanifest`, `og-image.png` : icônes et aperçu de partage.
- `CLAUDE.md` : la fiche projet que Claude Code lit au début de chaque session (règles de calcul, design, méthode de travail).

## Avertissement

Calibre fournit des estimations destinées aux adultes en bonne santé, sur la base des références de l'ANSES et de l'EFSA. Il ne remplace pas un avis médical.
