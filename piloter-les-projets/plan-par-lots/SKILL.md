---
name: plan-par-lots
description: "Rédige un plan de travail en phases et en lots, dans un vrai fichier Markdown, toujours avec la même structure : en-tête et état, sommaire cliquable, le problème et le but, décisions prises, ce qu'on a trouvé, comment les morceaux s'emboîtent, phases (objectif, résultat de phase) découpées en lots (objectif, pourquoi, à faire, dépend de, résultat attendu), actions de l'utilisateur, points à confirmer, décidé automatiquement, zone technique. Le plan est adapté au projet réel et à la demande : rien d'inventé, chaque constat vérifié. Il sert ensuite de source de vérité : état, décisions et « Fait » mis à jour à la fin de chaque lot. On l'exécute phase par phase, dans l'ordre strict des lots et sous-lots : analyse et déblocages avant la phase, tests unitaires à chaque lot, tests globaux pour clôturer la phase. Dès qu'une phase est clôturée, le plan se sépare en deux chapitres : phases non clôturées, puis phases clôturées. À utiliser dès qu'un travail demande plus d'un lot, ou sur « fais-moi un plan », « plan par phases », « plan par lots », « découpe ce chantier », « qu'est-ce qui m'attend », « feuille de route », « planifie cette fonctionnalité », « mets à jour le plan »."
---

# Plan par lots — savoir ce qui m'attend, lot par lot

> Un plan est un **fichier Markdown** rangé dans le projet. Il a toujours la même
> forme. Seul le contenu change, parce que le projet et la demande changent.

Le lecteur doit comprendre, sans lire le code : **où on va, par où on passe, ce qu'il
doit décider, ce qu'il doit faire lui-même, et comment il saura qu'un lot est fini.**

Le style d'écriture est celui de la skill `explainer` : français simple,
phrases courtes, un terme dur défini à sa première apparition, rien d'inventé.

> **La règle d'exécution, à ne jamais oublier** : on avance **phase par phase**, et
> dans une phase **lot par lot, sous-lot par sous-lot, dans l'ordre**. On ne laisse
> pas A pour commencer par E. Une phase s'ouvre par une analyse et la liste de ce
> que l'utilisateur doit débloquer ; elle se ferme par des tests globaux. Détail en
> section 8.

## 1. Quand l'utiliser

| Situation | Que faire |
|---|---|
| Le travail tient en un seul changement | Pas de plan. Faire, et le dire. |
| Le travail demande 2 lots ou plus | **Écrire le plan avec cette skill.** |
| Un plan existe déjà pour ce chantier | Ne pas en créer un second : le **mettre à jour** (section 7). |
| La demande est floue | Faire d'abord l'enquête (section 2), puis poser les décisions dans le plan. |

## 2. Avant d'écrire : l'enquête

On n'écrit pas un plan de mémoire. Dans cet ordre :

1. **Lire les règles du projet** : `CLAUDE.md`, `AGENTS.md`, la charte d'interface
   s'il y en a une. Elles s'imposent à chaque lot.
2. **Regarder l'existant** : le code touché, ce qui existe déjà et qu'on peut
   réutiliser, la machine ou l'hébergement si le chantier y touche.
3. **Noter les constats** avec leur preuve (un fichier, une commande, une mesure) et
   la date. Ce qui n'est pas vérifié s'écrit « à confirmer ».
4. **Repérer les décisions** : ce qui change le produit, les données, la sécurité, le
   design important ou les priorités appartient à l'utilisateur. Le reste : décider
   seul, et l'écrire dans « Décidé automatiquement ».
5. **Repérer ce que Claude ne fera pas** : mots de passe, clés, réglages système,
   comptes d'autres applications, commit, push, déploiement.

Pendant l'enquête, lire **peu et juste** : le document de la tâche, puis le code. Ne
jamais ouvrir un dossier de documentation en entier.

## 3. Où va le fichier

| Cas | Emplacement |
|---|---|
| Le projet dit où ranger ses plans | Suivre le projet. |
| Le projet a un dossier `doc/plans/` ou `docs/plans/` | Dedans. |
| Rien n'est prévu | `doc/plans/` à créer, et le dire en une ligne. |
| Pas de projet (réflexion hors code) | Le dossier que l'utilisateur indique. |

- **Nom** : `AAAA-MM-JJ-sujet-court.md`, date du jour où le plan est écrit.
- **Langue** : français, sauf si le projet impose une autre langue pour ses documents.
- Si le projet a un index de documentation, y **ajouter la ligne** du plan.

