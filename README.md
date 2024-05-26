# Домашнее задание к занятию «Система мониторинга Prometheus»` - Мельник Юрий Александрович


## Задание 1

### `Установите Prometheus.`
## `Процесс выполнения`

1. `Выполняя задание, сверяйтесь с процессом, отражённым в записи лекции`
2. `Создайте пользователя prometheus`
3. `Скачайте prometheus и в соответствии с лекцией разместите файлы в целевые директории`
4. `Создайте сервис как показано на уроке`
5. `Проверьте что prometheus запускается, останавливается, перезапускается и отображает статус с помощью systemctl`


### `Требования к результату`
 Прикрепите к файлу README.md скриншот systemctl status prometheus, где будет написано: prometheus.service — Prometheus Service Netology Lesson 9.4 — [Ваши ФИО]



## Решение 1
1. `Создаем пользователя`
 
 ```
 sudo useradd --no-create-home --shell /bin/false prometheus
 ```

2. `Скачиваем и устанавливаем prometheus`

 ```
 wget https://github.com/prometheus/prometheus/releases/download/v2.52.0/prometheus-2.52.0.linux-amd64.tar.gz
 ```
 
3. `разархивируем `
 ```
 tar xvfz prometheus-2.52.0.linux-amd64.tar.gz
 ```
 
4. `перейдем в директорию prometheus-2.52.0.linux-amd64` 
 ```
 cd prometheus-2.52.0.linux-amd64
 ```

 
