# broadlink\_ac\_mqtt\_addon

HassOS addon for [Broadlink AC to Mqtt](https://github.com/liaan/broadlink_ac_mqtt)

## Usage

Place your broadlink\_ac\_mqtt config file in `/config/broadlink_ac_mqtt.yaml`.
MQTT address and login information will be received directly from Home
Assistant and do not need to be included.

Note: MQTT port received from Home Assistant cannot
[currently](https://github.com/liaan/broadlink_ac_mqtt/pull/80) be used so
please specify it in your config file for now.
