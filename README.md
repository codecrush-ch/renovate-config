# Renovate Shared Config

Zentrale Renovate-Konfiguration für alle meine Projekte.

## Verwendung

In deinem Repo in der `renovate.json`:
```json
{
  "extends": [
    "github>DEIN-USERNAME/renovate-config"
  ]
}
```

Ersetze `DEIN-USERNAME` mit deinem GitHub-Benutzernamen.

## Konfiguration

- ✅ Nuxt 3.x Lock (keine Major)
- ✅ Vue 3.x Lock
- ✅ Major Updates mit Dashboard Approval
- ✅ Dev-Dependencies gebündelt
- ✅ npm Updates mit 3 Tagen Verzögerung
- ✅ Lock File Maintenance aktiviert

## Updates

Einfach diese Config updaten und alle Repos nutzen automatisch die neuen Einstellungen.
