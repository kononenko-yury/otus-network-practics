### _Описание решения лабораторной работы_

#### 
Лабораторная работа выполнена с использование ПО **PacketTracert 8.2.1**

#### 1. На коммутаторе S1 настроены VLAN управления и шлюз по умолчанию (аналогично выполнено и для S2)
       interface Vlan3
       ip address 192.168.3.11 255.255.255.0
       !
       ip default-gateway 192.168.3.1

#### 2. Выполнена следующая настройка портов (для S1 fa0/5 и  fa0/1) и (для S2 fa0/1)
        switchport trunk native vlan 8
        switchport trunk allowed vlan 3-4,8
        switchport mode trunk

#### 3. Конфигурация коммутаторов приведена в файлах [config_switch-s1](https://github.com/kononenko-yury/otus-network-practics/blob/main/Lesson1/config_switch-s1) и [config_switch-s2](https://github.com/kononenko-yury/otus-network-practics/blob/main/Lesson1/config_switch-s2)