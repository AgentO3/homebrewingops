
![bg-40](img/supplies.jpg)

# HomebrewOps

Adding Automation and <br> Control to The Hobby of Homebrewing

---

![bg-40](img/supplies.jpg)

# Homebrewer Evolution

---

![bg-100](img/mrbeer.png)

---

![bg-40](img/5gallon.jpg)

# 5 Gallon Batches

---

![bg-40](img/mashbag.jpg)

# Partial Mash

---

![bg-40](img/kegs.jpg)

# Kegging

---

![bg-40](img/allgrain.jpg)

# All Grain

---

![bg-40](img/flight.jpg)

# What's Next?

---

![bg-100](img/tworoads.jpg)

---

![bg-40](img/bottling.jpg)

## Quality & Consistency = Control

---

![bg-40](img/owen.jpg)

# About Me

---

![bg-40](img/pipes.jpg)

# Delivery Pipelines

---

![bg-40](img/matrix.gif)

# Virtual Engineer

---

![bg-40](img/hops.jpg)

# Putting Ops in Hops

---

![bg-20](img/brewfactory.jpg)

# 1) Avoid Premature Optimization

---

![bg-20](img/brewfactory.jpg)

## Rise of The BrewBots

---

![bg-20](img/brewfactory.jpg)

![](img/picobrew.jpg)

---

![bg-20](img/brewfactory.jpg)

![](img/brewbot.jpg)

---

![bg-20](img/brewfactory.jpg)

![](img/brewie.jpg)

---

![bg-20](img/brewfactory.jpg)


# 2) Make it Work

---

![bg-20](img/brewfactory.jpg)

![](img/brewdaytasks.png)

---

![bg-20](img/brewfactory.jpg)

![](img/brewdaywait.png)


---

![bg-20](img/brewfactory.jpg)

![](img/first-timer.jpg)

---

![bg-40](img/homebrewbot.jpg)

# Then Make It Great

---

![bg-20](img/brewfactory.jpg)

### The HomebrewOps Loop

![](img/brewloop.png)

---

![bg-20](img/brewfactory.jpg)

## Adding Plumbing

![](img/addvalve.jpg)

---

![bg-20](img/brewfactory.jpg)

### Lowes 10 Gallon Mash Tun

![](img/lowesmash.jpg)

---

![bg-40](img/brewtron.jpg)

## Meet BrewTron

![](img/assemble.gif)

---

![bg-40](img/brewtron.jpg)


MashTron<br/>BoilTron<br/>FermentTron

---

![bg-40](img/brewtron.jpg)

RaspberryPI<br/>DS18B20 Sensor<br/>NodeJS<br/>Cylon.js

---

![bg-100](img/brewtron.jpg)

---

![bg-100](img/setup.jpg)

---

![bg-20](img/brewfactory.jpg)

### Preparing the PI

<div class="code">
sudo modprobe w1_gpio && sudo modprobe w1_therm
</div>

---

![bg-20](img/brewfactory.jpg)

### Preparing the PI

<div class="code">
echo "w1_gpio" >> /etc/modules
echo "w1_therm" >> /etc/modules
</div>

---

![bg-20](img/brewfactory.jpg)

### Reading Sensor Data

<div class="code">
/sys/bus/w1/devices/28-0000066fc63a/w1_slave
</div>

---

![bg-20](img/brewfactory.jpg)

### Reading Sensor Data

<div class="code">
56 01 4b 46 7f ff 0a 10 d1 : crc=d1 YES
56 01 4b 46 7f ff 0a 10 d1 t=21375
</div>

---

![bg-20](img/brewfactory.jpg)

### Reading Sensor Data

<div class="code">
56 01 4b 46 7f ff 0a 10 d1 : crc=d1 YES
56 01 4b 46 7f ff 0a 10 d1 <span class="highlight">t=21375</span>
</div>

---

![bg-20](img/brewfactory.jpg)

### Reading Sensor Data

<div class="code">
21375 / 1000 = <span class="highlight">21.375 C<span>

21.375 * 9/5 + 32 = 70.475 F
</div>

---

![bg-20](img/brewfactory.jpg)

### Reading Sensor Data

<div class="code">
21375 / 1000 = 21.375 C

21.375 * 9/5 + 32 = <span class="highlight">70.475 F</span>
</div>

---

![bg-20](img/brewfactory.jpg)

# Cylon.js Intro

---

![bg-20](img/brewfactory.jpg)

### Robot

