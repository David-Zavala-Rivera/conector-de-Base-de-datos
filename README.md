# Subscriptor a TOPIC MQTT
#programa que ealiza una conexión al topic MQTT

import paho.mqtt.client as mqtt
import time
from SensorBase import SensorBase

def on_connect(client,userdata,flags,rc):
    client.subscribe("sensor/temperatura")

def on_message(client,userdata,msg):
    print(time.strftime("%d-%m-%Y %H:%M:%S", time.localtime())+" "+msg.topic+"$
    sensor = SensorBase(msg.topic,msg.payload)
    sensor.guardar()
    sensor.mostrar()    

client = mqtt.Client()
client.on_connect = on_connect
client.on_message = on_message
print("Esperando...")
client.connect("localhost",1883,60)
client.loop_forever()
