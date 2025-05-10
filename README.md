# Simulacro-Parcial-2-Redes

https://github.com/mdedifer/Simulacro-Parcial-2-Redes

En la clase del viernes no hemos estado haciendo esto del simulacro. En cuanto lo haga (posiblemente sábado por la mañana) lo verás aquí.

## Parte 1: Capa de Red

### 1. Cálculo de ruta más corta

#### **a)**  
El enrutamiento en el contexto de redes se trata de elegir el mejor camino para enviar datos desde un origen hasta un destino. Las redes se representan con grafos, donde los nodos son routers y los enlaces son las conexiones entre ellos. Estos enlaces tienen pesos asociados (que pueden indicar tiempo, distancia, etc.).  

El algoritmo de Dijkstra se utiliza para encontrar el camino más corto desde un nodo a todos los demás nodos. Estos caminos más cortos desde el router y hacia cada destino posible se almacenarán en una tabla de enrutamiento. Por lo tanto, cuando se termine el proceso, cada router tendrá su tabla de enrutamiento que usará cuando tenga que enviar un paquete, conociendo su destino.

El algoritmo de Dijkstra se hace por pasos:  
1. Inicializa todos los nodos con distancia infinita, excepto el de origen, que se pone a 0.
2. Crea un conjunto de nodos visitados (inicialmente vacío).
3. Escoge el nodo no visitado con la distancia más corta desde el origen.
4. Para cada vecino de ese nodo, actualiza su distancia si se encuentra un camino más corto a través del nodo actual.
5. Marca el nodo actual como visitado.
6. Repite desde el paso 3 hasta que todos los nodos estén visitados o se haya encontrado el destino.  

Por ejemplo protocolos como OSPF utilizan el algoritmo de Dikjstra.

#### **b)**

El enrutamiento por inundación es otro método para rutas posibles entre routers. Es un método más bruto que Dijkstra ya que no calcula rutas óptimas ni mira los pesos de los enlaces, solo asegura que llegue el paquete.  
En este método, cada router envía el paquete por todos sus puertos. El paquete se replica y viaja por toda la red hasta que:
- Llega al nodo de destino
- Se agota el TTL
- O el router detecta que ya le ha llegado ese paquete antes.

Este método es menos eficiente ya que genera mucho tráfico y usa muchos recursos al provocar muchos duplicados. Para limitar esto se utiliza el TTL, que es un contador de saltos, que limita cuántos nodos puede atravesar.

Normalmente no se utiliza inundación pura cada vez que se envía un mensaje. Solamente se utiliza la primera vez que se envía un paquete desde un origen a un destino para averiguar cuál es el camino más corto. Esto se apuntaría en la tabla de enrutamiento, para que cuando aparezcan futuros paquetes con la misma ruta, el router ya sepa por dónde lo tiene que enviar.


### 2. Cálculo de Direcciones de Broadcast y Subredes

#### **a)**



#### **b)**