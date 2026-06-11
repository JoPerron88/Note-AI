# Conventions Note AI — la référence

> Distillé de `CONCEPT.md §12` du projet Note AI, standard fr-CA arrêté le
> 2026-06-10. C'est le contrat entre l'humain et l'adjoint : les deux naviguent
> le coffre avec les mêmes règles.

## 1. Structure du coffre

```
<Coffre>/                          ← n'importe quel coffre Obsidian
├─ CLAUDE.md                       ← l'adjoint par défaut (généré à l'init)
├─ Cahier-maître.md                ← vue d'ensemble de TOUS les projets (§11)
├─ Cahier-maître.base              ← les vues base de données natives (§11)
├─ _boîte/                         ← boîte de réception : dépôt brut, trié sur demande
├─ Gens/                           ← le répertoire : une fiche par personne (§9)
│  ├─ _moi.md                      ← le PROPRIÉTAIRE du coffre (l'humain de l'adjoint)
│  └─ Marie Tremblay.md            ← une fiche = une personne
├─ Projets/
│  ├─ <Notebook>/                  ← un NOTEBOOK par projet (ex. Maison)
│  │  ├─ _projet.md                ← cahier de projet : objectif, statut, échéances
│  │  ├─ <Section>/                ← une SECTION par thème (ex. Cuisine, Échéancier)
│  │  │  ├─ AAAA-MM-JJ-slug.md     ← les PAGES
│  │  │  └─ captures/              ← images & pièces jointes de la section
├─ .note-ai/                       ← LA COUCHE MACHINE (§4) — invisible dans Obsidian
│  ├─ carte.md                     ← la carte du coffre (généré)
│  ├─ memoire.md                   ← la mémoire de l'adjoint
│  ├─ journal.md                   ← trace des actions
│  └─ index/                       ← les index condensés (généré)
│     ├─ <Notebook>.md             ← un par notebook
│     └─ gens.md                   ← l'infrastructure humaine
├─ .gemini/                        ← compat GEMINI CLI (§13) — le coffre est bi-moteur
│  ├─ settings.json                ← fait lire CLAUDE.md à Gemini (context.fileName)
│  └─ skills/note-ai/              ← copie du skill : voyage avec le coffre
└─ .obsidian/                      ← config Obsidian — NE PAS TOUCHER, sauf…
   └─ types.json                   ← …le typage des propriétés, fusionné à l'init (§3)
```

- **Notebook** = dossier direct sous `Projets/`. **Section** = sous-dossier.
  **Page** = fichier `.md`. Sections imbriquées permises mais 1 niveau suffit
  en général.
- Les fichiers et dossiers `_*` (underscore) sont l'outillage visible ;
  `.note-ai/` est l'outillage **invisible** (Obsidian masque les dossiers
  commençant par un point : exclus de l'explorateur, de la recherche et des
  liens).

## 2. Nommage — standard hybride

- **Dossiers** (Notebooks, Sections) : noms humains, **accents et majuscules
  permis** (`Maison`, `Échéancier`). Pas d'espaces de préférence (tiret si
  besoin).
- **Pages et images** : **slugs sans accent**, minuscules, tirets —
  pages `AAAA-MM-JJ-slug.md` (`2026-06-10-plan-cuisine.md`), images en slug
  parlant (`plan-v2.png`, jamais `IMG_4521.png`). Le vrai titre accentué vit
  dans le frontmatter (`titre:`). Bonus : le préfixe daté rend les noms
  uniques — aucune collision de wikilinks (§8).
- **Fiches de personnes** (`Gens/`) : exception assumée au slug — nom humain
  complet, espaces et accents permis (`Marie Tremblay.md`, `Paul Côté.md`),
  pour que `[[Marie Tremblay]]` soit la mention naturelle dans les notes.
- Exceptions figées : `Cahier-maître.md`, `_boîte/`, `Gens/`, `_moi.md`,
  `_projet.md`, `.note-ai/` — toujours ces graphies exactes.
