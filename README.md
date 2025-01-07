# onewire-to-mqtt.py

Onewire-to-mqtt.py is intended to run as a service, it accesses [owfs](https://owfs.org/index_php_page_owfs.html) and reads values from 1-Wire sensors.
The values aquired from owfs are published using an MQTT broker.

A running [owserver](https://owfs.org/index_php_page_owserver.html) with [owfs](https://owfs.org/index_php_page_owfs.html) and an MQTT broker (e.g: [mosquitto](https://mosquitto.org)) are required to use this daemon.

## Usage

A configuration file is the only parameter which has to be passed to the program:

```
usage: onewire-to-mqtt.py [-h] <config_file>

Reads sensors from owfs and publishes the values to an MQTT broker

positional arguments:
  <config_file>  file with configuration

optional arguments:
  -h, --help     show this help message and exit
```

## Example

```
 ./onewire-to-mqtt.py myconfig.cfg
```

## Configuration file

A self explaining sample configuration file is included.

```
# sample configuration 
 
# MQTT broker related config
[mqtt]
host = 127.0.0.1
port = 1883
# user and pw optional, leave empty if not necessary
user = mqtt
pw = 12345678

# polling interval for sensors
pollinterval = 30

# topic for status messages
statustopic = onewire-to-mqtt/status

# Onewire related config 
[onewire]
# 1wire needs to be available via owfs on the local file system, where owserver might connect to a different IP adress
dir = /mnt/1wire

[log]
loglevel = 0
logfile = /var/log/onewire-to-mqtt.log

# list of sensors to be polled and according mqtt topics
# might be sensors IDs or aliases provided in the owfs config
[sensors]
26.C51B8C000000/B1-R1-A/pressure = hhv7/jordkallare/pressure
26.C51B8C000000/humidity = hhv7/jordkallare/humidity
10.F19884010800/temperature = hhv7/jordkallare/temperature
basement_livingroom/temperature = homeassistant/sensor/basement_livingroom/temperature
```

## Libraries required 
The following libraries are required by onewire-to-mqtt.py 
- paho-mqtt (tested with version: 1.6.1-1)
- setproctitle (tested with version: 1.3.1-1+b2)

If on a Debian(/Ubuntu/etc) system, install with
```
apt-get install python3-paho-mqtt python3-setproctitle
```

## References 
- https://mosquitto.org
- http://owfs.org
- https://owfs.org/index_php_page_owfs.html
