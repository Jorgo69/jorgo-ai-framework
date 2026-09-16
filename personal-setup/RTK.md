# RTK — Rust Token Killer

CLI open-source (Apache 2.0) qui compresse les sorties de commandes avant qu'elles n'atteignent le contexte de l'agent. Gratuit, sans compte, sans clé API, sans limite d'usage. Site officiel et installation : https://www.rtk-ai.app/fr/

## Commandes meta (toujours en direct, sans passer par le hook)

```bash
rtk gain              # Affiche les économies de tokens réalisées
rtk gain --history     # Historique d'usage des commandes avec économies
rtk discover           # Analyse ton historique Claude Code pour repérer les opportunités ratées
rtk proxy <cmd>        # Exécute une commande brute sans filtrage (debug)
```

## Vérifier l'installation

```bash
rtk --version          # Doit afficher : rtk X.Y.Z
rtk gain               # Doit fonctionner (pas "command not found")
which rtk              # Vérifie le bon binaire
```

⚠️ **Collision de nom possible** : si `rtk gain` échoue, un autre outil nommé `rtk` (ex. un "Rust Type Kit") peut être installé à la place.

## Utilisation via hook

Une fois `rtk` installé (voir le site officiel), le hook ci-dessous réécrit automatiquement les commandes shell classiques pour passer par `rtk` — par exemple `git status` devient `rtk git status`, de façon transparente et sans coût de token supplémentaire pour toi.

Ajoute ce bloc dans `~/.claude/settings.json` (fusionne avec ta clé `hooks` existante si tu en as déjà une) :

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "rtk hook claude"
          }
        ]
      }
    ]
  }
}
```

C'est tout : `rtk` doit être sur le `PATH`, aucune autre configuration n'est nécessaire. Vérifie ensuite avec une commande verbeuse (`git log`, `git status` sur un gros repo) que la sortie est bien compressée.
