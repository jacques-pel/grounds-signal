# Grounds Signal (in progress)

**Can specialty coffee shop openings predict which Tokyo neighborhoods will appreciate next?**

## Why

Research in US cities has linked new coffee shops to rising home values: using Yelp data, Glaeser, Kim and Luca (2018) found each new coffee shop in a zip code associated with about a 0.5% increase in house prices. Grounds Signal tests whether that signal holds in Tokyo, a market with a public record of transaction prices to validate it against. The longer-term aim is to carry validated proxies like this into markets where transaction data is scarce, such as Mexico City.

## Approach (planned)

- **Validation:** a Spatial Durbin Model testing whether coffee shop openings predict price changes in a neighborhood and its neighbors (spatial spillover)
- **Prediction:** an XGBoost regressor forecasting the percent change in neighborhood price per square meter at 12, 24 and 36 months
- **Output:** classification bands derived from the forecast (neutral, early stage, active)

## Data

- **Coffee shops:** Google Places API (Text Search). Planned: two queries per neighborhood ("coffee shop" and "café"), deduplicated by place ID
- **Property prices:** quarterly transaction price data from Japan's Ministry of Land, Infrastructure, Transport and Tourism (MLIT)
- **Controls:** interest rates, station proximity, inflation, demographics

## Status

- [x] Google Places collection functions (`text_search`, `collect_places`) built and tested on Harajuku: 60 coffee shops retrieved
- [ ] Tokyo neighborhood list from the OpenStreetMap Overpass API
- [ ] Full Tokyo collection and deduplication
- [ ] MLIT data exploration and spatial join to neighborhood boundaries
- [ ] Lagged features, model training, and the spatial validation layer

## Setup

Requires Python 3.12.

    python -m venv grounds-signal-env
    source grounds-signal-env/bin/activate
    pip install -r requirements.txt

Then create a `.env` file containing `GOOGLE_PLACES_API_KEY=...`. It is excluded from the repository.

## Tools

Python, requests, pandas, python-dotenv, Jupyter. Planned: GeoPandas, PySAL, XGBoost.
