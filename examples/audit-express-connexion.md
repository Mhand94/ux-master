# Exemple : audit Express d'un écran de connexion mobile

Cet exemple montre un audit **Express** complet tel que le skill doit le produire : fiche de cadrage, parcours cognitif, constats dédoublonnés et classés, trois correctifs sous forme de tickets Claude Code, hypothèses. En Express, il n'y a pas de score ; le même écran passé en Standard donne le calcul présenté dans `references/scoring.md` (64/100, non lançable).

---

## Écran audité

Application mobile (iOS et Android), écran de connexion : champ e-mail, champ mot de passe avec icône « œil » pour afficher le mot de passe, bouton « Continuer », lien « Mot de passe oublié ? », deux boutons « Continuer avec Google » et « Continuer avec Apple », logo en haut.

Niveau retenu : **Express** (un écran, demande « ton avis sur l'écran de connexion »).

## Fiche de cadrage

| Champ | Contenu |
|---|---|
| Persona primaire | [Hypothèse] Commerçant indépendant, 35 à 60 ans, utilise WhatsApp et sa banque sur mobile, rien de plus technique |
| Contexte d'usage | [Hypothèse] Debout, dans sa boutique, entre deux clients ; une main ; interruptions fréquentes |
| Job à accomplir | Quand j'ouvre l'app pour voir si quelqu'un m'a répondu, je veux entrer en quelques secondes, pour ne pas perdre le fil de ma journée |
| Plateforme et posture | iOS et Android ; produit transitoire |
| Contraintes | Design system interne (tokens `colors.ts`) ; React Native / Expo ; connexion par e-mail ou fournisseur tiers |
| Prouvé / supposé | Aucun entretien ni test réalisé : tout le cadrage est [Hypothèse] |

## Parcours cognitif (tâche : se connecter avec son e-mail)

1. **Saisir l'e-mail** : le clavier propose les majuscules en début de champ (autocapitalisation par défaut) ; l'utilisateur tape « Nadia@… ». Pas de problème visible à ce stade.
2. **Saisir le mot de passe** : le placeholder « Mot de passe » disparaît dès la première lettre ; il ne reste aucun label. L'icône « œil » n'a pas de nom pour un lecteur d'écran.
3. **Valider** : le bouton « Continuer » reste gris. Rien n'explique pourquoi. L'utilisateur relit, retape, hésite. *(Cause réelle, vue dans le code : la validation rejette toute majuscule dans l'e-mail.)* Fossé d'exécution majeur : il ne sait pas comment avancer.
4. **Si la validation passe mais que le serveur échoue** : « Une erreur est survenue. » Ni cause, ni action. Fossé d'évaluation : il ne sait pas si c'est lui, le réseau ou le service.
5. **Chercher une sortie** : le lien « Mot de passe oublié ? » est en gris clair, peu visible ; l'utilisateur pressé ne le voit pas.

## Constats

| # | Sév. | Cat. | Lentille | Élément | Problème (vu par l'utilisateur) | Correction | Fréq. | Effort | Priorité |
|---|---|---|---|---|---|---|---|---|---|
| 1 | 4 | ERR | L1 contraintes, fossé d'exécution (L2 n°5, n°9) | Bouton « Continuer » | Le bouton reste gris sans raison quand l'e-mail contient une majuscule ; impossible d'avancer, aucune piste | Accepter les majuscules (normaliser en minuscules côté système, loi de Postel) ; si un champ est invalide, le dire sous le champ et laisser le bouton actif | 3 | 1 | 12 |
| 2 | 3 | ERR | L2 n°9 (L4 ne blâme jamais) | Message « Une erreur est survenue » | L'utilisateur ne sait pas si c'est lui, le réseau ou le service, ni quoi faire | Distinguer les cas : identifiants incorrects (près du champ), pas de réseau (bandeau + « Réessayer »), service indisponible (message + délai) | 2 | 2 | 3 |
| 3 | 3 | ACC | Socle accessibilité (L1 signifiant) | Icône « œil » | Un utilisateur de lecteur d'écran entend « bouton » sans savoir ce qu'il fait | `accessibilityLabel` « Afficher le mot de passe » / « Masquer le mot de passe », `accessibilityRole="button"`, cible 44 × 44 | 3 | 1 | 9 |
| 4 | 2 | CTN | L2 n°6 (L3 mots) | Champs e-mail et mot de passe | Le placeholder disparaît à la saisie ; après une interruption, on ne sait plus quel champ est lequel | Label visible au-dessus de chaque champ ; placeholder réservé à un exemple (« nadia@exemple.fr ») | 3 | 1 | 6 |
| 5 | 2 | ACC | Socle accessibilité (L3 hiérarchie) | Lien « Mot de passe oublié ? » | Gris `#8A8A8A` sur blanc : 3,2:1, sous le seuil ; le lien de secours est le moins visible de l'écran | Couleur de texte secondaire du design system à ≥ 4,5:1 ; placer le lien juste sous le champ mot de passe | 3 | 1 | 6 |
| 6 | 1 | COH | L5 esthétique | Logo | Désaligné de 6 px par rapport à la grille des champs | Aligner sur la grille de 4 px | 3 | 1 | 3 |

Dédoublonnage appliqué : le constat 1 avait été relevé trois fois (Norman « contraintes », Nielsen n°5 « prévention », Nielsen n°9 « diagnostiquer ») ; il est consigné une fois, en ERR, avec la lentille principale et les secondaires entre parenthèses.

## Ce qui fonctionne (à conserver)

- Un seul bouton principal, plein, en bas du formulaire : hiérarchie claire (L3), sous le pouce (Fitts).
- Les fournisseurs tiers sont présents et distincts du formulaire : chemin rapide pour l'intermédiaire permanent (L4).
- Aucune demande d'information avant la connexion : la valeur n'est pas conditionnée à un formulaire long (L6).

## Correctifs (Express : trois au plus, par priorité)

### UX-1 : Accepter les majuscules dans l'e-mail

```
Fichier(s) : apps/mobile/src/screens/auth/LoginScreen.tsx ; packages/shared/src/validation/email.ts

Problème (sév. 4, ERR) : quand l'utilisateur tape une majuscule dans son e-mail, le bouton « Continuer » reste gris sans aucune explication ; il ne peut pas se connecter et ne sait pas pourquoi.

Comportement attendu : un e-mail avec majuscules est accepté et normalisé en minuscules ; si l'e-mail est réellement invalide, un message s'affiche sous le champ et le bouton reste actif pour permettre la correction.

À faire :
1. Dans email.ts, normaliser la valeur (trim + toLowerCase) avant validation.
2. Dans LoginScreen.tsx, retirer la désactivation du bouton liée à la validité ; à l'appui, valider et afficher l'erreur sous le champ concerné.
3. Sur le TextInput e-mail : autoCapitalize="none", keyboardType="email-address", autoComplete="email", textContentType="emailAddress".

Contraintes : tokens du design system uniquement ; ne pas modifier le flux OAuth ; aucune dépendance nouvelle.

Critères d'acceptation :
- [ ] « Nadia@Exemple.fr » permet de se connecter
- [ ] « nadia@exemple » affiche « Vérifiez l'adresse e-mail » sous le champ, le bouton reste actif
- [ ] Le clavier e-mail s'ouvre sans majuscule automatique
- [ ] Accessibilité : le message d'erreur est lu par le lecteur d'écran (accessibilityLiveRegion="polite" sur Android, annonce sur iOS)

Test sur appareil : iPhone et Android → taper « Nadia@Exemple.fr » + mot de passe valide → appuyer sur Continuer → arriver sur l'écran d'accueil.
```

### UX-2 : Libellé accessible sur l'icône « œil »

```
Fichier(s) : apps/mobile/src/components/PasswordInput.tsx

Problème (sév. 3, ACC) : un utilisateur de VoiceOver ou TalkBack entend « bouton » sur l'icône « œil » sans savoir qu'elle affiche le mot de passe.

Comportement attendu : le lecteur d'écran annonce « Afficher le mot de passe, bouton », puis « Masquer le mot de passe, bouton » une fois activé ; la zone de toucher mesure au moins 44 × 44.

À faire :
1. Sur le Pressable de l'icône : accessibilityRole="button", accessibilityLabel dynamique selon l'état.
2. Porter la zone de toucher à 44 × 44 (minWidth/minHeight ou hitSlop).

Contraintes : tokens du design system uniquement ; ne pas changer l'icône.

Critères d'acceptation :
- [ ] VoiceOver et TalkBack annoncent le libellé et son changement
- [ ] Zone de toucher ≥ 44 × 44 vérifiée à l'inspecteur

Test sur appareil : Android, TalkBack → balayer jusqu'à l'icône → entendre « Afficher le mot de passe, bouton » → double-tap → le mot de passe apparaît, l'annonce devient « Masquer le mot de passe, bouton ».
```

### UX-3 : Labels visibles sur les champs

```
Fichier(s) : apps/mobile/src/screens/auth/LoginScreen.tsx ; apps/mobile/src/components/TextField.tsx

Problème (sév. 2, CTN) : le placeholder disparaît dès la saisie ; après une interruption, l'utilisateur ne sait plus quel champ contient quoi.

Comportement attendu : chaque champ a un label visible au-dessus (« E-mail », « Mot de passe ») qui reste affiché pendant la saisie ; le placeholder ne sert qu'à montrer un exemple.

À faire :
1. Ajouter une prop label au composant TextField, rendue au-dessus du champ avec le style de label du design system.
2. Dans LoginScreen, passer label="E-mail" (placeholder « nadia@exemple.fr ») et label="Mot de passe" (sans placeholder).
3. Lier le label au champ pour le lecteur d'écran (accessibilityLabel sur le TextInput reprenant le label).

Contraintes : tokens du design system uniquement ; conserver la hauteur totale du formulaire visible sans défilement sur un écran de 667 pt.

Critères d'acceptation :
- [ ] Les deux labels restent visibles pendant et après la saisie
- [ ] Le formulaire tient sans défilement sur iPhone SE
- [ ] Accessibilité : chaque champ est annoncé avec son label

Test sur appareil : iPhone SE → saisir un e-mail, quitter l'app, revenir → les labels sont lisibles au-dessus des valeurs saisies.
```

Le constat 5 (contraste du lien) est un quick win du même type que UX-3 ; en Standard, il aurait son ticket, ainsi que le constat 2.

## Hypothèses à tester avec de vrais utilisateurs

| Hypothèse | Risque si fausse | Méthode |
|---|---|---|
| [Hypothèse] La connexion par e-mail est le chemin principal ; Google et Apple sont secondaires | L'ordre des éléments est inversé | Analytics : part de chaque méthode après lancement |
| [Hypothèse] L'utilisateur se connecte souvent debout, d'une main | La taille des cibles et la position du bouton sont à revoir | Observation terrain, entretiens |
| [Hypothèse] Le persona ne connaît pas la connexion biométrique | Occasion manquée de supprimer l'écran pour les habitués | Test d'utilisabilité, question post-tâche |

## Suggestion au-delà de l'audit

Proposer la **connexion biométrique** (Face ID, empreinte) dès la deuxième ouverture : pour un produit transitoire utilisé plusieurs fois par jour, c'est l'écran lui-même qui disparaît pour l'habitué (L4 intermédiaire permanent, L6 dire non). Effort 2, bénéfice attendu : time-to-value réduit de la durée de la saisie à chaque ouverture.

## Prochaine étape

Traiter UX-1 en une session Claude Code, tester sur appareil, puis enchaîner UX-2 et UX-3 ; relancer un audit Standard sur le parcours complet « connexion → accueil » une fois les trois tickets clos.
