# renovate-config

Zentrale [Renovate](https://docs.renovatebot.com/) Konfiguration für alle Repos von [Code Crush GmbH](https://codecrush.ch).

---

## Einbinden

`renovate.json` im Root des Repos anlegen:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>codecrush-ch/renovate-config"]
}
```

> **Wichtig:** Renovate muss im jeweiligen Repo als [GitHub App](https://github.com/apps/renovate) installiert sein.

---

## Verhalten im Überblick

| Regel | Verhalten |
|---|---|
| **Major Updates** | Nur nach manueller Freigabe im Dependency Dashboard |
| **Minor & Patch** | Automatischer Squash-Merge, CI muss grün sein — Di/Mi/Do um 5 Uhr |
| **`nuxt`, `@nuxt/*`** | Locked auf `^3`, kein Major-PR |
| **`vue`, `vue-router`** | Locked auf `^3`, kein Major-PR |
| **devDependencies** | Gebündelt in einem einzigen PR |
| **npm/pnpm Releases** | 3 Tage Wartezeit vor erstem PR |
| **Lockfile Maintenance** | Automerge via Squash, Di/Mi/Do um 5 Uhr |
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

Für Repos mit `deploy.yaml` und Auto-Merge durch Renovate:

| Datei | Quelle |
|---|---|
| `renovate-production.yaml` | [`templates/github/workflows/renovate-production.yaml`](templates/github/workflows/renovate-production.yaml) |
| `deploy.yaml` Ergänzung | [`deploy-workflow-call.snippet.yaml`](templates/github/workflows/deploy-workflow-call.snippet.yaml) |
| `sync-develop.yaml` | [`sync-develop-renovate.snippet.yaml`](templates/github/workflows/sync-develop-renovate.snippet.yaml) |

Ablauf: Renovate merged auf `main` (oder `develop` ohne `main`) → Production-Deploy → optional `develop` mit `main` abgleichen. Keine Tags/Releases für Renovate.

**Test:** Workflow «♻️ Renovate Production» manuell starten, `skip_actor_check` aktivieren.

**Vorerst manuell prüfen:** Config-Repos, `movermap-app`, abweichende Deploy-Workflows (z. B. `schreiner-berneroberland.ch`, `gastrostory.ch`).

Template wandert später ins D3-Projekt-Repo für neue Projekte.

---

Änderungen an dieser Config wirken sich automatisch auf alle einbindenden Repos aus.
