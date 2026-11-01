# Ticket Claude Code — gabarit

Un ticket = un constat = une session Claude Code. Copier le bloc ci-dessous tel quel dans le prompt, après le contexte habituel du projet (design system, stack, conventions).

```
## UX-<n> : <titre en cinq mots>

Fichier(s) : <chemin/vers/Composant.tsx> (lignes <…> si connues)

Problème (sév. <0-4>, <CAT>) : <une phrase, du point de vue de l'utilisateur ; ce qu'il vit, pas ce que le code fait>

Comportement attendu : <une phrase observable à l'écran>

À faire :
1. <changement précis, verbe d'action, élément nommé>
2. <…>
3. <…>

Contraintes :
- Utiliser uniquement les tokens du design system (<nom du fichier de tokens>) ; aucune couleur, taille ou espacement en dur
- Ne pas modifier <composants, fichiers ou comportements à préserver>
- Aucune dépendance nouvelle sans accord
- Conserver les sept états existants (vide, chargement, erreur, succès, première fois, hors ligne, permission)

Critères d'acceptation :
- [ ] <observable 1 : ce que l'on voit ou fait, pas ce que le code contient>
- [ ] <observable 2>
- [ ] Accessibilité : <libellé accessible présent / cible ≥ 44 pt ou 48 dp / contraste ≥ 4,5:1 / focus visible / ordre de tabulation>
- [ ] Aucune régression sur <écran ou parcours lié>

Test sur appareil (avant de clore) :
<appareil ou navigateur> → <geste exact à faire> → <résultat visible attendu>
```

## Exemple rempli

```
## UX-3 : Libellé accessible sur l'épingle

Fichier(s) : apps/mobile/src/components/CandidateCard.tsx (bouton Pressable de l'icône épingle)

Problème (sév. 3, ACC) : un utilisateur de VoiceOver ou TalkBack entend « bouton » sans savoir que ce bouton garde le candidat de côté ; il ne peut ni l'utiliser ni comprendre l'état (épinglé ou non).

Comportement attendu : le lecteur d'écran annonce « Garder Sarah de côté, bouton » puis, une fois épinglé, « Retirer Sarah des favoris, bouton, sélectionné ».

À faire :
1. Ajouter accessibilityRole="button" sur le Pressable de l'épingle.
2. Ajouter accessibilityLabel dynamique : `Garder ${prenom} de côté` / `Retirer ${prenom} des favoris`.
3. Ajouter accessibilityState={{ selected: isPinned }}.
4. Porter la zone de toucher à 44 × 44 avec hitSlop si la taille visuelle reste à 32.

Contraintes :
- Tokens du design system uniquement (packages/ui/tokens.ts)
- Ne pas modifier l'animation d'épinglage existante
- Aucune dépendance nouvelle

Critères d'acceptation :
- [ ] VoiceOver et TalkBack annoncent le libellé et l'état sur chaque carte
- [ ] La zone de toucher mesure au moins 44 × 44 pt (vérifié avec l'inspecteur)
- [ ] L'animation et le compteur Favoris fonctionnent comme avant

Test sur appareil (avant de clore) :
iPhone, VoiceOver activé → balayer jusqu'à l'épingle d'une carte → entendre « Garder Sarah de côté, bouton » → double-tap → entendre « Retirer Sarah des favoris, bouton, sélectionné » et voir le compteur Favoris passer à +1.
```

## Règles d'écriture

- **Du point de vue de l'utilisateur** dans « Problème » : ce qu'il vit. Le code vient dans « À faire ».
- **Observable** dans les critères : « le toast reste affiché 5 secondes », pas « la constante TOAST_DURATION vaut 5000 ».
- **Un seul changement par ticket.** Deux constats proches sur le même composant restent deux tickets ; ils peuvent être enchaînés dans la même session, l'un après l'autre.
- **Le test sur appareil est obligatoire** : un ticket sans test n'est pas clos.
