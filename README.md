# renovate-config

Zentrale [Renovate](https://docs.renovatebot.com/) Konfiguration für alle Repos von [Code Crush GmbH](https://codecrush.ch).

---

## Einbinden

`renovate.json` im Root des Repos anlegen:

```json
{
  "extends": [
    "github>codecrush-ch/renovate-config"
  ],
  "baseBranchPatterns": [
    "main"
  ]
}
```

> **Wichtig:** Renovate muss im jeweiligen Repo als [GitHub App](https://github.com/apps/renovate) installiert sein.

---

## Verhalten im Überblick

| Regel | Verhalten |
|---|---|
| **Major Updates** | Nur nach manueller Freigabe im Dependency Dashboard |
| **Minor, Patch & Docker-Digests** | Auto-Merge durch Renovate (`platformAutomerge: false`) — Di/Mi/Do-Nacht **23:00–05:59** Europe/Zurich |
| **`nuxt`, `@nuxt/*`** | Locked auf `^3`, kein Major-PR |
| **`vue`, `vue-router`** | Locked auf `^3`, kein Major-PR |
| **devDependencies** | Gebündelt in einem einzigen PR |
| **npm/pnpm Releases** | 3 Tage Wartezeit vor erstem PR |
| **Lockfile Maintenance** | Automerge via Squash, Di/Mi/Do-Nacht (23:00–05:59) |
| **Max. offene PRs** | 5 gleichzeitig |

---

## Projektspezifisch überschreiben

Overrides einfach in der `renovate.json` des Repos ergänzen — sie werden mit dieser Config gemergt:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>codecrush-ch/renovate-config"],
  "packageRules": [
    {
      "matchPackageNames": ["some-package"],
      "enabled": false
    }
  ]
}
```

---

## Renovate → Production (GitHub Actions)

Vollständige Dokumentation mit Flowcharts: **[docs/RENOVATE-PRODUCTION.md](docs/RENOVATE-PRODUCTION.md)**

Kurz: Templates unter `templates/github/workflows/` — Pilot `backyardultrachur.ch`; Rollout und Ausnahmen siehe Doku.

---

Änderungen an dieser Config wirken sich automatisch auf alle einbindenden Repos aus.
