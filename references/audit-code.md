# Auditer l'UX dans le code (React Native / Expo, Next.js)

Le code révèle une partie des problèmes UX avant tout test : cibles trop petites, absence de feedback, états non gérés, accessibilité oubliée, valeurs en dur. Ce fichier donne les **motifs à rechercher**, le problème UX qu'ils signalent, la catégorie et la correction type, puis les **commandes `rg`** pour les trouver vite.

Règles :

- Un motif trouvé est un **indice**, pas un verdict : ouvrir le composant et confirmer avant de consigner.
- Le code ne dit pas tout : contraste réel, taille réelle à l'écran, fluidité, ressenti des animations se vérifient sur appareil (section 5).
- Chaque constat confirmé devient un ticket Claude Code (`templates/ticket-claude-code.md`), un par constat, avec le chemin du fichier.

---

## 1. Lecture d'un composant en dix points

Avant de chercher des motifs, lire chaque composant d'écran avec cette grille :

1. **Rôle** : quelle tâche de l'utilisateur ce composant sert-il ? Une seule ?
2. **Action principale** : un seul élément dominant ? Visible sans défilement ?
3. **États** : vide, chargement, erreur, succès, première fois, hors ligne, permission refusée. Lesquels sont codés ?
4. **Feedback** : chaque gestionnaire d'événement produit-il un changement visible immédiat (état pressé, désactivation, indicateur) ?
5. **Annuler** : les actions réversibles ont-elles un chemin de retour ? Les irréversibles une confirmation ?
6. **Accessibilité** : rôles, libellés, ordre de focus, taille des cibles, contraste par les tokens.
7. **Tokens** : couleurs, espacements, tailles viennent-ils du design system ou sont-ils en dur ?
8. **Micro-textes** : libellés, messages d'erreur, états vides sont-ils écrits, dans le vocabulaire de l'utilisateur, ou laissés par défaut ?
9. **Mesure** : l'action principale émet-elle un événement analytics ?
10. **Performance perçue** : listes virtualisées, images avec placeholder, mises à jour optimistes, pas de recalcul coûteux au rendu.

---

## 2. React Native / Expo : motifs à rechercher

