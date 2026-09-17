← [jorgo-ai-framework](../../README.md)

# devlog

Journal de développement automatique — pas un plugin `jai-*` maison, celui-ci vient d'ailleurs.

> Originellement créé par **Ibra (41Devs)** — [Estime229/devlog-plugin](https://github.com/Estime229/devlog-plugin). Inclus ici avec son autorisation. Tout le crédit du design revient à lui ; cette copie vit dans ce fork pour que quiconque récupère `jorgo-ai-framework` l'ait aussi, sans installation séparée.

## Ce que ça fait

Journalise automatiquement les changements significatifs (feature, bug, refactor, chore) dans un journal Markdown, avec un seuil anti-bruit — les micro-changements (typo, formatting) ne créent pas d'entrée.

- Écrit dans `.claude/session-log.md` s'il existe déjà dans le projet (compatible avec la convention perso `context.md`/`TASKS.md`/`DECISIONS.md`/`PATTERNS.md`/`ERRORS.md` — voir [`personal-setup/`](../../personal-setup/)), sinon dans `.claude/journal/CHANGELOG.md`.
- Un hook `Stop` surveille le nombre d'entrées et signale quand régénérer l'index.

## Skills et commandes

| Commande | Rôle |
|---|---|
| `devlog` (skill automatique) | Journalise en continu, sans intervention |
| `/log` | Force une entrée manuelle |
| `/journal-index` | Régénère la table des matières du journal |
| `/rapport` | Génère un rapport journalier (dev, projet, branche, blocages, fichiers modifiés, reste à faire) |
| `/todo` | Liste les tâches en attente issues du journal |

## Licence

Le dépôt d'origine n'a pas de licence formelle au moment de cette intégration. Inclus ici sur la base de l'autorisation directe de l'auteur — si tu récupères ce fork et que tu veux redistribuer ce plugin spécifiquement au-delà d'un usage personnel, vérifie d'abord avec [Ibra / Estime229](https://github.com/Estime229).
