# SolarQuant Model Zoo

A catalog of machine learning plugins for SolarQuant, the edge ML platform for solar energy systems. Each model listed here implements the [SolarQuant plugin spec](plugin-spec/) and can be deployed to SolarNodes for real-time inference on live inverter data.

Models live in their own repositories -- this zoo links to them with brief model cards and hosts the shared plugin specification.

## Available Models

| Model | Description | Repo |
|-------|-------------|------|
| [Stonybrook Anomaly Detection](models/stonybrook-anomaly-detection/) | Real-time solar inverter anomaly detection using cross-prediction | TODO |

## Plugin Architecture

All models in the zoo implement the [SolarQuant plugin specification](plugin-spec/), an HTTP-based interface with two endpoints:

- **`GET /health`** -- Health check used by SolarQuant to monitor plugin status
- **`POST /measure`** -- Receives measurement datums, returns predictions

Plugins are packaged as Docker containers and deployed to SolarNodes at the edge. SolarQuant sends live inverter measurements to your plugin and posts any returned predictions to SolarNetwork. See the [full plugin spec](plugin-spec/) for details.

