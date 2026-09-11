# Ackersteuerung — SoLaWi Ackervielfalt

Bewässerungssteuerung des Gemeinschaftsackers der SoLaWi Ackervielfalt
(Kooperation mit SALZ Automation), gebaut mit [ForgeIEC](https://forgeiec.io).

| Datei | Inhalt |
|---|---|
| `Ackersteuerung.forge` | SPS-Projekt (IEC 61131-3, ForgeIEC Studio): Programme, Bausteine, Buskonfiguration, Gerätebeschreibungen |
| `Ackersteuerung.hearth` | HMI-Projekt (Hearth Studio): Bildschirme, Symbole, Variablenanbindung |

## Anlage

Sechs Modbus-TCP-Feldboxen (Amsamotion ETH-MODBUS-IO8R-A und IO5R) an zwei
Segmenten, ein Weidmüller-UR20-Koppler im Schaltschrank. 24 Ventile, je Beet
Taster und Status-LED; ein Arbiter begrenzt die gleichzeitig offenen Ventile.

Betriebsarten: Aus, Manuell, One-Shot, Wiederkehrend, Auto (zurückgestellt).

## Dokumentation

Die vollständige Beschreibung steht im Projekt selbst: ForgeIEC Studio →
Projekteigenschaften. Jede Gruppe, jeder Baustein und jede persistente
Einstellung trägt dort Beschreibung und Label. Die Einstellungen:

| Variable | Label | Startwert |
|---|---|---|
| `Betrieb.xManuell` / `xOneShot` / `xWiederkehrend` / `xAuto` | Betriebsart | — |
| `Betrieb.uMaxVentile` | Max. offene Ventile | 24 |
| `Betrieb.rBlinkHz` | Blinkfrequenz Handbetrieb [Hz] | 0.1 |
| `Zeitplan.aValveJobs` | Ventil-Jobs | — |

## Öffnen

* SPS: ForgeIEC Studio, `Ackersteuerung.forge`
* HMI: Hearth Studio, `Ackersteuerung.hearth`

Pakete: https://apt.forgeiec.io

## Hinweis zum Einchecken

`Ackersteuerung.hearth` enthält lokal den Passwort-Hash des HMI-Benutzers.
Der Git-Filter `hearth-nopw` nimmt ihn beim Einchecken heraus. Er muss in
jedem Klon einmal gesetzt werden:

```
git config filter.hearth-nopw.clean "sed -E 's/ pw-hash=\"[^\"]*\"//; s/ pw-hash-epoch=\"[^\"]*\"//'"
git config filter.hearth-nopw.smudge cat
```