<div class="code">
<span class="highlight">var Cylon = require('cylon')</span>
...
Cylon.robot({
  work: function(my) {
    # Do Stuff
...
}).start();
</div>

---

![bg-20](img/brewfactory.jpg)

### Robot

<div class="code">
var Cylon = require('cylon')
...
<span class="highlight">Cylon.robot({
  work: function(my) {
    # Do Stuff</span>
...
}).start();
</div>


---

![bg-20](img/brewfactory.jpg)

### Robot

<div class="code">
var Cylon = require('cylon')
...
Cylon.robot({
  work: function(my) {
    # Do Stuff
...
<span class="highlight">}).start();</span>
</div>

---

![bg-20](img/brewfactory.jpg)

### Connections

<div class="code">
...
Cylon.robot({
  <span class="highlight">connections: {
    robot: { adaptor: "loopback" }
    },</span>
  work: function(my) {
    my.robot.emit("some-event");
...
</div>

---

![bg-20](img/brewfactory.jpg)

### Connections

<div class="code">
...
Cylon.robot({
  connections: {
    robot: { adaptor: "loopback" }
    },
  work: function(my) {
    <span class="highlight">my.robot.emit("some-event");</span>
...
</div>

---

![bg-20](img/brewfactory.jpg)

### Devices

<div class="code">
...
Cylon.robot({
  ...
  <span class="highlight">devices: {
    lcd: { driver: 'lcd' }
  },</span>
  ...
  work: function(my) {
    my.lcd.print("Hello!");
...
</div>


---

![bg-20](img/brewfactory.jpg)

### Devices

<div class="code">
...
Cylon.robot({
  ...
  devices: {
    lcd: { driver: 'lcd' }
  },
  ...
  work: function(my) {
    <span class="highlight">my.lcd.print("Hello!");</span>
...
</div>

---

![bg-20](img/brewfactory.jpg)

### Utilities

<div class="code">
...
  work: function(my) {
    <span class="highlight">every((10).seconds(), function(){
      my.sampleTemp(my);</span>

      my.when(my.currentTemp >= my.waterTemp, function(){
        my.robot.emit("heat-water");
    });
...
    my.robot.once("heat-water", function(){
    # Only do this once
...
</div>

---

![bg-20](img/brewfactory.jpg)

### Utilities

<div class="code">
...
  work: function(my) {
    every((10).seconds(), function(){
      my.sampleTemp(my);

      <span class="highlight">my.when(my.currentTemp >= my.waterTemp, function(){
        my.robot.emit("heat-water");</span>
    });
...
    my.robot.once("heat-water", function(){
    # Only do this once
...
</div>

---

![bg-20](img/brewfactory.jpg)

### Utilities

<div class="code">
...
  work: function(my) {
    every((10).seconds(), function(){
      my.sampleTemp(my);

      my.when(my.currentTemp >= my.waterTemp, function(){
        my.robot.emit("heat-water");
    });
...
    <span class="highlight">my.robot.once("heat-water", function(){
    # Only do this once</span>
...
</div>

---

![bg-40](img/measure.jpg)

# 3) Measure All The Things

---

![bg-20](img/brewfactory.jpg)


# StatsD

---

![bg-20](img/brewfactory.jpg)


# Librato

---

![bg-20](img/brewfactory.jpg)


![](img/graph2.png)

---

![bg-20](img/brewfactory.jpg)


# 4) Worst is Better

---

![bg-20](img/brewfactory.jpg)

![](img/tweet.png)

---

![bg-20](img/brewfactory.jpg)

# 5) The Backlog

---

![bg-20](img/brewfactory.jpg)


### Pumps

![](img/pump.jpg)

---

![bg-20](img/brewfactory.jpg)


## Solenoid Valves

![](img/valves.jpg)

---

![bg-20](img/brewfactory.jpg)

### Water Volume Sensor

---

![bg-20](img/brewfactory.jpg)


### Cloud Controller

---

![bg-20](img/brewfactory.jpg)


# Build A Community

---

![bg-20](img/brewfactory.jpg)

![](img/diybrewbot.jpg)

---

![bg-20](img/brewfactory.jpg)

![](img/chiller.jpg)

---

![bg-20](img/brewfactory.jpg)

![](img/bubblelogger.jpg)

---

![bg-20](img/brewfactory.jpg)

![](img/gravitysensor.jpg)

---

![bg-20](img/brewfactory.jpg)

![](img/fermentationchamber.jpg)

---

![bg-20](img/brewfactory.jpg)

![](img/propane.jpg)

---

![bg-20](img/brewfactory.jpg)


## Open Homebrewing Automation Project

https://github.com/open-homebrewing-project

---

## Thank You!

![bg-20](img/brewfactory.jpg)

![](img/doge.jpg)


---

![bg-20](img/brewfactory.jpg)

## References

[DS18B20 Wiring and Setup for RaspberryPI](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-11-ds18b20-temperature-sensing/hardware) <br/> [More info on DS18B20](http://www.tweaking4all.com/hardware/arduino/arduino-ds18b20-temperature-sensor/) <br/> [What Modules you will need](http://www.reuk.co.uk/DS18B20-Temperature-Sensor-with-Raspberry-Pi.htm) <br/> [Installing Node.js on RaspberryPI](http://weworkweplay.com/play/raspberry-pi-nodejs/) <br/> [Prevent Wifi Sleep](http://electronut.in/preventing-raspberry-pi-wifi-from-going-into-sleep-mode/) <br/> [Cylon.js Docs](http://cylonjs.com/documentation/guides/working-with-robots/)

---

![bg-20](img/brewfactory.jpg)

## Code

[MashTron](https://github.com/open-homebrewing-project/mashtron) <br/> [BoilTron](https://github.com/open-homebrewing-project/boiltron) <br/> [FermentTron](https://github.com/open-homebrewing-project/fermentron)
