# Lorawan Server

LoRaWAN server is an all-in-one LoRaWAN platform that acts as Network Server, Join Server and App Server, intergated into a single application.

It provides a simple HTTP interface to monitor the server, by watching the connected gateways, the joined devices, and the received device data.
In addition, three different interfaces (based on MQTT, HTTP, and CoAP protocols) are provided for receiving and sending data from/to the devices.

Running the LoRaWAN server is very simple and all you need is:

- a Java Runtime Environment (JRE) installed (Java 17 or above);
- the jar files located in the `lib` folder;
- configuring the server.cfg and server-devices.json files located within the `cfg` folder.

See the following "Server configuration" section for a simple guide on how to set the two configuration files.

Once the server has been correctly configured, you can run it by executing the following command:
```
java -cp "lib/*" run.server.Server
```

More execution options are described in the "Running the server" section.


## Server configuration

The server loads its configuration from a JSON file that by default is `cfg/server.cfg`. However a different file can be specified by using the '-f' command option, e.g.:
```
java -cp "lib/*" run.server.Server -f cfg/server-alt.cfg
```

You could start by using the default `server.cfg` file already present within the `cfg` folder. In general the only field that you may be interested in configured is the 'allowedGateways', that specifies the EUIs of the gateways that are authorized to connect to (and exchange messages with) the server. However, if the field is not present, any gateway can connect to the server.

Probably the only other configuration that you have to set is within the `server-devices.json` file (or equivalent, if you changed the name in the `deviceFile` filed of the server configuration file), that specifies the configuration of the registered devices (DevEUI, JoinEUI, and AppKey). See below for datails.


The default `server.cfg` file contains the following configuration (note that character '#' can be used to comment a line):
```
{
	"homeNetId":  "000001",
	
	"port": 1700,
	
	"deviceFile": "cfg/server-devices.json",
	
	"stateFile": "cfg/server-state.json",
	
#	"allowedGateways": [],

	"managementPort": 4998,
	
#	"httpConnector": {
#		"port": 4999,
#		"endpoints": [
#			{ "soaddr": "127.0.0.1:8000", "authToken": "PASS1" },
#			{ "authToken": "PASS2" }
#		]
#	},

#	"coapConnector": {
#		"port": 4999,
#		"endpoints": [
#			{ "soaddr": "127.0.0.1:8000", "authToken": "PASS1" },
#			{ "authToken": "PASS2" }
#		]
#	},

#	"mqttConnector": {
#		"broker": "127.0.0.1:1883",	
#		"user": "testuser",
#		"passwd": "passwd"
#	},
	
	"log": {
		"fileName": "log/server.log",
		"rotations": 7,
		"maxSize": 1000000
	}	
}
```

The `homeNetId` field specifies the identifier of the LoRaWAN network administrated by the server. If you you don't have to interact with other network you can keep the default ID "000001" that is one of the two IDs (0x000000 and 0x000001) officially reserved for private use.

The `port` field specifies the UDP port where the Network Server listen for packets sent by the LoRaWAN gateways. Currently the standard Semtech protocol is used between by the gateways for communicationg with the Network Server. UDP port 1700 is the default one and can be also omitted.

The `deviceFile` field specifies the name of the file that list the registered devices. The default value is `cfg/server-devices.json`. This JSON file contains the setting of the registered devices (DevEUI, JoinEUI, and AppKey). 

The `stateFile` field specifies the name of the file used to store the server state. This is used when you want to stop and restart the server without loosing the curent state (associated gateways, joined devices, etc.).

The `allowedGateways` field specifies the EUIs of the gateways that are authorized to connect to (and exchange messages with) the server. If the field is not present, any gateway can connect to the server.

The `managementPort` field specifies the TCP port used by the server to provide a HTTP-based REST interface for monitoring the current state (registered gateways, joinined deivces, last received device payload, etc.).

The `log` field specifies the file used to write log message, the numbef of file rotations, and the maximum file size. When the maximum size is received no more log messages are written.

Then there are three fields `httpConnector`, `coapConnector`, and  `mqttConnector` for configuring three possible different interfaces that can be used by external applications for receiving and/or sending data from/to LoRaWAN devices.

The various interface sub-fields are almost straightforward.





## Running the server

Once the configuration files are correctly set, you can run the server by using the following command:
```
java -cp "lib/*" run.server.Server
```

With option '-f' followed by a file name it is possible to set a different server configuration file.
With option '-v' or '-vv' it is possible tu run the server in _verbose_ or _very verbose_ mode, respectively.

Use '-h' to list all possible command-line options.

