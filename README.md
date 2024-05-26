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
 
 разархивируем 
 ```
 tar xvfz prometheus-2.52.0.linux-amd64.tar.gz
 ```
 
 перейдем в директорию prometheus-2.52.0.linux-amd64
 ```
 cd prometheus-2.52.0.linux-amd64
 ```

 
 
![alt text](https://github.com/ysatii/gitlab-hw/blob/zabbix2/img1/image1.jpg)

 
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
1. `Создаем пользователя`
 
 ```
 sudo useradd --no-create-home --shell /bin/false prometheus
 ```

2. `Скачиваем и устанавливаем prometheus`

 ```
 wget https://github.com/prometheus/prometheus/releases/download/v2.52.0/prometheus-2.52.0.linux-amd64.tar.gz
 ```
 
 разархивируем 
 ```
 tar xvfz prometheus-2.52.0.linux-amd64.tar.gz
 ```
 
 перейдем в директорию prometheus-2.52.0.linux-amd64
 ```
 cd prometheus-2.52.0.linux-amd64
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

 
 

