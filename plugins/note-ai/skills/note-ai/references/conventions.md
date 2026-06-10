# Conventions Note AI — la référence

> Distillé de `CONCEPT.md §12` du projet Note AI. C'est le contrat entre
> l'humain et l'adjoint : les deux naviguent le coffre avec les mêmes règles.

## 1. Structure du coffre

```
<Coffre>/                          ← n'importe quel coffre Obsidian
├─ CLAUDE.md                       ← l'adjoint par défaut (généré à l'init)
├─ Cahier-maître.md                ← vue d'ensemble de TOUS les projets
├─ _inbox/                         ← dépôt brut, zéro réflexion ; trié sur demande
├─ Projets/
│  ├─ <Notebook>/                  ← un NOTEBOOK par projet (ex. Maison)
│  │  ├─ _projet.md                ← cahier de projet : objectif, statut, échéances
│  │  ├─ _index.ai.md              ← index condensé GÉNÉRÉ (couche machine)
│  │  ├─ <Section>/                ← une SECTION par thème (ex. Cuisine)
│  │  │  ├─ AAAA-MM-JJ-slug.md     ← les PAGES
│  │  │  └─ captures/              ← images & pièces jointes de la section
└─ .obsidian/                      ← config Obsidian (ne jamais y toucher)
```

- **Notebook** = dossier direct sous `Projets/`. **Section** = sous-dossier.
  **Page** = fichier `.md`. Sections imbriquées permises mais 1 niveau suffit
  en général.
- Les fichiers `_*` (underscore) sont l'outillage : jamais comptés comme pages.

## 2. Nommage

- Pages : `AAAA-MM-JJ-slug.md` — date du jour de création, slug court en
  minuscules avec tirets (ex. `2026-06-10-plan-cuisine.md`).
- Notebooks/Sections : noms humains capitalisés (`Maison`, `Cuisine`).
- Images rangées : renommer en slug parlant (`plan-v2.png`), jamais garder
  `IMG_4521.png` ou `capture-….png`.

## 3. Frontmatter de page (obligatoire)

```yaml
---
titre: Plan cuisine
projet: Maison/Cuisine          # Notebook/Section
date: 2026-06-10
statut: en-cours                # à-faire | en-cours | en-pause | terminé
tags: [cuisine, structure]
resume: Calcul de la poutre porteuse + relevé des dimensions.
---
```

Le `resume:` (une ligne) est la matière première de l'index — le soigner.

## 4. `_index.ai.md` — la couche machine (généré)

Un par notebook. Format strict, une ligne par page :

```markdown
# Index IA — Notebook <Nom>   (généré par Note AI, ne pas éditer à la main)
- <Section>/<fichier>.md — <resume> [<tags>] (<statut>)
- Cuisine/captures/plan-v2.png — IMAGE : plan révisé de la poutre
```

- **Lire l'index d'abord, toujours** : c'est lui qui dit où aller sans tout
  relire. Les images y figurent avec leur légende (préfixe `IMAGE :`).
- **Régénérer à chaque écriture** dans le notebook (création, déplacement,
  changement de statut/resume). Source de vérité = les frontmatters des pages :
  en cas de doute, reconstruire l'index entier depuis les frontmatters.

## 5. Protocole `_inbox/`

1. L'utilisateur dépose n'importe quoi (texte, PDF, image) — aucune règle.
2. Sur « range ça / range l'inbox » : pour chaque élément, **proposer**
   destination + nouveau nom + (si texte) la réécriture, **attendre le OK**,
   puis exécuter : déplacer, créer/mettre à jour la page, lier, régénérer
   l'index. L'inbox finit vide.
3. Élément inclassable → demander (une fois) ou créer la page dans le notebook
   le plus plausible avec `statut: à-classer`.

## 6. Images et pièces jointes — pas d'OCR

- On **range**, on ne lit pas : jamais d'OCR, jamais de description du contenu.
- Chaque image rangée reçoit une **légende d'une ligne** (fournie par
  l'utilisateur ou déduite du contexte de la demande), stockée :
  dans la page qui l'embarque (`![[captures/plan-v2.png]]` + légende en
  dessous) ET dans `_index.ai.md`.
- Une image sans légende est introuvable — ne jamais ranger sans légende.

## 7. Tâches et échéances

- Format standard : `- [ ] Faire X 📅 AAAA-MM-JJ` dans les pages.
- L'adjoint sait : les lister par projet, trier par échéance, signaler les
  retards (grep `- [ ]` sur le notebook, comparer à la date du jour).

## 8. Liens

- `[[wikilinks]]` entre pages liées — l'adjoint pose les liens pertinents à la
  création/rangement (la cible affiche le backlink automatiquement côté
  Obsidian).
- Tout déplacement/renommage → grep l'ancien nom et corriger les liens.

## 9. `Cahier-maître.md` — le tableau de bord

- Table des projets : nom, statut, prochaine échéance, tâches ouvertes +
  section « Activité récente » (5 dernières actions de rangement).
- **Si l'utilisateur a les plugins Obsidian Dataview/Tasks** : les blocs de
  requête du template font le travail tout seuls.
- **Sinon (autosuffisance)** : l'adjoint maintient la table statique à la main,
  à chaque changement de statut/échéance. Le template contient les deux —
  ne supprimer ni l'un ni l'autre.

## 10. `_projet.md` — le cahier de projet

Objectif du projet, statut global, jalons/échéances, décisions notables.
Mis à jour quand le projet évolue ; lu (avec l'index) pour répondre à
« où en suis-je ». Template : `templates/projet.md`.
