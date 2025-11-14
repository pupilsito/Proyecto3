![](img/00.png)

Jhon Justiniano-Nil Lozano-Anthony Milla-Hugo Muiños / SMX-B / Seguretat Informàtica

---

## Index:

- 1. Introducció:
- 2. Part Linux: LVM amb Zorin OS
- 2.1. Configuració Inicial: Crear un grup de volums (VG) i un volum lògic (LV) utilitzant inicialment un mínim de dos discs durs (simulats) de 10 GB de capacitat. Aquest volum haurà estar formatat i muntat automàticament al sistema mitjançant l’edició de l’arxiu /etc/fstab.
- 2.2. Alta Disponibilitat: Implementar la configuració d’un mirall (lvm_mirror) que protegeixi la informació davant la fallada d'un disc.
- 2.3. Instantànies (snapshots):  Crear i afegir dos discos de 10 GB al grup de volums. Crear un volum (lvm_dades) amb el primer disc afegit, formatar-lo i muntar-lo. A continuació afegir arxius al volum (poden ser imatges d’Internet). Usar el segon disc afegit per crear un snapshot (lv_snapshot) i documentar com es pot restaurar aquest snapshot, si per exemple, la informació del volum original es danyés.
- 2.4. Escalabilitat: Demostrar el procés d'ampliació. Usar l’espai que quedi lliure dins el grup de volums per ampliar el volum lv_dades.
- 3. Part Windows: Espais d'Emmagatzematge (Storage Spaces)
- 3.1.Configuració inicial: Creació d'un Storage Pool: Crear un pool d'emmagatzematge inicialment amb tres discos de 10 GB (simulats).
- 3.2. Estudi de Configuracions: Demostrar i documentar la creació d'un Espai d'Emmagatzematge utilitzant:
- 3.3. Demostració de la Gestió: Mostrar com es visualitza l'estat dels discos i del pool des de la consola de gestió de Windows, simulant la facilitat de manteniment.


---
## 1. Introducció:
Un cop superada la fase de formació, ja esteu preparats per afrontar el repte dels nostres clients. Com ja es va explicar, tenim un nou i important client, el bufet d’advocats Garriga i associats un dels més prestigiosos de la ciutat, ha requerit els serveis de la nostra consultora. Gestiona una gran quantitat d'informació legal sensible, per la qual cosa la integritat, la disponibilitat (alta redundància) i la facilitat de gestió del seu emmagatzematge són d'importància crítica.

La direcció de "Garriga i Associats" ha expressat la necessitat urgent de renovar els seus sistemes de servidors per garantir que la informació estigui protegida contra fallades de disc i que l'espai pugui ser ampliat sense interrupcions.

Com a tècnics d'Everpia, teniu l'encàrrec de dissenyar i documentar les solucions d'emmagatzematge que compliran aquests requisits tant en entorns Linux com Windows. Aquest disseny permetrà presentar al client una proposta de solució.

L'objectiu principal és dissenyar i documentar dues solucions d'emmagatzematge (una per servidors Linux i una per servidors Windows) que compleixin amb els principis d'alta disponibilitat, redundància i escalabilitat per al client. Com ha de ser una prova de concepte, no treballareu amb servidors, sinó que, per facilitat, usareu màquines virtuals de sistemes operatius clients per documentar els procediments.

---
## 2. Part Linux: LVM amb Zorin OS
S'ha d'utilitzar la distribució Zorin OS (o una alternativa Linux compatible) per demostrar la utilitat del Logical Volume Manager (LVM).
Requisits de la Implementació i Demostració:

2.1. Configuració Inicial: Crear un grup de volums (VG) i un volum lògic (LV) utilitzant inicialment un mínim de dos discs durs (simulats) de 10 GB de capacitat. Aquest volum haurà estar formatat i muntat automàticament al sistema mitjançant l’edició de l’arxiu /etc/fstab.


---
Configuració Inicial: Crear un grup de volums (VG) i un volum lògic (LV) utilitzant inicialment un mínim de dos discs durs (simulats) de 10 GB de capacitat. Aquest volum haurà estar formatat i muntat automàticament al sistema mitjançant l’edició de l’arxiu /etc/fstab.

