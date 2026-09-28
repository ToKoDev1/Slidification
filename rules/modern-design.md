# Regeln „modernes Foliendesign“ (Entwurf)

Ergänzt `management-ready.md` um die **visuelle** Ebene. Gilt klientenunabhängig: Der Klienten-Stil liefert Farben und Schriften, diese Regeln legen fest, **wie** sie eingesetzt werden.
Jede Regel muss **maschinell prüfbar** sein. Grenzwerte sind vorläufig und werden anhand aktueller Referenzdecks (ab 2021) kalibriert.

## Leitgedanke

- Modern wirkt eine Folie nicht wegen des Templates, sondern wegen **Disziplin**: wenig Farbe, viel Weißraum, beschriftete Daten, keine Dekoration.
- Gemeinsamer Nenner aktueller MBB-Decks (McKinsey seit Identität 2019, BCG und Bain 2024–2026): Grau als Standard, **ein** Akzent für die Kernaussage, das Chart beweist den Titel.
- Altes Material (Rahmen, Schatten, Farbverläufe in Shapes, Legenden, ClipArt, volle Bullet-Seiten) ist **kein** Vorbild – Referenzen vor 2021 nur für Struktur, nicht für Design nutzen.

## Farbe
1. **Grau ist Standard**: Alle Elemente ohne Aussagefunktion in `muted` bzw. Grautönen.
2. **Ein Akzent pro Folie**: `accent` markiert ausschließlich die Kernaussage (ein Balken, eine Reihe, eine Box). Max. 1 Akzentfarbe je Folie.
3. **Primärfarbe für Struktur**: `primary` nur für Titel, Kopfzeilen, Achsen-Hervorhebung – nicht für Flächenfüllung ganzer Grafiken.
4. **Ampelfarben nur mit Bedeutung**: `positive` / `warning` / `negative` ausschließlich für Status oder Bewertung, nie als Dekoration.
5. **Max. 3 Farbtöne** je Folie (ohne Grau und Text).

## Weißraum & Raster
6. **Weißraum als Budget**: Mind. ~30 % der Inhaltsfläche bleibt leer. Reicht der Platz nicht, wird verdichtet (siehe Kapazität), nicht verkleinert.
7. **Raster statt Augenmaß**: Alle Elemente liegen auf dem Raster aus `spacing_cm` (Rand, Gutter); gleiche Elemente haben gleiche Größe und gleiche Abstände.
8. **Eine Blickrichtung**: Leseführung links → rechts oder oben → unten; keine konkurrierenden Blickfänge.

## Typografie
9. **Max. 2 Schriftgrößen im Inhalt** (plus Titel und Fußnote). Hierarchie über Gewicht (fett) statt über Größe.
10. **Keine Unterstreichung, keine Kursiv-Hervorhebung, kein Versal-Fließtext**. Hervorhebung nur fett oder Akzentfarbe.
11. **Mindestgröße** gemäß `sizes_pt.min`; darunter wird verdichtet.

## Charts
12. **Direkt beschriften**: Werte an Balken/Punkten, Reihennamen am Linienende – keine Legende, wo direkte Beschriftung möglich ist.
13. **Keine Chart-Deko**: keine Gitterlinien (oder nur sehr hell), keine y-Achse bei beschrifteten Werten, kein 3D, keine Schatten, kein Chart-Titel (der Action Title ersetzt ihn).
14. **Chart-Kopf zweiteilig**: Kennzahl fett, darunter Einheit/Zeitraum in `muted` (z. B. „Kosten, Mio. EUR, 2025–2027“).
15. **Prognose unterscheidbar**: Plan-/Prognosewerte als Umriss oder gestrichelt, Ist-Werte gefüllt.
16. **Hervorhebung = Aussage**: Der akzentuierte Datenpunkt ist genau der, den der Action Title benennt.

## Shapes & Elemente
17. **Flach**: keine Schatten, keine Farbverläufe, keine 3D-Effekte, keine abgerundeten „Bonbon“-Formen; dünne oder keine Rahmenlinien.
18. **Icons sparsam**: einfarbig, Linienstil, ein einheitliches Set; nur wenn sie Kategorien unterscheiden, nie als Füllmaterial.
19. **Keine Bilder** für Grafiken (siehe `CLAUDE.md`); Fotos nur auf Titel-/Kapiteltrennern, falls der Klienten-Master das vorsieht.

