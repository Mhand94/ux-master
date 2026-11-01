# Les six lentilles en détail

Chaque lentille est présentée de la même façon : origine, idée centrale, concepts à vérifier avec leurs **signes d'alerte** (ce que l'on voit dans l'interface quand le principe est violé) et leurs **corrections types**, puis les **pièges d'interprétation**. La dernière section cartographie les recoupements entre lentilles pour ne jamais consigner deux fois le même constat.

Les lentilles sont des reformulations opérationnelles des travaux cités. Pour la pensée complète de chaque auteur, lire la source indiquée.

---

## L1 · Don Norman : le modèle d'interaction

**Source** : *The Design of Everyday Things* (1988, édition révisée 2013). Norman est aussi celui qui a nommé l'« expérience utilisateur » chez Apple, au début des années 1990.

**Idée centrale** : quand une personne se trompe avec un objet ou un écran, la faute revient à la conception, pas à la personne. Le design doit rendre visible ce qu'on peut faire, et visible ce qui s'est passé.

### Concepts à vérifier

| Concept | Définition opérationnelle | Signes d'alerte | Corrections types |
|---|---|---|---|
| **Affordance** | Ce que l'objet permet réellement (un écran tactile permet de toucher partout) | On croit qu'un élément est actif alors qu'il ne l'est pas, ou l'inverse | Aligner apparence et possibilité réelle |
| **Signifiant** | L'indice perceptible qui dit *où* et *comment* agir | Carte glissable sans indice ; texte cliquable identique au texte normal ; icône seule ambiguë ; action accessible uniquement par appui long | Relief ou ombre légère, libellé, animation d'amorce au premier affichage (la carte « dépasse » légèrement), bouton équivalent au geste |
| **Correspondance (mapping)** | La disposition de la commande ressemble à son effet | Flèche « suivant » à gauche ; ordre des champs différent de l'ordre logique ; curseur vertical pour une valeur horizontale | Aligner spatialement commande et effet ; respecter le sens de lecture |
| **Feedback** | Réponse immédiate, informative, proportionnée | Tap sans réaction visible ; indicateur de chargement muet pendant plus de trois secondes ; toast qui disparaît avant d'être lu ; modale de succès pour une action banale | État « pressé » visible, micro-animation, texte de progression, toast de 4 à 6 secondes avec action, succès signalé en place plutôt qu'en modale |
| **Contraintes** | Rendre l'erreur impossible ou improbable | Bouton actif alors que le formulaire est invalide, sans explication ; saisie libre là où un sélecteur suffirait | Désactiver **et** expliquer pourquoi ; sélecteurs, masques de saisie, valeurs par défaut sûres |
| **Modèle conceptuel** | L'histoire que l'utilisateur se raconte sur le fonctionnement | Deux actions proches qui semblent identiques (« épingler » et « contacter ») ; même icône pour deux sens ; une action dont l'effet n'est jamais montré | Libellés explicites, résultat de l'action rendu visible, vocabulaire stable |
| **Connaissance dans le monde** | Afficher plutôt que faire mémoriser | Code à retenir d'un écran à l'autre ; filtres actifs invisibles ; valeurs précédentes à ressaisir | Rappeler le contexte à l'écran, préremplir, afficher les filtres actifs |

### Les sept étapes de l'action et les deux fossés

| Étape | Question à poser à l'interface |
|---|---|
| 1. But | L'écran répond-il au but de l'utilisateur, ou à celui du système ? |
| 2. Plan | Voit-il par quelle option commencer ? |
| 3. Spécification | Sait-il quel geste précis effectuer ? |
| 4. Exécution | Le geste est-il facile et sûr (taille, position) ? |
| 5. Perception | Le changement d'état est-il visible ? |
| 6. Interprétation | Comprend-il ce que signifie ce changement ? |
| 7. Comparaison | Peut-il juger si le but est atteint ? |

Les étapes 2 à 4 forment le **fossé d'exécution** (« comment je fais ? »), les étapes 5 à 7 le **fossé d'évaluation** (« est-ce que ça a marché ? »). Un constat de L1 se rattache toujours à l'un des deux.

### Erreurs : ratés et méprises

- **Raté** (*slip*) : l'intention est bonne, le geste est faux. Tap à côté, double envoi, geste mal interprété, erreur de mode (on croyait être dans l'autre onglet). Correction : cibles généreuses, Annuler systématique, modes visibles, protection contre le double envoi.
- **Méprise** (*mistake*) : l'intention est fausse parce que le modèle conceptuel est faux. Correction : libellés, aide contextuelle, montrer le résultat avant de valider.
- **Fonctions de forçage** : empêcher physiquement l'erreur (impossible de valider sans le champ requis), ou verrouiller (confirmation uniquement pour l'irréversible : suppression définitive, paiement).
- **Règle** : préférer l'annulation à la confirmation. La confirmation systématique s'automatise et ne protège plus de rien.

