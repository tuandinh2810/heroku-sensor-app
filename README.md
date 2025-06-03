
# Heroku Sensor App

Tämä sovellus simuloi mittausdataa (lämpötila, kosteus, CO₂), tallentaa sen SQLite-tietokantaan ja tarjoaa REST API:n datan noutamiseen. Datan syöttö voidaan käynnistää ja pysäyttää Node-REDin kautta MQTT-komentojen avulla. Data visualisoidaan Node-RED dashboardilla. Sovellus on julkaistavissa Herokuun. Sovellus julkaistaan automaattisesti Herokuun GitHubin kautta (CI/CD).

# Ominaisuudet
- Simuloitu sensoridata (lämpötila, kosteus, CO₂).
- MQTT-ohjaus: käynnistä tai keskeytä datan syöttö.
- Tallennus SQLite-tietokantaan.
- Flask-pohjainen REST API.
- Node-RED dashboard mittausdatan visualisointiin.
- Julkaistavissa Herokuun.

# Käytetyt teknologiat

- Python + Flask
- SQLite
- Gunicorn (WSGI-palvelin Herokua varten)
- Heroku
- GitHub Actions (CI/CD)

# REST API

GET /data - palauttaa 20 viimeisintä mittausta

```json
[
  {
    "timestamp": "2024-05-29 12:34:56",
    "temperature": 22.5,
    "humidity": 55.0,
    "co2": 420
  },
  ...
]

# Paikallinen ajaminen
- Asenna riippuvuudet
     =>  pip install -r requirements.txt
- Käynnistä mittaussimulaattori (data + MQTT-ohjaus)
     => python mqtt_data_sender.py
- Käynnistä Flask API
     =>python api_server.py.

# MQTT-ohjaus (Node-REDistä)
- Broker: test.mosquitto.org
- Topic: data/control
- Payload: start tai stop

# Heroku-julkaisu
- Luo uusi Heroku-sovellus
     heroku create tuan3105

- Lähetä sovellus
     git push heroku main

# Konfiguraatio:

- Procfile: sisältää rivin "web: gunicorn api_server:app"
- requirements.txt: sisältää Flaskin ja Gunicornin
- Heroku on yhdistetty GitHub-repoon (branch: main)
- Automaattinen julkaisu on käytössä

# CI/CD:

- Jokainen `main`-branchiin tehty push laukaisee automaattisen julkaisun Herokuun
- Julkaisun tilaa voi seurata GitHubin "Actions"-välilehdeltä

# Projektin rakenne

heroku-sensor-app/
├── api_server.py
├── requirements.txt
├── Procfile
├── measurements.db
└── .github/
    └── workflows/
        └── <CI/CD workflow (jos käytössä)>

# Mahdollisia jatkokehityksiä

- Lisää yksikkötestit `pytest`-kirjastolla
- Lisää Node-RED-pohjainen käyttöliittymä
- Lisää anturidatan lähetys MQTT:n avulla

# Tekijä

- Nimi: Tuan Dinh, Yasir Abdulwahid 
- Heroku-sovellus:[https://tuan2905.herokuapp.com/data](https://tuan2905.herokuapp.com/data)
