# Guide des commandes — jorgo-ai-framework

Référence pratique de toutes les commandes disponibles, le temps de prendre le framework en main. Ce fichier vit ici, dans le fork — un seul endroit à jour, consultable depuis n'importe quel projet puisque les plugins sont installés globalement (`scope: user`).

## Par où commencer

Dans un projet, la toute première commande à lancer :

```
/jai-context:00-onboard
```

Elle lit le projet, explique où il en est dans le flow, et propose la prochaine étape logique — adapté aux plugins installés. À relancer à tout moment si tu ne sais plus quoi faire ensuite.

Pour une feature de bout en bout sans piloter chaque étape toi-même :

```
/jai-orchestrator:01-sdlc "description de ce que tu veux livrer"
```

Elle enchaîne cadrage → plan (validation obligatoire) → implémentation → tests → commit (validation obligatoire) → revue → PR draft. Pas besoin de connaître les autres commandes pour commencer — celle-ci les orchestre pour toi.

---

## jai-context — connaissance du projet

| Commande | Rôle | Quand l'utiliser |
|---|---|---|
| `/jai-context:00-onboard` | Explique où en est le projet, propose la prochaine étape | Point d'entrée, à chaque fois que tu ne sais pas par où commencer |
| `/jai-context:01-bootstrap` | Imagine et valide l'architecture technique d'un nouveau SaaS (Q&A, comparaison de stacks, audit multi-agent, `INSTALL.md`) | Tout début d'un projet greenfield |
| `/jai-context:02-project-memory` | Initialise/rafraîchit la mémoire du projet | Après un gros changement d'archi, ou périodiquement |
| `/jai-context:03-context-generate` | Génère des artefacts (skills, agents, règles, commandes, hooks, plugins) | Quand tu veux créer un nouveau skill/agent perso pour ce projet |
| `/jai-context:09-mermaid` | Génère des diagrammes Mermaid depuis du markdown | Documentation visuelle |
| `/jai-context:10-learn` | Capture les leçons apprises (conversation ou historique git) et les route vers mémoire/décision/règle/skill | En fin de tâche, pour capitaliser |
| `/jai-context:11-explore` | Explore le projet (tooling, contexte, code) et pointe vers ce qui correspond le mieux à un objectif | Pour se repérer dans un projet inconnu |
| `/jai-context:12-cook` | Gère des "recettes" projet (liste, recherche, création, application) | Procédures répétitives documentées |

---

## jai-dev — transformation de code

Pipeline typique : `plan` → `implement` → `assert` → `review`/`test` → (`refactor`/`debug` au besoin).

| Commande | Rôle | Quand l'utiliser |
|---|---|---|
| `/jai-dev:01-plan` | Transforme une demande/ticket/fichier en plan d'implémentation phasé | Avant tout développement non trivial |
| `/jai-dev:02-implement` | Exécute un plan phase par phase jusqu'à complétude | Après validation du plan |
| `/jai-dev:03-assert` | Vérifie que le travail fonctionne (assertions générales, conformité archi, UI) | Après implémentation |
| `/jai-dev:04-audit` | Audit read-only en 7 axes qualité, rapport classé | Diagnostic de dette technique |
| `/jai-dev:05-review` | Revue d'un diff sur 3 axes : qualité code, comportement vs plan, pertinence | Avant de livrer un changement |
| `/jai-dev:06-test` | Écrit et itère des tests jusqu'à ce qu'ils passent, ou valide un parcours utilisateur en navigateur | Ajout de couverture, validation E2E |
| `/jai-dev:07-refactor` | Améliore le code (nettoyage, perf, sécurité, archi) | Amélioration ciblée, pas pour ajouter des tests |
| `/jai-dev:08-debug` | Reproduit et corrige un bug via hypothèses et TDD | Bug identifié ou cause inconnue |
| `/jai-dev:09-for-sure` | Boucle autonome jusqu'à une condition de succès vérifiable — **ne committe/pousse jamais seule**, un commit interactif unique à la fin | Tâche longue à faire "tourner" sans supervision constante |
| `/jai-dev:10-todo` | Découpe une demande en todos indépendants, exécute en parallèle | Demandes multi-parties indépendantes |
| `/jai-dev:11-browser-qa` | Enregistre de courtes vidéos QA d'un parcours navigateur | Preuve de non-régression visuelle |

---

## jai-vcs — opérations git/plateforme

