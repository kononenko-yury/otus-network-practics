### _Описание решения лабораторной работы_ 28

#### 1. В офисе Москва выполнена фильтрация для предотвращения транзитного трафика (as-path)

      neighbor 192.168.1.0 filter-list 10 out
      ip forward-protocol nd
      ip as-path access-list 10 permit ^$

#### 2. В офисе Санкт-Петербург выполнена фильтрация для предотвращения транзитного трафика (prefix-list)
       neighbor 192.168.6.0 prefix-list LOCAL-TRANFER out
       neighbor 192.168.7.0 prefix-list LOCAL-TRANFER out
       ip prefix-list LOCAL-TRANFER seq 5 permit 10.20.1.0/24
       ip prefix-list LOCAL-TRANFER seq 10 permit 10.20.2.0/24

 #### 3. Провайдер Киторн отдает маршрут только по умолчанию (вывод на R14)
      ![](r14_ip_route.jpg)
#### 4. Провайдер Ламас отдает маршрут только  умолчанию и префиксы офиса Санкт-Петербург
      ip prefix-list ALLOW-DEFAULT-SPB seq 5 permit 10.20.1.0/24
      ip prefix-list ALLOW-DEFAULT-SPB seq 10 permit 10.20.2.0/24
      ip prefix-list ALLOW-DEFAULT-SPB seq 15 permit 0.0.0.0/0

       neighbor 192.168.5.1 route-map ALLOW-DEFAULT-SPB out

Проверка общей связанности
![](check_ping.jpg)

Файлы конфигурации маршрутизаторов :  
  [r14](https://github.com/kononenko-yury/otus-network-practics/blob/main/lab28/r14);
  [r15](https://github.com/kononenko-yury/otus-network-practics/blob/main/lab28/r15);
  [r18](https://github.com/kononenko-yury/otus-network-practics/blob/main/lab28/r21);
  [r22](https://github.com/kononenko-yury/otus-network-practics/blob/main/lab28/r22);
  [r21](https://github.com/kononenko-yury/otus-network-practics/blob/main/lab28/r21);