- ⚠️ Piège multi-machines : les noms accentués s'encodent différemment entre
  macOS et Windows (NFD/NFC). Si le coffre passe par git, recommander
  `git config core.precomposeunicode true` sur Mac. Les pages (slugs ASCII)
  sont immunisées par construction.

## 3. Frontmatter de page (obligatoire) — clés en français accentué

```yaml
---
titre: Plan cuisine révisé
projet: Maison/Cuisine          # Notebook/Section
date: 2026-06-10                # ISO, toujours
statut: en-cours                # à-faire | en-cours | en-pause | terminé
tags: [cuisine, structure]
résumé: Calcul de la poutre porteuse + relevé des dimensions.
échéance: 2026-06-20            # ISO ; optionnelle
---
```

- **Graphies canoniques, une seule façon d'écrire** : clés `titre`, `projet`,
  `date`, `statut`, `tags`, `résumé`, `échéance` (avec leurs accents, jamais
  `resume` ni `echeance`) ; valeurs de statut `à-faire`, `en-cours`,
  `en-pause`, `terminé` — exactement ces chaînes, pour que grep et Dataview
  restent fiables.
- Le `résumé:` (une ligne) est la matière première de l'index — le soigner.
- Les clés natives d'Obsidian (`tags`, `aliases`) restent telles quelles.

**Propriétés typées (`.obsidian/types.json`).** Le frontmatter EST le système de
**propriétés** d'Obsidian. À l'init, l'adjoint **fusionne** des types dans
`.obsidian/types.json` (gabarit : `templates/obsidian-types.json`) :

