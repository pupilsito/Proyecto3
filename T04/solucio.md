# T04: You serve as director. LDAP  

## 1️⃣ Creación of the virtual machine

De repente, update the packages:

```bash
sudo apt update && sudo apt upgrade -y
```

Edit the archivo `/etc/hosts` to define the domain:

```bash
sudo nano /etc/hosts
```

<img src="img/59.png" alt="Edició de l'arxiu /etc/hosts per definir el domini del servidor.">

Verificamos que los cambios se han aplicado correctamente en el dominio.

<img src="img/60.png" alt="Visualització dels canvis aplicats al domini després d'editar l'arxiu hosts.">

---

## 2️⃣ Configuración de red

Para permitir la comunicación con el anfitrión, configuramos una interfaz **Host-Only**:

<img src="img/61.png" alt="Configuració d'una interfície de xarxa host-only per comunicar-se amb l'amfitrió." width="750">

Editaremos el archivo `/etc/netplan/50-cloud-init.yaml` con el siguiente pedido para habilitar la interfaz:

```bash
sudo nano /etc/netplan/50-cloud-init.yaml
```

<img src="img/63.png" alt="Edició de l'arxiu /etc/netplan/50-cloud-init.yaml per habilitar la interfície host-only.">

Aplicamos los cambios y comprobamos la interfaz con `ip a`:

<img src="img/62.png" alt="Comprovació de la nova interfície de xarxa amb la comanda ip a." width="750">

---

## 3️⃣ Instalación de OpenLDAP

Instalamos el servidor LDAP y las utilidades:

```bash
sudo apt install slapd ldap-utils -y
```

Durante la instalación, el sistema nos pedirá la contraseña del administrador. Introduciremos `p@ssw0rd`, tal y como se indica en el Pliego de Condiciones Técnicas.

<img src="img/9.png" alt="Instal·lació del servei OpenLDAP mitjançant la comanda apt install slapd ldap-utils.">
<img src="img/10.png" alt="Instal·lació del servei OpenLDAP mitjançant la comanda apt install slapd ldap-utils.">
<img src="img/11.png" alt="Instal·lació del servei OpenLDAP mitjançant la comanda apt install slapd ldap-utils.">
<img src="img/12.png" alt="Instal·lació del servei OpenLDAP mitjançant la comanda apt install slapd ldap-utils.">

Una vez ejecutado el pedido anterior, comprobaremos que el servicio se está ejecutando correctamente con el siguiente pedido:

```bash
sudo systemctl status slapd
```

<img src="img/64.png" alt="Verificació de l'estat del servei slapd amb systemctl status.">

Ahora comprobaremos que el directorio se ha creado con el nombre deseado:

```bash
sudo slapcat
```

<img src="img/65.png" alt="Consulta del contingut del directori LDAP amb la comanda slapcat.">

En caso de que el nombre del directorio no sea el correcto, deberemos reconfigurar el servicio con el siguiente pedido:

```bash
sudo dpkg-reconfigure slapd
```

---

## 4️⃣ Creación de unidades organizativas (OU)

Ahora deberemos crear dos unidades organizativas (*OUs*): **users** y **groups**, mediante un archivo `.ldif`.  

Para hacerlo, en mi caso he creado dos archivos, `OU_users.ldif` `OU_groups.ldif` con el siguiente pedido:

```bash
sudo nano OU_users.ldif
```

Dentro del archivo añadiremos el siguiente contenido:

```ldif
dn: ou=users,dc=innovatech26,dc=test
ou: users
objectClass: top
objectClass: organizationalUnit

dn: ou=groups,dc=innovatech26,dc=test
ou: groups
objectClass: top
objectClass: organizationalUnit
```

<img src="img/15.png" alt="Creació del fitxer OU_users.ldif per definir les unitats organitzatives d'usuaris i grups.">
<img src="img/16.png" alt="Creació del fitxer OU_users.ldif per definir les unitats organitzatives d'usuaris i grups.">


Para crear finalmente las OUs, ejecutaremos el siguiente comando:

```bash
sudo ldapadd -D "cn=admin,dc=innovatech26,dc=test" -W -f OU_users.ldif
```

Para comprobar que se ha hecho correctamente pondremos el siguiente pedido:

```bash
ldapsearch -xLLL -b "dc=innovatech26,dc=test"
```

<img src="img/66.png" alt="Verificació de les OUs creades amb ldapsearch.">

---

## 5️⃣ Instalación del gestor LDAP (LAM)

Puesto que administrar el servidor de dominio desde la línea de mandatos puede resultar complejo, es recomendable utilizar un gestor de usuarios LDAP como **LDAP Account Manager (LAM)**.

Para instalarlo, ejecutaremos el siguiente comando (el parámetro `-y` evita que aparezcan mensajes de confirmación durante la instalación):

```bash
sudo apt install ldap-account-manager -y
```

