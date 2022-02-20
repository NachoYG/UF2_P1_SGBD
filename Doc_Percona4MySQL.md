# 1 - INSTALACIÓ Percona Server for MySQL.

Primer de tot instal·larem el repositori de Percona.

‘yum install
https://repo.percona.com/yum/percona-release-latest.noarch.rpm’

Tot seguit hem de activar el repositori.

![](media/image1.png)

Ja podem procedir a instal·lar el paquet.

![](media/image2.png)

Ara comprovarem l’estat del servei ‘mysql’ i l’iniciem si cal.

![](media/image3.png)

Per tal de que el nostre server permeti les connexions mysql, hem
d’habilitar el port 3306 al Firewall.

![](media/image4.png)

![](media/image5.png)

Tot seguit, ens dirigim a ‘/etc/my.cnf’ i afegim la seguent línia i
reiniciem el servei mysql. La IP indicada es la IP del meu server.

![](media/image6.png)

![](media/image7.png)

![](media/image8.png)

## 2 – SECURITZACIÓ

Per poder realitzar la securització primer de tot hem de editar la
política de seguretat de MySQL, per fer fer-ho ens dirigim al següent
fitxer i afegim les següent línies al final.

![](media/image9.png)

![](media/image10.png)

![](media/image11.png)

Tot seguit, hem de ‘descobrir’ quina contrasenya te l’usuari root, per
fer-ho consultarem el seguent log

![](media/image12.png)

Ara podem realitzar la securització demanda root – patata.

![](media/image13.png)

![](media/image14.png) Hem de introduir la contrasenya temporal.

![](media/image15.png) Introduïm la nova contrasenya.

## 3 – USUARI ASIX

El primer que hem de fer es crear el nostre usuari ASIX al nostre
CentOS, abans de crear-lo hem de modificar la política de password del
CentOS, per tal de poder-li donar al usuari el password demanat. ASIX –
patata.

Per fer-ho, hem d’executar la seguent comanda.

![](media/image16.png)

Ara ens dirigim al seguent fitxer i comentem la línia que apareix, també
esborrarem . ‘/etc/pam.d/system-auth’

![](media/image17.png)

Ja podem procedir a crear l’usuari.

![](media/image18.png)

Per crear l’usuari MySQL, hem de realitzar les següents sentències
dintre del terminal MySQL.

![](media/image19.png)

  - Si encara s’indica que la contrasenya no compleix els requeriments,
    podem indicar la següent sentència.

‘SET GLOBAL validate\_password.policy=LOW;’

‘SET GLOBAL validate\_password.length=6;’

Per fer que l’usuari es pugui connecti sense que si li demani el
password hem de, primer de tot, editar el fitxer ‘/etc/my.cnf’ afegint
les següents línies al final.

![](media/image20.png)

Tot seguit, hem de canviar-li els permisos al fitxer my.cnf per tal de
fer el password segur.

![](media/image21.png)

Provem a obrir MySQL amb l’usuari asix sense indicar cap password.

![](media/image22.png)

## 4 – PROVA DE CONNEXIÓ.

Fent servir el MySQL Workbench8.0, em connectaré al meu servidor MySQL.

[MySQL :: Download MySQL
Workbench](https://dev.mysql.com/downloads/workbench/)

Primer de tot, creo la meva nova connexió al meu server.

![](media/image23.png)

![](media/image24.png)

Un cop introduïdes les dades de la connexió, fem el test de connexió.

![](media/image25.png)

![](media/image26.png)![](media/image27.png)

Realitzem la connexió.

![](media/image28.png)