| Propriété | Type Obsidian | Effet |
|---|---|---|
| `date`, `échéance` | `date` | sélecteur de date pour l'humain ; tri fiable dans les vues |
| `tags`, `aliases` | `tags` / `aliases` | listes natives |
| `statut`, `titre`, `projet`, `résumé`, `relation`, `organisation`, `rôle`, `coffre` | `text` | (Obsidian n'a pas de type « choix » — les 4 valeurs de `statut` restent garanties par la convention, pas par Obsidian) |

C'est la **seule** entorse à « ne jamais toucher `.obsidian/` » : fusionner nos
clés (créer le fichier si absent ; sinon ajouter les nôtres **sans écraser**
celles de l'utilisateur). Bénéfice : renforce le **double accès** — l'humain
édite `statut`/`échéance` via une belle UI, l'adjoint édite le même YAML comme
du texte.

## 4. `.note-ai/` — la couche machine (le territoire de l'adjoint)

Dossier **invisible pour l'humain** (Obsidian masque les dossiers pointés).
C'est l'espace de travail de l'adjoint : il y écrit **à sa façon** — l'humain
n'y met jamais les pieds, l'adjoint n'y range jamais de contenu humain (rien
dans `.note-ai/` ne peut être wikilinké).

- **`index/<Notebook>.md`** (généré) — un index condensé par notebook, une
  ligne par page :

  ```markdown
  # Index — Notebook Maison   (généré, source de vérité = les frontmatters)
  - Cuisine/2026-06-10-plan-cuisine.md — calcul poutre porteuse [cuisine,structure] (en-cours) ⏰2026-06-20
  - Cuisine/captures/plan-v2.png — IMAGE : plan révisé de la poutre
  ```

  **Lire l'index d'abord, toujours** ; régénérer à chaque écriture dans le
  notebook ; en cas de doute, reconstruire depuis les frontmatters.
- **`index/gens.md`** (généré) — l'infrastructure humaine (§9) : le
  propriétaire en tête, puis les fiches regroupées intelligemment.
- **`carte.md`** (généré) — la carte du coffre en ~30 lignes : arborescence
  condensée, compteurs (notebooks/sections/pages/fiches), pages-carrefours
  (les plus liées), dernier rangement. **Premier fichier lu par toute
  session.**
- **`memoire.md`** — la mémoire de travail de l'adjoint : préférences du
  propriétaire (« vas-y sans demander pour la boîte »), habitudes de
  classement constatées, raccourcis. Relue à chaque session, mise à jour
  quand l'adjoint apprend quelque chose de durable.
- **`journal.md`** — trace des actions (une ligne : date ISO · action ·
  fichiers touchés), les plus récentes en premier. Répond à « qu'est-ce que
  tu as fait hier ? » et au débogage d'un mauvais classement. Tronquer au-delà
  de ~200 lignes (garder les récentes).
- **Format libre** : au besoin, l'adjoint peut créer d'autres fichiers dans
  `.note-ai/` à sa convenance (notation compacte, listes de travail) — du
  texte seulement, et seulement si ça l'aide vraiment. Les nommer clairement.

## 5. Grille d'effort — calibrer modèle et moyens sur la requête

Toutes les requêtes ne se valent pas. Avant d'agir, jauger :

| Niveau | Déclencheurs typiques | Moyens |
|---|---|---|
| **Léger** (défaut) | Ranger 1 élément, créer 1 note, question simple | Lire `carte.md` + l'index concerné seulement ; proposition en 1 ligne |
| **Moyen** | Boîte pleine, résumé de projet, recherche transversale | Indexes + fichiers ciblés ; plan bref avant d'agir |
| **Lourd** | Synthèse multi-notebooks, réorganisation, reconstruction des index | **Annoncer l'ampleur d'abord** ; le mécanique de masse part en **sous-agent sur modèle économique** si le harnais en offre, sinon **par lots** ; le jugement reste au modèle principal |

- En cas de doute : niveau du dessous, puis escalader si ça ne suffit pas.
- **Sous-agents** : seulement au niveau lourd, seulement pour du **mécanique**
  (régénérer tous les index, corriger des liens en masse, inventorier) —
  brief court, résultat vérifié au retour. **Jamais de jugement en sous-agent**
  (classement, réécriture, fiches de personnes). Disponibilité selon le
  moteur : Claude Code = outil Agent + modèle économique (Haiku) ;
  Gemini CLI = pas de sous-agents → traiter par lots en annonçant la
  progression.
- Le choix du modèle de la session principale appartient à l'utilisateur —
  l'adjoint ne le change pas, il adapte ses moyens.

## 6. Protocole `_boîte/` (la boîte de réception)

1. L'utilisateur dépose n'importe quoi (texte, PDF, image) — aucune règle.
2. Sur « range ça / range la boîte / range l'inbox » : pour chaque élément,
   **proposer** destination + nouveau nom + (si texte) la réécriture,
   **attendre le OK**, puis exécuter : déplacer, créer/mettre à jour la page,
   lier, régénérer l'index. La boîte finit vide.
3. Élément inclassable → demander (une fois) ou créer la page dans le notebook
   le plus plausible avec `statut: à-faire` et tag `à-classer`.

## 7. Images et pièces jointes — pas d'OCR

- On **range**, on ne lit pas : jamais d'OCR, jamais de description du contenu.
- Chaque image rangée reçoit une **légende d'une ligne** (fournie par
  l'utilisateur ou déduite du contexte de la demande), stockée :
  dans la page qui l'embarque (`![[captures/plan-v2.png]]` + légende en
  dessous) ET dans l'index du notebook (préfixe `IMAGE :`).
- Une image sans légende est introuvable — ne jamais ranger sans légende.

## 8. Liens — comment Obsidian les fait, comment l'adjoint les voit

- **Résolution par nom de fichier, sur tout le coffre** : `[[plan-cuisine]]`
  trouve la page où qu'elle soit — Obsidian ne regarde le chemin qu'en cas
  d'ambiguïté. Deux pages du même nom = collision ; notre préfixe daté
  l'élimine pour les pages, les fiches `Gens/` portent des noms de personnes
  (uniques par nature). En cas de doute, lier avec le chemin.
