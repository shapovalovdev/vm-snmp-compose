# vm-snmp-compose


Запуск контейнеров

```
$ docker compose up -d
```

Поднимит контейнеры в фоновом режиме

Посмотреть статус запуска можно через 

```
$ docker compose top
$ docker compose ps 
```

### Из чего состоит композ

#### vm-agent

Этот сервис отвечает за собирание метрик с экспортеров.

Он запущен с prometheus.yml конфигом, который подтягивается с хоста.

#### snmp-exporter

Наш единственный экспортер. Собирает метрики с SNMP таргетов.

Он запущен с snmp.yml конфигом, который подтягивается с хоста.

#### victoria-metrics

База данных. В неё пишет метрики vmagent через remoteWrite.

Опции запуска указаны в docker-compose.yml

### Какие есть конфиги?

#### Prometheus.yml

Конфиг vmagent. В нём указываются jobs, которые собирают метрики. В частности мы сделали job eltex для snmp-exporter.

#### snmp.yml

Про него написано в гитхабе snmp-exporter. Чтобы его получить, нужно иметь MIB файлы устройста, с которого собирают метрики и сгенерировать с помощью generator.

#### Что почитать дополнительно?

https://monhouse.tech/vmagent-kombajn-dlya-monitoringa-nikolaj-hramchihin-victoriametrics/ более подробно про vmagent

https://habr.com/ru/articles/568090/
