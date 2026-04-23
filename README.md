# Звіт: Адміністрування користувачів та керування командними інтерпретаторами в GNU/Linux  
**Виконав:** Виноградов Антон  

---

## 1. Встановлення та конфігурування командних інтерпретаторів

Для розширення функціональних можливостей системи та виконання завдань згідно з регламентом лабораторної роботи було проведено інсталяцію альтернативних оболонок **Zsh** та **Fish**.

| Пакет | Опис інтерпретатора | Команда інсталяції |
|:---:|:---|:---:|
| **Zsh** | Потужна оболонка з підтримкою плагінів та тем. | `sudo apt install zsh` |
| **Fish** | Інтерактивна оболонка з автодоповненням та підказками. | `sudo apt install fish` |

> **Статус:** Середовище підготовлено, інтерпретатори встановлено успішно.

<p align="center">
  <img src="https://i.ibb.co/0RFx4pwW/photo-2026-03-23-18-42-51.jpg" width="70%" />
</p>

---

## 2. Керування обліковими записами та групами

Було створено структуру користувачів, що імітує організаційну модель підприємства. Для кожної ролі визначено відповідну групу та політику доступу.

| Етап | Технічна дія | Візуалізація |
|:---:|:---|:---:|
| 01 | Створення груп користувачів | <img src="https://i.ibb.co/p63Gz8bV/photo-2026-03-23-19-15-50.jpg" width="200px" /> |
| 02 | Створення облікових записів (10 користувачів) | <img src="https://i.ibb.co/p6hTkBZ6/photo-2026-03-23-19-19-26.jpg" width="200px" /> |
| 03 | Призначення оболонок користувачам | <img src="https://i.ibb.co/5hCqL7FK/photo-2026-03-23-19-34-10.jpg" width="200px" /> |

---

## 3. Технічна реалізація конфігурації

```bash
# Оновлення системи та встановлення оболонок
sudo apt update && sudo apt upgrade -y
sudo apt install zsh fish -y

# Створення груп
sudo groupadd tech_support
sudo groupadd developers
sudo groupadd financiers
sudo groupadd founders
sudo groupadd guests

# Створення користувачів із призначенням shell

# Tech Support (Bash)
sudo useradd -m -g tech_support -s /bin/bash tech1
sudo useradd -m -g tech_support -s /bin/bash tech2

# Developers (Zsh)
sudo useradd -m -g developers -s /usr/bin/zsh dev1
sudo useradd -m -g developers -s /usr/bin/zsh dev2

# Founders (Fish)
sudo useradd -m -g founders -s /usr/bin/fish founder1
sudo useradd -m -g founders -s /usr/bin/fish founder2

# Financiers (обмежений доступ)
sudo useradd -m -g financiers -s /usr/sbin/nologin fin1
sudo useradd -m -g financiers -s /usr/sbin/nologin fin2

# Guests (обмежений доступ)
sudo useradd -m -g guests -s /usr/sbin/nologin guest1
sudo useradd -m -g guests -s /usr/sbin/nologin guest2
4. Верифікація та демонстрація роботи середовищ

Для перевірки налаштувань виконано тестове перемикання користувачів через su - та виконання базових команд.

Базові перевірки:
whoami
date
uptime
Перевірка входу:
su - dev1
su - fin1

Очікуваний результат для обмежених користувачів:

This account is currently not available.
Порівняльна таблиця доступу
Користувач	Група	Shell	Статус
tech1	tech_support	Bash	Дозволено
dev1	developers	Zsh	Дозволено
founder1	founders	Fish	Дозволено
fin1	financiers	nologin	Заборонено
guest1	guests	nologin	Заборонено
<p align="center"> <img src="https://i.ibb.co/yBPJbrST/image.png" width="30%" /> <img src="https://i.ibb.co/Z1XDs5qW/image.png" width="30%" /> <img src="https://i.ibb.co/C5dft39T/image.png" width="30%" /> </p>
5. Висновки
1. Розподіл оболонок

Використання різних інтерпретаторів (Bash, Zsh, Fish) дозволяє:

оптимізувати роботу під різні ролі;
підвищити продуктивність розробників;
забезпечити гнучкість адміністрування.
2. Безпека системи

Використання /usr/sbin/nologin:

повністю блокує інтерактивний доступ;
дозволяє зберігати облікові записи без ризику входу;
є стандартною практикою захисту Linux-систем.
6. Фінальний аудит системи
<p align="center"> <a href="https://ibb.co/1Jm2k3d9"> <img src="https://i.ibb.co/Z1MT03Yh/image.png" width="70%" /> </a> </p> ```
