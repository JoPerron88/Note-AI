# Handoff — Note AI
> Dernière mise à jour : 2026-06-10. Reprise à froid : si tu n'as pas l'outillage de ce projet,
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
- Contexte d'usage : l'utilisateur a installé **Obsidian + Claude sidebar** (Claude Code
  interactif dans Obsidian) — c'est le terrain de test réel.

## Ce qui était prévu ensuite
1. **Test réel** : installation via `/plugin marketplace add JoPerron88/Note-AI` +
   `/plugin install note-ai@note-ai` dans Claude sidebar, init d'un coffre, scénarios du
   concept (« range ça », « où en suis-je »…). Les ratés observés = matière du REFACTOR
   (le skill n'a pas eu de tests sous-agents — le test réel en tient lieu).
2. Itérations sur le skill selon les retours ; « plus tard » du §12.6 (Ollama, automatisations).

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
