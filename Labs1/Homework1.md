### _�������� ������� ������������ ������_

#### 
������������ ������ ��������� � ������������� �� **PacketTracert 8.2.1**

#### 1. �� ����������� S1 ��������� VLAN ���������� � ���� �� ��������� (���������� ��������� � ��� S2)
       interface Vlan3
       ip address 192.168.3.11 255.255.255.0
       !
       ip default-gateway 192.168.3.1

#### 2. ��������� ��������� ��������� ������ (��� S1 fa0/5 �  fa0/1) � (��� S2 fa0/1)
        switchport trunk native vlan 8
        switchport trunk allowed vlan 3-4,8
        switchport mode trunk

#### 3. ������������ ������������ ��������� � ������ [config_switch_s1](https://github.com/kononenko-yury/otus-network-practics/blob/main/Labs1/config_switch_s1) � [config_switch_s2](https://github.com/kononenko-yury/otus-network-practics/blob/main/Labs1/config_switch_s2)

#### 4. ������������ �������������� ��������� � ����� [config_router_r1](https://github.com/kononenko-yury/otus-network-practics/blob/main/Labs1/config_router_r1)

