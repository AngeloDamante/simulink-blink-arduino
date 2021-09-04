# Simulink and Arduino configuration
A simple repo to test principal components of Arduino Shield on Simulink with Matlab R2021a. This tests are made on Ubuntu (Linux Distro).

Requirements:

```
> MATLAB R2021a
> MATLAB Support Package for Arduino Hardware 
> Simulink Support Package for Arduino Hardware 
> Ubuntu 20.04 LTS
> Arduino Shield (Uno, Mega or others)
```

## Configuration
First we enable permissions for the port in question. The name changes depending on the shield.
```
> sudo chmod a+rwx /dev/ttyUSB0     # if we have an arduino clone shield
> sudo chmod a+rwx /dev/ttyACM0     # if we have an arduino original shield
```

Once that's done, let's move on to setting the baudrate in the matlab workspace. 
The possible choices are:
```
>> codertarget.arduinobase.registry.setBaudRate('sim_model_name', 9600)
>> codertarget.arduinobase.registry.setBaudRate('sim_model_name', 153660)
>> codertarget.arduinobase.registry.setBaudRate('sim_model_name', 230400)
```
with ```'sim_model_name'``` as name of simulnk model and 9600 is usually baudrate.


And now we switch to simulink by opening a blank model. In the first sheet that appears, let's go to:
```
Model Settings > Hardware Implementation 
    > Hardware Board: Arduino Shield (UNO, Mega, ...)
    > Target Hardware Resources
        > Host-board connection:
            > Manually /dev/ttyUSB0     # arduino clone
            > Automatically             # arduino original
```
with Model Settings in ```Prepare Toolbar```.

## Arduino Components
The ``` FooBlink.slx``` file is the model that I have tested with Led, Servo and HC-SR04 component (in ```Simulink Support Package for Arduino Hardware```). The simple circuit to first test is as follows:

### Led
With ```Digital Output``` block.
<p align=center>
    <img src=docs/led.png />
</p>

### Servo
With ```Standard Servo Write``` block.
<p align=center>
    <img src=docs/servo.png />
</p>

### HC-SR04
With ```Ultrasonic Sensor``` block.
<p align=center>
    <img src=docs/ultrasonic.png />
</p>