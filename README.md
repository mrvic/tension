# tension
Measure tension with Load cell and HX711, using NTC C.H.I.P and arduino mini


C.H.I.P

1) install and start node-red
----------------
```
chip@chip:~$ node-red
7 Feb 14:05:43 - [info] 

Welcome to Node-RED
===================

7 Feb 14:05:43 - [info] Node-RED version: v0.17.5
7 Feb 14:05:43 - [info] Node.js  version: v7.10.1
7 Feb 14:05:43 - [info] Linux 4.4.13-ntc-mlc arm LE
7 Feb 14:05:46 - [info] Loading palette nodes
7 Feb 14:05:54 - [warn] ------------------------------------------------------
7 Feb 14:05:54 - [warn] [rpi-gpio] Info : Ignoring Raspberry Pi specific node
7 Feb 14:05:54 - [warn] ------------------------------------------------------
7 Feb 14:05:54 - [info] Settings file  : /home/chip/.node-red/settings.js
7 Feb 14:05:54 - [info] User directory : /home/chip/.node-red
7 Feb 14:05:54 - [info] Flows file     : /home/chip/.node-red/flows_chip.json
7 Feb 14:05:54 - [info] Server now running at http://127.0.0.1:1880/
7 Feb 14:05:54 - [info] Starting flows
7 Feb 14:05:55 - [info] Started flows
7 Feb 14:05:55 - [info] serial port /dev/ttyS0 opened at 38400 baud 8N1

```
----------------
2) Import flow in the Node-red:


```
[{"id":"70835b45.824e04","type":"tab","label":"Flow 3","disabled":false,"info":""},{"id":"5064bb31.abdd94","type":"influxdb out","z":"70835b45.824e04","influxdb":"67b50be2.5101b4","name":"","measurement":"tlak","precision":"","retentionPolicy":"","x":781,"y":130,"wires":[]},{"id":"67a3cf78.d7c8","type":"debug","z":"70835b45.824e04","name":"","active":true,"console":"false","complete":"false","x":730,"y":360,"wires":[]},{"id":"81771af5.543ba8","type":"function","z":"70835b45.824e04","name":"dodajem arduino tag","func":"msg.payload.machine=\"arduino\"\n//msg.payload=Math.round(Math.random()*1000)\nmsg.payload=Math.round(msg.payload)\nreturn msg","outputs":1,"noerr":0,"x":405,"y":318,"wires":[["5064bb31.abdd94","67a3cf78.d7c8"]]},{"id":"c4226fb1.f17ad","type":"serial in","z":"70835b45.824e04","name":"CHIP UART serial","serial":"79139bc6.fb21c4","x":237.5,"y":441,"wires":[["81771af5.543ba8"]]},{"id":"67b50be2.5101b4","type":"influxdb","z":"","hostname":"192.168.2.100","port":"8086","protocol":"http","database":"chip","name":"chip","usetls":false,"tls":"ec1a7d5e.6f42f"},{"id":"79139bc6.fb21c4","type":"serial-port","z":"","serialport":"/dev/ttyS0","serialbaud":"38400","databits":"8","parity":"none","stopbits":"1","newline":"\\n","bin":"false","out":"char","addchar":false},{"id":"ec1a7d5e.6f42f","type":"tls-config","z":"","name":"","cert":"","key":"","ca":"","certname":"","keyname":"","caname":"","verifyservercert":true}]

```
-----------------


2) enable UART reading
```
sudo usermod -a -G tty chip
sudo systemctl stop serial-getty@ttyS0.service
sudo systemctl disable serial-getty@ttyS0.service
sudo chmod 660 /dev/ttyS0
sudo chown root:dialout /dev/ttyS0

```

3) Install influxDB
```
https://www.npmjs.com/package/node-red-contrib-influxdb
```

4) Install node-red bluetooth
```
https://flows.nodered.org/node/node-red-contrib-noble
```

5) Install node-red serialport
```
https://www.npmjs.com/package/serialport

MUST INSTALL FROM SOURCE !!!

sudo apt-get install build-essential
sudo npm install serialport --unsafe-perm --build-from-source

```




