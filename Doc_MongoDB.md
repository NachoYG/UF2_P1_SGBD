# PART III – INSTAL·LACIÓ SGBD MongoDB (max. 1 punts)
Com sempre, abans de començar, hem de configurar la màquina al nostre
gust.<br>
```nmtui``` >> ```Modificar una connexió``` >> ```Acceptar``` >> ```Interficie``` >> ```Modificar``` >> ```Connectar de forma automàtica```<br>
```ip a```<br>
```yum update```
```yum install -y nano```

## 1 – INSTALACIÓ MongoDB 5.0.
Abans de començar la instal·lació del repositori, serà eliminar
qualsevol altre que tinguem de mongodb, per fer això executem el
següent.
```rm -rf /etc/yum.repos.d/mongod*```
```yum clean all```

Tot seguit, dintre de la carpeta dels repositoris yum, crearem el fitxer
```nano /etc/yum.repos.d/mongodb-org-5.0.repo``` amb el següent contingut.<br>
```[mongodb-org-5.0]```<br>
```name=MongoDB Repository```<br>
```baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/5.0/x86_64/```<br>
```gpgcheck=1```<br>
```enabled=1```<br>
```gpgkey=https://www.mongodb.org/static/pgp/server-5.0.asc```

Un cop afegit el repositori, realitzem un Update i instal·lem la última
versió amb la següent comanda.<br>
```yum update```<br>
```yum install -y mongodb-org```

Un cop instal·lat mongodb, hem de iniciar el servei.<br>
```service mongod start```<br>
```service mongod restart```<br>
```service mongod status```<br>

Ja podem ingressar a la consola de comandes de mongo amb la següent
comanda.
```mongo```


## 2 – SECURITZACIÓ

Per tal de securitzar el nostre sistema mongo, crearé un usuari
administrador i activaré la validació amb password.

Des de la <b>línia de comandes mongo</b> executaré la següent sentència.<br>
```use admin```<br>
```db.createUser({user:"Nacho", pwd:"patata"}, roles:[{role"userAdminAnyDatabase", db:"admin"}]});```<br>
```exit```

Per activar la autenticació, ens dirigim al fitxer ```nano /etc/mongodb.conf``` i
l’editem. Hem de decomentar secutity i dexar-ho així.<br>
```security:```<br>
```     authorization: "enabled"```

Un cop guardem l’arxiu, reiniciem el servei.<br>
```service mongod restart```

Comprovem que ens demani la contrasenya.<br>
```mongo -U Nacho -p --authenticationDatabase admin```

## 3 – CONFIGURACIÓ CONNEXIÓ.

Per tal de permetre les connexions al nostre servidor mongo, el que hem
de fer es permetre la connexió a través del port 27017, per fer-ho
executem les següents comandes.<br>
```iptables -A INPUT <interficie> -p tcp --destination-port 27017 -j ACCEPT```<br>
```firewall-cmd --zone=public --add-port=27017/tcp --permanent```<br>
```firewall-cmd --reload```

Un cop permès el port, hem de especificar la ip del server al arxiu de
configuració de mongodb ```nano /etc/mongod.conf```.<br>
```net:```<br>
```port:27017```<br>
```bindIP: 127.0.0.1, 192.168.31.148```<br>

Un cop especificada la IP, reiniciem el servei.<br>
```service mongod restart```

## 4 – PROVA DE CONNEXIÓ.

Per realitzar la prova de connexió faré servir el software Robo3T.

[Robo 3T | Free, open-source MongoDB GUI (formerly
Robomongo)](https://robomongo.org/)

```Administrar Connexions``` >> ```Crear``` >> ```Introduir dades servidor``` >> ```Autenticació``` >> ```Introduir dades usuari``` 





