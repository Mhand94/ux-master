# Rechercher et tester : la méthode complète

Un audit heuristique trouve des violations de principes. Seuls de vrais utilisateurs révèlent ce qu'ils font, veulent et comprennent. Ce fichier donne la méthode pour **découvrir** (entretiens, observation), **synthétiser** (thèmes, personas, parcours) et **tester** (utilisabilité, SUS), puis **mesurer** après le lancement.

Gabarits prêts à remplir : `templates/guide-entretien.md`, `templates/protocole-test.md`.

---

## 1. Avant de concevoir : la découverte

### Quand

Avant de dessiner le moindre écran, et à chaque fois qu'une hypothèse risquée n'a pas été vérifiée. Règle pratique : **aucun écran ne part en développement tant que son hypothèse principale n'a pas été confrontée à au moins trois vrais utilisateurs.**

### Lister les hypothèses risquées

Écrire ce que l'on croit sans l'avoir vérifié, et ce qui se passe si c'est faux :

| Hypothèse | Si elle est fausse… | Comment la vérifier |
|---|---|---|
| Le problème existe et fait souffrir aujourd'hui | Pas de produit | Entretiens : récit du dernier épisode |
| La cible accepte de payer pour la solution | Modèle économique cassé | Entretiens : ce qu'elle paie déjà, combien, pour quoi |
| La cible utilise tel support à tel moment | Mauvaise plateforme prioritaire | Entretiens + observation |
| Le mécanisme central (swipe, inversion de rôle…) est compris et accepté | Refonte du cœur | Test d'utilisabilité sur maquette |

### Recruter

- **5 à 8 personnes par type d'utilisateur**. Au-delà, les thèmes se répètent ; en dessous, un cas isolé pèse trop.
- Des personnes qui vivent le problème **aujourd'hui**, pas des amis qui l'imaginent.
- Où les trouver : là où elles sont déjà (commerces, groupes locaux, associations professionnelles, clients existants, forums). Proposer un dédommagement modeste ou un service.
- À distance : visio ou téléphone, 20 à 30 minutes, fonctionne très bien pour les entretiens ; l'observation terrain peut être déléguée à une personne sur place munie d'une grille.

### Consentement et RGPD

Avant chaque entretien : expliquer l'objectif, la durée, l'usage des notes ; demander l'accord pour enregistrer (audio ou vidéo) ; préciser que la personne peut arrêter à tout moment ; anonymiser les notes (prénom fictif ou initiales). Conserver les enregistrements le temps de l'analyse, puis les supprimer.

### Structure d'un entretien de 30 minutes

| Temps | Phase | Objectif |
|---|---|---|
| 2 min | Introduction | Objectif, durée, anonymat, « il n'y a pas de bonne réponse », accord d'enregistrement |
| 5 min | Contexte | Qui est la personne, son quotidien, sa place dans le problème |
| 15 min | Récit du dernier épisode | « Racontez-moi la dernière fois que… », du déclencheur au résultat, étape par étape |
| 5 min | Douleurs et contournements | Ce qui a été le plus pénible, ce qu'elle a bricolé, ce qu'elle paie ou a payé |
| 3 min | (Optionnel) Réaction à une maquette | Seulement après le récit, pour ne pas orienter ; observer, ne pas vendre |
| 1 min | Clôture | Remercier, demander si l'on peut recontacter, demander une mise en relation |

### Les règles d'or

1. **Des faits passés, jamais des intentions.** « Racontez-moi la dernière fois que vous avez cherché quelqu'un » plutôt que « Utiliseriez-vous une app pour recruter ? ». Tout le monde répond oui à la seconde, et cela ne prédit rien.
2. **Ne pas parler du produit** pendant les deux premiers tiers. Dès qu'on le montre, la personne cesse de raconter sa vie et commence à évaluer votre travail.
3. **Relancer** sans suggérer : « Pourquoi ? », « Et ensuite ? », « Comment vous avez fait ? », « Qu'est-ce qui s'est passé après ? », « Vous pouvez me donner un exemple ? ».
4. **Écouter 80 % du temps.** Un silence de trois secondes fait souvent sortir la phrase la plus utile.
5. **Noter les citations exactes**, pas des résumés : « je mets une affichette et je prie » vaut plus que « utilise des méthodes traditionnelles ».
6. **Ne pas défendre le produit**, ne pas corriger la personne, ne pas expliquer. On apprend ; on ne convainc pas.
7. **Chercher le comportement, pas l'opinion.** Ce qu'elle a fait, payé, abandonné, bricolé, compte ; ce qu'elle « pense qu'il faudrait » compte peu.

