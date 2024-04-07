# CCNA-DATABASE

SWITCH CAPA 3
___________________________________________________________
    Vlan "Nomber"
      Name "nombre que desea colocar"
      
    int Vlan "nomber"
      ip address "Ip - Mask"

    ip default-gateway 192.168.0.1

    ip routing          ----- para que cree la tabla de rutas
    no switchport       ----- para que el puerto puede tomar ip y poder enrutar 

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

    ////////////////////////
    Vlan Nativa 
    



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




LLDP Protocolo de decubrimiento de dispocitivos  como el CDP pero este es de estandar abierto
___________________________________________________________________
    lldp run -- para activar el protocolo
    lldp holdtime 120
    lldo reinit 2
    lldp timer 30
    int f/ 
        lldp transmit
        lldp recive

    sh lldp int
    show lldp int f/
    sh llpd neighbors detail


    
CDP --- protocolo de cisco Cisco discovery protocol
____________________________________________________________________
    viebe habilitada ya por defecto, pero si queremos restringirlo para        que no envia paqutes de informacion a otra red lo configuramos asi

    (Config)# No cdp run 
    
    int g/
        no cdp enable




  Router On Stick
___________________________________________________________________

    interface FastEthernet 0/0.1 
    -------- sub interface





Router
__________________________________________________________________
    Show ip interface brief
    Show ip interface


RIP  ---- Protocolo de RUTAS
__________________________________________________________________






Balanceo de Carga
_________________________________________________________________






STP  Spanning Tree Protocol
__________________________________________________________________

    Show spanning-tree  -----  aqui podemos ver cual es el sw bridge y costo de llegada etc
    shw spanning-tree interface fastethernet 0/10 portfast
    PortFast            ---- te saltas el proceso de spanning tree pero es solo para host no para otros dispositivos por que no es recomendable
        int f/
        spanning-tree portfast
        spanning-tree portfast trunk --- si es trunk el puerto
        

    -------------------Envia tramas llamadas BPDU------------------------



OSPF
___________________________________________________________________
      Curso de OSPF  https://www.youtube.com/playlist?list=PL-Ml_Z_JW-XuyVdNKhTRSdzh6vO-jgO-O 

    Show ip OSPF neighbor
    Show ip OSPF database  -- nos va a mostrar todas la base de datos que esta en todos los routers por son iguales en todos
    Show ip route

    Router ID  -- si no colocamos manualmente un router ID el tomara el de una looback si no hay tomara la ip add mas alta
        rputer ospf 1
            router-id 1.1.1.1
        
            _________________________________________

            Interfaces Pasivas
            para que no envie OSPF hello, pero si seran anadidas a la red

            route OSPF 1
                passive-interface f/
            Anucio de rutas para internet con rutas estaticas 0.0.0.0 0.0.0.0 192.168.2.1

            METRICAS - COSTO DE INTERFACE
            
                metodo #1 
                int f/
                    ip ospf cost # 1-65500

                metodo #2
                dentro de la instancia
                formula cost= reference Bandwidth / int Bandwidth
                auto-cost reference-bandwidth #

                metodo #3 no recomendado
                 int f/
                     bandwidth # 


            Show ip ospf interface g/ ----- tota la informacion de la interface con respecto al protocolo

            
NAT  Network Address Traslation
_______________________________________________________________________________________
        Nat estatico///////////////////////////////////////////////////////////////////
        por lo generarl se usa para los servidores

        
        para los hots
        access-list 1 permit 10.0.0.0 0.255.255.255

        INTERFACE DE RED LAN int f/
            ip nat inside

        En la interface que va para el ISP int f/
            ip nat outside

        Modo global #
            ip nat inside source static ip_privada ip_publica
            
        Show Ip Nat Translation

    Dinamica//////////////////////////////////////////////////////////////////////

    INTERFACE DE RED LAN int f/
            ip nat inside

        En la interface que va para el ISP int f/
            ip nat outside

        ////////////////////////////// AHORA HAY QUE HACER UNA POOL, y colocamos una direccion de inicio y una de final
        
        ip NAT pool "Name" 198.1.1.100 198.1.1.254 NETMASK 255.255.255.0
        
        access-list 1 permit 10.1.1.0 0.0.0.255

        ip nat inside source list 1 pool "name" Overload

        ip route 0.0.0.0 0.0.0.0 "IP de proveedor"
        

PAT  Port address traslation
______________________________________________________________________________________
    










