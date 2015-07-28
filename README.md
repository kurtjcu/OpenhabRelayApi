# OpenhabRelayApi
using openhab on a Rpi to control some relays - to be controlled remotely via openhab API and connected to BomScraperPy


This project is to control some relays from openhab on a rpi.

Using default raspbian install as of 28/07/15 (installed from noobs1.4).

1. install noobs on sd card.
2. boot Rpi with sd card and install raspbian.
3. get wireless card working with Rpi
4. install openhab - from http://www.instructables.com/id/OpenHAB-on-Raspberry-Pi/
5. install openhab gpio binding - from https://github.com/openhab/openhab/wiki/GPIO-Binding via apt-get
6. configure openhab to use gpio.
7. Test openhab talking to gpio.


or

3. install openhab gpio binding - from https://github.com/openhab/openhab/wiki/GPIO-Binding via apt-get
4. test gpio via commandline.
5. install openhab runtime.
6. test openhab runtime.
7. configure gpio in openhab.
8. test gpio from openhab interface.s



downloading 
-----------
```
wget https://bintray.com/artifact/download/openhab/bin/distribution-1.7.0-runtime.zip
wget https://bintray.com/artifact/download/openhab/bin/distribution-1.7.0-addons.zip
wget https://bintray.com/artifact/download/openhab/bin/distribution-1.7.0-demo-configuration.zip
```



Core
----
```
sudo mkdir /opt/openhab
cd /opt/openhab/
/opt/openhab $ sudo unzip /home/pi/distribution-1.7.0-runtime.zip

```
