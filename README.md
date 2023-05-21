# hw-9-05_mon_prometheus2
HW-9-05_Система мониторинга Prometheus. Часть 2

# Домашнее задание к занятию «Система мониторинга Prometheus. Часть 2»

### Задание 1

Создайте файл с правилом оповещения, как в лекции, и добавьте его в конфиг Prometheus.

#### Процесс выполнения

Создадим конфиг-файл **netology-test.yml** с правилом оповещения:
```
nano /etc/prometheus/netology-test.yml
```
```
groups: # Список групп

- name: netology-test # Имя группы
  rules: # Список правил текущей группы
  - alert: InstanceDown # Название текущего правила
    expr: up == 0 # Логическое выражение
    for: 1m # Сколько ждать отбоя сработки перед отправкой оповещения
    labels:
      severity: critical # Критичность события
    annotations: # Описание
      description: '{{ $labels.instance }} of job {{ $labels.job }} has been down for more than 1 minute.' # Полное описание оповещения
      summary: Instance {{ $labels.instance }} down # Краткое описание оповещения
```
Присвоим пользователю **prometheus** права доступа с созданному конфиг-файлу **netology-test.yml**:
```
chown prometheus:prometheus /etc/prometheus/netology-test.yml
```
Подключим правило **InstanceDown** к **Prometheus**:
```
cd /etc/prometheus
nano ./prometheus.yml
```
В конфиг-файле **prometheus.yml** найдем раздел **rule_files:** и пропишем там конфиг-файл **netology-test.yml**
своего правила:
```
rule_files:
  - "netology-test.yml"
```
<kbd>![Раздел rule_files в prometheus.yml](img/prometheus_config_rule_files.png)</kbd>

Остановим сервис **node_exporter.service**:
```
systemctl stop node_exporter.service
systemctl status node_exporter.service
```
Работа сервиса остановлена:

<kbd>![Сервис node_exporter остановлен](img/node_exporter_status_stopped.png)</kbd>

Скриншот раздела оповещений **Alerts** в **Prometheus**:

<kbd>![Prometheus Alerts Pending Status](img/prometheus_alerts_pending.png)</kbd>


---

### Задание 2

Установите Node Exporter.

#### Процесс выполнения

2. Скачаем **Node Exporter 1.5.0** из официального репозитория:

```
cd
wget https://github.com/prometheus/node_exporter/releases/download/v1.5.0/node_exporter-1.5.0.linux-amd64.tar.gz
```
Распакуем архив **node_exporter-1.5.0.linux-amd64.tar.gz**:
```
tar xvfz node_exporter-1.5.0.linux-amd64.tar.gz
```
Переходим в созданную директорию:
```
cd node_exporter-1.5.0.linux-amd64.tar.gz
```
Создадим директорию **/etc/prometheus/node-exporter** и скопируем туда файл **node_exporter**:
```
mkdir /etc/prometheus/node-exporter
cp ./node_exporter /etc/prometheus/node-exporter/
```
Передадим права файл **node_exporter** нашему пользователю **prometheus**:
```
chown prometheus:prometheus /etc/prometheus/node-exporter/node_exporter
```
Проверим работоспособность **node_exporter**:

<kbd>![Запуск node_exporter без создания сервиса](img/node_exporter_manual_start.png)</kbd>

3. Создадим сервис **node-exporter.service** для автоматического запуска утилиты:
```
nano /etc/systemd/system/node-exporter.service
```
```
[Unit]
Description=Node Exporter Lesson 9.4
After=network.target
[Service]
User=prometheus
Group=prometheus
Type=simple
ExecStart=/etc/prometheus/node_exporter/node_exporter
[Install]
WantedBy=multi-user.target
```
Включим автозапуск сервиса:
```
systemctl enable node-exporter.service
```
Запустим новый сервис и проверим его статус:
```
systemctl start node-exporter.service
systemctl status node-exporter.service
```
<kbd>![Статус работы сервиса node_exporter](img/node_exporter_service_status.png)</kbd>

---

### Задание 3

Подключите Node Exporter к серверу Prometheus.

#### Процесс выполнения
2. Добавление нашего end-point, чтобы **Prometheus** начал опрашивать с него данные:
```
cd
nano /etc/prometheus/prometheus.yml
```
Найдем раздел **scrape_configs** и добавим в него информацию о порте, на котором работает **node_exporter**
- **localhost:9100**:

```
static_configs:
  -targets ["localhost:9090", "localhost:9100"]
```
<kbd>![Добавление нашего end-point в prometheus.yml](img/scrape_configs_updated.png)</kbd>

Перезапустим сервис **prometheus.service**:
```
systemctl restart prometheus.service
```
Проверим статус работы сервиса:
```
systemctl status prometheus.service
```
<kbd>![Повторная проверка статуса prometheus.service](img/prometheus_service_status_1.png)</kbd>

Скриншот раздела Prometheus **Status** -> **Configuration**:

<kbd>![Status -> Configuration](img/prometheus_status_configuration.png)</kbd>

Скриншот раздела Prometheus **Status** -> **Targets**:

<kbd>![Status -> Targets](img/prometheus_status_targets.png)</kbd>
