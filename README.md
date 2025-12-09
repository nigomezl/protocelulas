# protocelulas

# Indice
- Indice
- Concepto
- Estructuras
- Instalacion

# Concepto
Explicación del Simulador de Protocélulas El simulador reproduce un escenario prebiótico donde
distintos tipos de moléculas interactúan física y químicamente en un entorno cerrado. Cada "bola" que
aparece en pantalla representa una molécula con propiedades específicas. 1. Tipos de moléculas (las
“bolas”) Cada partícula es uno de estos cuatro tipos: Aminoácidos (A): Representan bloques básicos
de proteínas. Lípidos (L): Forman membranas y son esenciales para crear compartimentos. Azúcares
(S): Fuentes de energía y soporte estructural. Nucleótidos (N): Bases para material genético. Cada
tipo tiene un color propio y se mueve con velocidad aleatoria similar al movimiento browniano. 2.
Movimiento y comportamiento físico Las moléculas se mueven continuamente dentro del espacio: Se
desplazan con velocidad aleatoria. Rebotan en los bordes del contenedor. Interactúan mediante
colisiones elásticas simples. Esto crea un entorno dinámico que imita un caldo prebiótico. 3. Enlaces y
atracciones Cuando dos moléculas quedan lo suficientemente cerca: Si la distancia es menor al
umbral de enlace (bondDist), se dibuja una línea entre ellas. Con cierta probabilidad (bindProb) forman
un enlace temporal. Los lípidos sienten atracción entre ellos: tienden a agruparse para formar
membranas. 4. Formación de protocélulas Una protocélula aparece cuando: Un grupo de moléculas
está lo suficientemente cerca (protoDist). El grupo supera un tamaño mínimo (minProto). Contiene
suficientes lípidos para actuar como membrana (lipFracThreshold). Cuando se detecta una protocélula:
El simulador traza un círculo violeta que representa su membrana. Ese grupo de moléculas actúa
como un compartimento emergente. 5. Visualización en tiempo real El simulador muestra: El
movimiento de todas las moléculas. Enlaces cercanos (líneas grises). Protocélulas detectadas
(círculos violetas). Una gráfica a la derecha con la evolución del número de moléculas y protocélulas.
6. Controles principales Init: Genera nueva población de moléculas. Play/Pause: Inicia o detiene la
simulación. Step: Avanza un solo paso. Reset: Reinicia todo el entorno. Sliders para ajustar
parámetros físicos y químicos. 7. Interpretación El modelo simula cómo moléculas simples pueden
auto-organizarse y formar estructuras parecidas a protocélulas. Aunque simplificado, ilustra principios
reales de química prebiótica: Auto-organización espontánea. Importancia de lípidos para formar
compartimentos. Interacciones físicas que llevan a estructuras emergentes. Conclusión El simulador
no intenta replicar la biología real con exactitud, sino mostrar visualmente cómo unidades simples,
cuando siguen reglas físicas y químicas básicas, pueden producir estructuras complejas y “vivas”
como protocélulas

# Estructuras
Estructuras de Datos en el Simulador de Protocélulas
Este documento explica de forma sencilla cómo está construido el simulador y cuáles son las
estructuras de datos que permiten que funcione, centrándonos en el grafo dinámico.
1. Arreglo principal: molecules[]
Cada molécula se almacena como un objeto con:- x, y: posición normalizada- vx, vy: velocidad- type: A, L, S, N- graphics: componente visual- boundTo: Set() donde se guardan enlaces temporales con otras moléculas
Este arreglo permite recorrer todas las moléculas y aplicar física cuadro a cuadro.
2. Grafo dinámico entre moléculas
El grafo NO se almacena explícitamente como matriz o lista de adyacencia.
Se construye implícitamente en cada paso usando proximidad, con dos tipos de aristas:
• Arista de proximidad: existe si distancia < protoDist
• Arista química (enlace temporal): existe si dos moléculas se unieron y se agrega el índice al Set
boundTo
Este grafo es dinámico porque cambia cada frame, dependiendo de la física.
3. Grid espacial (hash 2D)
Estructura clave para acelerar el grafo:
grid = { "i,j": [indices de partículas] }
Permite consultar vecinos en O(1) promedio en vez de O(n²).
4. BFS con colas para detectar clústeres
Una cola FIFO se usa para explorar el grafo de proximidad:- Se comienza desde una molécula- Se añaden vecinos cercanos- Se expande hasta formar el clúster completo
Esto permite detectar protocélulas (componentes conexos).
5. Sets para enlaces químicos
boundTo es un Set() que almacena índices de moléculas enlazadas.
Esto evita duplicados y permite borrar/enlazar rápidamente.
6. Resumen
El simulador usa:- Arreglos para almacenar partículas- Un grafo dinámico basado en distancia- Un hash grid espacial para optimización- Colas BFS para hallar clústeres- Sets para enlaces entre moléculas
Estructuras de datos esenciales:
→ Grafo dinámico
→ Grid hash 2D
→ Cola BFS
→ Sets
→ Arreglo de objetos

# Instalacion
Solo hay que descargar el archivo html y luego ejecutarlo por medio de un navegador
