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

### ``
## `Процесс выполнения`

1. `Выполняя ДЗ сверяйтесь с процессом отражённым в записи лекции.`
2. `Скачайте node exporter приведённый в презентации и в соответствии с лекцией разместите файлы в целевые директории`
3. `Создайте сервис для как показано на уроке`
4. `Проверьте что node exporter запускается, останавливается, перезапускается и отображает статус с помощью systemctl`


### `Требования к результату`

1. `Прикрепите к файлу README.md скриншот systemctl status node-exporter, где будет написано: node-exporter.service — Node Exporter Netology Lesson 9.4 — [Ваши ФИО]`

## Решение 2
1. ` 
 
 ```
  
 ```

2. ` `

 ```
  
 ```
 





## Задание 3

### `Привяжите созданный шаблон к двум хостам. Также привяжите к обоим хостам шаблон Linux by Zabbix Agent.`


1. `Выполняя ДЗ сверяйтесь с процессом отражённым в записи лекции.`
2. `Отредактируйте prometheus.yaml, добавив в массив таргетов установленный в задании 2 node exporter`
3. `Перезапустите prometheus`
4. `Проверьте что он запустился`
### `Требования к результату`
 Прикрепите к файлу README.md скриншот конфигурации из интерфейса Prometheus вкладки Status > Configuration
 Прикрепите к файлу README.md скриншот из интерфейса Prometheus вкладки Status > Targets, чтобы было видно минимум два эндпоинта
## Решение 3
 
1. `Установим Zabbix Agent на 2 виртмашины`
![alt text](https://github.com/ysatii/gitlab-hw/blob/zabbix2/img1/image2.jpg)


 

 

# Дополнительные задания со звёздочкой*
## Задание 4 *
### Интегрируйте Grafana и Prometheus.
 




### `Требования к результату`
 Прикрепите к файлу README.md скриншот дашборда (ID:11074) с поступающими туда данными из Node Exporter


## Решение 4

 
1. `` 




## Задание 5 *
###  Интегрируйте Grafana и Prometheus.
 
### `Требования к результату`
 Прикрепите к файлу README.md скриншот дашборда (ID:11074) с поступающими туда данными из Node Exporter

## Решение 5
 
![alt text](https://github.com/ysatii/gitlab-hw/blob/zabbix2/img1/image5.jpg)

 
 

