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

### Calculo de tiempo total entre dos puntos

El calculo de tiempo total de un viaje, tiene en cuenta la suma de los calculos de los tiempos que tarda el solicitante en recorrer cada **Trayecto** para esto se utiliza un patron **Adapter** donde se almacena en la clase Trayecto un atributo de tipo interface **CalculadorDistancia**.
Esta interface tiene un metodo _calcularDistancia_ que toma dos parametros de Lugar y devuelve un Double con la distancia entre dos puntos.

### Calculo del tiempo total de un viaje

El usuario antes de iniciar un Viaje define el Modo en que quiere Viajar: Si parametriza los minutos a esperar en cada parada o si va avisando punto por punto su salud.
En nuestro caso pensamos un patron **Strategy** donde se utiliza una clase abstracta llamada **ModoDeViaje** esa clase tiene un metodo llamado calcularTiempoDemoraTotal que devuelve un double.De esa clase heredan dos clases hijas **DetenerseNMinutosEnCadaParada** que tiene un atributo minutosAEsperar parametrizable y otra clase que hereda llamada **AvisarEnCadaPunto**
Ambas clases implementan su calculo del viaje total segun lo que haya configurado el usuario para ese viaje que se guarda en el atributo modoDeViaje dentro de la clase Viaje que ejecuta un metodo calcularTiempoDemora que calcula el tiempo demora del Viaje delegando la responsabilidad en el atributo indicado.


