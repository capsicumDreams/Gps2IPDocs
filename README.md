---
description: Every setting in GPS2IP
---

# Settings

## Time between sending positions

You can choose how often messages are sent by GPS2IP.

* **No delay**

  Send as quickly as possible, on every new location received by the hardware

* **1s**  Send every second, even if there is no new location data. If you do not want identical data being sent when the device is not moving, see  See [Disable when Static](./#disable-when-static), below. Every slower rate follows this same logic.
* **5s**
* **30s**
* **60s**
* **5 minutes**
* **30 minutes**
* **1 hour**

### Disable when Static

When this is enabled, GPS2IP will not send location data unless the device has moved.  
So, if if it _doesn't_ move, no messages will be transmitted.

This can save data charges by reducing transmission of redundant information.

If this setting is disabled, data will _always_ be transmitted according to the time interval selected, regardless of having received new data or not.

## GPS Accuracy

You can select with what level of accuracy GPS2IP functions. The higher accuracy levels consume more power.

The levels you can select from are

* **The very best** This mode uses quite a lot of energy. You should keep the device plugged in to avoid flattening the battery.
* **Pretty good** Receives a location update approximately every 10m, and uses less power than _The very best_ setting
* **Moderate** A new location will be detected roughly every 100m of travel
* **Lazy** This uses the lowest amount of power. But accuracy is very low - perhaps every 3km, or so

## NMEA messages to send

### GGA

Sends the GPGGA message. If desired, the time field can be transmitted with millisecond information by hitting the **ⓘ**  info button, and enabling that option.

Without milliseconds, you might get a message like`$GPGGA,193420,3351.80400,S,15112.66000,E,1,8,0.9,0.0,M,46.9,M,0,2*64`

With milliseconds, you would get something more like  
`$GPGGA,194900.882,3351.80400,S,15112.66000,E,1,8,0.9,0.0,M,46.9,M,0,2*70`

{% hint style="warning" %}
Horizontal Dilution of Position is hard-coded to `0.9`.  
Number of satellites tracked is fixed to `8`.  
Height of geoid above WGS84 ellipsoid is hard-coded to `46.9`m.
{% endhint %}

### RMC

Sends the GPRMC message.  
If desired, the time field can be transmitted with millisecond information by hitting the **ⓘ**  info button, and enabling that option, in exactly the same way as GGA.

{% hint style="warning" %}
Magnetic variation is fixed to `3.1`°W.
{% endhint %}

### GLL

Sends the GPGLL message.

### HDG

This displays the Heading Deviation & Variation. Only supported on hardware with an electronic compass.

### HDM

This displays the _Magnetic_ heading. Only on supported hardware with an electronic compass.

### HDT

This displays the _True_ heading. Only on supported hardware with an electronic compass.

## Other messages

### PASHR

This is a non-standard message, that transmits Inertial Attitude Data.  
Reference, [here](https://docs.novatel.com/OEM7/Content/SPAN_Logs/PASHR.htm).

{% hint style="warning" %}
Heave is fixed to `0.0`m  
Roll and pitch angle accuracy estimate fixed to `3.14159`°
{% endhint %}

Using the [True North](./#true-north) setting in the General section, you can select between a True and Magnetic north output in this sentence.

### GPTXT

You can enter a custom message here, and it will be transmitted _once_, when GPS2IP is first enabled.  
This was designed to associate a device with an IP address, but not to send more data than necessary.

If your device has an IP address that changes, or you need to send some identity information in every message, consider the [Custom Prefix](./#custom-prefix) setting, below.

### Custom Prefix

GPS2IP can be configured to modify each transmitted message with a customizable prefix. This allows _every_ received message to be associated with a particular device.

For instance, if you have three devices running GPS2IP, and all transmitting to the same server, you could assign some unique text into this field, and it would be easy to determine which message is from what device.

If a normal message is

```text
$GPRMC,123519,A,4807.038,N,01131.000,E,022.4,084.4,230394,003.1,W*6A
```

and you define the _Custom Prefix_ as `#Unit3`, the transmitted message would be

```text
#Unit3$GPRMC,123519,A,4807.038,N,01131.000,E,022.4,084.4,230394,003.1,W*6A
```

The other two devices might have their Custom Prefix configured as `#Unit1`, and `#Unit2`, for example.

There is _no_ separator between the custom prefix and the rest of the NMEA message.

The NMEA checksum \(the last three characters of the message\), **does not** take into account the _Prefix_. If you remove the prefix text from the beginning of the message, the NMEA message remains correct. So the prefix is just for uniquely identifying which device sent the message - remove the prefix, and the NMEA is just a standard message.

## General Settings

### Operate in background mode

If this is enabled, GPS2IP will operate when the device goes to sleep, or another app is running in the foreground.

{% hint style="info" %}
We **highly** recommend to enable this setting to continue to receive location data.
{% endhint %}

### Operate when terminated if enabled

This automatically restarts GPS2IP after the device has restarted after having had flat batteries, or being turned off.

GPS2IP can use quite a lot of energy, and if this setting is inadvertently enabled when you do not require it, your device will  This can use a lot of eneraccidentally use 

### True North

Here you can configure whether the PASHR message outputs True or Magnetic north.  
Whether you enable this depends on your software or personal preference.

### Lock with Password

You can configure a password so that no settings can be changed without re-entering the password.

As one example, if you have staff members that you need to keep track of, you can set up the device according to your needs, enable GPS2IP, and lock it with this feature.

{% hint style="info" %}
The is an app designed expressly for tracking iOS devices, that does not require parsing NMEA. It is based on the same prinicples as GPS2IP.  
It is called [6signals](https://itunes.apple.com/us/app/6signals-track-your-device-and-view-on-the-web/id918928539?mt=8), on the AppStore. 
{% endhint %}

With the lock enabled, **nothing** can be changed, and GPS2IP cannot be turned off without the password.

{% hint style="danger" %}
**Don't forget this password!** You _cannot_ reset this password!
{% endhint %}

Because _nothing_ can be changed without the password, GPS2IP must be enabled first \(check that you are receiving messages\), then go back into Settings and enable the lock.  
To stop GPS2IP transmitting data, you must first unlock it.

## Connection Method

In this section, you can configure how you will be connecting with GPS2IP.

### Socket

When GPS2IP is operating as a [socket](https://en.wikipedia.org/wiki/Network_socket), it waits and listens _for something to connect to it_.

Many different devices can connect to GPS2IP simultaneously, and when it transmits data, it will transmit to them all. In this situation, it is easy to receive the same data on different computers on your network.

There are different ways to connect using a socket, for example

#### Telnet or netcat

```bash
telnet 192.168.0.101 11123
```

```bash
nc 192.168.0.101 11123
```

Several marine apps connect to NMEA servers using this method. There are [some examples ](http://capsicumdreams.com/iphone/gps2ip/index.php#compatible)on the GPS2IP website.

See the [Socket ](http://capsicumdreams.com/iphone/gps2ip/socketMode.php)section on the main GPS2IP website for more details about setting up sockets in general.

### TCP Push

Using this method, GPS2IP transmits to any IP address and port that you enter, using TCP/IP.

In this situation, GPS2IP is 'pushing' to some other device - the other device is 'listening'.  
This could be a server on the internet, or something on your LAN. As long as there is a path through routers/firewalls, you should be able to receive data anywhere in the world from GPS2IP.

The address can be any valid IP4 adress, and also a URL such as _receivenmea.com_  
\(http:// is assumed\).  
The Port number should be the port that _the other machine is listening on_.

{% hint style="warning" %}
This method can be complex to setup. If it is not working, please don't give up, and give GPS2IP zero stars, and complain on the AppStore.  
This mode **does** work, and works well.  
Unfortunately, though, networking can be a very complicated subject.  
Get in touch, so we can try to help!
{% endhint %}

There is some [helpful information](http://capsicumdreams.com/iphone/gps2ip/tcpPushMode.php) on configuring TCP & UDP Push on the GPS2IP website.

### UDP Push

This is exactly the same as TCP Push, but uses the UDP protocol. There are no other differences.  
Here is some [helpful information](http://capsicumdreams.com/iphone/gps2ip/tcpPushMode.php).

## Network Selection

To connect to GPS2IP, you must establish a network connection.  
You may choose from any of the following.

### Wifi IP

This is probably the most common way to connect to GPS2IP.

Both the iOS device with GPS2IP and another computer will be on the same local wifi network, and communicate over that.

### Cellular IP

If your network carrier supports it, and you have a plan with data, you might be able to transmit the data over your network provider's system.

{% hint style="warning" %}
This can be a very complicated method. Carriers differ greatly, and depending on which [Connection Method](./#connection-method) you select, you might suffer from the IP address changing without warning.  
Please consider this option only if you are confident you can troubleshoot and spend some time to make sure it is operating correctly.

GPS2IP cellular data transmission **does** work, but it can be complicated to setup.
{% endhint %}

### Hotspot

### Bluetooth

If your computer and software support BLE, GPS2IP can act as a BLE peripheral.

{% hint style="danger" %}
BLE is **not** 'normal' Bluetooth. You cannot just connect GPS2IP to your computer to 'magically' have a GPS.

The software you use **must** be expressly designed to use BLE. The operating system \(Windows or Mac\) **will not see** GPS2IP as a Bluetooth GPS.

SeaNav, for example, has been written to take advantage of BLE devices, like GPS2IP.
{% endhint %}

{% embed url="http://capsicumdreams.com/gps2ip/bluetoothMode.php" %}



