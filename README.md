# Demo

some description!
from gpiozero import LED
from signal import pause
from time import sleep
import paho.mqtt.client as mqtt

led = LED(24)

def on_connect(client, userdata, flags, rc):
    print("connected" + str(rc))
    client.subscribe("Final Exam")
    
def on_message(client,userdata, msg):
    print(msg.topic+ " "+str(msg.payload))
    
    if msg.payload == "TOGGLE":
        led.toggle()
        print("Received: TOGGLE")
        

client = mqtt.Client()
client.on_connect = on_connect
client.on_message = on_message

client.connect("161.200.199.2", 1883,60)

client.loop_forever()

------------------------------------------------------------

from gpiozero import Button
import paho.mqtt.publish as publish
from signal import pause

button = Button(25)

def msg():
    publish.single("Final Exam", "Pharunyu Laowahutanon", hostname = "161.200.199.2")
    print("Done")
    
button.when_pressed = msg

pause()

---------------------------------------------------------

import paho.mqtt.publish as publish

publish.single("Final Exam","TOGGLE", hostname="161.200.199.2")
print("Done")