## 4. La structure, toujours la même

Le gabarit complet, prêt à remplir, est dans
[`references/gabarit-plan.md`](references/gabarit-plan.md). Le copier, puis remplir.

| # | Section | Ce qu'elle dit | Obligatoire |
|---|---|---|---|
| 1 | **Titre + citation** | Le chantier en une phrase, puis 2 ou 3 lignes : quoi, pour qui, où | oui |
| 2 | **Fiche** | Date et version, auteur, branche de travail, **État** daté | oui |
| 3 | **Sommaire** | Lien vers chaque section, chaque phase et chaque lot | oui |
| 4 | **Le problème et le but** | « Aujourd'hui » / « Le but », puis le tableau besoin → où ce sera | oui |
| 5 | **Décisions prises** | Tableau numéroté : sujet, choix, conséquence dans le plan | oui (vide au départ si rien n'est tranché) |
| 6 | **Ce qu'on a trouvé** | Les constats vérifiés, datés, rangés par sujet | oui |
| 7 | **Comment les morceaux s'emboîtent** | Un schéma en texte, puis 3 à 5 lignes de règles | si plusieurs morceaux se parlent |
| 8 | **Phases et lots** | Le cœur du plan (section 5). Dès qu'une phase est clôturée : deux chapitres, **Phases non clôturées** puis **Phases clôturées** | oui |
| 9 | **Actions de l'utilisateur** | Tableau « quand → action » : ce que Claude ne fait pas | oui |
| 10 | **Points à confirmer** | Tableau « point, quand, pourquoi » | oui |
| 11 | **Décidé automatiquement** | Tableau « sujet, choix, pourquoi » | oui |
| 12 | **Zone technique concernée** | Fichiers, routes, tables, scripts, rangés par sujet | oui |

Règles de forme :

- Chaque section, phase et lot porte une **ancre** : `<a id="phase-1"></a>`,
  `<a id="lot-1-2"></a>`. Le sommaire pointe dessus.
- Un trait `---` sépare les grandes sections.
- Les chemins de fichiers vont dans « Zone technique concernée » et dans les « À
  faire » des lots. Jamais dans « Le problème et le but ».
- Un tableau plutôt qu'une liste dès qu'on compare.

## 5. Phases et lots

### Une phase

Une phase = **un résultat que l'utilisateur peut constater**. Elle commence par :

```md
<a id="phase-1"></a>
## Phase 1 — [nom court]

**Objectif** : [ce que la phase apporte, en une phrase].
**Pourquoi** : [seulement si ce n'est pas évident].
**Résultat de phase** : [ce qu'on voit quand elle est finie].
```

- Numérotation : `0, 1, 2…`. La phase 0 sert au socle (installation, accès, sauvegarde).
- Une phase ajoutée plus tard **ne renumérote rien** : `4 bis`, `4C`, `4D`. Aucune
  référence existante ne doit casser.
- Un constat propre à la phase se met sous son en-tête : `**Constat (date)** : …`.
- Chaque phase finit par un bloc **« Clôture de la phase N »** : les tests globaux
  (toute la suite de tests, le build, et le parcours réel si la phase touche le réel).
  Elle n'est clôturée que si ce bloc est vert.

### Un lot

Un lot = **une chose que l'utilisateur peut voir et vérifier**. Ni plus, ni moins.

```md
<a id="lot-1-2"></a>
### Lot 1.2 — [nom court]

- **Objectif** : [une phrase].
- **Pourquoi** : [le constat qui rend ce lot nécessaire — seulement s'il n'est pas évident].
- **À faire**
  - [geste concret, vérifiable]
  - [geste concret, vérifiable]
- **Dépend de** : [lots, ou « rien »].
- **Tests du lot** : [les tests unitaires qui prouvent le lot].
- **Résultat attendu** : [ce qu'on observe quand c'est fini].
```

Lignes en plus, seulement quand elles servent :

| Ligne | Quand |
|---|---|
| **Décision nécessaire** | Le lot ne peut pas avancer sans un choix : contexte, options, conséquence de chaque option, sur place |
| **Toi** : … | Un geste du lot appartient à l'utilisateur (dans « À faire », en gras) |
| **À confirmer** : … | Un point du lot n'est pas vérifié |
| **Fait (date)** : … | Ajoutée quand le lot est fini (section 7) |

Règles :

- Un lot tient en **5 à 12 lignes**. Plus long : le couper en deux.
- « À faire » contient des gestes, pas des intentions. « Rendre plus robuste » n'est pas un geste.
- « Résultat attendu » est **observable** : une page qui s'ouvre, une commande qui
  répond, un test vert. Pas « le code est propre ».
- Un lot qui touche l'interface rappelle la charte du projet dans son « À faire » :
  composition propre, jetons de design, vérification ordinateur et téléphone.
- Un lot qui touche des données commence par la sauvegarde.
- 3 à 8 lots par phase. Au-delà, c'est deux phases.
- Un lot trop gros pour un seul geste se découpe en **sous-lots** : `Lot 4.2a`,
  `4.2b`… (ancre `lot-4-2a`). Ils s'exécutent eux aussi dans l'ordre.

### Les deux chapitres

Tant qu'aucune phase n'est clôturée, les phases se suivent sous un seul titre. Dès
que **une phase ou plus est clôturée**, la section se coupe en deux chapitres :

```md
<a id="phases-ouvertes"></a>
## Phases non clôturées

[la phase en cours, puis les phases à venir, dans l'ordre]

---

<a id="phases-cloturees"></a>
## Phases clôturées

[les phases finies, dans l'ordre, chacune avec sa ligne « Clôturée (date) »]
```

- Les phases non clôturées viennent **en premier** : c'est ce que l'utilisateur lit.
- On **déplace** le bloc de la phase, avec ses lots, sans le réécrire ni le
  renuméroter. Les ancres ne changent pas : aucun lien ne casse.
- Le sommaire suit : les deux chapitres, et les phases sous chacun.

## 6. Les décisions

- **Avant d'écrire le plan**, ce qui bloque tout se demande d'abord, avec la fiche de
  décision habituelle (pourquoi, référence, options et conséquences, avis technique).
  Six décisions au plus.
- **Dans le plan**, une décision tranchée va dans « Décisions prises », avec sa date
  et sa conséquence (« Lot 2.3 »).
- Une décision qui change **ne s'efface pas** : l'ancienne ligne est ~~barrée~~, avec
  la date et la raison, et une nouvelle ligne est ajoutée.
- Une proposition n'est jamais écrite comme une décision. Tant que l'utilisateur n'a
  pas tranché, c'est un bloc « Décision nécessaire » dans le lot.

## 7. Le plan vit : la mise à jour

Le plan est la **source de vérité** du chantier. À la fin de chaque lot, dans le même
changement que le code :

1. Ajouter au lot une ligne **`Fait (AAAA-MM-JJ)`** : ce qui a été réellement fait, ce
   qui diffère de ce qui était prévu, la preuve (test, page vue, commande).
2. Mettre à jour la ligne **État** de la fiche, en tête.
3. Ranger les nouvelles décisions, les choix automatiques et les points à confirmer
   dans leurs tableaux.
4. Compléter « Zone technique concernée » et « Actions de l'utilisateur » (marquer
   **fait** ce qui l'est).

À la clôture d'une phase, en plus :

5. Ajouter sous l'en-tête de la phase **`Clôturée (AAAA-MM-JJ)`** : les tests
   globaux lancés et leur résultat.
6. Déplacer la phase dans le chapitre **Phases clôturées** (section 5), et mettre le
   sommaire à jour.

Ne jamais réécrire l'histoire : un lot abandonné reste, marqué « abandonné (date,
raison) ». Un lot ajouté prend le numéro suivant de sa phase.