### Banque de questions (à adapter au domaine)

**Pour un décideur ou un acheteur** (celui qui a le problème et le budget) :

- Racontez-moi la dernière fois que [le problème] s'est posé. Comment avez-vous su qu'il se posait ?
- Qu'avez-vous fait en premier ? Et ensuite ? Combien de temps cela a pris ?
- Qu'est-ce qui a été le plus pénible ? Qu'est-ce qui a bien marché ?
- Comment avez-vous choisi entre les options ? Qu'avez-vous regardé en premier ?
- Avez-vous déjà payé pour résoudre ce problème ? Combien ? Était-ce rentable ?
- Quand vous traitez ce genre de chose, c'est sur quel appareil ? À quel moment de la journée ? Debout, assis ?
- Qu'est-ce qui vous ferait dire « cette fois, ça s'est bien passé » ?

**Pour un utilisateur final** (celui qui se sert du produit au quotidien) :

- Racontez-moi votre dernière [recherche, démarche, utilisation]. Par où avez-vous commencé ?
- Qu'attendiez-vous qu'il se passe ensuite ? Que s'est-il passé réellement ?
- À quel moment avez-vous hésité, ou failli abandonner ?
- Qu'avez-vous fait quand vous n'avez pas eu de réponse ?
- Quelles apps ou quels outils utilisez-vous déjà pour ce genre de chose ? Qu'est-ce que vous aimez dedans ?
- Si vous aviez un seul vœu pour que ce soit plus simple, ce serait quoi ? (en dernier, et à prendre avec prudence)

**Pour l'observation terrain** (grille à remplir sur place, une heure) : rythme et interruptions · appareils présents et où ils sont posés · moments où la personne cherche une information · bricolages visibles (post-it, cahier, affichette) · qui d'autre intervient · ce qu'elle fait en attendant.

### Grille de prise de notes

| Citation exacte | Thème provisoire | Douleur ou besoin | Hypothèse touchée | Intensité (1 à 3) |
|---|---|---|---|---|
| « … » | | | | |

Remplir pendant l'entretien ou immédiatement après, jamais le lendemain.

---

## 2. Synthétiser : des notes aux décisions

### Regroupement par affinités

1. Une citation par carte (post-it ou outil de tableau blanc).
2. Regrouper les cartes qui parlent de la même chose, sans catégories préétablies ; nommer chaque groupe par une phrase à la première personne (« Je ne sais jamais si la personne va venir au rendez-vous »).
3. Compter : un thème cité par la majorité des participants est un **vrai problème** ; un thème cité une fois est une anecdote.
4. Pour chaque thème majeur, noter : fréquence, intensité, contournements actuels, ce que les gens paient déjà.

### Personas (méthode Cooper)

Un persona est un portrait **tiré des entretiens**, pas un stéréotype marketing.

```
Prénom, rôle, situation en une phrase
Contexte : où, quand, sur quoi il utilise le produit
Objectifs finaux : ce qu'il veut accomplir (2 ou 3)
Objectifs d'expérience : comment il veut se sentir (1 ou 2)
Frustrations actuelles : citations
Comportements observés : ce qu'il fait réellement aujourd'hui
Niveau numérique : apps qu'il maîtrise
Ce qu'il ne fera jamais : limites à respecter
Primaire / secondaire / négatif
```

Un seul persona **primaire** par interface. Les autres sont secondaires ou négatifs.

### Jobs à accomplir

