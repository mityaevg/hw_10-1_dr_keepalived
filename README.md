# hw-9-04_mon_prometheus1
HW-9-04_Система мониторинга Prometheus. Часть 1

# Домашнее задание к занятию «Система мониторинга Prometheus. Часть 1»

### Задание 1

Установите Prometheus.

#### Процесс выполнения

2. Создадим пользователя **prometheus**:
```
su -
```
```
useradd --no-create-home --shell /bin/false prometheus
```
3. Скачивание **Prometheus 2.44.0** из официального репозитория: 
```
wget https://github.com/prometheus/prometheus/releases/download/v2.44.0/prometheus-2.44.0.linux-amd64.tar.gz
```
Распаковываем файлы из архива **prometheus-2.44.0.linux-amd64.tar.tz** и переходим в созданную директорию:
```
tar xvfz prometheus-2.44.0.linux-amd64.tar.tz
cd prometheus-2.44.0.linux-amd64.tar.tz/
```
Создадим директории, необходимые для работы **Prometheus**:
```
mkdir /etc/prometheus/
mkdir /var/lib/prometheus
```
Скопируем утилиты **prometheus** и **promtool** в директорию **/usr/local/bin**:
```
cp ./prometheus promtool /usr/local/bin
```
Скопируем директорию **console_libraries** в **/etc/prometheus**:
```
cp -R ./console_libraries /etc/prometheus
```
Скопируем директорию **consoles** в **/etc/prometheus**:
```
cp -R ./consoles /etc/prometheus
```
Скопируем файл конфигурации **prometheus.yml** в **/etc/prometheus**:
```
cp ./prometheus.yml /etc/prometheus
```
Проверим содержимое директории **/etc/prometheus**:

<kbd>![Содержимое директории /etc/prometheus](img/etc_prometheus_contents.png)</kbd>

Все необходимые на данном этапе объекты: **console_libraries** (директория), **consoles** (директория)
и **prometheus.yml** (конфиг-файл) находятся на месте.

Передадим пользователю **prometheus** права ко всех необходимым объектам:
```
chown -R prometheus:prometheus /etc/prometheus

4. Создал item **CPU Load** (`system.cpu.util[all,system]`).
5. Создал item **RAM Load** (`vm.memory.size[pused]`).

<kbd>![Шаблон Assignment 1](img/template_assigment1.png)</kbd>

<kbd>![Items Assignment 1](img/items_assignment1.png)</kbd>

---

### Задание 2

Добавьте в Zabbix два хоста и задайте им имена <фамилия и инициалы-1> и <фамилия и инициалы-2>. Например: ivanovii-1 и ivanovii-2.

#### Процесс выполнения

5. Прикрепил к хостам **mityaevgv-1** и **mityaevgv-2** шаблон **Linux by Zabbix agent**:

<kbd>![Список хостов](img/hosts.png)</kbd>

6. Проверил раздел **Monitoring** -> **Latest data**:

<kbd>![Assignment 2 Latest data](img/latest_data_1.png)</kbd>

<kbd>![Assignment 2 Latest data](img/latest_data_2.png)</kbd>

---

### Задание 3

Привяжите созданный шаблон к двум хостам. Также привяжите к обоим хостам шаблон Linux by Zabbix Agent.

#### Процесс выполнения
2. Дополнительно прикрепил шаблон **Assignment 1** к каждому хосту:

<kbd>![Прикрепил шаблон Assignment 1 к хостам](img/template_assigment1_added.png)</kbd>

3. Проверил раздел **Monitoring** -> **Latest data** с учетом внесенных изменений:

<kbd>![Latest data только для Assignment 1 шаблона](img/latest_data_assignment1_only.png)</kbd>

---

### Задание 4

Создайте свой кастомный дашборд.

#### Процесс выполнения
2. Создал новый дэшборд **Assignment 4**.
3. Разместил на дэшборде 4 графика: **CPU Utilisation**, **Available RAM**, **Load Average (15m)** и **Disk Space (in use)**.

<kbd>![Дэшборд Assignment 4_1](img/dashboard_assignment4_1.png)</kbd>

<kbd>![Дэшборд Assignment 4_2](img/dashboard_assignment4_2.png)</kbd>

<kbd>![Дэшборд Assignment 4_3](img/dashboard_assignment4_3.png)</kbd>

---