## 8. Exécuter le plan : phase par phase, dans l'ordre

Le plan s'exécute toujours de la même façon. Pas de saut, pas de désordre.

| Étape | Ce qu'on fait | Ce qu'on montre à l'utilisateur |
|---|---|---|
| **1. Analyser la phase** | Relire la phase dans le plan, puis le code qu'elle touche. Vérifier que les lots sont dans le bon ordre et toujours justes. | Le plan de la phase : les lots dans l'ordre, ce que chacun va faire |
| **2. Demander les déblocages** | Lister ce que l'utilisateur doit faire pour que la phase puisse aller au bout : décision, accès, clé, réglage, compte, donnée. | « Ce dont j'ai besoin de toi pour cette phase ». Attendre avant de commencer |
| **3. Faire les lots dans l'ordre** | Lot 1, puis 2, puis 3. Sous-lots a, b, c dans l'ordre. Chaque lot finit par **ses tests unitaires**, verts, et sa ligne « Fait ». | Un point court à la fin de chaque lot |
| **4. Clôturer la phase** | Lancer les **tests globaux** : toute la suite, le build, le parcours réel. Corriger jusqu'au vert. | Les tests lancés et leur résultat |
| **5. Ranger** | « Clôturée (date) », phase déplacée dans le chapitre des phases clôturées. | L'état mis à jour |

