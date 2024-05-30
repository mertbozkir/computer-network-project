# Computer Networks Term Project

## Overview
This project investigates the performance of a wireless communication technology, such as LoRaWAN, under the influence of mobility. The project utilizes simulations for performance measurement, with a focus on realistic mobility simulation using traffic simulators like SUMO.

## Project Structure
The project directory contains the following files:

- `randomtrip.py`: Python script for generating random trips based on the network.
- `spiderman.net.xml`: XML file describing the network topology.
- `spider.rou.alt.xml`: Alternative route file for the simulation.
- `spider.rou.xml`: Main route file for the simulation.
- `spider-sim.sumo.cfg`: SUMO simulation configuration file.
- `sumoTrace.xml`: Detailed simulation trace output file.
- `trips.trips.xml`: Generated trip file based on the network.

## Prerequisites
- ns-3 simulator (https://www.nsnam.org) for LoRaWAN simulations.
  - LoRaWAN module: https://github.com/signetlabdei/lorawan
- SUMO traffic simulator (https://eclipse.dev/sumo/) for realistic mobility simulation.

## Installation
### ns-3 Installation
1. Download ns-3:
   ```
   wget https://www.nsnam.org/releases/ns-allinone-3.41.tar.bz2
   ```
2. Extract the downloaded archive:
   ```
   tar xfj ns-allinone-3.41.tar.bz2
   ```
3. Navigate to the ns-3 directory:
   ```
   cd ns-allinone-3.41/ns-3.41
   ```
4. Configure and build ns-3:
   ```
   ./ns3 configure --enable-examples --enable-tests
   ./ns3 build
   ```
5. Run tests:
   ```
   ./test.py
   ```

### SUMO Installation
Follow the installation instructions provided in the SUMO documentation.

## Network Generation
To generate the network topology, use the following command:
```
netgenerate --spider --spider.arm-number=7 --spider.circle-number=3 --spider.space-radius=200 -o spiderman.net.xml
```
This command creates a spider-like network with 7 arms and 3 circles.

## Trip Generation
To generate random trips based on the network, use the `randomtrip.py` script:
```
python3 randomtrip.py -n spiderman.net.xml -e 50
```
This script generates trips and saves them in the `trips.trips.xml` file.

## Route Generation
To generate routes based on the generated trips, use the `duarouter` command:
```
duarouter -n spiderman.net.xml --route-files trips.trips.xml -o spider.rou.xml --ignore-errors
```
This command generates routes and saves them in the `spider.rou.xml` file.

## Simulation
To run the simulation and obtain a detailed simulation trace, use the following command:
```
sumo -c spider-sim.sumo.cfg --fcd-output sumoTrace.xml
```
This command runs the simulation using the configuration file `spider-sim.sumo.cfg` and generates a detailed trace output in the `sumoTrace.xml` file.

## LoRaWAN Simulation
The project also includes a LoRaWAN simulation using the ns-3 simulator and the Adaptive Data Rate (ADR) algorithm. However, due to issues with the CMakeLists.txt file, the LoRaWAN simulation could not be completed.

## Conclusion
This project provides a foundation for investigating the performance of wireless communication technologies under the influence of mobility. The simulation setup and generated files can be used as a starting point for further analysis and experimentation.