| Motif dans le code | Problème UX probable | Cat. | Correction type |
|---|---|---|---|
| `Pressable` ou `Touchable*` dont l'enfant est une icône seule, sans `accessibilityLabel` | Lecteur d'écran muet ; bouton anonyme | ACC | Ajouter `accessibilityLabel` et `accessibilityRole="button"` |
| `onPress` sur `<Text>` ou `<View>` | Pas de rôle, pas d'état pressé, cible imprécise | ACT | Remplacer par `Pressable` avec style d'état pressé |
| Pressable avec `height` ou `padding` donnant moins de 44 pt, sans `hitSlop` | Cible trop petite (Fitts) | ACC | `minHeight: 44`, `minWidth: 44` ou `hitSlop={{ top: 8, bottom: 8, left: 8, right: 8 }}` |
| `Alert.alert(` pour confirmer une action réversible | Confirmation inutile, friction, s'automatise | ERR | Exécuter puis proposer Annuler (snackbar ou toast avec action) |
| `Alert.alert(` pour signaler un succès | Interruption pour une information banale | FBK | Feedback en place (changement d'état, toast court) |
| `FlatList` ou `FlashList` sans `ListEmptyComponent` | Écran vide non conçu | ETA | Composant d'état vide : explication + action |
| `FlatList` sans `keyExtractor`, ou avec `index` comme clé | Sauts et pertes d'état visuels au rafraîchissement | PRF | Clé stable issue des données |
| Requête (`useQuery`, `fetch`, `useEffect` + `setState`) sans branche `isError` / `catch` affichée | Échec silencieux ; l'utilisateur attend sans fin | ERR | Afficher l'erreur en langage clair avec « Réessayer » |
| Requête sans branche `isLoading` / `isPending` visible | Écran blanc ou figé pendant le chargement | FBK | Squelette ou indicateur avec texte |
| `allowFontScaling={false}` | Texte non redimensionnable | ACC | Supprimer ; adapter la mise en page aux grandes tailles |
| Couleurs `#RRGGBB` ou `rgba(` dans les composants, hors fichiers de thème | Incohérence, contraste non maîtrisé | COH | Tokens du design system |
| `PanGestureHandler`, `Gesture.Pan`, `Swipeable`, `onSwipe` sans indice visuel ni bouton équivalent | Geste caché, fonction invisible | ACT | Animation d'amorce au premier affichage + boutons équivalents |
| `TextInput` sans `keyboardType`, `autoComplete`, `textContentType`, `returnKeyType` adaptés | Clavier inadapté, saisie plus longue, pas de remplissage automatique | CHG | Attributs adaptés au champ (e-mail, téléphone, code) |
| `TextInput` sans label visible (placeholder seul) | Le placeholder disparaît à la saisie ; on oublie ce qu'on remplit | CTN | Label visible au-dessus du champ |
| Formulaire sans `KeyboardAvoidingView` ni gestion du clavier | Champ masqué par le clavier | ACT | `KeyboardAvoidingView` ou bibliothèque dédiée, défilement vers le champ actif |
| Écran sans gestion des insets (`SafeAreaView`, `useSafeAreaInsets`) | Contenu sous l'encoche ou la barre système | COH | Insets appliqués au conteneur |
| Aucun usage de `NetInfo`, `onlineManager` ou équivalent | Hors ligne non géré | ETA | Bandeau hors ligne, actions mises en file, lecture du cache |
| `setTimeout` pour masquer un message en moins de 4 s | Message illisible | FBK | 4 à 6 s pour une phrase ; permanent si une action est attendue |
| Suppression (`delete`, `remove`) sans confirmation ni Annuler | Perte de données sur un raté | ERR | Annuler pendant quelques secondes, ou confirmation si irréversible |
| `console.log` résiduels, `TODO UX`, `FIXME` dans les écrans | Dette, écrans inachevés | ETA | Nettoyer ; convertir les TODO en tickets |
| Aucun appel analytics (`track`, `logEvent`, `capture`) dans l'écran principal | Impossible de mesurer le time-to-value | VAL | Événement sur l'action principale et sur la réussite |
| `Haptics` absent sur l'action clé, ou présent sur chaque tap | Pas de confirmation sensible, ou bruit haptique | FBK | Haptique légère sur l'action significative uniquement |

### Commandes de recherche (React Native / Expo)

À lancer à la racine du projet ; `-t ts` couvre `.ts` et `.tsx`. Exclure `node_modules` est automatique si le projet a un `.gitignore`. **Toujours donner un chemin** (`.`, `src`, `app`) : sans chemin, `rg` lit l'entrée standard quand il tourne hors d'un terminal, ce qui est le cas quand Claude Code l'exécute, et la commande semble se figer.

```bash
# Boutons pressables : comparer le nombre de pressables et le nombre de libellés accessibles
rg -t ts -c "<(Pressable|TouchableOpacity|TouchableHighlight|TouchableWithoutFeedback)" .
rg -t ts -c "accessibilityLabel" .

# onPress posé sur Text ou View (cible sans rôle)
rg -t ts -n "<(Text|View)[^>]*onPress" .

# Alert.alert utilisé comme confirmation ou succès
rg -t ts -n "Alert\.alert\(" .

# Listes sans état vide : lister les FlatList, puis vérifier ListEmptyComponent
rg -t ts -n "<(FlatList|FlashList|SectionList)" .
rg -t ts -c "ListEmptyComponent" .

# Clés instables
rg -t ts -n "keyExtractor=\{\(.*index" .
rg -t ts -n "key=\{index\}" .

# Requêtes sans erreur ni chargement affichés (comparer les compteurs)
rg -t ts -c "isLoading|isPending|isFetching" .
rg -t ts -c "isError|error\b" .

# Texte non redimensionnable
rg -t ts -n "allowFontScaling=\{false\}" .

# Couleurs en dur hors du thème
rg -t ts -n "#[0-9a-fA-F]{3,8}\b|rgba?\(" . -g '!**/theme/**' -g '!**/tokens/**' -g '!**/*.config.*'

# Gestes : vérifier ensuite la présence d'un indice visuel et d'un bouton équivalent
rg -t ts -n "PanGestureHandler|Gesture\.Pan|Swipeable|onSwipe|useAnimatedGestureHandler" .

# Champs de saisie : afficher le bloc pour vérifier keyboardType, autoComplete, label
rg -t ts -n -A8 "<TextInput" .

# Clavier et zones sûres
rg -t ts -c "KeyboardAvoidingView|KeyboardAwareScrollView|useSafeAreaInsets|SafeAreaView" .

# Hors ligne
rg -t ts -n "NetInfo|onlineManager|useNetworkState" .

# Suppressions : vérifier Annuler ou confirmation à proximité
rg -t ts -n -i -B2 -A6 "(delete|remove|supprimer)\w*\(" .

# Dette et traces
rg -t ts -n "console\.(log|warn)|TODO|FIXME" .

# Mesure
rg -t ts -n "track\(|logEvent\(|capture\(|analytics\." .
```

---

## 3. Next.js / web : motifs à rechercher

| Motif dans le code | Problème UX probable | Cat. | Correction type |
|---|---|---|---|
| `<div>`, `<span>`, `<li>`, `<p>` avec `onClick` | Inaccessible au clavier et au lecteur d'écran ; pas d'état focus | ACC | `<button type="button">` ou `<a href>` |
| `<a>` sans `href` | Lien non focalisable, non navigable | ACC | `href` réel, ou `<button>` si c'est une action |
| `<button>` sans `type` dans un formulaire | Soumission involontaire | ERR | `type="button"` pour les actions, `type="submit"` pour l'envoi unique |
| `<input>` sans `<label htmlFor>` ni `aria-label` | Champ anonyme ; placeholder qui disparaît | CTN | Label visible lié par `htmlFor` / `id` |
| Message d'erreur non relié au champ (`aria-describedby` absent) | Lecteur d'écran n'annonce pas l'erreur | ACC | `aria-describedby` vers le message, `aria-invalid` |
| `outline: none` / `outline-none` sans `:focus-visible` de remplacement | Focus invisible au clavier | ACC | Style `:focus-visible` explicite avec contraste ≥ 3:1 |
| `<img>` sans `alt`, ou sans `next/image` | Image muette ; décalage de mise en page (CLS) | ACC, PRF | `alt` descriptif (ou `alt=""` si décorative) ; `next/image` avec dimensions |
| Dossier `app/` sans `loading.tsx`, `error.tsx`, `not-found.tsx` | Écran blanc pendant le chargement ; erreur et 404 par défaut du framework | ETA | Créer les trois avec le design system et une action de sortie |
| Modale sans `role="dialog"`, `aria-modal`, gestion de Échap et du focus | Piège au clavier, contexte perdu | ACC | Composant de dialogue accessible (focus trap, Échap, retour du focus) |
| Action révélée uniquement au survol (`opacity-0 group-hover:opacity-100`) | Invisible au clavier et au tactile | ACT | Visible par défaut, ou révélée aussi au focus |
| `window.alert`, `window.confirm`, `window.prompt` | Dialogues natifs bloquants, non stylés, non accessibles | ERR | Composant de dialogue ou Annuler en place |
| `<html>` sans `lang` | Synthèse vocale dans la mauvaise langue | ACC | `lang="fr"` dans le layout racine |
| Animations sans `prefers-reduced-motion` | Gêne, nausée pour certains utilisateurs | ACC | `motion-reduce:` (Tailwind) ou media query |
| Couleurs `#RRGGBB` hors `tailwind.config` et fichiers de thème | Incohérence, contraste non maîtrisé | COH | Tokens / classes du thème |
| Aucun événement analytics sur l'action principale | Time-to-value non mesurable | VAL | Événement sur l'action et sur la réussite |
| Tableau large sans conteneur `overflow-x-auto` | Défilement horizontal de toute la page sur mobile | COH | Conteneur défilant, colonnes prioritaires |
| Pas de `metadata` / `title` par page | Onglets illisibles, historique inutilisable (test du coffre) | NAV | `title` explicite par route |

### Commandes de recherche (Next.js)

Même règle : toujours donner un chemin.

```bash
# Éléments non sémantiques cliquables
rg -t ts -n "<(div|span|li|p|section|article)[^>]*onClick" .

# Liens sans href et boutons sans type (PCRE2 pour les lookaheads)
rg -t ts -nP "<a(?![^>]*\bhref=)[^>]*>" .
rg -t ts -nP "<button(?![^>]*\btype=)[^>]*>" .

# Champs sans label : lister les inputs, puis compter les htmlFor
rg -t ts -n "<(input|select|textarea)" . -g '!**/ui/**'
rg -t ts -c "htmlFor=" .

# Erreurs non reliées
rg -t ts -c "aria-describedby|aria-invalid" .

# Focus supprimé
rg -n "outline:\s*none|outline-none" . --glob '*.{tsx,css,scss}'
rg -c "focus-visible" . --glob '*.{tsx,css,scss}'

# Images
rg -t ts -nP "<img(?![^>]*\balt=)" .
rg -t ts -c "<img" .

# États de route (lister ce qui existe)
rg --files app | rg "loading\.tsx|error\.tsx|not-found\.tsx|global-error\.tsx"

# Modales
rg -t ts -n "role=\"dialog\"|aria-modal" .

# Révélation au survol uniquement
rg -t ts -n "opacity-0[^\"]*group-hover:opacity-100|hidden[^\"]*group-hover:block" .

# Dialogues natifs
rg -t ts -n "window\.(alert|confirm|prompt)\(|[^.]\balert\(" .

# Langue du document
rg -t ts -n -A1 "<html" .

# Animations et réduction de mouvement (comparer)
rg -c "animate-|transition|@keyframes" . --glob '*.{tsx,css}'
rg -c "prefers-reduced-motion|motion-reduce" . --glob '*.{tsx,css}'

# Couleurs en dur hors configuration
rg -t ts -n "#[0-9a-fA-F]{3,8}\b" . -g '!tailwind.config.*' -g '!**/theme/**' -g '!**/tokens/**'

# Tableaux : lister, puis vérifier le conteneur défilant autour de chacun
rg -t ts -n -B3 "<table" .
rg -t ts -c "overflow-x-auto" .

# Titres de page
rg -t ts -c "export const metadata|generateMetadata" .
```

---

## 4. Lire les résultats : du motif au constat

1. **Confirmer** : ouvrir le fichier, vérifier que le motif correspond bien à un problème (un `div onClick` dans un composant de bibliothèque déjà accessible n'en est pas un).
2. **Reformuler du point de vue de l'utilisateur** : « l'icône d'épingle n'a pas de libellé » devient « un utilisateur de VoiceOver entend "bouton" sans savoir ce qu'il fait ».
3. **Classer** : une catégorie, une lentille principale.
4. **Évaluer la sévérité** avec `scoring.md`. Repère : accessibilité manquante sur l'action principale = 4 ; sur une action secondaire = 3 ; état vide non conçu sur l'écran d'accueil = 3 ; couleur en dur = 1 ou 2 selon le contraste réel.
5. **Rédiger le ticket** avec le chemin exact, la ligne, le changement attendu et le test sur appareil.

---

## 5. Ce que le code ne dit pas : à vérifier sur appareil

| À vérifier | Comment |
|---|---|
| Contraste réel | Calculer avec les valeurs effectives des tokens, sur le fond réel (y compris sur image) |
| Taille réelle des cibles | Mesurer à l'écran ; un `padding` peut être écrasé par un parent |
| Fluidité | Défilement d'une liste de 100 éléments, transitions, clavier ; sur un appareil milieu de gamme, pas seulement sur le simulateur |
| Lecteur d'écran | Parcourir la tâche principale avec VoiceOver / TalkBack ; chaque élément est annoncé avec un nom et un rôle |
| Grande taille de texte | Activer la taille maximale système ; rien ne se coupe |
| Hors ligne | Mode avion au milieu d'une action |
| Première utilisation | Compte neuf, données vides, permissions non accordées |
| Retour système (Android) | Depuis chaque écran et chaque modale |
| Clavier (web) | Tâche principale entière sans souris ; focus toujours visible |
| Latence réelle | Réseau bridé (3G) ; l'écran reste informatif |

Un constat issu de ces vérifications se consigne comme les autres, avec la mention « observé sur appareil » dans la colonne Élément.
