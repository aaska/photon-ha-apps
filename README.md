# Home Assistant Photon Geocoder Repository

This repository contains a custom Home Assistant Add-on for the **Photon Geocoder** by Komoot.

Photon is a geocoding and reverse geocoding service built on top of OpenStreetMap data and Elasticsearch. It provides a fast, offline-capable location search API.

## Installation

To add this repository to your Home Assistant instance:

1. Copy the URL of this repository.
2. In Home Assistant, navigate to **Settings** -> **Add-ons** -> **Add-on Store**.
3. In the top right corner, click the three-dot menu (**...**) and select **Repositories**.
4. Paste the repository URL and click **Add**.
5. Close the dialog, refresh the page, and search for **Photon Geocoder**.
6. Select it and click **Install**.

## Configuration

Once installed, you can configure the add-on in the **Configuration** tab:

* `import_mode`: Set to `db` (default) to download a prebuilt index, or `jsonl` to build one from raw data.
* `region`: The country or region to download (e.g. `germany`, `andorra`, `france`).
* `languages`: Comma-separated languages to index (e.g. `en,de,fr`).
* `update_strategy`: Update policy (`PARALLEL` or `SEQUENTIAL` or `DISABLED`).
* `update_interval`: Check interval for index updates (e.g., `720h`).

## Usage

After starting the add-on, it will download and import the index for the selected region. Once the logs show that the server has started, the geocoder API will be available on the local network on port `2322`.

### Example Query

```bash
curl "http://<homeassistant-ip>:2322/api?q=berlin"
```
