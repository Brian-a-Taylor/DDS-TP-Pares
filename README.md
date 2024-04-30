# Decisiones de Diseño

## Clase Cuidadora y Solicitante 

En virtud de resolver el dilema de pensar los Cuidadores y los Solicitantes de los viajes se pensaron dos clases: **Cuiadador** y **Solicitante**.
Cada clase almacena el nombre, la dirreccion(normalizada con otra clase como **Lugar**),sexo(Enum debido a simplicidad de la decision),telefono(normalizada con otra clase como **Contacto**)

## Clase Viaje 

A nuestro entender una clase fundamental del diseño que proponemos es el **Viaje** que alamcena el Solicitante,la lista de Cuidadores que aceptan el viaje,el origen del viaje,el destino del viaje,una lista de estados
Un viaje se instancia cada vez que el solicitante mediante la app solicita un viaje(donde detalla la lista de Trayectos que va a recorrer y la lista de Cuidadores elegidos).
Al realizar esto se agrega a la lista de estados de Viaje un **EstadoViaje** que almacena la fecha y hora y ademas un **PosibleEstadoViaje** que es de tipo _Solicitado_

## Acciones a configurar por Solicitante

En nuestro diseño en lo referido a como reacciona el usuario frente a un incidente en el Viaje, se penso en un patron **Strategy**.La clase Contexto seria el Solicitante que almacena una **Accion**
que esta modelada como clase abstracta y cada tipo de reaccion que puede elegir el solicitante,hereda de **Accion** y define su propia implementacion del metodo ejecutar que recibe como parametro **Viaje**