### Pièges

- Ajouter un tutoriel ne corrige pas un signifiant manquant ; c'est un aveu que l'écran ne s'explique pas seul.
- Un feedback n'est pas une notification : il répond à une action de l'utilisateur, il ne l'interrompt pas.
- Désactiver un bouton sans dire pourquoi crée un fossé d'exécution pire que le bouton actif.

---

## L2 · Jakob Nielsen : les dix heuristiques

**Source** : « 10 Usability Heuristics for User Interface Design » (1994, mis à jour sur nngroup.com), et la méthode d'évaluation heuristique qui les accompagne.

**Idée centrale** : des principes généraux, vérifiables par un évaluateur, qui détectent la majorité des problèmes d'utilisabilité avant tout test.

| # | Heuristique | Ce qu'elle exige | Signes d'alerte | Corrections types |
|---|---|---|---|---|
| 1 | Visibilité de l'état du système | L'utilisateur sait toujours ce qui se passe, dans un délai raisonnable | Chargement muet ; envoi sans accusé ; progression inconnue dans un parcours | Indicateurs, jauge d'étapes, statut explicite (« Envoyé », « En attente de réponse ») |
| 2 | Correspondance avec le monde réel | Mots, concepts et ordre familiers à l'utilisateur | Jargon interne (« entité », « item », « soumettre ») ; codes ; ordre technique | Vocabulaire du métier de l'utilisateur, exemples concrets, ordre naturel |
| 3 | Contrôle et liberté | Sortie de secours, Annuler, Rétablir | Modale sans fermeture ; parcours sans retour ; action irréversible sans annulation | Bouton fermer, retour toujours possible, Annuler sur toute action réversible |
| 4 | Cohérence et standards | Mêmes mots, mêmes composants, mêmes positions ; conventions de plateforme | Trois libellés pour une même action ; bouton principal qui change de place ; icône détournée de son sens habituel | Design system appliqué, glossaire, conventions iOS / Android / web |
| 5 | Prévention des erreurs | Supprimer les situations à risque, demander confirmation pour l'irréversible | Champ date libre ; suppression en un tap ; options proches aux effets opposés | Sélecteurs, valeurs par défaut, confirmation ciblée, séparation des actions dangereuses |
| 6 | Reconnaître plutôt que se souvenir | Options et informations visibles au moment utile | Saisie à refaire ; critères de filtre cachés ; instruction donnée deux écrans plus tôt | Préremplissage, récapitulatifs, rappels contextuels |
| 7 | Flexibilité et efficacité | Accélérateurs pour les habitués, sans gêner les novices | Aucun raccourci clavier sur PC ; impossible d'agir sur plusieurs éléments ; favoris absents | Raccourcis, actions groupées, récents, personnalisation légère |
| 8 | Esthétique et minimalisme | Chaque élément en trop concurrence l'essentiel | Texte d'accueil, bannières, trois CTA de même poids, décorations | Supprimer, hiérarchiser, un seul élément dominant |
| 9 | Reconnaître, diagnostiquer, corriger les erreurs | Message en langage clair, cause précise, solution | « Une erreur est survenue » ; code technique ; message loin du champ fautif | Message près du champ, cause, action proposée, ton non accusateur |
| 10 | Aide et documentation | Aide contextuelle, courte, au moment du besoin | FAQ hors de l'app ; tutoriel long au premier lancement | Infobulles, exemples dans les champs, aide à l'endroit du blocage |

### Méthode d'évaluation heuristique

- Idéalement 3 à 5 évaluateurs indépendants, puis consolidation ; seul, compenser en passant deux fois : une passe « vue d'ensemble », une passe « élément par élément ».
- Chaque problème reçoit une sévérité (voir `scoring.md`) qui combine fréquence, impact et persistance.
- Cinq utilisateurs en test révèlent la majorité des problèmes majeurs ; plusieurs petits tests itératifs valent mieux qu'un grand test unique.
- Une évaluation heuristique trouve des violations de principes ; un test utilisateur trouve des comportements réels. Les deux sont nécessaires, ils ne se remplacent pas.

### Pièges

- Attribuer un constat à plusieurs heuristiques ne le rend pas plus grave ; une seule catégorie suffit.
- Les heuristiques détectent, elles ne priorisent pas : la priorité vient de la sévérité et de la fréquence.

---

## L3 · Steve Krug : la clarté immédiate

