# Работа с jail (curl)

## Описание

Jail образ представляет собой очень легковесный контейнер на базе FreeBSD jail, в котором вы можете работать как обычном окружении FreeBSD.
Контейнера могут быть с RO базой (применяется nullfs для создания нового окружения), с записью в каталоги /etc, /var, /usr/local, /tmp, /home, так и полноценные RW контейнера (более тяжелые, поскольку для
каждого контейнера будет создана новая копия rootfs). Также, контейнера могут быть созданы с виртуальным сетевым стеком (VNET/VIMAGE). Обратитесь к официальному руководству FreeBSD для получения подробной информации.

Также, возможно задать ограничения по ресурсам контейнера параметрами 'imgsize','cpus', ram'.

При создании контейнера, вы можете задать hostname/FQDN окружения через параметр 'host_hostname'.
При создании контейнера, вы можете установить ПО, доступное для FreeeBSD, указав через пробел списки пакетов в параметре 'pkglist'.

## Создание jail

Для создания контейнера, используйте [endpoint](api.md): **'/api/v1/create/'**.

Минимальный payload для создания окружения на базе jail:

```
{
  "image": "jail",
  "pubkey": "ssh-ed25519 AAAA..XXX your@localhost"
}
```

Например:

1)
```
cat > jail.json <<EOF
{
 "image": "jail",
 "pubkey": "ssh-ed25519 AAAA..XXX your@localhost"
}
```

2)
> curl --no-progress-meter -X POST -H "Content-Type: application/json" -d @jail.json http://HOST/api/v1/create/jail1

Пример payload для создания контейнера 'secret.place' с ограничением в 1 ядро, дисковым пространством 10g, 2g RAM и с установленным пакетом bash:
```
{
  "image": "jail",
  "host_hostname": "secret.place",
  "imgsize": "10g",
  "ram": "2g",
  "cpus": "2",
  "pkglist": "bash",
  "pubkey": "ssh-ed25519 AAAA..XXX your@localhost"
}

```

Обратите внимание, что время на создания первого контейнера зависит от наличия образа 'jail' и качества вашего Internet соединения. 
Рекомендуется через запуск 'jail' в  шелл оболочки администраторской консоли сначала получить образ. Если вы этого не сделаете, при запросе на /create,
система автоматически сначала выкачает архив rootfs для FreeBSD, затем распакует на файловую систему и только после этого создаст и запустит контейнер. 
Все последующие запуски контейнеров будут происходить мгновенно.


## Статус jail

Для просмотра информации по контейнеру, используйте свой token/CID и [endpoint](api.md): **'/api/v1/status/'**, например:

1) Если не знаете свой токен, получите его из вашего pubkey:
>  md5sum -qs 'ssh-ed25519 AAAA..XXX your@localhost'
> 90af7aa8bc164240521753a105df6a05

2) Посмотреть информацию по контейнеру jail1, используя токен:
> curl -H cid:90af7aa8bc164240521753a105df6a05 http://HOST/api/v1/status/jail1

Среди информации по статусу окружения, вы можете найти порт (он может быть динамический, если используется expose портов) и IP адрес для соединения в контейнер через SSH.


## Удаление jail

Для удаления jail, используйте свой token/CID и [endpoint](api.md): **'/api/v1/status/'**, например:

1) Если не знаете свой токен, получите его из вашего pubkey:
>  md5sum -qs 'ssh-ed25519 AAAA..XXX your@localhost'
> 90af7aa8bc164240521753a105df6a05

2) Удалите контейнер с использованием вашего токена:
> curl -H cid:90af7aa8bc164240521753a105df6a05 http://HOST/api/v1/destroy/jail1


---

Дальше: [Работа с ВМ (curl)](bhyve_curl.md)

