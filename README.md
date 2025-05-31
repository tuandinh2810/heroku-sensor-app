
# Heroku Sensor App

Tämä on yksinkertainen Flask-pohjainen sovellus, joka näyttää mittaustietoja (lämpötila, kosteus, CO₂) SQLite-tietokannasta. Sovellus julkaistaan automaattisesti Herokuun GitHubin kautta (CI/CD).

# Ominaisuudet

- REST API palauttaa 20 uusinta mittausdataa `measurements.db`-tiedostosta
- Luo tietokantataulu automaattisesti, jos sitä ei ole
- Automaattinen julkaisu Herokuun GitHubista

# Käytetyt teknologiat

- Python + Flask
- SQLite
- Gunicorn (WSGI-palvelin Herokua varten)
- Heroku
- GitHub Actions (CI/CD)

# API

GET /data
```

Palauttaa JSON-listan 20 uusimmasta mittauksesta:

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

```bash
git clone https://github.com/tuandinh2810/heroku-sensor-app.git
cd heroku-sensor-app
pip install -r requirements.txt
python api_server.py
```
Selaa osoitteeseen `http://localhost:5000/data` nähdäksesi mittaustiedot.

# Heroku-julkaisu

# Konfiguraatio:

- Procfile: sisältää rivin `web: gunicorn api_server:app`
- requirements.txt`: sisältää Flaskin ja Gunicornin
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
