# P2-IntroDS
Autor: Rebeca Sánchez

Fecha entrega: 19/10/2022

En esta segunda práctica el objetivo es crear un diagrama de clases inicial para la empresa que nos describen a lo largo del enunciado.

## 1. Introducción
Este problema se irá resolviendo poco a poco a lo largo del curso. 
El problema es el sigueinte: una empresa solicita desarrollar un sistema software para dar soporte a una completa infraestrucctura de sensores. Tendremos que diseñar el sistema que da solución al problema e implementarlo empleando programación orientada a objetos (POO).

## 2. Especificaciones de requerimiento
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

El **dashboard** debe contener información actualizada de los valores vertidos por los sensores y las imágenes en tiempo real vertidas por las cámaras de seguridad. También debe haber una opción de salida del sistema en cualquier momento.

Debe haber un mínimo de cuatro sensores y dos cámaras conectadas, aunque en cualquier momento puede variar el número.  Las opciones por defecto en el dashboard son:
1. Temperatura
2. Humedad
3. calidad del aire
4. Nivel de iluminación
5. Cámara RGB
6. Cámara térmica
7. Salir

Deben estar numeradas para que el usuario pueda acceder. Si introduce una opción inválida se muestra un mensaje de error y vuelve a mostrar el menú principal. Si introduce *Salir* se cierra el sistema y vuelve a la pantalla de bienvenida. Si introduce una opción válida se debe cambiar a la pantalla la información más detallada con los datos de la última hora y una opción *Volver al menú*. 

## 3. Análisis del sistema 




## 4. Diagramas de casos de uso




## 5. Diseño del sistema multisensorial



