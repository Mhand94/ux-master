# Socle commun : lois cognitives, accessibilité, plateformes

Ce socle s'applique quelle que soit la lentille. Il contient les **seuils chiffrés** que SKILL.md résume, avec leur justification et leur application concrète.

---

## 1. Lois cognitives

| Loi | Énoncé | Application concrète | Signe d'alerte |
|---|---|---|---|
| **Hick** | Le temps de décision croît avec le nombre et la complexité des choix | Une action principale par écran ; 3 à 5 options visibles au plus ; le reste derrière « Plus » ; filtres progressifs plutôt que simultanés | Trois boutons de même poids ; menu de douze entrées ; formulaire aux quinze champs d'un coup |
| **Fitts** | Le temps pour atteindre une cible dépend de sa taille et de sa distance | Cibles ≥ 44 × 44 pt (iOS) / 48 × 48 dp (Android) / 24 × 24 px minimum WCAG, 44 px recommandé (web) ; action principale dans la zone du pouce (tiers inférieur de l'écran sur mobile) ; actions destructrices éloignées des actions courantes | Icône de 20 px sans zone de toucher élargie ; bouton principal en haut à droite sur mobile ; « Supprimer » collé à « Enregistrer » |
| **Charge cognitive (Miller, Sweller)** | La mémoire de travail est limitée à quelques éléments ; tout effort inutile dégrade la performance | Rien à mémoriser entre deux écrans ; blocs de 3 à 5 éléments ; une décision à la fois ; récapitulatif avant validation | Code à retenir ; instruction donnée plus tôt ; vingt lignes de densité égale |
| **Jakob** | Les utilisateurs passent l'essentiel de leur temps ailleurs ; ils attendent que votre produit fonctionne comme les autres | Conventions de plateforme ; schémas connus (tab bar, carte, liste et détail, swipe) ; icônes universelles | Geste inventé, navigation originale, icône maison pour une fonction standard |
| **Tesler (complexité irréductible)** | Toute tâche a une complexité minimale ; elle est portée soit par le système, soit par l'utilisateur | Le système déduit (position, date, valeurs par défaut), préremplit, calcule ; l'utilisateur confirme | L'utilisateur saisit ce que le système sait déjà ; il convertit, trie ou calcule à la main |
| **Doherty** | Sous 400 ms de réponse, l'utilisateur reste engagé ; au-delà, l'attention décroche | Feedback immédiat (état pressé) ; indicateur si > 400 ms ; squelette ou mise à jour optimiste si > 1 s ; estimation ou progression si > 3 s ; jamais d'écran blanc | Tap sans réaction ; indicateur sans texte au-delà de trois secondes ; attente avant d'afficher quoi que ce soit |
| **Pic et fin (Kahneman)** | Le souvenir d'une expérience est dominé par son moment le plus intense et par sa fin | Soigner le moment magique (premier résultat utile) et la clôture de chaque parcours (confirmation claire, suite proposée) | Parcours qui se termine sur un écran vide ou technique ; succès non célébré, échec non accompagné |
| **Zeigarnik et progression** | Une tâche entamée et visiblement inachevée pousse à la terminer | Jauge de complétion, étapes numérotées, brouillon sauvegardé automatiquement | Saisie perdue à la fermeture ; aucune idée du nombre d'étapes restantes |
| **Von Restorff (isolation)** | L'élément qui se distingue est celui qu'on remarque et retient | Un seul élément visuellement distinct par écran : l'action principale | Plusieurs éléments en couleur d'accent ; la couleur d'action utilisée en décoration |
| **Postel (robustesse)** | Être tolérant sur ce qu'on accepte, strict sur ce qu'on produit | Accepter les espaces, majuscules et formats variés dans les saisies ; normaliser côté système | Refus d'un numéro de téléphone à cause d'un espace ; date exigée dans un seul format |

---

## 2. Accessibilité : le minimum non négociable (WCAG 2.1 niveau AA)

Un problème d'accessibilité est au moins de sévérité 3, et de sévérité 4 s'il exclut un groupe entier (par exemple, aucune cible n'a de libellé pour lecteur d'écran).

| Critère | Seuil | Comment vérifier |
|---|---|---|
| **Contraste du texte** | ≥ 4,5:1 pour le texte normal ; ≥ 3:1 pour le texte large (≥ 24 px, ou ≥ 19 px en gras) | Calculer avec les vraies couleurs du design system (outil de contraste). Un gris `#8A8A8A` sur blanc fait environ 3,3:1 : il échoue pour du texte normal |
| **Contraste des composants** | ≥ 3:1 pour les bordures de champs, icônes porteuses de sens, indicateurs de focus | Idem, sur l'élément et son fond |
| **Couleur seule** | Jamais la seule façon de porter une information | Chaque état coloré a aussi une forme, une icône ou un texte (rouge + icône + « Erreur ») |
| **Taille des cibles** | ≥ 24 × 24 px (minimum WCAG 2.2) ; viser 44 × 44 pt / 48 × 48 dp | Mesurer la zone réellement touchable, padding inclus |
| **Libellés** | Toute icône seule a un libellé accessible ; tout champ a un label visible ou accessible | Lecteur d'écran (VoiceOver, TalkBack) : chaque élément est annoncé avec son rôle et son nom |
| **Redimensionnement du texte** | L'interface reste utilisable à 200 % (web) et avec Dynamic Type / échelle système (mobile) | Activer la plus grande taille système ; rien ne doit se couper ni se chevaucher |
| **Focus visible** (web) | L'élément focalisé est toujours identifiable | Parcourir l'écran au clavier avec Tab ; l'anneau de focus est visible partout |
| **Clavier** (web) | Toute fonction est accessible au clavier : Tab, Entrée, Espace, Échap, flèches | Faire la tâche principale sans souris |
| **Erreurs** | L'erreur est identifiée, décrite en texte, reliée au champ, avec une suggestion | `aria-describedby` vers le message ; message près du champ |
| **Messages d'état** | Les changements (succès, chargement terminé) sont annoncés sans déplacer le focus | `role="status"` ou `aria-live="polite"` sur web ; `accessibilityLiveRegion` sur Android |
| **Mouvement** | Les animations non essentielles respectent `prefers-reduced-motion` ; aucune animation clignotante | Activer la réduction des animations dans le système et vérifier |
| **Langue** | `lang` sur `<html>` ; langue déclarée pour la synthèse vocale | Inspecter le document |
| **Ordre de lecture** | L'ordre du DOM ou de la hiérarchie des vues suit l'ordre visuel | Lecteur d'écran : l'ordre d'annonce est logique |

---

## 3. Règles par plateforme

### iOS (Human Interface Guidelines)

- **Cibles** : 44 × 44 pt minimum.
- **Navigation** : barre d'onglets en bas, 3 à 5 onglets, toujours visible dans les sections principales ; pile de navigation avec bouton Retour **et** geste de balayage depuis le bord gauche, les deux toujours fonctionnels.
- **Modalité** : feuilles (sheets) pour les tâches ponctuelles et autonomes, fermeture par glissement vers le bas et bouton explicite ; ne pas empiler les modales.
- **Actions destructrices** : en rouge, dans une feuille d'action ou avec confirmation ; jamais à côté de l'action courante.
- **Grands titres** : titre de section en haut, qui se réduit au défilement.
- **Rafraîchir** : tirer pour rafraîchir sur les listes de contenu.
- **Texte** : Dynamic Type respecté ; SF Pro ou police de marque avec échelle équivalente.
- **Haptique** : légère et rare, pour confirmer une action significative (épingle, succès), jamais pour chaque tap.
- **Permissions** : demander au moment du besoin, après avoir expliqué pourquoi, jamais au premier lancement.
- **À éviter** : menu hamburger quand une tab bar suffit ; boutons « retour » personnalisés ; onglets dupliquant la navigation système.

### Android (Material 3)

- **Cibles** : 48 × 48 dp minimum, espacement ≥ 8 dp entre cibles.
- **Retour** : le bouton ou geste Retour système fonctionne toujours et fait ce que l'utilisateur attend (fermer la modale, revenir à l'écran précédent, jamais quitter l'app sans prévenir depuis un écran profond).
- **Navigation** : barre de navigation en bas, 3 à 5 destinations ; tiroir de navigation seulement au-delà ; barre supérieure avec titre et actions.
- **Action principale** : bouton d'action flottant (FAB) pour l'action de création principale d'un écran, un seul par écran.
- **Feedback** : snackbar en bas, 4 à 10 secondes, avec action Annuler quand c'est pertinent ; dialogues réservés aux décisions.
- **Texte** : échelle de police système respectée ; Roboto ou police de marque.
- **Affichage bord à bord** : respecter les encoches et la barre de navigation (insets).
- **Permissions** : demander en contexte ; gérer le refus définitif en guidant vers les réglages.
- **À éviter** : copier les motifs iOS (bouton Retour dans la barre à gauche sans gestion du Retour système, feuilles iOS) ; ignorer le thème sombre système.

### Web et PC

- **Sémantique** : `<button>` pour agir, `<a href>` pour naviguer ; jamais de `div` ou `span` cliquable.
- **Clavier** : Tab suit l'ordre visuel ; Entrée et Espace activent ; Échap ferme ; flèches dans les listes et onglets ; raccourcis affichés pour les habitués (posture souveraine).
- **Focus** : visible partout ; `:focus-visible` plutôt que suppression de l'outline.
- **Survol** : le survol enrichit, il ne révèle jamais seul une action (un bouton qui n'apparaît qu'au survol est invisible au clavier et au tactile).
- **Formulaires** : label visible lié au champ ; erreur près du champ ; validation à la sortie du champ ou à la soumission, pas à chaque frappe ; bouton de soumission unique.
- **Lecture** : 60 à 80 caractères par ligne ; 16 px minimum pour le corps ; interligne 1,4 à 1,6.
- **Responsive** : fonctionne de 320 px à 1440 px et au-delà ; les panneaux latéraux deviennent des tiroirs sous 1024 px ; les tableaux larges défilent dans un conteneur ; aucun défilement horizontal de la page.
- **Performance** (Core Web Vitals) : LCP < 2,5 s ; INP < 200 ms ; CLS < 0,1. Au-delà, les utilisateurs partent avant d'avoir vu l'interface.
- **États de route** : pages de chargement, d'erreur et 404 conçues (pas celles par défaut du framework).
- **Modales** : `role="dialog"`, `aria-modal`, focus déplacé dans la modale à l'ouverture et rendu à l'origine à la fermeture, Échap ferme.
- **Mouvement** : `prefers-reduced-motion` respecté.
- **Impression et export** : si l'écran produit un document, prévoir sa mise en page imprimée.

### Du mobile au PC : adapter, pas recopier

| Sur mobile | Sur PC |
|---|---|
| Un élément à la fois (carte, swipe) | Grille ou liste comparée, panneau de détail à côté |
| Geste | Clic, raccourci clavier, survol enrichi |
| Filtres dans un tiroir | Filtres visibles en colonne |
| Tab bar | Navigation horizontale ou latérale |
| Modale plein écran | Panneau latéral ou dialogue centré |
| Action sous le pouce | Action en haut du contenu ou à droite du panneau |

La logique métier et les données ne changent pas ; seule la présentation s'adapte à la posture (transitoire sur mobile, souveraine sur PC).
