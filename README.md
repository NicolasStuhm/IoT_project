# Greenhoues monitoring
Nicolas Stuhm | ns223de

The device resulting from this project should be installed in/on a greenhouse and has the following capabilities: it measures the temperature in the greenhouse and based on the values obtained, a door is opened. It comes furthermore with a movement detector, which notifies the user via a message on the phone when triggered, as there might be a cat or rabbit in the greenhouse.

### Estimated time needed for this project: 3 hours
<br>

# Objective
The reason I chose this project is that I myself am living on a farm together with some friends of mine and I intend to make our lives a little easier with this device. The temperature sensor makes it unnecessary to walk to the remote greenhouse, as it lets the user observe the values online. Based on those, one can estimate how often the plants need water throughout the day and furthermore, the door of the greenhouse opens automatically in the morning, when the temperature rises above a certain temperature. Previous cases have led me to include a motion detector, as there had been cats or other animals digging in the soil or destroying the tomato- or other plants.

The insights this project will hopefully provide to those reproducing it are:
- a general understanding of how IoT devices operate
- some knowledge about electronic circuits
- some knowledge about coding in (micro)python
- the capability to work with IFTTT as well as adafruit.io
<br><br>

# Material
| component                                                                                                                                                                  | purpose                                                                                                                                  | where to buy   | cost         |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|----------------|--------------|
| RPI Pico W ![pico w](https://m.media-amazon.com/images/I/41FwT1rutlL.jpg)                                                                                                  | This is the microcontroller, which is taking care of connecting to the internet and managing the other electronic parts of this project. | electrokit.com | in a package |
| Jumper wires ![jumper wires](https://lawicel-shop.se/images/zoom/11026-jumper_wires_standard_7in._m_m_-_30_awg__30_pack_-01.jpg)                                           | The jumper wires server the purpose of connecting the different parts of the project with eachother.                                     | electrokit.com | in a package |
| Breadboard ![breadboard](https://cdn.sparkfun.com/assets/d/c/a/b/4/513a1dface395fa524000001.JPG)                                                                           | The breadboard is the base, where connections from the pico to for instance the relay are made.                                          | electrokit.com | in a package |
| Relay ![relay](https://quickbutik.imgix.net/7394y/products/5e0298f64b2f9.jpeg?auto=format)                                                                                 | The relay activates the electromagnetic lock when told so by the pico.                                                                   | ebay.com       | 10 kr        |
| Electromagentic lock ![elect. lock](https://i.ebayimg.com/images/g/dGkAAOSwDvxiqFoP/s-l1600.jpg)                                                                           | This lock keeps the door closed until activated by the pico, which leads the door to swing open.                                         | ebay.com       | 50 kr        |
| PIR motion sensor ![pir sensor](https://teknikprojektet.se/wp-content/uploads/2020/04/pir.jpg)                                                                             | This sensor detects motion in the greenhouse, for instance from unwanted visitors like cats or rabbits.                                  | ebay.com       | 20 kr        |
| Batteries ![batteries](https://i5.walmartimages.com/asr/829fe603-6500-40ff-a678-9e62c4ca2a4a.9e886b05ead4c0ca2b36eeaa9711251c.png?odnHeight=612&odnWidth=612&odnBg=FFFFFF) | Eight of these AA batteries connected in series are necessary to provide the electromagnetic lock with enough volts(12) to open.          | ICA            | 50 kr        |

In addition, I build a little box out of wood, as I needed some kind of container to connect the eight batteries in series.
<br><br>


# Setup
My subject of studies lies within the realm of IT, so I did not have to go about installing a lot of software. The IDE I am using is Visual Studio Code, with the plugins flake8 and Pico-W-Go. I had, in the beginning, installed Thonny, in order to test and try it, however, I thought it is somewhat limited and one would have more opportunities using VS code.<br>
The flashing, that is the installation of the new firmware (uf2 file), I had to do on a different computer, as mine did not recognise the pico W as mass storage space and I was therefore not able to copy the file needed to it. The process is simple. One must plug the pico W in with an USB cable, while holding down the BOOTSEL button on the board. Now the computer should "see" the micorcontroller like a simple USB stick and a certain file containing firmware, which can be found online must be copied to it. After that, disconnect and connect the pico W again.<br>
Another problem arose during connecting the pico W to my IDE. I had to disable the "Auto Connect" option in the Pico-W-Go extension and specified the port "COM6" in the "Manual Com Device" (also part of the Pico-W-Go extension), in order for it to work.<br>

For you with a well functioning laptop this might not be necessary, but I also had to install a new driver for the pico w to be recognised by my computer.
<br><br>

# Physical- and web connectivity
The wiring is fairly simple and can be seen in figure one. Both the relay and the PIR sensor are connected to a ground- and 3 volts rail at the bottom of the breadboard, which is connected to the pico W. The relay is furthermore connected to pin GP16 and the sensor to GP0 on the microcontroller. There are two more terminals used on the realy: COM (common) and NC (normally closed). The COM port is connected with the positive terminal of the batteries, while the NC is connected to the positive end of the electromagnetic lock (represented by a resistor in the diagram). The circuit is then closed by a connection between the negative terminal of the lock and the ground of the batteries.<br><br>
![diagram](pictures/diagram.png)
_Figure one, physical setup diagram_<br><br>

When starting the project, I intended to use a transformer or two 9 volt batteries and limit them down to 12 volts with a 10k and 15k resistor, however the final descision fell on eight 1.5 volts batteries connected in series to get the desired output. This setup is the most energy- and cost efficient solution, which in theory could be used for production.

Concerning the websites and platforms, I am using adafruit io and IFTTT. Adafruit is a website, which provides so called "feeds" which accept data from for example a microcontroller. I am using two different feeds, one for the temperature and one to monitor if the pir sensor has detected motion. This data is the visualised by a different tool within adafruit: the dashboard. <br>
With the other service, IFTTT, one can create applets, which in my case read certain values from one of my afruit feeds and send a message to my phone that the pir sensor had been triggered. The limit is at two applets, however one can choose a paid subscription to unlock more.

# The code
not in its final state yet, coming soon

# Connectivity
I am using wifi and the MQQT protocol to send data from my microcontroller to the adafruit website. I decided to send a temperature reading every half an hour and the pir sensor, obviously, sends whenever it is triggered. The second platform, IFTTT (installed on my phone), is connected via a webhook to the adafruit website and pops a notification whenever a previously defined value arrives in the adafruit feed. 


# Final thoughts
This project did not go as intended as firstly non of the hardware worked (due to my laptop I guess) and second, midway through the course I found out that my project had to act upon sensory data and I therefore had to shift my it completely.<br><br>
In addition, I am certainly not satisfied with the final product and would like to implement a few more things. I wanted to buy a new DHT11, as mine burned out in the last week, such that I could show a humidity measurement on my dashboard and act upon those readings. Other ideas are soil moisture sensor to check when the plants need more water or a buzzer, which is beeping at a certain frequency, in order to scare away cats or other animals.

On the positive side, the courese touched on many aspects of the IoT and I am happy I could extend my knowledge a bit.
