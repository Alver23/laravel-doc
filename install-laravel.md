# Creando proyecto en Laravel

Existen dos formas de crear un proyecto con Laravel, la primera es descargando el archivo master desde su [repositorio oficial de GitHub](https://github.com/laravel/laravel/archive/master.zip) y la otra es usando Composer desde la consola que es precisamente lo que haremos en esta ocasión.

Desde la consola, dirígete al directorio donde guardas tus proyectos web

```
cd /home/vagrant/code/
```

Ahora crearemos el proyecto laravel escribiendo las siguientes palabras mágicas:

```
composer create-project laravel/laravel nombre_del_proyecto --prefer-dist
```

En mi caso en un arranque de creatividad llamaré a mi proyecto “pruebita”

![](https://styde.net/wp-content/uploads/2014/11/laravel-composer.png)

Composer empezará a descargar las librerías necesarias para nuestro proyecto, esto requiere un poco de tiempo.

![](https://styde.net/wp-content/uploads/2014/11/composer-descarga-paquetes.png)

Si no ocurrió algún problema de conexión a Internet veremos que nuestro proyecto “pruebita” se creó correctamente.

![](https://styde.net/wp-content/uploads/2014/11/proyecto-creado-composer-laravel.png)

Para que nuestro proyecto funcione correctamente debemos darle permisos a las siguientes carpetas:

* boostrap/cache
* storage/

Para esto, realizamos el siguiente paso dentro de la consola y parado en nuestro proyecto:

```
cd Code/nombre_proyecto
sudo chmod 775 boostrap/cache -R && sudo chmod 775 storage/ -R 
```

Finalmente para verificar que la creación de nuestro proyecto “pruebita” se realizó de manera correcta, accede a http://192.168.10.10/nombre_del_proyecto/public en el navegador de tu preferencia, despues de ejecutar por la consola

```
php artisan serve
```


Tambien puedes configurar tu virtualhost para que apunte a dicha carpeta y no tener que ejecutar el servidor local.