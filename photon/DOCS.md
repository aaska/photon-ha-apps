# Home Assistant Add-on: Photon Geocoder

Photon is an open-source geocoder for OpenStreetMap data. This add-on lets you host your own local, offline-capable geocoding and reverse geocoding API on your Home Assistant computer.

## Requirements

> [!WARNING]
> Photon is highly resource-intensive!
> * **Storage**: Depending on the region selected, the database size can be large. A small country (e.g., Andorra) takes a few hundred megabytes, but a large country (e.g., Germany, France) takes 5GB - 15GB, and the full world (planet) index takes over 70GB - 100GB+.
> * **RAM**: Elasticsearch runs under the hood. It is recommended to have at least 4GB of RAM on your Home Assistant host to run a medium-sized country index smoothly.

## Configuration Options

Configure the following options in the **Configuration** tab in the Home Assistant UI:

### `import_mode`
* **Type**: `list` (Options: `db` or `jsonl`)
* **Default**: `db`
* **Description**: In `db` mode, the container downloads a prebuilt index which is much faster. In `jsonl` mode, it imports raw geodata (useful if you want custom extra tags).

### `region`
* **Type**: `string`
* **Default**: `germany`
* **Description**: The country or continent to download data for. Examples: `germany`, `france`, `andorra`, `europe`. Refer to Geofabrik/Photon extract lists for supported names.

### `languages`
* **Type**: `string` (Optional)
* **Default**: `en`
* **Description**: Comma-separated list of languages to include in the index (e.g., `en,de,fr`).

### `update_strategy`
* **Type**: `list` (Options: `PARALLEL`, `SEQUENTIAL`, `DISABLED`)
* **Default**: `PARALLEL`
* **Description**: Sets how database updates are downloaded and imported.

### `update_interval`
* **Type**: `string` (Optional)
* **Default**: `720h`
* **Description**: Time duration between update checks (e.g., `720h` for 30 days).

### `download_max_retries`
* **Type**: `integer` (Optional)
* **Default**: `5`
* **Description**: Maximum download retries for geodata files.

### `extra_tags`
* **Type**: `string` (Optional)
* **Description**: Extra tags to include when importing in `jsonl` mode (e.g. `surface,smoothness`).

## Network and Access

The add-on exposes port `2322`. It is mapped to the host port `2322` by default.
Once the container starts up and imports the geodata, you can query it from your local network using:

```bash
curl "http://<homeassistant-ip>:2322/api?q=berlin"
```

To perform a reverse geocoding query (convert coordinates to address):

```bash
curl "http://<homeassistant-ip>:2322/reverse?lon=13.40&lat=52.52"
```

## Logs and Troubleshooting

If the add-on starts but is not immediately responsive, check the logs. During the first start, the container will download the selected region's database index, which can take anywhere from a few minutes to hours depending on your internet connection and the size of the region.
