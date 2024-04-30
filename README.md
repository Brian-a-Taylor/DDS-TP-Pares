# Decisiones de Diseño

## Clase Cuidadora y Solicitante 

En virtud de resolver el dilema de pensar los Cuidadores y los Solicitantes de los viajes se pensaron dos clases: **Cuiadador** y **Solicitante**.
Cada clase almacena el nombre, la dirreccion(normalizada con otra clase como **Lugar**),sexo(Enum debido a simplicidad de la decision),telefono(normalizada con otra clase como **Contacto**).

## Clase Viaje 

A nuestro entender una clase fundamental del diseño que proponemos es el **Viaje** que alamcena el Solicitante,la lista de Cuidadores que aceptan el viaje,el origen del viaje,el destino del viaje,una lista de estados
Un viaje se instancia cada vez que el solicitante mediante la app solicita un viaje(donde detalla la lista de Trayectos que va a recorrer y la lista de Cuidadores elegidos).
Al realizar esto se agrega a la lista de estados de Viaje un **EstadoViaje** que almacena la fecha y hora y ademas un **PosibleEstadoViaje** que es de tipo _Solicitado_.

## Acciones a configurar por Solicitante

En nuestro diseño en lo referido a como reacciona el usuario frente a un incidente en el Viaje, se penso en un patron **Strategy**.La clase Contexto seria el Solicitante que almacena una **Accion** que esta modelada como clase abstracta y cada tipo de reaccion que puede elegir el solicitante,hereda de **Accion** y define su propia implementacion del metodo _ejecutar_ que recibe como parametro **Viaje**.
Cada vez que un Viaje se interrumpe por X motivo, se agrega a la lista de estados de Viaje, el estado _Interrumpido_, se almcena la fecha y hora y ademas el usuario ejecuta la accion preventiva que configuro previamente.

## Notificaciones

En relacion a las notificaciones que deshabilita/habilita el Solicitante se penso en tener almacenada en la clase **Contacto** un atributo _notificacionActiva_ que indica si el contacto del usuario puede recibir o no notificaciones,se va cambiando ese valor segun lo detallado en los distintos momentos del sistema.
Tambien se almacena en una lista las notificaciones que va recibiendo el solicitante en su telefono mediante la clase **Notificacion** que almacena la fecha/hora de la notificacion y el mensaje de la misma.

## Trayectos dentro de un Viaje

En relacion al punto 2,como el solicitante ahora puede aclarar distintos trayectos dentro de un mismo viaje,se almacena en la clase **Viaje** una lista de **Trayecto**.
Cada **Trayecto** almacena el origen y el destino, el orden en que se recorre y ademas un atributo de tipo **CalculadorDistancia** que sera desarrollada abajo.

### Calculo de tiempo total de un viaje

El calculo de tiempo total de un viaje, tiene en cuenta la suma de los calculos de los tiempos que tarda el solicitante en recorrer cada **Trayecto** para esto se utiliza un patron **Adapter** donde se almacena en la clase Trayecto un atributo de tipo interface **CalculadorDistancia**.
Esta interface tiene un metodo _calcularDistancia_ que toma dos parametros de Lugar y devuelve un Double con la distancia entre dos puntos.


