# charles-tools

Privater Plugin-Marketplace fuer Claude (Cowork, Chat und Claude Code).

## Inhalt

| Plugin | Skills |
| --- | --- |
| `dozent` | dozenten-reiseplanung, dozenten-briefing, seminar-recherche |
| `ablage-system` | ablage, fragenset-ablage |
| `frmd-pasn` | frmd-bildoptimierung |
| `oberflaeche` | cockpit-ui |

## Installation

**Cowork / Chat:** Customize → Plugins → Add marketplace → `charleshuetten-dot/claude-plugins` → gewuenschte Plugins installieren.

**Claude Code:**

```
/plugin marketplace add charleshuetten-dot/claude-plugins
/plugin install dozent@charles-tools
```

## Pflege

Skills werden hier bearbeitet, nicht mehr lokal je Umgebung. Es ist bewusst keine
`version` gesetzt: jeder Commit gilt als neue Version, Updates kommen also
automatisch an. Nach Aenderungen im Repo: `/plugin marketplace update charles-tools`.
