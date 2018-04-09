# onewire-to-mqtt.py

onewire-to-mqtt.py connects to [owserver](http://owfs.org/index.php?page=owserver) (from [owfs](http://owfs.org) and reads values from 1-Wire sensors.
The values aquired from owserver are published using an MQTT broker.

A running [owserver](http://owfs.org/index.php?page=owserver) and an MQTT broker (e.g: [mosquitto](https://mosquitto.org)) are required to use this daemon.

## Usage

A configuration file is the only parameter which has to be passed to the program:

```
usage: onewire-to-mqtt.py [-h] <config_file>

Reads sensors from owserver and publishes the values to an MQTT broker

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

A self explanatory sample configuration file is included.

```
# sample configuration 
 
# MQTT broker related config
[mqtt]
host = 127.0.0.1
port = 1883

# polling interval for sensors
pollinterval = 30

# topic for status messages
statustopic = onewire-to-mqtt/status

# Onewire related config 
[onewire]
host= 127.0.0.1
port = 4304      

[log]
verbose = false
logfile = /var/log/onewire-to-mqtt.log

# list of sensors to be polled and according mqtt topics 
[sensors]
26.C51B8C000000/B1-R1-A/pressure = hhv7/jordkallare/pressure
26.C51B8C000000/humidity = hhv7/jordkallare/humidity
10.F19884010800/temperature = hhv7/jordkallare/temperature
```

## Libraries required 
The following libraries are required by onewire-to-mqtt.py 
- paho-mqtt (tested with version: 1.3.1) 
- owpython (tested with version: 2.9p8)
- setproctitle (tested with version: 1.1.10)

If on a Debian(/Ubuntu/etc) system, install with
```
apt-get install python-ow python-pip
pip install paho-mqtt
pip install setproctitle

```

## References 
- https://mosquitto.org
- http://owfs.org
- http://owfs.org/index.php?page=owserver
