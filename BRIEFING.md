# Briefing: Slidification – Start einer lokalen Session

> Diesen Text komplett in eine neue Claude-Code-Session kopieren (Desktop App oder `claude` im Terminal), gestartet in einem **leeren lokalen Ordner**, z. B. `Slidification/`. Kein GitHub nötig.

---

## Auftrag

Du unterstützt mich beim Bau von **Slidification**: ein Tool, das aus einer ExecSum, Gesprächsnotizen oder einem ersten Draft **top-management-taugliche PowerPoint-Folien (v1.0)** baut – im Design des jeweiligen Klienten, wählbar per Stil-Schalter.

Ich bin Transformationsberater im Financial-Services-Umfeld. Arbeite auf Deutsch, direkt, top-down.

**Schritt 1 (jetzt):** Lege das Grundgerüst unten an. Ausschließlich lokal – kein GitHub-Remote, kein Push.
**Schritt 2:** Sobald ich Folien in `reference/` abgelegt habe, analysierst du sie (siehe „Referenzanalyse“).

---

## Bereits getroffene Entscheidungen

1. **Zeitfresser ist das Bauen der Folien**, nicht die Storyline. Priorität 1 ist die Folien-Engine; Storyline-Intelligenz folgt später.
2. **Visuell statt Bullets:** Management-taugliche Folien = Schaubilder, Roadmaps, Matrizen etc. Bullet-Folien nur als Ausnahme.
3. **Native, editierbare .pptx:** Grafiken als echte PowerPoint-Shapes, Text in echten Platzhaltern. Keine Bilder, keine losen Textboxen.
4. **Trennung Inhalt / Design:**
   - Archetypen (Grafik-Baupläne) sind designneutral und werden vom Tool gezeichnet.
   - Klienten-Master (`.potx`) liefert nur Rahmen, Logo, Titelzeile.
   - Klienten-Tokens (Farben, Schriften, Abstände) färben die Archetypen ein.
   - Neuer Klient = Master + `style.yaml`. Ziel: < 1 Stunde Onboarding.
5. **Kapazität je Archetyp:** Jede Grafik hat Maximalwerte (Elemente, Wörter). Das Tool **verdichtet Inhalte**, statt Schrift zu verkleinern oder zu quetschen.
6. **Vertraulichkeit:** Klienten-Master, Referenzfolien und Decks bleiben lokal und werden nie committet. Referenzmaterial wird anonymisiert.
7. **Einstieg als Claude-Skill / lokales Tool**, nicht als Web-App. Qualität zuerst beweisen, Form später.

## Marktlage (Kurzfassung)

- Copilot, Plus AI, Prezent: Templates ja, aber je *eine* Corporate Identity, Vendor-Onboarding; Copilot mit unzuverlässigem Platzhalter-Handling.
- Deckary / think-cell Assist: Action Titles, aber keine Klienten-Templates.
- Gamma / Beautiful.ai: eigene Themes, für Klienten-CI ungeeignet.
- **Lücke:** Multi-Klienten-Templates + visuelle Archetypen + eingebauter Management-QA in einem Tool.

## Zielarchitektur (Pipeline)

```
Input (ExecSum / Notizen / Draft)
  → 1. Aussagen extrahieren        (eine Kernaussage je Folie, Action Title)
  → 2. Archetyp wählen             (welche Visualisierung trägt die Aussage?)
  → 3. Verdichten auf Kapazität    (Text passt in die Form)
  → 4. Rendern                     (Archetyp-Bauplan + Klienten-Tokens + Klienten-Master)
  → 5. QA / Red-Team               (Prüfung gegen rules/management-ready.md)
  → .pptx
```

---

## Grundgerüst – bitte anlegen

```
Slidification/
├── README.md                       # Konzept (aus diesem Briefing ableiten)
├── CLAUDE.md                       # Arbeitsregeln (Inhalt unten)
├── .gitignore                      # Inhalt unten (für späteres lokales git)
├── slidification.config.example.yaml
├── library/slide-types/README.md   # Archetyp-Katalog (unten)
├── rules/management-ready.md       # QA-Rubrik (unten)
├── clients/_example/style.yaml     # Beispiel-Klientenstil (unten)
├── reference/README.md             # Ablagehinweise für Best-Practice-Folien
└── output/
```

### CLAUDE.md
- Konzept und Architektur: siehe `README.md`.
- Niemals Klienten- oder Referenzdateien (`.pptx`, `.potx`, `.pdf`, …) committen, hochladen oder außerhalb dieses Rechners ablegen.
- Für `.pptx`/`.potx` den pptx-Skill nutzen.
- Referenzanalyse: pro Folie Archetyp, Aussage-Typ, Anzahl Elemente, Wörter je Element, Farb-/Hervorhebungslogik erfassen; Ergebnisse in `library/slide-types/` und `rules/` einarbeiten – ohne Klienteninhalte zu übernehmen.
- Grafiken immer als native, editierbare Shapes – keine Bilder.
- Folien: Deutsch, formal; Stil gemäß `rules/management-ready.md`.