Una vez instalado, nos conectaremos desde la máquina física a través de la interfaz **host-only**, introduciendo su dirección IP seguida de `/lam` en el navegador:

```
http://IP_DEL_SERVER/lam
```

<img src="img/19.png" alt="Accés a la interfície web del LAM des del navegador mitjançant la IP del servidor." width="750">

Una vez dentro, accederemos a **Edit server profiles** para empezar la configuración del perfil del servidor.
<img src="img/20.png" alt="Pantalla inicial de configuració del LAM, accedint a Edit server profiles." width="750">

En este apartado configuraremos las opciones generales del gestor, como el idioma, la cuenta de administrador y otros parámetros básicos.

<img src="img/67.png" alt="Configuració general del servidor LDAP al LAM, idioma i compte d'administrador." width="750">

<img src="img/68.png" alt="Configuració general del servidor LDAP al LAM, idioma i compte d'administrador." width="750">

En la segunda pestaña **Account Types**, definiremos los **DN** de los usuarios y de los grupos, incluyendo una **OU** para los usuarios y otra para los grupos.

<img src="img/70.png" alt="Definició dels DN per a usuaris i grups a la pestanya Account Types del LAM." width="750">

A continuación, aparecerá el panel de inicio de sesión, al que accederemos con el usuario administrador del dominio:
```
Usuario: admin  
Contraseña: p@ssw0rd
```
<img src="img/71.png" alt="Pantalla d'inici de sessió al panell d'administració amb admin/p@ssw0rd." width="750">

---

## 6️⃣ Creación de grupos y usuarios

### Grupos

Una vez dentro del panel de administración, debemos crear dos **grupos de seguridad** en el directorio: `tech` y `manager`.  

Para ello, iremos a **Accounts → Groups**.

Una vez dentro de este apartado, haremos clic en **New group** para crear ambos grupos.

<img src="img/72.png" alt="Creació dels grups de seguretat tech i manager dins del LAM." width="750">

Después de configurarlos, pulsamos **Save** para guardar los cambios.

Por último, ya tenemos creados los dos grupos en el directorio.

<img src="img/73.png" alt="Confirmació de la creació correcta dels grups tech i manager." width="750">

### Usuarios

Repetiremos el mismo proceso para crear un usuario para cada grupo, llamados `tech01` y `manager01`.  

Para ello, nos dirigiremos a **Accounts → Users** y haremos clic en **New user**.

En el interior del formulario deberemos introducir la información personal del usuario, como la dirección, el teléfono, la fotografía y otros datos básicos.

<img src="img/74.png" alt="Formulari d'usuari amb informació personal i Unix per tech01." width="750">

También configuraremos la información **Unix**, necesaria para que el usuario pueda iniciar sesión en el cliente.

<img src="img/75.png" alt="Formulari d'usuari amb informació personal i Unix per tech01." width="750">

En este paso, deberemos crear el **grupo primario** con el mismo nombre que el usuario.

<img src="img/77.png" alt="Formulari d'usuari amb informació personal i Unix per tech01." width="750">

Deberemos añadir el usuario al **grupo correspondiente**.  

Para ello, haremos clic en el botón **Edit groups** y, una vez dentro, moveremos el grupo `tech` (en este caso) en la sección **Selected groups** para asignarlo correctamente al usuario.

Por último, deberemos crear una **contraseña** para que el usuario de dominio pueda iniciar sesión.  

Para ello, haremos clic en el botón **Set password**, introduciremos la contraseña `1234` y marcaremos la casilla que obliga al usuario a cambiarla en el **primer inicio de sesión**.

<img src="img/78.png" alt="Assignació de l'usuari tech01 al grup tech mitjançant Edit groups." width="750">

Una vez completados estos pasos, guardaremos al nuevo usuario haciendo clic en el botón **Save**.  

A continuación, repetiremos el mismo proceso con el usuario y el grupo `manager01`, obteniendo el siguiente resultado:

<img src="img/76.png" alt="Configuració de la contrasenya de l'usuari tech01 amb l'opció de canvi obligatori.">

---

## 7️⃣ Configuración del cliente (ZorinOS)

Para comprobar que el servidor **LDAP** funciona correctamente, configuraremos un **cliente ZorinOS**.  

A este cliente le crearemos una **segunda interfaz de red** en modo **host-only**, para que pueda comunicarse con el servidor.

Una vez dentro del cliente, deberemos **configurar el nombre del equipo** para que forme parte del mismo dominio que el servidor.

Como no disponemos de un servicio **DNS**, editaremos el archivo `/etc/hosts` del cliente para que pueda resolver el nombre del servidor correctamente.

<img src="img/79.png" alt="Edició de l'arxiu /etc/hosts del client per afegir el servidor de domini.">

Ahora comprobaremos que los nombres se resuelven correctamente ejecutando los siguientes pedidos:

### Verificar el nombre de host del cliente