5. `Создадим необходимые директории и переместим в них файлы`
 ```
 mkdir /etc/prometheus/
 mkdir /var/lib/prometheus/
  
 cp ./prometheus promtool /usr/local/bin
 cp -R ./console_libraries/ /etc/prometheus/
 cp -R ./consoles/ /etc/prometheus/
 cp -R ./prometheus.yml /etc/prometheus/
 ```
 
 ![alt text](https://github.com/ysatii/prometheus/blob/main/img1/image1.jpg)
 
6. `передача прав пользователю prometheus` 
 ```
 chown -R prometheus:prometheus /etc/prometheus/ /var/lib/prometheus/
 chown -R prometheus:prometheus /usr/local/bin/prometheus
 chown -R prometheus:prometheus /usr/local/bin/promtool
 ```
7. `проверим ответ prometheus на порту 9090`
 ```
 /usr/local/bin/prometheus --config.file /etc/prometheus/prometheus.yml --storage.tsdb.path /var/lib/prometheus/ --web.console.templates=/etc/prometheus/consoles --web.console.libraries=/etc/prometheus/console_libraries
 ```
 ![alt text](https://github.com/ysatii/prometheus/blob/main/img1/image1_2.jpg)
 ![alt text](https://github.com/ysatii/prometheus/blob/main/img1/image1_3.jpg)
 ![alt text](https://github.com/ysatii/prometheus/blob/main/img1/image1_4.jpg)
 
8. `создадим сервис prometheus и проверим его работоспособность`
 ------------------
 ```
 nano /etc/systemd/system/prometheus.service
 ``` 
 
 Листинг /etc/systemd/system/prometheus.service
 ```
 [Unit]
 Description=Prometheus Service Netology Lesson 9.4 - Мельник Юрий Александрович 
 After=network.target
 [Service]
 User=prometheus
 Group=prometheus
 Type=simple
 ExecStart=/usr/local/bin/prometheus \
 --config.file /etc/prometheus/prometheus.yml \
 --storage.tsdb.path /var/lib/prometheus/ \
 --web.console.templates=/etc/prometheus/consoles \
 --web.console.libraries=/etc/prometheus/console_libraries
 ExecReload=/bin/kill -HUP $MAINPID Restart=on-failure
 [Install]
 WantedBy=multi-user.target
 ```
 ![alt text](https://github.com/ysatii/prometheus/blob/main/img1/image1_5.jpg)


 Передайте права на файл:
 ```
 chown -R prometheus:prometheus /var/lib/prometheus
 ```
 ```
 sudo systemctl enable prometheus
 sudo systemctl start prometheus
 sudo systemctl status prometheus
 ```
 
![alt text](https://github.com/ysatii/prometheus/blob/main/img1/image1_6.jpg)





 
## Задание 2

### `Установите Node Exporter.`
## `Процесс выполнения`

1. `Выполняя ДЗ сверяйтесь с процессом отражённым в записи лекции.`
2. `Скачайте node exporter приведённый в презентации и в соответствии с лекцией разместите файлы в целевые директории`
3. `Создайте сервис для как показано на уроке`
4. `Проверьте что node exporter запускается, останавливается, перезапускается и отображает статус с помощью systemctl`


### `Требования к результату`

1. `Прикрепите к файлу README.md скриншот systemctl status node-exporter, где будет написано: node-exporter.service — Node Exporter Netology Lesson 9.4 — [Ваши ФИО]`

## Решение 2
1. `Скачаем Node Exporter`
 
 ```
 wget https://github.com/prometheus/node_exporter/releases/download/v1.8.1/node_exporter-1.8.1.linux-amd64.tar.gz
 ```

2. `Перейдем в директорию Перейдем в директорию`

 ```
  cd node_exporter-1.8.1.linux-amd64
 ```
 
3. `Создадим /etc/prometheus/node-exporter`

 ```
 mkdir /etc/prometheus/node-exporter
 ```
 
4. `Скопируем файл node_exporter в /etc/prometheus/node-exporter/`

 ```
 cp ./node_exporter /etc/prometheus/node-exporter/

 ```
 
5. `Создадим сервис node-exporter.service `

 ```
 nano /etc/systemd/system/node-exporter.service 
 chown -R prometheus:prometheus /etc/prometheus/node-exporter/
 ```

6. `Листинг /etc/systemd/system/node-exporter.service`

 ```
 [Unit]
 Description=Node Exporter Lesson 9.4 - Мельник Юрий Александрович 
 After=network.target
 [Service]
 User=prometheus
 Group=prometheus
 Type=simple
 ExecStart=/etc/prometheus/node-exporter/node_exporter
 [Install]
 WantedBy=multi-user.target
 ```
 ![alt text](https://github.com/ysatii/prometheus/blob/main/img1/image2.jpg)
 
7. `Установим автозагрузку и запустим сервис`

 ```
 sudo systemctl enable node-exporter
 sudo systemctl start node-exporter
  ```
8. `Проверим состояние сервиса`
 sudo systemctl status node-exporter
 
 ![alt text](https://github.com/ysatii/prometheus/blob/main/img1/image2_1.jpg)
 ![alt text](https://github.com/ysatii/prometheus/blob/main/img1/image2_2.jpg)
 

 
 



## Задание 3

### `Подключите Node Exporter к серверу Prometheus.`


1. `Выполняя ДЗ сверяйтесь с процессом отражённым в записи лекции.`
2. `Отредактируйте prometheus.yaml, добавив в массив таргетов установленный в задании 2 node exporter`
3. `Перезапустите prometheus`
4. `Проверьте что он запустился`
### `Требования к результату`
1. `Прикрепите к файлу README.md скриншот конфигурации из интерфейса Prometheus вкладки Status > Configuration`
2. `Прикрепите к файлу README.md скриншот из интерфейса Prometheus вкладки Status > Targets, чтобы было видно минимум два эндпоинта`
## Решение 3
 
1. `Сервис prometheus до настройки`

 ![alt text](https://github.com/ysatii/prometheus/blob/main/img1/image3.jpg)

2. `Произведем настройку и перезапустим сервис`
 Листинг /etc/prometheus/prometheus.yml
 
 ```
 # my global config
 global:
  scrape_interval: 15s # Set the scrape interval to every 15 seconds. Default is every 1 minute.
  evaluation_interval: 15s # Evaluate rules every 15 seconds. The default is every 1 minute.
  # scrape_timeout is set to the global default (10s).

 # Alertmanager configuration
 alerting:
   alertmanagers:
     - static_configs:
         - targets:
           # - alertmanager:9093

 # Load rules once and periodically evaluate them according to the global 'evaluation_interval'.
 rule_files:
   # - "first_rules.yml"
   # - "second_rules.yml"

 # A scrape configuration containing exactly one endpoint to scrape:
 # Here it's Prometheus itself.
 scrape_configs:
   # The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
   - job_name: "prometheus"
 
     # metrics_path defaults to '/metrics'
     # scheme defaults to 'http'.
 
     static_configs:
       - targets: ["localhost:9090", "localhost:9100"]
 ```
 ![alt text](https://github.com/ysatii/prometheus/blob/main/img1/image3_1.jpg)
 ![alt text](https://github.com/ysatii/prometheus/blob/main/img1/image3_2.jpg)
 
3. `Сервис после перезапуска`
 
 ![alt text](https://github.com/ysatii/prometheus/blob/main/img1/image3_3.jpg)
 ![alt text](https://github.com/ysatii/prometheus/blob/main/img1/image3_4.jpg)

# Дополнительные задания со звёздочкой*
## Задание 4 *
### Интегрируйте Grafana и Prometheus.
 




### `Требования к результату`
 Прикрепите к файлу README.md скриншот дашборда (ID:11074) с поступающими туда данными из Node Exporter


## Решение 4

 
1. `Установка Grafana ` 
 ```
 sudo apt-get install -y adduser libfontconfig1 musl
 wget wget https://dl.grafana.com/oss/release/grafana_11.0.0_amd64.deb
 sudo dpkg -i grafana_11.0.0_amd64.deb
 ```
  ![alt text](https://github.com/ysatii/prometheus/blob/main/img1/image4.jpg)
  ![alt text](https://github.com/ysatii/prometheus/blob/main/img1/image4_1.jpg)
  ![alt text](https://github.com/ysatii/prometheus/blob/main/img1/image4_2.jpg)
 
2. `Запуск Grafana` 
 ```
 systemctl enable grafana-server
 systemctl start grafana-server
 systemctl status grafana-server
 ```

 




## Задание 5 *
###  Интегрируйте Grafana и Prometheus.
 
### `Требования к результату`
 Прикрепите к файлу README.md скриншот дашборда (ID:11074) с поступающими туда данными из Node Exporter

## Решение 5
 
  ![alt text](https://github.com/ysatii/prometheus/blob/main/img1/image5.jpg)
  ![alt text](https://github.com/ysatii/prometheus/blob/main/img1/image5_1.jpg)
  ![alt text](https://github.com/ysatii/prometheus/blob/main/img1/image5_2.jpg)
  ![alt text](https://github.com/ysatii/prometheus/blob/main/img1/image5_3.jpg)
  ![alt text](https://github.com/ysatii/prometheus/blob/main/img1/image5_4.jpg)
 
 