## Folienrahmen
20. **Quelle und Fußnoten** unten links in Fußnotengröße, nummeriert (¹ ² ³), einheitlich formuliert („Quelle: …“).
21. **Tracker optional**: Kapitel-/Abschnittsmarke oben, klein, in `muted` – nie mehr als ein Tracker.
22. **Kapiteltrenner** dürfen invertiert sein (dunkler Hintergrund in `primary`, weiße Schrift); Inhaltsfolien bleiben hell.

## Handwerk – keine Standardformen
23. **Keine SmartArt, keine Office-Formvorlagen**: Jede Grafik wird aus Grundformen selbst gebaut; Office-Schnellformatvorlagen und Theme-Effekte sind tabu.
24. **Keine Default-Farben**: Office-Standardpalette (z. B. Blau #4472C4, Orange #ED7D31) kommt nie vor – nur Klienten-Tokens.
25. **Linie vor Box**: Wo eine Trennlinie oder Weißraum gliedert, entfällt der Kasten. Boxen nur, wenn sie eine Einheit bilden.
26. **Reduzierte Formen**: Rechtecke eckig oder minimal gerundet (einheitlicher Radius); keine Blockpfeile, Sterne, Sprechblasen, Standard-Chevrons. Pfeile als dünne Linien mit kleiner Spitze.
27. **Typografie als Gestaltungsmittel**: Nummerierung, Kennzahlen und Kernwerte als große, fette Ziffern statt Kreis-Bubbles oder Icons.
28. **Einheitliche Linienstärken**: max. 2 Strichstärken je Folie (z. B. 0,75 pt Struktur, 2 pt Akzent).
29. **Tabellen schlank**: keine Tabellenformatvorlagen, keine Zebrastreifen, keine vertikalen Linien; nur dünne horizontale Trenner, Kopfzeile fett.
30. **Optische Präzision**: Kanten bündig, Textblöcke auf gemeinsamer Grundlinie, einheitliche Innenabstände in allen Formen; kein Autofit-Schrumpfen.
31. **Begründungspflicht**: Jedes Element hat eine Funktion für die Aussage – sonst wird es entfernt.

## Prüfbarkeit (für QA-Schritt)

| Regel | Maschinell prüfbar über |
|---|---|
| 2, 5 | Zählung verwendeter Füllfarben je Folie gegen Tokens |
| 6 | Summe Shape-Flächen / Inhaltsfläche |
| 7 | Positionen und Größen gegen Raster, Varianz gleicher Elemente |
| 9–11 | Zählung Schriftgrößen/-stile in Textläufen |
| 12–13 | Chart-XML: Legende, Gitterlinien, Achsen, 3D-Flags |
| 17 | Shape-XML: Schatten, Verläufe, Effekte |
| 20 | Existenz und Position Quellen-Platzhalter |
| 23–24, 26 | Shape-XML: SmartArt-/Diagramm-Parts, Preset-Geometrien, Farbwerte gegen Tokens |
| 28–30 | Linienstärken, Tabellen-Styles, Innenabstände, Autofit-Flags |

## Referenzquellen (öffentlich, aktuell)

Zum lokalen Herunterladen nach `reference/` (Dateien bleiben lokal, siehe `.gitignore`):
- BCG AI Radar 2026 (Jan. 2026) – bcg.com/publications/2026/as-ai-investments-surge-ceos-take-the-lead
- BCG AI at Work 2025 (Juni 2025, Slideshow-Format) – bcg.com/publications/2025/ai-at-work-momentum-builds-but-gaps-remain
- BCG AI Radar 2025 (Jan. 2025) – bcg.com/publications/2025/closing-the-ai-impact-gap
- McKinsey Technology Trends Outlook 2025 (Juli 2025) – mckinsey.com/capabilities/tech-and-ai/our-insights/the-top-trends-in-tech-2025
- Sammlungen nach Jahr filtern (nur ab 2021): slideworks.io (McKinsey, BCG, Bain)