Règles :

- **Ordre strict.** On ne commence pas le lot E tant que A, B, C et D ne sont pas
  faits. Si un lot ne peut pas avancer, on s'arrête et on le dit : on ne passe pas
  au suivant en douce.
- **Une seule phase ouverte à la fois.** La phase suivante ne s'ouvre qu'après la
  clôture de la précédente.
- **Une phase commencée se termine.** On va au bout de tous ses lots et sous-lots
  avant de faire autre chose.
- Un test qui échoue n'est jamais contourné : le lot n'est pas fait tant qu'il est
  rouge.
- Si l'analyse montre que l'ordre prévu est faux (un lot dépend d'un lot plus loin),
  on le dit, on corrige le plan (« Décidé automatiquement » ou décision à prendre),
  **puis** on avance.

## 9. Ce qu'on met dans la réponse

Le plan est dans le fichier. La réponse, elle, reste courte :

```md
## Ce qu'on va faire
[2 ou 3 lignes]

## Les phases
| Phase | Ce qu'elle apporte | Lots |

## Décisions à prendre
[les fiches de décision, s'il y en a]

## Ce que tu devras faire toi-même
[3 à 5 lignes]

## Zone technique concernée
- le fichier du plan
```

On n'y recopie pas le plan. On ne commence **aucun lot** avant que l'utilisateur ait
lu le plan et tranché les décisions qui bloquent.

À l'ouverture d'une phase (section 8, étapes 1 et 2), la réponse prend cette forme :

```md
## Phase N — ce qu'on va faire
| Ordre | Lot | Ce qu'il fait | Tests |

## Ce dont j'ai besoin de toi pour cette phase
- [déblocage 1 : décision, accès, clé, réglage…]

## Comment on saura que la phase est clôturée
[les tests globaux qu'on lancera]
```

## 10. Contrôle avant de rendre le plan

| Contrôle | |
|---|---|
| Les 12 sections sont là, dans l'ordre | ☐ |
| Chaque lien du sommaire tombe sur une ancre qui existe | ☐ |
| Chaque lot a Objectif, À faire, Dépend de, Résultat attendu | ☐ |
| Chaque « Résultat attendu » est observable | ☐ |
| Chaque constat a une preuve ; le reste est « à confirmer » | ☐ |
| Aucune proposition écrite comme une décision | ☐ |
| Aucun secret, aucune valeur de `.env` dans le plan | ☐ |
| Tout fichier, route ou script cité existe (vérifié) | ☐ |
| Les gestes réservés à l'utilisateur sont dans « Actions de l'utilisateur » | ☐ |
| Chaque lot a ses tests ; chaque phase a son bloc « Clôture » | ☐ |
| Si une phase est clôturée : deux chapitres, non clôturées d'abord | ☐ |

## 11. Ce qu'on ne fait pas

| À ne pas faire | Pourquoi |
|---|---|
| Écrire le plan seulement dans la réponse | Il se perd à la fin de la session ; personne ne peut le mettre à jour |
| Changer l'ordre ou le nom des sections | L'utilisateur retrouve chaque plan au même endroit |
| Un lot « divers » ou « finitions » | On ne peut ni le vérifier ni le finir |
| Renuméroter après un ajout | Les références aux lots cassent partout |
| Inventer un constat, un chiffre, un nom de fichier | Un plan faux coûte plus cher que pas de plan |
| Commencer à coder dans la même réponse | Le plan se lit et se valide d'abord |
| Un second plan pour le même chantier | Deux sources de vérité se contredisent |
| Sauter un lot, ou commencer par la fin (laisser A pour faire E) | Le travail n'a plus de logique ; les lots suivants reposent sur du vide |
| Ouvrir une phase sans analyse ni liste de déblocages | On bloque en plein milieu, faute d'un accès ou d'une décision |
| Ouvrir la phase suivante sans tests globaux verts | Une phase « presque finie » n'est pas finie |
| Mélanger phases clôturées et non clôturées | L'utilisateur ne voit plus ce qui reste |
