# Sévérité, score et priorisation

Ce fichier calibre les trois outils de mesure de SKILL.md : la **sévérité** d'un constat, le **score** d'un écran et la **priorité** d'une correction. Il donne des exemples étalonnés pour que deux audits du même écran produisent les mêmes chiffres.

---

## 1. Sévérité (0 à 4)

La sévérité combine trois facteurs, dans l'esprit de l'échelle de Nielsen :

- **Fréquence** : combien d'utilisateurs rencontrent le problème, et à quelle fréquence.
- **Impact** : à quel point il est difficile de s'en sortir une fois rencontré.
- **Persistance** : le problème gêne-t-il une fois (on apprend), ou à chaque usage.

| Sév. | Nom | Définition | Exemples étalonnés |
|---|---|---|---|
| **4** | Bloquant | Empêche d'accomplir la tâche principale ; ou perd des données ; ou piège l'utilisateur (dark pattern) ; ou exclut un groupe entier (accessibilité) | Le bouton de validation reste inactif sans explication alors que tout est rempli · La saisie d'un formulaire de dix champs se perd quand le clavier se ferme · Aucune cible de l'écran n'a de libellé pour lecteur d'écran · Le prix n'apparaît qu'après la saisie de la carte bancaire · Le Retour système quitte l'app depuis un écran profond |
| **3** | Majeur | La tâche aboutit, mais au prix d'un effort, d'erreurs ou d'abandons fréquents | Le geste principal (swipe) n'a aucun indice ni bouton équivalent · Message d'erreur « Une erreur est survenue » sans cause ni action · Liste principale sans état vide au premier usage · Cible de 28 px pour l'action secondaire la plus utilisée · Paywall affiché avant toute démonstration de valeur |
| **2** | Mineur | Gêne, ralentit ou agace ; l'utilisateur s'en sort seul | Trois libellés différents pour la même action selon l'écran · Confirmation demandée pour une action réversible · Toast de deux secondes pour une phrase de douze mots · Filtres actifs non rappelés sur la liste · Placeholder utilisé comme seul label |
| **1** | Cosmétique | Incohérence sans effet mesurable sur la tâche | Alignement à 2 px près · Deux gris proches pour le même rôle · Majuscule manquante · Icône légèrement différente du reste du set |
| **0** | Non-problème | Préférence personnelle, goût, choix défendable | « J'aurais mis le bouton en bleu » |

### Questions de calibrage

1. **Test des cinq** : « Si cinq utilisateurs représentatifs faisaient la tâche, combien échoueraient ? » Plus de deux → 4. Un ou deux peinent fortement → 3. Ils tiquent ou ralentissent → 2. Ils ne remarquent rien → 1.
2. **Test de l'apprentissage** : « Le problème disparaît-il après la première fois ? » Si oui, baisser d'un niveau (sauf si la première fois est décisive, comme l'onboarding).
3. **Test du groupe exclu** : « Un groupe entier d'utilisateurs est-il empêché ? » (lecteur d'écran, grande taille de texte, clavier seul, connexion lente). Si oui → 4, quelle que soit la proportion.
4. **Test de la confiance** : « L'utilisateur se sent-il trompé ? » Si oui → 4 (ETH).

### Règles d'arbitrage

- Un constat sur **l'action principale** vaut un niveau de plus que le même constat sur une action secondaire.
- Un constat sur **l'écran d'entrée** (premier écran vu, onboarding) vaut un niveau de plus.
- En cas d'hésitation entre deux niveaux, retenir le plus élevé et le signaler « (3, possiblement 2) » ; le test utilisateur tranchera.
- La sévérité ne tient **pas** compte de l'effort de correction : un bouton de 28 px est un 3 même s'il se corrige en une minute. L'effort intervient dans la priorité.

---

## 2. Score UX d'un écran (sur 100)

```
Score = 100 − (15 × n₄ + 7 × n₃ + 3 × n₂ + 1 × n₁)
```

- `n₄`, `n₃`, `n₂`, `n₁` : nombre de constats de chaque sévérité **sur cet écran**.
- Plancher à 0.
- Score global d'un parcours ou d'une app = **moyenne** des scores des écrans audités (pas la somme des constats, qui pénaliserait les grands périmètres).
- **Lançable : non** dès qu'un constat de sévérité 4 subsiste, quel que soit le score.

