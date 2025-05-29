# Heroku Sensor App

Tämä on Python-pohjainen client-server-sovellus, joka:
- Simuloi mittausdataa (lämpötila, kosteus, CO2)
- Tallentaa tiedot SQLite-tietokantaan
- Tarjoaa API:n Flaskin avulla
- Julkaistu Herokuun
- Visualisoidaan Node-REDin avulla

## Rakenne

- `mqtt_data_sender.py` – tuottaa ja tallentaa dataa
- `api_server.py` – Flask API, julkaistu Herokuun

## Käyttö

```bash
python mqtt_data_sender.py
python api_server.py
```

## CI/CD

Projektissa on GitHub Actions workflow, joka julkaisee automaattisesti Herokuun kun koodi pusketaan GitHubiin.
