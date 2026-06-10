# FinalGoal — Note AI

**Ce que c'est :** Un carnet de notes personnel « façon OneNote augmenté à l'IA », 100 % local,
construit **sur Obsidian** — Notebooks › Sections › Pages = dossiers / fichiers Markdown. Un
assistant **Claude (Claude Code interactif dans le terminal intégré)** range, réécrit, retrouve
et suit les projets, en s'appuyant sur une couche d'index optimisée pour économiser les tokens.

**Pour qui / dans quel contexte :** Un seul utilisateur — concepteur mécanique, développeur
amateur — sur **Windows + Mac**, données dans un dossier synchronisé sur le cloud. Usage : prise
de notes technique (formules incluses) + suivi de projets.

**« Réussi » signifie concrètement :** Je dépose n'importe quoi (texte, PDF, capture) et je dis
à Claude « range ça dans tel projet » ; en quelques secondes c'est **classé à la bonne place,
réécrit proprement, indexé**, et je peux demander un résumé ou une référence **sans qu'il relise
tout**. Je consulte et modifie mes pages **à la main aussi naturellement que via le chat** (double
accès, mêmes fichiers Markdown). Cahier maître, cahiers de projet et tâches/échéances vivent dans
le même vault.

## Contraintes à ne jamais perdre de vue

- **Local d'abord** : données chez l'utilisateur ; sauvegarde + historique (Git en coulisse).
- **PAS l'API payante Claude.** Pilotage via **Claude Code interactif** (sur l'abonnement) ;
  **Ollama** en repli local. Le mode headless `claude -p` est exclu (facturé au tarif API depuis
  le 15/06/2026).
- **Double accès** : notes en Markdown lisibles et modifiables à la main ET par l'IA, sur les
  mêmes fichiers. Maths **LaTeX inline** mélangées au Markdown.
- **Couche machine optimisée tokens** : `_index.ai.md` par notebook + liens `[[…]]`, pour que
  l'IA se repère sans tout relire.
- **Open source préféré** ; Obsidian (propriétaire) toléré car les données restent du Markdown
  brut, non verrouillées.
- **Windows + Mac** ; mono-utilisateur ; multi-appareils via dossier cloud synchronisé.
- **Ne pas réinventer OneNote** : orchestrer Claude + des conventions sur les briques Obsidian
  existantes (dossiers, liens/backlinks, tags, propriétés YAML, Dataview, Tasks, terminal).

- **Autosuffisance** (ajouté 2026-06-10) : Note AI = un **plugin Claude Code** qui se suffit à
  lui-même — aucune dépendance à d'autres skills/plugins Claude Code, outils natifs seulement.
  Installable depuis GitHub sur toute machine (mac/win/linux), dans n'importe quel coffre.

## Statut

Direction arrêtée le 2026-06-10 (débat à 3 entités convergent → Route Obsidian). Maquette livrée
(`maquette/`). **V1 construite le 2026-06-10** : le dépôt est un marketplace Claude Code, le
plugin vit dans `plugins/note-ai/` (skill + conventions + templates ; bootstrap automatique d'un
coffre, `CLAUDE.md` déposé = adjoint par défaut). Terrain d'usage : Claude Code interactif dans
Claude sidebar (Obsidian). Prochaine étape : test réel par l'utilisateur, puis itérations.
