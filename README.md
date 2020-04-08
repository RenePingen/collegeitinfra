# Introduction
This repository contains lab examples for IT infrastructure lectures on virtualization and cloud. The content will be handled in more detail in the lectures. This manual consist of two parts: reading material and hands-on lab. The reading material and labs help in understanding the concepts of virtualization and container technology.

## Reading material
Read through the following pages to get an understanding of virtualisation and container technology:
https://www.freecodecamp.org/news/a-beginner-friendly-introduction-to-containers-vms-and-docker-79a9e3e119b/
https://www.freecodecamp.org/news/docker-simplified-96639a35ff36/ ( this second link already contains some practical examples)

## Lab excercises
Based on the instructions in the second link you can choose to use play-with-docker (https://labs.play-with-docker.com/) or install docker on your own computer.

The instructions below are based on play-with-docker. Also watch the video in this repository for an explanation.

### 1. Launch the docker helloworld application

Vanuit de docker console (het scherm waar je docker kunt aansturen), kun je docker commando's uitvoeren. Voer het volgende commando uit:
"docker run hello-world"
Dit zal als het goed is het resultaat geven:
"
Hello from Docker!
This message shows that your installation appears to be working correctly.
"
	2. Start een simpele webserver in docker
In dit lab gaan we een simpele webserver starten die via de browser te bereiken is. 
Voer het volgende commando uit:
docker run -d -p 80:80 nginx

	3. Start een eigen webapplicatie in docker
Start nu een eigen webapplicatie. Hiervoor is het verstandig om een nieuwe instance aan te maken in playwithdocker door op de knop "add new instance" te drukken.
Voer het volgende commando uit om een webapplicatie op te halen:
git clone https://github.com/RenePingen/collegeitinfra.git

Optioneel: pas de website aan
Gebruik de editor om het bestand index.html in de map collegeitinfra/Webserverdemo aan de passen. In de docker webomgeving (play-with-docker), klik op editor, navigeer naar het bestand index.html en open het bestand. Pas de tekst aan en sla op

Bouw de image
Bouw de image van de webapplicatie als docker container met het volgende commando:
docker build -t webserverdemo collegeitinfra/Webserverdemo/

Start een docker container met de webapplicatie
Voer het volgende commando uit:
docker run -d -p 80:80 webserverdemo
Test de image
In play with docker, klik op het poortnummer 80 of klik "open port" en vul dan 80 in.

	3. Lanceer een virtuele desktop met een webinterface

Optioneel: Maak een eigen docker image en lanceer deze


docker run -d -p 5901:5901 -p 6901:6901 consol/centos-xfce-vnc





