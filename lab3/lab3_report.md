<p>University: <a href="https://itmo.ru/ru/">ITMO University</a></p>

<p>Faculty: <a href="https://fict.itmo.ru">FICT</a></p>

<p>Course: <a href="https://github.com/itmo-ict-faculty/introduction-in-routing">Introduction in routing</a></p>

<p>Year: 2022/2023</p>

<p>Group: K33212</p>
<p>Author: Guseynov Guseyn Muradovich</p>
<p>Lab: Lab3</p>
<p>Date of create: 18.11.2022</p>
<p>Date of finished: 26.12.2022</p><h1>Лабораторная работа 3 "ЭЭмуляция распределенной корпоративной сети связи, настройка OSPF и MPLS, организация первого EoMPLS"</h1>
<p><b>Цель работы:</b></p>
<p>Изучить протоколы OSPF и MPLS, механизмы организации EoMPLS.</p>

<p><b>Ход работы:</b></p>

<p>R01.NY:</p>

     /interface bridge
     add name=EoMPLS_Bridge
     add name=Lo0
     /interface vpls
     add cisco-style=yes cisco-style-id=100 disabled=no l2mtu=1500 mac-address=02:BD:27:52:DB:8E name=EoMPLS remote-peer=4.4.4.4
     /interface wireless security-profiles
     set [ find default=yes ] supplicant-identity=MikroTik
     /routing ospf instance
     set [ find default=yes ] router-id=1.1.1.1
     /interface bridge port
     add bridge=EoMPLS_Bridge interface=ether2
     add bridge=EoMPLS_Bridge interface=EoMPLS
     /ip address
     add address=172.15.1.1/30 interface=ether3 network=172.15.1.0
     add address=172.15.2.1/30 interface=ether4 network=172.15.2.0
     add address=1.1.1.1 interface=Lo0 network=1.1.1.1
     /ip dhcp-client
     add disabled=no interface=ether1
     /mpls ldp
     set enabled=yes transport-address=1.1.1.1
     /mpls ldp interface
     add interface=ether3
     add interface=ether4
     /routing ospf network
     add area=backbone
     /system identity
     set name=R01.NY
    
<p>R01.LND:</p>

     /interface bridge
     add name=Lo0
     /interface wireless security-profiles
     set [ find default=yes ] supplicant-identity=MikroTik
     /routing ospf instance
     set [ find default=yes ] router-id=2.2.2.2
     /ip address
     add address=2.2.2.2 interface=Lo0 network=2.2.2.2
     add address=172.15.1.2/30 interface=ether2 network=172.15.1.0
     add address=172.15.3.1/30 interface=ether3 network=172.15.3.0
     /ip dhcp-client
     add disabled=no interface=ether1
     /mpls ldp
     set enabled=yes transport-address=2.2.2.2
     /mpls ldp interface
     add interface=ether2
     add interface=ether3
     /routing ospf network
     add area=backbone
     /system identity
     set name=R01.LND
     
<p>R01.HKI:</p>

     /interface bridge
     add name=Lo0
     /interface wireless security-profiles
     set [ find default=yes ] supplicant-identity=MikroTik
     /routing ospf instance
     set [ find default=yes ] router-id=3.3.3.3
     /ip address
     add address=172.15.3.2/30 interface=ether2 network=172.15.3.0
     add address=172.15.4.1/30 interface=ether3 network=172.15.4.0
     add address=172.15.5.1/30 interface=ether4 network=172.15.5.0
     add address=3.3.3.3 interface=Lo0 network=3.3.3.3
     /ip dhcp-client
     add disabled=no interface=ether1
     /mpls ldp
     set enabled=yes transport-address=3.3.3.3
     /mpls ldp interface
     add interface=ether4
     add interface=ether3
     add interface=ether2
     /routing ospf network
     add area=backbone
     /system identity
     set name=R01.HKI

