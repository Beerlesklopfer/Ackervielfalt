# Bildschirmschoner

Fünf Symbole der Kategorie `screensaver`. Ein Schirm nennt einen davon per
Kennung (`screensaver="<uuid>"`); der Compiler holt das Bild beim Deploy aus
der Registratur des Projekts.

| Datei | Fassung | Art | Kennung |
|---|---|---|---|
| `Esse-Glut.hearth_symbol` | 0.2.0 | SMIL | 6b1d7d4e-…5f02 |
| `Herbstlaub.hearth_symbol` | 0.2.0 | **rechnet** | 4f1c8ad2-7e63-4b09-9d51-2a6c0f83be74 |
| `Schwarz.hearth_symbol` | 0.2.0 | — | 6b1d7d4e-…5f04 |
| `Sommerwiese.hearth_symbol` | 0.4.5 | **rechnet** | 6b1d7d4e-…5f01 |
| `Winterstimmung.hearth_symbol` | 0.3.2 | **rechnet** | 6b1d7d4e-…5f03 |

## ACHTUNG: es gibt eine ZWEITE Stelle, und sie gewinnt beim Start

`hearth-studio/resources/symbols/screensaver/` liefert dieselben fünf Schoner
im Paket mit. Beim Öffnen der Bibliothek gleicht `FStore::ensureBuiltinSymbols()`
sie **nach Namen** ab und schreibt bei abweichendem Inhalt die mitgelieferte
Fassung über die des Anwenders — still, ohne Meldung.

Gemessen am 12.09.2026: nach einem Studio-Neustart stand die Sommerwiese wieder
auf 0.2.0, und der nächste Deploy schob den alten Stand bis auf die Anlage.
Das ist hearth-studio#48.

**Bis das behoben ist gilt:** wer hier eine Fassung ändert, muss sie in
`hearth-studio/resources/symbols/screensaver/` mitziehen und Studio neu bauen.
Sonst hält die Änderung bis zum nächsten Start.

## Die Bibliothek führt, die Dateien sind die Ausfuhr

`../screensaver.hearth_library` hält dieselben fünf Symbole. Gearbeitet wird
**im Symboleditor**, nicht in der Datei: dort zählt die Fassung von selbst
hoch, dort sind die Elemente kommentierbar, und dort steht ein Stand statt
fünf Dateien nebeneinander. Der Weg ist

    Editor: doc_open(screensaver.hearth_library) → ändern → doc_save
            → hearthsym_export(path=…/screensaver/<Name>.hearth_symbol)
    Studio: set_symbols_symbol(id=…, path=…) → refresh_project_symbol_bodies
            → save_project → publish_project

## Was der Rundlauf durch den Editor kostet (Stand 12.09.2026)

Die **Zeichnung** kommt vollständig durch — an der Sommerwiese gemessen:
182 SMIL-Animationen, 37 `<use>`, 4 Rollen, 126 `<path>` hin wie zurück; an
Herbstlaub 20 von 20 Rollen und die Steuerklasse zeichengleich. Die Ebene liegt
dabei als Bild (`svg-content`), weil sie Gruppen trägt — hearth-symbols#12.

Der **Kopf und der Rahmen** kommen nicht durch: `viewBox` fällt auf 200×150
zurück, `preserveAspectRatio` und `hearth:element` gehen verloren, ebenso
`category`, `author`, `description` und die Fassung aus der Datei —
hearth-symbols#13. Deshalb nach jedem Import von Hand:

    symbol_set_viewbox(x=0, y=0, w=1920, h=1080)
    symbol_set_meta(category="screensaver", version="<die aus der Datei>")

`author` und `description` haben über MCP keinen Rückweg; sie stehen
verlässlich nur in Studios Bibliothek (`set_symbols_symbol(author=…,
description=…)`).

Der Prüfer meldet an allen fünf „Kein Element trägt: …" und „Das Symbol
zeichnet nichts". Beides ist falsch — er liest die Elementzeilen und nicht das
Bild der Ebene: hearth-symbols#14.
