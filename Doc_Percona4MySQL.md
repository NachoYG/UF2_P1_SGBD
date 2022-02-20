# PART I – INSTAL·LACIÓ SGBD MySQL Percona (max. 6 punts)
## 1 - INSTALACIÓ Percona Server for MySQL.

Primer de tot instal·larem el repositori de Percona.
```yum install https://repo.percona.com/yum/percona-release-latest.noarch.rpm```

Tot seguit hem de activar el repositori.
```percona-release setup ps80```

Ja podem procedir a instal·lar el paquet.
```yum install percona-server-server```

Ara comprovarem l’estat del servei ‘mysql’ i l’iniciem si cal.
```service mysqld status```
```service mysqld start```
```service mysqld restart```

Per tal de que el nostre server permeti les connexions mysql, hem
d’habilitar el port 3306 al Firewall.<br>
```iptables -A INPUT -i <interficie> -p tcp --destination-port 3306 -j ACCEPT```<br>
```firewall-cmd --zone=public --add-port=3306/tcp --permanent```

Tot seguit, ens dirigim a ‘/etc/my.cnf’ i afegim la seguent línia i
reiniciem el servei mysql. La IP indicada es la IP del meu server.<br>
``` nano /etc/myconf``` --> Afegir línia: ```bind-address=<IP del servidor>```


## 2 – SECURITZACIÓ
Per poder realitzar la securització primer de tot hem de editar la
política de seguretat de MySQL, per fer fer-ho ens dirigim al següent
fitxer i afegim les següent línies al final.
```nano /etc/my.cnf```<br>
``` validate_password.policy=LOW ```<br>
``` validate_password.length=6 ```<br>
Necessari:
``` service mysqld restart ```<br>

Tot seguit, hem de ‘descobrir’ quina contrasenya te l’usuari root, per
fer-ho consultarem el seguent log. <br>
``` grep "temporary password" /var/log/mysqld.log ```


Ara podem realitzar la securització demanda root – patata.
``` mysql_secure_installation ```

## 3 – USUARI ASIX

El primer que hem de fer es crear el nostre usuari ASIX al nostre
CentOS, abans de crear-lo hem de modificar la política de password del
CentOS, per tal de poder-li donar al usuari el password demanat. ASIX –
patata.

Per fer-ho, hem d’executar la seguent comanda.
```authconfig --passminlen=6 --update ```


Hem de editar aquestes línies de la seguent manera. ```nano /etc/pam.d/system-auth```.<br>
```#password    requisite     pam_pwquality.so```<br>
```#password    sufficient    pam_unix.so sha512```<br>
```#password    requiered     pam_deny.so```<br>

Ja podem procedir a crear l’usuari amb el password desitjat.<br>
```adduser asix```<br>
```passwd asix```

Per crear l’usuari MySQL, hem de realitzar les següents sentències
dintre del terminal MySQL.<br>
```CREATE USER 'asix'@'%' IDENTIFIED BT 'patata';```<br>
```GRANT ALL PRIVILEGES ON *.* TO 'asix'@'%';```<br>
  - Si encara s’indica que la contrasenya no compleix els requeriments,
    podem indicar la següent sentència.<br>
```SET GLOBAL validate\_password.policy=LOW;```<br>
```SET GLOBAL validate\_password.length=6;```

Per fer que l’usuari es pugui connecti sense que si li demani el
password hem de, primer de tot, editar el fitxer ```nano /etc/my.conf``` afegint
les següents línies al final.<br>
```[client]```<br>
```password=patata ```



Tot seguit, hem de canviar-li els permisos al fitxer my.cnf per tal de
fer el password segur.<br>
```chmod 600 /etc/my.cnf```

Provem a obrir MySQL amb l’usuari asix sense indicar cap password.<br>
```mysql -u asix```


## 4 – PROVA DE CONNEXIÓ.

Fent servir el MySQL Workbench8.0, em connectaré al meu servidor MySQL.

[MySQL :: Download MySQL
Workbench](https://dev.mysql.com/downloads/workbench/)

Primer de tot, creo la meva nova connexió al meu server.
```MySQL Connections >> ADD >> <Set Server Info> >> Test Connection ```

Si no hi han errors, ens connectem.