**Source** : *Don't Make Me Think* (2000, 3e édition 2014) et *Rocket Surgery Made Easy* (2010).

**Idée centrale** : les utilisateurs ne lisent pas, ils **survolent** ; ils ne choisissent pas la meilleure option, mais **la première raisonnable** ; ils ne comprennent pas comment ça marche, ils **se débrouillent**. Concevoir pour cette réalité, pas pour un lecteur attentif imaginaire.

### Les trois lois de Krug

1. **Ne me faites pas réfléchir.** Chaque élément doit être évident ; à défaut, s'expliquer de lui-même en une fraction de seconde.
2. **Le nombre de clics importe peu, si chaque clic est évident et sans ambiguïté.** Trois clics évidents valent mieux qu'un clic hésitant.
3. **Supprimez la moitié des mots de chaque écran, puis la moitié de ce qui reste.** Le bavardage et les instructions disparaissent en premier.

### Checklist

| Point | Signes d'alerte | Corrections types |
|---|---|---|
| **Test des cinq secondes** | On hésite sur le rôle de l'écran ou sur l'action à faire | Titre explicite, un seul élément dominant, suppression du bruit |
| **Test du coffre** (sur un écran quelconque, pris au hasard) : quelle app ? quelle section ? où suis-je ? quelles options ? comment chercher ou revenir ? | Un seul « je ne sais pas » | Titre de section, état actif dans la navigation, retour visible |
| **Hiérarchie visuelle** | Deux éléments de même poids qui n'ont pas la même importance ; éléments liés dispersés | Taille, graisse, contraste et espace proportionnels à l'importance ; regroupement |
| **Conventions** | Innovation gratuite (geste inventé, icône maison, menu inhabituel) | Revenir à la convention ; innover seulement si c'est nettement meilleur et que la différence est signalée |
| **Cliquable évident** | Doute sur ce qui réagit au toucher | Formes de bouton, soulignement, couleur d'action réservée aux actions |
| **Bruit** | Bannières, texte d'accueil, animations décoratives, trois niveaux de promotion | Supprimer ; garder le contenu et les actions |
| **Texte pour le survol** | Paragraphes, instructions longues | Titres, listes courtes, mots-clés en gras, phrases d'une ligne |

### Le réservoir de bonne volonté

Chaque utilisateur arrive avec un capital de patience, variable et personnel. L'interface le vide ou le remplit.

- **Le vide** : cacher une information attendue (prix, délai, conditions) ; imposer un format de saisie que la machine pourrait tolérer ; demander des données inutiles ; interrompre (pop-ups, demandes de notation) ; donner l'impression d'une fausse sincérité ; faire travailler l'utilisateur pour une chose que le produit devrait savoir.
- **Le remplit** : rendre la chose principale facile ; répondre aux questions évidentes au bon endroit ; épargner des étapes ; permettre de se rattraper après une erreur ; s'excuser et expliquer quand ça coince.

### Tests « maison »

Krug défend des tests fréquents et légers : trois participants par mois, une matinée, l'équipe observe, débriefing le midi, et l'on corrige d'abord les problèmes les plus graves par **l'ajustement le plus simple** possible, pas par une refonte. Protocole détaillé dans `recherche-et-tests.md`.

### Pièges

- « Ajouter une explication » est rarement la solution : si l'écran a besoin d'un texte pour être compris, c'est l'écran qu'il faut changer.
- Sur mobile, les fonctions cachées (menus, gestes) sont la première source de « je ne savais pas qu'on pouvait ».

---

## L4 · Alan Cooper : la conception par objectifs

**Source** : *About Face* (1995, 4e édition 2014, avec Reimann, Cronin et Noessel) et *The Inmates Are Running the Asylum* (1999).

**Idée centrale** : on ne conçoit pas pour « les utilisateurs », on conçoit pour **une personne précise** qui poursuit **un objectif précis**. Les tâches changent avec la technologie ; les objectifs restent.

### Personas

- Construits à partir de recherches réelles (entretiens, observation), jamais inventés en réunion.
- **Un seul persona primaire** par interface : s'il est satisfait, les autres le sont ou ne sont pas trahis. Les personas secondaires ajoutent des besoins ponctuels. Un persona négatif dit explicitement pour qui on ne conçoit pas.
- Décrits par leurs comportements, objectifs, frustrations et contexte ; la démographie n'est là que si elle change le design.
- Portent un prénom et une situation concrète ; on doit pouvoir dire « que ferait Nadia ici ? ».

### Objectifs

