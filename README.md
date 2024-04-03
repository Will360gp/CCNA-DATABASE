# CCNA-DATABASE

SWITCH CAPA 3
___________________________________________________________
    Vlan "Nomber"
      Name "nombre que desea colocar"
      
    int Vlan "nomber"
      ip address "Ip - Mask"

    ip default-gateway 192.168.0.1

    ip routing                         ----- para que cree la tabla de rutas
    no switchport                      ----- para que el puerto puede tomar ip y poder enrutar 

    \\\\\\\\\\\\\\\\\\\\\
    TRUNK
    switchport mode access
    switchport trunk encapsulation dot1q
    switchport trunk allowed vlan all
    switchport mode trunk

    ip route 0.0.0.0 0.0.0.0 "Ip de destino" routing estatico por defecto
    
    switchport trunk native Vlan 1

DHCP
DHCP Snooping
_________________________________________________________

    int f0/0
      ip dhcp snooping limit rate 5
    Ip dhcp snooping vlan 2 3 etc...

    int f0/1 
      ip dhcp snooping trust


    DHCP
    ip dhcp pool "nombre" ------------------podemos crear distintas pool
    network 192.168.10.0 255.255.255.0
    defoult-router 192.168.10.1
    dns-server 8.8.8.8

    ip dhcp exclude-address 192.168.10.10

    ip helper-address --------------------para el router   que va a distribuir la ip del servoidor de dhcp

    sh ip dhcp binding
    sh ip dhcp pool
    

SEGURIDAD DE PUERTOS
_________________________________________________________
    Switchport port-segurity mac address sticky
    Switchport port-security maximun 1
  
    Switchport port-security violation \  protect  \  shutdown  \  restrict

    Show port-security int f/
    sho port-security mac-address



SSH    ---Security Shell
_________________________________________________________

    Username will privilege 15 password cisco
    ip domain-name cisco.com
    crypto key generate rsa
    ip ssh version 2
    
    line vty 0 15
    login local
    transport input ssh
    
    show ip ssh
    show ssh











VLAN - VTP
___________________________________________________________
    VTP mode server
    vtp domain cisco.com
    
    //////////////////////
    
    vtp mode client
    vtp domain cisco.com


HSRP      Protocolo de redundancia
____________________________________________________

    SERVER
    int g/
    standby 1 ip 192.168.10.1 --- ip virtual
    standby 1 priority 200 
    standby 1 preempt  ---- comunicacion de los routers
    
    
    CLIENTE
    int g/
    standby 1 ip 192.169.10.1
    standby 1 preempt
    
    
    Sh standby



Etherchannel
_________________________________________________________________

    interface port-channel 1
    description "aqui colocamos una nota referente"
    
    rango de interfaces# Channel-group 1 mode desireble
    
    show etherchannel sumary



    
    
    

  
