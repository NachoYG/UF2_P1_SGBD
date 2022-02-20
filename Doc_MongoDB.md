# PART III – INSTAL·LACIÓ SGBD MongoDB (max. 1 punts)
Com sempre, abans de començar, hem de configurar la màquina al nostre
gust.<br>
```nmtui```



## 1 – INSTALACIÓ MongoDB 5.0.

Abans de començar la instal·lació del repositori, serà eliminar
qualsevol altre que tinguem de mongodb, per fer això executem el
següent.



Tot seguit, dintre de la carpeta dels repositoris yum, crearem el fitxer
‘mongodb-org-5.0.repo’ amb el següent contingut.


Un cop afegit el repositori, realitzem un Update i instal·lem la última
versió amb la següent comanda.





Un cop instal·lat mongodb, hem de iniciar el servei.



Ja podem ingressar a la consola de comandes de mongo amb la següent
comanda.



## 2 – SECURITZACIÓ

Per tal de securitzar el nostre sistema mongo, crearé un usuari
administrador i activaré la validació amb password.

Des de la línia de comandes mongo executaré la següent sentència.



Per activar la autenticació, ens dirigim al fitxer ‘/etc/mongodb.conf’ i
l’editem.



Un cop guardem l’arxiu, reiniciem el servei.


Comprovem que ens demani la contrasenya.


## 3 – CONFIGURACIÓ CONNEXIÓ.

Per tal de permetre les connexions al nostre servidor mongo, el que hem
de fer es permetre la connexió a través del port 27017, per fer-ho
executem les següents comandes.



Un cop permès el port, hem de especificar la ip del server al arxiu de
configuració de mongodb.



Un cop especificada la IP, reiniciem el servei.



## 4 – PROVA DE CONNEXIÓ.

Per realitzar la prova de connexió faré servir el software Robo3T.

[Robo 3T | Free, open-source MongoDB GUI (formerly
Robomongo)](https://robomongo.org/)

Fem clic a ‘administrar connexions’ i després clic en crear.


Seguidament, indiquem les dades del nostre server. A la finestra de
Autenticació, també indicarem les credencials del usuari creat abans.




