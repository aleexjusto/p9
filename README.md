# P9 DUÁS PÁXINAS WEBS

Nesta práctica configurei duás páxinas webs, fabulasmaravillosas e fabulas oscuras, a unha mesma dirección ip do meu DNS, onde os arquivos son os seguintes:

# Docker-compose.yml
Neste arquivo temos dous servicios, a das páxinas webs e o do servidor DNS, e ademáis definimos a red.

## web

Nesta parte temos definido a imaxe, neste caso php, o nome do servidor, o porto que empregaremos, que sera o 80, os volumes que máis adiante configuramos e a red, que a chamei apared.
```
web:
    image: php:7.4-apache
    container_name: apaserver
    ports:
      - "80:80"
    volumes:
      - ./www:/var/www
      - ./confApache:/etc/apache2
    networks:
      apared:
        ipv4_address: 172.39.4.2
```

## dns

Igual que nas anteriores prácticas, configuramos a imaxe, os volumes que configuraremos máis adiante, o porto que empregaremos e a red, que ten que ser a mesma pero cunha ip distinta.

```
dns:
    container_name: dnsserver
    image: ubuntu/bind9
    ports:
      - "51:53"
    volumes:
      - ./confDNS/conf:/etc/bind
      - ./confDNS/zonas:/var/lib/bind
    networks:
      apared:
        ipv4_address: 172.39.4.3
```
## red