- **Formes utiles** : `[[page|texte affiché]]` (alias d'affichage),
  `[[page#Section]]` (lien vers un titre), `![[page]]` / `![[image.png]]`
  (incrustation).
- **`aliases:` du frontmatter** : une page liste ses surnoms —
  `aliases: [Marie, la cheffe]` sur la fiche `Marie Tremblay.md` fait que
  `[[Marie]]` propose la bonne fiche. À poser sur les fiches de personnes
  (prénom seul) et les pages au titre long.
- **Les backlinks n'existent pas sur disque** : Obsidian les calcule dans
  l'app. L'adjoint les voit en **grepant `[[Nom`** sur le coffre — c'est SA
  technique pour « où est-ce qu'on parle de X ». Les pages-carrefours (très
  liées) sont notées dans `carte.md`.
- **Tout déplacement/renommage** → grep l'ancien nom, corriger les liens qui
  pointaient dessus (Obsidian ne le fait que si le renommage passe par lui).
- **Tâches et échéances** : format `- [ ] Faire X 📅 AAAA-MM-JJ` (date ISO —
  ce que les outils savent trier). L'adjoint sait les lister par projet,
  trier par échéance, signaler les retards (grep `- [ ]`, comparer à la date
  du jour).

## 9. Le répertoire des gens (`Gens/`)

Une fiche Markdown par personne — **pas de base de données** : les
`[[wikilinks]]` font le réseau. Chaque mention `[[Marie Tremblay]]` dans une
note pointe vers la fiche, et les backlinks d'Obsidian listent automatiquement
toutes les notes où la personne apparaît.

- **Frontmatter de fiche** (clés canoniques, accents compris) :

  ```yaml
  ---
  titre: Marie Tremblay
  aliases: [Marie]                   # surnoms → [[Marie]] résout vers la fiche
  relation: collègue                 # voir « adaptation » ci-dessous
  organisation: Constructions ABC    # optionnelle
  rôle: ingénieure de structure      # optionnel
  date: 2026-06-10                   # création de la fiche
  tags: [gens]
  résumé: Responsable des plans du chantier Nord.
  ---
  ```

- **`_moi.md` — le propriétaire** : fiche spéciale créée à l'initialisation du
  coffre par une **mini-entrevue** (nom · coffre travail/personnel/mixte ·
  rôle/contexte). C'est **l'humain de l'adjoint** : toute session la lit pour
  savoir à qui elle parle et comment classer.
- **`.note-ai/index/gens.md`** (généré) : l'infrastructure humaine condensée,
  le propriétaire en tête, puis les fiches **regroupées intelligemment** —
  coffre travail : par organisation/équipe ; coffre personnel : par cercle
  (famille, amis, contacts). Une ligne par personne :
  `- <fichier> — <rôle, organisation> [<relation>]`.
- **Détection au rangement** : une note mentionne une personne nouvelle et
  significative → l'adjoint **propose** la fiche (+ le `[[lien]]` dans la
  note) dans son plan propose-puis-applique. Nouvelle information sur
  quelqu'un de connu (changement de rôle, d'équipe…) → proposer la mise à
  jour de sa fiche. Toute fiche créée/modifiée → régénérer l'index des gens.
- **Adaptation** : le vocabulaire de `relation:` suit le contexte du coffre
  (lu dans `_moi.md`) — travail : collègue, patron, client, fournisseur,
  partenaire ; personnel : famille, ami, voisin, professionnel. Pas de liste
  fermée — rester cohérent avec les fiches existantes.
- **Discrétion** : le répertoire est local et **factuel** — il consigne ce que
  les notes et l'utilisateur disent, jamais de déductions ni de profils
  inventés. Pas de fiche pour un nom sans importance (auteur cité, personnage,
  commerce).

## 10. Rédaction fr-CA (quand l'adjoint écrit ou réécrit)

- **Typographie OQLF** : « guillemets français avec espaces insécables » ·
  espace insécable avant le deux-points · **aucune espace avant `; ! ?`**
  (différence avec la France) · nombres `1 234,56` · monnaie `10,50 $` ·
  heures `14 h 30`.
