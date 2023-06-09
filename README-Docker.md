[Link utilizado de base](https://www.aprendendolinux.com/implantando-o-glpi-em-2-minutos-com-o-docker/)

```sh
docker run -d --name='mariadb' \
     --hostname='mariadb' \
     -e MARIADB_ROOT_PASSWORD='senhaderootmariadb' \
     -e MARIADB_DATABASE='glpi' \
     -e MARIADB_USER='glpi' \
     -e MARIADB_PASSWORD='senhadousuarioglpi' \
     -v /home/glpi/mariadb:/var/lib/mysql \
--restart=always mariadb:latest
```

```sh
docker run -d --name='glpi' \
     --hostname='glpi' \
     --link='mariadb:mariadb' \
     -e TIMEZONE='America/Sao_Paulo' \
     -e VERSION='10.0.2' \
     -v /home/glpi/php:/var/www/html \
     -p 80:80 \
--restart=always aprendendolinux/glpi:latest
```
