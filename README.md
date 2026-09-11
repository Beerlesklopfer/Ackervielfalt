# Ackersteuerung — SoLaWi Ackervielfalt

Bewässerungssteuerung des Gemeinschaftsackers der SoLaWi Ackervielfalt,
gebaut mit [ForgeIEC](https://forgeiec.io).

| Datei | Inhalt |
|---|---|
| `Ackersteuerung.forge` | SPS-Projekt (IEC 61131-3, ForgeIEC Studio): Programme, Bausteine, Buskonfiguration, Gerätebeschreibungen |
| `Ackersteuerung.hearth` | HMI-Projekt (Hearth Studio): Bildschirme, Symbole, Variablenanbindung |

## Anlage

Sechs Modbus-TCP-Feldboxen (Amsamotion ETH-MODBUS-IO8R-A und IO5R) an zwei
Segmenten, ein Weidmüller-UR20-Koppler im Schaltschrank. Je Beet vier Ventile
mit Taster und Status-LED; ein Arbiter begrenzt die gleichzeitig offenen
Ventile.

Betriebsarten: Aus, Manuell, One-Shot, Wiederkehrend, Auto.

## Öffnen

* SPS: ForgeIEC Studio, `Ackersteuerung.forge`
* HMI: Hearth Studio, `Ackersteuerung.hearth`

Pakete: https://apt.forgeiec.io
