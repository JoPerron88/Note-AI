# Maquette — Note AI

> Maquette visuelle du concept (stade conception, 2026-06-10). **Source de vérité des
> conventions : `CONCEPT.md` §12.** Ce fichier est la référence versionnée ; le rendu
> navigateur vit dans `maquette.html` (même contenu, en plus évocateur).
>
> Quatre vues : la fenêtre Obsidian complète · le flux « drop → range » · le
> cahier-maître · une page type en détail.

---

## Vue 1 — La fenêtre Obsidian complète

Tout Note AI tient dans une seule fenêtre : l'arborescence du vault à gauche
(Notebooks › Sections › Pages), la page rendue au centre, et **Claude Code interactif
dans le terminal intégré en bas** — le chat-adjoint, sur l'abonnement.

```
┌──────────────────────────────────────────────────────────────────────────────┐
│ ● ● ●   Note-AI-Vault — Obsidian                                             │
├──────────────────────┬───────────────────────────────────────────────────────┤
│ EXPLORATEUR          │  Plan cuisine                                         │
│                      ├───────────────────────────────────────────────────────┤
│ Cahier-maître        │  titre  : Plan cuisine       statut : en-cours        │
│ _inbox (1)           │  projet : Maison/Cuisine     tags   : cuisine, struct │
│ ▾ Projets            │ ───────────────────────────────────────────────────── │
│   ▾ Maison           │                                                       │
│      _projet.md      │  # Plan cuisine                                       │
│      _index.ai.md    │                                                       │
│     ▾ Cuisine        │  Poutre porteuse, charge répartie q sur longueur L.   │
│        2026-06-10-…  │  Flèche maximale :                                    │
│        devis-armoi…  │               5 · q · L⁴                              │
│        captures/     │      δmax = ─────────────         ← LaTeX rendu       │
│     ▸ Jardin         │               384 · E · I                             │
│   ▸ Atelier          │                                                       │
│                      │  ┌────────────────────────┐                           │
│                      │  │  [image : plan-v2.png] │     ← embed ![[…]]        │
│                      │  └────────────────────────┘                           │
│                      │                                                       │
│                      │  [ ] Valider la section IPN — échéance 2026-06-20     │
│                      │  Voir aussi [[devis-armoires]]                        │
├──────────────────────┴───────────────────────────────────────────────────────┤
│ TERMINAL — Claude Code interactif (sur l'abonnement, jamais headless)        │
│                                                                              │
│ ❯ range la dernière capture dans Maison/Cuisine, c'est le plan révisé       │
│                                                                              │
│ ⏺ Je propose :                                                              │
│    1. déplacer _inbox/capture-2026-06-10-1432.png                           │
│       → Projets/Maison/Cuisine/captures/plan-v2.png                         │
│    2. mettre à jour « Plan cuisine » (légende + lien — pas d'OCR)           │
│    3. régénérer _index.ai.md                                                │
│    OK ? (o/n)                                                               │
│                                                                              │
│ ❯ o                                                                          │
│ ✓ Rangé. 1 image, 1 page mise à jour, index régénéré (3 entrées).           │
└──────────────────────────────────────────────────────────────────────────────┘
```

**À lire dans cette vue :**
- Le **double accès** : la page du centre s'édite à la main, ET Claude la modifie
  depuis le terminal — *mêmes fichiers Markdown*.
- `_inbox (1)` : une capture attend d'être rangée (vue 2).
- `_index.ai.md` visible dans l'arbre : la couche machine vit *dans* le vault.
- Le mode **« propose puis applique »** : Claude montre son plan avant d'agir.

---

## Vue 2 — Le flux « drop → range » (storyboard)

Le scénario cœur du concept (`CONCEPT.md` §12.4) : capturer sans réfléchir,
ranger à froid en langage naturel.

```
  ÉTAPE 1 — CAPTURER (zéro réflexion)
┌────────────────────────────────────────────────┐
│  Réunion chantier : tu photographies le plan   │
│  annoté, puis tu le glisses dans la boîte.     │
│                                                │
│    plan-annoté.jpg  ── drag & drop ──▶ _inbox/ │
│                                                │
│  _inbox/                                       │
│  └─ capture-2026-06-10-1432.png         (1)    │
└────────────────────────────────────────────────┘
                        │
                        ▼
  ÉTAPE 2 — ORDONNER (langage naturel, terminal)
┌────────────────────────────────────────────────┐
│ ❯ range la dernière capture dans               │
│   Maison/Cuisine, c'est le plan révisé         │
│   de la poutre                                 │
└────────────────────────────────────────────────┘
                        │
                        ▼
  ÉTAPE 3 — PROPOSER PUIS APPLIQUER (confiance)
┌────────────────────────────────────────────────┐
│ ⏺ Je propose :                                 │
│   • déplacer + renommer → captures/plan-v2.png │
│   • légende : « plan révisé de la poutre »     │
│     (pas d'OCR — on range, on ne lit pas)      │
│   • lier depuis [[2026-06-10-plan-cuisine]]    │
│   • régénérer _index.ai.md                     │
│   OK ?                              ❯ o        │
└────────────────────────────────────────────────┘
                        │
                        ▼
  ÉTAPE 4 — RÉSULTAT (classé, lié, indexé)
┌────────────────────────────────────────────────┐
│ Projets/Maison/Cuisine/                        │
│ ├─ 2026-06-10-plan-cuisine.md    ← mise à jour │
│ └─ captures/plan-v2.png          ← rangée      │
│                                                │
│ _index.ai.md régénéré  ·  _inbox/ vide (0)     │
│ (Git versionne tout, en silence)               │
└────────────────────────────────────────────────┘
```

