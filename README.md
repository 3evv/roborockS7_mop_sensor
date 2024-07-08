# roborockS7_mop_sensor
A DIY tutorial for fixing mop not detected on Roborock S7 by overriding/changing the sensor. 

# Hello!

This is a short guide how to bypass the sensor determining if the mopping tray is installed on roborock s7.

The presence of the mopping platform/rig is detected via a hall(magnetic field) sensor. I firmly belive its the C6111 sensor listed [here](https://www.lcsc.com/product-detail/Magnetic-Sensors_Cross-chip-CC6111ST_C285991.html), with schematic available [here](https://datasheet.lcsc.com/lcsc/2304140030_Cross-chip-CC6111ST_C285991.pdf). The proper way would be the replace the sensor, but given that the failure mode is liquid damage on the board that contains it and rest of the circuit might fail in recent future, I advise against changing it. I just shorted two pins of the cable responsible for delivering voltage and recieving data from the board and it forced a mop detection.

### TL:DR : Use prefered method: short sensing pin to +Vcc via resistor. Be **warned** that it ignores the actual state of the mop tray, duh.

## The fix: 
![Fixed_module](https://github.com/3evv/roborockS7_mop_sensor/assets/26227520/34bfc63f-e0dc-486b-a130-800c3034ae96)

Confirm with the app that the missing mop changes it's status to detected before assembly, and double check your connection - liquid damaged contacts tend to make poor soldiering surfaces, and a "cold" connection happened to me after the robot bumped into a wall (temporary fix with a fistbump was successful), despite cleaning it with IPA - had to dissasemble the thing twice :<, but I confirm it works.  

## Explanation: 

![fix2](https://github.com/3evv/roborockS7_mop_sensor/assets/26227520/2b39fb93-d6ee-42c2-98fb-98e536db93bb)

- Blue - Ground 
- **Yellow** - Sensing wire for the Hall sensor - use as output. 
- **Red** - Vcc, in my case it read about 3.2 V - connect to _Yellow_ with a smd resistor (10k Ohm in my case) - you can replace the hall sensor with your resistance.
- Green - ~~Don't know what it does, prob. better to leave it alone.~~ 

~~Use your preffered method of shorting the two connections.~~ 
Use resistor to fool the controller that the hall sensor is working properly. I suggest experimenting what combination of rezistances works for your board, since water damage makes things unpredictable, as I experienced myself. Consider using a voltage divider - in my case it worked fine with only 1 resistor. (These are just symbolic colours, not the ones on the wire connecting to the module!)

## Photos of the module, 
![board 2](https://github.com/3evv/roborockS7_mop_sensor/assets/26227520/5f33c0ca-ea53-4d74-9158-61d39c83c23f)
![board 1](https://github.com/3evv/roborockS7_mop_sensor/assets/26227520/d8520071-2375-4e97-94e1-8ac15c455db4)
## and its general location:
![general 1 (3)](https://github.com/3evv/roborockS7_mop_sensor/assets/26227520/53b792dd-6453-4767-8672-6d70a2fa0f4a)
- L - left, R - right, F - front, B - back
- Directions when the robot is on the floor, belly down, facing away from you. 
![general 1](https://github.com/3evv/roborockS7_mop_sensor/assets/26227520/2d603d01-51bd-47c2-9ee4-9a9223e6888a)
![general 2](https://github.com/3evv/roborockS7_mop_sensor/assets/26227520/2f4949fc-d878-406b-83c6-606b7c0dde54)
# Endnote: 
I am not responsible for the damage **you did**. Its a dirty, and in a best case scenario, temporary fix until you replace the mopping module. If you brick your device, it is your own fault. 
### And remember, since you bypassed a safety check, the robot might: 
- Give you up
- Let you down
- Ride around and desert you
- Make you cry
- Say goodbye
- Tell lies _(the tray is installed)_ and hurt you _(by eating your delicious headphone wires)_
