# SPEC TECHNIQUE — Site Web "Les Petits Pots"
## Document de référence pour agent de développement

---

## 1. IDENTITÉ VISUELLE

### Palette de couleurs (variables CSS)
```css
--creme:       #F5F0E8;   /* fond principal, chaud et doux */
--noir:        #1A1A1A;   /* texte principal, logo */
--rose-vif:    #FF3CAC;   /* accent fort — titres séries humoristiques */
--rose-doux:   #F2A7C3;   /* accent secondaire, hover états */
--beige-fonce: #D4C4A8;   /* séparateurs, fonds de cartes */
--bleu-poussiere: #8FA5B2; /* accent froid occasionnel */
--texte-muted: #6B5E52;   /* corps de texte secondaire */
```

### Typographie
Charger via Google Fonts :
- **DM Serif Display** → titres émotionnels/doux (italic disponible)
- **Bebas Neue** → mots forts/chocs/series names
- **Lora** → corps de texte, descriptifs

Règle d'or : chaque titre doit mixer les deux display fonts.
Exemple : "La pire" en DM Serif Display italic + "RUPTURE" en Bebas Neue.

### Texture de fond
Appliquer un grain SVG subtil sur le fond crème pour effet "papier" :
```css
background-image: url("data:image/svg+xml,..."); /* noise filter */
```

---

## 2. STRUCTURE DE LA PAGE (ordre vertical)

```
[HERO]
[HIGHLIGHTS DE L'ANNÉE]   ← contrôlé par highlights.csv
[SÉRIES / REELS]          ← contrôlé par series.csv
[LIENS EXTERNES]          ← contrôlé par liens.csv
[FOOTER]
```

---

## 3. SECTION HERO

