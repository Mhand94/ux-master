# UX Master — skill Claude Code

Une méthode UX opérationnelle, en français, qui réunit en un seul outil les apports de **Don Norman**, **Jakob Nielsen**, **Steve Krug**, **Alan Cooper**, **Dieter Rams** et **Steve Jobs / Jony Ive**. Le skill sert à **concevoir** un écran ou un parcours, **auditer** une maquette, une capture ou du code, et **préparer la recherche utilisateur** (entretiens, tests d'utilisabilité), avec des livrables prêts à l'emploi : rapport scoré, spécification d'écran, tickets Claude Code à coller tels quels.

## Pourquoi

Construire une application avec Claude Code va vite. Construire la **bonne** application, que les gens comprennent du premier coup, demande une méthode. Sans elle, l'UX se décide au goût, écran par écran, et les problèmes se découvrent après la mise en ligne.

Ce skill donne à Claude une discipline de lead UX : il cadre avant de dessiner, passe chaque écran au crible de six lentilles complémentaires, note la gravité des problèmes avec une échelle fixe, priorise les corrections par rapport à leur effort, et transforme chaque constat en un ticket exécutable. Il distingue toujours ce qui est **prouvé** (observé chez de vrais utilisateurs) de ce qui est **supposé**.

## Ce que le skill fait

| Mode | Quand | Livrable |
|---|---|---|
| **A · Concevoir** | Un écran, un parcours ou une fonctionnalité à créer | Flux, spécification par écran (sept états, micro-textes, mesure), checklist pré-vol à 15 points, hypothèses à valider |
| **B · Auditer** | Une maquette, une capture, un prototype ou du code existant | Rapport : constats classés en 12 catégories, sévérité 0–4, score /100 par écran, priorisation sévérité × fréquence ÷ effort, tickets Claude Code |
| **C · Rechercher et tester** | Avant de concevoir, ou pour valider | Guide d'entretien, protocole de test d'utilisabilité à 5 participants, questionnaire SUS, synthèse (thèmes, personas, carte du parcours), métriques post-lancement |

Trois niveaux de profondeur calibrent l'effort : **Express** (un écran, huit constats au plus, trois correctifs), **Standard** (un parcours, score et tickets complets), **Complet** (toute l'application, plan de recherche inclus).

### Les six lentilles

| Lentille | Maître | Question posée à l'interface |
|---|---|---|
| Interaction | Don Norman | L'utilisateur voit-il quoi faire, et voit-il que ça a marché ? |
| Utilisabilité | Jakob Nielsen | Les dix heuristiques sont-elles respectées ? |
| Clarté | Steve Krug | Faut-il réfléchir pour comprendre l'écran ? |
| Objectifs | Alan Cooper | Pour qui exactement, et pour quel but réel ? |
| Design | Dieter Rams | Est-ce « moins, mais mieux », et honnête ? |
| Focus | Steve Jobs et Jony Ive | Fait-on une chose excellemment, de bout en bout ? |

Un **socle commun** complète les lentilles : lois cognitives chiffrées (Hick, Fitts, Doherty…), accessibilité WCAG 2.1 AA, règles iOS, Android et web.

## Installation

Le dossier du dépôt **est** le skill : `SKILL.md` à la racine, fichiers de référence à côté.

**Pour tous vos projets (skill personnel)**

```bash
git clone https://github.com/Mhand94/ux-master.git ~/.claude/skills/ux-master
```

