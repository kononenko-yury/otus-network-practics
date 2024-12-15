## _Описание решения лабораторной работы_ 36

#### 1. Выполнена настройка двух туннелей GRE между Москвой и Санкт-Петербургом
     tunnel 100 на маршрутизаторе R14 и GRE tunnel 200 на маршрутизаторе R15  (Москва)
     На маршрутизаторе R18 (Санкт-Петербург) настроено 2 (100 и 200) туннеля на Москву 
![](pingSPB_to_MSK.jpg)
#### 2. Выполнена настройка DMVPN туннеля (Tunnel 300) между Москвой (R15-hub) и Чокурдах, Лабытнанги
![](dmvpn_R15_to_R28_and_27.jpg)

Файлы конфигурации маршрутизаторов :  
  [r14](https://github.com/kononenko-yury/otus-network-practics/blob/main/lab36/r14);
  [r15](https://github.com/kononenko-yury/otus-network-practics/blob/main/lab36/r15);
  [r18](https://github.com/kononenko-yury/otus-network-practics/blob/main/lab36/r18);
  [r27](https://github.com/kononenko-yury/otus-network-practics/blob/main/lab36/r27);
  [r28](https://github.com/kononenko-yury/otus-network-practics/blob/main/lab36/r28);
