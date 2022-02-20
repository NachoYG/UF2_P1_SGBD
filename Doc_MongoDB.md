# PART III – INSTAL·LACIÓ SGBD MongoDB (max. 1 punts)
Com sempre, abans de començar, hem de configurar la màquina al nostre
gust.

![](media/image1.png)

![](media/image2.png) ![](media/image3.png)

![](media/image4.png)

![](media/image5.png)

![](media/image6.png)

![](media/image7.png)

## 1 – INSTALACIÓ MongoDB 5.0.

Abans de començar la instal·lació del repositori, serà eliminar
qualsevol altre que tinguem de mongodb, per fer això executem el
següent.

![](media/image8.png)

Tot seguit, dintre de la carpeta dels repositoris yum, crearem el fitxer
‘mongodb-org-5.0.repo’ amb el següent contingut.

![](media/image9.png)

Un cop afegit el repositori, realitzem un Update i instal·lem la última
versió amb la següent comanda.

![](media/image10.png)

![](media/image11.png)

Un cop instal·lat mongodb, hem de iniciar el servei.

![](media/image12.png)

Ja podem ingressar a la consola de comandes de mongo amb la següent
comanda.

![](media/image13.png)

## 2 – SECURITZACIÓ

Per tal de securitzar el nostre sistema mongo, crearé un usuari
administrador i activaré la validació amb password.

Des de la línia de comandes mongo executaré la següent sentència.

![](media/image14.png)

Per activar la autenticació, ens dirigim al fitxer ‘/etc/mongodb.conf’ i
l’editem.

![](media/image15.png)

![](media/image16.png)

Un cop guardem l’arxiu, reiniciem el servei.

![](media/image17.png)

Comprovem que ens demani la contrasenya.

![](media/image18.png)

## 3 – CONFIGURACIÓ CONNEXIÓ.

Per tal de permetre les connexions al nostre servidor mongo, el que hem
de fer es permetre la connexió a través del port 27017, per fer-ho
executem les següents comandes.

![](media/image19.png)

Un cop permès el port, hem de especificar la ip del server al arxiu de
configuració de mongodb.

![](media/image20.png)

Un cop especificada la IP, reiniciem el servei.

![](media/image21.png)

## 4 – PROVA DE CONNEXIÓ.

Per realitzar la prova de connexió faré servir el software Robo3T.

[Robo 3T | Free, open-source MongoDB GUI (formerly
Robomongo)](https://robomongo.org/)

Fem clic a ‘administrar connexions’ i després clic en crear.

![](media/image22.png)![](media/image23.png)

Seguidament, indiquem les dades del nostre server. A la finestra de
Autenticació, també indicarem les credencials del usuari creat abans.

![](media/image24.png)![](media/image25.png)

![](media/image26.png)![](media/image27.png)

