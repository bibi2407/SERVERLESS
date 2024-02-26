<h1 align="center"> SERVERLESS </h1>

## ÍNDICE
- [¿Que es serverless?](#QUE_ES?)
- [Beneficios](#Beneficios)
- [Ventajas y Desventajas](#Ventajas_Desventajas) 
- [¿Que operador dispone?](#que-operador-dispone)
- [Arquitectura](#Arquitectura)
- [Funciones Serverless](#Funciones) 
- [Como implementar SERVERLESS en OpenShift](#Implemantación)   

<br>

## QUE ES SERVERLESS?
<br>
Red Hat OpenShift Serverless es una capa oculta que se encuentra encima de la plataforma de contenedores de Red Hat Openshift(RHCOP), la cual permite desplegar contenedores de una manera estandarizada.

### Para que sirve?
OpenShift Serverless ayuda a los desarrolladores a implementar y ejecutar aplicaciones que se escalarán verticalmente o se reducirán a cero a petición. Esto elimina el consumo de recursos cuando no están en uso. El código de la aplicación puede empaquetarse en un contenedor junto con los runtime adecuados.

<br>

## BENEFICIOS

<br>

- Esta capa hace que los usuarios no se tengan que preocupar por despliegues, actualizaciones, interconexion entre aplicaciones, ni autoescalado. Por tanto, la implementación de esta capa mejora los requerimientos de calidad de escalabilidad, elasticidad, e interoperabilidad para cualquier proyecto.

<br>


## VENTAJAS Y DESVENTAJAS
<br>

![alt text](<ventajas y desventajas-1.png>)


### <em>VENTAJAS DE SERVERLESS</em>
<br>

`1. Escalabilidad Automática`: Las funciones serverless se escalan automáticamente según la demanda, permitiendo un manejo eficiente de cargas variables.

`2. Eficiencia en Costos`: Solo pagas por el tiempo de ejecución de las funciones, lo que puede resultar más económico que mantener servidores activos continuamente.

`3. Simplificación del Desarrollo`: Los desarrolladores pueden centrarse en escribir código sin preocuparse por la gestión de la infraestructura, acelerando el desarrollo.

`4.Despliegue Rápido`: Las funciones se despliegan de manera rápida, facilitando la implementación y actualización continua.

`5. Menos Administración de Infraestructura`: Reducción significativa de tareas administrativas, ya que el proveedor de servicios en la nube maneja la infraestructura subyacente.
<br>
<br>

### <em>DESVENTAJAS DE SERVERLESS</em>
<br>

`1. Tiempo de Arranque`: Las funciones serverless pueden experimentar tiempos de arranque, lo que puede afectar la latencia en comparación con servidores que ya están en ejecución.

`2. Límites de Ejecución`: Hay límites en el tiempo de ejecución y el tamaño de los recursos para cada función, lo que puede afectar aplicaciones intensivas en cómputo o memoria.

`3. Complejidad en el Monitoreo`: Puede ser más desafiante monitorear y depurar aplicaciones serverless debido a su naturaleza efímera y distribuida.

`4. Limitaciones de Entorno`: Algunos entornos serverless pueden tener limitaciones en las bibliotecas y configuraciones del entorno de ejecución.

`5. Posible "Cold Start"`: La primera ejecución de una función después de un período de inactividad puede experimentar un "cold start" con un tiempo de inicio más largo.

<br>

## QUE OPERADOR DISPONE?
<br>

OpenShift Serverless está basado en Knative, un proyecto open-source. Ademas, OpenShift Serverless se integra con OpenShift Service Mesh, OpenShift cluster monitoring service para un despliegue y monitoreo unificado de servicios. Tambien se integra con Apache Camel K para soportar fuentes de eventos, como mensajes de Kafka.

<br>

## ARQUITECTURA 


<br>
En primer lugar, OpenShift usa el algoritmo/mecanismo de control loop, el cual se encarga de comparar el estado "buscado" de la aplicación con el estado real, y si hay alguna diferencia, las arregla.

El algoritmo mencionado es parecido al que usa Kubernetes al controlar el estado de los pods. Suponga que el estado "buscado" o ideal de un proyecto en kubernetes tiene 2 pods(replicas), y el estado real es que esos 2 pods estan online. Sin embargo, uno se cae, por lo que el estado ideal y el real serian distintos. Entonces el mecanismo procede a actual y lleva al proyecto al estado ideal.

OpenShift Serverless tiene __2 componentes principales__ :

### <em>SERVING :</em>

Se encarga del despliegue, actualizacion, routing y autoescalado de las aplicaciones.

Por cada versión creada de una aplicación, se crea un nuevo despliegue. Apenas estos despliegues estan disponibles, el componente que hace el routing redirige el trafico hacia estas versiones, aunque tambien se puede hacer de manera manual.

Cuando no hay trafico, los pods de la aplicación se escalan a 0 y el trafico es redirigido a un componente que se llama activador. Cuando haya peticiones que reciba el activador, este envia una peticion al auto-escalador para que active los pods. El usuario puede cambiar esta opción si desea que los pods permanezcan activos.

### <em>EVENTING :</em>


Se encarga de interconectar asincronicamente todas las distintas partes de una aplicación distribuida. Para lograr esto, es necesario que las aplicaciones sigan una arquitectura basada en eventos, en donde estos son el mecanismo de comunicación entre las partes de la aplicación.

Una arquitectura basada en eventos se basa en 2 partes, en la primera, una parte de la aplicación envia un evento, el cual significa " Algo ha pasado", y las otras partes de la aplicación puede que esten escuchen esos eventos, lo cual significa " Cuando esto pase, hazmelo saber "

Se pueden usar __2 tipos de modelo de eventos__ :

- `Messaging` : Usa canales como interfaces que emiten eventos, y suscripciones como el destino para los eventos que emiten los canales.

- `Eventing` : Se usan los triggers(disparadores) para consumir eventos de un broker basado en los atributos del evento.

### <em>KAFKA :</em>
...

<br>

## FUNCIONES SERVERLESS
<br>
Las funciones Serverless son una versión mas simple del modelo serverless, que se enfoca en tareas especícficas, las cuales ya vienen con plantillas prediseñadas para crear funciones cloud. En general, las funciones serverless reciben un parametro de entrada, ejecutan el codigo, y retornan una salida. OpenShift Serverless provee un ambiente para correr estas funciones.


<br>

## Como implementar SERVERLESS en OpenShift


### crear un serving

 


### Prerequisitos
- [Instalaciones OpenShift CLI (oc), KNATIVE CLI(kn), OpenShift Serverless Operator](Instalaciones)

