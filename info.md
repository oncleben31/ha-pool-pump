# Pool Pump Manager

[![GitHub Release][releases-shield]][releases]
[![GitHub Activity][commits-shield]][commits]
[![License][license-shield]][license]

[![hacs][hacsbadge]][hacs]

[![Discord][discord-shield]][discord]
[![Discord francophone][discord-fr-shield]][discord-fr]
[![Community Forum][forum-shield]][forum]

_Component developped by using the amazing development template [blueprint][blueprint]._

This custom component for Home Assistant can be used to automatically control
a pool pump that is turned on/off by a switch that Home Assistant can control.

This component is based on the work of [@exxamalte](https://github.com/exxamalte/home-assistant-customisations/tree/master/pool-pump).

On top of the orignal version by @exxamalte, this version can be installed by HACS
and you can use the [blueprint][blueprint] feature to quickly fork this repo and
have a working development environment in a container.

I will adapt it to my needs. At completion this plugin will compute the filtering
schedule taking into account the pool water temperature.

## Minimum requirements

* A switch supported in Home Assistant that can turn on/off power to your
  pool pump.

## Features

* Compute the totatl duration according to the pool water tempearture.
* Can control any switch (or other entity) that supports being turned on/off.
* Support for distinguishing three different switch modes:
    * Auto: Turn switch on/off automatically based on rules and configuration.
    * On: Turn switch on.
    * Off: Turn switch off.
* Splits the total target duration into two runs arround the solar noon.
1/3 before ans 2/3 after to allow filtering during the hottest part of the day.
* You can add a customisable break between the two runs.
* Initializes the following entities:
    * `pool_pump.next_run_schedule`: Pretty string of the scheduled current/next run.
    * `pool_pump.next_run_start`: Starting datetime of the current/next run.
    * `pool_pump.next_run_stop`: End datetime of the current/next run.
    * `pool_pump.total_daily_filtering_duration`: Turn switch off.
* Optional: Support for a water level sensor to specify an entity that indicates if the
  pool has reached a critical water level in which case the pool pump should
  not run at all.

## Installation

1. Click `install`.
2. Modify your `configuration.yaml` as explain below.
3. Restart Home Assistant.


## Configuration is done in in configuration.yaml file

Minimal content in your `configuration.yaml` file is:

```yaml
pool_pump:
  switch_entity_id: switch.pool_pump_switch
  pool_pump_mode_entity_id: input_select.pool_pump_mode
  pool_temperature_entity_id: sensor.pool_water_temperature
  # optional:
  water_level_critical_entity_id: binary_sensor.pool_water_level_critical
  schedule_break_in_hours: 1.0
```

All parameters are required except the two after `# optional` comment.

You will need to set some automations and inputs (input_boolean, input_select and input_numbers)
to use it. Please read [README.md](https://github.com/oncleben31/ha-pool_pump/blob/master/README.md) for additional documentation.

<!---->

<!---->

***

[blueprint]: https://github.com/custom-components/blueprint
[commits-shield]: https://img.shields.io/github/commit-activity/y/oncleben31/ha-pool_pump.svg?style=for-the-badge
[commits]: https://github.com/oncleben31/ha-pool_pump/commits/master
[hacs]: https://github.com/custom-components/hacs
[hacsbadge]: https://img.shields.io/badge/HACS-Custom-orange.svg?style=for-the-badge
[discord]: https://discord.gg/Qa5fW2R
[discord-fr]: https://discord.gg/JeTFJzE$
[discord-shield]: https://img.shields.io/discord/330944238910963714.svg?style=for-the-badge&label=HA%20Discord
[discord-fr-shield]: https://img.shields.io/discord/542746125292273674?style=for-the-badge&label=Discord%20francophone
[forum-shield]: https://img.shields.io/badge/community-forum-brightgreen.svg?style=for-the-badge
[forum]: https://community.home-assistant.io/
[license-shield]: https://img.shields.io/github/license/custom-components/blueprint.svg?style=for-the-badge
[releases-shield]: https://img.shields.io/github/release/oncleben31/ha-pool_pump.svg?style=for-the-badge
[releases]: https://github.com/oncleben31/ha-pool_pump/releases
[license]: https://github.com/oncleben31/ha-pool_pump/blob/master/LICENSE