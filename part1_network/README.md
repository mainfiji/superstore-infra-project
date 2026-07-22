# Часть 1. Дизайн и конфигурация сети

В этой части выполнены все 13 заданий по настройке сетевой связности в дарксторе и головном офисе.

## Задание 1. VLAN на коммутаторах даркстора
- Настроены VLAN 30, 40, 60 на SW1-DS, SW2-DS, SW3-DS.
- Trunk-порты с ограниченным списком VLAN.
- Клиентским устройствам назначены статические IP (до перехода на DHCP).
- Проверка ping между устройствами в одном VLAN:

| Пара | Скриншот |
|------|----------|
| PCL-3 ↔ PCL-4 | [`task1_vlan/ping_PCL-3_to_PCL-4.png`](task1_vlan/ping_PCL-3_to_PCL-4.png) |
| Portal ↔ FS | [`task1_vlan/ping_Portal_to_FS.png`](task1_vlan/ping_Portal_to_FS.png) |
| PCL-1 ↔ PCL-2 | [`task1_vlan/ping_PCL-1_to_PCL-2.png`](task1_vlan/ping_PCL-1_to_PCL-2.png) |
| PCS-1 ↔ PCS-2 | [`task1_vlan/ping_PCS-1_to_PCS-2.png`](task1_vlan/ping_PCS-1_to_PCS-2.png) |

## Задание 2. Маршрутизация на R-Darkstore
- Созданы субинтерфейсы для VLAN 30, 40, 60 с IP-адресами шлюзов.
- Проверка ping до шлюзов и между разными VLAN:

| Проверка | Скриншот |
|----------|----------|
| PCL-1 → шлюз (10.10.3.1) | [`task2_routing/ping_PCL-1_to_gateway.png`](task2_routing/ping_PCL-1_to_gateway.png) |
| PCS-1 → шлюз (10.10.4.1) | [`task2_routing/ping_PCS-1_to_gateway.png`](task2_routing/ping_PCS-1_to_gateway.png) |
| Portal → шлюз (10.10.6.1) | [`task2_routing/ping_Portal_to_gateway.png`](task2_routing/ping_Portal_to_gateway.png) |
| PCL-3 → PCS-3 | [`task2_routing/ping_PCL-3_to_PCS-3.png`](task2_routing/ping_PCL-3_to_PCS-3.png) |
| PCL-4 → PCS-1 | [`task2_routing/ping_PCL-4_to_PCS-1.png`](task2_routing/ping_PCL-4_to_PCS-1.png) |
| PCL-1 → PCS-2 | [`task2_routing/ping_PCL-1_to_PCS-2.png`](task2_routing/ping_PCL-1_to_PCS-2.png) |

## Задание 3. DHCP на R-Darkstore
- Созданы пулы для VLAN 30 и 40.
- Статические адреса на клиентах удалены, получены по DHCP.
- Проверка:

| Устройство | Скриншот |
|------------|----------|
| PCL-3 | [`task3_dhcp/ip_dhcp_PCL-3.png`](task3_dhcp/ip_dhcp_PCL-3.png) |
| PCS-1 | [`task3_dhcp/ip_dhcp_PCS-1.png`](task3_dhcp/ip_dhcp_PCS-1.png) |

## Задание 4. Выход в интернет (даркстор)
- Настроен стык R-Darkstore ↔ ISP (55.55.55.105/30 и 55.55.55.106/30).
- Добавлен маршрут по умолчанию.
- Проверка:

| Проверка | Скриншот |
|----------|----------|
| ping R-Darkstore → ISP | [`task4_internet/ping_R-Darkstore_to_ISP.png`](task4_internet/ping_R-Darkstore_to_ISP.png) |
| Таблица маршрутизации R-Darkstore | [`task4_internet/show_ip_route_R-Darkstore.png`](task4_internet/show_ip_route_R-Darkstore.png) |

## Задание 5. Тестовый интернет-сервер
- На ISP добавлен интерфейс с адресом 1.1.1.2/24 (подключение к VPC с адресом 1.1.1.1).
- Проверка:

| Проверка | Скриншот |
|----------|----------|
| ping ISP → 1.1.1.1 | [`task5_test_server/ping_ISP_to_test_server.png`](task5_test_server/ping_ISP_to_test_server.png) |
| Таблица маршрутизации ISP | [`task5_test_server/show_ip_route_ISP.png`](task5_test_server/show_ip_route_ISP.png) |

## Задание 6. NAT в дарксторе
- Настроен PAT для всех внутренних VLAN.
- Проверка:

| Проверка | Скриншот |
|----------|----------|
| Конфигурация NAT (show run) | [`task6_nat_darkstore/show_run_nat_R-Darkstore.png`](task6_nat_darkstore/show_run_nat_R-Darkstore.png) |
| ping PCL-1 → 1.1.1.1 | [`task6_nat_darkstore/ping_PCL-1_to_1.1.1.1.png`](task6_nat_darkstore/ping_PCL-1_to_1.1.1.1.png) |
| ping PCS-3 → 1.1.1.1 | [`task6_nat_darkstore/ping_PCS-3_to_1.1.1.1.png`](task6_nat_darkstore/ping_PCS-3_to_1.1.1.1.png) |
| Статистика NAT | [`task6_nat_darkstore/show_ip_nat_statistics_R-Darkstore.png`](task6_nat_darkstore/show_ip_nat_statistics_R-Darkstore.png) |

## Задание 7. VLAN в головном офисе
- Настроены VLAN 10, 20, 50 на SW1-HQ и SW2-HQ.
- Trunk-порты.
- Проверка ping в одном VLAN:

| Пара | Скриншот |
|------|----------|
| PCI-1 ↔ PCI-2 | [`task7_vlan_hq/ping_PCI-1_to_PCI-2.png`](task7_vlan_hq/ping_PCI-1_to_PCI-2.png) |
| FS ↔ Mail | [`task7_vlan_hq/ping_FS_to_Mail.png`](task7_vlan_hq/ping_FS_to_Mail.png) |
| PCM-1 ↔ PCM-2 | [`task7_vlan_hq/ping_PCM-1_to_PCM-2.png`](task7_vlan_hq/ping_PCM-1_to_PCM-2.png) |

## Задание 8. Маршрутизация на R-HQ
- Субинтерфейсы для VLAN 10, 20, 50.
- Проверка между VLAN:

| Пара | Скриншот |
|------|----------|
| PCI-1 → PCM-1 | [`task8_routing_hq/ping_PCI-1_to_PCM-1.png`](task8_routing_hq/ping_PCI-1_to_PCM-1.png) |
| PCM-2 → DC | [`task8_routing_hq/ping_PCM-2_to_DC.png`](task8_routing_hq/ping_PCM-2_to_DC.png) |
| PCI-2 → DNS | [`task8_routing_hq/ping_PCI-2_to_DNS.png`](task8_routing_hq/ping_PCI-2_to_DNS.png) |

## Задание 9. DHCP в головном офисе
- Пулы для VLAN 10 и 20.
- Проверка:

| Устройство | Скриншот |
|------------|----------|
| PCI-1 | [`task9_dhcp_hq/ip_dhcp_PCI-1.png`](task9_dhcp_hq/ip_dhcp_PCI-1.png) |
| PCM-1 | [`task9_dhcp_hq/ip_dhcp_PCM-1.png`](task9_dhcp_hq/ip_dhcp_PCM-1.png) |

## Задание 10. Выход в интернет (головной офис)
- Стык R-HQ ↔ ISP (55.55.55.101/30 и 55.55.55.102/30).
- Маршрут по умолчанию.
- Проверка:

| Проверка | Скриншот |
|----------|----------|
| ping R-HQ → ISP | [`task10_internet_hq/ping_R-HQ_to_ISP.png`](task10_internet_hq/ping_R-HQ_to_ISP.png) |
| Таблица маршрутизации R-HQ | [`task10_internet_hq/show_ip_route_R-HQ.png`](task10_internet_hq/show_ip_route_R-HQ.png) |

## Задание 11. NAT в головном офисе
- PAT для всех VLAN.
- Проверка:

| Проверка | Скриншот |
|----------|----------|
| Конфигурация NAT | [`task11_nat_hq/show_run_nat_R-HQ.png`](task11_nat_hq/show_run_nat_R-HQ.png) |
| ping PCI-1 → 1.1.1.1 | [`task11_nat_hq/ping_PCI-1_to_1.1.1.1.png`](task11_nat_hq/ping_PCI-1_to_1.1.1.1.png) |
| ping PCM-1 → 1.1.1.1 | [`task11_nat_hq/ping_PCM-1_to_1.1.1.1.png`](task11_nat_hq/ping_PCM-1_to_1.1.1.1.png) |
| Статистика NAT | [`task11_nat_hq/show_ip_nat_statistics_R-HQ.png`](task11_nat_hq/show_ip_nat_statistics_R-HQ.png) |

## Задание 12. Публикация веб-сервера
- Статический DNAT: порт 8080 внешнего интерфейса → 10.10.5.60:80.
- Проверка:

| Проверка | Скриншот |
|----------|----------|
| Конфигурация с DNAT | [`task12_web_publish/show_run_nat_with_dnat.png`](task12_web_publish/show_run_nat_with_dnat.png) |
| telnet с ISP на 55.55.55.101:8080 | [`task12_web_publish/telnet_to_R-HQ_8080.png`](task12_web_publish/telnet_to_R-HQ_8080.png) |
| Трансляции NAT | [`task12_web_publish/show_ip_nat_translations.png`](task12_web_publish/show_ip_nat_translations.png) |

> **Примечание:** В моём тесте telnet не ответил (возможно, веб-сервер не был запущен), но конфигурация DNAT корректна.

## Задание 13. Связность между локациями
- Статическая маршрутизация через WAN (192.168.10.0/29 и 192.168.20.0/29).
- Проверка:

| Пара | Скриншот |
|------|----------|
| PCI-1 (HQ) → PCS-3 (Darkstore) | [`task13_wan/ping_PCI-1_to_PCS-3.png`](task13_wan/ping_PCI-1_to_PCS-3.png) |
| PCM-1 (HQ) → PCL-1 (Darkstore) | [`task13_wan/ping_PCM-1_to_PCL-1.png`](task13_wan/ping_PCM-1_to_PCL-1.png) |
| DC (HQ) → FS (Darkstore) | [`task13_wan/ping_DC_to_FS.png`](task13_wan/ping_DC_to_FS.png) |
| Таблица маршрутизации WAN | [`task13_wan/show_ip_route_WAN.png`](task13_wan/show_ip_route_WAN.png) |
| Таблица маршрутизации R-HQ | [`task13_wan/show_ip_route_R-HQ.png`](task13_wan/show_ip_route_R-HQ.png) |
| Таблица маршрутизации R-Darkstore | [`task13_wan/show_ip_route_R-Darkstore.png`](task13_wan/show_ip_route_R-Darkstore.png) |

Все тесты пройдены успешно, сеть работает согласно ТЗ.
