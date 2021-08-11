# Руководство по установке Home Assistant для Raspberry Pi 3 с помощью Docker

## Для Windows

Удобный SSH клиент - <https://www.putty.org/>

## Образ системы для Raspberry

Raspberry Pi OS Lite
страница загрузки - <https://www.raspberrypi.org/software/operating-systems/>

Ссылка на образ - <https://downloads.raspberrypi.org/raspios_lite_armhf/images/raspios_lite_armhf-2021-05-28/2021-05-07-raspios-buster-armhf-lite.zip>

Разворачиваем образ на носитель и создаем в корневом каталоге пустой файл с именем ssh

Логин и пароль по умолчанию - pi / raspberry

``` bash
cd /
sudo touch ssh
sudo reboot
```

### Обновление системы

``` bash
sudo apt update && sudo apt upgrade -y
```

### Обновление прошивки

``` bash
sudo rpi-update
```

### Перезагрузка

``` bash
sudo reboot
```

### Добавляем пользователя

``` bash
sudo adduser <имя пользователя>
sudo usermod -aG sudo <имя пользователя>
```

Переключение на нового пользователя - su <имя пользователя>

### Настраиваем систему

``` bash
sudo raspi-config
```

8 Update - обновление приложение
5 Localisation Options / I1 Change Locale - ищем и выбираем пробелом ru_RU.UTF-8 UTF-8
5 Localisation Options / I2 Change Timezone - выбираем часовой пояс
1 Add Wi-Fi

### Проверка сетевых интерфейсов

``` bash
ifconfig
```

## Установка avahi

``` bash
```

## Установка docker

``` bash
sudo curl -fsSL get.docker.com -o get-docker.sh && sh get-docker.sh
sudo groupadd docker
sudo gpasswd -a $USER docker
newgrp docker
```

## Устанавливаем Portainer

``` bash
docker pull portainer/portainer-ce
docker volume create portainer_data
docker run -d -p 9000:9000 --name portainer --restart always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce
```

Веб интерфейс Portainer - <http://raspberrypi.local:9000>

## Устанавливаем Home Assistant как контейнер

```bash
cd 

mkdir home-assistant

pwd

docker run -d -p --name homeassistant --privileged --restart=unless-stopped -e TZ=Europe/Moscow -v /home/suting/home-assist:/config --network=host ghcr.io/home-assistant/raspberrypi3-homeassistant:stable
```

Веб интерфейс Home Assistant - <http://raspberrypi.local:8123>
