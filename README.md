# Lorawan Server

LoRaWAN server platform, intergating in a single application a LoRaWAN Network Server, Join Server, and Application Server.

Running the LoRaWAN server is very simple and all you need is:
- a Java Runtime Environment (JRE) installed (Java 17 or above);
- the jar files located in the `lib` folder;
- configure the server.cfg and devices.cfg files located within the `cfg` folder.

See the following "Server configuration" section for a simple guide on how to set the two configuration files.

Once the server has been correctly configured, you can run it by executing the following command:
```
java -cp "lib/*" run.server.Server -f cfg/server.cfg
```

More running options are described in the "Running the server" section.


## Server configuration

[TODO]


## Running the server

[TODO]