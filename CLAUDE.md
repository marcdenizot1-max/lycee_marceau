# Lycée Marceau — Site statique

Site vitrine HTML/CSS pur (pas de framework, pas de JS de build) pour le **Lycée Marceau de Chartres**, calqué sur les informations publiques de l'établissement.

## Architecture

10 pages HTML autonomes + 1 maquette d'origine (`design1.html`, à ne pas toucher : référence de design conservée pour mémoire).

```
index            -> Accueil (synthèse, ne PAS y entasser tout le contenu)
etablissement    -> Présentation, identité, projet pédagogique, chiffres
histoire         -> Histoire 1587→aujourd'hui, patrimoine, gal Marceau
anciens-eleves   -> Galerie + 6 portraits (Vigo, Chautemps, Chasles…)
formations       -> Vue d'ensemble + tableau de synthèse
cpge             -> MPSI / PCSI / MP / PC, taux, candidature Parcoursup
sections         -> Sections européennes, sportives, BIA, langues
vie-lyceenne     -> Internat, restauration, sport, CDI, CVL, label 2030
actualites       -> Cards news (JPO, CPGE, Pôle Espoir, BIA, voyage…)
contact          -> Coordonnées, carte OSM, formulaire, accès
```

**Règle clé donnée par l'utilisateur :** ajouter du contenu dans les pages dédiées, **pas dans `index`**. L'accueil reste une vitrine de synthèse avec liens vers les pages détaillées.

## Conventions

- **Liens internes sans `.html`** : `href="cpge"`, pas `href="cpge.html"`. Sur GitHub Pages cela impose que les fichiers soient bien `cpge.html` et que le serveur résolve l'extension (ou bien il faut `cpge/index.html`). Les URL externes en `.html` (annuaire MEN) sont conservées telles quelles.
- **Header / footer dupliqués** dans chaque page (pas de moteur de templating). Toute modification doit être propagée aux 10 pages — utiliser un script Python plutôt qu'un edit manuel.
- `assets/partials.html` est juste une note explicative, il n'est jamais chargé.
- Tags HTML : on garde les `&rarr;`, les `<sup>` pour les ordinaux (1<sup>re</sup>, III<sup>e</sup>), les guillemets typographiques français.

## Design system

Variables dans `assets/style.css` (tout le CSS partagé, ~530 lignes) :

```
--primary-color: #083F86    (bleu Marceau, repris du nom du lycée sur le site officiel)
--secondary-color: #cda052  (or doux / laiton)
--bg-color:      #fcfcfc
--text-color:    #333
--muted:         #666
--border-soft:   #ececec
--font-title:    'Playfair Display' (h1-h4, .logo)
--font-text:     'Inter'           (body)
```

Variante "Innovation & Avenir" (vert sapin / cuivre) commentée dans `design1.html` si l'utilisateur veut basculer.

Composants présents dans le CSS : `header / .nav-links / .submenu`, `.btn-cta / .btn-ghost`, `.alert-band`, `.hero` + `.hero.short`, `.section / .section.alt`, `.section-head`, `.grid + .card + .card-news + .tag + .card-link`, `.split + .key-figures`, `.alumni .person`, `.contact-grid + .contact-info + .contact-form`, `.styled-table`, `.prose`, `footer / .footer-grid / .socials`. Responsive : breakpoints 960 px et 768 px (menu hamburger via `.menu-toggle` + classe `.open` togglée en JS inline).

## Logos & images

- **Blason officiel** : extrait du bandeau du site officiel (`bandeauv4.jpg`) puis croppé à 700×700 puis redimensionné à 300×300 avec `sips`. Stocké dans `assets/logos/blason-marceau.jpg`. Le bandeau d'origine entier est conservé dans `assets/logos/marceau-banner.jpg` au cas où on voudrait recropper.
- **Favicons partenaires** (footer "Liens utiles") : servis par `https://www.google.com/s2/favicons?domain=<domaine>&sz=64`. Affichés sur fond blanc arrondi via `footer ul a img` pour rester lisibles sur le footer bleu nuit.
- **Hero** : photo Wikimedia de la cour d'honneur, en background avec overlay bleu nuit 78 %.
- **Images d'actualité** : Unsplash (URLs en clair dans le HTML, pas de download local).
- **Carte contact** : iframe OpenStreetMap (pas Google Maps, donc pas de clé API).

