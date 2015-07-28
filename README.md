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

I then mapped the share on my local machine





#References

Install of OpenHAB
------------------
http://www.element14.com/community/community/design-challenges/forget-me-not/blog/2014/08/04/enoceanpi-and-sensors#jive_content_id_Setting_Up_OpenHAB
http://www.element14.com/community/community/design-challenges/forget-me-not/blog/2014/10/02/remember-me-always--part-018xx












