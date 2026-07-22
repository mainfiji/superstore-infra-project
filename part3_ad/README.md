# Часть 3. Настройка Active Directory

## Задание 1. Развёртывание AD
- На Windows Server установлены роли AD DS и DNS.
- Сервер повышен до контроллера домена `practicumsuperstore.local`.
- Создана OU `IT`.
- Создан пользователь `student` (Ф.И.О. указаны в скриншоте).
- Создана GPO `IT-policy`, которая выводит заголовок «Поздравляем» и текст «Политика успешно применена!» при входе.
- Клиентский компьютер `PCI-1` введён в домен и перемещён в OU `IT`.

## Проверки:

| Проверка | Скриншот |
|----------|----------|
| Active Directory Users and Computers (OU IT, пользователь student, компьютер PCI-1) | [`ad_users_computers.png`](ad_users_computers.png) |
| Group Policy Management (политика для IT) | [`gpmc_policy.png`](gpmc_policy.png) |
| Клиент присоединён к домену (свойства системы) | [`client_joined_domain.png`](client_joined_domain.png) |
| Приветственное сообщение после входа пользователя student | [`logon_message.png`](logon_message.png) |

Политика применена успешно.
