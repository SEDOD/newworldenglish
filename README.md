# New World English Center (NWEC)

Site vitrine statique de **New World English Center**, centre de formation spécialisé dans l’apprentissage et le perfectionnement de l’anglais.

Le projet utilise uniquement :

- **HTML** pour la structure des pages ;
- **CSS** pour le design, les couleurs et la responsivité ;
- **JavaScript** pour les interactions ;
- **JFIF** pour le logo officiel fourni.

Il n’y a pas de backend, de base de données, de framework ou de dépendance à installer.

## Fonctionnalités

- Page d’accueil en anglais par défaut ;
- Traduction instantanée anglais/français avec les boutons `EN` et `FR` ;
- Mode clair/sombre avec le bouton `☾` / `☀` ;
- Mémorisation du thème sombre dans le navigateur avec `localStorage` ;
- Menu hamburger sur téléphone et tablette ;
- Bouton WhatsApp flottant ;
- Bouton de retour automatique en haut de page après défilement ;
- Formulaire de contact qui prépare un email avec `mailto:` ;
- Sections de présentation, offres, avantages, entreprises et contact ;
- Footer complet avec les coordonnées de NWEC ;
- Design responsive pour ordinateur, tablette et téléphone.

## Arborescence

```text
new-world-english/
├── index.html   # Structure et contenu de la page
├── style.css    # Mise en forme, responsive et dark mode
├── script.js    # Traduction, interactions et formulaire
├── logo.jfif    # Logo officiel de New World English Center
└── README.md    # Documentation du projet
```

## 1. Structure de `index.html`

Le fichier HTML est le point d’entrée du site.

### En-tête

La section `<header>` contient :

- le logo NWEC ;
- la navigation vers les différentes sections ;
- le bouton d’inscription ;
- le bouton du menu mobile ;
- le bouton de dark mode ;
- les boutons de langue `EN` et `FR`.

Les textes traduisibles utilisent l’attribut `data-i18n`, par exemple :

```html
<a href="#offers" data-i18n="navOffers">Our offers</a>
```

JavaScript identifie ensuite la clé `navOffers` et remplace le texte selon la langue sélectionnée.

### Section d’accueil

La section `.hero` présente :

- le nom de NWEC ;
- le slogan principal ;
- une description du centre ;
- les boutons d’action ;
- une carte de contact rapide avec le logo.

### Section À propos

La section `#about` explique la mission de NWEC et son objectif : développer des compétences solides en anglais et les utiliser avec confiance.

### Section Nos offres

La section `#offers` est remplie dynamiquement par JavaScript. Elle présente :

- l’anglais parlé ;
- l’anglais professionnel ;
- les cours à domicile ;
- la préparation aux examens, concours et bourses ;
- le coaching linguistique ;
- la traduction certifiée ;
- l’interprétation multilingue.

### Section Pourquoi NWEC

La section `#why` présente les principaux avantages :

- approche flexible ;
- pratique immersive ;
- niveau adapté ;
- présentiel ou distance ;
- accompagnement personnalisé.

### Section entreprises

La section `#business` présente les formations sur mesure pour les équipes de **2 à 12 personnes**.

### Formulaire

La section `#register` contient un formulaire avec :

- prénom ;
- nom ;
- email ;
- téléphone ou WhatsApp ;
- objectif ;
- consentement au contact.

Le formulaire n’enregistre pas les données sur un serveur. JavaScript prépare un email et ouvre l’application email du visiteur avec `mailto:`.

### Footer

Le footer contient :

- le logo NWEC ;
- un résumé de l’activité ;
- les liens principaux ;
- le numéro `01 61 89 11 97` ;
- l’adresse `newworldenglishcenter4@gmail.com` ;
- les informations d’activité et de taille d’entreprise.

## 2. Structure de `style.css`

### Variables globales

Les couleurs principales sont regroupées dans `:root` :

```css
:root {
  --ink: #102746;
  --navy: #0a2345;
  --blue: #1e63c9;
  --sky: #eaf3ff;
  --muted: #66788f;
  --line: #dce6f1;
  --bg: #f5f8fc;
  --card: #fff;
}
```

Cela permet de modifier rapidement l’identité visuelle du site.

### Mise en page

Le CSS définit notamment :

- la largeur maximale `.container` ;
- la grille de la page d’accueil ;
- les cartes ;
- les boutons ;
- la navigation ;
- les sections ;
- le footer ;
- les éléments flottants WhatsApp et retour en haut.

### Responsive design

Deux points de rupture principaux sont utilisés :

- `950px` : passage vers le menu hamburger et réorganisation des colonnes ;
- `600px` : affichage mobile, cartes sur une colonne et footer réorganisé.

Exemple :

```css
@media (max-width: 950px) {
  .hero-grid {
    grid-template-columns: 1fr;
  }
}
```

### Dark mode

Le dark mode est activé par la classe suivante :

```css
body.dark-mode {
  --bg: #0c1b31;
  --card: #122844;
  --ink: #edf4ff;
}
```

Le JavaScript ajoute ou retire cette classe sur `<body>`.

## 3. Structure de `script.js`

