# Simple cover control

This is a simple blueprint for cover control. It will be modified over time with stuff thats needed in my own home. Currently the cover will open and close by sun elevation. You can also define an early and late open and close time which will override the sun elevation condition if the times are passed. 

## Planned:

- Implementing Workday/Weekend/Holliday switch to set other late and early times

## Installation

1. **Blueprint importieren**  
   Klicke auf den folgenden Link, um das Blueprint direkt in dein Home Assistant zu importieren:
    
   [![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2Fkreativmonkey%2Fha-share%2Frefs%2Fheads%2Fmain%2Fblueprints%2Fautomation%2Fsimple_cover_control%2Fsimple_cover_control.yaml)

2. **Alternativ: Manuelles Hinzufügen**  
   - Erstelle (falls nicht vorhanden) einen Ordner im Home Assistant Config-Verzeichnis unter:  
     `config/blueprints/automation/DEIN-ORDNERNAME/`  
   - Lege dort eine `.yaml`-Datei für das Blueprint an (z.B. `simple_cover_control.yaml`).  
   - Kopiere den **Blueprint-Code** (siehe Repository oder Original-Quelle) in diese Datei.  
   - Lade danach die Blueprints neu, z.B. über:  
     `Einstellungen > Automatisierungen & Szenen > Blueprints > Neuladen`.

3. **Automatisierung anlegen**  
   - Gehe in Home Assistant zu:  
     `Einstellungen > Automatisierungen & Szenen > Blueprints`  
   - Wähle das **„Simple Cover Control“**-Blueprint aus und erstelle eine neue Automatisierung.  
   - Nimm die gewünschten Einstellungen vor (siehe [Konfiguration](#konfiguration)).