### .gitignore
```
*.pptx
*.potx
*.ppt
*.pdf
*.docx
*.xlsx
*.vtt
*.srt
clients/*
!clients/_example/
reference/*
!reference/README.md
slidification.config.yaml
output/
__pycache__/
.venv/
node_modules/
.DS_Store
~$*
```

### slidification.config.example.yaml
```yaml
clients_dir: ./clients
reference_dir: ./reference
output_dir: ./output
default_client: _example
```

### library/slide-types/README.md – Archetyp-Katalog (Entwurf)

Kapazitätswerte sind Platzhalter und werden an den Referenzfolien kalibriert.

| # | Archetyp | Trägt Aussagen wie … | Kapazität (vorläufig) |
|---|---|---|---|
| 1 | Kernaussage + 3 Treiber | „X gelingt nur, wenn A, B, C“ | 3–4 Säulen, je ≤ 25 Wörter |
| 2 | Roadmap / Gantt | „Umsetzung in 3 Wellen bis Q4“ | ≤ 6 Workstreams, ≤ 8 Meilensteine |
| 3 | Optionenvergleich (Harvey Balls + Empfehlung) | „Option B ist die beste Balance aus …“ | ≤ 4 Optionen × ≤ 5 Kriterien |
| 4 | 2×2-Matrix | „Fokus auf Quick Wins oben links“ | ≤ 10 Items |
| 5 | Prozesskette / Zielbild | „Zielprozess reduziert Schritte von 9 auf 5“ | ≤ 7 Schritte, je ≤ 8 Wörter |
| 6 | Status-/Risiko-Dashboard | „2 von 6 Workstreams gefährden Go-live“ | ≤ 8 Zeilen |
| 7 | Ist → Soll | „Von fragmentiert zu integriert“ | ≤ 5 Dimensionen |
| 8 | Wasserfall / KPI-Brücke | „Kosteneffekt von 12 Mio. durch …“ | ≤ 8 Balken |
| 9 | Organigramm / Governance | „Klare Entscheidungsrechte über 3 Ebenen“ | ≤ 3 Ebenen, ≤ 12 Boxen |
| 10 | Entscheidungsvorlage | „Vorstand beschließt heute Option B“ | Situation / Optionen / Empfehlung / Beschluss |

### rules/management-ready.md – QA-Rubrik (Entwurf, jede Regel maschinell prüfbar)

**Folie**
1. Action Title: Aussage (Satz mit Verb), kein Thema; max. 2 Zeilen.
2. Eine Aussage pro Folie; der Inhalt belegt ausschließlich den Titel.
3. So what: jede Folie hat eine Implikation oder einen Entscheidungsbedarf.
4. Visual vor Bullet: Bullet-Folie nur, wenn kein Archetyp die Aussage besser trägt.
5. Kapazität: kein Element über Archetyp-Kapazität; kein Text-Overflow.
6. Zukunftsgerichtet: Status nur mit Konsequenz (Risiko, Maßnahme, Entscheidung).

**Deck**
7. Top-down: ExecSum vorne; Folgefolien begründen deren Punkte in gleicher Reihenfolge.
8. Zahlenkonsistenz: gleiche Kennzahl = gleicher Wert auf allen Folien.
9. Ownership: Maßnahmen haben Owner und Termin.
10. Keine Floskeln („holistisch“, „leverage“, „Journey“ …).

### clients/_example/style.yaml
```yaml
name: Beispielbank
master: master.potx
layouts:
  title: "Titelfolie"
  content: "Titel und Inhalt"
  blank_with_title: "Nur Titel"
tokens:
  colors:
    primary: "#002D62"
    secondary: "#6B8EAD"
    accent: "#E87722"
    positive: "#2E7D32"
    warning: "#F9A825"
    negative: "#C62828"
    text: "#1A1A1A"
    muted: "#8C8C8C"
  fonts: { heading: "Arial", body: "Arial" }
  sizes_pt: { title: 20, body: 12, min: 9 }   # unter min wird verdichtet, nicht verkleinert
  spacing_cm: { margin: 1.2, gutter: 0.4 }
tone:
  language: de
  address: formal
  terminology: {}
```

### reference/README.md
Ablage für 8–15 anonymisierte Best-Practice-Folien (verschiedene Typen), 1–2 Folien mit Präfix `zeitfresser_`, optional ein Klienten-Master (`.potx`).

---

## Referenzanalyse (Schritt 2)

Wenn ich sage „Analysiere die Referenzfolien“:
1. Jede Folie in `reference/` mit dem pptx-Skill lesen (inkl. gerenderter Ansicht).
2. Je Folie erfassen: Archetyp (oder neuer Typ), Aussage-Typ, Anzahl Elemente, Wörter je Element, Farb- und Hervorhebungslogik, was sie managementtauglich macht.
3. `zeitfresser_`-Folien gesondert auswerten: Was genau kostet beim Bauen Zeit?
4. Ergebnis:
   - **Top-5-Archetypen für v1.0** mit Begründung
   - kalibrierte Kapazitäten im Katalog
   - geschärfte QA-Regeln
   - Vorschlag für den ersten Prototyp: **ein Archetyp end-to-end in zwei Klienten-Stilen**
5. Keine Klienteninhalte in Katalog oder Regeln übernehmen.
