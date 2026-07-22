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

## Задание 2. Настройка маршрутизации на R-Darkstore

**Что было сделано:**
- На маршрутизаторе R-Darkstore созданы субинтерфейсы (sub-interfaces) для маршрутизации между VLAN:
  - `Ethernet0/0.30` — VLAN 30 (Logistics) с IP 10.10.3.1/24
  - `Ethernet0/0.40` — VLAN 40 (Storage) с IP 10.10.4.1/24
  - `Ethernet0/1.60` — VLAN 60 (DS-Servers) с IP 10.10.6.1/24
- Каждый субинтерфейс выполняет роль шлюза по умолчанию для своей подсети.
- Проверена доступность шлюзов с устройств из соответствующих VLAN, а также межсетевое взаимодействие между VLAN 30 и 40.

**Результаты проверки:**

**1. Доступность шлюзов по умолчанию:**

| Устройство | VLAN | Шлюз | Результат | Скриншот |
|------------|------|------|-----------|----------|
| PCL-1 | 30 (Logistics) | 10.10.3.1 | Успешно (TTL=255) | [`ping_PCL-1_to_gateway.png`](task2_routing/ping_PCL-1_to_gateway.png) |
| PCS-1 | 40 (Storage) | 10.10.4.1 | Успешно (TTL=255) | [`ping_PCS-1_to_gateway.png`](task2_routing/ping_PCS-1_to_gateway.png) |
| FS | 60 (DS-Servers) | 10.10.6.1 | Успешно (TTL=255) | [`ping_FS_to_gateway.png`](task2_routing/ping_FS_to_gateway.png) |
| Portal | 60 (DS-Servers) | 10.10.6.1 | Успешно (TTL=255) | [`ping_Portal_to_gateway.png`](task2_routing/ping_Portal_to_gateway.png) |

> **TTL=255** в ответах от шлюза говорит о том, что шлюз (маршрутизатор) отвечает сам, без дополнительных пересылок.

**2. Межсетевое взаимодействие между VLAN:**

| Проверяемая пара | Из VLAN | В VLAN | Результат | Скриншот |
|------------------|---------|--------|-----------|----------|
| PCL-1 → PCS-2 | 30 (Logistics) | 40 (Storage) | Успешно (TTL=63) | [`ping_PCL-1_to_PCS-2.png`](task2_routing/ping_PCL-1_to_PCS-2.png) |
| PCL-3 → PCS-3 | 30 (Logistics) | 40 (Storage) | Успешно (TTL=63) | [`ping_PCL-3_to_PCS-3.png`](task2_routing/ping_PCL-3_to_PCS-3.png) |
| PCL-4 → PCS-1 | 30 (Logistics) | 40 (Storage) | Успешно (TTL=63) | [`ping_PCL-4_to_PCS-1.png`](task2_routing/ping_PCL-4_to_PCS-1.png) |

> **TTL=63** — это признак того, что пакет прошёл через маршрутизатор (R-Darkstore), который уменьшил TTL на 1 (с 64 до 63). Это подтверждает, что межсетевая маршрутизация работает корректно.

**Вывод:** Субинтерфейсы на R-Darkstore настроены правильно. Шлюзы доступны для всех VLAN, а маршрутизация между VLAN 30 и 40 функционирует штатно.
