# Bildschirmschoner

Fünf Symbole der Kategorie `screensaver`. Ein Schirm nennt einen davon per
Kennung (`screensaver="<uuid>"`); der Compiler holt das Bild beim Deploy aus
der Registratur des Projekts, nicht aus einer Bibliothek.

| Datei | Fassung | Kennung |
|---|---|---|
| `Esse-Glut.hearth_symbol` | 0.2.0 | 6b1d7d4e-…5f02 |
| `Herbstlaub.hearth_symbol` | 0.2.0 | 4f1c8ad2-7e63-4b09-9d51-2a6c0f83be74 |
| `Schwarz.hearth_symbol` | 0.2.0 | 6b1d7d4e-…5f04 |
| `Sommerwiese.hearth_symbol` | 0.2.0 | 6b1d7d4e-…5f01 |
| `Winterstimmung.hearth_symbol` | 0.2.0 | 6b1d7d4e-…5f03 |

## Warum Dateien und keine `.hearth_library`

Gemessen am 12.09.2026: `hearthsym_import` im Symboleditor bringt einen
Schoner nicht heil in eine Bibliothek. Beide Formen verlieren die Hälfte —

| Eingabe | Zeichnung | Steuerklasse |
|---|---|---|
| `<symbol uuid …><svg>…` (Studios Exportform) | **0 Elemente** | 33 234 Zeichen |
| blankes `<svg>` (der Kern daraus) | 117 Elemente | **leer** |

Das ist hearth-symbols#7. Eine Bibliothek, die so entsteht, trägt Symbole, die
entweder nichts zeichnen oder sich nicht bewegen — schlimmer als keine.

Eine `.hearth_symbol` ist dagegen das vollständige Symbol in einer Datei:
Zeichnung, Steuerklasse, Eigenschaften, Kennung und Fassung. Sie ist Text,
also sichtbar im Diff, und Studio liest sie direkt:

    add_symbols_symbol(path="…/screensaver/Herbstlaub.hearth_symbol", library="…")
    set_symbols_symbol(id=<id>, path="…")   # eine vorhandene erneuern

Sobald der Import heil ist, kann hier eine `screensaver.hearth_library`
danebenstehen; die Dateien bleiben dann die Quelle.
