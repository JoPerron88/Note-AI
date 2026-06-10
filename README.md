# Note AI

**L'adjoint maître des notes** : un plugin Claude Code qui transforme n'importe
quel coffre Obsidian en carnet façon OneNote (**Notebooks › Sections › Pages**),
piloté en langage naturel — Claude range, réécrit, retrouve et suit tes projets.

- **100 % local, 100 % Markdown** : tes notes restent des fichiers lisibles à la
  main, dans ton coffre. Aucun service tiers, aucune base de données.
- **Autosuffisant** : aucune dépendance à d'autres plugins ou skills Claude
  Code. (Côté Obsidian, Dataview/Tasks sont optionnels — tout fonctionne sans.)
- **Économe en tokens** : Claude lit des index condensés (`_index.ai.md`), pas
  tout le coffre.
- Multi-plateforme : partout où Claude Code tourne (macOS, Windows, Linux).

## Installation (sur n'importe quelle machine)

Dans Claude Code (terminal, ou Claude sidebar dans Obsidian) :

```
/plugin marketplace add JoPerron88/Note-AI
/plugin install note-ai@note-ai
```

Mise à jour plus tard : `/plugin update note-ai`.

## Démarrage (dans n'importe quel coffre)

1. Ouvre une session Claude Code **dans ton coffre Obsidian** (par exemple via
   le terminal intégré / Claude sidebar).
2. Note AI détecte un coffre sans structure et **propose de l'initialiser** —
   tu peux aussi le demander : *« initialise Note AI ici »*. Il crée :
   `CLAUDE.md` (l'adjoint par défaut), `Cahier-maître.md`, `_inbox/`, `Projets/`.
3. Utilise-le en langage naturel :
   - *« crée un projet Maison »*
   - *(tu glisses une photo dans `_inbox/`)* — *« range ça dans Maison/Cuisine,
     c'est le plan révisé de la poutre »*
   - *« où en suis-je sur la cuisine ? »*

Le `CLAUDE.md` déposé dans le coffre se suffit à lui-même : toute session
Claude Code ouverte dans ce coffre devient l'adjoint, même sur une machine où
le plugin n'est pas installé.

## Le dépôt

| Dossier | Contenu |
|---|---|
| `plugins/note-ai/` | **Le produit** : le plugin (skill + conventions + templates) |
| `CONCEPT.md` | Le concept complet (vision, arbitrages, conventions §12) |
| `maquette/` | Maquette de l'interface (`MAQUETTE.md` + `maquette.html`) |
| `session-handoff/` | État du projet et reprise de session |

Conventions détaillées : `plugins/note-ai/skills/note-ai/references/conventions.md`.