### Contenu
- Logo "LES PETITS POTS" (texte stylisé, pas d'image)
- Tagline : *"ta safe place et ton média doudou qui t'accompagne dans ta rupture 💔"*
- Sous-tagline : "Interviews · Psys · Conseils"
- Bouton CTA : "Nous suivre sur Instagram" → lien externe

### Design
- Fond : crème (#F5F0E8) avec grain papier
- Logo : Bebas Neue, très grand (clamp 60px → 120px), noir
- "petits" en DM Serif Display italic, taille plus petite, décalé vers le bas (overlap typographique)
- Tagline : Lora italic, taille medium, couleur texte-muted
- Animation d'entrée : les mots du logo tombent un par un avec un léger rebond (stagger 150ms, transform: translateY(-30px) → 0, easing bounce)
- Un cœur brisé animé tourne lentement en arrière-plan, très transparent (opacity 0.04), grand format

### Élément décoratif
Ligne ondulée SVG horizontale (trait fin rose-doux) sépare le hero du reste.

---

## 4. SECTION HIGHLIGHTS DE L'ANNÉE

### Source de données
Fichier : `highlights.csv`

### Structure CSV (en-têtes en français)
```csv
emoji,titre,description,couleur_accent
💔,La pire rupture de Kemmler,Notre épisode le plus regardé de l'année avec + de 50k vues,#FF3CAC
🎙️,Cœur à cœur — saison 2,8 épisodes de confessions intimes avec des invités surprises,#F2A7C3
🌍,Seoul & rupture,Notre premier épisode filmé à l'étranger — Corée du Sud,#8FA5B2
```

### Design des cartes
- Layout : grille 3 colonnes sur desktop, 1 colonne sur mobile
- Chaque carte :
  - Fond blanc cassé avec légère ombre portée douce
  - Emoji grand format en haut (64px), légèrement rotaté aléatoirement (-3° à +3°)
  - Titre en DM Serif Display, noir
  - Description en Lora, texte-muted
  - Bordure gauche épaisse (4px) de la couleur couleur_accent du CSV
  - Au hover : légère élévation (transform: translateY(-4px)), transition 200ms ease
- Titre de section : "✦ l'année en quelques moments" — DM Serif Display italic, centré, taille large

---

## 5. SECTION SÉRIES / REELS

### Source de données
Fichier : `series.csv`

### Structure CSV
```csv
nom_serie,description_courte,lien_instagram,image_miniature,couleur_label
La pire rupture de…,Des célébrités racontent leur pire rupture,https://instagram.com/reel/xxx,img/rupture.jpg,#FF3CAC
La parole aux ZOMMES,Les hommes parlent d'amour enfin,https://instagram.com/reel/xxx,img/zommes.jpg,#FF3CAC
T'as 2 min pour parler d'amour?,Micro-trottoir émotionnel,https://instagram.com/reel/xxx,img/2min.jpg,#8FA5B2
Ouin-ouin académie,Humor & auto-dérision post-rupture,https://instagram.com/reel/xxx,img/ouinouin.jpg,#FF3CAC
Micro rupture,Pourquoi tu ghostes?,https://instagram.com/reel/xxx,img/micro.jpg,#D4C4A8
Cœur à cœur,Confessions intimes en podcast,https://instagram.com/reel/xxx,img/coeur.jpg,#F2A7C3
```

### Design
- Layout : scroll horizontal sur mobile (overflow-x: auto, snap), grille 3 colonnes sur desktop
- Chaque carte série :
  - Image miniature en format 9:16 (portrait), border-radius 12px
  - Si pas d'image : fond dégradé crème → beige-fonce avec le nom en grand Bebas Neue centré
  - Label coloré en haut gauche de l'image : nom de série en Bebas Neue, fond couleur_label, texte blanc
  - Description en Lora italic en dessous
  - Bouton "Voir les épisodes →" : lien vers lien_instagram, style minimaliste (underline animée au hover)
- Titre de section : "SÉRIES" en Bebas Neue très grand + "& reels" en DM Serif Display italic en dessous, légèrement décalé à droite

### Animation
- Les cartes apparaissent avec un Intersection Observer : fade-in + translateY(20px) → 0 quand elles entrent dans le viewport, stagger de 100ms entre chaque carte

---

## 6. SECTION LIENS EXTERNES

### Source de données
Fichier : `liens.csv`

### Structure CSV
```csv
titre,description,url,categorie,emoji
Notre podcast Spotify,Tous les épisodes audio disponibles,https://spotify.com/xxx,Audio,🎧
Notre chaîne YouTube,Interviews longue durée,https://youtube.com/xxx,Vidéo,▶️
Article Le Monde — ruptures,Un article qui nous a inspirés,https://lemonde.fr/xxx,Lecture,📖
Marie Tattu — psychologue,Notre psy partenaire,https://xxx.com,Partenaire,🤝
```

### Design
- Layout : liste verticale avec séparateurs fins (1px beige-fonce)
- Chaque lien :
  - Emoji à gauche (40px)
  - Titre en DM Serif Display + catégorie en Bebas Neue petit, couleur rose-vif, sur la même ligne
  - Description en Lora, texte-muted, en dessous
  - Flèche → à droite qui se déplace de +4px au hover
  - L'ensemble est cliquable (balise `<a>` sur toute la rangée)
  - Hover : fond passe légèrement à beige-fonce, transition douce
- Titre de section : "par ici aussi 👇" — DM Serif Display italic, taille medium, pas de majuscules

---

## 7. FOOTER

- Logo "LES PETITS POTS" répété en petit, Bebas Neue
- Tagline courte : *"média doudou • fait avec 💔"*
- Lien Instagram
- Mention : "© 2025 Les Petits Pots"
- Fond noir, texte crème — contraste avec le reste de la page

---

## 8. COMPORTEMENTS GLOBAUX & ANIMATIONS

### Chargement CSV
- Utiliser `fetch()` + `PapaParse` (CDN) pour parser les 3 CSV au chargement de la page
- Chaque section se rend dynamiquement via du JavaScript vanilla (innerHTML)
- Si un CSV est absent ou vide, la section affiche un message : *"Bientôt disponible 💔"*

### Animations globales
| Élément | Animation |
|---|---|
| Logo hero | Lettres tombent en stagger (translateY + opacity) |
| Cœur background hero | Rotation lente continue (360deg, 20s, linear, infinite) |
| Cartes highlights | Élévation au hover |
| Cartes séries | Fade + slide-up au scroll (IntersectionObserver) |
| Liens externes | Flèche glisse à droite au hover |
| Ligne ondulée SVG | Dessin progressif (stroke-dashoffset animation) |

### Curseur custom (optionnel)
Remplacer le curseur par un petit cœur brisé SVG en CSS.

### Responsive breakpoints
- Mobile : < 768px → 1 colonne partout, scroll horizontal pour séries
- Tablet : 768–1024px → 2 colonnes highlights
- Desktop : > 1024px → 3 colonnes

---

## 9. FICHIERS À CRÉER

```
/
├── index.html          ← page principale
├── highlights.csv      ← données highlights
├── series.csv          ← données séries
├── liens.csv           ← données liens externes
└── img/                ← miniatures séries (optionnel)
```

---

## 10. DÉPENDANCES CDN (aucun build tool requis)

```html
<!-- Fonts -->
<link href="https://fonts.googleapis.com/css2?family=DM+Serif+Display:ital@0;1&family=Bebas+Neue&family=Lora:ital,wght@0,400;0,600;1,400&display=swap" rel="stylesheet">

<!-- CSV Parser -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/PapaParse/5.4.1/papaparse.min.js"></script>
```

Aucun framework JS. HTML/CSS/JS vanilla uniquement.

---

## 11. NOTES DE TON POUR L'AGENT

- Ne pas sur-produire : le charme vient du côté brut et humain
- Éviter les effets trop "corporate" ou trop lisses
- Les textes d'exemple dans les CSV sont en français, conserver cette langue partout
- Le fond crème + grain papier est NON NÉGOCIABLE — c'est le fondement esthétique
- Les deux fonts display (Bebas + DM Serif) doivent apparaître ensemble dans chaque titre de section
- Pas de Bootstrap, pas de Tailwind — CSS custom variables uniquement
