Raspberry Pi OS Lite
Загрузка программы для записи образа - https://www.raspberrypi.org/software/

Обновляем bootloader для загрузки с USB

Удобный SSH клиент - https://www.putty.org/

Разворачиваем образ на носитель и создаем в корневом каталоге пустой файл ssh

Логин и пароль по умолчанию - pi / raspberry

Обновление списка пакетов и пакетов
sudo apt update
sudo apt upgrade -y

Обновление прошивки
sudo rpi-update

Перезагрузка
sudo reboot

Добавление пользователя - 
sudo adduser имя

Добавление в группу sudo - 
sudo usermod -aG sudo имя

Переключение на нового пользователя - su имя


Приложение для настройки - sudo raspi-config
8 Update - обновление приложение
5 Localisation Options / I1 Change Locale - ищем и выбираем пробелом ru_RU.UTF-8 UTF-8
5 Localisation Options / I2 Change Timezone - выбираем часовой пояс
1 Add Wi-Fi

Проверка сетевых интерфейсов
ifconfig

Установка docker - 
sudo curl -fsSL get.docker.com -o get-docker.sh && sh get-docker.sh

Добавляем группу docker и добавляем в нее пользователя
sudo groupadd docker
sudo gpasswd -a $USER docker
newgrp docker

ставим Portainer - 
docker pull portainer/portainer-ce
docker volume create portainer_data
docker run -d -p 9000:9000 --name portainer --restart always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce

Веб интерфейс Portainer - IP adress:9000

## Устанавливаем Home Assistant как контейнер

```bash
cd 

mkdir home-assistant

pwd

docker run -d --name homeassistant --privileged --restart=unless-stopped -e TZ=Europe/Moscow -v /home/suting/home-assist:/config --network=host ghcr.io/home-assistant/raspberrypi3-homeassistant:stable
```

Веб интерфейс Home Assistant - IP adress:8123
