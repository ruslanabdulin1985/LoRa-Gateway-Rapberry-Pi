# Important!
Never Power up the device with antana deattached! It may harm the hardware!

# Raspberry pi 4
version  2019-09-26 Buster

# iC880A LoRaWAN Gateway Backplane v2.1 
https://shop.coredump.ch/product/ic880a-lorawan-gateway-backplane/

# Nice Tutorial
[mainTutorial](www.youtube.com/watch?v=ZFVA6cQyheY&list=WL&index=2&t=0s)

# Repository to make the gateway work
https://github.com/ttn-zh/ic880a-gateway/blob/spi/README.md

# Manual mode
EUI DCA632FFFE3221C6

Checking online doesn't work. Command to check is: tail -f /var/log/syslog

registring on TTN using legacy mode 
* checkbox I'm using the legacy packet forwarder

# GPS coordinates

Extra: Using the onboard GPS data as gateway location
The installation package uses “fake_gps” by default. This means that the program will ignore the GPS data received from the onboard GPS module. In order to use “real” GPS, one line  "fake_gps": false,  should be added to the /opt/ttn-gateway/bin/local_conf.json file in order to override the default setting in the global_conf.json file. The result should look like this:

1
2
3
4
5
6
7
8
9
10
11
12
{
        "gateway_conf": {
                "gateway_ID": "B827EBFFFEEB487F",
                "servers": [ { "server_address": "router.eu.thethings.network", "serv_port_up": 1700, "serv_port_down": 1700, "serv_enabled": true } ],
                "fake_gps": false,
                "ref_latitude": 0,
                "ref_longitude": 0,
                "ref_altitude": 0,
                "contact_email": "",
                "description": "ttn-ic880a"
        }
}
Extra: Fixing the serial port (uart) issue on RasPi 3
WiFi and Bluetooth hardware are added to RasPi 3 and RasPi Zero W. New issues are introduced at the same time. The bluetooth hardware takes /dev/ttyAMA0 from the system which was used as a general UART interface on the GPIO header on RasPi “pre-3”. The TTN source code we use above still try to use /dev/ttyAMA0 to get GPS data. This obviously will not work. One way to fix this is to disable bluetooth and return /dev/ttyAMA0 to general UART interface:

run sudo raspi-config, go to Interfacing Options->Serial
Choose <No> for “Would you like a login shell to be accessible over serial?”
Choose <Yes> for “Would you like the serial port hardware to be enabled?”
Exit raspi-config
Add a line at the end of /boot/config.txt: dtoverlay=pi3-disable-bt
Reboot the RasPi. The general UART interface should now be accessible via /dev/ttyAMA0
For more detail about the serial port on RasPi 3, refer to this blog page:
https://spellfoundry.com/2016/05/29/configuring-gpio-serial-port-raspbian-jessie-including-pi-3/



Global config file /opt/ttn-gateway/bin/global_conf.json
/* GPS configuration */
        "gps_tty_path": "/dev/ttyACM0",
        "fake_gps": false,
        "ref_latitude": 10,
        "ref_longitude": 20,
        "ref_altitude": -1,

Coverage map
https://www.thethingsnetwork.org/map