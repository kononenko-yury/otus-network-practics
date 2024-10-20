### _Описание решения лабораторной работы_

#### 1. Разработано и задокументировано адресное пространство для лабораторного стенда с использованием Visual Studio

![](otus_%D0%B4%D0%B7_pic.jpg)

#### 2. VPC разнесены по разным VLAN путем выполнения соответсвующей настройки на коммутаторах доступа
     interface Ethernet0/2
     switchport access vlan 10
     switchport mode access
     spanning-tree portfast edge
     spanning-tree bpduguard enable

#### 3. На коммутаторах настроены интерфейсы управления 
     interface Vlan44
     ip address 10.0.1.30 255.255.255.0
     !
     ip default-gateway 10.0.1.3

#### 4. Между коммутаторами SW4 (порты e0/2 и e0/3)  и SW5 (порты e0/2 и e0/3) настроен протокол LACP
     interface Port-channel1
     switchport trunk allowed vlan 10,20,44
     switchport trunk encapsulation dot1q
     switchport mode trunk

     interface Ethernet0/2
     switchport trunk allowed vlan 10,20,44
     switchport trunk encapsulation dot1q 
     switchport mode trunk
     channel-protocol lacp 
     channel-group 1 mode active
     !
     interface Ethernet0/3
     switchport trunk allowed vlan 10,20,44
     switchport trunk encapsulation dot1q
     switchport mode trunk
     channel-protocol lacp
     channel-group 1 mode active

![](lacp_prot1.png)

#####  Аналогичная настройка выполнена и для коммутаторов  SW9  и SW10 (порты e0/2 и e0/3)

#### 5. С целью повышения отказоустойчивости на маршрутизаторах R12 и R13 поднят протокол HSRP. Для сетей 
#### 10.10.1.0 и 10.0.1.0 маршрутизатор R12 настроен с роль active, а R13 для сети 10.10.2.0
     interface Ethernet0/0.20
     encapsulation dot1Q 20
     ip address 10.10.2.2 255.255.255.0
     standby version 2
     standby 20 ip 10.10.2.3
     standby 20 preempt delay minimum 10
     standby 20 authentication Cisco20
     !

     interface Ethernet0/1.10
     encapsulation dot1Q 10
     ip address 10.10.1.1 255.255.255.0
     standby version 2
     standby 10 ip 10.10.1.3
     standby 10 priority 110
     standby 10 preempt delay minimum 10
     standby 10 authentication Cisco10
     !
     interface Ethernet0/1.44
     encapsulation dot1Q 44
     ip address 10.0.1.1 255.255.255.0
     standby version 2
     standby 44 ip 10.0.1.3
     standby 44 priority 110
     standby 44 preempt delay minimum 10
     standby 44 authentication Cisco44

![](show_standby.jpg)

#### Аналогичные настройки выполнены и на маршрутизаторах R17 и R16 (только настроен протокол vrrp)

#### 6. С целью оптимального функционирования сетей в офисе Москва для сетей 10.10.1.0 и 10.0.1.0 коммутатор SW4 
#### установлен как root primary, а SW5 как root secondary. Для сети 10.10.2.0 коммутатор SW5 как root primary, 
#### а SW4 как root secondary.

    SW4#sh span vlan 10,20,44
    
    VLAN0010
      Spanning tree enabled protocol rstp
      Root ID    Priority    32778
                 Address     aabb.cc00.2000
                 Cost        100
                 Port        2 (Ethernet0/1)
                 Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec

      Bridge ID  Priority    32778  (priority 32768 sys-id-ext 10)
                 Address     aabb.cc00.4000
                 Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec
                 Aging Time  300 sec

    Interface           Role Sts Cost      Prio.Nbr Type
    ------------------- ---- --- --------- -------- --------------------------------
    Et0/0               Desg FWD 100       128.1    Shr
    Et0/1               Root FWD 100       128.2    Shr
    Et1/1               Desg FWD 100       128.6    Shr
    Po1                 Desg FWD 56        128.65   Shr
    
    
    VLAN0020
      Spanning tree enabled protocol rstp
      Root ID    Priority    24596
                 Address     aabb.cc00.5000
                 Cost        56
                 Port        65 (Port-channel1)
                 Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec

      Bridge ID  Priority    32788  (priority 32768 sys-id-ext 20)
                 Address     aabb.cc00.4000
                 Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec
                 Aging Time  300 sec

    Interface           Role Sts Cost      Prio.Nbr Type
    ------------------- ---- --- --------- -------- --------------------------------
    Et0/0               Desg FWD 100       128.1    Shr
    Et0/1               Desg FWD 100       128.2    Shr
    Et1/0               Desg FWD 100       128.5    Shr
    Po1                 Root FWD 56        128.65   Shr
    
    
    VLAN0044
      Spanning tree enabled protocol rstp
      Root ID    Priority    32812
                 Address     aabb.cc00.2000
                 Cost        100
                 Port        2 (Ethernet0/1)
                 Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec
    
      Bridge ID  Priority    32812  (priority 32768 sys-id-ext 44)
                 Address     aabb.cc00.4000
                 Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec
                 Aging Time  300 sec
    
    Interface           Role Sts Cost      Prio.Nbr Type
    ------------------- ---- --- --------- -------- --------------------------------
    Et0/0               Desg FWD 100       128.1    Shr
    Et0/1               Root FWD 100       128.2    Shr
    Et1/1               Desg FWD 100       128.6    Shr
    Po1                 Desg FWD 56        128.65   Shr

#### 7. VPC имеет доступ во все сети.

![](ping_Москва1.jpg)

Файлы конфигурации коммутаторов :

  [sw2](https://github.com/kononenko-yury/otus-network-practics/blob/main/lab11/sw2);
  [sw3](https://github.com/kononenko-yury/otus-network-practics/blob/main/lab11/sw3);
  [sw4](https://github.com/kononenko-yury/otus-network-practics/blob/main/lab11/sw4);
  [sw5](https://github.com/kononenko-yury/otus-network-practics/blob/main/lab11/sw5);
  [sw9](https://github.com/kononenko-yury/otus-network-practics/blob/main/lab11/sw9);
  [sw10](https://github.com/kononenko-yury/otus-network-practics/blob/main/lab11/sw10)

Файлы конфигурации маршрутизаторов :  
  [r12](https://github.com/kononenko-yury/otus-network-practics/blob/main/lab11/r12);
  [r13](https://github.com/kononenko-yury/otus-network-practics/blob/main/lab11/r13);
  [r16](https://github.com/kononenko-yury/otus-network-practics/blob/main/lab11/r16);
  [r17](https://github.com/kononenko-yury/otus-network-practics/blob/main/lab11/r17);
  [r28](https://github.com/kononenko-yury/otus-network-practics/blob/main/lab11/r28)
