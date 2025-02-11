# List of GOLD images

MyB will provide the user with tools to create and use custom cloud images. The list of images registered in (and operated on) MyB is available at [endpoint](api.md): **'/list'**.

For example:

> curl http://HOST/images

```
{
  "images": [
    "centos7",
    "centos8",
    "centos9",
    "debian10",
    "debian11",
    "dflybsd6",
    "freebsd13_ufs",
    "freebsd13_zfs",
    "freebsd14_ufs",
    "freebsd14_zfs",
    "freepbx",
    "homeass",
    "jail",
    "k8s",
    "netbsd9",
    "openbsd7",
    "openbsd70",
    "opnsense22",
    "oracle7",
    "oracle8",
    "rocky8",
    "ubuntu20",
    "ubuntu22"
  ]
}
```

The basic MyB installation comes with cloud images supported by the [CBSD](https://cbsd.io) project, but their naming may change from version to version. The name of the image is specified as the 'images' parameter when creating a new environment.

Typically, image names characterize the image of the OS distribution:

|           name            |                                   description                                  |
| ------------------------- | ------------------------------------------------------------------------------ |
|          centosX          | Linux CentOS                                                                   |
|          debianX          | Linux Debian                                                                   |
|         dflybsdX          | DragonFlyBSD OS, HAMMERFS on root                                              |
|        freebsdX_ufs       | FreeBSD with UFS on root                                                       |
|        freebsdX_zfs       | FreeBSD with ZFS on root                                                       |
|          freepbx          | FreePBX (Asterisk VoIP), please open URL after VM start: http://IP             |
|          homeass          | Home Assistant, please open URL after VM start: http://IP:8123                 |
|           jail            | Образ FreeBSD rootfs для создания контейнеров на базе FreeBSD jail, представляет из себя архив base.txz с официального сайта проекта FreeBSD |
|           k8s             | Образ для разворачивания Kubernetes инстансов                                  |
|         netbsdX           | NetBSD OS                                                                      |
|         openbsdX          | OpenBSD OS: 'openbsd7' for LATEST (7.1), 'openbsd70' - 7.0                     |
|         opnsenseX         | OPNSense, please open URL after VM start: http:/IP, lg: 'root', pw: 'opnsense' |
|          oracleX          | Linux Oracle                                                                   |
|          rockyX           | Linux Rocky                                                                    |
|         ubuntuX           | Linux Ubuntu                                                                   |
|         rabbitmq          | Образ для разворачивания RabbitMQ кластеров                                    |


---

Дальше: [Работа с jails (curl)](jail_curl.md)
