## Задание 1. Настройка VLAN на коммутаторах даркстора

**Что было сделано:**
- На коммутаторах SW1-Darkstore, SW2-Darkstore, SW3-Darkstore созданы VLAN 30 (Logistics), VLAN 40 (Storage), VLAN 60 (DS-Servers).
- Пользовательские порты переведены в режим access с соответствующими VLAN.
- Все соединения между коммутаторами и маршрутизатором R-Darkstore настроены как trunk-порты с разрешёнными VLAN 30,40,60.
- Клиентским устройствам временно назначены статические IP-адреса из соответствующих подсетей (например, PCL-1 получил 10.10.3.1/24) для проверки связности до настройки DHCP.

**Результаты проверки:**
Связность между устройствами в пределах одного VLAN проверена с помощью `ping`. Все пинги успешны, что подтверждает корректную работу VLAN и trunk-портов.

| Проверяемая пара | VLAN | Скриншот |
|------------------|------|----------|
| PCL-1 → PCL-2 | VLAN 30 (Logistics) | [`ping_PCL-1_to_PCL-2.png`](task1_vlan/ping_PCL-1_to_PCL-2.png) |
| PCL-3 → PCL-4 | VLAN 30 (Logistics) | [`ping_PCL-3_to_PCL-4.png`](task1_vlan/ping_PCL-3_to_PCL-4.png) |
| PCL-4 → PCL-3 (обратный) | VLAN 30 (Logistics) | [`ping_PCL-4_to_PCL-3.png`](task1_vlan/ping_PCL-4_to_PCL-3.png) |
| PCS-1 → PCS-2 | VLAN 40 (Storage) | [`ping_PCS-1_to_PCS-2.png`](task1_vlan/ping_PCS-1_to_PCS-2.png) |
| Portal → FS | VLAN 60 (DS-Servers) | [`ping_Portal_to_FS.png`](task1_vlan/ping_Portal_to_FS.png) |

**Вывод:** Настройка VLAN и trunk-соединений выполнена корректно, устройства внутри одной VLAN видят друг друга.
