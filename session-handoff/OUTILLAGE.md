# Outillage — Note AI
> Lis ceci EN PREMIER si tu reprends sur une machine neuve, avant de connaître le projet.

## Plugins / skills Claude Code utilisés sur ce projet

- **superpowers** (plugin, marketplace officiel) — méthodes de travail (brainstorming, plans, TDD).
  Disponible mais peu sollicité directement ici (le projet est passé par Multivac).
  Installer : `/plugin marketplace add claude-plugins-official`
  puis `/plugin install superpowers@claude-plugins-official`.

- **Multivac** (skill **personnel**, `~/.claude/skills/multivac/`) — l'orchestrateur qui a piloté
  toute la conception (analyse → casting de sous-agents → débat → synthèse). C'est lui qui écrit
  le dossier `.multivac/` (dont `goal.md`, le cap). **Skill perso, pas un marketplace public** :
  pour le retrouver sur une machine neuve, il faut **recopier le dossier du skill dans
  `~/.claude/skills/`** depuis ta propre sauvegarde — il n'y a pas d'URL d'install publique.

- **newproject** et **session-handoff** (skills **personnels**, `~/.claude/skills/`) — amorçage du
  projet et préparation de la reprise (ce dossier). Même remarque : skills perso, à recopier dans
  `~/.claude/skills/` depuis ta sauvegarde.

## Repli — si tu n'installes pas l'outillage
Tu peux continuer sans rien de tout ça : **c'est un dépôt git normal**, et tout le contenu utile
est en **Markdown brut, lisible sans aucun plugin**. Lis `CONCEPT.md` (le concept complet) et
`.multivac/goal.md` (le cap) directement. Les skills ci-dessus ne faisaient qu'**organiser** le
travail — ils ne sont pas nécessaires pour comprendre le projet ni pour avancer à la main en
suivant les conventions décrites dans `CONCEPT.md` §12.

## Puis
Lis `HANDOFF.md` (à côté) pour l'état exact et la prochaine étape.