Pour chaque thème majeur : « **Quand** [situation déclenchante], **je veux** [motivation], **pour** [résultat attendu]. » Le job est stable ; les solutions changent. Il guide le mode A.

### Carte du parcours actuel

| Étape | Ce que la personne fait | Ce qu'elle pense | Émotion (−2 à +2) | Douleur | Opportunité |
|---|---|---|---|---|---|
| Déclencheur | | | | | |
| Recherche | | | | | |
| Choix | | | | | |
| Action | | | | | |
| Suite | | | | | |

Le produit doit soulager d'abord les étapes à −2.

### Questions « Comment pourrions-nous… ? »

Chaque douleur majeure devient un défi de conception ouvert : « Comment pourrions-nous éviter que le candidat ne vienne pas au rendez-vous ? ». Ces questions ouvrent le mode A ; elles ne présupposent pas la solution.

### Mettre à jour la liste des hypothèses

Pour chaque hypothèse de départ : **validée**, **invalidée** ou **à tester en utilisabilité**, avec les citations qui le justifient. Les hypothèses invalidées changent le produit, pas le discours.

---

## 3. Tester : le test d'utilisabilité

### Quand

Dès qu'il existe quelque chose à montrer : croquis, maquette interactive, version de développement. Plus c'est tôt, moins c'est cher à corriger. Puis à chaque évolution importante.

### Participants

- **5 participants** représentatifs du persona primaire par cycle. Au-delà, on revoit les mêmes problèmes ; mieux vaut corriger et refaire un cycle de cinq.
- Pas de membres de l'équipe, pas de proches qui connaissent le projet.
- Un cycle court et régulier (trois participants par mois, méthode Krug) vaut mieux qu'un grand test annuel.

### Déroulé d'une session de 45 minutes

| Temps | Phase |
|---|---|
| 5 min | Accueil : objectif (« on teste le produit, pas vous »), penser à voix haute, accord d'enregistrement, pas de bonne réponse |
| 3 min | Questions de contexte (deux ou trois, pour situer la personne) |
| 30 min | 3 à 5 tâches, une par une |
| 5 min | Questions post-test et SUS |
| 2 min | Remerciement |

### Rédiger les tâches

Une tâche est une **situation**, jamais une instruction qui nomme les éléments de l'interface.

| Mauvaise formulation | Bonne formulation |
|---|---|
| « Cliquez sur Explorer puis épinglez un candidat » | « Vous cherchez une vendeuse disponible tout de suite près de chez vous. Gardez de côté celle qui vous plaît le plus. » |
| « Utilisez le filtre quartier » | « Vous ne voulez voir que des personnes de votre quartier. Faites ce qu'il faut. » |

Ordonner les tâches de la plus simple à la plus complexe ; commencer par la tâche principale du produit si l'on n'a le temps que pour une.

### Conduite

- **Ne jamais aider.** Si la personne bloque, demander « que feriez-vous si j'étais absent ? ». Si elle est vraiment coincée, noter l'échec et passer à la suite.
- **Ne pas expliquer**, ne pas défendre, ne pas réagir aux erreurs (ni sourire gêné, ni « ah »).
- **Relancer la pensée à voix haute** : « Qu'est-ce que vous regardez ? », « À quoi vous vous attendiez ? ».
- Un observateur prend les notes ; le modérateur se concentre sur la personne.

### Mesures par tâche

| Mesure | Comment |
|---|---|
| **Réussite** | Réussie seule · Réussie avec aide · Échec ou abandon |
| **Temps** | Du début de la lecture de la tâche à la réussite ou à l'abandon |
| **Erreurs** | Actions hors du chemin attendu ; retours en arrière |
| **Hésitations** | Pauses de plus de trois secondes avant d'agir ; relecture ; « hmm » |
| **Citations** | Phrases exactes au moment du blocage |
| **Confiance** | Après la tâche : « Pensez-vous avoir réussi ? » (révèle les fausses réussites) |

### Questionnaire SUS (System Usability Scale)