**Pour un seul projet (skill partagé avec l'équipe, versionné avec le code)**

```bash
git clone https://github.com/Mhand94/ux-master.git .claude/skills/ux-master
```

ou, pour suivre les mises à jour :

```bash
git submodule add https://github.com/Mhand94/ux-master.git .claude/skills/ux-master
```

Claude Code charge automatiquement `.claude/skills/*/SKILL.md`. Aucune autre configuration.

**Dans claude.ai** : importez le dossier dans vos skills ; il sera disponible dans le chat et les sessions cloud. Seul `SKILL.md` est alors chargé ; il a été écrit pour fonctionner seul, les fichiers `references/` et `templates/` apportant la profondeur quand ils sont présents.

## Utilisation

Claude active le skill de lui-même quand la demande parle d'UX, d'écran, de maquette, de parcours ou de test utilisateur. Vous pouvez aussi l'appeler explicitement :

```
/ux-master audit src/screens/ExplorerScreen.tsx
/ux-master concevoir l'onboarding recruteur, mobile, 3 écrans maximum
/ux-master tester : prépare le guide d'entretien pour des commerçants
/ux-master que penses-tu de cette capture ?   (avec une image jointe)
```

Exemples de demandes en langage naturel :

- « Audite cet écran avant que je le donne à Claude Code. »
- « Ce parcours d'inscription est-il clair ? Donne-moi les trois corrections les plus rentables. »
- « Conçois l'écran de liste et de détail pour la version PC, posture souveraine. »
- « Passe la checklist pré-vol sur cette spec. »
- « Prépare un test d'utilisabilité à cinq participants sur la maquette. »

Le skill répond dans la langue de la demande (français par défaut), termine chaque livrable par une seule prochaine étape, et marque **[Hypothèse]** tout ce qui n'a pas été vérifié auprès de vrais utilisateurs.

## Structure du dépôt

```
ux-master/
├── SKILL.md                         Orchestrateur : modes, niveaux, lentilles, scoring, checklist pré-vol
├── README.md
├── LICENSE
├── references/
│   ├── lentilles.md                 Les six lentilles en détail : signes d'alerte, corrections, pièges, recoupements
│   ├── socle.md                     Lois cognitives chiffrées, critères WCAG, règles iOS / Android / web
│   ├── audit-code.md                Motifs à rechercher en React Native/Expo et Next.js, commandes rg
│   ├── scoring.md                   Sévérité, score, priorisation : exemples calibrés et pièges
│   └── recherche-et-tests.md        Entretiens, synthèse, personas, test d'utilisabilité, SUS, métriques
├── templates/
│   ├── rapport-audit.md
│   ├── spec-ecran.md
│   ├── ticket-claude-code.md
│   ├── guide-entretien.md
│   └── protocole-test.md
└── examples/
    └── audit-express-connexion.md   Un audit Express complet, du constat au ticket
```

`SKILL.md` reste sous 500 lignes et charge les références à la demande, selon les recommandations de Claude Code sur les skills.

## Principes de conception du skill

- **Une seule méthode**, pas six : les lentilles se recoupent, le skill classe chaque constat une seule fois dans douze catégories stables.
- **Des chiffres reproductibles** : la sévérité suit des critères écrits et des exemples étalonnés ; le score compare deux versions d'un même écran.
- **Du constat à l'action** : chaque problème de sévérité ≥ 2 devient un ticket Claude Code avec fichier, comportement attendu, critères d'acceptation et test sur appareil. Un ticket, une session.
- **L'honnêteté avant l'élégance** : aucune donnée utilisateur inventée ; un audit heuristique ne remplace pas un test ; la recherche (mode C) est ce qui rend l'UX réellement bonne.

## Sources et crédits

Le skill est une **synthèse opérationnelle reformulée** ; il ne reproduit pas les textes originaux. Pour la pensée complète de chaque auteur :

- Don Norman, *The Design of Everyday Things* (édition révisée, 2013).
- Jakob Nielsen, *10 Usability Heuristics for User Interface Design* et articles de Nielsen Norman Group (nngroup.com).
- Steve Krug, *Don't Make Me Think, Revisited* (2014) et *Rocket Surgery Made Easy* (2010).
- Alan Cooper, Robert Reimann, David Cronin, Christopher Noessel, *About Face: The Essentials of Interaction Design* (4e édition, 2014).
- Dieter Rams, les dix principes du bon design (Vitsœ).
- John Brooke, *SUS: A Quick and Dirty Usability Scale* (1986), libre d'utilisation avec mention de la source.
- Web Content Accessibility Guidelines (WCAG) 2.1, W3C.
- Apple Human Interface Guidelines ; Google Material Design 3.

## Contribuer

Les propositions bienvenues : un signe d'alerte manquant dans une lentille, un motif de code à ajouter pour une autre stack (Flutter, SwiftUI, Vue), un exemple d'audit calibré. Ouvrez une issue ou une pull request ; gardez `SKILL.md` sous 500 lignes et placez la matière détaillée dans `references/`.

## Licence

MIT, voir `LICENSE`.

## Versions

- **1.0.0** — Première version publique : trois modes, trois niveaux, six lentilles, douze catégories, scoring calibré, audit de code React Native et Next.js, gabarits et exemple complet.