<p>R01.SPB:</p>

     /interface bridge
     add name=EoMPLS_Bridge
     add name=Lo0
     /interface vpls
     add cisco-style=yes cisco-style-id=100 disabled=no l2mtu=1500 mac-address=02:96:AE:D1:9C:3F name=EoMPLS remote-peer=1.1.1.1
     /interface wireless security-profiles
     set [ find default=yes ] supplicant-identity=MikroTik
     /routing ospf instance
     set [ find default=yes ] router-id=4.4.4.4
     /interface bridge port
     add bridge=EoMPLS_Bridge interface=ether4
     add bridge=EoMPLS_Bridge interface=EoMPLS
     /ip address
     add address=4.4.4.4 interface=Lo0 network=4.4.4.4
     add address=172.15.5.2/30 interface=ether2 network=172.15.5.0
     add address=172.15.6.1/30 interface=ether3 network=172.15.6.0
     /ip dhcp-client
     add disabled=no interface=ether1
     /mpls ldp
     set enabled=yes transport-address=4.4.4.4
     /mpls ldp interface
     add interface=ether3
     add interface=ether2
     add interface=ether4
     /routing ospf network
     add area=backbone
     /system identity
     set name=R01.SPB
     
<p>R01.MSK:</p>

     /interface bridge
     add name=Lo0
     /interface wireless security-profiles
     set [ find default=yes ] supplicant-identity=MikroTik
     /routing ospf instance
     set [ find default=yes ] router-id=5.5.5.5
     /ip address
     add address=172.15.7.1/30 interface=ether2 network=172.15.7.0
     add address=172.15.6.2/30 interface=ether3 network=172.15.6.0
     add address=5.5.5.5 interface=Lo0 network=5.5.5.5
     /ip dhcp-client
     add disabled=no interface=ether1
     /mpls ldp
     set enabled=yes transport-address=5.5.5.5
     /mpls ldp interface
     add interface=ether2
     add interface=ether3
     /routing ospf network
     add area=backbone
     /system identity
     set name=R01.MSK
     
<p>R01.LBN:</p>

     /interface bridge
     add name=Lo0
     /interface wireless security-profiles
     set [ find default=yes ] supplicant-identity=MikroTik
     /routing ospf instance
     set [ find default=yes ] router-id=6.6.6.6
     /ip address
     add address=6.6.6.6 interface=Lo0 network=6.6.6.6
     add address=172.15.2.2/30 interface=ether2 network=172.15.2.0
     add address=172.15.4.2/30 interface=ether3 network=172.15.4.0
     add address=172.15.7.2/30 interface=ether4 network=172.15.7.0
     /ip dhcp-client
     add disabled=no interface=ether1
     /mpls ldp
     set enabled=yes transport-address=6.6.6.6
     /mpls ldp interface
     add interface=ether4
     add interface=ether2
     add interface=ether3
     /routing ospf network
     add area=backbone
     /system identity
     set name=R01.LBN
     
<p>PC1:</p>

     /interface wireless security-profiles
     set [ find default=yes ] supplicant-identity=MikroTik
     /ip address
     add address=192.168.10.1/24 interface=ether2 network=191.168.10.0
     /ip dhcp-client
     add disabled=no interface=ether1
     /system identity
     set name=PC1
     
<p>SGI.Prism:</p>
     
     /interface wireless security-profiles
     set [ find default=yes ] supplicant-identity=MikroTik
     /ip address
     add address=192.168.10.2/24 interface=ether2 network=192.168.10.0
     /ip dhcp-client
     add disabled=no interface=ether1
     /system identity
     set name=SGI.Prism
     
     
<p><ins>Результаты пингов, проверки локальной связности</ins></p>
<img src="ping.png">
<img src="ping2.png">
<img src="mpls.png">
<img src="mpls2.png">
<p><b>Вывод:</b></p>
<p>В ходе лабораторной работы были изучены протоколы OSPF и MPLS, механизмы организации EoMPLS.</p>