| Commande | Rôle | Quand l'utiliser |
|---|---|---|
| `/jai-vcs:00-repo-init` | Initialise un repo (git init, branche par défaut, commit bootstrap **avec confirmation**, `CONTRIBUTING.md`, remote optionnel) | Tout début d'un nouveau repo |
| `/jai-vcs:01-commit` | Commit avec message conventionnel — **mode interactif par défaut**, confirme avant de committer | Après chaque unité de travail cohérente |
| `/jai-vcs:02-pull-request` | Crée une PR/MR en draft depuis la branche courante | Branche prête à être revue |
| `/jai-vcs:03-release-tag` | Tag semver annoté + notes de release — demande toujours validation avant de tagger | Moment de release |
| `/jai-vcs:04-issue-create` | Crée une issue dans l'outil de ticketing configuré — attend toujours ton approbation avant création | Signaler un bug/besoin |

---

## jai-pm — gestion produit

| Commande | Rôle | Quand l'utiliser |
|---|---|---|
| `/jai-pm:01-ticket-info` | Récupère et affiche les infos d'un ticket | Contexte rapide sur un ticket existant |
| `/jai-pm:02-user-stories` | Découpe et affine des User Stories ordonnées | Backlog produit |
| `/jai-pm:03-prd` | Génère un PRD structuré | Nouvelle feature majeure |
| `/jai-pm:04-spec` | Génère/affine une spec (contrat immuable qu'un plan consomme) | Avant `/jai-dev:01-plan` sur une feature ambiguë |
| `/jai-pm:05-spike` | Enregistre/investigue une incertitude bloquant l'estimation | Question technique ouverte |
| `/jai-pm:06-product-brief` | Produit un Product Brief basé sur preuves | Cadrage produit |
| `/jai-pm:07-epic` | Cadre et gère un Epic orienté résultat | Regroupement de features |
| `/jai-pm:08-three-amigos` | Évalue un Epic/Story sous 3 angles (produit, delivery, qualité) | Avant de valider un refinement |
| `/jai-pm:09-defect` | Enregistre, évalue, vérifie un écart produit observé | Bug côté produit (pas côté code) |
| `/jai-pm:10-task` | Enregistre/gère une tâche technique ou fonctionnelle bornée | Travail délimité, hors Epic |

---

## jai-orchestrator — orchestration

| Commande | Rôle | Quand l'utiliser |
|---|---|---|
| `/jai-orchestrator:01-sdlc` | Orchestre tout : cadrage → plan (validation) → livraison → commit (validation) → revue indépendante → PR draft | Livrer une feature de bout en bout |
| `/jai-orchestrator:02-backlog` | Route intake/triage/refinement/lifecycle/revue sur le backlog produit | Gestion globale du backlog |
| `/jai-orchestrator:00-async-dev` | Pipeline bot asynchrone sur issues/PR GitHub (setup/run/review) | **Non utilisé pour l'instant** — laissé de côté volontairement |

---

## jai-refine — méta-cognition

| Commande | Rôle | Quand l'utiliser |
|---|---|---|
| `/jai-refine:01-brainstorm` | Clarifie une intention floue par découverte progressive | Idée pas encore assez précise pour agir |
| `/jai-refine:02-challenge` | Recontrôle un travail déjà fait par rapport au plan validé | Après une implémentation, avant de considérer que c'est fini |
| `/jai-refine:03-shadow-areas` | Scanne un artefact écrit pour trouver les angles morts | Relecture de spec/PRD avant validation |
| `/jai-refine:04-fact-check` | Vérifie des affirmations factuelles contre des sources, cite ou nuance | Contenu qui cite des faits externes |

---

## devlog — journal de développement (plugin invité)

Pas un `jai-*` — plugin distinct d'un collègue (Ibra, 41Devs), inclus avec son autorisation. Voir [`plugins/devlog/README.md`](plugins/devlog/README.md).

| Commande | Rôle | Quand l'utiliser |
|---|---|---|
| `devlog` (automatique) | Journalise en continu les changements significatifs | Toujours actif, pas d'invocation manuelle nécessaire |
| `/log` | Force une entrée manuelle dans le journal | Changement que tu veux documenter explicitement |
| `/journal-index` | Régénère la table des matières du journal | Après un signal du hook, ou à la demande |
| `/rapport` | Génère un rapport journalier complet | Fin de journée, partage d'avancement |
| `/todo` | Liste les tâches en attente issues du journal | Reprise de contexte |

---

## Non installés (à la demande seulement)

- `jai-ui` — alpha, un seul skill smoke-test, pas encore de vraies capacités UI/UX.
- `jai-telemetry` — suivi coût/usage, volontairement opt-in (données personnelles).

```
claude plugin install jai-ui@jorgo-ai-framework
claude plugin install jai-telemetry@jorgo-ai-framework
```

## Points de vigilance déjà corrigés dans ce fork

- `01-sdlc` et `09-for-sure` ne committent/poussent jamais sans validation explicite (corrigé par rapport à l'original `ai-driven-dev/framework`).
- `00-repo-init` demande confirmation même pour son commit bootstrap vide.
- Tous les autres skills touchant à un artefact visible (PR, issue, tag) demandaient déjà confirmation nativement.
