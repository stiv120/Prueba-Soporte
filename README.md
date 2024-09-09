# Prueba Técnica - Sistema de Gestión de Tareas

## Descripción del Proyecto

Este proyecto es un sistema básico de gestión de tareas desarrollado con Laravel y Vue.js. El objetivo de esta prueba técnica es identificar y corregir errores en el código tanto en el backend como en el frontend. El sistema permite a los usuarios crear, actualizar, eliminar y visualizar tareas.

## Objetivo de la Prueba

El objetivo principal de esta prueba es evaluar tus habilidades para depurar y corregir errores en un proyecto existente que utiliza Laravel, PHP, JavaScript, y Vue.js. Deberás:

- Identificar y corregir errores en el backend relacionado con la creación, actualización, eliminación y validación de tareas.
- Corregir problemas en el frontend que afectan la visualización y manejo de la lista de tareas.
- Asegurarte de que las tareas se gestionen correctamente en la interfaz de usuario.

Además, deberás agregar una funcionalidad extra para filtrar las tareas completadas y pendientes.

## Instrucciones de Instalación

Sigue los siguientes pasos para configurar el proyecto en tu entorno local:


1. **Clona el repositorio:**

       Prueba-Soporte
   
2. **Instala las dependencias de PHP y Node.js:**

   .Composer: Para instalar las dependencias de PHP, ejecuta:
   
        composer install

   .NPM: Para instalar las dependencias de Node.js, ejecuta:

        npm install
        npm run dev

3. **Configura el archivo de entorno .env:**

   .Copia el archivo .env.example a .env:

       cp .env.example .env
   
   .Genera la clave de la aplicación:

       php artisan key:generate
   
   .Configura la base de datos en el archivo .env. Asegúrate de tener una base de datos MySQL disponible y configurada.
   
4. **Ejecuta las migraciones para crear las tablas necesarias:**

       php artisan migrate

5. **Compilar Recursos de Frontend:**

   .Compila los archivos de frontend utilizando Laravel Mix:

       npm run dev

6. **Iniciar el Servidor:**

   .Inicia el servidor de desarrollo de Laravel:

       php artisan serve

       
**Objetivo de la Prueba**

El proyecto contiene errores tanto en el backend (Laravel/PHP) como en el frontend (JavaScript). Tu objetivo es:

 1.Identificar los errores en el código.
 2.Corregir los errores para que la aplicación funcione correctamente.
 3.Probar la aplicación después de realizar las correcciones para asegurarte de que todo funcione como se espera.
 
**Entrega**

Sube el código corregido a un repositorio de GitHub y envíanos el enlace. Asegúrate de describir los problemas que encontraste y cómo los solucionaste en este archivo README.md.

**Notas**

Puedes añadir cualquier comentario adicional sobre las decisiones que tomaste al corregir el código.
Recuerda que el objetivo es demostrar tu capacidad para depurar y mejorar código existente.

¡Buena suerte!

Puedo notar que la versión de laravel del proyecto es la 7, en la cual tienen especificado en el composer.json que se
pueda usar una versión de PHP 7.2.5 O 8.0, actualmente laravel se encuentra en la versión 11 y php 8.3 estable.

## Errores a nivel de backend 
1. El primer error que pude identificar al correr la aplicación fue al intentar crear la tarea, sale el error de tabla user
no encontrada, este error se debe a que en el modelo User está definido el nombre de la tabla users y en la BD la tabla se
llama user, este error viene de la migración ya que el estándar popular de laravel es que el nombre de las tablas en BD debe
ser plural.

2. En el controlador se agregó el método para obtener las tareas, llamado fetchTasks el cual carga el listado de tareas si
existen al cargar la página. también se añadió el método para filtrar las tareas completadas y pendientes (pending and completed),
ambos métodos con sus respectivas rutas. se optimizó el código de acuerdo a los principios SOLID ya que se estaban ejecutando las
validaciones de los campos ahí, esto lo mejoré agregando un formRequest para validar los campos al insertar y realizar la consulta
del usuario y hacer la respectiva validación en la clase TaskRequest, además de esto se optimizaron las respuestas de los métodos
para que retorne el json de respuesta esperado en la petición del cliente (frontend).

## Errores a nivel de frontend
1. Los errores encontrados fue que no se cargaba el listado al iniciar ya que faltaba hacer la petición del método fetchTasks,
la mutación  y añadirlo al mounted(), el método completeTask se llamaba updateTask en el archivo store.js por lo cual no se estaba
encontrando el método para realizar la petición.

2. Se añadió al igual que en el backend el método para filtrar las tareas con la respectiva petición, mutación y la ruta, también
se añade un vue-select para seleccionar las tareas que se requieren filtrar, ya sea una sola o ambas, el select es múltiple.

Por último añadí cómo nueva funcionalidad, toast de vue, para mostrar las respuestas de las acciones al usuario.
   
