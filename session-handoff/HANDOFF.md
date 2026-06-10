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
- **Stade = CONCEPTION.** Aucun code, aucun vault Obsidian construit pour l'instant — uniquement
  les documents de concept.
- ✅ **`CLAUDE.md` créé à la racine** (2026-06-10) : instructions projet pour les futures
  sessions — décisions arrêtées, conventions du vault, carte des documents.

## Ce qui était prévu ensuite
Deux pistes en attente (dans l'ordre logique) :
1. **La maquette** — passer du texte à un visuel de l'interface (le vault, le terminal-chat, le
   flux « drop → range »).
2. **Scope V1** puis construction — voir `CONCEPT.md` §12.6 (périmètre V1 déjà ébauché).

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
