# Slidification

Tool, das aus einer ExecSum, Gesprächsnotizen oder einem ersten Draft **top-management-taugliche PowerPoint-Folien** (Version 1.0) baut – im Design des jeweiligen Klienten, umschaltbar per Stil-Schalter.

## Kernthese

- Der Zeitfresser ist nicht die Storyline, sondern **das Bauen der Folien** – insbesondere visueller Folien (Roadmaps, Matrizen, Schaubilder), nicht Bullet-Folien.
- Differenzierung ggü. Copilot / Gamma / Prezent: **Multi-Klienten-Templates + visuelle Archetypen + eingebauter Management-Qualitätscheck** in einem Tool.
- Output ist **natives, editierbares .pptx** – echte Shapes und Platzhalter, keine Bilder.

## Architektur (Zielbild)

```
Input (ExecSum / Notizen / Draft)
  → 1. Aussagen extrahieren        (eine Kernaussage je Folie, Action Title)
  → 2. Archetyp wählen             (welche Visualisierung trägt die Aussage?)
  → 3. Verdichten auf Kapazität    (Text passt in die Form, nicht umgekehrt)
  → 4. Rendern                     (Archetyp-Bauplan + Klienten-Tokens + Klienten-Master)
  → 5. QA / Red-Team               (Prüfung gegen rules/management-ready.md)
  → .pptx
```

**Trennung von Inhalt und Design:**
- `library/slide-types/` – Baupläne der Archetypen, designneutral (Raster, Kapazität, Varianten).
- `clients/<name>/` – Klienten-Stil: Master (`.potx`) für Rahmen/Logo/Titelzeile + Tokens (Farben, Schriften, Abstände). **Liegt lokal, nie im Repo.**
- Neuer Klient = Master ablegen + `style.yaml` ausfüllen. Ziel: < 1 Stunde Onboarding.

## Ordnerstruktur

| Pfad | Inhalt | Im Repo? |
|---|---|---|
| `library/slide-types/` | Archetyp-Katalog & Baupläne | ja |
| `rules/` | Regeln „managementtauglich“ (QA-Rubrik) | ja |
| `clients/_example/` | Beispiel-Stilkonfiguration | ja |
| `clients/<klient>/` | echte Klienten-Master & Tokens | **nein** (gitignored) |
| `reference/` | Best-Practice-Folien zum Lernen | **nein** (gitignored) |

## Vertraulichkeit

- Das Repo enthält **nur Code, Baupläne und Regeln**.
- Klienten-Master, Referenzfolien und Klienten-Decks bleiben **lokal** – `.gitignore` blockiert `.pptx`, `.potx`, `.pdf` etc. repo-weit.
- Referenzmaterial trotzdem anonymisieren (Namen, Logos, echte Zahlen): Beim Lesen durch Claude wird der Inhalt zur Verarbeitung übertragen.

## Nächste Schritte

1. Repo lokal klonen, Claude Code im Repo starten (Desktop App oder `claude`).
2. 8–15 anonymisierte Best-Practice-Folien in `reference/` ablegen (+ 1–2 „Zeitfresser“-Folien, optional ein `.potx`).
3. Analyse → Top-5-Archetypen für v1.0, Kapazitätsregeln, QA-Regeln schärfen.
4. Prototyp: ein Archetyp end-to-end in zwei Klienten-Stilen.
