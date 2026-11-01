# Protocole de test d'utilisabilité — <produit> — <version ou maquette>

Date : <…> · Participants : 5 (<persona primaire>) · Durée par session : 45 minutes · Modérateur : <…> · Observateur : <…> · Support : <maquette interactive / build / appareil réel>

## Objectifs du test

1. Vérifier que <tâche principale> aboutit sans aide.
2. Éprouver l'hypothèse <H…> : <…>.
3. Mesurer le ressenti (SUS) et le comparer à <version précédente / 68>.

## Tâches (de la plus simple à la plus complexe)

| # | Situation lue au participant (jamais le nom des éléments de l'interface) | Chemin attendu | Critère de réussite |
|---|---|---|---|
| T1 | « Vous … Faites ce qu'il faut. » | | |
| T2 | | | |
| T3 | | | |
| T4 (optionnelle) | | | |

## Script du modérateur

### Accueil (5 minutes)

« Merci d'être là. Nous testons <le produit>, pas vous : si quelque chose n'est pas clair, c'est le produit qui doit changer. Je vais vous donner des petites situations ; faites comme si vous étiez seul, et pensez à voix haute : dites ce que vous regardez, ce que vous attendez, ce qui vous surprend. Je ne pourrai pas vous aider pendant les tâches. Vous pouvez arrêter quand vous voulez. Puis-je enregistrer l'écran et la voix ? »

### Questions de contexte (3 minutes)

- <Deux ou trois questions pour situer le participant par rapport au persona>

### Tâches (30 minutes)

Pour chaque tâche : lire la situation, la laisser affichée, lancer le chronomètre, se taire.

Relances autorisées : « Qu'est-ce que vous regardez ? » · « À quoi vous vous attendiez ? » · « Que feriez-vous si j'étais absent ? » · « Continuez à penser à voix haute. »

Interdit : expliquer, montrer, défendre, réagir aux erreurs, dire si c'est juste.

Après chaque tâche : « Pensez-vous avoir réussi ? » · « Sur une échelle de 1 à 5, c'était facile ? » · « Qu'est-ce qui vous a gêné ? »

### Questions post-test (3 minutes)

- Qu'est-ce que vous retenez de ce produit, en une phrase ?
- Qu'est-ce qui vous a le plus plu ? Le plus gêné ?
- L'utiliseriez-vous dans votre situation de <…> ? Pourquoi ? *(à prendre avec prudence : intention, pas comportement)*

### SUS (2 minutes)

Remettre le questionnaire des dix affirmations (voir `references/recherche-et-tests.md`), notées de 1 à 5.

### Clôture (2 minutes)

Remercier, dédommager, demander l'accord pour un prochain cycle.

## Feuille d'observation (une par participant)

Participant : P<n> · Profil : <…> · Date : <…>

| Tâche | Réussite (seul / aidé / échec) | Temps | Erreurs | Hésitations (> 3 s) | Citations au moment du blocage | Confiance (pense avoir réussi ?) | Facilité (1 à 5) |
|---|---|---|---|---|---|---|---|
| T1 | | | | | | | |
| T2 | | | | | | | |
| T3 | | | | | | | |

SUS : <score /100>

## Synthèse du cycle (après les 5 participants)

| Problème observé | Participants concernés (/5) | Tâche | Sévérité | Citation | Ajustement le plus simple | Ticket |
|---|---|---|---|---|---|---|
| | | | | | | UX-<n> |

- Taux de réussite seul par tâche : T1 <…>/5 · T2 <…>/5 · T3 <…>/5
- SUS moyen : <…> (médiane <…>) · Référence : 68
- Hypothèses : <H… validée / invalidée>, avec preuves
- Ce que le test confirme de l'audit heuristique : <…>
- Ce que le test révèle de nouveau : <…>

## Prochaine étape

Corriger les problèmes de sévérité ≥ 3 par l'ajustement le plus simple, puis refaire un cycle de 5 sur la version corrigée.