1- Creamos la máquina donde le asignaremos el nombre correspondiente

![](img/01.png)

2- Asignamos la cantidad de recursos que le daremos a la máquina

![](img/01.png)

3- Comenzamos a crear los discos donde se observa que se le asigna 10GB

![](img/02.png)

4- En esta imagen podemos observar cómo se han creado los discos correspondientes

![](img/03.png)

5- Montamos el primer disco

![](img/04.png)

6- Montamos el segundo disco

![](img/05.png)

5- Montamos el tercer disco

![](img/06.png)

6- En esta imagen podemos observar el estado de los discos creados

![](img/07.png)

7- Creamos un grupo de volúmenes

![](img/08.png)

8- Los VG son como particiones así que para que nos sean útiles tendremos que formatearlos con un sistema de archivos

![](img/09.png)

9- Para poder utilizar el VG tendremos que utilizar la comanda mount para montar el volumen

![](img/10.png)

10- Seguidamente iremos a este fichero para modificarlo de manera que el LV este montado de forma permanente

![](img/11.png)

11- Esta comanda sirve para hacer comprobaciones

![](img/12.png)

2.2. Alta Disponibilitat: Implementar la configuració d’un mirall (lvm_mirror) que protegeixi la informació davant la fallada d'un disc.

Alta Disponibilitat: Implementar la configuració d’un mirall (lvm_mirror) que protegeixi la informació davant la fallada d'un disc.

1- Aquí hacemos pvs para ver los discos montados

![](img/13.png)

2- Creamos el VG mirror con los 2 discos

![](img/14.png)

3- Creamos un LV de 90Mb del mirror

![](img/15.png)

4- Aquí comprobamos que se ha hecho correctamente

![](img/16.png)

2.3. Instantànies (snapshots):  Crear i afegir dos discos de 10 GB al grup de volums. Crear un volum (lvm_dades) amb el primer disc afegit, formatar-lo i muntar-lo. A continuació afegir arxius al volum (poden ser imatges d’Internet). Usar el segon disc afegit per crear un snapshot (lv_snapshot) i documentar com es pot restaurar aquest snapshot, si per exemple, la informació del volum original es danyés.

Instantànies (snapshots):  Crear i afegir dos discos de 10 GB al grup de volums. Crear un volum (lvm_dades) amb el primer disc afegit, formatar-lo i muntar-lo. A continuació afegir arxius al n snapshot (lv_snapshot) i documentar com es pot restaurar aquest snapshot, si per exemple, la informació del volum (poden ser imatges d’Internet). Usar el segon disc afegit per crear uvolum original es danyés.

1- Crearemos un volumen denominado lmv_dades

![](img/17.png)

2- Montamos la copia para ver el contenido

![](img/18.png)

3-Montamos el volumen creado

![](img/19.png)

4- Modificamos el archivo de forma que sea permanente el montaje del archivo

![](img/20.png)

5- Creamos un archivo donde lo pondremos en la carpeta de lvm_dades

![](img/21.png)

6- En esta imagen crearemos otro LV denominado lv_snapshot, donde se le crea una carpeta

![](img/22.png)

7-  Seguidamente se prosigue a montar el LV

![](img/23.png)

8- En esta imagen lo montamos de forma permanente

![](img/24.png)

9- Movemos el archivo a la carpeta

![](img/25.png)

10- Seguidamente creamos el siguiente LV

![](img/26.png)

11- Aquí comprobamos que se han creado correctamente

![](img/27.png)

12- Aquí en la imagen se montamos los discos

![](img/28.png)

2.4. Escalabilitat: Demostrar el procés d'ampliació. Usar l’espai que quedi lliure dins el grup de volums per ampliar el volum lv_dades.

Escalabilitat: Demostrar el procés d'ampliació. Usar l’espai que quedi lliure dins el grup de volums per ampliar el volum lv_dades.

1- Hacemos el siguiente comando que nos permite extender el volumen del LV

![](img/29.png)

## 3. Part Windows: Espais d'Emmagatzematge (Storage Spaces)