### Sélecteur DOM

Le raccourci suivant permet de sélectionner rapidement un élément :

```js
const $ = selector => document.querySelector(selector);
```

### Traductions

Les traductions sont regroupées dans l’objet `data` :

```js
const data = {
  en: { ... },
  fr: { ... }
};
```

Chaque texte possède une clé commune entre l’anglais et le français. La fonction `updateLanguage()` :

1. parcourt les éléments avec `data-i18n` ;
2. récupère la traduction correspondante ;
3. remplace le contenu ;
4. actualise l’attribut `lang` du document.

### Cartes dynamiques

Les offres et les avantages sont générés avec :

- `renderCards()` pour les offres et les avantages ;
- les tableaux `offers` et `why` dans les traductions.

Cela évite de dupliquer la même structure HTML pour chaque langue.

### Dark mode

Le thème est mémorisé ainsi :

```js
let theme = localStorage.getItem('nwe_theme') || 'light';
```

Quand l’utilisateur clique sur le bouton :

1. le thème passe de `light` à `dark` ou inversement ;
2. la classe `dark-mode` est appliquée au `<body>` ;
3. le choix est enregistré dans le navigateur ;
4. l’icône passe de `☾` à `☀`.

### Menu mobile

Le bouton `#menuToggle` ajoute ou retire la classe `.open` sur `#navLinks`. Le CSS affiche la navigation uniquement lorsque cette classe existe sur petit écran.

### Retour en haut

Le bouton `#backTop` devient visible lorsque l’utilisateur dépasse 300 pixels de défilement :

```js
window.addEventListener('scroll', () => {
  top.classList.toggle('visible', window.scrollY > 300);
});
```

Son clic utilise un défilement animé vers le haut de la page.

### Formulaire

La fonction `mailLink()` prépare un lien `mailto:` contenant les données saisies. L’adresse utilisée est :

```js
const CONTACT_EMAIL = 'newworldenglishcenter4@gmail.com';
```

Pour un formulaire réellement stocké automatiquement, il faudra plus tard connecter un service externe comme Formspree, Google Forms ou un backend.

## Lancer le site en local

Aucune installation n’est nécessaire. Depuis le dossier du projet, utilisez l’une des méthodes suivantes.

### Méthode simple

Double-cliquez sur `index.html`.

### Avec Python

```bash
python3 -m http.server 3000
```

Puis ouvrez :

```text
http://localhost:3000
```

### Avec VS Code

1. Installez l’extension **Live Server** ;
2. ouvrez le dossier du projet ;
3. cliquez droit sur `index.html` ;
4. choisissez **Open with Live Server**.

## Mettre le projet sur GitHub

### 1. Créer un dépôt GitHub

1. Connectez-vous à [github.com](https://github.com) ;
2. cliquez sur **New repository** ;
3. donnez un nom, par exemple `new-world-english-center` ;
4. choisissez `Public` si le site doit être visible par tous ;
5. ne cochez pas forcément l’ajout automatique d’un README, puisque ce projet en contient déjà un ;
6. cliquez sur **Create repository**.

### 2. Ouvrir un terminal dans le projet

Placez-vous dans le dossier qui contient les cinq fichiers :

```bash
cd chemin/vers/new-world-english-html-css-js
```

### 3. Initialiser Git

```bash
git init
git add index.html style.css script.js logo.jfif README.md
git commit -m "Create NWEC static website"
git branch -M main
```

### 4. Relier le dépôt distant

Remplacez `VOTRE_NOM` et `new-world-english-center` par vos informations :

```bash
git remote add origin https://github.com/VOTRE_NOM/new-world-english-center.git
git push -u origin main
```

GitHub peut demander votre authentification. Utilisez GitHub Desktop ou un Personal Access Token si votre mot de passe classique est refusé.

## Publier gratuitement avec GitHub Pages

1. Ouvrez le dépôt sur GitHub ;
2. allez dans **Settings** ;
3. cliquez sur **Pages** dans le menu de gauche ;
4. dans **Build and deployment**, choisissez `Deploy from a branch` ;
5. choisissez la branche `main` et le dossier `/ (root)` ;
6. cliquez sur **Save** ;
7. attendez quelques instants.

GitHub affichera ensuite une adresse similaire à :

```text
https://VOTRE_NOM.github.io/new-world-english-center/
```

## Mettre à jour le site après une modification

Après avoir modifié un fichier :

```bash
git add .
git commit -m "Update NWEC website"
git push
```

GitHub Pages republiera automatiquement la nouvelle version.

## Modifier les coordonnées

Les coordonnées principales se trouvent dans `index.html` et `script.js`.

Coordonnées actuelles :

- Téléphone / WhatsApp : `01 61 89 11 97` ;
- lien WhatsApp international : `https://wa.me/2290161891197` ;
- email : `newworldenglishcenter4@gmail.com`.

Pour WhatsApp, le préfixe international `229` est conservé dans le lien afin que le bouton fonctionne correctement.

## Licence

Projet créé pour **New World English Center (NWEC)**. Le logo et les contenus de marque appartiennent à NWEC.
