# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Ce qu'est ce dépôt

**Note AI** : un carnet de notes personnel « OneNote augmenté à l'IA », 100 % local, construit
**sur Obsidian** (Notebooks › Sections › Pages = dossiers / fichiers Markdown), où **Claude Code
interactif** (dans le terminal intégré d'Obsidian) range, réécrit, retrouve et suit les projets.

**Stade actuel : CONCEPTION.** Le dépôt ne contient que des documents Markdown — aucun code,
aucun build, aucun test, aucun vault Obsidian construit. Ne pas chercher de commandes de
développement : il n'y en a pas.

Tout le travail se fait **en français** (documents, commits, échanges).

## Carte des documents (où trouver quoi)

- **`CONCEPT.md`** — le document de référence. Vision (§1-7), idées (§8), recherche (§9),
  arbitrage des 3 routes (§10), briques Obsidian exploitées (§11), **concept concret : structure
  du vault, conventions, scénario d'usage, périmètre V1 (§12)**.
- **`.multivac/goal.md`** — le cap (FinalGoal) en version courte, avec les contraintes fermes.
- **`session-handoff/HANDOFF.md`** — état exact du projet et prochaine étape. **À lire en début
  de session de reprise, et à mettre à jour en fin de session de travail significative.**
- **`session-handoff/OUTILLAGE.md`** — plugins/skills utilisés (Multivac, superpowers… —
  facultatifs pour avancer).

## Décisions arrêtées (ne pas rouvrir sans demande explicite)

Ces arbitrages ont été tranchés le 2026-06-10 après recherche et débat (détail : `CONCEPT.md` §9-10) :

1. **Route Obsidian** (vs VSCodium vs app de zéro). Critère décisif : quasi zéro code à écrire.
   Obsidian est propriétaire mais les données restent du Markdown brut → pas de verrouillage.
   Logseq écarté (modèle outliner trop loin de OneNote).
2. **Moteur IA = Claude Code interactif** (sur l'abonnement). **`claude -p` / headless / Agent
   SDK sont EXCLUS** : facturés au tarif API depuis le 15/06/2026, ce qui contredit la contrainte
   ferme « pas d'API payante ». Ne jamais proposer une architecture qui repose sur l'usage
   programmatique de Claude. Ollama = repli local optionnel (plus tard, pas V1).
3. **Le vrai livrable = un jeu de conventions + un mode d'emploi de Claude**, très peu de code.
   Ne pas réinventer ce qu'Obsidian fournit déjà (dossiers, liens/backlinks, tags, frontmatter,
   Dataview, Tasks, terminal intégré).
4. **Structure OneNote non négociable** : Notebooks › Sections › Pages, double accès à parts
   égales (édition à la main ET via le chat, sur les mêmes fichiers).

## Conventions du futur vault (référence : CONCEPT.md §12)

Tout artefact produit pour le vault doit respecter ces conventions, déjà fixées :

- Arborescence : `_inbox/` (capture brute), `Projets/<Notebook>/<Section>/<page>.md`,
  `Cahier-maître.md` (Dataview), `_projet.md` et `_index.ai.md` par notebook.
- Pages : frontmatter YAML (`titre`, `projet`, `date`, `statut`, `tags`, `resume`) ; nommage
  `AAAA-MM-JJ-slug.md` ; tâches en `- [ ] … 📅 AAAA-MM-JJ` ; LaTeX inline autorisé.
- `_index.ai.md` : index condensé généré (une ligne par page : chemin — résumé [tags] (statut)),
  que Claude lit **à la place** du contenu complet → économie de tokens.
- Images : rangées + légendées au drop, **pas d'OCR**.
- Mode « propose puis applique » : Claude montre ses rangements avant de les exécuter.

## Notes pratiques

- ⚠️ Le chemin local contient des espaces (`…/Projet Claude Code/Note AI`) — **toujours quoter**
  dans les commandes shell.
- Le dépôt vit dans iCloud Drive (synchro auto) ET sur GitHub (`JoPerron88/Note-AI`).
- Prochaines étapes prévues (ordre logique) : maquette de l'interface, puis scope V1 et
  construction du vault (périmètre déjà ébauché dans `CONCEPT.md` §12.6).