| Score | Lecture | Décision |
|---|---|---|
| 90 à 100 | Excellent | Mettre en ligne ; tester avec de vrais utilisateurs pour trouver ce que l'heuristique ne voit pas |
| 75 à 89 | Bon | Corriger les quick wins, puis mettre en ligne |
| 60 à 74 | Fragile | Corriger les sévérités 3 avant lancement |
| Moins de 60 | À refondre | Reprendre la conception (mode A) plutôt que corriger constat par constat |

### Exemple calibré

Écran de connexion mobile. Constats : un 4 (le bouton « Continuer » reste gris sans explication quand l'e-mail contient une majuscule), deux 3 (message d'erreur générique ; aucun libellé sur l'icône « afficher le mot de passe »), deux 2 (placeholder seul comme label ; lien « mot de passe oublié » en gris 3,2:1), un 1 (icône de marque désalignée).

```
Score = 100 − (15 × 1 + 7 × 2 + 3 × 2 + 1 × 1) = 100 − 36 = 64 → Fragile
Lançable : non (une sévérité 4)
```

Après correction du 4 et des deux 3, l'écran passe à `100 − (3 × 2 + 1) = 93` : le score sert exactement à mesurer ce progrès.

### Limites du score

- Il **compare deux versions du même écran** ; il ne compare pas deux produits.
- Il mesure ce qu'un audit heuristique voit ; un test utilisateur peut révéler un problème grave invisible au score.
- Il ne remplace ni le SUS (mesure déclarative après test), ni les métriques d'usage (entonnoir, rétention). Voir `recherche-et-tests.md`.

---

## 3. Priorisation des corrections

```
Priorité = Sévérité × Fréquence ÷ Effort
```

| Facteur | 1 | 2 | 3 |
|---|---|---|---|
| **Fréquence** | Rare : quelques utilisateurs, cas limite | Souvent : une part notable des utilisateurs, ou à chaque session pour certains | À chaque usage, pour tous (action principale, écran d'entrée) |
| **Effort** | Moins d'une heure : texte, taille, couleur, attribut d'accessibilité | Une demi-journée à une journée : nouveau composant, nouvel état, logique locale | Plusieurs jours : flux, navigation, architecture, backend |

Priorité maximale : 4 × 3 ÷ 1 = 12. Priorité minimale : 1 × 1 ÷ 3 ≈ 0,3.

### Ordre de traitement

1. **Bloquants** (sévérité 4) : tous, quel que soit l'effort.
2. **Quick wins** : sévérité ≥ 2 et effort 1, par priorité décroissante. Souvent un tiers des constats ; en une demi-journée, le score bondit.
3. **Le reste** par priorité décroissante.
4. Les sévérités 1 vont au backlog et se traitent par lot, quand on touche déjà le composant.

### Exemple calibré

| # | Constat | Sév. | Fréq. | Effort | Priorité | Rang |
|---|---|---|---|---|---|---|
| 1 | Bouton inactif sans explication | 4 | 3 | 1 | 12 | 1 |
| 2 | Icône sans libellé accessible | 3 | 3 | 1 | 9 | 2 |
| 3 | Message d'erreur générique | 3 | 2 | 2 | 3 | 4 |
| 4 | Placeholder comme seul label | 2 | 3 | 1 | 6 | 3 |
| 5 | Lien gris sous contraste | 2 | 3 | 1 | 6 | 3 |
| 6 | Icône désalignée | 1 | 3 | 1 | 3 | 5 |

Les constats 1, 2, 4 et 5 sont des quick wins : une heure de travail fait passer l'écran de 64 à 86.

---

## 4. Pièges de mesure

- **Double comptage** : le même élément relevé par deux lentilles compte une fois. Vérifier la colonne Élément avant de scorer.
- **Inflation de périmètre** : auditer dix écrans en Express produit un score trompeur ; en Express, pas de score.
- **Sévérité par l'effort** : « c'est facile à corriger donc ce n'est pas grave » est faux ; l'effort n'entre que dans la priorité.
- **Sévérité par l'esthétique** : un écran beau avec un bouton muet est un écran avec une sévérité 3.
- **Score comme objectif** : atteindre 95 en supprimant des fonctionnalités utiles n'est pas un progrès ; le score mesure la qualité d'exécution, pas la valeur. La valeur se mesure par le time-to-value et la rétention.
- **Oubli des hypothèses** : un score élevé sur un écran dont le besoin n'a jamais été vérifié chez de vrais utilisateurs reste un score **[Hypothèse]**.
