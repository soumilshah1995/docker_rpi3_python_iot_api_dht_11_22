# Raspberry Pi 3 IoT Demo using Docker &amp; Python 2.7 to read a DHT11 or DHT22 Temperature and Humidity Sensor using a RESTful API

The Dockerfile in this repo can be used to build an IoT demo container that runs a Python 2.7 application that will work with the GPIO pins configured to match the following setup :



The docker image can be found here: 


To build the dockerfile on a raspberry pi 3 after cloning this repository: 
```bash
docker image build --tag allthingscloud/rpi3-python-iot-api-dht -f Dockerfile . 
```

Launch as follows:
```bash
docker container run -d -p 4321:8989 --name my-python-iot-demo --device /dev/gpiomem allthingscloud/rpi3-python-iot-api-dht
```
# Verification
## Using curl
```bash
curl http://raspberry-pi-ip-address:4321/   <-- Returns the status of the LED
						  
curl http://raspberry-pi-ip-address:4321/17/on   <-- Turns on the LED attached to GPIO17 and Returns a json status response
						       
curl http://raspberry-pi-ip-address:4321/17/off   <-- Turns off the LED attached to GPIO17 and Returns a json status response
```
							
							
## Using a browser
Navigate to :
```bash
http://raspberry-pi-ip-address:4321/   <-- Returns the status of the LED
					     
http://raspberry-pi-ip-address:4321/17/on   <-- Turns on the LED attached to GPIO17 and Returns a json status response
						  
http://raspberry-pi-ip-address:4321/17/off   <-- Turns off the LED attached to GPIO17 and Returns a json status response
```


# Raspberry Pi 3 - Docker Installation
Please check the official documentation at https://docs.docker.com

I used the following steps :

```bash

sudo apt-get update

sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
	
curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg | sudo apt-key add -
sudo apt-key fingerprint 0EBFCD88

echo "deb [arch=armhf] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") \
     $(lsb_release -cs) stable" | \
    sudo tee /etc/apt/sources.list.d/docker.list   
   
sudo apt-get update

sudo apt-get install docker-ce

```