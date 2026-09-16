# Règles globales

## Communication
- Réponses courtes et directes. Zéro remplissage, zéro récapitulatif de fin non demandé.
- Un seul sujet à la fois. Si ambiguïté, une question précise avant d'agir.
- (Adapte la langue de réponse à la tienne — ceci est un exemple en français.)

## Avant de coder
- **Toujours discuter et valider le plan** avant d'écrire du code. Pas d'exception.
- Si l'intention est floue, reformuler et demander confirmation.

## Pendant le développement
- Ne jamais affirmer qu'un fix fonctionne sans l'avoir testé.
- Tester **avant** le fix (reproduire/observer le bug) et **après** (confirmer la correction).
- Ne jamais casser un flow existant — toute régression est inacceptable.
- Modifier les fichiers existants de préférence, pas créer de nouveaux inutilement.

## Protocole de test (principe universel)
- Toujours écrire : tests unitaires + tests feature/intégration + tests manuels (méthode selon la stack).
- La méthode exacte est définie dans le `CLAUDE.md` du projet (généré par ton skill d'init, ou écrit à la main).
  - API Node/NestJS → `jest` + `curl` sur localhost
  - Laravel → `php artisan test` / Pest (feature tests = équivalent curl)
  - Front React/Vue → `vitest` + Playwright/Cypress si E2E disponible
  - Full-stack (front+back) → protocole séparé pour chaque couche

## Git — règle absolue
- **Ne jamais exécuter `git commit` ni `git push`** — l'utilisateur décide seul quand committer.
- Proposer les messages au format Conventional Commits, attendre validation.
- Si tu ajoutes une règle d'attribution (co-auteur, signature), documente-la ici explicitement — ne compte pas sur un défaut implicite.

## Économie de tokens — règle de lecture

En début de session, lire dans cet ordre et s'arrêter dès que le contexte est suffisant :
1. `.claude/context.md` si présent → remplace le scan du projet (stack, modules, conventions)
2. `.claude/session-log.md` si présent → où on s'est arrêtés
3. `CLAUDE.md` du projet → règles stack-spécifiques
4. `TASKS.md` → tâches en cours

Ne jamais re-scanner tout le code source si ces fichiers existent.
Faire des lectures ciblées (fichier précis, ligne précise) plutôt que des explorations larges.

## Architecture préférée (à détecter, pas à imposer)

Exemple d'organisation qu'on peut préférer :
- **NestJS** : CQRS (CommandBus/QueryBus NestJS), modules avec `commands/`, `queries/`, `handlers/`, `helpers/`, `enums/` centralisés dans un dossier `shared/`
- **Laravel** : CQRS custom (Bus maison), modules avec `Commands/`, `Queries/`, `Handlers/`, `DTOs/`, `Enums/`, couche `Shared/` globale (Bus, Helpers, Traits, Exceptions)

Si cette structure est détectée dans un projet → la noter dans `.claude/context.md` et respecter le pattern.
Si le projet n'a pas encore cette structure → proposer uniquement si pertinent, ne pas imposer.

## Fichiers de contexte du projet (si présents)
- `.claude/context.md` — carte du projet, lu en priorité
- `.claude/session-log.md` — historique des sessions
- `.claude/architecture.md` — avant toute modification structurelle
- `.claude/audit.md` — avant tout travail sécurité/qualité
- `CLAUDE.md` — règles stack-spécifiques du projet
- `TASKS.md` — tâches en cours
- `DECISIONS.md` — avant tout choix d'archi
- `ERRORS.md` — avant tout debugging

## Sub-agents disponibles partout
- **reviewer** — relecture code post-modification
- **testeur** — écriture et maintenance des tests
- **architecte** — décisions structurelles, nouveaux modules

Définitions dans [`agents/`](agents/) — copie ces fichiers dans `~/.claude/agents/` pour les activer.

## Outil complémentaire : RTK

[RTK (Rust Token Killer)](https://www.rtk-ai.app/fr/) est un CLI open-source (Apache 2.0, gratuit, sans compte ni clé API) qui compresse les sorties de commandes avant qu'elles n'atteignent le contexte de l'agent — jusqu'à 90% de bruit en moins sur les sorties CLI verbeuses (git, build, tests). Une fois installé, un hook Claude Code réécrit les commandes shell courantes pour passer par `rtk` automatiquement. Voir [`RTK.md`](RTK.md) pour les commandes de base, et le site officiel pour l'installation.
