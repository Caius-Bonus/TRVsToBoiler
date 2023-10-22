# TRVsToBoiler
A collection of blueprints to control a boiler with multiple Smart Thermostatic Radiator Valve knobs (without a Room Thermostat)

## Background

Old fashioned heating systems have a boiler, a central thermostat in the living room and radiators in every room. 
All radiators in the living room have valves that are open-close.
All radiators in the other rooms were a long time also open-close. Later this was replaced with Thermostatic Radiator Valves. These valves would be closed partly or fully depending on the temperature in the room and setting. The living room in this situation always has to be heated to be able to heat other rooms.

Boilers self-modulate to the correct water temperature and flow (to a certain extent). These boilers can be communicated with through on-off signals using any kind of switch like a mercury thermostat. Boilers can also support the OpenTherm protocol. This protocol allows for control over different aspects of the boiler including heating.

## Solution

You want a boiler to produce heat for the rooms you are in and not the rooms you are not in. For this there are probably multiple solutions.
The solution in this project however is as follows:
There is no Room Thermostat, but only an OpenTherm Gateway, used to turn the boiler on and off.
Every radiator in the house is equipped with a Flow Rate Limited Thermostatic Radiator Valve, which is tuned to return a specific temperature (Heat Recovery Systems require low temperatures, also returning high temperature water loses more energy in the pipes below your house). 
Every Thermostatic Radiator Valve in a room that needs to be independently heated is equipped with a Smart TRV knob. This knob indicates whether a room requires heat or not. This information triggers an automation which requests heat from the Boiler using the OpenTherm Gateway. 

Smart TRV knobs are unfortunately pricey and not water-proof. Therefore, it is best to buy quality Dumb TRV knobs for the rooms that can reasonably be heated alongside other rooms or are too humid for the Smart TRV knob. These will open, when it gets too cold, to protect the system and when heat is required and a smart TRV knob is also requesting. Example: The shower is too humid for a smart TRV knob, but you want to go to the office right after the shower. You can open the dumb TRV knob in the shower and the smart TRV knob in the office.

This way even in the living room, it is possible to use TRVs, because if no TRV knob requests heat, the OpenTherm Gateway stops requesting heat from the boiler.

Smart TRV knobs provide a way to close the valve, a way to set the temperature for a room and an algorithm for heating a room without overshooting.

## Specifics

Currently used valves (not guarantee):
  - Danfoss Ally (and derivatives): Zigbee Connection and runs well and long on Ni-Mh batteries (might complain about the voltage, but it will work if you have high quality batteries that don't have high self-discharge).

The 3 Blueprints provided are:
  - Boiler Request Heating:
  
    This requests heat from the boiler when one of the TRV knobs requests heat.
    
  - Sync TRV External Temp:

    This synchronizes the external temperature sensor between the TRV knobs in the room.
    
  - TRV Group:

    This synchronizes the setpoint between TRV knobs in the same room after a change.