Quelques secondes du début à la fin. La capture est instantanée, le rangement se
fait quand *tu* le décides.

---

## Vue 3 — Le cahier-maître (tableau de bord vivant)

`Cahier-maître.md` n'est pas tenu à la main : c'est une page dont les tables sont
**générées par Dataview** (et les tâches centralisées par le plugin Tasks) à partir
du frontmatter de toutes les pages. Toujours à jour, zéro maintenance.

```
┌───────────────────────────────────────────────────────────────┐
│  Cahier maître — vue d'ensemble                               │
├───────────────────────────────────────────────────────────────┤
│                                                               │
│  ## Projets                  (table Dataview — générée)       │
│  ┌──────────┬──────────┬─────────────────┬─────────────────┐  │
│  │ Projet   │ Statut   │ Proch. échéance │ Tâches ouvertes │  │
│  ├──────────┼──────────┼─────────────────┼─────────────────┤  │
│  │ Maison   │ en-cours │ 2026-06-20      │ 4               │  │
│  │ Atelier  │ en-pause │ —               │ 2               │  │
│  └──────────┴──────────┴─────────────────┴─────────────────┘  │
│                                                               │
│  ## Tâches en retard           (plugin Tasks — centralisé)    │
│  [ ] Commander l'IPN — 2026-06-08 (Maison/Cuisine)   ⚠ +2 j   │
│                                                               │
│  ## Activité récente                                          │
│  • 2026-06-10 — plan-v2.png rangé dans Maison/Cuisine         │
│  • 2026-06-09 — devis-armoires.md réécrit par Claude          │
│                                                               │
└───────────────────────────────────────────────────────────────┘
```

Et côté chat, la même information sans rien ouvrir :
*« Rappelle-moi où j'en suis sur la cuisine »* → Claude lit `_index.ai.md` +
`_projet.md` (quelques lignes, pas tout le contenu) et répond.

---

## Vue 4 — Une page type, en détail

La page telle qu'elle vit sur disque (`CONCEPT.md` §12.2), annotée. Chaque zone a
un rôle précis dans la mécanique humain + machine.

```markdown
---
titre: Plan cuisine                      ─┐
projet: Maison/Cuisine                    │  frontmatter YAML : la matière
date: 2026-06-10                          │  première de _index.ai.md et
statut: en-cours                          │  des tables Dataview
tags: [cuisine, structure]                │
resume: Calcul de la poutre porteuse      │  ← LA ligne que Claude récolte
        + relevé des dimensions.         ─┘    pour l'index (économie de tokens)
---

# Plan cuisine

Poutre porteuse, charge répartie q sur longueur L. Flèche maximale :

$$\delta_{max} = \frac{5\,q\,L^4}{384\,E\,I}$$    ← LaTeX inline, rendu par Obsidian

![[captures/plan-v2.png]]                          ← image rangée + légendée (pas d'OCR)

- [ ] Valider la section IPN 📅 2026-06-20         ← tâche standard (plugin Tasks)
- Voir aussi [[devis-armoires]]                    ← wikilink (backlink automatique)
```

### La couche machine, vue par Claude (`_index.ai.md`)

Ce que Claude lit **à la place** du contenu complet — trois lignes au lieu de
trois pages :

```markdown
# Index IA — Notebook Maison   (généré par Claude, ne pas éditer à la main)
- Cuisine/2026-06-10-plan-cuisine.md — calcul poutre porteuse + dimensions [cuisine,structure] (en-cours)
- Cuisine/devis-armoires.md — devis 3 fournisseurs [cuisine,devis] (à-faire)
- Jardin/semis-printemps.md — planning + plan de massif [jardin] (terminé)
```

---

## Qui fait quoi (rappel, `CONCEPT.md` §12.5)

| Couche | Dans la maquette |
|---|---|
| **Obsidian** (gratuit) | La fenêtre : arbre, rendu Markdown + LaTeX, Dataview/Tasks, terminal intégré |
| **Claude Code** (abonnement) | Le terminal : comprendre, ranger, réécrire, indexer, résumer |
| **Les conventions** (le livrable) | Tout le reste : `_inbox/`, frontmatter, `_index.ai.md`, nommage, « propose puis applique » |
