# Copying a gateway

### Copy an image
1 Copy an image of the gateway to another sd card
Any disk-to-disk software can be used for that reason. After copying you should be able to load the operating system into Desktop Environment

### Reinstalling software
If you are going to use another IMST IC880A-SPI you need to reinstall the software
Open console and put two commands

```console
  $ cd ~/ic880a-gateway
  $ sudo ./install.sh spi
```  
After the second command you will be asked to specify hostname, descriptive name and GPS coordinates. You can skip it keep it by default, just click Enter several times. After the instalation system will be reboted

### Specifiing GPS dongle

If you are going to use USB dongle you need to specify the port for the gateway. For this you have to open global configuration file of the program:

```console
sudo nano /opt/ttn-gateway/bin/global_conf.json
```
Then find section responsible for gps and make it look like that

```json
        "gps_tty_path": "/dev/ttyACM0",
        "fake_gps": false,
        "ref_latitude": 10,
        "ref_longitude": 20,
        "ref_altitude": -1,
```

At that point the gateway is ready. It should work straight away, but you beter reboot it one more time.