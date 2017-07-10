# Instalar Laravel Homestead en Windows

Laravel Homestead es el box de vagrant oficial para Laravel, en sí es una herramienta de desarrollo hecha por Taylor Otwell, el creador de Laravel, la cual nos brinda un ambiente lo más cercano posible a un entorno de producción solo que en nuestra propia máquina local, esto con la finalidad de que al estar desarrollando nuestras aplicaciones podamos estar probándolo constantemente con la máquina virtual (que será como nuestro servidor) y así poder estar seguros de que cuando vayamos a hacer el deploy a producción no tengamos ningún problema.

Laravel Homestead, a grandes rasgos, es una máquina virtual con un Ubuntu Server y tiene instaladas varias herramientas out of the box, es decir, ya están pre-cargadas para no preocuparnos por instalar software que probablemente vayamos a utilizar, tales como lo son:

* Ubuntu 14.04
* PHP 5.6
* HHVM
* Nginx
* MySQL
* Postgres
* Node (Con Bower, Grunt, y Gulp)
* Redis
* Memcached
* Beanstalkd
* Laravel Envoy
* Blackfire Profiler

## Instalando los requerimientos básicos

Dado que estaremos haciendo la instalación para Windows, debemos de habilitar la virtualización por hardware (VT-x), esto varía mucho debido a que esto se debe de habilitar en el BIOS, si no sabes cómo habilitar la virtualización en tu equipo primero deberás ver en la documentación del fabricante de tu motherboard (en su página de internet, foros, etc.) la manera de hacerlo ya que esto podrá ocasionar que no puedas instalar Laravel Homestead en tu computadora.