| Type | Question | Exemple |
|---|---|---|
| D'expérience | Comment la personne veut-elle se *sentir* ? | Ne pas se sentir stupide, ne pas perdre de temps |
| Finaux | Que veut-elle *accomplir* ? | Trouver quelqu'un de fiable pour samedi |
| De vie | Qui veut-elle *être* ? | Un patron qui gère bien son équipe |

L'interface sert l'objectif final sans violer les objectifs d'expérience.

### Concepts à vérifier

| Concept | Signes d'alerte | Corrections types |
|---|---|---|
| **Scénario de contexte** | Le flux a été dessiné écran par écran, sans récit d'usage | Écrire d'abord le récit du persona, du déclencheur au résultat, puis en déduire les écrans |
| **Intermédiaires permanents** | Interface pensée pour le débutant (tout expliqué, lent) ou pour l'expert (dense, sans guidage) | Apprentissage rapide, puis raccourcis ; l'aide s'efface quand on progresse |
| **Excise** | Travail imposé qui ne sert pas l'objectif : confirmations, ressaisies, navigations répétées, réglages préalables, écrans intermédiaires | Supprimer, préremplir, mémoriser, fusionner |
| **Posture** | Produit transitoire traité comme souverain (trop dense) ou l'inverse (trop vide) | Transitoire : simple, gros éléments, une action. Souverain : dense, efficace, clavier, fenêtre pleine |
| **Logiciel poli** | Questions inutiles, confirmations systématiques, préférences oubliées, messages accusateurs | Mémoriser, anticiper, proposer des valeurs par défaut intelligentes, assumer ses erreurs |
| **Feedback non modal** | Chaque information bloque la progression | Informer en place, sans modale, sans interrompre |
| **Concevoir pour le probable, prévoir le possible** | Le cas rare pèse autant que le cas courant dans l'interface | Chemin principal optimisé ; cas rares accessibles mais discrets |

### Pièges

- Un persona sans recherche est une fiction : le marquer **[Hypothèse]** et prévoir les entretiens qui le confirmeront.
- Satisfaire tout le monde produit une interface qui ne satisfait personne ; choisir le primaire est une décision, pas une omission.

---

## L5 · Dieter Rams : les dix principes du bon design

**Source** : les dix principes formulés par Rams dans les années 1970-1980 (travaux pour Braun et Vitsœ), résumés par « *Weniger, aber besser* », moins, mais mieux.

**Idée centrale** : un bon design est utile, compréhensible, honnête et discret ; il se concentre sur l'essentiel et soigne chaque détail.

| Principe | Traduction logicielle | Signes d'alerte |
|---|---|---|
| **Innovant** | Un vrai progrès pour l'utilisateur, pas une nouveauté gratuite | Geste inventé, interface « originale » qui ralentit |
| **Utile** | Chaque élément sert la tâche | Widgets décoratifs, données affichées sans usage |
| **Esthétique** | La qualité visuelle fait partie de l'utilité | Désordre, alignements approximatifs, hiérarchie floue |
| **Compréhensible** | Le produit s'explique de lui-même | Besoin d'un tutoriel, d'infobulles partout |
| **Discret** | L'interface s'efface derrière le contenu et la tâche | Marque et décor plus visibles que le contenu |
| **Honnête** | Aucune promesse non tenue, aucune manipulation | Dark patterns (ci-dessous) |
| **Durable** | Résiste aux modes | Effets à la mode (dégradés, verre dépoli, ombres lourdes) qui vieilliront |
| **Minutieux jusqu'au dernier détail** | Tous les états sont conçus | États vides, erreurs ou chargements laissés par défaut |
| **Respectueux de l'environnement** | Sobre en données, batterie, notifications, attention | Notifications fréquentes, images lourdes, animations permanentes |
| **Aussi peu de design que possible** | Retirer tout ce qui n'est pas essentiel | Trois façons de faire la même chose |

### Dark patterns à bannir (principe « honnête »)

Culpabilisation du refus (« Non merci, je préfère payer plus cher ») · case pré-cochée · coût caché jusqu'au dernier écran · abonnement facile, résiliation cachée · faux compte à rebours ou fausse rareté · question piège à double négation · harcèlement (redemander après un refus) · obstruction (désinscription en huit étapes) · interférence visuelle (le bouton de refus déguisé en lien gris).

### Les sept états à concevoir (principe « minutieux »)

Vide (premier usage, aucune donnée) · Chargement · Erreur (réseau, serveur, validation) · Succès · Première utilisation (découverte) · Hors ligne · Permission refusée (caméra, position, notifications). Chaque état explique, rassure et propose une action.

### Pièges

- Minimalisme ne veut pas dire vide : retirer le superflu, pas l'information utile.
- « Honnête » s'applique aussi aux micro-textes : pas de « Gratuit » si une carte bancaire est demandée.