## Données factuelles à respecter

Vérifiées sur Wikipédia / annuaire MEN / Onisep / Parcoursup au moment de la création (avril 2026) — à recroiser avant tout changement chiffré.

- Adresse : 2, rue Pierre Mendès-France · BP 10309 · 28006 Chartres Cedex
- Tél : 02 37 91 62 00
- Email : ce.0280007f@ac-orleans-tours.fr
- Code RNE : 0280007F · Académie d'Orléans-Tours
- ~1 614 élèves · public · mixte · internat
- Construit en 1887 par **Alfred-Étienne Piébourg** (style III<sup>e</sup> République)
- Hérite d'un collège de **1587** ; intègre l'ancien couvent franciscain (XVI<sup>e</sup>, MH 1979) et l'abbaye bénédictine (XVIII<sup>e</sup>, réaménagée 1973)
- Nommé d'après le général **François-Séverin Marceau** (1769-1796), élève en 1785
- 4 CPGE : MPSI, PCSI, MP, PC · plus de 95 % atteignent un niveau Master · ~29 % boursiers · ~200 écoles d'ingénieurs accessibles
- Sections européennes anglais (DNL : physique-chimie + histoire-géo) et allemand
- Pôle Espoir Handball, sections sportives basket / plongée / natation
- 7 langues : anglais, allemand, espagnol, italien, russe, latin, grec
- Label **Génération 2030** (sport et engagement)
- JPO de référence : samedi **14 mars 2026** · 9h30-12h30
- Anciens élèves illustres : Jean Vigo, Camille Chautemps, Michel Chasles, J.-B. Duroselle, Michel Vovelle, gal Marceau

## Liens externes utilisés

- Annuaire MEN : `https://www.education.gouv.fr/annuaire/28006/chartres/lycee/0280007f/lycee-marceau.html`
- Onisep : `https://www.onisep.fr/ressources/structures-enseignement/centre-val-de-loire/eure-et-loir/lycee-marceau`
- Parcoursup CPGE : `https://dossier.parcoursup.fr/Candidats/public/fiches/afficherFicheFormation?g_ta_cod=3724`
- Académie : `https://www.ac-orleans-tours.fr/`
- Site officiel du lycée : `https://lyc-marceau-chartres.tice.ac-orleans-tours.fr/eva/`

## Git

- Remote : `https://github.com/marcdenizot1-max/lycee_marceau`
- Branche : `main`
- Premier commit : initial complet (29 avr. 2026)
- Deuxième commit : `de7966a` — blason officiel + favicons partenaires + retrait des `.html` dans les liens internes

## Recettes utiles

**Propager une modif de header / footer aux 10 pages** — utiliser Python plutôt que `sed` (Unicode + regex multi-lignes) :

```python
import glob
OLD = '...'
NEW = '...'
for p in glob.glob('*.html'):
    if p == 'design1.html': continue
    s = open(p, encoding='utf-8').read()
    open(p, 'w', encoding='utf-8').write(s.replace(OLD, NEW))
```

**Recroper le blason** depuis `marceau-banner.jpg` (5291×756) :

```bash
cp assets/logos/marceau-banner.jpg assets/logos/blason-marceau.jpg
sips --cropToHeightWidth 700 700 --cropOffset 0 1200 assets/logos/blason-marceau.jpg
sips -Z 300 assets/logos/blason-marceau.jpg
```

**Tester en local** : pas de build, ouvrir `index.html` directement dans un navigateur (ou `python3 -m http.server` à la racine si on veut tester les liens sans `.html`).

## Pièges à éviter

- Ne pas remettre `.html` dans les `href` internes (l'utilisateur les a fait retirer).
- Ne pas amender `design1.html` (référence de design d'origine).
- Ne pas centraliser le contenu dans `index` — chaque thème a sa page.
- Ne pas changer les classes CSS sans mettre à jour les 10 pages qui les consomment.
- Le menu mobile fonctionne via `onclick` inline qui toggle `.nav-links.open` — pas de framework JS, garder ça simple.
