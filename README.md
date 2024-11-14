# Методичка по установке Grafana + Prometheus + Node Exporter + VictoriaMetrics
## 1. Введение

### Данный документ описывает процесс установки и базовой настройки системы мониторинга на основе Grafana, Prometheus, Node Exporter и VictoriaMetrics.
## 2. Установка Prometheus
#### Шаги:

    Скачайте последнюю версию Prometheus с официального сайта:

wget https://github.com/prometheus/prometheus/releases/download/v2.x.x/prometheus-2.x.x.linux-amd64.tar.gz

## Распакуйте архив:
```
tar -xvzf prometheus-2.x.x.linux-amd64.tar.gz
cd prometheus-2.x.x.linux-amd64
```
## Запустите Prometheus:
```
    ./prometheus --config.file=prometheus.yml

    Настройте Prometheus в файле prometheus.yml (по умолчанию можно оставить для базового запуска).
```
## 3. Установка Node Exporter
Шаги:

    Скачайте Node Exporter с официального репозитория Prometheus:
```
wget https://github.com/prometheus/node_exporter/releases/download/vX.X.X/node_exporter-X.X.X.linux-amd64.tar.gz
```
Распакуйте архив:
```
tar -xvzf node_exporter-X.X.X.linux-amd64.tar.gz
cd node_exporter-X.X.X.linux-amd64
```
Запустите Node Exporter:
```
    ./node_exporter
```
    Убедитесь, что Node Exporter доступен по адресу http://localhost:9100/metrics.

## 4. Установка VictoriaMetrics
Шаги:

    Скачайте VictoriaMetrics с официального сайта:
```
wget https://github.com/VictoriaMetrics/VictoriaMetrics/releases/download/vX.X.X/victoria-metrics-linux-amd64-vX.X.X.tar.gz
```
### Распакуйте архив:
```
tar -xvzf victoria-metrics-linux-amd64-vX.X.X.tar.gz
cd victoria-metrics-linux-amd64
```
Запустите VictoriaMetrics:

./victoria-metrics-prod -retentionPeriod=1 -storageDataPath=/path/to/data

Настройте Prometheus для отправки данных в VictoriaMetrics, добавив в prometheus.yml:

    remote_write:
      - url: "http://localhost:8428/api/v1/write"

## 5. Установка Grafana
Шаги:

    Добавьте репозиторий Grafana и установите её:
```
sudo apt-get install -y software-properties-common
sudo add-apt-repository "deb https://packages.grafana.com/oss/deb stable main"
sudo apt-get update
sudo apt-get install grafana
```
## Запустите Grafana:
```
    sudo systemctl start grafana-server
    sudo systemctl enable grafana-server

    Откройте интерфейс Grafana по адресу http://localhost:3000 (логин/пароль по умолчанию: admin / admin).
    Настройте источник данных:
        Перейдите в "Configuration" > "Data Sources".
        Добавьте Prometheus или VictoriaMetrics как источник.
```
## 6. Настройка интеграции

    Настройте Prometheus для сбора метрик от Node Exporter, добавив в prometheus.yml:
```
scrape_configs:
  - job_name: 'node_exporter'
    static_configs:
      - targets: ['localhost:9100']
```
В Grafana создайте дашборды для визуализации метрик, полученных от Prometheus или VictoriaMetrics.



Необходимые для работы скрины


### Демонстрация графаны
<img width="1440" alt="изображение" src="https://github.com/user-attachments/assets/a594de64-63b4-4066-97cd-61f2d745bb11">


### Файл Docker-compose.yaml
<img width="711" alt="изображение" src="https://github.com/user-attachments/assets/a52805b6-ce25-4e6e-af7c-12f1a438ecbd">

<img width="711" alt="изображение" src="https://github.com/user-attachments/assets/01b0407b-15fe-49f8-bacc-664ac8d649b6">

<img width="711" alt="изображение" src="https://github.com/user-attachments/assets/52660510-3b32-478e-af38-21364735fc43">

<img width="711" alt="изображение" src="https://github.com/user-attachments/assets/2d4adbd6-5af7-4508-a18d-9e998cf60923">

<img width="711" alt="изображение" src="https://github.com/user-attachments/assets/67f1cfea-c747-456e-ab7d-59793ef05377">


### Демонстрация имени юзера и файловой архитектуры

<img width="711" alt="изображение" src="https://github.com/user-attachments/assets/62d85eb2-f97d-489b-835b-f3e7d1a2006b">

### Демонстрация прометеуса

<img width="1440" alt="изображение" src="https://github.com/user-attachments/assets/ef6971be-1d0b-468c-ab19-d925cefe027d">

### П