Para asegurarnos de que el nombre del equipo se ha cambiado correctamente:

```bash
hostname -f
```

### Comprobar la resolución del servidor de dominio

Para verificar que la resolución DNS hacia el servidor de dominio es correcta:

```bash
dig server.innovatech26.test
```

<img src="img/80.png" alt="Comprovació del nom d'amfitrió amb la comanda hostname -f i consulta DNS del domini server.innovatech26.test amb la comanda dig." width="750">

### Instalación de los módulos de autenticación LDAP

Para poder utilizar el cliente dentro del dominio, debemos instalar los **módulos necesarios** con el siguiente pedido:

```bash
sudo apt install libnss-ldap libpam-ldap ldap-utils nscd -y
```

A continuación, se iniciará el proceso de configuración de los **módulos de autenticación**.


<img src="img/81.png" alt="Configuració inicial dels mòduls d'autenticació LDAP.">
<img src="img/82.png" alt="Configuració inicial dels mòduls d'autenticació LDAP.">
<img src="img/83.png" alt="Configuració inicial dels mòduls d'autenticació LDAP.">
<img src="img/84.png" alt="Configuració inicial dels mòduls d'autenticació LDAP.">
<img src="img/85.png" alt="Configuració inicial dels mòduls d'autenticació LDAP.">
<img src="img/86.png" alt="Configuració inicial dels mòduls d'autenticació LDAP.">

Para comprobar la conectividad con el servidor, haremos una consulta **ldapsearch** desde el cliente con el siguiente pedido:

```bash
ldapsearch -x -D "cn=admin,dc=innovatech26,dc=test" -W -H ldap://server.innovatech26.test -b "dc=innovatech26,dc=test" objectClass=posixAccount uid
```

<img src="img/87.png" alt="Comprovació de la connectivitat LDAP amb la comanda ldapsearch.">

---

## 8️⃣ Integración PAM y NSS

Ahora configuraremos el archivo `nsswitch.conf` para indicar que se utilizará **LDAP** para la gestión de usuarios y grupos.

```bash
sudo nano /etc/nsswitch.conf
```

<img src="img/88.png" alt="Edició de l'arxiu /etc/nsswitch.conf per afegir suport LDAP a usuaris i grups.">

En el archivo `/etc/pam.d/common-password`, eliminaremos la línea que contenga el término `use_authok`.

<img src="img/89.png" alt="Modificació de l'arxiu /etc/pam.d/common-password per eliminar use_authok.">

En el archivo `/etc/pam.d/common-session`, añadiremos la siguiente línea para permitir la **creación automática de los perfiles de usuario**:

<img src="img/90.png" alt="Afegir línia a /etc/pam.d/common-session per crear perfils d'usuari.">

Ahora reiniciaremos el servicio con el siguiente pedido:

```bash
sudo systemctl restart nscd
```

Una vez que el servicio se haya reiniciado, comprobaremos que detecta correctamente los usuarios **LDAP** con este pedido:

```bash
getent passwd | tail
```

Podemos verificar que el sistema muestra correctamente a los usuarios provenientes del directorio **LDAP**.
<img src="img/91.png" alt="Reinici del servei nscd i comprovació dels usuaris LDAP amb getent passwd.">

## 9️⃣ Inicio de sesión gráfica

Para finalizar, editaremos el archivo `/etc/pam.d/gdm-launch-environment` para permitir el inicio de sesión gráfica de los usuarios del dominio.

<img src="img/92.png" alt="Edició de l'arxiu /etc/pam.d/gmd-launch-environment per permetre inici de sessió gràfic.">

Reiniciaremos el cliente y, en la pantalla de inicio de sesión, haremos clic en **Not listed** para introducir manualmente otro usuario.

<img src="img/47.png" alt="Pantalla d'inici de sessió del client amb l'opció Not listed per introduir tech01.">

A continuación, introduciremos el usuario `tech01` para iniciar sesión con las siguientes credenciales:

- **Usuario:** `tech01`
- **Contraseña:** `1234`

<img src="img/48.png" alt="Primera connexió de l'usuari tech01 i creació automàtica del directori personal.">

Después de introducir la contraseña, aparecerá un mensaje indicando que se está creando el **directorio personal** del usuario, en este caso `/home/tech01`.

<img src="img/49.png" alt="Primera connexió de l'usuari tech01 i creació automàtica del directori personal.">

Una vez iniciada la sesión, se puede comprobar que todo se ha creado correctamente.

<img src="img/50.png" alt="Sessió iniciada correctament amb l'usuari tech01 verificant el bon funcionament del domini.">

Si repetimos el mismo proceso con el usuario `manager01`, obtendremos el mismo resultado.

<img src="img/51.png" alt="Sessió iniciada correctament amb l'usuari manager01 verificant el bon funcionament del domini.">

[Tornar a enunciat](README.MD)
