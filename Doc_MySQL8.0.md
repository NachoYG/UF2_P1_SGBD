# PART II – INSTAL·LACIÓ SGBD MySQL 8.0 (max. 2 punts)
Abans de començar el que hem de fer es instal·lar el nostre CentOS 7 a
una màquina virtual.

Un cop hàgim instal·lat CentOS, el que hem de fer es activar la
interfície de xarxa, ja que per defecte ve desactivada.<br>
```nmtui``` >> ```Modificar una connexió``` >> ```Acceptar``` >> ```Interficie``` >> ```Modificar``` >> ```Connectar de forma automàtica```

Es pot observar que ja en tenim IP. ```ip a ```

## 1 – INSTALACIÓ MySQL 8.0.

Un cop configurada la nostra màquina podem precedir amb la instal·lació.
El primer que farem serà afegir el repositori necessari per instal·lar
el mysql80.<br>
```rpm -Uvh https://repo.mysql.com/mysql80-community-release-el7-3.noarch.rpm```

Per poder instal·lar la versió 8.0, hem de desactivar la possibilitat de
que s’instal·li una altra versió. Per fer això, desactivem els
repositoris de mysql-community.<br>
```sed -i 's/enabled=1/enabled=0' /etc/yum.repos.d/mysql-community.repo```

Tot seguit procedim a instal·lar el nostre mysql80. Per fer-ho, el que
haurem de realitzar serà una actualització del repositori de GPG Keys i
posterior ment instal·lar el servei.<br>
```rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022```
```yum --enablerepo=mysql80-community install mysql-community-server```

Un cop finalitzi la instal·lació iniciarem el servei i comprovarem que
sigui funcionant.<br>
```service mysqld status``` ```service mysqld start``` ```service mysqld restart```


Dintre del fitxer ```nano /etc/my.cnf```, definirem quina es la ip del nostre
servidor amb la següent línia. Després reiniciem el servei.<br>
```bind-address=<IP del servidor>```<br>
Requerit: ```service mysqld restart```

Tot seguit, permetrem la connexió de la resta de màquines al nostre port
3306 a través del nostre Firewall.<br>
```iptables -A INPUT -i <interficie> -p tcp --destination-port 3306 -j ACCEPT```<br>
```firewall-cmd --zone=public --add-port=3306/tcp --permanent```<br>
```firewall-cmd --reload```


## 2 – SECURITZACIÓ

Com al exercici anterior, hem de modificar la Política de Contrasenyes
per tal de ficar-li al nostre usuari root el password ‘patata’. Ens
dirigim al fitxer ```nano /etc/my.cnf``` i l’editem afegint les següents línies.
Després reiniciem el servei.<br>
```validate_password.policy=LOW```<br>
```validate_password.length=6```<br>
```service mysqld restart```<br>

Ara hem de saber quin es el password temporal de usuari root, per
saber-ho executem la següent comanda.<br>
```grep 'temporary password' /var/log/mysqld.log```

Ja podem executar la instal·lació segura de mysql i canviar-li el
password al nostre root.
```mysql_secure_installation```


## 3 – USUARI ASIX

En aquest cas, per no repetir-nos, crearem l’usuari ‘asix2’. Com abans,
el primer que hem de fer es canviar la política de contrasenyes de
CentOS per tal de que ens deixi crear l’usuari en local amb el password
requerit (patata).

Executem la següent comanda.<br>
```authconfig --passminlen=6 --update```

Tot seguit ens dirigim al fitxer ```nano /etc/pam.d/system-auth``` i l’editem.
Hem de posicionar-nos a les línies que indiquen ‘password’ i comentar la
primera línia. Despés deixar la segona no més amb sha512.<br>
```#password     requsite     pam_pwquality.so```<br>
```password      sufficient   pam_unix.so sha512```<br>
```password      required     pam_deny.so```<br>

Procedim a crear l’usuari.<br>
```adduser asix2```<br>
```passwd asix2```

Ara crearé l’usuari al mysql, per fer això executem les següents
sentències des de el <b>terminal de mysql</b>.<br>
```CREATE USER 'asix2'@'%' IDENTIFIED BY 'patata';```<br>
```GRANT ALL PRIVILEGES ON *.* TO 'asix2'@'%';```
```exit```

Comprovem que puguem accedir.
```mysql -u asix2 -ppatata```

<b>En aquest cas, no farem que l’usuari es connecti automàticament amb el
password per defecte ‘patata’.</b>

## 4 – PROVA DE CONNEXIÓ.

Com a l’exercici anterior, amb el Software MySQL Workbench8.0, provarem
de connectar-nos de manera remota al nostre servidor.

[MySQL :: Download MySQL
Workbench](https://dev.mysql.com/downloads/workbench/)

Primer de tot, creo la meva nova connexió al meu server.
```MySQL Connections >> ADD >> <Set Server Info> >> Test Connection ```

Si no hi han errors, ens connectem.


