# Установка и настройка CENTOS в leaseweb для clickhouse

Для clickhouse рекомендован RAID6 для случая когда больше 4 дисков. Притом RAID должен быть software. Лизвеб из коробки так не умеет. Поэтому нужно было восползоватья pxe


# Нужно опубликовать файл pxe и kickstart
Я для каждой ноды делал свой ipxе и какстарт файл, копируя шаблон и седом меняя айпишник.

Настроить PXE boot
curl --request POST \
  --url https://api.leaseweb.com/bareMetals/v2/servers/12345/leases \
  --header 'X-Lsw-Auth: 213423-2134234-234234-23424' \
  --header 'content-type: application/json' \
  --data '{
    "bootFileName": "https://raw.githubusercontent.com/epanoff/centos7_kickstart/master/ipxe"
}'

# Рестарт сервера
Настройка PXE не подразумеват что серверы будут перезагружены.
Можно так же через апи их перезагрузить, я же просто заходил на них и ребутил
or i in 83.149.119.138 83.149.119.139 83.149.119.140 83.149.119.141 83.149.119.142 83.149.119.144 83.149.119.145;do ssh -i .ssh/id_rsa_gitlab root@$i reboot ;done

# Удаление PXE boot
Если вовремя не удалить, то будет переустанавливаться вечно.
curl --request DELETE \
  --url https://api.leaseweb.com/bareMetals/v2/servers/12345/leases \
  --header 'X-Lsw-Auth: 213423-2134234-234234-23424'
Leaseweb api
