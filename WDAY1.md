
Pour linux commande:

Voici mon fichier exécutable pour avoir les informations:


yum check-update

if [[ $1 == "--update" ]]; then
    yum update -y
fi

echo "========================================"
echo "           Script de Vérification        "
echo "========================================"

echo "Nom d'hôte du système :" $hostname

echo "Version du noyau Linux :" $uname -r

echo "Date et Heure :" $date

echo -n "Adresse IPv4 : "
ip -4 addr show | grep inet | awk '{print $2}' | sed 's/\/[0-9]*//'

echo -n "Adresse IPv6 de liaison locale : "
ip -6 addr show scope link | awk '{print $2}' | sed 's/\/[0-9]*//'

echo "Serveurs DNS présents :"
cat /etc/resolv.conf

echo "Nettoyage du journal des logs..."
journalctl --vacuum-time=1d

echo -n "Le pare-feu est-il activé? "
if systemctl is-active firewalld; then
    echo "Oui"
else
    echo "Non"
fi
 


Cisco packet tracer niveau 2 :
J’ai réussi à tout faire, j’ai mis ma config d’un des mes routeurs.
Les 3 pc se ping avec 3 routeurs différents.



Processor board ID PT0123 (0123)
PT2005 processor: part number 0, mask 01
Bridging software.
X.25 software, Version 3.0.0.
4 FastEthernet/IEEE 802.3 interface(s)
2 Low-speed serial(sync/async) network interface(s)
32K bytes of non-volatile configuration memory.
63488K bytes of ATA CompactFlash (Read/Write)

Press RETURN to get started!



Router>en
Router#conf t
Enter configuration commands, one per line. End with CNTL/Z.
Router(config)#ip route 10.0.1.0 255.255.255.0 20.0.1.1
%Invalid next hop address (it's this router)
Router(config)#ip route 10.0.1.0 255.255.255.0 20.0.1.2
Router(config)#
%LINK-5-CHANGED: Interface Serial2/0, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface Serial2/0, changed state to up

%LINK-3-UPDOWN: Interface Serial2/0, changed state to down

%LINEPROTO-5-UPDOWN: Line protocol on Interface Serial2/0, changed state to down

%LINK-5-CHANGED: Interface Serial2/0, changed state to up

%LINK-3-UPDOWN: Interface Serial2/0, changed state to down

%LINK-5-CHANGED: Interface Serial2/0, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface Serial2/0, changed state to up

Router(config)#interface FastEthernet1/0
Router(config-if)#
Router(config-if)#exit
Router(config)#interface Serial2/0
Router(config-if)#
Router(config-if)#exit
Router(config)#interface FastEthernet1/0
Router(config-if)#
Router(config-if)#exit
Router(config)#interface Serial2/0
Router(config-if)#
Router(config-if)#exit
Router(config)#interface FastEthernet1/0
Router(config-if)#
Router(config-if)#exit
Router(config)#interface Serial2/0
Router(config-if)#ip address 255.255.255.0
% Incomplete command.
Router(config-if)#ip address 30.0.1.1 255.255.255.0
Router(config-if)#ip address 30.0.1.2 255.255.255.0
Router(config-if)#exit
Router(config)#ip route 10.0.1.0 255.255.255.0 30.0.1.1
Router(config)#exit
Router#
%SYS-5-CONFIG_I: Configured from console by console

Router#configure terminal
Enter configuration commands, one per line. End with CNTL/Z.
Router(config)#interface FastEthernet1/0
Router(config-if)#
Router(config-if)#exit
Router(config)#interface Serial2/0
Router(config-if)#ip address 30.0.1.2 255.255.255.252
Router(config-if)#exit
Router(config)#do ping 30.0.1.1

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 30.0.1.1, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 5/8/12 ms

Router(config)#ip route 10.0.1.0 255.255.255.0 30.0.1.1
Router(config)#exit
Router#
%SYS-5-CONFIG_I: Configured from console by console













Router>enable
Router#
Router#configure terminal
Enter configuration commands, one per line. End with CNTL/Z.
Router(config)#interface Serial2/0
Router(config-if)#ip address 30.0.1.2 255.255.255.252
Router(config-if)#
Router(config-if)#exit
Router(config)#interface Serial3/0
Router(config-if)#ip address 30.0.1.11 255.255.255.252
Bad mask /30 for address 30.0.1.11
Router(config-ip address 30.0.1.11 255.255.255.252ip address 30.0.1.11 255.255.255.252
Bad mask /30 for address 30.0.1.11
Router(config-if)#exit
Router(config)#
Router(config)#interface Serial3/0
Router(config-if)#no shutdown
Router(config-if)#
Router(config-if)#exit
Router(config)#interface Serial2/0
Router(config-if)#
Router(config-if)#exit
Router(config)#interface Serial3/0
Router(config-if)#
Router(config-if)#exit
Router(config)#interface Serial2/0
Router(config-if)#
Router(config-if)#exit
Router(config)#interface Serial3/0
Router(config-if)#ip address 30.0.1.20 255.255.255.252
Bad mask /30 for address 30.0.1.20
Router(config-if)#no ip address
Router(config-if)#shutdown
Router(config-if)#ip address 30.0.1.10 255.255.255.252
Router(config-if)#ip address 30.0.1.10 255.255.255.252
Router(config-if)#no shutdown

%LINK-5-CHANGED: Interface Serial3/0, changed state to down
Router(config-if)#exit
Router(config)#
Router(config)#interface Serial3/0
Router(config-if)#
Router(config-if)#exit
Router(config)#interface Serial3/0
Router(config-if)#
%LINK-5-CHANGED: Interface Serial3/0, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface Serial3/0, changed state to up

Router(config-if)#exit
Router(config)#interface Serial2/0
Router(config-if)#ip address 30.0.3.1 255.255.255.252
Router(config-if)#
Router(config-if)#exit
Router(config)#interface Serial3/0
Router(config-if)#
Router(config-if)#exit
Router(config)#interface Serial2/0
Router(config-if)#ip address 30.0.1.2 255.255.255.252
Router(config-if)#
Router(config-if)#exit
Router(config)#interface Serial3/0
Router(config-if)#ip address 30.0.3.1 255.255.255.252
Router(config-if)#
Router(config-if)#end
Router#copy running-config startup-config
Destination filename [startup-config]? 
Building configuration...
[OK]
Router#
%SYS-5-CONFIG_I: Configured from console by console

?Bad filename
%Error parsing filename (Bad file number)
Router#conf t
Enter configuration commands, one per line. End with CNTL/Z.
Router(config)#router eigrp 1
Router(config-router)#network 10.0.1.0 255.255.255.0
Router(config-router)#network 20.0.1.0 255.255.255.0
Router(config-router)#network 60.0.1.0 255.255.255.0
Router(config-router)#redistribute connected 
Router(config-router)#network 30.0.3.0 255.255.255.0
Router(config-router)#
%DUAL-5-NBRCHANGE: IP-EIGRP 1: Neighbor 30.0.3.2 (Serial3/0) is up: new adjacency

Router(config-router)#network 30.0.2.0 255.255.255.0
Router(config-router)#redistribute connected 
Router(config-router)#do show run
