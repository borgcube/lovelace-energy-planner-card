# Energy Planner Card

<p align="center">
  <img src="logo.png" alt="Energy Planner Card logo" width="160">
</p>

The Energy Planner Card is a dependency-free Home Assistant Lovelace card for
the [Energy Planner integration](https://github.com/borgcube/home-assistant-energy-planner).
It presents the adjusted electricity-price timeline as a compact chart, keeps
fixed monthly costs separate, and shows the latest plan without controlling
any device.

The card is a Marketplace **Dashboard** package. Updating it only needs a
browser reload; updating the backend integration still follows Home
Assistant's normal integration update process.

## Install

Install **Energy Planner Card** from Home Assistant's Marketplace/HACS
Dashboard section. The dashboard resource is added by the Marketplace
installer. Reload the browser after installation or an update.

The card requires the Energy Planner backend integration. Install or update
that integration separately, then restart Home Assistant when Home Assistant
requests it.

## Configure

Add the card to a dashboard with the entity IDs created by the integration:

```yaml
type: custom:energy-planner-card
title: Energy Planner
price_sensor: sensor.energy_planner_adjusted_electricity_price
fixed_cost_sensor: sensor.energy_planner_fixed_monthly_electricity_cost
last_plan_sensor: sensor.energy_planner_last_plan
history_sensor: sensor.energy_planner_plan_history
price_mode: all_in
show_spot: true
```

The card also accepts `price_mode: spot`, an optional `entry_id`, and a
`currency` label. The price sensor's `data` attribute may contain hourly or
higher-resolution points, including 15-minute ENTSO-E data.

The form in the collapsed **Plan an appliance** section calls the integration's
plan-only service. It does not start, switch, or schedule a device.

The price chart is interactive: hover or drag across it to inspect a rate, and
click a point to keep its interval and exact values visible below the chart.
The plan-only form remains open while Home Assistant refreshes its state.

## Migrating from the bundled card

The backend integration previously registered a card resource automatically.
After installing this package:

1. Keep the existing `custom:energy-planner-card` YAML configuration.
2. Remove the old `/energy_planner/energy-planner-card.js` resource if it is
   still listed under dashboard resources.
3. Reload the browser.

The integration keeps its legacy static path for manually configured dashboards,
but the Marketplace Dashboard package is the supported card distribution and
receives frontend updates independently of backend restarts.

## Development

The card has no build step. Validate the JavaScript with:

```sh
node --check energy-planner-card.js
```
