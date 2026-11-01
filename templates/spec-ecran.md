# Spécification d'écran — <nom de l'écran>

Produit : <…> · Parcours : <…> · Plateforme : <iOS / Android / web / PC> · Version : <…>

## 1. Rôle

- **Rôle unique de l'écran** (une phrase) : <…>
- **Persona primaire et posture** : <prénom, situation ; transitoire ou souverain>
- **Job servi** : Quand <situation>, je veux <motivation>, pour <résultat>.
- **Place dans le parcours** : vient de <écran précédent>, mène à <écran suivant>.
- **Moment magique visé** (si cet écran y participe) : <…> · Time-to-value cible : <…>

## 2. Actions

| Type | Libellé exact | Effet | Feedback immédiat | Réversible ? Comment ? |
|---|---|---|---|---|
| **Principale (une seule)** | | | | |
| Secondaire 1 | | | | |
| Secondaire 2 | | | | |
| Secondaire 3 (au plus) | | | | |

Gestes cachés (swipe, appui long, glisser) : <aucun> ou <geste → indice visible + bouton équivalent>.

## 3. Contenu, par ordre d'importance

1. <élément dominant>
2. <…>
3. <…>

Ce qui a été **retiré** et pourquoi (dire non) : <…>

## 4. Les sept états

| État | Ce que l'utilisateur voit | Texte exact | Action proposée |
|---|---|---|---|
| Vide (aucune donnée) | | | |
| Chargement | squelette / indicateur + texte | | |
| Erreur (réseau, serveur, validation) | | | « Réessayer » / correction |
| Succès | | | suite du parcours |
| Première utilisation | | | |
| Hors ligne | | | |
| Permission refusée (le cas échéant) | | | vers les réglages |

## 5. Micro-textes

| Emplacement | Texte exact |
|---|---|
| Titre | |
| Sous-titre ou aide | |
| CTA principal | |
| CTA secondaires | |
| Message d'erreur type | |
| État vide | |
| Confirmation (si irréversible) | |

Vocabulaire de l'utilisateur, verbes d'action, aucun jargon.

## 6. Navigation et sorties

- Retour : <bouton + geste / Retour système>
- Sorties : <fermer, annuler, aller à…>
- Test du coffre : titre visible <oui/non>, section active <oui/non>, chemin de retour <oui/non>

## 7. Accessibilité

- Cibles ≥ 44 pt / 48 dp : <oui>
- Contraste ≥ 4,5:1 sur tous les textes (tokens utilisés : <…>) : <oui>
- Libellés accessibles des icônes seules : <liste>
- Ordre de lecture et de focus : <…>
- Grande taille de texte : <comportement prévu>

## 8. Design system

Tokens utilisés : couleurs <…>, typographie <…>, espacements <…>, rayons <…>. Aucune valeur en dur.

## 9. Mesure

- Événement analytics sur l'action principale : `<nom_evenement>` avec <propriétés>
- Événement de réussite : `<…>`
- Indicateur suivi : <taux de complétion, time-to-value, …>

## 10. Hypothèses à valider

- [Hypothèse] <…> → vérifiée par <entretien / test / analytics>

## 11. Checklist pré-vol

Reporter ici le résultat des 15 points de SKILL.md : <n>/15. Points manquants : <…>. L'écran part en développement à 15/15.
