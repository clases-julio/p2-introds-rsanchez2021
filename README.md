# P2-IntroDS
Autor: Rebeca Sánchez

Fecha entrega: 19/10/2022

En esta segunda práctica el objetivo es crear un diagrama de clases inicial para la empresa que nos describen a lo largo del enunciado.

## Introducción
Este problema se irá resolviendo poco a poco a lo largo del curso. 
El problema es el sigueinte: una empresa solicita desarrollar un sistema software para dar soporte a una completa infraestrucctura de sensores. Tendremos que diseñar el sistema que da solución al problema e implementarlo empleando programación orientada a objetos (POO).

## Especificaciones de requerimiento
Una empresa dedicada al desarrollo autosostenible pretende implementar un sistema multisensorial en un invernadero, de forma que pueda tener controladas todas las variables climatológicas tanto de forma **presencial como remota**. Debe incorporar los mecanismos necesarios para **controlar la seguridad de la empresa**: alarma, detención de puertas/ventanas abiertas, etc.

Cualquier empleado podrá acceder al sistema para acceder a todos los datos. Cada **empleado solo puede tener una cuanta** en el sistema.

**Componentes hardware de la interfaz de usuario**:
- **Pantalla** con los datos
- **Teclado** para la entrada de datos
- **Micrófoco** para dar instrucciones y que sean escuchadas desde las distintas estaciones
- **Interruptor** o similar para activar/desactivar la alarma

**Software** --> leer datos de los sensores y cámaras de las **distintas ubicaciones** y que los vierta de forma más sencilla mediante un **interfaz gráfico**.
Se utilizará el monitor para simular la interfaz, el teclado como entrada de datos y los dispositivos sensoriales verterán los datos mediante distintos algoritmos.

Una sesión con el interfaz del sistema consiste en la autentificación de un usuario (**empleado**) mediante la autentificación de un número de identificacción (**dashboard**). Para autenticar al usuario y que pueda acceder, el programa debe **interactuar con la base de datos** de información sobre los empleados registrados en la empresa. Para cada uno, la base almacena un **número de usuario, un  NIF y un timestamp** que indica la fecha del último acceso al sistema. Para simplificar el ejemplo se va a suponer que la empresa confía en este sistema para que acceda a la información de la base de datos y la manipule sin necesidad demedidas de seguridad considerables.

El usuario deberá experimentar la siguiente secuencia de eventos:
1. La pantalla muestra un mensaje de bienvenida y pide al usuario que introduzca un número de empleado.
2. El usuario introduce el número de empleado de conco dígitos mediante el teclado numérico.
3. Aparece un mensaje en la pantallla en elque pide el NIF asociado al empleado.
4. Introduce el NIF de och dígitos mediante el teclado.
5. Si el número de empleado y el NIF son correctos en la pantalla aparece dashboard. Si el usuario introduce un número de empleado o NIF inválidos la pantalla muestra un mensaje y después el sistema regresa al paso 1.

El **dashboard** debe contener información actualizada de los valores vertidos por los sensores y las **imágenes en tiempo real** vertidas por las cámaras de seguridad. También debe haber una opción de salida del sistema en cualquier momento.

Debe haber un mínimo de cuatro sensores y dos cámaras conectadas, aunque en cualquier momento puede variar el número. Las opciones por defecto en el dashboard son:
1. Temperatura
2. Humedad
3. calidad del aire
4. Nivel de iluminación
5. Cámara RGB
6. Cámara térmica
7. Salir

Deben estar numeradas para que el usuario pueda acceder. Si introduce una opción inválida se muestra un mensaje de error y vuelve a mostrar el menú principal. Si introduce *Salir* se cierra el sistema y vuelve a la pantalla de bienvenida. Si introduce una opción válida se debe cambiar a la pantalla la información más detallada con los datos de la última hora y una opción *Volver al menú*. 


## Ejercicio
El ejercicio consiste en hacer un boceto del diagrama de clases para la empresa con las especificaciones explicadas en el apartado anterior. 

En un primer momento no entendía muy bien cómo hacer el diagrama. El primer boceto que se me ocurrió fue el siguiente:

![Esquema inicial](https://github.com/rsanchez2021/Image/blob/main/esquema_inicial.jpeg "primer esquema")

En este primer esquema partí todo en base a la clase *User* pero no me terminaba de convencer pues era comlicado de enterder y aún me faltaban muchas clases que no sabía donde meter y conectar como el *Server*, el *Dashboard* o *Security*.

En el segundo diagrama en sucio añadí todo el hardware y la seguridad:

![Boceto esquema final](https://github.com/rsanchez2021/Image/blob/main/esquema_final.jpeg "Boceto esquema final")

En este boceto ya se puede ver que están todas las clases que creo que eran necesarias y todos los componentes. Este segundo boceto lo centralicé más en la clase *Server* y *Dashboar* pues algunos de mis compañeros me lo recomendaros y explicaron para que lo pudiése mejorar. Se puede ver también algunas anotaciones de qué métodos tengo que poner en algunas clases o los atributos para entender cómo funcionan los distintos tipos de flechas.

La clase *User* en rojo se debe a que tenía varias opciones de cómo hacerlo:

En esta primera opción de user sale administrador y empleado y ambos tienen acceso a Dashboard, pero como tanto empleado y administrador eran igual soloque el admin puede acceder a la base de datos y modificarla, descarté esa opción.
![User opción 1](https://github.com/rsanchez2021/Image/blob/main/user_inicial.jpeg "Primera opción User")

En la segunda opción son admin y empleado son diferentes clases que heredan de un clase User. Esta opción la descarté pues el empleado no puede modificar la base de datos yno sabía qué métodos utilizar en cada uno.
![User opción 2](https://github.com/rsanchez2021/Image/blob/main/otro_user.jpeg?raw=true "Segunda opción user")

Al final la solución fue unificar administrador y empleado en una clase *User* e introducir una variable booleana de si es administrador y que el server lo chequee en un método para que pueda acceder a la base de datos o no. 

Finalmente, el diagrama de clases con atributos y métodos pero sin las uniones entre clases correspondientes se queda de la siguiente maner: 

![Diagrama de clases sin uniones](https://github.com/rsanchez2021/Image/blob/main/diagrama_clase.PNG "Diagrama sin uniones finales")

## Explicación diagrama

Para poder explicar el diagrama, voy a dividirlo en cuatro secciones: seguridad, sensores, user y Dashboard.

En seguridad, se centra en una clase *Security* que obtiene información tanto de los sensores de la puerta y la ventana, y de las cámaras de seguridad. También depende de un interruptor para encender y apagar la alarma y de un altavoz por el cual se puede utilizar en caso de que haya un intruso (play_alarm).

La parte de sensores abarca las siete clases de los sensores y una clase *Sensors* de la que heredan encender, apagar, localización, estado y tipo de sensor. Como la interfaz debe mostrar los datos de la última hora de los sensores, todos ellos están conectados directamente al *Server* donde se guardan todos los datos en las diferentes arrays ( #database: array(sensor) )

Para User, ya se ha explicado antes las diferentes opciones y la opción final, introducir un booleano para comprobar si lo es y así poder acceder a la base de datos. Para poder saber qué empleado es se ha creado la clase *Login* donde se comprueba el número de empleado y nif, y luego en la clase "User" se obtienen de la base de datos. 

El dashboard se fundamenta en mostrar los datos, utilizar los componentes hardware (de entrada y salida) y algún método concreto de las especificaciones como exit() o return().
