# Stonybrook Anomaly Detection

Real-time solar inverter anomaly detection using cross-prediction models. Developed at Stony Brook University.  The research paper published on this work is available [here](https://www.researchgate.net/publication/396743294_Identifying_High-Significance_Latent_Physical_Anomalies_in_Solar_Energy_Systems) and a general news article on the topic is available [here](https://pv-magazine-usa.com/2025/12/18/machine-learning-models-identify-hidden-physical-defects-in-solar-arrays/).

## Overview

This plugin monitors a fleet of solar inverters by predicting each inverter's expected output based on its peers. When an inverter's actual production diverges from what the model predicts, it is flagged as anomalous. This allows operators to catch failing or underperforming inverters early.

## API

This plugin implements the [SolarQuant plugin spec](../../plugin-spec/) (`/health` and `/measure`).

### `POST /measure` -- Example

**Request:**
```json
{
  "datums": [
    {
      "nodeId": 377,
      "sourceId": "/G4/MA/S1/INV/1",
      "timestamp": 1672531200,
      "i": {
        "watts": 2450.5,
        "voltage": 240.2
      },
      "a": {
        "wattHours": 32455000
      }
    }
  ]
}
```

**Response:**
```json
{
  "accepted": 1,
  "rejected": 0,
  "predictions": [
    {
      "nodeId": 377,
      "sourceId": "/G4/MA/S1/INV/1",
      "timestamp": 1672531200,
      "i": {
        "watts": 2435.2
      },
      "s": {
        "anomalyStatus": "NORMAL"
      },
      "meta": {
        "confidence": 0.95,
        "method": "xgboost-cross-prediction"
      }
    }
  ],
  "message": "processed"
}
```

## Tech Stack

- Python 3.11
- FastAPI + Uvicorn
- XGBoost (cross-prediction models)
- scikit-learn (preprocessing)
- SciPy (statistical testing)