S'ha d'utilitzar Windows 11 (per demostrar les configuracions possibles mitjançant els Espais d'Emmagatzematge (Storage Spaces).

Requisits de la Implementació i Demostració:

3.1.Configuració inicial: Creació d'un Storage Pool: Crear un pool d'emmagatzematge inicialment amb tres discos de 10 GB (simulats).

Amb la màquina apagada, anem a paràmetres, emmagatzematge i creem 3 discos de 10 GB (simulats) i guardem.

![](img/30.png)

Ara dins de la màquina anem administració d’equips, inicialitzem els discos, utilitzem l’estil de partició MBR.

![](img/31.png)

3.2. Estudi de Configuracions: Demostrar i documentar la creació d'un Espai d'Emmagatzematge utilitzant:

Resiliència de Mirall (Mirroring): Usar dos dels discos. Comprovar que ofereix alta disponibilitat.

Anem a espais d'emmagatzematge i creem.

![](img/32.png)

Seguidament creem grup, usant 2 dels discos.

![](img/33.png)

Posem tipus de resistència en reflexe doble i de capacitat màxima 30,70 GB.

![](img/34.png)

I ja estaria creat.

![](img/35.png)

![](img/36.png)

I posem algun arxiu (carpeta amb un arxiu a dins, un document de text per exemple) dins de l’espai per fer la prova de disponibilitat.

![](img/37.png)

Comprovació que ofereix alta disponibilitat. Desconnectem el disc 2.

![](img/38.png)

![](img/39.png)

Surt una alerta que s’ha perdut el mirall.

![](img/40.png)

Surt una alerta que s’ha perdut el mirall, però podem continuar llegint la informació que havíem guardat.

![](img/41.png)

![](img/42.png)

Afegim el tercer disc a l'espai de reflex doble i entrem, no surt la alerta i podem veure el nostre disc de reflex doble amb normalitat i sense problemes. 

![](img/43.png)

![](img/44.png)

![](img/45.png)

Resiliència de Paritat (Parity): Explicant la seva eficiència d'espai en comparació amb el mirall. Cal usar els tres discos.

Creem grup, usant els 3 discos.

![](img/46.png)

Posem tipus de resistència en paritat i de capacitat màxima 30,70 GB.

![](img/47.png)

I ja estaria creat.

![](img/48.png)

![](img/49.png)

Eficiència d'espai: Paritat vs Mirall

Mirall (2 discos): Guarda una còpia exacta de les dades en cada disc. Si tens 2 discos de 10 GB, només pots usar 10 GB per dades. L'altre 10 GB és per la còpia.  50% d'eficiència d'espai.

Paritat (3 discos): Distribueix les dades i la informació de recuperació entre els discos. Amb 3 discos de 10 GB, pots usar 20 GB per dades i 10 GB per paritat.  ≈66% d'eficiència d'espai.

Conclusió: La paritat és més eficient en espai que el mirall, però pot ser una mica més lenta en rendiment.

Resiliència de mirall triple. Afegir tant discos de 10 GB com siguin necessaris.

Creem grup, usant tant discos de 10 GB com siguin necessaris (5 discos). 
Amb la màquina apagada, anem a paràmetres, emmagatzematge i hem de tenir/crear 5 discos de 10 GB (simulats) i guardem. Dins de la màquina anem administració d’equips, inicialitzem els discos, utilitzem l’estil de partició MBR.

![](img/50.png)

Anem a espais d'emmagatzematge i creem.

![](img/51.png)

Seguidament creem grup, usant els 5 discos.

![](img/52.png)

Posem tipus de resistència en reflexe triple i de capacitat màxima 30,70 GB.

![](img/53.png)

I ja estaria creat.

![](img/54.png)

![](img/55.png)

3.3. Demostració de la Gestió: Mostrar com es visualitza l'estat dels discos i del pool des de la consola de gestió de Windows, simulant la facilitat de manteniment.

Mostrem com es visualitza l'estat dels discos i del pool des de la consola de gestió de Windows, per simular la facilitat de manteniment. Ho hem fet amb el mirall triple.

![](img/56.png)
