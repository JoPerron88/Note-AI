# Concept — « Note AI » (OneNote augmenté à l'IA)

> Document de travail vivant. Capture des idées et du cadrage avant toute décision
> technique ferme. Rien ici n'est gravé dans le marbre — c'est une mise au propre
> de la réflexion en cours.
>
> Dernière mise à jour : 2026-06-10

---

## 1. La vision en une phrase

Un **atelier de connaissance personnel, 100 % local, en Markdown**, où une IA (Claude)
joue le rôle de **bibliothécaire / adjoint** : elle range, réécrit, retrouve et suit
tes projets — le tout pensé pour **économiser les tokens**.

Autrement dit : **un « OneNote piloté par l'IA »**, où l'IA n'est pas un gadget collé
à côté mais le **cœur de l'organisation**.

### Le but final, en clair (modèle mental verrouillé)

Avoir **quelque chose** — peu importe la forme : logiciel, interface, extension, outil
en terminal… — qui **ressemble à OneNote** dans sa structure :

- **Notebooks** (carnets) › **Sections** › **Pages**.

…avec **deux façons de l'utiliser, à parts égales** :

1. **À la main** : je consulte et je modifie mes pages directement, comme dans n'importe
   quel carnet de notes.
2. **Via le chat** : je demande à Claude / Claude Code ce que je veux, et il agit
   (range, crée, réécrit, retrouve).

👉 En somme : **un « Notebook » assisté par Claude — « Note AI ».**
La structure OneNote (Notebooks / Sections / Pages) **n'est pas négociable** ; ce qui
reste ouvert, c'est *sous quelle forme* on la livre (voir §5, le carrefour technique).

---

## 2. Ce que ça fait (fonctionnalités imaginées)

- **Un chat-adjoint conversationnel** : tu écris en langage naturel
  (« mets ça dans le projet X », « crée un projet Y », « retrouve-moi mes notes sur Z »)
  et l'IA agit : elle prend des notes, les **réécrit proprement**, classe, crée des projets,
  retrouve l'information.
- **« Drop n'importe quoi »** : tu lui balances du texte, des fichiers ou des images,
  et tu dis où ça va — ou tu la laisses décider.
- **Documents en entrée** : PDF, TXT, et autres formats courants.
- **Images** : à **classer / ranger** dans le bon projet. ❌ Pas besoin d'OCR
  (on ne lit pas le contenu des images, on les range).
- **Deux couches de stockage** :
  - **Couche humaine** → notes en **Markdown**, avec une **interface de lecture** propre.
  - **Couche machine** → un **index condensé, optimisé pour l'IA**, qu'elle lit pour se
    repérer **sans relire tout le contenu** à chaque fois (l'astuce NotebookLM :
    la référence reste accessible, mais on ne recharge pas tout bêtement → économie de tokens).
