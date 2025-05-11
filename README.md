# Simulacro-Parcial-2-Redes

https://github.com/mdedifer/Simulacro-Parcial-2-Redes


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

A través de la máscara de subred obtenermos el número de bits de red (fijos) (1s de la máscara).  
255     = 11111111  
255     = 11111111  
248     = 11111000  
0       = 00000000  
Hay 21 bits de red, por lo que sería una subred /21: 172.29.152.0/21. 
Tendrá 32-21=11 bits de host (variables). Esto indica que la red tendrá 2^11=2048 direcciones.

Pasamos la dirección ip de la subred a binario e identificamos los 21 bits fijos:  
172     = 10101100  
29      = 00011101  
152     = 10011|000  
0       = 00000000

La dirección de broadcast es la última dirección disponible de la subred, por lo que todos los bits de host tienen que estar puestos a 1:


172     = 10101100 = 172  
29      = 00011101 = 29  
152     -> 10011|111 (+7)= 159  
0       -> 11111111 = 255  

Dirección de broadcast: 172.29.159.255 .

#### **b)**

A través del prefijo de subred /23 obtenermos que el número de bits de red (fijos) (1s) es 23.  
255     = 11111111  
255     = 11111111  
254     = 11111110  
0       = 00000000  
Hay 23 bits de red, por lo que tendrá 32-23=9 bits de host (variables). Esto indica que la red tendrá 2^9=512 direcciones.

Pasamos la dirección ip de la subred a binario e identificamos los 23 bits fijos:  
172  → 10101100  
18   → 00010010  
26   → 0001101|0  
0    → 00000000

La dirección de broadcast es la última dirección disponible de la subred, por lo que todos los bits de host tienen que estar puestos a 1:


172  → 10101100  
18   → 00010010  
27   → 0001101|1  
255    → 11111111 

Dirección de broadcast: 172.18.27.255 .


### 3. Última Dirección Válida y Rango de Hosts

#### **a)**

A través de la máscara de subred obtenermos el número de bits de red (fijos) (1s de la máscara).  
255     = 11111111  
255     = 11111111  
255     = 11111111  
192       = 11000000  
Hay 26 bits de red, por lo que sería una subred /26: 172.30.67.192/26. 
Tendrá 32-26=6 bits de host (variables). Esto indica que la red tendrá 2^6=64 direcciones.

Pasamos la dirección ip de la subred a binario e identificamos los 26 bits fijos:  
172     = 10101100  
30      = 00011110  
67      = 01000011  
192     = 11|000000

La última dirección válida es la penúltima dirección ya que la última dirección disponible es la dirección de broadcast. De esta manera, hay que poner todos los bits de host a 1 excepto el último:  
172     = 10101100  
30      = 00011110  
67      = 01000011  
254     = 11|111110  

Última dirección válida: 172.30.67.254 .

#### **b)**

A través de la máscara de subred obtenermos el número de bits de red (fijos) (1s de la máscara).  
255     = 11111111  
255     = 11111111  
252     = 11111100  
0       = 00000000   
Hay 22 bits de red, por lo que sería una subred /22. 
Tendrá 32-22=10 bits de host (variables). Esto indica que la red tendrá 2^10=1024 direcciones.

Pasamos la dirección ip a binario e identificamos los 22 bits fijos:  
172     = 10101100  
22      = 00010110  
53      = 001101|01  
199     = 11000111

De aquí sacamos que la subred es:  
172     = 10101100  
22      = 00010110  
52      = 001101|00  
0       = 00000000

Subred: 172.22.52.0/22, siendo:  
- Dirección de red: 172.22.52.0  
- Dirección de broadcast: 172.22.55.255  
Y lo que nos piden en el problema:  
- Primera dirección válida: 172.22.52.1  
- Última dirección válida: 172.22.55.254  


### 4. Capacidad y Segmentación de Subredes

#### **a)**

A través de la máscara de subred obtenermos el número de bits de red (fijos) (1s de la máscara).  
255     = 11111111  
255     = 11111111  
255     = 11111111  
192     = 11000000
Hay 26 bits de red, por lo que sería una subred /26: 172.26.0.0/26. 
Tendrá 32-26=6 bits de host (variables). Esto indica que la red tendrá 2^6=64 direcciones.  
Siempre la primera dirección será la dirección de red y la última la dirección de broadcast. Esto implica que esta subred tendrá 62 direcciones disponibles (=número de equipos/hosts posibles).


#### **b)**

A través del prefijo de subred /23 obtenermos que el número de bits de red (fijos) (1s) es 23.  
255     = 11111111  
255     = 11111111  
254     = 11111110  
0       = 00000000  
Hay 23 bits de red, por lo que tendrá 32-23=9 bits de host (variables). Esto indica que la red tendrá 2^9=512 direcciones.

Pasamos la dirección ip a binario e identificamos los 23 bits fijos:  
172     = 10101100  
18      = 00010010  
171     = 1010101|1  
190     = 10111110  

La dirección de red es la primera dirección, donde los bits de hosts (a partir del bit 23) son 0:


172     = 10101100  
18      = 00010010  
170     = 1010101|0  
0     = 00000000 

Dirección de red: 172.18.170.0 .


### 5. Número de Subredes Necesarias

La fórmula: "Nº de subredes = 2^s" se explica fácilmente entendiendo el concepto de los bits de hosts. Los bits de hosts son los bits que identifican al host en una red. Son los bits de detrás del último bit de red, cuya posición viene indicada por el prefijo de la red.  
Cada bit puede tomar 2 valores, 1 o 0 (al estar en binario) por lo que, cada vez que tomemos un bit de host (de la red padre) y lo consideremos parte del identificador de la subred, se duplicarán el número de subredes posible. Visto en un ejemplo más fácil:
- 1 bit de host transformado en bit de red: 2¹ = 2 subredes
- 2 bits de host transformado en bit de red: 2² = 4 subredes
- 3 bits de host transformado en bit de red: 2³ = 8 subredes

**Aplicación práctica con al menos 4 subredes**

Utilizando la fórmula, vemos que para tener 4 subredes necesitamos 2 bits de hosts que pasen a ser parte del identificador de la subred (2^2=4).  
Si quisiéramos más subredes, tendríamos que dar más bits de hosts.  
Para verlo en una aplicación real de una red: Si tuviésemos una red /24 y quisiéramos 4 subredes, tendríamos que utilizar 2 bits adicionales del campo de host, justo después del bit 24, como parte del identificador de subred, quedándonos 4 subredes /26.