← [jorgo-ai-framework](../README.md)

# personal-setup

Ma configuration Claude Code générale — indépendante des plugins `jai-*` de ce repo. Ce sont les règles et sub-agents que j'utilise sur **tous** mes projets, pas seulement ceux qui installent le marketplace `jorgo-ai-framework`.

> Ce n'est pas un plugin installable via `claude plugin install`. C'est de la configuration brute à copier dans ton dossier `~/.claude/`.

## Ce qu'il y a dedans

- [`CLAUDE.md`](CLAUDE.md) — règles globales : discipline git, protocole de test par stack, "toujours valider le plan avant de coder", organisation de fichiers de contexte projet.
- [`agents/`](agents/) — 3 sub-agents : `reviewer` (relecture code), `testeur` (écriture de tests), `architecte` (décisions structurelles).
- [`RTK.md`](RTK.md) — référence rapide pour [RTK](https://www.rtk-ai.app/fr/), un CLI open-source qui compresse les sorties de commandes pour économiser du contexte.

## Installation

### 1. Les règles globales

```bash
# Si tu n'as pas encore de ~/.claude/CLAUDE.md :
cp personal-setup/CLAUDE.md ~/.claude/CLAUDE.md

# Si tu en as déjà un : fusionne à la main, ou ajoute en import à la fin du tien :
echo '@jorgo-ai-framework/personal-setup/CLAUDE.md' >> ~/.claude/CLAUDE.md
```

Adapte-le à ton cas : langue de réponse, stack de prédilection, protocole de test. Ce fichier est un point de départ, pas une vérité universelle — il reflète mes préférences, pas des règles absolues pour tout le monde.

### 2. Les sub-agents

```bash
mkdir -p ~/.claude/agents
cp personal-setup/agents/*.md ~/.claude/agents/
```

Vérifie qu'ils apparaissent avec `claude agent list` (ou l'équivalent selon ta version de Claude Code), puis invoque-les via l'agent `general-purpose`/`Task` en précisant le nom, ou laisse Claude les invoquer proactivement selon leur `description`.

### 3. RTK (optionnel mais recommandé)

Gratuit, open-source, aucune inscription. Le binaire n'est pas vendu dans ce repo — installe-le depuis [rtk-ai.app](https://www.rtk-ai.app/fr/). Une fois `rtk` sur ton `PATH`, ajoute le hook fourni dans [`RTK.md`](RTK.md) à ton `~/.claude/settings.json` pour qu'il s'active automatiquement sur chaque commande shell — sans ce hook, `rtk` est installé mais ne fait rien.

## Pourquoi séparé des plugins `jai-*`

Les plugins `jai-*` (voir [`COMMANDS.md`](../COMMANDS.md) à la racine) sont des **skills Claude Code** — des commandes que tu invoques explicitement (`/jai-dev:01-plan`, etc.), installables/désinstallables par projet ou globalement via le marketplace.

Ce dossier `personal-setup/` est différent : ce sont des **règles de fond** qui s'appliquent en permanence, à toute la session, peu importe si un plugin `jai-*` est installé ou non. Les deux sont complémentaires mais indépendants — tu peux prendre l'un sans l'autre.