---

## L6 · Steve Jobs et Jony Ive : le focus et le bout en bout

**Source** : pratique d'Apple des années 1997-2019, telle que documentée par les biographies et les entretiens publics. Ce n'est pas une méthode académique ; on l'applique comme un jeu de questions, pas comme un dogme.

**Idée centrale** : partir de l'expérience que l'on veut faire vivre, dire non à tout ce qui la dilue, et soigner l'ensemble du parcours comme un seul produit.

| Principe | Question à poser | Signes d'alerte | Corrections types |
|---|---|---|---|
| **Partir de l'expérience** | Qu'est-ce que la personne doit ressentir, et quand ? | Le flux reproduit la structure de la base de données | Réécrire le parcours depuis le ressenti visé, puis adapter la technique |
| **Dire non** | Que retire-t-on pour que l'essentiel soit excellent ? | Dix fonctionnalités moyennes ; menu « plus » fourre-tout | Liste explicite des « non » et de leur justification ; MVP réellement minimal |
| **Moment magique** | À quel instant la personne pense « c'est exactement ce qu'il me fallait » ? Combien de temps pour y arriver ? | Inscription longue avant toute valeur ; démo impossible en trente secondes | Time-to-value mesuré et raccourci ; valeur montrée avant toute demande |
| **Simplicité profonde** | A-t-on compris le problème assez à fond pour que la solution paraisse évidente ? | Options exposées parce qu'on n'a pas su choisir | Choisir la valeur par défaut juste ; cacher le réglage rare |
| **Bout en bout** | Le store, l'inscription, la notification, l'e-mail, le support et la désinscription sont-ils au même niveau que l'écran principal ? | E-mails bruts, page 404 par défaut, support injoignable | Traiter chaque point de contact comme un écran du produit |
| **Soin de l'invisible** | Les transitions, micro-textes, états intermédiaires, comportements hors connexion sont-ils conçus ? | Sauts d'affichage, textes par défaut, écrans blancs | Transitions sobres, squelettes, textes écrits, hors ligne géré |
| **Ça marche, tout simplement** | Faut-il configurer avant d'utiliser ? | Écran de préférences avant le premier usage | Valeurs par défaut justes ; configuration différée au moment du besoin |

### Pièges

- Le focus se décide à partir des objectifs du persona (L4), pas du goût de l'équipe.
- « Simple » n'est pas « pauvre » : un dashboard souverain peut être dense et rester simple si tout est à sa place.

---

## Recoupements entre lentilles

Un constat est classé **une seule fois**, dans sa catégorie (voir SKILL.md), avec la lentille principale et les secondaires entre parenthèses. Le tableau indique les recoupements les plus fréquents.

| Type de constat | Lentilles qui le détectent | Catégorie |
|---|---|---|
| Trop de mots, trop d'options, bruit visuel | L3 (mots, bruit), L2 n°8, L5 « aussi peu que possible » | CHG |
| Pas d'Annuler, pas de sortie | L1 (erreurs), L2 n°3, L4 (logiciel poli) | ERR |
| Convention de plateforme violée | L2 n°4, L3 (conventions), loi de Jakob | COH |
| Geste caché sans indice | L1 (signifiant), L3 (cliquable évident, mobile) | ACT |
| Action sans réponse visible | L1 (feedback), L2 n°1 | FBK |
| Information à mémoriser entre écrans | L1 (connaissance dans le monde), L2 n°6, L4 (excise) | CHG |
| Message d'erreur technique ou accusateur | L2 n°9, L4 (ne blâme jamais), L1 (fossé d'évaluation) | ERR ou CTN selon la cause |
| Travail inutile imposé | L4 (excise), L3 (réservoir), L6 (dire non) | VAL |
| État vide ou d'erreur non conçu | L5 (minutieux), L6 (invisible), L2 n°1 | ETA |
| Dark pattern, promesse non tenue | L5 (honnête), L3 (réservoir) | ETH |
| Valeur montrée trop tard, paywall prématuré | L6 (moment magique), L4 (objectifs), L3 (réservoir) | VAL |
| Cible trop petite, contraste faible | Socle (Fitts, accessibilité), L1 (exécution) | ACC |
| Vocabulaire interne, jargon | L2 n°2, L3 (mots), L1 (modèle conceptuel) | CTN |

Quand deux catégories semblent possibles, choisir celle qui décrit **la cause** du problème, pas son symptôme : un message d'erreur illisible parce que le système ne sait pas quoi dire est ERR ; le même message illisible parce qu'il est rédigé en jargon est CTN.