- **Vocabulaire québécois** : courriel, téléverser, gabarit, fin de semaine,
  clavardage… — dans les réécritures et les réponses de l'adjoint. **Ne jamais
  corriger les mots de l'utilisateur** quand on cite ou qu'on range sans
  réécrire.
- **Dates en toutes lettres dans la prose** : « 8 septembre 2025 » (pas de
  zéro initial, mois en minuscules). Les dates **machine** restent ISO :
  noms de fichiers, `date:`/`échéance:` du frontmatter, `📅` des tâches.
- **Orthographe traditionnelle** (non rectifiée).

## 11. `Cahier-maître.md` + `Cahier-maître.base` — le tableau de bord

Trois couches, du plancher au confort — **ne supprimer aucune** :

1. **Table statique** dans `Cahier-maître.md` (le plancher autosuffisant) :
   projets — nom, statut, prochaine échéance, tâches ouvertes — + « Activité
   récente » (5 dernières actions). L'adjoint la maintient à la main à chaque
   changement de statut/échéance. Marche partout, sans aucun plugin ni version
   récente.
2. **Vues Bases natives** dans `Cahier-maître.base`, embarquées dans le `.md`
   via `![[Cahier-maître.base#Projets]]` et `![[…#Échéances à venir]]`. Bases
   fait partie du **cœur d'Obsidian** (pas un plugin communautaire) → cohérent
   avec l'autosuffisance, contrairement à Dataview qu'on n'utilise plus ici.
   Les vues lisent les **propriétés** (`statut`, `échéance`, `file.name`).
   ⚠️ Le `.base` livré est un **gabarit de départ** : si une vue s'affiche mal,
   l'ouvrir dans l'éditeur de Bases d'Obsidian, qui réécrit la syntaxe exacte
   de la version installée. Propriété accentuée → forme `note["échéance"]`.
3. **Tasks (plugin optionnel)** : seul à centraliser les cases `- [ ]` (Bases
   travaille sur les propriétés, pas sur les tâches en ligne). Sans Tasks,
   l'adjoint tient la section « Tâches en retard » à la main.

## 12. `_projet.md` — le cahier de projet

Objectif du projet, statut global, jalons/échéances, décisions notables.
Mis à jour quand le projet évolue ; lu (avec l'index du notebook) pour
répondre à « où en suis-je ». Template : `templates/projet.md`.

## 13. Multi-moteurs — Claude Code ET Gemini CLI, à égalité

Le même coffre fonctionne sous les deux moteurs. Trois principes :

- **Une seule source de vérité** : `CLAUDE.md` est LE fichier d'adjoint,
  rédigé **neutre-moteur** (jamais d'instruction qui n'a de sens que pour un
  moteur ; les différences se conditionnent : « si ton harnais offre X… »).
  Gemini le lit grâce à `<coffre>/.gemini/settings.json`
  (`{"context": {"fileName": ["CLAUDE.md", "GEMINI.md"]}}` — anciennes
  versions : clé plate `contextFileName`). **Fusionner** ce réglage à l'init,
  même règle que `types.json` : ne jamais écraser les réglages existants.
- **Le skill voyage avec le coffre** : à l'init, le skill complet est copié
  dans `<coffre>/.gemini/skills/note-ai/` (même format SKILL.md que Claude
  Code, activé via `activate_skill`). Une machine neuve avec Gemini CLI n'a
  **rien à installer** : ouvrir le coffre suffit. Côté Claude Code, le skill
  vient du plugin (marketplace) — la copie du coffre ne sert qu'à Gemini.
- **Différences de moyens connues** : sous-agents (Claude : oui, Haiku ;
  Gemini : non → par lots) · mode YOLO (`--dangerously-skip-permissions` /
  `--yolo`) · le bootstrap d'un coffre **vierge** demande le skill (plugin
  Claude ou copie dans `~/.gemini/skills/`) — un coffre déjà initialisé n'a
  besoin de rien.