Lo siguiente que se debe tomar en cuenta y que yo en lo personal recomiendo mucho es no utilizar la consola de Windows, esto debido a que no tiene soporte nativo para la generación de llaves SSH las cuales vamos a necesitar para conectarnos a nuestro servidor virtual, en su lugar recomiendo (y en lo personal utilizo) [la consola de Git](https://git-scm.com/download).

También debemos tener instalado composer en nuestro ordenador, si no lo has hecho aquí te explicamos como instalar Composer y Laravel en Windows


También debemos tener instalado composer en nuestro ordenador, si no lo has hecho aquí te explican como [instalar Composer y Laravel en Windows](https://styde.net/instalacion-de-composer-y-laravel-en-windows/)

Después de tener instalado composer en nuestro equipo necesitamos instalar **[VirtualBox](https://www.virtualbox.org/)** o **[vmware](https://www.vmware.com/)** para poder correr nuestra máquina virtual, para este ejercicio nosotros vamos a usar VirtualBox.

Lo siguiente que debemos de hacer es tener [Vagrant](https://www.vagrantup.com/) instalado en nuestro equipo, esto debido a que **Homestead** es una **box** de **vagrant**, es decir, todo lo que necesitamos para tener nuestro entorno de desarrollo listo para empezar a trabajar con él. Una vez instalado vagrant debemos agregar el **box**, lo cual se hace desde la consola con el siguiente comando

```bash
vagrant box add laravel/homestead
```

y cuando nos pregunte que provider vamos a utilizar seleccionamos virtualbox dado que nuestra máquina virtual estará corriendo sobre él.

Por último debemos de tener un cliente SSH para poder conectarnos a nuestra máquina virtual. Dado que Windows no tiene soporte nativo para conexiones de este tipo nosotros utilizaremos PuTTY un cliente SSH muy ligero que podemos [descargar desde su página web](http://the.earth.li/~sgtatham/putty/latest/x86/putty.exe).

##Instalar Homestead

Una vez que tengamos todos los requerimientos podemos empezar con la instalación de Laravel Homestead, desde nuestra consola de git tecleamos el comando

```bash
composer global require "laravel/homestead=~2.0"
```

con esto descargaremos todos los archivos necesarios para poder hacer uso del comando homestead, sin embargo antes de eso tenemos que agregar la ruta a nuestro PATH la cual debe estar apuntando hacia donde tenemos nuestro ejecutable de homestead.

Agregar una ruta al PATH es muy sencillo en Windows, tan solo tenemos que dar clic derecho sobre Equipo e ir a las propiedades, luego hacer clic en configuración avanzada del sistema como se muestra en esta pantalla

![](https://styde.net/wp-content/uploads/2015/05/homestead-windows-1.png)

Nota, también podemos llegar a esa ventana tecleando al mismo tiempo la tecla de Windows + Pausa

Después veremos otra ventana en la cuál debemos dar clic sobre el botón que diga variables de entorno, esto nos abrirá otra ventana en la cuál debemos buscar en las variables del sistema la opción Path y modificarla

![](https://styde.net/wp-content/uploads/2015/05/homestead-windows-2.png)

Propiedades del sistema

![](https://styde.net/wp-content/uploads/2015/05/homestead-windows-3.png)


Editar variables del sistema

Una vez que demos clic en editar se abrirá una ventana nueva donde debemos indicar la ruta de nuestro composer, la cuál por defecto debe ser la siguiente:

C:\Users\Nombre_del_usuario\AppData\Roaming\Composer\vendor\bin;

Esto hará que una vez que instalemos Homestead podamos hacer uso de ese comando de manera global en nuestro sistema, para verificarlo vamos a abrir la consola de git (Git Bash) y tecleamos.

```bash
homestead -V
```

En caso que no configuremos homestead globalmente entramos a la carpeta Homestead que queda almacena en la carpeta del usuario de windows y ejecutamos

```bash
vagrant -V
```


con esto podemos verificar que nuestra ruta se haya configurado correctamente y podremos ver la versión de Homestead que se ha instalado en nuestro sistema, deberías ver algo como lo siguiente:

![](https://styde.net/wp-content/uploads/2015/06/homestead-version.png)

Nos muestra la versión actual de Homestead

Nota.- No debemos olvidar que antes de todo esto ya debemos tener la box de Homestead instalada.

Ya que estamos en la consola de git, aprovechemos de una vez para generar nuestras llaves SSH si es que no lo hemos hecho con anterioridad, para esto vamos a teclear el comando

![](https://styde.net/wp-content/uploads/2015/06/generate-key.png)

Llave generada correctamente

Ya con nuestra llave lista podemos proceder a correr el comando para iniciar Homestead, esto es importante para que se genere nuestro archivo de configuración, para esto tecleamos

```bash
homestead init
```
Si tenemos homestead configurado globalmente, en caso que no tecleamos
```bash
vagrant init
```

después tecleamos
```bash
homestead edit
// o
vagrant edit
```

para poder configurar nuestro entorno, al hacer esto nos aparecerá un bloc de notas con las configuraciones por default, aquí solo debemos agregar o modificar los parámetros que necesitemos, tales como agregar o quitar proyectos, incrementar o decrementar la memoria ram, indicar la ruta de nuestras llaves SSH, etc.

Para este ejemplo vamos a agregar un proyecto el cual llamaremos prueba.app, nuestro documento de configuración deberá verse como se ve a continuación:

![](https://styde.net/wp-content/uploads/2015/06/homestead-init.png)

Parámetros de nuestro entorno

Presten especial atención al área marcada, la sección de folders nos indica el mapa que se va a tomar como relación en nuestra máquina virtual, esto quiere decir que debemos tener una carpeta llamada Code en nuestro home de Windows, así que debemos crearla tecleando en la consola de git

```bash
mkdir ~/Code
```

La sección de sites nos indica cuáles son los proyectos que vamos a tener configurados en homestead, en este ejemplo tenemos dos, homestead.app y prueba.app, estos debemos de configurarlos en windows para que puedan reconocerse al momento de querer entrar al navegador, para esto debemos modificar nuestro archivo de hosts ubicado en **C:\Windows\System32\drivers\etc** y debe estar como se muestra a continuación:

![](https://styde.net/wp-content/uploads/2015/06/homestead-hosts.png)

Virtual Hosts de los proyectos

Al final del archivo en cada linea agregamos la IP de nuestro homestead y el nombre que le daremos a nuestro host virtual, todo esto podemos indicarlo cuando ejecutamos el comando

```bash
homestead edit
// o
vagrant edit
```

##Correr Homestead

Una vez que tengamos todo listo solo debemos teclear

```bash
homestead up
// o
vagrant up
```

y automáticamente se empezará a cargar nuestra máquina virtual con homestead

![](https://styde.net/wp-content/uploads/2015/06/homestead-up.png)

Cargando máquina virtual

Importante

Una vez que se termine de cargar la máquina virtual, lo más común es que intenten entrar a ella con el comando

```bash
homestead ssh
// o
vagrant ssh
```

pero esto en windows no es así dado que puede ocasionar que la consola muestre símbolos raros y no podamos ver nada, aquí es donde entra PuTTY al rescate, al abrir PuTTY nosotros podemos acceder por SSH a nuestro servidor sin problemas, solo debemos indicarle la dirección IP de la máquina virtual y listo, nos permitirá entrar a ella, al hacerlo nos pedirá usuario y password, para ambos es vagrant

![](https://styde.net/wp-content/uploads/2015/06/vagrant.png)

Conectando a Homestead

Una vez dentro de **homestead** tenemos todo el servidor de **ubuntu** a nuestra disposición para crear, eliminar y trabajar sobre proyectos sin restricción alguna, vamos a crear nuestro proyecto de prueba, para estro primero vamos a la carpeta que configuramos para el proyecto, la cual es **/home/vagrant/Code/prueba/** así que para esto primero vamos a la carpeta Code tecleando

```bash
cd /home/vagrant/code/
```

una vez que estemos ahí podemos crear nuestro proyecto de la manera habitual

```ssh
composer create-project laravel/laravel prueba
```

y una vez que se termine de descargar nuestro proyecto podemos trabajar con el de manera normal.

Por último sólo me queda decirles que para detener la máquina virtual solo deben teclear

```bash
homestead halt
// o
vagrant halt
```

en nuestra consola de git, esto apagará la máquina virtual sin afectar los proyectos en los que estemos trabajando.
