# ☀️ Zon-bewuste Rolluik Bediening

[![version](https://img.shields.io/badge/version-1.1.0-blue.svg)](https://github.com/r3mcos3/blueprints)
[![Home Assistant](https://img.shields.io/badge/Home%20Assistant-2025.12.0%2B-blue.svg)](https://www.home-assistant.io/)

Automatische rolluik bediening op basis van de zonpositie. Sluit rolluiken wanneer de zon op de voor- of achterkant van je huis schijnt, en opent ze weer zodra de zon wegdraait. Respecteert handmatige bediening zodat jij altijd de baas blijft! 🌞

## ✨ Features

- ☀️ **Automatisch sluiten** - Sluit rolluiken wanneer de zon op die gevel schijnt
- 🔄 **Automatisch openen** - Opent rolluiken zodra de zon naar een andere richting draait (optioneel)
- 🖐️ **Handmatige override** - Detecteert handmatige bediening en raakt die rolluiken niet meer aan tot de zon wegdraait
- 📐 **Configureerbaar zon-venster** - Stel in hoeveel graden marge de zon op een gevel mag staan
- 🌅 **Minimale zonnehoogte** - Geen actie bij laagstaande ochtend- of avondzon
- 🔽 **Flexibele posities** - Stel sluit- en openingspositie in (bijv. half dicht op 50%)
- 🏠 **Voor- en achterkant apart** - Afzonderlijke rolluiken per gevelzijde

## 📋 Requirements

Voor gebruik heb je nodig:

1. **Cover entiteiten** - Rolluiken of zonwering als `cover` domein in Home Assistant
2. **Sun integratie** - Ingebouwde HA sun-integratie (`sun.sun`), standaard beschikbaar
3. **Kompasrichting voorkant** - De azimut van je voorgevel (zie tip hieronder)

### Optioneel

- **Input Boolean helpers** - Voor handmatige override detectie (één per gevelzijde)

## 🌐 Azimut van je huis bepalen

Ga naar **[suncalc.org](https://www.suncalc.org/)**, zoek je huis op en bepaal in welke richting je voordeur wijst:

| Richting | Azimut |
|----------|--------|
| Noord | 0° |
| Oost | 90° |
| Zuid | 180° |
| West | 270° |

De achterkant van je huis wordt automatisch berekend als voorkant + 180°.

## 🚀 Installatie

### Automatische installatie

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fsun_shutter_control%2Fsun_shutter_control.yaml)

### Handmatige installatie

1. Ga in Home Assistant naar **Instellingen** → **Automatiseringen & scènes** → **Blauwdrukken**
2. Klik op **Blauwdruk importeren**
3. Voer de blueprint URL in:
   ```
   https://github.com/r3mcos3/blueprints/blob/main/sun_shutter_control/sun_shutter_control.yaml
   ```
4. Klik op **Voorbeeld** en dan **Importeren**

### Override helpers aanmaken (optioneel)

Voor de handmatige override functie maak je per gevelzijde een schakelaar-helper aan:

1. Ga naar **Instellingen** → **Hulpapparaten en -diensten** → **Helper maken**
2. Kies **Schakelaar (Toggle)**
3. Geef hem een naam, bijv. `Rolluik voorkant handmatig`
4. Koppel de helper aan de blueprint in de sectie **Handmatige Override**

## ⚙️ Configuratie

### Verplichte instellingen

| Parameter | Omschrijving |
|-----------|--------------|
| 🏠 Richting voorkant huis | Azimut van de voorgevel in graden (0–359°) |
| 🏠 Rolluiken voorkant | Cover entiteiten aan de voorkant |
| 🏡 Rolluiken achterkant | Cover entiteiten aan de achterkant |

### ☀️ Zon-instellingen (uitklapbaar)

| Parameter | Omschrijving | Standaard |
|-----------|--------------|-----------|
| 📐 Zon-venster hoek | Graden links/rechts van de gevel die meetellen | 90° |
| 🌅 Minimale zonnehoogte | Minimale zonhoogte boven de horizon | 10° |

### ⚙️ Rolluik-instellingen (uitklapbaar)

| Parameter | Omschrijving | Standaard |
|-----------|--------------|-----------|
| 🔽 Sluitpositie | Positie bij zon op de gevel (0% = volledig dicht) | 0% |
| 🔼 Automatisch openen | Openen als zon wegdraait | Aan |
| 🔼 Openingspositie | Positie bij automatisch openen | 100% |

### 🖐️ Handmatige Override (uitklapbaar)

| Parameter | Omschrijving | Standaard |
|-----------|--------------|-----------|
| 🖐️ Override helper voorkant | Input Boolean helper voor voorkant | Optioneel |
| 🖐️ Override helper achterkant | Input Boolean helper voor achterkant | Optioneel |

## 🎯 Hoe het werkt

### Zonpositie berekening

De blueprint gebruikt het **azimut** van `sun.sun` — de kompasrichting van de zon (0–360°). Elke 5 minuten wordt berekend of de zon op de voor- of achtergevel staat:

```
Hoekverschil = ((zon-azimut − gevelrichting + 180) % 360) − 180
Zon op gevel = hoekverschil < zon-venster EN zonhoogte > minimum
```

Deze formule werkt correct voor alle richtingen, inclusief de overgang rond Noord (359° → 1°).

### Beslislogica

Voor elke gevelzijde (voor/achter) geldt:

```
Als zon op gevel EN geen handmatige override
  → Rolluiken naar sluitpositie

Als zon NIET op gevel EN automatisch openen aan
  → Rolluiken naar openingspositie
  → Handmatige override resetten

Als zon op gevel EN handmatige override actief
  → Niets doen (respecteert handmatige bediening)
```

### Handmatige override

HA registreert bij elke toestandswijziging **wie** de wijziging initieerde. Als een gebruiker een rolluik handmatig bedient (via de app, dashboard of fysieke schakelaar), bevat de context een `user_id`. De blueprint detecteert dit en zet de override-helper aan.

De override wordt **automatisch gereset** zodra de zon van die gevel wegdraait en auto-open actief is — zodat alles de volgende dag weer normaal werkt.

### Trigger momenten

| Trigger | Wanneer |
|---------|---------|
| ⏱️ Periodieke check | Elke 5 minuten |
| 🏠 HA herstart | Bij opstarten van Home Assistant |
| 🖐️ Cover wijziging | Direct bij handmatige rolluikbediening (alleen voor override detectie) |

## 💡 Gebruik voorbeelden

### Voorbeeld 1: Voorkant naar het oosten

Huis met voordeur op het oosten (ochtendzon op de voorkant):

```yaml
automation:
  - alias: "Rolluiken op zonpositie"
    use_blueprint:
      path: r3mcos3/sun_shutter_control
      input:
        front_facing_azimuth: 90
        front_covers:
          - cover.rolluik_woonkamer_voor
          - cover.rolluik_slaapkamer_voor
        back_covers:
          - cover.rolluik_keuken_achter
```

**Verwacht gedrag:**
- Ochtend (zon in het oosten): voorkant gaat dicht
- Middag/namiddag (zon in het westen): achterkant gaat dicht
- Avond: alles gaat open

### Voorbeeld 2: Half sluiten met override

Rolluiken gaan op 50% bij zon, met handmatige override:

```yaml
automation:
  - alias: "Rolluiken op zonpositie"
    use_blueprint:
      path: r3mcos3/sun_shutter_control
      input:
        front_facing_azimuth: 180
        front_covers:
          - cover.rolluik_woonkamer
        back_covers:
          - cover.rolluik_slaapkamer
        close_position: 50
        open_position: 100
        front_override_helper: input_boolean.rolluik_voor_handmatig
        back_override_helper: input_boolean.rolluik_achter_handmatig
```

**Verwacht gedrag:**
- Zon op gevel: rolluiken gaan naar 50%
- Iemand opent handmatig: override aan, automatie raakt het niet aan
- Zon draait weg: rolluiken gaan naar 100% open, override reset

### Voorbeeld 3: Alleen sluiten, nooit automatisch openen

Alleen automatisch dichtgaan, handmatig openen:

```yaml
automation:
  - alias: "Rolluiken dicht bij zon"
    use_blueprint:
      path: r3mcos3/sun_shutter_control
      input:
        front_facing_azimuth: 270
        front_covers:
          - cover.rolluik_voor
        back_covers:
          - cover.rolluik_achter
        auto_open: false
        close_position: 0
```

**Verwacht gedrag:**
- Zon op gevel: rolluiken gaan volledig dicht
- Zon weg: niets, rolluiken blijven waar ze zijn

## 🔧 Problemen oplossen

### Rolluiken bewegen niet

1. Controleer of de cover-entiteiten bestaan en reageren via **Ontwikkelaarstools → Staten**
2. Controleer of de automatie ingeschakeld is
3. Controleer de azimut van de zon via `sun.sun` → attribuut `azimuth`
4. Bekijk traces: **Instellingen → Automatiseringen → [naam] → Traces**
5. Controleer of de zonhoogte (`elevation`) boven het minimum staat

### Verkeerde richting berekend

1. Controleer de ingestelde azimut via [suncalc.org](https://www.suncalc.org/)
2. Vergroot het zon-venster (standaard 90°) als de zon net buiten de marge valt
3. Controleer via de traces welke waarden de variabelen `v_sun_on_front` en `v_sun_on_back` bevatten

### Handmatige override werkt niet

1. Controleer of de input_boolean helper bestaat en correct gekoppeld is
2. Bekijk in **Staten** of de helper aan/uitschakelt na handmatige bediening
3. Zorg dat de rolluiken als `cover`-entiteit zijn geconfigureerd (niet als `switch`)
4. Controleer of de bediening via een HA gebruikersaccount gedaan wordt (Alexa/Google-acties hebben geen `user_id` en worden niet als handmatig gezien)

### Override reset niet automatisch

1. Controleer of **Automatisch openen** aanstaat in de rolluik-instellingen
2. De override reset alleen als de zon VAN die gevel wegdraait (niet bij nacht/lage zon)
3. Je kunt de helper altijd handmatig uitzetten via het HA dashboard

## 📝 Versiegeschiedenis

### Versie 1.1.0
- 🖐️ Handmatige override detectie via context `user_id`
- 🔄 Automatisch resetten van override bij wegdraaiende zon
- ✨ Optionele input_boolean helpers per gevelzijde

### Versie 1.0.1
- 📝 Tip voor [suncalc.org](https://www.suncalc.org/) toegevoegd aan beschrijving

### Versie 1.0.0
- 🎉 Eerste release
- ☀️ Azimut-gebaseerde rolluik bediening
- 📐 Configureerbaar zon-venster met wrap-around correctie
- 🌅 Minimale zonnehoogte instelling
- 🔽 Configureerbare sluit- en openingspositie

## 🤝 Bijdragen

Bug gevonden of een suggestie? Maak een [issue aan op GitHub](https://github.com/r3mcos3/blueprints/issues)!

## 📄 Licentie

Deze blueprint wordt aangeboden onder de MIT Licentie.

## 🙏 Credits

Gemaakt door [r3mcos3](https://github.com/r3mcos3)
