# Handoff — Note AI
> Dernière mise à jour : 2026-06-11. Reprise à froid : si tu n'as pas l'outillage de ce projet,
> lis d'abord `OUTILLAGE.md` (à côté), puis ce fichier.

## Le but (FinalGoal)
Un carnet de notes personnel « façon OneNote augmenté à l'IA », **100 % local**, construit **sur
Obsidian** (Notebooks › Sections › Pages = dossiers / fichiers Markdown). Un assistant **Claude
(Claude Code interactif dans le terminal intégré)** range, réécrit, retrouve et suit les projets,
avec une couche d'index optimisée pour économiser les tokens.
*Réussi =* je dépose n'importe quoi (texte, PDF, capture), je dis « range ça dans tel projet », et
c'est classé/réécrit/indexé en quelques secondes ; je consulte/modifie à la main aussi
naturellement que via le chat. → Détail complet dans `.multivac/goal.md`.

## Où on en est
- Branche : `main` · Arbre de travail **propre** (tout commité et poussé).
- Remote : `origin → github.com/JoPerron88/Note-AI.git`.
- **Stade = V1 CONSTRUITE, EN TEST.** Le produit est un **plugin Claude Code autosuffisant**
  (aucune dépendance à d'autres skills/plugins — décision ferme du 2026-06-10).
- ✅ **`CLAUDE.md` créé à la racine** (2026-06-10) : instructions projet pour les futures
  sessions — décisions arrêtées, conventions du vault, carte des documents.
- ✅ **Maquette livrée** (2026-06-10) dans `maquette/` : `MAQUETTE.md` + `maquette.html`,
  4 vues (fenêtre Obsidian, flux « drop → range », cahier-maître, page type).
- ✅ **Plugin V1 construit** (2026-06-10) : le dépôt est un marketplace Claude Code
  (`.claude-plugin/marketplace.json`) ; le plugin vit dans `plugins/note-ai/` —
  `SKILL.md` (déclencheurs + comportements + bootstrap automatique d'un coffre),
  `references/conventions.md` (le §12 distillé), `references/templates/` (`CLAUDE-coffre.md`
  déposé à l'init = adjoint par défaut, `Cahier-maitre.md`, `projet.md`). README d'installation
  refait. Manifestes validés (JSON + chemins + frontmatter ≤ 1024 car.).
- ✅ **Standard fr-CA arrêté et appliqué** (2026-06-10) : nommage hybride (dossiers accentués,
  pages en slug), frontmatter en français accentué (`titre, projet, date, statut, tags, résumé,
  échéance` ; statuts `à-faire/en-cours/en-pause/terminé`), `_inbox/` → `_boîte/`, typographie
  OQLF + vocabulaire québécois à la réécriture, dates longues en prose (ISO pour la machine),
  orthographe traditionnelle.
- ✅ **Répertoire des gens** (2026-06-10) : `Gens/` à la racine du coffre, une fiche par
  personne au nom humain (`Marie Tremblay.md`, avec `aliases:`), `Gens/_moi.md` = fiche du
  **propriétaire** créée par mini-entrevue à l'init (l'adjoint sait qui est son humain et
  adapte : travail → organisations ; privé → cercles). Détection au rangement (propose la
  fiche), garde-fou : factuel seulement, jamais de déductions.
- ✅ **Couche machine `.note-ai/` + grille d'effort** (2026-06-10) : dossier caché (invisible
  dans Obsidian) = territoire de l'adjoint — `carte.md` (lue en premier), `memoire.md`,
  `journal.md`, `index/<Notebook>.md` + `index/gens.md` (**les index ont déménagé ici**),
  format libre permis. Grille d'effort léger/moyen/lourd ; au lourd, mécanique de masse en
  sous-agent **Haiku** (jamais de jugement en sous-agent). §liens réécrit : résolution par nom,
  `aliases:`, backlinks = `grep "[[Nom"` (n'existent pas sur disque).
- ✅ **Propriétés Obsidian exploitées** (2026-06-10) : (a) typage via
  `templates/obsidian-types.json`, **fusionné** dans `.obsidian/types.json` à l'init
  (`date`/`échéance` → Date, `tags`/`aliases` → Liste) — **seule exception** à « ne jamais
  toucher `.obsidian/` » (fusion sans écraser) ; (b) Cahier-maître en **Base native**
  (`templates/Cahier-maitre.base`, 2 vues : Projets + Échéances à venir), embarquée dans
  `Cahier-maître.md` via `![[…#vue]]`, **bloc Dataview retiré** (Bases = cœur d'Obsidian =
  autosuffisant). Tableau de bord = 3 couches : table statique (plancher) + Bases (confort) +
  Tasks (optionnel, cases `- [ ]`). Syntaxe `.base` vérifiée sur la doc officielle ; livrée en
  **gabarit** (propriété accentuée → `note["échéance"]`), à confirmer dans l'éditeur de Bases.
- ✅ **Extension Claude sidebar comprise + 2 raffinements** (2026-06-11) : l'extension
  `derek-larson14/obsidian-claude-sidebar` lance **Claude Code CLI en interactif** (PTY +
  xterm.js), **sans clé API** (s'appuie sur la CLI authentifiée → reste sur l'abonnement) —
  confirme toute la fondation. Déps : Python 3 + Claude Code (Windows : `pywinpty`). Deux
  durcissements ajoutés au SKILL + `CLAUDE.md` de coffre : (1) **ancrage à la racine du
  coffre** (l'extension peut ouvrir Claude dans un sous-dossier via clic droit → ancrer tous
  les chemins là où vit `.obsidian/`) ; (2) **mode YOLO** (`--dangerously-skip-permissions`)
  → propose-puis-applique devient le seul garde-fou, à garder strict.
- ✅ **Bi-moteur : Gemini CLI à égalité avec Claude Code** (2026-06-11, cap amendé dans
  `goal.md` + `CLAUDE.md` projet — « pas d'API payante » intact, Gemini = palier gratuit).
  Architecture : (1) **source unique** — le `CLAUDE.md` du coffre, réécrit **neutre-moteur** ;
  Gemini le lit via `<coffre>/.gemini/settings.json` (`context.fileName: ["CLAUDE.md",
  "GEMINI.md"]`, template `gemini-settings.json`, fusion sans écraser) ; (2) **skill copié dans
  le coffre** à l'init (`.gemini/skills/note-ai/` — même format SKILL.md, vérifié doc
  officielle) → coffre autoportant, zéro install sur machine neuve ; (3) différences
  conditionnées (conventions §13) : sous-agents Haiku si harnais le permet sinon par lots,
  YOLO = `--dangerously-skip-permissions`/`--yolo`. À confirmer au test : forme
  `context.fileName` (ancienne clé plate `contextFileName` notée en §13) et fiabilité du
  bootstrap auto via `activate_skill` côté Gemini.
- Contexte d'usage : l'utilisateur a installé **Obsidian + Claude sidebar** (Claude Code
  interactif dans Obsidian) — c'est le terrain de test réel.
- ✅ **Piste v2 ouverte : app standalone sur base Claudian** (2026-06-11, demande explicite).
  Deux décisions du 2026-06-10 rouvertes POUR LA V2 (la v1 reste en test, voie zéro surcoût) :
  forme = **app Electron standalone** réutilisant le code du plugin Claudian (~70 % déjà
  indépendant d'Obsidian — `ClaudeChatRuntime` ne demande que 4 choses à son hôte) ; moteur =
  **Agent SDK accepté** en connaissance de cause (coût = risque n°1, parades prévues au plan).
  Cap amendé dans `goal.md` + `CONCEPT.md` §13. **Tout le travail v2 vit dans le repo
  `JoPerron88/Claudian-Note`** : `NOTE-AI-V2-PLAN.md` (architecture : un repo Electron+React,
  claudian en git subtree + shim du module `obsidian`, phases 0-5 avec critères de done),
  `FAISABILITE-STANDALONE.md`, `CLAUDIAN-COMPREHENSION.md` ; clones de référence `claudian/`
  et `Note-AI/` à côté (dossier iCloud `…/Projet Claude Code/Claudian Note/`).

## Ce qui était prévu ensuite
1. **Test réel** : installation via `/plugin marketplace add JoPerron88/Note-AI` +
   `/plugin install note-ai@note-ai` dans Claude sidebar, init d'un coffre, scénarios du
   concept (« range ça », « où en suis-je »…). Les ratés observés = matière du REFACTOR
   (le skill n'a pas eu de tests sous-agents — le test réel en tient lieu).
2. Itérations sur le skill selon les retours ; « plus tard » du §12.6 (Ollama, automatisations).
3. **Piste v2 — Phase 0 LIVRÉE (2026-06-11)** : repo **`JoPerron88/note-ai-app`** (privé).
   Walking skeleton fonctionnel : vendor claudian en subtree + shim obsidian, AgentService
   (ClaudeChatRuntime hors Obsidian), **smoke test headless VERT** (tour réel → approbation
   Write → fichier créé → contexte conservé), fenêtre Electron minimale (picker de dossier,
   chat streamé, carte d'approbation) qui boot sans crash. `npm run smoke` / `npm run dev`.
   Pièges résolus consignés dans `findings.md` du dossier parent (`Claudian Note/`) :
   ApprovalDecision='allow', safeMode 'default' obligatoire pour les approbations,
   types obsidian@1.8.7 + runtime shim, casse APFS (note-ai = Note-AI → note-ai-app).
   **Phase 1 (le carnet) LIVRÉE aussi (2026-06-11)** : arbre Notebooks›Sections›Pages avec
   CRUD (corbeille système), éditeur CodeMirror 6 (source + bascule Lecture), préview
   markdown-it (wikilinks navigables, cases cochables qui réécrivent le fichier, KaTeX,
   images via protocole `noteai-asset://` borné), bandeau frontmatter tolérant, watcher
   chokidar (reload auto si buffer propre, bannière si conflit). `npm run smoke:notes` VERT.
   Coffre de test prêt : `Claudian Note/coffre-test/` (page CONCEPT §12.2 complète).
   **Phase 2 (chat complet) LIVRÉE aussi (2026-06-11)** : sessions persistées + reprise avec
   contexte (meta `.claudian/sessions/`, messages rechargés des JSONL natifs — piège realpath
   résolu), ChatPanel riche (markdown + wikilinks cliquables, thinking/tool calls repliables,
   carte d'approbation avec DIFF, historique, usage tokens), drag & drop → `_boîte/`.
   `npm run smoke:range` VERT = scénario CONCEPT §12.4 de bout en bout (image rangée, page
   créée avec embed, approbations, reprise de session). ⚠️ Vigilance ouverte : couverture des
   approbations Write à auditer (un run a vu des Write non gatés — voir task_plan).
   **Phase 3 (intelligence) LIVRÉE aussi (2026-06-11)** : initialisation du coffre aux
   conventions v1 réelles (CLAUDE.md d'adjoint v2 — sans Obsidian, propose-puis-applique =
   cartes d'approbation —, Cahier-maître, `.note-ai/` carte/mémoire/journal/index/gabarits,
   Gens/_moi), non destructive ; boutons « Range la boîte » / « Où en suis-je ? » ; vue
   Tâches (retard/à venir, clic → page). `npm run smoke:vault` VERT — la preuve forte :
   « Range la boîte. » a produit slug + frontmatter + réécriture + _projet.md + index IA +
   carte + journal, par conventions seules. Leçon durcie dans le CLAUDE.md de coffre :
   la boîte se liste TOUJOURS sur disque (l'agent croyait la carte périmée).
   **Phase 4 (filet de sécurité) LIVRÉE aussi (2026-06-12)** : Git silencieux via
   isomorphic-git (`.git` HORS du coffre dans userData — le piège iCloud du plan —, commits
   auto débouncés 30 s + après chaque tour d'agent, jamais de push), panneau « ⏪ Historique »
   par page avec restauration (commit de sûreté préalable), recherche full-text MiniSearch
   dans la sidebar (< 1 ms), modal Réglages ⚙ (modèle, permissions avec avertissement yolo,
   chemin CLI, env vars). `npm run smoke:git` VERT.
   **Reste humain** : test visuel (`npm run dev`) + test sur Windows.
   Ensuite : Phase 5 (distribution : electron-builder .dmg/NSIS, CI, GitHub Releases) —
   la DERNIÈRE du plan v2.
   ⚠️ Vigilance : le plan v2 cite le §12 du CONCEPT (`_inbox/`, `_index.ai.md`) — à l'exécution,
   prendre les conventions **réelles** de la v1 (`_boîte/`, couche `.note-ai/`, standard fr-CA,
   `plugins/note-ai/references/conventions.md`), qui ont évolué depuis le §12.

## Reprendre sur une machine neuve (le projet)
1. `git clone https://github.com/JoPerron88/Note-AI.git` (ou ouvrir le dossier iCloud).
2. Lire `session-handoff/OUTILLAGE.md` puis ce fichier, puis **`CLAUDE.md`** (l'essentiel) et
   **`CONCEPT.md`** (le concept complet) au besoin.
3. **Pas de build / test / lancement** à ce stade : le projet est au stade concept (Markdown
   uniquement). Le « produit » futur sera un **vault Obsidian + Claude Code interactif +
   conventions** — pas encore construit.
   ⚠️ Le chemin local contient des espaces (`.../Projet Claude Code/Note AI`) — penser à quoter.

## Pièges à connaître
- **`claude -p` (headless) est exclu** : facturé au tarif API depuis le **15/06/2026** (crédit
  séparé hors abonnement). → On pilote Claude via **Claude Code INTERACTIF** (terminal intégré),
  qui reste sur l'abonnement. Vérifié (centre d'aide Claude + ticket GitHub anthropics/claude-code).
- **Obsidian est propriétaire** mais les notes restent du **Markdown brut** → aucun verrouillage
  des données. C'est ce qui a justifié de passer outre la préférence open source.
- **Ollama** = repli local optionnel (hors-ligne, gratuit) si on veut s'affranchir de Claude.
- Le projet vit dans **iCloud Drive** (synchro/sauvegarde automatique, en plus de GitHub).

## Décisions clés & pourquoi
- **Route Obsidian** (vs VSCodium vs app de zéro) : débat à 3 entités (avocat Obsidian, avocat
  VSCodium, arbitre neutre) → **convergence**. Critère décisif = *combien de code l'amateur doit
  écrire* (Obsidian : quasi zéro ; VSCodium : extension TypeScript). Open source quasi neutre car
  données = Markdown libre. **Logseq écarté** (modèle outliner trop loin de OneNote).
- **Moteur IA = Claude Code interactif** (abonnement), Ollama en repli ; **pas l'API payante** (ferme).
- **Le vrai livrable = un jeu de conventions + un mode d'emploi de Claude**, très peu de code.

## Où trouver le détail
- **`CONCEPT.md`** : tout — vision (§1-7), idées (§8), reconnaissance (§9), arbitrage des 3 routes
  + verdict du débat (§10), fonctions Obsidian exploitées (§11), **concept concret : vault,
  conventions, scénario, scope V1 (§12)**.
- **`.multivac/goal.md`** : le cap (FinalGoal) en version courte.
