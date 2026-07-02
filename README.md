# DeutschMeister · Allemand A1

Plateforme web d'apprentissage de l'allemand niveau **A1** (Goethe / CECRL).
100 % local : ouvre simplement `index.html` dans ton navigateur. Aucun serveur requis.

---

## 🚀 Lancement
1. Garde **tous les fichiers dans la même arborescence** (voir ci-dessous).
2. Double-clique sur `index.html` (ou ouvre-le dans Chrome / Edge / Firefox).
3. C'est tout. La progression est sauvegardée automatiquement (LocalStorage).

> 🔊 **Audio** : la prononciation utilise la synthèse vocale du navigateur (Web Speech API),
> voix allemande **de-DE**. Aucun fichier audio n'est nécessaire. (Chrome/Edge donnent les meilleures voix.)

---

## 📁 Architecture
```
deutsch-a1/
├── index.html              ← coquille + ordre de chargement des scripts
├── css/
│   ├── tokens.css          ← design tokens (couleurs, espacements, thèmes clair/sombre)
│   └── app.css             ← reset, layout, composants, animations, responsive
├── js/
│   ├── utils.js            ← helpers DOM, icônes SVG, synthèse vocale, confettis  (window.U)
│   ├── store.js            ← état global + LocalStorage + XP/streak/favoris       (window.Store)
│   ├── router.js           ← navigation par hash (#/route)                        (window.Router)
│   ├── data/
│   │   ├── registry.js     ← registre des contenus                               (window.A1)
│   │   └── deck-01-begruessung.js  ← module de vocabulaire #1
│   ├── views/
│   │   ├── dashboard.js    ← tableau de bord
│   │   ├── vocabulary.js   ← liste des decks + cartes de mots
│   │   └── placeholder.js  ← écrans « à venir » (grammaire, exercices, quiz…)
│   └── app.js              ← démarrage : construit l'UI et lance le routeur       (window.App)
└── README.md
```

---

## 🧩 Comment ÉTENDRE (pour les étapes suivantes)

### Ajouter un module de vocabulaire
1. Crée `js/data/deck-02-xxx.js` qui appelle `A1.registerDeck({ id, title, de, icon, color, words: [...] })`.
2. Ajoute une ligne dans `index.html` :
   `<script src="js/data/deck-02-xxx.js"></script>` (après le registre).
   → Le deck apparaît automatiquement dans le Vocabulaire. **Rien d'autre à modifier.**

Schéma d'un mot :
```js
{ id, de, art:'m|f|n|', plural, ipa, fr, ar, ex, exFr, tip, freq }
```

### Ajouter une vue / un module (grammaire, exercices, quiz…)
1. Crée `js/views/xxx.js` qui appelle `Router.register('route', { title, render })`.
2. Ajoute son `<script>` dans `index.html`.
   → La route devient active. (Les routes sont déjà câblées dans la barre latérale.)

---

## ✅ État d'avancement (feuille de route)
- [x] **Étape 1** — Architecture, design system, moteur (store/router/thème), coquille, tableau de bord, module Vocabulaire fonctionnel + deck #1.
- [x] **Étape 2** — Composant carte partagé (`WC`), recherche intelligente, favoris / à revoir, + modules **Nombres** et **Famille** (decks #2 et #3).
- [x] **Étape 3** — Moteur d'exercices : QCM (sens), articles (der/die/das), textes à trous, **association** et **dictée audio**, avec correction automatique, score, XP et confettis.
- [x] **Étape 4** — Système de quiz : **examen blanc Goethe A1** (20 questions mixtes, seuil 60 %) + **quiz chronométrés par thème**, minuteur, meilleurs scores enregistrés, XP & récompenses.
- [x] **Contenu (en cours)** — Schéma de mot **enrichi** (synonymes, antonymes, collocations, préposition, erreur fréquente, note de grammaire, exemples, mini-dialogue) + **fiche détaillée** dépliable. Thèmes ajoutés : Maison, Nourriture & boissons, Couleurs. Objectif : 1800–2500 mots couvrant tous les thèmes officiels.
- [ ] Puis : grammaire A1 interactive, dialogues de la vie quotidienne, situations réelles, exercices avancés, examen blanc complet, révision générale.

### 🧩 Ajouter un thème de vocabulaire (rappel)
Crée `js/data/deck-XX-theme.js` → `A1.registerDeck({...})`, ajoute son `<script>` dans `index.html`. Le thème apparaît partout (vocabulaire, recherche, exercices, quiz, progression) automatiquement. Champs d'un mot : `id, de, art, plural, ipa, fr, ar, ex, exFr, tip, freq` + optionnels `syn, ant, coll, prep, err, note, ex2, ex2Fr, dialog`.

---

*Conçu pour Nouha — vers le B2, une étape à la fois.* 🇩🇪
