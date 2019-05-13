# FAQ

## Can I use GPS2IP for Apple Maps or Google Maps?

No. Both of these apps _only_ listen to the _onboard_ GPS.  
If your iOS device doesn't have a GPS, you _cannot_ use either of these apps. Period.  
We're sorry that GPS2IP \(or any other app\) can't help you.

## Will it work with app _X_?

Maybe, yes. Please check the main website, and see if your app is listed there.  
If your app is a maritime or aviation app, then it is quite likely.  
If you are a computer hobbyist, then I'm sure you can make it work! 

If it isn't, please get in touch _before buying_ GPS2IP, and we'll try and help figure out if you can!  
We're happy to help, and would prefer that you didn't buy something that you couldn't use.

## What's NMEA? Why do I need it?

If you don't know what NMEA is - then you probably don't need GPS2IP.  
It is a rather specific means of transmitting location and movement data, and lies in a rather niche area.

> I shall not today attempt further to define the kind of protocol I understand to be NMEA. But I know it when I see it.
>
> \(with apologies to\) [Potter Stewart](https://en.wikiquote.org/wiki/Potter_Stewart)

If you want general lat/long data, with speed and heading information without having to decode NMEA, perhaps you would prefer another app [6signals](https://itunes.apple.com/us/app/6signals-track-your-device-and-view-on-the-web/id918928539?mt=8).

## Do I need a cellular network?

There are two situations in which you would need a cellular network rather than wi-fi:

* You are using your cellular provider to send information to GPS2IP \(over a long distance that a LAN cannot support\)
* Your iOS device needs a cell network to determine location \(See **Does my device have a** _**real**_ **GPS?**\)

If you are sending the data from GPS2IP to a remote computer, located in a different place, then you will probably need a cellular provider to send the data from GPS2IP to your computer at a different location.

If the machine you are sending the data to is within metres, then you can use a wi-fi connection to connect them, saving data charges and reception problems.

If you are at the beach, or in the mountains, and your computer is somewhere else, then the Cell network is what you want.

### But I'm on my boat!

Then your navigation computer is close to you, and you can set up a wi-fi connection between GPS2IP and your computer with the navigation sytem on it.

You can usually set up a wi-fi LAN on the comnputer, and then connect GPS2IP to that wi-fi network.  
No cellular network required.  
\(Unless of course, your iOS device doesn't have a real GPS, and needs the network. See **Does my device have a real GPS?**\)

Depending on what navigation software you are running, and your requirements, you can either:

* Use GPS2IP [as a socket](http://capsicumdreams.com/iphone/gps2ip/socketMode.php)
* [Push data](http://capsicumdreams.com/iphone/gps2ip/tcpPushMode.php) to your computer with GPS2IP

## Does my device have a real GPS?

For iPads, this is pretty easy to determine.  
The GPS-equipped versions have a big plastic bar on the back that covers the GPS antenna, and it also has a slot for a SIM card to connect to the network.  
So: If it has a SIM-card slot - you have a real GPS.  
If you don't, if you are out on the water far from cellular networks - you may be unable to get your location.

For iPhones, it's even easier.  
Yes, you do. All iPhone have _real_ GPS. it can use cellular or GPS networks to determine location.  
Either way, you should be able to get your location just fine.