Dix affirmations notées de 1 (pas du tout d'accord) à 5 (tout à fait d'accord). Le questionnaire a été créé par John Brooke (1986) et est libre d'utilisation avec mention de la source.

1. Je pense que j'aimerais utiliser ce système fréquemment.
2. J'ai trouvé ce système inutilement complexe.
3. J'ai trouvé ce système facile à utiliser.
4. Je pense que j'aurais besoin de l'aide d'une personne technique pour pouvoir utiliser ce système.
5. J'ai trouvé que les différentes fonctions de ce système étaient bien intégrées.
6. J'ai trouvé qu'il y avait trop d'incohérences dans ce système.
7. J'imagine que la plupart des gens apprendraient très vite à utiliser ce système.
8. J'ai trouvé ce système très lourd à utiliser.
9. Je me suis senti très en confiance en utilisant ce système.
10. J'ai dû apprendre beaucoup de choses avant de pouvoir utiliser ce système.

**Calcul** : pour les items impairs (1, 3, 5, 7, 9), prendre la note − 1 ; pour les items pairs (2, 4, 6, 8, 10), prendre 5 − la note. Additionner les dix contributions et multiplier par 2,5. Le résultat est sur 100.

**Lecture** : 68 est la moyenne des produits mesurés ; en dessous de 50, le produit est en difficulté ; au-dessus de 80, l'utilisabilité est excellente. Le SUS mesure le **ressenti**, pas la performance : le croiser avec le taux de réussite.

### Analyser et rapporter

1. Lister chaque problème observé, avec le nombre de participants concernés (sur 5) et une citation.
2. Attribuer une sévérité (voir `scoring.md`) : un problème qui a fait échouer trois participants sur cinq à la tâche principale est un 4.
3. Rapprocher des constats de l'audit heuristique : ce que le test confirme, ce qu'il contredit, ce qu'il révèle de nouveau.
4. Pour chaque problème de sévérité ≥ 2, proposer **l'ajustement le plus simple** qui le résout (Krug), puis le ticket Claude Code.
5. Mettre à jour la liste des hypothèses : validées, invalidées.

---

## 4. Après le lancement : mesurer en continu

| Indicateur | Définition | Pourquoi |
|---|---|---|
| **Entonnoir** | Taux de passage entre chaque étape clé (installation → inscription → première action → moment magique → action payante) | Montre où les gens abandonnent |
| **Time-to-value** | Temps médian entre l'inscription et le moment magique | L'indicateur UX le plus prédictif de la rétention |
| **Taux de complétion de la tâche principale** | Part des sessions où la tâche principale aboutit | Mesure directe de l'utilisabilité en conditions réelles |
| **Rétention J1 / J7 / J30** | Part des nouveaux utilisateurs actifs un, sept et trente jours après l'inscription | Dit si le produit tient sa promesse |
| **Taux d'erreur** | Part des actions qui déclenchent un message d'erreur | Repère les écrans à auditer |
| **Rage taps / clics morts** | Taps répétés au même endroit sans effet ; clics sur des éléments non interactifs | Signifiants manquants (L1) |
| **Désinstallation et désabonnement** | Taux et moment | Révèle les promesses non tenues |

### Rituels

- **Un entretien utilisateur par semaine**, trente minutes, avec un utilisateur réel : la source la plus riche et la moins chère.
- **Un cycle de test d'utilisabilité par version majeure.**
- **Revue mensuelle de l'entonnoir** : l'étape qui perd le plus devient le prochain audit (mode B).
- **Enregistrements de sessions et heatmaps** uniquement avec consentement explicite et anonymisation ; les données personnelles ne sont jamais capturées.

### RGPD en pratique

- Consentement explicite pour les analytics non essentiels et pour tout enregistrement ; refus aussi facile que l'acceptation (aucun dark pattern dans la bannière, voir L5).
- Minimisation : ne collecter que les événements qui servent une décision.
- Anonymiser les notes d'entretien et de test ; supprimer les enregistrements après analyse.
- Documenter les traitements (registre) ; permettre l'accès, la rectification et la suppression des données.
