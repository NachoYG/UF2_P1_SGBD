Abans de començar el que hem de fer es instal·lar el nostre CentOS 7 a
una màquina virtual.

![](media/image1.png)

Un cop hàgim instal·lat CentOS, el que hem de fer es activar la
interfície de xarxa, ja que per defecte ve desactivada.

![](media/image2.png)

![](media/image3.png)

![](media/image4.png)

Es pot observar que ja en tenim IP.

![](media/image5.png)

# 1 – INSTALACIÓ MySQL 8.0.

Un cop configurada la nostra màquina podem precedir amb la instal·lació.
El primer que farem serà afegir el repositori necessari per instal·lar
el mysql80.

![](media/image6.png)

Per poder instal·lar la versió 8.0, hem de desactivar la possibilitat de
que s’instal·li una altra versió. Per fer això, desactivem els
repositoris de mysql-community.

![](media/image7.png)

Tot seguit procedim a instal·lar el nostre mysql80. Per fer-ho, el que
haurem de realitzar serà una actualització del repositori de GPG Keys i
posterior ment instal·lar el servei.

![](media/image8.png)

![](media/image9.png)

Un cop finalitzi la instal·lació iniciarem el servei i comprovarem que
sigui funcionant.

![](media/image10.png)

Dintre del fitxer ‘/etc/my.cnf’, definirem quina es la ip del nostre
servidor amb la següent línia. Després reiniciem el servei.

![](media/image11.png)

![](media/image12.png)

Tot seguit, permetrem la connexió de la resta de màquines al nostre port
3306 a través del nostre Firewall.

![](media/image13.png)

![](media/image14.png)

# 2 – SECURITZACIÓ

Com al exercici anterior, hem de modificar la Política de Contrasenyes
per tal de ficar-li al nostre usuari root el password ‘patata’. Ens
dirigim al fitxer ‘/etc/my.cnf’ i l’editem afegint les següents línies.
Després reiniciem el servei.

![](media/image15.png)

![](media/image16.png)

Ara hem de saber quin es el password temporal de usuari root, per
saber-ho executem la següent comanda.

![](media/image17.png)

Ja podem executar la instal·lació segura de mysql i canviar-li el
password al nostre root.

![](media/image18.png)

# 3 – USUARI ASIX

En aquest cas, per no repetir-nos, crearem l’usuari ‘asix2’. Com abans,
el primer que hem de fer es canviar la política de contrasenyes de
CentOS per tal de que ens deixi crear l’usuari en local amb el password
requerit (patata).

Executem la següent comanda.

![](media/image19.png)

Tot seguit ens dirigim al fitxer ‘/etc/pam.d/system-auth’ i l’editem.
Hem de posicionar-nos a les línies que indiquen ‘password’ i canviar la
primera línia.

![](media/image20.png)

![](media/image21.png)

Procedim a crear l’usuari.

![](media/image22.png)

\*\* Com es pot observar, el primer cop que s’introdueix el password
indica que el password no compleix el requisits, al segon cop accepta el
password. Captura de inici de sessió.

![](media/image23.png)

Ara crearé l’usuari al mysql, per fer això executem les següents
sentències des de el terminal de mysql.

![](media/image24.png)

![](media/image25.png)

Comprovem que puguem accedir.

![](media/image26.png)

En aquest cas, no farem que l’usuari es connecti automàticament amb el
password per defecte ‘patata’.

# 4 – PROVA DE CONNEXIÓ.

Com a l’exercici anterior, amb el Software MySQL Workbench8.0, provarem
de connectar-nos de manera remota al nostre servidor.

[MySQL :: Download MySQL
Workbench](https://dev.mysql.com/downloads/workbench/)

Afegim la connexió.

![](media/image27.png)![](media/image28.png)

![](media/image29.png)