- **Structure de suivi de projet intégrée** :
  - un **cahier maître** (suivi global, vue d'ensemble) ;
  - des **cahiers de projet** (un par projet) ;
  - un **système de tâches + échéances**.
- **Local d'abord** : sauvegarde et **historique / versionnement** des notes.

---

## 3. Qui s'en sert

- **Un seul utilisateur** (toi). Pas de multi-utilisateur prévu.
- **Possiblement plusieurs appareils** (PC fixe + portable), si les données vivent dans
  un **dossier synchronisé sur le cloud** (iCloud / Dropbox / OneDrive — à préciser).

---

## 4. Contraintes (ce qui est ferme vs. flexible)

| Sujet | Statut | Détail |
|-------|--------|--------|
| **Plateformes** | 🔒 Ferme | **Windows + Mac** |
| **Local** | 🔒 Ferme | Données chez l'utilisateur, pas dans un service tiers |
| **Open source** | 🔒 Ferme | On reste dans l'écosystème open source |
| **IA — pas d'API Claude** | 🔒 Ferme | On **n'utilise pas** l'API payante d'Anthropic |
| **IA — comment piloter Claude** | 🔓 Ouvert | `claude -p` (Claude Code en mode headless) est **une piste parmi d'autres**, pas une obligation |
| **Langage** | 🔓 Ouvert | Indifférent. Faible pour le **C#**, mais **pas obligatoire** |
| **Format** | 🔓 Ouvert | Markdown pressenti pour les notes, mais rien d'imposé |
| **Multi-appareils** | 🔓 Souhait | Pas bloquant, mais ne pas se fermer la porte (via dossier cloud synchro) |

---

## 5. Le carrefour technique (3 routes à explorer)

Le projet peut prendre des formes très différentes. Trois directions, pas encore tranchées :

### Route A — Construire l'app de zéro
- Ex. C# (Avalonia / MAUI pour le multi-plateforme), ou autre stack.
- ✅ Contrôle total, exactement ce qu'on veut.
- ⚠️ On « réinvente OneNote » → gros effort, risque de s'enliser.

### Route B — Greffer le « cerveau IA » sur Obsidian
- Obsidian est **déjà** : un vault Markdown local, une belle interface de lecture,
  une sync par dossier cloud, un écosystème de plugins (tâches, Kanban, **terminal intégré**…).
- On n'écrirait **que la partie IA** (un plugin).
- ✅ 80 % du « OneNote » est déjà fait.
- ⚠️ Obsidian lui-même **n'est pas open source** (gratuit mais propriétaire) →
  **à confronter avec la contrainte open source**.

### Route C — Greffer sur VSCode / VSCodium
- VSCodium = build **open source** de VSCode. Terminal natif, multi-plateforme,
  énorme écosystème d'extensions.
- ✅ Cohérent avec la contrainte open source + Win/Mac.
- ⚠️ Interface plus « éditeur de code » que « carnet de notes » → à voir si l'expérience colle.

> 💡 Observation déclencheuse : l'existence d'un **plugin terminal dans Obsidian** suggère
> que le projet pourrait être **un plugin/extension** plutôt qu'un logiciel autonome.

---

## 6. Idées en vrac (à trier plus tard)

- Pouvoir « droper n'importe quoi » et dire « mets ça dans tel projet ».
- L'IA **réécrit** les notes (pas juste stockage brut).
- Référence façon **NotebookLM** : l'IA a accès au corpus quand elle en a besoin.
- Index « mécanique » optimisé tokens (format compact, lisible machine).
- Cahier maître + cahiers de projet + tâches/échéances comme ossature de suivi.

---

## 7. À explorer ensuite (prochaines étapes)

- [ ] **Recherche : comment fonctionne OneNote** → extraire les bonnes idées à reprendre.
- [ ] **Comparer les 3 routes** (A/B/C) sous l'angle : open source + Win/Mac + IA sans API.
- [ ] **Clarifier le pilotage de l'IA** sans API (options au-delà de `claude -p`).
- [ ] **Maquette** de l'interface une fois la direction choisie.
- [ ] Définir le **scope de la V1** (qu'est-ce qui livre 80 % de la valeur avec 30 % de l'effort ?).

---

## 8. Idées de Claude (suggestions à débattre — rien d'arrêté)

> Pistes que je lance pour nourrir la réflexion. À garder, modifier ou jeter.

### 8.1 — L'IA n'a peut-être pas besoin qu'on « construise » grand-chose
Claude Code est **déjà** un agent qui sait lire/écrire des fichiers dans un dossier,
chercher dedans (`grep`), créer des sous-dossiers, etc. Pointé sur ton vault de notes,
**il fait déjà 80 % du « cerveau »**. Conséquence possible : le projet n'est pas tant
« coder une IA » que **poser les bonnes conventions** (structure de dossiers, format
des notes, index) **+ une interface agréable** par-dessus. Ça réduit énormément l'effort.

### 8.2 — Le dossier `_inbox/` (séparer capturer et ranger)
Un dossier « boîte de réception » où tu **déposes n'importe quoi** sans réfléchir
(texte, PDF, image). Quand tu veux, tu dis « range l'inbox » et l'IA **trie** :
elle classe, renomme, réécrit, et vide la boîte. Avantage : capturer une idée devient
instantané, le rangement se fait à froid. C'est le « drop n'importe quoi » version propre.

### 8.3 — La hiérarchie OneNote = une arborescence de dossiers
On mappe directement **Notebook › Section › Page** sur le système de fichiers.
Chaque page est un `.md`. Lisible, durable, et l'IA s'y repère nativement :
```
Notebooks/
  Maison/                    ← NOTEBOOK
    _notebook.ai.md          ← index condensé du notebook (généré, économie de tokens)
    Cuisine/                 ← SECTION
      2026-06-10-plan.md     ← PAGE
      devis-armoires.md      ← PAGE
      captures/
        plan-cuisine.png
    Jardin/                  ← SECTION
      semis-printemps.md     ← PAGE
Cahier-maître.md             ← vue d'ensemble de tous les notebooks
```
Chaque page commence par un petit en-tête (titre, date, tags, résumé d'une ligne).
**Tout reste lisible et modifiable à la main** — même sans le logiciel, tu t'y retrouves.
C'est ce qui rend possible le **double accès** (main + chat) sur les *mêmes* fichiers.

### 8.4 — La « couche machine » = des index générés, pas une base de données
Pas besoin d'un format exotique. L'index optimisé tokens peut être un simple
`_index.ai.md` par projet : **le nom de chaque note + un résumé d'une ligne + ses tags**.
L'IA lit *cet index* d'abord (quelques lignes) au lieu de relire toutes les notes →
elle sait *où* aller chercher avant d'ouvrir le bon fichier. **C'est exactement ta couche
mécanique optimisée**, et c'est trivial à régénérer.

### 8.5 — Images sans OCR : une légende au moment du drop
Puisqu'on ne lit pas dans les images, le seul moyen de les retrouver, c'est une
**légende d'une ligne** écrite au moment où tu la déposes (« plan de la cuisine, version 2 »).
Stockée à côté de l'image (dans l'index, ou un petit `.md` jumeau). Sinon une image
devient introuvable. Petit détail, gros impact sur l'utilité.

### 8.6 — Tâches = cases à cocher Markdown standard
Pas de système maison. Les tâches sont des `- [ ] Faire X 📅 2026-06-15` dans les notes.
**Avantage** : c'est le format que comprennent déjà Obsidian, les plugins Tasks, etc.
L'IA peut les lister, les trier par échéance, te faire un récap — sans qu'on invente rien.

### 8.7 — L'historique gratuit : Git en coulisse
Pour « sauvegarde + historique », **Git** fait tout le travail, gratuitement et localement :
chaque modif est versionnée, tu peux revenir en arrière, et ça se synchronise via le
dossier cloud. L'utilisateur ne voit jamais Git — le logiciel l'utilise en silence.

### 8.8 — Mode « propose puis applique » (confiance)
Au début, l'IA **propose** ses rangements (« je classe ces 3 fichiers comme ça, OK ? »)
plutôt que d'agir en douce. Quand tu lui fais confiance, tu passes en mode automatique.
Ça évite la peur de « l'IA qui met le bordel dans mes notes ».

---

## 9. Reconnaissance — Phase 1 (recherche, 2026-06-10)

> Synthèse condensée de deux recons web. Faits, pas décisions. La décision (Phase 2) suit.

### 9.1 — Ce qu'on pique à OneNote / ce qu'on évite

**Hiérarchie réelle de OneNote :** Notebook › *Section Group* › Section › Page › *Subpage*
(subpages limitées à **2 niveaux** — frustration connue).

**À reprendre :**
- **Tags + vue résumé transversale** : regrouper tous les éléments tagués (To-Do, Important…)
  à travers tout le carnet, filtrables. Très fort pour le suivi de tâches.
- **Recherche full-text** partout, instantanée.
- **Modèle mental « classeur à onglets »** : familier, onboarding rapide.
- **Multimédia sur la page** (images, pièces jointes) sans quitter la note.

**À éviter (les douleurs de OneNote) :**
- ❌ **Format binaire propriétaire `.one`**, **zéro Markdown**, **export laborieux** → lock-in.
- ❌ **OneDrive obligatoire** (sync capricieuse, ralentit sur gros carnets).
- ❌ **Gestion de tâches faible** : pas de date d'échéance native, pas de vue calendrier/kanban.

**💡 Positionnement clé :** OneNote 2016 (la dernière version *locale*) est en fin de vie
(support étendu jusqu'à oct. 2025) → OneNote devient **cloud-only**. Le créneau « **100 % local,
Markdown, à toi** » que vise Note AI est *exactement* le manque que OneNote laisse béant.

### 9.2 — Comparatif des 3 routes (condensé)

| Critère | A — App de zéro | B — Plugin Obsidian | C — Extension VSCodium |
|---|---|---|---|
| Effort pour un amateur | 🔴 Très élevé (mois de travail) | 🟢 Modéré (TypeScript, bcp réutilisé) | 🟡 Modéré-faible |
| UX d'édition « carnet » à la main | 🔴 À tout construire | 🟢 **La meilleure** (live preview) | 🟡 Ressenti « éditeur de code » |
| Arborescence Notebook/Section/Page | 🔴 À construire | 🟢 Native (dossiers = carnet) | 🟡 Native mais ambiance IDE |
| Open source | 🟢 Total | 🔴 **Obsidian propriétaire** (gratuit) | 🟢 **Total (MIT)** |
| Windows + Mac | 🟢 Oui | 🟢 Oui | 🟢 Oui (via Open VSX) |
| Brancher Claude sans API | 🟡 OK (subprocess) | 🟢 **Prouvé** (plugin *Claudian*) | 🟡 Faisable, moins éprouvé |

**En clair :** Obsidian = effort minimal + meilleure expérience, mais propriétaire.
VSCodium = 100 % open source, mais ambiance IDE. App de zéro = liberté totale, coût hors de
proportion pour un amateur visant une V1 rapide.

### 9.3 — ⚠️ VÉRIFIÉ : `claude -p` bascule en facturation API au 15 juin 2026

**Confirmé** par plusieurs sources, dont le **centre d'aide Claude officiel** et un **ticket
GitHub sur `anthropics/claude-code`** (#37686). Annoncé le 14 mai 2026, effet **15 juin 2026** :

- Le mode **headless `claude -p`** (+ Claude Agent SDK, Claude Code GitHub Actions, agents
  tiers) **sort des limites de l'abonnement** et bascule sur un **crédit mensuel séparé,
  facturé au tarif API**, sans report (~20 $ Pro / 100 $ Max 5x / 200 $ Max 20x par mois).
  Une fois épuisé → facturation à l'API. *Un utilisateur du ticket GitHub rapporte 1 800 $ de
  facturation API en 2 jours via `claude -p`.*
- ✅ **Reste sur l'abonnement, inchangé** : **Claude Code interactif dans le terminal**, et
  Claude.ai (web/desktop/mobile). **Seul l'usage programmatique** (`claude -p`, SDK, Actions)
  bascule sur le crédit séparé.

**Conséquences pour Note AI :**
1. ❌ Piloter Claude via `claude -p` en arrière-plan = **revient de facto à payer l'API** →
   **contredit ta règle « pas d'API »** au-delà du petit crédit mensuel.
2. 💡 **Mais le Claude Code *interactif* reste sur l'abonnement.** Piste à creuser en Phase 2 :
   Note AI pourrait-il s'appuyer sur une session Claude Code **interactive** plutôt que headless ?
3. 🔄 **Alternative sérieuse** : **modèle local via Ollama** (Llama/Mistral/Qwen) — zéro coût
   récurrent, hors-ligne, compatible avec les 3 routes.
- (Détail technique réglé : le bug Node qui bloquait `claude -p` depuis un plugin est contourné
  en pratique — le plugin *Claudian* le fait tourner sur Win/Mac.)

---

## 10. Arbitrage — Phase 2 (synthèse et recommandation, 2026-06-10)

> La décision se joue sur **deux axes croisés** : la **forme de livraison** (A/B/C) ET le
> **moteur IA** (comment piloter Claude sans payer l'API). Il faut trancher les deux.

### 10.1 — Axe 1 : la forme de livraison

| Critère (pondéré pour un amateur visant une V1 rapide) | A — App de zéro | B — Obsidian | C — VSCodium |
|---|---|---|---|
| Effort jusqu'à une V1 utilisable | 🔴 Mois | 🟢 Jours/semaines | 🟡 Semaines |
| Expérience « carnet » à la main (double accès) | 🔴 À bâtir | 🟢 **Excellente** | 🟡 Ambiance IDE |
| Structure Notebook/Section/Page native | 🔴 À bâtir | 🟢 Dossiers natifs | 🟡 Arbo IDE |
| Open source | 🟢 Total | 🔴 Propriétaire* | 🟢 Total (MIT) |
| Brancher Claude prouvé en pratique | 🟡 | 🟢 *Claudian* + terminal intégré | 🟡 À faire soi-même |
| Risque d'enlisement | 🔴 Élevé | 🟢 Faible | 🟡 Moyen |

*\*Obsidian est propriétaire, MAIS tes données restent du Markdown brut dans un dossier → **aucun
verrouillage des données**, seul l'outil serait à remplacer. C'est la « supériorité nette »
qui justifie de passer outre la préférence open source (cf. ton choix « résultat prime »).*

→ **Route A écartée** pour la V1 (effort hors de proportion ; reste une aspiration long terme).
La vraie question est **B vs C** : confort maximal (Obsidian, propriétaire) **vs** pureté open
source (VSCodium, ambiance éditeur de code). *Note : entre les deux, **Logseq** existe — open
source, Markdown local — mais son modèle « outliner » colle moins à la structure OneNote.*

### 10.2 — Axe 2 : le moteur IA (le point qui a tout changé)

| Option | Coût | Qualité | Verdict |
|---|---|---|---|
| `claude -p` headless / Agent SDK | 🔴 **Tarif API** dès le 15/06/2026 | 🟢 Claude | ❌ Contredit « pas d'API » |
| **Claude Code *interactif*** (terminal) | 🟢 **Sur l'abonnement** | 🟢 Claude | ✅ **La voie** |
| Modèle local (Ollama) | 🟢 Gratuit, hors-ligne | 🟡 < Claude sur « range/réécris » | 🟡 Repli/option privée |

💡 **L'insight clé :** le terminal intégré que tu as repéré dans Obsidian n'était pas un détail —
c'est *la* solution. **Claude Code tourne en interactif dans ce terminal, pointé sur ton vault,
sur ton abonnement.** Tu lui parles, il lit/écrit tes fichiers Markdown directement. Le plugin
n'a pas à « appeler une IA » : il fournit **les conventions** (structure, `_index.ai.md`, inbox)
**et le confort de lecture** ; le « chat-adjoint », c'est Claude Code lui-même.

### 10.3 — Recommandation

**Direction recommandée : Route B (Obsidian) + Claude Code interactif dans le terminal intégré,
avec Ollama en repli local optionnel.**

- Livre vite, expérience de carnet la meilleure, structure OneNote native, pilotage de Claude
  **sur l'abonnement** (pas d'API), wiring déjà éprouvé par la communauté.
- Le travail réel se concentre sur **les conventions + le confort**, pas sur réinventer OneNote.
- ⚠️ Seul compromis : Obsidian propriétaire (données non verrouillées car Markdown).

**Alternative de principe : Route C (VSCodium)** si la pureté open source pèse plus que le
confort quotidien — au prix d'une ergonomie « éditeur de code » et de plus de travail de wiring.

→ **Décision qui te revient (c'est un arbitrage de valeurs) : B ou C ?**

### 10.4 — Verdict du débat (Obsidian vs VSCodium, 2026-06-10)

Débat à 3 entités : un avocat pro-Obsidian, un avocat pro-VSCodium, un arbitre neutre.
**Convergence claire → Route B (Obsidian).** Les trois s'accordent sur :

1. **Le critère qui départe = combien de code l'amateur doit écrire.** Obsidian fournit la
   structure Notebook/Section/Page, le rendu Markdown, la recherche, le drag&drop **sans une
   ligne de code** (+ *Claudian* prouve le terminal Claude Code). VSCodium impose d'écrire une
   extension TypeScript (~300-500 lignes) — barrière réelle pour un concepteur non-développeur.
   *L'avocat VSCodium le concède lui-même.*
2. **L'open source pèse quasi nul ici.** Tu as dit « résultat prime », et surtout : tes données
   restent du Markdown brut local dans les deux cas → **aucun verrouillage**. La dépendance à
   Obsidian porte sur l'interface, pas sur les données.
3. **Logseq = fausse piste** (tranché par l'arbitre) : modèle « outliner » qui diverge de
   OneNote, pilotage Claude moins éprouvé. N'apporte rien de net face à Obsidian.

**Risques à surveiller (verdict de l'arbitre) :**
- **Maintenance de Claudian** : vérifier qu'il est activement maintenu ; prévoir un repli
  « terminal natif » si besoin.
- **Modèle de licence Obsidian** : surveiller (gratuit usage perso aujourd'hui ; données libres).
- **Dérive du vault** : fixer **dès le départ la convention de nommage** Notebook/Section/Page
  pour que l'humain ET l'IA naviguent pareil.

## ✅ DIRECTION ARRÊTÉE

**Note AI = plugin/conventions sur Obsidian + Claude Code interactif dans le terminal intégré
(sur abonnement), Ollama en repli local optionnel.** Reste à faire : maquette, puis scope V1.

---

## 11. Fonctions Obsidian exploitées par Note AI (acquis « gratuits »)

> Ce qu'Obsidian fournit déjà, et qu'on n'a donc **pas à construire**. Le travail de Note AI
> = orchestrer tout ça via Claude + des conventions, pas le réinventer.

### 11.1 — Les liens : le réseau de connaissance (façon NotebookLM)
- **Wikilinks `[[Page]]`** (et `[[Page|alias]]`) : liens internes cliquables entre notes.
- **Backlinks (rétroliens)** : chaque page liste *automatiquement* qui pointe vers elle —
  zéro maintenance. Ouvrir `Acier-S235` → voir tous les projets qui l'utilisent.
- **Mentions non liées** : Obsidian repère le nom d'une page cité sans lien et propose de lier.
- **Embeds `![[Page]]` / `![[Page#Section]]`** : incruster une note (ou une section, un bloc)
  dans une autre → idéal pour un **cahier maître** qui agrège des bouts de cahiers de projet.
- **Vue graphe** : carte visuelle (globale ou locale) des notes reliées.
- 💡 **Claude lit et écrit ces liens depuis le terminal** : il relie une nouvelle note aux pages
  pertinentes automatiquement. Les `[[liens]]` font partie de la « couche machine » (avec
  `_index.ai.md`).

### 11.2 — Classement et métadonnées
- **Dossiers** = Notebooks › Sections › Pages (la structure OneNote, gratuite).
- **Tags hiérarchiques `#projet/maison`** : le classement **transversal** repris de OneNote.
- **Propriétés (frontmatter YAML)** : métadonnées par note (`date`, `statut`, `échéance`…),
  **lisibles par la machine** → socle de l'index IA, des tâches/échéances, du suivi de projet.

### 11.3 — Tâches, tableaux de bord, contenu
- **Cases à cocher `- [ ]`** : système de tâches en Markdown standard.
- **Recherche full-text** : Claude et toi retrouvez tout instantanément.
- **Pièces jointes (drag & drop PDF/images)** : ton « drop n'importe quoi » ; images rangées +
  légendées par Claude (pas d'OCR).
- **Canvas** (tableau blanc infini) et **Templates** (gabarits de notes) : optionnels.
- **Maths LaTeX inline** *(acquis V1)* : `$...$` et `$$...$$` rendus nativement, **mélangés au
  Markdown dans le même fichier** — parfait pour les formules d'un carnet technique.

### 11.4 — Trois plugins clés pour Note AI
- **Terminal** → fait tourner Claude Code interactif dans Obsidian (le chat-adjoint).
- **Dataview** → requêtes dans une note (« liste les pages du projet Maison à échéance cette
  semaine ») → table générée auto = **cahier maître / tableau de bord vivant**.
- **Tasks** → centralise toutes les `- [ ]` avec échéances dans une vue unique.

→ **Conclusion :** liens+backlinks+graphe (réseau), tags+propriétés (classement machine),
Dataview+Tasks (tableaux de bord) donnent **déjà** l'ossature du cahier maître, des cahiers de
projet et du système de tâches. Note AI = la couche d'orchestration Claude + conventions.

---

## 12. Note AI, concrètement (capstone — 2026-06-10)

> Synthèse tangible une fois toutes les décisions prises. C'est à ça que ressemble Note AI.

### 12.1 — À quoi ressemble le vault

```
Note-AI-Vault/                     ← le dossier, synchronisé sur le cloud
├─ Cahier-maître.md                ← vue d'ensemble de TOUS les projets (table Dataview)
├─ _inbox/                         ← tu déposes ici sans réfléchir ; Claude trie ensuite
│  └─ capture-2026-06-10-1432.png
├─ Projets/
│  ├─ Maison/                      ← NOTEBOOK
│  │  ├─ _projet.md                ← cahier de projet (objectif, statut, échéances)
│  │  ├─ _index.ai.md              ← index condensé POUR CLAUDE (généré, économie de tokens)
│  │  ├─ Cuisine/                  ← SECTION
│  │  │  ├─ 2026-06-10-plan-cuisine.md     ← PAGE
│  │  │  └─ captures/plan-v2.png
│  │  └─ Jardin/                   ← SECTION
│  └─ Atelier/                     ← NOTEBOOK
└─ .obsidian/                      ← config + plugins (Terminal, Dataview, Tasks)
```

### 12.2 — À quoi ressemble une page

```markdown
---
titre: Plan cuisine
projet: Maison/Cuisine
date: 2026-06-10
statut: en-cours
tags: [cuisine, structure]
resume: Calcul de la poutre porteuse + relevé des dimensions.
---

# Plan cuisine

Poutre porteuse, charge répartie q sur longueur L. Flèche maximale :
$$\delta_{max} = \frac{5\,q\,L^4}{384\,E\,I}$$

![[captures/plan-v2.png]]

- [ ] Valider la section IPN 📅 2026-06-20
- Voir aussi [[devis-armoires]]
```

Le `resume:` et les `tags:` du frontmatter sont ce que Claude récolte pour bâtir l'index ↓

### 12.3 — La « couche machine » : `_index.ai.md` (généré)

```markdown
# Index IA — Notebook Maison   (généré par Claude, ne pas éditer à la main)
- Cuisine/2026-06-10-plan-cuisine.md — calcul poutre porteuse + dimensions [cuisine,structure] (en-cours)
- Cuisine/devis-armoires.md — devis 3 fournisseurs [cuisine,devis] (à-faire)
- Jardin/semis-printemps.md — planning + plan de massif [jardin] (terminé)
```

Claude lit **ces 3 lignes** pour savoir *où* aller, au lieu de relire toutes les pages → économie
de tokens. Mis à jour à chaque rangement.

### 12.4 — Une journée avec Note AI (scénario concret)

1. **Réunion chantier.** Tu photographies le plan annoté → tu glisses la photo dans `_inbox/`.
2. **Tu ouvres le terminal** (Claude Code, dans Obsidian) et tu écris en langage naturel :
   *« range la dernière capture dans Maison/Cuisine, c'est le plan révisé de la poutre. »*
3. **Claude agit** : déplace l'image dans `Projets/Maison/Cuisine/captures/`, la renomme, crée
   ou met à jour la page avec une **légende** (pas d'OCR), pose le lien `[[…]]`, régénère
   `_index.ai.md`. → Mode **« propose puis applique »** : il te montre le changement, tu valides.
4. **Plus tard.** *« Rappelle-moi où j'en suis sur la cuisine. »* → Claude lit `_index.ai.md` +
   `_projet.md` (pas tout le contenu) → te sort un résumé + les tâches en retard.

### 12.5 — Qui fait quoi (répartition claire)

| Couche | Rôle |
|---|---|
| **Obsidian** (gratuit) | Rendu Markdown + LaTeX, arborescence, liens/backlinks/graphe, recherche, tags, propriétés, Dataview/Tasks, terminal intégré |
| **Claude Code** (abonnement, terminal) | Comprendre le langage naturel ; ranger/renommer/réécrire ; générer les `_index.ai.md` ; poser les liens ; résumer ; suivre les tâches |
| **Les conventions** (ce qu'ON définit = le vrai livrable) | Structure Notebook/Section/Page, `_inbox/`, frontmatter type, `_index.ai.md`, `Cahier-maître.md`, nommage `AAAA-MM-JJ-slug`, mode « propose puis applique » |

→ **Le « produit » Note AI = surtout un jeu de conventions + un mode d'emploi de Claude**, pas du
code lourd. (Un petit plugin/commandes peut venir plus tard pour automatiser, mais n'est pas
indispensable à la V1.)

### 12.6 — Périmètre V1 (80 % de la valeur, 30 % de l'effort)

**Dans la V1 :** structure + conventions · `_inbox` + « range ça » piloté par Claude · frontmatter
+ `_index.ai.md` généré · `Cahier-maître.md` en Dataview · tâches en cases à cocher (plugin Tasks)
· LaTeX inline · images rangées + légendées.

**Plus tard :** repli Ollama hors-ligne · automatisations/commandes packagées · génération
proactive · multi-vault · raffinements d'ergonomie.
