# OpenhabRelayApi
using openhab on a Rpi to control some relays - to be controlled remotely via openhab API and connected to BomScraperPy


This project is to control some relays from openhab on a rpi.

Using default raspbian install as of 28/07/15 (installed from noobs1.4).

#Workflow - to be edited

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


#Getting openhab

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

Bindings
--------

You should already be in "/opt/openhab"
```
cd addons/
sudo unzip /home/pi/distribution-1.7.0-addons.zip
cd ..
sudo cp configurations/openhab_default.cfg configurations/openhab.cfg
```


Demo
--------

You should still be in "/opt/openhab"
```
sudo unzip /home/pi/distribution-1.7.0-demo-configuration.zip
```


Running OpenHAB
---------------

start.sh will not be executable by default so....
You should still be in "/opt/openhab"
```
sudo chmod +x start.sh 
sudo ./start.sh
```

congratulations you should now see the OpenHAB OSGI server running.

using a web browser point it at http://[yourpiIPAddress}:8080/openhab.app?sitemap=demo

and you should see the demo :)


#OpenHAB Designer

Installation
------------
I wished to use my Rpi as a headless unit however I need to be able to edit config files in openhab designer on my local machine.
So after installing openhab designer on my local machine I needed to make the remote files accessable.

Share the OpenHAB installation.
-------------------------------
```
sudo passwd root
sudo apt-get install samba samba-common-bin 
sudo nano /etc/samba/smb.conf 
```

make the file look like
```
[openhab]  
   comment=OpenHAB  
   path=/opt/openhab  
   browseable=Yes  
   writeable=Yes  
   only guest=no  
   create mask=0777  
   directory mask=0777  
   public=no 
   
```

Then create share password

```
sudo smbpasswd -a root 
```

I then mapped the share on my local machine and opened in designer.

#configure gpio

change openhab.cfg in the gpio section.
---------------------------------------
(use ctrl+f to find "gpio")

uncomment the lines to look like
```
################################### GPIO Binding ######################################

# Optional directory path where "sysfs" pseudo file system is mounted, when isn't
# specified it will be determined automatically if "procfs" is mounted
gpio:sysfs=/sys

# Optional time interval in miliseconds when pin interrupts are ignored to
# prevent bounce effect, mainly on buttons. Global option for all pins, can be
# overwritten per pin in item configuration. Default value if omitted: 0
gpio:debounce=10
```

install package for native JNA library
--------------------------------------
```
sudo apt-get install libjna-java
```

you need to add a parameter in command line which starts openHAB and specify 
the path to JNA library, e.g. edit the last line in "start.sh" and 
append
```-Djna.boot.library.path=/usr/lib/jni \``` 
right after java \.


```
echo Launching the openHAB runtime...
java \
    -Djna.boot.library.path=/usr/lib/jni \
	-Dosgi.clean=true \
	-Declipse.ignoreApp=true \
	-Dosgi.noShutdown=true  \
	-Djetty.port=$HTTP_PORT  \
	-Djetty.port.ssl=$HTTPS_PORT \
	-Djetty.home=.  \
	-Dlogback.configurationFile=configurations/logback.xml \
	-Dfelix.fileinstall.dir=addons -Dfelix.fileinstall.filter=.*\\.jar \
	-Djava.library.path=lib \
	-Djava.security.auth.login.config=./etc/login.conf \
	-Dorg.quartz.properties=./etc/quartz.properties \
	-Dequinox.ds.block_timeout=240000 \
	-Dequinox.scr.waitTimeOnBlock=60000 \
	-Dfelix.fileinstall.active.level=4 \
	-Djava.awt.headless=true \
	-jar $cp $* \
	-console
```
Give OpenHAB gpio privilages - did not work (no openhab user)
----------------------------
```
sudo adduser openhab gpio
```









#TODO:

Create startup script to load at power on. 
------------------------------------------
https://github.com/openhab/openhab/wiki/Samples-Tricks#how-to-configure-openhab-to-start-automatically-on-linux

Make openhab release gpio binding on stop
-----------------------------------------
https://github.com/openhab/openhab/wiki/Samples-Tricks#how-to-configure-openhab-to-start-automatically-on-linux


#References

Install of OpenHAB
------------------
http://www.element14.com/community/community/design-challenges/forget-me-not/blog/2014/08/04/enoceanpi-and-sensors#jive_content_id_Setting_Up_OpenHAB
http://www.element14.com/community/community/design-challenges/forget-me-not/blog/2014/10/02/remember-me-always--part-018xx












