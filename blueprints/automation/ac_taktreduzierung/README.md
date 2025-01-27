# Taktreduzierung Klimaanlage

Dieses Blueprint dient dazu, die Taktung von Klimaanlagen im Heiz- oder Kühlbetrieb zu reduzieren bzw. zu vermeiden.  
Durch eine geschickte Steuerung der Soll-Temperatur, welche sich an der Ist-Temperatur orientiert, wird ein unnötiges Ein- und Ausschalten (Takten) der Klimaanlage verhindert.  
Die Idee basiert auf Nutzererfahrungen aus dem Forum [akkudoktor.net](https://akkudoktor.net), insbesondere aus dem Thread:  
[Taktvermeidung bei LLWP](https://akkudoktor.net/t/taktvermeidung-bei-llwp).

---

## Funktionsübersicht

1. **Solltemperatur-Dynamik**  
   - Die Zieltemperatur (Sollwert) wird in Abhängigkeit zur gemessenen Isttemperatur gesetzt.  
   - Sobald die Raumtemperatur zwischen einem konfigurierten **Mindest-** und **Höchstwert** liegt, wird die Solltemperatur an die Isttemperatur „nachgeführt“.  

2. **Maximalwerte-Modus**  
   Wenn die Temperatur die festgelegte **maximale** Ist-Temperatur überschreitet, kann gewählt werden, was geschehen soll:
   - **Hovering**:  
     Das Klimagerät bleibt auf dem eingestellten Maximalwert.  
   - **Standby**:  
     Wechselt auf eine definierte Standby-Temperatur (z.B. 16 °C).  
   - **Turn Off/On**:  
     Klimaanlage wird beim Erreichen des Maximalwerts komplett ausgeschaltet und später wieder eingeschaltet.

3. **Feste Soll-Temperatur oder dynamischer Sollwert**  
   - Du kannst eine **feste Solltemperatur** definieren (z.B. 21 °C).  
   - Alternativ lässt sich ein **`input_number`** als Sollwert-Regler hinterlegen.

4. **Optionale Raumtemperatur**  
   - Ein **Raumtemperatursensor** kann angegeben werden, um perspektivisch statt der internen Temperaturmessung des Klimageräts zu regeln.  
   - *Aktuell* wird der Sensorwert jedoch noch **nicht** ausgewertet.

5. **Einschaltsenke („Startup Peak“)**  
   - Bei Aktivierung dieser Option kann beim **Einschalten** für eine einstellbare Zeit (z.B. 2:30 min) eine niedrigere Temperatur gefahren werden, um die Startlast zu verringern.  
   - Nach Ablauf dieser Zeit wird zur eigentlichen Solltemperatur gewechselt.

---

## Voraussetzungen

- Home Assistant Core oder Home Assistant OS/Supervised (empfohlen).  
- Ein über Home Assistant steuerbares Klimagerät (`climate.xxx`).  
- Optional:  
  - **Input Number** (`input_number.xxx`) für einen variablen Sollwert.  
  - **Temperatursensor** (`sensor.xxx`), der später genutzt werden kann, um die Raumtemperatur zu ermitteln.

---

## Installation

1. **Blueprint importieren**  
   Klicke auf den folgenden Link, um das Blueprint direkt in dein Home Assistant zu importieren:
    
   [![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2Fkreativmonkey%2Fha-share%2Frefs%2Fheads%2Fmain%2Fblueprints%2Fautomation%2Fac_taktreduzierung%2Fac_taktreduzierung.yaml)

2. **Alternativ: Manuelles Hinzufügen**  
   - Erstelle (falls nicht vorhanden) einen Ordner im Home Assistant Config-Verzeichnis unter:  
     `config/blueprints/automation/DEIN-ORDNERNAME/`  
   - Lege dort eine `.yaml`-Datei für das Blueprint an (z.B. `taktreduzierung_klimaanlage.yaml`).  
   - Kopiere den **Blueprint-Code** (siehe Repository oder Original-Quelle) in diese Datei.  
   - Lade danach die Blueprints neu, z.B. über:  
     `Einstellungen > Automatisierungen & Szenen > Blueprints > Neuladen`.

3. **Automatisierung anlegen**  
   - Gehe in Home Assistant zu:  
     `Einstellungen > Automatisierungen & Szenen > Blueprints`  
   - Wähle das **„Taktreduzierung Klimaanlage“**-Blueprint aus und erstelle eine neue Automatisierung.  
   - Nimm die gewünschten Einstellungen vor (siehe [Konfiguration](#konfiguration)).

---

## Konfiguration

| Parameter                  | Beschreibung                                                                                                                                                                                                                   | Standardwert   |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------- |
| **Climate-Gerät**         | Das zu steuernde Klimagerät (z.B. `climate.wohnzimmer`).                                                                                                                                                                      | *(Pflicht)*    |
| **Raumtemperatur**        | Optionaler externer Raumtemperatursensor (noch nicht aktiv genutzt).                                                                                                                                                          | *leer*         |
| **Solltemperatur**        | Feste Solltemperatur, falls kein `input_number` hinterlegt wird.                                                                                                                                                              | `21°C`         |
| **Solltemperaturregler**  | Optionaler `input_number` zur dynamischen Einstellung der Solltemperatur.                                                                                                                                                     | *leer*         |
| **Interne minimale Temp.**| Unterhalb dieses Werts beginnt die Anlage zu heizen/kühlen.                                                                                                                                                                    | `20°C`         |
| **Interne maximale Temp.**| Ab dieser Temperatur setzt einer der drei Maximalwert-Modi ein.                                                                                                                                                                | `25°C`         |
| **Regelungsmodus**        | Verhalten beim Erreichen der Maximaltemperatur:<br> – **Hovering**: Gerät bleibt auf Max-Wert.<br> – **Standby**: Gerät geht auf definierte Standby-Temp.<br> – **Turn Off/On**: Gerät wird ein-/ausgeschaltet.                 | `Standby`      |
| **Abschalttemperatur AC** | Temperatureinstellung für den Standby-Modus (z.B. 16 °C), falls nicht komplett abgeschaltet wird.                                                                                                                             | `16°C`         |
| **Einschaltsenke aktivieren** | Aktiviert/Deaktiviert die Option, beim Starten für kurze Zeit auf eine niedrige Temperatur zu gehen, um den Strombedarf zu senken.                                                                                       | `false`        |
| **Einschaltsenke Verzögerung** | Dauer (z.B. 2:30 min), für die dieser niedrige Wert gilt, bevor zur Zieltemperatur zurückgekehrt wird.                                                                                                                     | `2:30`         |

---

## Verwendung

1. **Automatisierung aktivieren**:  
   Stelle sicher, dass die erstellte Automatisierung aktiv ist.  
2. **Feinjustierung**:  
   - Passe bei Bedarf die **Interne maximale Temperatur** nach oben oder unten an, um Takten zu reduzieren.  
   - Nutze das `input_number`-Entity, um bequem im Betrieb den Sollwert zu ändern.  
3. **Einschaltsenke („Startup Peak“)**:  
   - Aktiviere diese Option, wenn das Gerät beim Einschalten sehr viel Leistung zieht und du dies verhindern möchtest.  
   - Die Klimaanlage fährt zunächst die **Abschalttemperatur AC** an und wechselt erst nach Ablauf der eingestellten Verzögerung auf die eigentliche Solltemperatur.

---

## Tipps & Hinweise

- **Min-/Max-Grenzen des Geräts**: Achte darauf, dass deine eingestellten Werte (z.B. 16 °C bis 30 °C) mit dem realen Betriebsbereich deiner Klimaanlage kompatibel sind.  
- **Raumtemperatursensor**: Obwohl das Blueprint die Option hierfür anbietet, ist es in dieser Version noch nicht aktiviert. Zukünftig könnte dieser externe Wert genutzt werden, um genauer zu regeln.  
- **Kompatibilität**: Für einen reibungslosen Betrieb wird Home Assistant ≥ 2022.XX empfohlen.  

---

## Feedback & Weiterentwicklung

- Siehe den Thread im [akkudoktor.net-Forum](https://akkudoktor.net/t/taktvermeidung-bei-llwp) für Diskussionen und Erfahrungsberichte.  
- Pull Requests, Verbesserungsvorschläge und Anregungen sind willkommen.

---

*Letzte Aktualisierung: Version 2025.01.3*
