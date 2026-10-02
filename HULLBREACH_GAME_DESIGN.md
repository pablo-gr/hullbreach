# Hullbreach — Especificación de diseño del juego

**Estado:** Documento vivo de diseño
**Versión:** 1.13
**Fuente canónica:** este fichero

Este documento consolida las decisiones de diseño tomadas hasta ahora para Hullbreach. Distingue principios ya fijados de elementos todavía pendientes de concretar.

---

# 1. Concepto general

Hullbreach es un videojuego de navegación, comercio, exploración y combate espacial centrado en el mando de una nave.

La presentación visual del combate toma como referencia general a *Nexus: The Jupiter Incident*: cámara 3D en tercera persona alrededor de la nave, ritmo táctico lento y posibilidad de operar junto a varias naves.

El jugador puede llegar a tener varias naves bajo su mando, pero solo controla completamente su propia nave. Las demás reciben órdenes tácticas de alto nivel y son operadas por sus propios oficiales y tripulaciones.

El juego combina:

- combate espacial inspirado en guerra naval y aérea moderna;
- múltiples modelos de nave;
- modificación profunda de armamento, sensores, defensas, generación eléctrica y otros sistemas;
- consumo básico de recursos;
- comercio, reparación y reclutamiento;
- misiones e información obtenida en estaciones y otros puntos habitados;
- exploración básica de sistemas y planetas;
- una historia principal con misiones secundarias;
- oficiales reclutables con habilidades;
- tripulación genérica con nivel de experiencia general.

---

# 2. Pilares de diseño

## 2.1. Combate de información

El combate se basa en descubrir al enemigo antes de ser descubierto, obtener información suficiente para atacarlo y evitar que el enemigo consiga una solución equivalente.

La situación táctica ideal es:

> Yo sé dónde estás. Tú no sabes dónde estoy.

Los sensores, el sigilo, la orientación, el entorno y el control de emisiones son tan importantes como el armamento.

## 2.2. Player agency directo

Detectar, atacar y defenderse deben ser acciones que el jugador pueda realizar bien o mal.

El combate no debe reducirse a seleccionar un enemigo, pulsar un botón y dejar que una probabilidad determine el resultado.

El azar puede generar incertidumbre en las mediciones, pero no debe sustituir las decisiones del jugador.

## 2.3. Ritmo lento, letalidad alta

El combate es deliberado y da tiempo para observar, interpretar, orientar la nave, configurar armas y reaccionar.

Esto no implica armas poco letales. Una batalla puede desarrollarse lentamente hasta que una buena solución de tiro produzca un desenlace en segundos.

## 2.4. No existen puntos de vida

Las naves no tienen HP.

Un impacto afecta físicamente a estructura, blindaje, compartimentos, tripulación y sistemas. Un impacto directo de un arma antinave suele ser suficiente para producir un mission kill o destruir la nave, independientemente de que sea grande o pequeña.

El blindaje sirve principalmente para resistir armas ligeras, fragmentación, impactos parciales y daño secundario. No convierte una nave en un damage sponge.

## 2.5. Las naves son conceptualmente submarinos

La supervivencia depende principalmente de:

1. no ser detectado;
2. no proporcionar una buena solución de tiro;
3. detectar amenazas a tiempo;
4. romper la solución del atacante;
5. interceptar o confundir las armas entrantes;
6. evitar situaciones desfavorables.

---

# 3. Control de flota

El jugador controla directamente una nave.

Las naves aliadas adicionales reciben órdenes de alto nivel, por ejemplo:

- mantener formación;
- mantener distancia;
- proteger una nave;
- cubrir un sector;
- mantener silencio electrónico;
- explorar;
- patrullar;
- atacar un eco o una zona;
- defender contra misiles;
- retirarse;
- desplazarse a una posición.

La calidad de oficiales y tripulación influirá en la ejecución de estas órdenes.

El objetivo es evitar que el juego se convierta en un RTS de micromanagement.

---

# 4. Filosofía de diseño de naves y componentes

## 4.1. No existen naves perfectas

Ninguna nave debe maximizar simultáneamente sensores, armas, defensas, movilidad, sigilo y autonomía.

Una nave moderna puede disponer de componentes excelentes, pero cada capacidad potente impone costes que fuerzan sacrificios en otras áreas.

## 4.2. No existen componentes perfectos

Ningún componente debe puntuar al máximo en todas sus prestaciones funcionales.

Puede haber componentes objetivamente mejores que otros gracias a tecnología superior, pero incluso estos deben conservar una frontera de eficiencia y algún compromiso.

## 4.3. Huella energética como trade-off por defecto

La huella energética es el coste sistémico principal asociado a componentes de alto rendimiento.

Como regla general:

> Cuanto más capaz es un sistema, mayor Huella energética tiene.

La **Huella energética** es también la medida de la energía que consume el dispositivo. No existe una estadística separada de consumo eléctrico para cada componente.

Esto tiene dos efectos simultáneos:

- exige más capacidad de generación eléctrica;
- hace la nave más fácil de detectar mediante sensores energéticos.

Los sistemas de prestaciones extremas deben experimentar un crecimiento no lineal de consumo y huella energética. Las últimas mejoras de rendimiento deben resultar especialmente caras.

## 4.4. Generación eléctrica como límite emergente

Los sistemas potentes requieren generadores más grandes o numerosos.

Los generadores ocupan espacio que no puede utilizarse para otros sistemas y contribuyen también a la huella energética de la nave.

Por tanto, gran parte de las limitaciones de diseño deben emerger de:

- espacio disponible;
- demanda eléctrica;
- generación necesaria;
- firma física;
- huella energética.

Se deben evitar límites arbitrarios cuando el propio modelo físico pueda producir la restricción.

## 4.5. Tamaño y vulnerabilidad

Una nave más grande puede llevar más sistemas, armas y defensas, pero su tamaño incrementa la firma física y normalmente también la huella energética.

En Hullbreach una nave grande no es necesariamente más peligrosa ni más difícil de destruir.

Una nave muy grande sería extremadamente fácil de detectar, seguir y atacar. Dado que ninguna defensa puede detener indefinidamente todos los ataques y un impacto directo suele resultar catastrófico, el gigantismo naval es una mala doctrina.

El lore no contempla superacorazados espaciales. Las naves grandes, cuando existen, dependen de escoltas para sobrevivir, de forma análoga a las grandes unidades navales modernas.

## 4.6. Nave defensiva de escolta

El equivalente funcional a un 'tanque' no es una nave que soporte impactos.

Puede ser una nave pequeña con:

- firma baja;
- buenos sensores pasivos;
- gran capacidad antimisil;
- defensa puntual;
- capacidad ofensiva pobre;
- sensores activos limitados.

Su función es interceptar muchas amenazas y proteger a otras naves mientras resulta difícil de localizar y destruir.

Si recibe un impacto directo importante, probablemente queda fuera de combate como cualquier otra nave.

---

# 5. Información real e información conocida

Cada objeto posee un estado físico real:

- posición;
- velocidad;
- orientación;
- aceleración;
- firma;
- huella energética;
- sistemas activos;
- daños;
- identidad;
- armamento.

El jugador no conoce automáticamente ese estado.

Los sensores producen mediciones imperfectas. La interfaz nunca debe revelar información que la nave del jugador no haya obtenido.

---

# 6. Firmas de una nave

## 6.1. Firma física

La firma representa lo fácil que resulta detectar físicamente una nave.

Depende principalmente de:

- diseño y tamaño del casco;
- características stealth del diseño;
- estado del motor principal;
- estela de propelente generada durante aceleración o desaceleración.

La velocidad absoluta de la nave no aumenta por sí misma la firma.

Cuando el motor principal acelera o desacelera la nave, expulsa propelente y genera una larga estela detectable que incrementa fuertemente la firma física.

Cuando el motor deja de emitir propelente, esa contribución desaparece y la firma vuelve hacia su nivel base, independientemente de que la nave continúe desplazándose a gran velocidad.

En el espacio no es necesario mantener el motor encendido para conservar velocidad. Una nave puede:

1. encender motores;
2. acelerar intensamente, aumentando mucho su firma durante la maniobra;
3. apagar motores;
4. continuar desplazándose por inercia a gran velocidad con una firma física mucho menor.

Las naves pueden tener una firma base anormalmente alta o baja.

## 6.2. Huella energética

La huella energética representa la energía detectable emitida por la nave.

Depende principalmente de los sistemas activos y de la generación necesaria para alimentarlos.

Contribuyen, entre otros:

- sensores activos;
- motores;
- armas;
- defensas;
- guerra electrónica;
- comunicaciones;
- soporte vital;
- generadores;
- sistemas auxiliares.

La tripulación puede reducir drásticamente esta huella apagando sistemas y reduciendo actividad.

Por tanto:

- la firma es más difícil de reducir voluntariamente;
- la energía puede reducirse mucho, pero exige renunciar temporalmente a capacidades.

---

# 7. Sensores: principios generales

Una nave no tiene por qué llevar simultáneamente todos los tipos de sensores.

Puede:

- tener solo sensores de firma;
- tener solo sensores energéticos;
- tener ambos;
- carecer de sensores activos;
- tener sensores pasivos sin activos;
- carecer de sensores pasivos;
- tener uno o varios tipos de sensores pasivos;
- combinar sensores de diferente calidad.

Esto forma parte de la especialización de la nave.

---

# 8. Sensores activos

## 8.1. Arco de efecto

Los sensores activos están orientados principalmente hacia el morro.

Su eficacia:

- es máxima hacia delante;
- cae rápidamente al aumentar el ángulo respecto al morro;
- es baja hacia los laterales;
- es prácticamente nula arriba y abajo;
- es nula o casi nula detrás.

La orientación de la nave es por tanto parte directa del minijuego de detección.

## 8.2. Franjas de distancia

Cada barrido activo debe ejecutarse sobre una franja de distancia seleccionada.

No se introduce manualmente una distancia exacta.

Se prevé utilizar aproximadamente cuatro bandas de distancia predeterminadas, aunque sus valores y nombres definitivos se diseñarán más adelante junto con la interfaz.

Las bandas representan capas del espacio con límites estrictos y sin solapamiento. Por ejemplo, de forma puramente ilustrativa:

- corta: 0-50.000 km;
- media: 50.001-150.000 km;
- larga: siguiente intervalo;
- extrema: intervalo más lejano.

Elegir una banda incorrecta hace que el sensor no detecte un objeto situado fuera de ella.

La sensibilidad efectiva se degrada con la distancia. Las bandas más lejanas aplican penalizaciones crecientes a la sensibilidad del sensor. Un sensor de sensibilidad baja puede resultar completamente inútil a partir de cierta banda sin necesidad de una regla especial por tipo de sensor.

La distancia también degrada la Precisión. Incluso cuando un objetivo sigue superando el umbral de detección, un eco obtenido a mayor distancia tendrá normalmente un error posicional mayor que uno obtenido a corta distancia en las mismas condiciones.

## 8.3. Barridos discretos y retardo de propagación

Un sensor activo no proporciona un flujo continuo de posiciones.

Cada uso ordena un barrido discreto y genera cero o más ecos.

El barrido en sí es instantáneo cuando ocurre, pero no ocurre en el mismo momento en que el jugador pulsa el botón. Existe un retardo antes de que el barrido alcance la franja seleccionada y ese retardo aumenta con la distancia.

La detección se calcula respecto al estado real del objetivo en el momento en que el barrido ocurre efectivamente, no respecto a su posición cuando el jugador dio la orden.

La orientación debe mantenerse de forma válida hasta que el barrido se ejecute. Si la nave modifica suficientemente su orientación antes de ese momento, el barrido deja de ser válido o se pierde.

Cada barrido es una observación valiosa.

## 8.4. Detección determinista

La detección es determinista.

Dadas exactamente las mismas condiciones, un objeto será detectado o no detectado siempre del mismo modo.

Conceptualmente, la capacidad de detección depende de:

- sensibilidad del sensor;
- detectabilidad del objetivo para ese tipo de sensor;
- ángulo;
- distancia;
- entorno.

Si se supera el umbral de detección se genera un eco.

El azar no decide si existe detección.

## 8.5. Error de medición

Cuando existe detección, el sensor no devuelve la posición real.

Devuelve una posición medida desviada mediante un vector aleatorio tridimensional.

La magnitud máxima del error depende de varios factores:

- precisión base del sensor;
- holgura con la que se ha superado el umbral de detección;
- distancia;
- ángulo;
- características stealth del objetivo;
- correspondencia entre sensor y objetivo;
- condiciones ambientales que afecten a precisión.

La holgura de detección es solo uno de esos factores.

## 8.6. Sensibilidad y precisión son estadísticas independientes

Un sensor activo tiene al menos dos prestaciones principales:

- Sensibilidad: capacidad para conseguir una detección;
- Precisión: capacidad para producir una posición medida próxima a la real.

Ningún sensor puede maximizar ambas.

Alcanzar el máximo en una limita el valor potencial de la otra.

Ejemplo conceptual permitido:

- Sensibilidad 10;
- Precisión 7;
- Huella energética 250.

Ejemplo conceptual no permitido:

- Sensibilidad 10;
- Precisión 10;
- Huella energética mínima.

## 8.7. Curva energética no lineal

Cuanto mayores sean sensibilidad y precisión, mayor será el consumo y la huella energética.

El crecimiento debe acelerarse al acercarse a prestaciones extremas.

Ejemplo puramente ilustrativo de una nave:

- sensor avanzado: huella 250;
- soporte vital: 10;
- motores: 45;
- defensas: 20;
- armas ofensivas: 30.

En esta configuración el sensor domina la huella energética de toda la nave y puede delatarla a gran distancia.

Un sensor discreto podría ser:

- Sensibilidad 3;
- Precisión 4;
- Huella energética 45.

Puede requerir más tiempo y mejores condiciones para localizar un blanco, pero permite operar con mucha mayor discreción.

## 8.8. Tecnología superior

La tecnología avanzada puede desplazar la frontera de eficiencia:

- mismas prestaciones con menor huella;
- mejores prestaciones con una huella equivalente.

Pero nunca elimina la frontera ni permite maximizar todas las características.

## 8.9. Instalación y uso de sensores activos

Una nave puede instalar como máximo dos sensores activos.

Puede instalar dos sensores del mismo tipo o de tipos distintos, siempre que el diseño de la nave tenga capacidad para ello.

Solo puede utilizarse un sensor activo a la vez. No se permiten barridos simultáneos con dos sensores.

Una nave con dos sensores puede, por ejemplo, combinar:

- un sensor muy sensible pero impreciso;
- un sensor menos sensible pero mucho más preciso;

o bien:

- un sensor de firma;
- un sensor energético.

La elección de cuál utilizar en cada momento forma parte del gameplay.

## 8.10. Huella energética durante el uso

Por defecto, la huella energética de cualquier dispositivo existe de forma permanente mientras el dispositivo está activo, no únicamente durante el instante en que realiza una acción.

Por tanto, un sensor activo contribuye a la huella energética de la nave durante todo el tiempo que permanece encendido.

Algunos componentes concretos pueden romper esta regla y tener una huella reducida mientras están armados o preparados y una huella mucho mayor únicamente al utilizarse. Esta será una propiedad específica del componente y no una característica general de los sensores.

No se prevé por ahora permitir al jugador seleccionar manualmente niveles de potencia de barrido.

---

# 9. Tipos de sensores activos

Como mínimo existirán dos familias funcionalmente diferentes.

## 9.1. Sensor de firma

Busca la firma física del objetivo.

Características generales:

- especialmente eficaz a distancias medias y cortas;
- más difícil de evadir cuando el objetivo está suficientemente cerca;
- el objetivo puede reducir su firma principalmente apagando el motor principal y dejando de emitir propelente;
- se ve muy afectado por el entorno.

## 9.2. Sensor energético

Busca la huella energética del objetivo.

Características generales:

- suele ser más útil a grandes distancias;
- permite detectar sistemas de gran potencia desde lejos;
- el objetivo puede reducir drásticamente su detectabilidad apagando sistemas;
- depende mucho del estado operativo de la nave;
- en general el entorno lo perjudica menos que a la detección por firma, salvo fuentes de energía muy intensas.

---

# 10. Ecos y seguimiento

## 10.1. Un barrido produce ecos, no contactos identificados

Si un barrido detecta dos naves, aparecen dos ecos.

El juego no asigna automáticamente un identificador persistente que revele qué eco de un nuevo barrido corresponde a qué objeto de un barrido anterior.

El jugador debe interpretar la secuencia de observaciones.

## 10.2. Identificación progresiva

Cada eco contribuye no solo a estimar una posición, sino también a identificar qué clase de objeto está siendo observado.

La identificación progresa por niveles de conocimiento:

1. **Objeto:** se sabe únicamente que existe algo.
2. **Categoría general:** nave, estación u otro tipo general de objeto.
3. **Tipo funcional:** escolta, crucero, mercante u otra categoría equivalente.
4. **Modelo o clase exacta:** identificación completa del objeto observado.

Cada nuevo eco compatible aumenta un porcentaje de certeza de identificación.

La certeza puede ser errónea durante las fases intermedias. Por ejemplo, un objeto puede ser clasificado provisionalmente como mercante y, tras obtener nuevos ecos, pasar a ser considerado una corbeta.

Al alcanzar el 100 % se conoce el modelo o clase exacta con certeza.

La identificación adquirida no se degrada con el tiempo. Una vez identificado un modelo exacto, futuras detecciones de ese mismo objeto conservan esa información cuando el sistema puede asociarlas de manera válida al historial conocido.

La identificación y la precisión posicional son independientes. Un objeto puede estar perfectamente identificado y, al mismo tiempo, tener una posición muy imprecisa.

## 10.3. Identificación y precisión del sensor

La velocidad y fiabilidad del progreso de identificación dependen principalmente de la **Precisión** del sensor.

No existe una estadística separada de identificación.

Los sensores de firma no tienen penalización base de identificación.

Los sensores energéticos aplican una penalización base al progreso de identificación, por lo que en igualdad de precisión necesitan más ecos para alcanzar el mismo nivel de certeza.

Las condiciones que degradan la precisión degradan también la identificación. Esto incluye:

- distancia;
- geometría desfavorable;
- entorno;
- Jammer;
- otras interferencias que afecten a precisión.

## 10.4. Ambigüedad entre naves similares

La identificación de clase no implica identidad individual.

Si tres naves idénticas viajan juntas y se alcanza el 100 % de identificación, el jugador puede saber que los tres objetos son, por ejemplo, corbetas de una clase concreta, pero no necesariamente qué eco de un barrido corresponde a qué nave concreta del barrido anterior.

Si dos naves similares viajan juntas, los ecos de distintos barridos pueden cruzarse y hacer imposible mantener una asociación individual estable.

Viajar en convoy puede utilizarse deliberadamente para dificultar el seguimiento de unidades concretas.

Cambiar de sensor puede ayudar cuando las naves difieren en características que el otro tipo de sensor puede distinguir, pero solo puede utilizarse un sensor activo a la vez.

## 10.5. Nube estadística

Si un objeto permaneciera inmóvil y se realizasen muchísimos barridos, los ecos tenderían a formar una nube aproximadamente esférica alrededor de la posición real.

La posición real estaría aproximadamente en el centro estadístico de la nube, pero el jugador normalmente no dispone del tiempo suficiente para acumular tantas observaciones.

Debe estimar la posición con pocas detecciones.

## 10.6. Movimiento aparente lento

Las escalas espaciales son grandes.

Aunque una nave se desplace a gran velocidad física, su movimiento angular desde el punto de vista del jugador puede ser lento.

En varios barridos próximos, los ecos tenderán a formar una nube que deriva gradualmente, no una trayectoria que cruza rápidamente la pantalla.

Esto permite obtener una estimación de posición antes de disponer de una buena estimación de movimiento.

## 10.7. Ecos antiguos

Las observaciones anteriores permanecen visibles durante un tiempo y se degradan visualmente, por ejemplo mediante transparencia.

El jugador puede comparar grupos de ecos separados temporalmente para estimar deriva, dirección y velocidad relativa.

Si un nuevo barrido no detecta nada, el jugador recibe simplemente ausencia de ecos. El juego no indica si la zona estaba realmente vacía o si existían objetos por debajo del umbral de detección.

Los ecos antiguos se conservan de acuerdo con las reglas visuales correspondientes; el juego no mantiene un marcador actualizado de un objeto que ya no está siendo detectado.

Un mismo barrido devuelve todos los objetos del volumen explorado que superen individualmente el umbral de detección. No existe un límite artificial de contactos por barrido.

---

# 11. Sensores pasivos

Existen al menos dos familias de sensores pasivos con funciones diferentes:

- sensores defensivos;
- sensores pasivos direccionales.

Los sensores defensivos y los sensores pasivos direccionales detectan energía.

Ninguno necesita emitir un barrido activo para funcionar.

La detección pasiva es determinista: dadas exactamente las mismas condiciones, un objetivo se detecta o no se detecta siempre del mismo modo.

## 11.1. Sensores defensivos

Los sensores defensivos son el tipo de sensor pasivo más común y normalmente permanecen encendidos durante toda la operación de la nave.

Funcionan continuamente mientras están activos; el jugador no ejecuta barridos manuales.

Su función principal es detectar misiles que se aproximan, marcarlos y habilitar el uso de las contramedidas que requieran una amenaza detectada.

La mayoría de las contramedidas necesitan sensores defensivos para poder emplearse contra un misil.

### 11.1.1. Características

Los sensores defensivos tienen tres características principales:

- **Sensibilidad:** capacidad para detectar objetos próximos por su huella energética.
- **Precisión:** capacidad para localizar con exactitud el objeto detectado.
- **Huella energética:** energía consumida por el sensor y contribución del dispositivo a la huella energética total mientras permanece activo.

Su Precisión suele ser muy alta porque su función principal exige localizar con exactitud misiles rápidos y cercanos.

Una vez que detectan y localizan un misil con calidad suficiente, habilitan las contramedidas compatibles. El resultado posterior depende de la contramedida empleada, no de una tirada abstracta del sensor defensivo.

La distancia afecta tanto a la Sensibilidad como a la Precisión del sensor defensivo, igual que ocurre con los demás sensores.

### 11.1.2. Cobertura e interferencia propia

Son omnidireccionales en principio, pero determinados sistemas de la propia nave crean sectores completamente ciegos.

#### Motor principal

Mientras el motor principal está funcionando:

- el sector trasero queda completamente ciego para el sensor defensivo;
- las amenazas que llegan desde detrás no pueden ser detectadas por él.

El motor debe apagarse para eliminar esta interferencia.

Esto no obliga a detener la nave: en el espacio continúa moviéndose por inercia. El motor principal se necesita para acelerar o desacelerar, no para mantener velocidad.

#### Sensores activos

Mientras un sensor activo está funcionando:

- el sector delantero queda completamente ciego para el sensor defensivo;
- las amenazas que llegan desde delante no pueden ser detectadas por él.

Para recuperar la cobertura frontal hay que apagar el sensor activo.

Esto introduce una decisión táctica importante: cuando una salva de misiles llega por delante, la nave no puede mantener simultáneamente una búsqueda activa frontal y confiar en sus sensores defensivos para marcar esos misiles. Debe interrumpir la búsqueda activa hasta que la amenaza haya sido resuelta.

#### Propulsores de maniobra

Los propulsores laterales o de maniobra también producen interferencia, pero mucho menor.

Funcionan con un consumo energético reducido y principalmente con propelente, por lo que normalmente no generan una ceguera comparable a la del motor principal.

### 11.1.3. Alcance y blancos detectables

Su alcance es reducido.

Están pensados principalmente para detectar misiles cuando ya se encuentran relativamente cerca. La Sensibilidad determina cuánto margen de reacción obtiene la nave antes del impacto y la Precisión determina la calidad de la localización.

Sin embargo, no están limitados artificialmente a misiles.

También pueden detectar y localizar:

- naves;
- estaciones;
- otros objetos;

si estos se encuentran dentro de su corto alcance y superan el umbral de detección energética.

Normalmente las naves enemigas no se aproximarán tanto, por lo que su uso principal sigue siendo defensivo. Pero una nave que entre en la burbuja de detección de un sensor defensivo puede ser localizada aunque la nave observadora carezca de sensores de búsqueda activos.

Una nave con mejores sensores defensivos puede marcar una amenaza antes y mantener disponibles más capas de contramedidas.

### 11.1.4. Identificación

Los objetos detectados por sensores defensivos participan en un proceso de identificación progresiva.

En el caso de un misil, mientras el sensor defensivo mantiene la detección aumenta con el tiempo un porcentaje de identificación hasta alcanzar el 100 %.

Antes del 100 % la clasificación puede ser incompleta o incorrecta.

Al alcanzar el 100 % se conoce exactamente el modelo de misil.

Las naves y otros objetos detectados a corto alcance siguen igualmente las reglas generales de identificación progresiva de los sensores energéticos.

La detección y la identificación son independientes de la efectividad posterior de las armas o contramedidas.

### 11.1.5. Detección de emisiones activas enemigas

Los sensores defensivos también pueden detectar que una emisión de sensor activo enemigo está alcanzando o buscando la zona donde se encuentra la nave.

Esto incluye los seekers activos de misiles y torpedos.

Pueden distinguir si se trata de:

- un sensor de firma;
- un sensor energético.

Cuando la emisión corresponde a un seeker que está iluminando o buscando la propia nave, puede generarse una alerta de emergencia de targeting.

Esta alerta no proporciona por sí sola una solución contra el arma:

- no localiza su posición;
- no proporciona bearing;
- no genera un eco posicional;
- no permite disparar una contramedida hasta que el misil o torpedo sea detectado y localizado con suficiente calidad.

## 11.2. Sensores pasivos direccionales

Los sensores pasivos direccionales son menos frecuentes y solo aparecen en determinadas naves o configuraciones.

Funcionan continuamente mientras están encendidos. El jugador no ordena un barrido: debe orientar físicamente la nave hacia la zona que quiere observar.

Su función es localizar objetivos a partir de su huella energética sin emitir una señal activa de búsqueda.

Su principal ventaja es la discreción:

- no revelan la presencia de la nave mediante un barrido;
- su propia huella energética suele ser mucho menor que la de un sensor activo equivalente.

A cambio tienen limitaciones severas.

### 11.2.1. Interfaz y uso

Su interfaz es más simple que la de un sensor activo:

- no se elige tipo de detección: siempre detectan energía;
- no se selecciona banda de alcance: solo trabajan a corta distancia;
- no se ordena un barrido: funcionan continuamente mientras están encendidos.

La acción principal del jugador consiste en orientar correctamente la nave y mantener unas condiciones suficientemente silenciosas.

### 11.2.2. Direccionalidad

Están orientados hacia el morro de la nave.

Son mucho más sensibles a la orientación que los sensores activos.

La nave debe estar casi perfectamente orientada hacia el objetivo para detectarlo. Pequeñas desviaciones angulares reducen fuertemente la sensibilidad efectiva y pueden impedir completamente la detección.

### 11.2.3. Interferencia de la propia nave

La firma física y la huella energética de la propia nave penalizan permanentemente la Sensibilidad efectiva del sensor pasivo direccional.

La penalización crece de forma exponencial.

Consecuencias:

- una nave con firma media o grande llega rápidamente a un punto en el que el sensor resulta prácticamente inútil;
- estos sensores están pensados principalmente para naves de caza extremadamente discretas, equivalentes doctrinalmente a submarinos;
- incluso una nave pequeña y stealth debe apagar casi todos sus sistemas para utilizarlos correctamente;
- cualquier sistema activo que aumente la huella energética reduce su capacidad de detección;
- cualquier condición que aumente la firma física también reduce su capacidad de detección.

Motores, sensores activos, armas, defensas, comunicaciones y otros sistemas pueden degradar el sensor simplemente por aumentar la huella energética total de la nave.

Otros sensores pasivos pueden permanecer encendidos al mismo tiempo. No interfieren por ser sensores, sino únicamente por la huella energética adicional que generan.

### 11.2.4. Propulsión y firma

Cualquier factor que aumente la firma física propia perjudica al sensor pasivo direccional.

La velocidad absoluta no penaliza el sensor por sí misma.

Lo que perjudica fuertemente al sensor es utilizar el motor principal para acelerar o desacelerar, porque la estela de propelente aumenta la firma física de la propia nave.

Por tanto, una nave que quiera utilizar este sensor eficazmente tenderá a:

- mantener una firma base muy baja;
- apagar el motor principal;
- reducir sistemas activos;
- desplazarse principalmente por inercia.

Una nave puede moverse muy rápido y seguir utilizando eficazmente un sensor pasivo direccional si alcanzó esa velocidad antes, apagó el motor y su firma restante es suficientemente baja.

### 11.2.5. Alcance y sensibilidad

Tienen muy poco alcance.

Solo detectan objetivos dentro de la banda corta y, aun dentro de ella, su Sensibilidad no suele ser alta.

No sustituyen a los sensores activos como sistema general de búsqueda.

Su utilidad consiste en permitir una búsqueda silenciosa de corto alcance a una nave específicamente diseñada y operada para ello.

### 11.2.6. Características

Un sensor pasivo direccional tiene:

- **Sensibilidad**;
- **Precisión**;
- **Huella energética**.

La Sensibilidad y la Huella energética suelen ser bajas.

En cuanto a detección, precisión e identificación, funcionan como un sensor activo energético salvo por sus reglas específicas de pasividad, alcance, orientación e interferencia propia.

### 11.2.7. Ecos e identificación

Cuando detectan un objetivo generan un eco posicional siguiendo las mismas reglas generales que un sensor activo:

- posición real;
- desviación determinada por Precisión y condiciones;
- identificación progresiva;
- posibilidad de clasificación provisional errónea.

La identificación sigue la lógica de los sensores energéticos y aplica su penalización base frente a los sensores de firma.

### 11.2.8. Entorno

Hereda los modificadores ambientales de la detección energética.

Por tanto:

- el polvo puede reducir su capacidad de detección;
- las fuentes energéticas intensas pueden enmascarar blancos;
- una estrella de fondo puede resultar especialmente perjudicial;
- cualquier condición ambiental que degrade detección o precisión energética afecta también al sensor pasivo direccional.

### 11.2.9. Jammer

Los sensores pasivos no detectan un Jammer por el mero hecho de que esté funcionando.

La detección de la fuente de un Jammer requiere sensores activos.

Sin embargo, un sensor pasivo direccional que intente observar un objeto situado dentro del área de efecto de un Jammer sí sufre la interferencia correspondiente a un sensor energético.

Esto incluye al propio sensor de la nave emisora: si está dentro del campo de interferencia de su Jammer, su capacidad de localizar objetivos energéticos queda degradada.

### 11.2.10. Instalación

No existe un límite global específico de sensores pasivos.

Cada casco determina cuántos slots de sensores puede montar.

Técnicamente una nave puede instalar varios sensores pasivos direccionales si dispone de slots suficientes, aunque normalmente no resulta útil montar más de uno.

Una configuración habitual puede combinar:

- un sensor activo;
- un sensor pasivo direccional;
- sensores defensivos.

## 11.3. Principio doctrinal

Los sensores pasivos no forman una burbuja perfecta de conocimiento.

Los sensores defensivos:

- proporcionan alerta antimisil;
- localizan amenazas con Precisión normalmente muy alta;
- permiten utilizar contramedidas;
- identifican progresivamente misiles;
- pueden detectar y localizar naves u otros objetos si entran dentro de su corto alcance;
- detectan barridos activos enemigos sin localizar su origen;
- pueden quedar ciegos por la actividad de la propia nave.

Los sensores pasivos direccionales:

- permiten localizar objetivos sin emitir;
- requieren orientación casi perfecta;
- funcionan solo a corta distancia;
- sufren una penalización exponencial por la firma y huella de la propia nave;
- están pensados principalmente para naves pequeñas y muy stealth.

Esto preserva la posibilidad de aproximaciones no detectadas y refuerza el paradigma de combate similar al de submarinos.

---

# 12. Jammer e interferencia de sensores

El Jammer es una contramedida electrónica destinada a degradar la precisión de sensores y seekers dentro de una zona del espacio.

Su principio fundamental es crear una **zona volumétrica de interferencia** centrada en la nave que lo emite.

## 12.1. Características

Un Jammer tiene tres características principales:

- **Interference:** intensidad con la que degrada la calidad de las mediciones afectadas.
- **Energy footprint:** energía consumida por el dispositivo y contribución a la huella energética total de la nave mientras está activo.
- **Area of effect:** volumen alrededor de la nave emisora cubierto por la interferencia.

La potencia del Jammer es fija. No existen modos de potencia baja, media o alta.

No tiene sentido activar deliberadamente un Jammer a potencia reducida: cuando se utiliza se pretende obtener toda su capacidad de interferencia.

## 12.2. Área de efecto

El Jammer es omnidireccional.

Su interferencia cubre un volumen alrededor de la nave emisora.

La intensidad de la interferencia no depende de la distancia entre el sensor observador y el Jammer. Lo relevante es si el objeto que se intenta observar se encuentra dentro o fuera del área de efecto.

Todo objeto situado dentro de esa zona resulta más difícil de localizar con los sensores afectados.

Esto incluye:

- la propia nave emisora;
- naves aliadas;
- naves enemigas;
- señuelos;
- otros objetos que puedan ser observados mediante sensores afectados.

El Jammer no distingue amigo de enemigo.

Una nave de guerra electrónica puede por tanto proteger a otras naves cercanas manteniéndolas dentro de su campo de interferencia.

Una nave enemiga que entre en la misma zona obtiene también el beneficio de la interferencia, aunque a esas distancias el combate puede haber pasado ya al alcance de sensores y armas defensivas.

## 12.3. Solapamiento de varios Jammers

Las áreas de varios Jammers pueden solaparse.

Las intensidades no se acumulan.

Un objeto situado simultáneamente dentro de varios campos de Jammer no recibe una suma de todas las penalizaciones. Se aplica la interferencia correspondiente según las reglas de resolución que se definan para dispositivos solapados.

Esto evita que una formación multiplique indefinidamente la distorsión acumulando Jammers.

## 12.4. Efecto sobre sensores energéticos

Los sensores energéticos son los más afectados.

La enorme huella energética de la nave que utiliza el Jammer hace que un sensor activo energético pueda detectar fácilmente su presencia, pero el campo de interferencia dificulta enormemente determinar una posición precisa para cualquier objeto cubierto.

Por tanto, dentro del área:

- la Precisión energética sufre una penalización muy alta;
- el progreso futuro de identificación energética se ralentiza fuertemente;
- construir una solución de tiro precisa resulta mucho más difícil.

La identificación ya obtenida no disminuye. Si un objeto ya estaba identificado al 100 %, seguirá identificado al 100 %.

## 12.5. Efecto sobre sensores de firma

Los sensores de firma también sufren interferencia, pero en menor medida.

Dentro del área del Jammer:

- la Precisión de firma recibe una penalización moderada;
- el progreso futuro de identificación se ralentiza de forma moderada.

La información de identificación ya conseguida tampoco disminuye.

Cambiar a un sensor de firma puede ser una respuesta táctica válida contra una nave protegida por Jammer.

## 12.6. Sensores defensivos

Los sensores defensivos son energéticos y, por tanto, se ven fuertemente afectados por el Jammer.

Mientras una nave mantiene activo su propio Jammer:

- la Precisión de sus sensores defensivos queda muy degradada;
- la identificación de amenazas progresa mucho peor;
- puede resultar incapaz de localizar con calidad suficiente un misil entrante para habilitar sus contramedidas.

Esto crea una decisión táctica deliberada.

El Jammer puede impedir que un seeker enemigo consiga una solución precisa, pero si el misil consigue atravesar la interferencia y aproximarse a la nave, el jugador debe advertir la situación y apagar el Jammer a tiempo para recuperar la capacidad normal de los sensores defensivos.

Un Jammer mal utilizado puede por tanto convertirse en una calamidad defensiva: protege contra la adquisición enemiga pero puede cegar la capa de sensores necesaria para disparar interceptores, láseres o defensas cinéticas.

Una vez apagado el Jammer, su interferencia desaparece inmediatamente y los sensores defensivos recuperan su funcionamiento normal, sujeto a sus demás limitaciones de alcance y sectores ciegos.

## 12.7. Sensores pasivos

Los sensores pasivos no detectan la existencia de un Jammer por su emisión.

En particular:

- un sensor defensivo no genera una alerta de Jammer;
- un sensor pasivo direccional no localiza automáticamente la fuente del Jammer.

La fuente debe ser detectada mediante sensores activos.

Aunque no puedan localizar la fuente del Jammer, ambos tipos de sensores pasivos energéticos sufren su interferencia cuando intentan observar objetos situados dentro del área de efecto.

## 12.8. Efecto sobre seekers

Interferir seekers de misiles es una de las funciones principales del Jammer.

Un seeker se considera un sensor instalado en el misil y tendrá, entre otras propiedades:

- Sensibilidad;
- Precisión;
- familia de detección, como energía o firma.

Cuando un seeker activo intenta localizar un blanco dentro del área de un Jammer, recibe la penalización correspondiente a su familia.

Un Jammer puede degradar suficientemente la Precisión de un seeker como para hacerle perder un lock ya adquirido y obligarlo a volver a buscar.

No existe una tirada abstracta de "jamming success". El fallo surge de la degradación normal de las propiedades del sensor.

El diseño detallado de seekers se resolverá en el apartado de misiles.

## 12.9. Activación y desactivación

Como el resto de dispositivos, un Jammer necesita un tiempo de activación entre la orden de encendido y el momento en que comienza a funcionar.

Se contempla añadir una característica general de dispositivo para representar este **activation delay**, ya que puede ser importante también en otros sistemas.

Una vez completado el arranque, el Jammer aplica inmediatamente su interferencia a toda su área de efecto.

Al apagarlo, la interferencia desaparece inmediatamente.

## 12.10. Ecos e información previa

El Jammer no modifica retroactivamente información ya obtenida.

Los ecos anteriores:

- permanecen donde estaban;
- conservan la precisión que tenían;
- conservan la identificación acumulada.

Si el enemigo ya había localizado con gran precisión una nave antes de que esta activase el Jammer, activar el dispositivo no borra esa información.

En ese caso el Jammer pierde gran parte de su utilidad para impedir la localización inicial, aunque sigue siendo útil contra nuevas mediciones y especialmente contra seekers de misiles entrantes.

## 12.11. Relación con señuelos

Un señuelo situado dentro del área de un Jammer también se beneficia de la interferencia y resulta más difícil de localizar e identificar correctamente.

Sin embargo, normalmente un señuelo se utiliza lejos de la nave que lo lanzó precisamente para desviar la atención hacia otra zona, por lo que esta sinergia no siempre será fácil de aprovechar.

## 12.12. Entorno

Los efectos ambientales y el Jammer se aplican conjuntamente.

Un entorno que ya perjudique la Precisión de un sensor puede combinarse con el campo del Jammer y producir una solución todavía peor.

Ejemplos:

- una estrella de fondo junto con Jammer perjudica especialmente a sensores energéticos;
- polvo u otros entornos que degraden Precisión pueden combinarse con la interferencia.

## 12.13. Coste táctico

Activar un Jammer implica aceptar una Huella energética muy alta.

No sirve para permanecer oculto frente a sensores activos energéticos.

Su uso intercambia discreción por protección:

- hace más difícil obtener nuevas soluciones precisas sobre los objetos protegidos;
- protege seekers y ataques entrantes mediante degradación de sus sensores;
- perjudica también a los sensores propios afectados, incluidos los sensores defensivos;
- puede obligar al jugador a apagarlo cuando un misil entrante se aproxima para recuperar la defensa terminal;
- puede proteger simultáneamente a varias naves;
- también puede proteger accidentalmente a enemigos situados dentro del área.

## 12.14. Diseño pendiente

Queda por concretar:

- valores concretos de Interference;
- valores concretos de Energy footprint;
- tamaños concretos de Area of effect;
- fórmula exacta de penalización sobre Precisión;
- efecto exacto sobre progreso de identificación;
- regla de prioridad cuando se solapan Jammers de distinta potencia;
- tiempos concretos de activación;
- interacción detallada con los distintos seekers de misiles.

---

# 13. Entorno y detección

El entorno es una parte estratégica del combate. Las rutas de aproximación y las posiciones relativas respecto a cuerpos celestes y fenómenos ambientales deben importar.

Los principales elementos ambientales previstos son:

- cuerpos celestes: planetas, estrellas, lunas, asteroides;
- polvo y nebulosas;
- fuentes de energía, principalmente estrellas.

Se distinguen dos mecanismos:

- ocultación: un objeto se encuentra físicamente entre sensor y objetivo;
- enmascaramiento: el objetivo se encuentra delante de un fondo que dificulta distinguirlo.

## 13.1. Cuerpos celestes y firma

Si una nave se encuentra delante de un cuerpo celeste desde el punto de vista del sensor, la detección por firma empeora.

El efecto aumenta con la importancia del cuerpo como fondo; cuerpos más masivos o visualmente dominantes producen mayor enmascaramiento.

Si la nave se encuentra al otro lado del cuerpo celeste, la detección de firma queda completamente bloqueada.

Un planeta, luna o asteroide grande puede por tanto proporcionar cobertura real contra sensores de firma.

## 13.2. Cuerpos celestes y energía

Si una nave se encuentra detrás de un cuerpo celeste, la detección energética también se reduce.

El bloqueo energético no tiene por qué ser idéntico al bloqueo de firma y queda sujeto al tipo concreto de sensor.

## 13.3. Polvo y nebulosas

El polvo degrada todos los métodos de detección.

Afecta más a la detección de firma que a la energética.

Una nebulosa se modela como una gran región con polvo, no como una excepción completamente diferente.

Pueden existir nubes de polvo localizadas fuera de nebulosas.

El polvo puede afectar tanto a capacidad de detección como a precisión.

## 13.4. Estrellas y huella energética

Las estrellas enmascaran fuertemente la huella energética.

Este efecto existe tanto si la nave está delante de la estrella como si está detrás de ella desde el punto de vista del sensor.

La enorme fuente energética de fondo dificulta separar la emisión de la nave.

## 13.5. Detección y precisión ambiental independientes

El entorno puede afectar por separado a:

- capacidad de detección de firma;
- precisión de firma;
- capacidad de detección energética;
- precisión energética.

Por tanto puede existir una situación en la que un objetivo sea detectable de forma fiable pero su posición medida sea muy imprecisa.

## 13.6. Consecuencia estratégica

El espacio abierto es generalmente el entorno más desfavorable para una nave que quiera permanecer oculta.

Los cuerpos celestes, el polvo y las estrellas crean:

- rutas de aproximación;
- zonas de ocultación;
- posiciones de emboscada;
- sectores de mala observación;
- oportunidades para romper seguimiento;
- decisiones sobre qué sensor utilizar.

Ningún entorno debe proporcionar stealth universal: una posición excelente frente a sensores de firma puede seguir siendo vulnerable a sensores energéticos y viceversa.

---

# 14. Armas ofensivas guiadas: misiles y torpedos

Existen dos familias principales de armas ofensivas guiadas:

- **misiles**;
- **torpedos**.

Ambas utilizan un seeker propio para adquirir el blanco y ambas pueden producir impactos letales.

La diferencia fundamental es la doctrina de aproximación:

- el misil acepta ser detectado a cambio de velocidad, persecución y saturación;
- el torpedo intenta permanecer inerte durante la mayor parte de su recorrido para activarse tarde y atacar por sorpresa.

## 14.1. Arquitectura común

Misiles y torpedos son objetos completos con componentes internos.

Cada modelo tiene una capacidad interna determinada y distribuye ese espacio entre, como mínimo:

- seeker;
- motor;
- combustible;
- generador;
- carga explosiva;
- electrónica y estructura necesarias.

Todo sistema que consume energía necesita generación correspondiente también en misiles y torpedos.

El jugador no construye un misil pieza a pieza.

Los modelos son prefabricados por diseño, pero internamente siguen las mismas reglas generales de espacio, energía, firma y compromiso entre prestaciones que el resto de objetos principales del juego.

## 14.2. Seeker

Todo misil y torpedo dispone de un **seeker**.

El seeker es funcionalmente un pequeño sensor activo instalado en el arma.

Puede ser:

- de firma;
- energético.

Hereda las reglas generales de su familia de sensor, incluidos efectos de distancia, entorno y Jammer.

### 14.2.1. Características

Un seeker tiene al menos:

- **Angle:** apertura del cono de observación;
- **Sensitivity:** capacidad para detectar un blanco;
- **Precision:** calidad de la localización obtenida;
- **Energy footprint:** energía consumida y huella generada mientras está activo.

El Angle es fijo para cada modelo de seeker.

El cono está orientado hacia el morro del misil o torpedo.

Un Angle grande:

- cubre un volumen mayor;
- tolera mejor errores en la dirección inicial de disparo;
- permite encontrar un objetivo más alejado del eje de vuelo;
- produce mayor Huella energética;
- hace el arma activa más fácil de detectar.

Un Angle pequeño:

- exige una dirección inicial más precisa;
- tolera peor desviaciones del blanco;
- reduce la Huella energética;
- favorece ataques discretos.

### 14.2.2. Mediciones periódicas

El seeker no conoce continuamente la posición real del blanco.

Realiza mediciones cada cierto intervalo de tiempo.

El intervalo de medición es una característica propia del seeker, por ejemplo **Scan interval**.

A diferencia de los sensores activos de una nave, el seeker no utiliza bandas de distancia seleccionables: observa todo el volumen contenido dentro de su cono y la distancia degrada Sensitivity y Precision de forma normal.

Cada medición funciona como un barrido de sensor activo:

- utiliza Sensitivity y Precision;
- aplica los modificadores de distancia;
- aplica el retardo de propagación correspondiente;
- puede verse afectada por entorno y Jammer;
- produce una estimación imperfecta de la posición real.

A medida que el arma se acerca, las nuevas mediciones tienden a ser mucho más precisas en términos absolutos.

Por ello la Precision sigue siendo una característica real, pero normalmente es menos crítica en fase terminal que en sensores de búsqueda a millones de kilómetros.

### 14.2.3. Adquisición de blancos

El seeker considera blancos válidos:

- naves no amigas;
- estaciones no amigas;
- señuelos capaces de presentarse como un blanco válido.

Se asume la existencia de un sistema de **IFF** capaz de distinguir blancos amigos de no amigos.

La selección utiliza siempre la **posición estimada por las mediciones del propio seeker**, nunca la posición real oculta del objeto.

El seeker comienza buscando dentro de una zona estrecha alrededor del eje central de su cono.

Entre los blancos válidos detectados dentro de esa zona prioriza:

1. proximidad al eje central;
2. cercanía al seeker.

Si no encuentra ningún blanco válido, amplía progresivamente el ángulo de búsqueda hasta alcanzar el Angle máximo de su seeker.

Si aun así no encuentra ningún objetivo, no adquiere ninguno y continúa en línea recta.

No existe una regla especial para señuelos: un señuelo que consiga parecer un blanco legítimo participa normalmente en esta selección.

### 14.2.4. Seguimiento

Una vez adquirido un blanco, el seeker utiliza sus sucesivas mediciones para calcular una estimación cada vez mejor de su posición real.

La guía del arma utiliza esa posición estimada como referencia.

Cada modelo de arma puede tener una variable de configuración de **reacquisition**.

Si reacquisition está activa y el seeker pierde el lock:

- el arma continúa hacia la última posición estimada;
- el seeker sigue realizando mediciones;
- puede adquirir de nuevo el mismo blanco o seleccionar otro blanco válido según sus reglas normales de adquisición.

Si reacquisition está desactivada:

- una vez fijado un objetivo, el arma ignora los demás;
- si pierde el lock continúa hacia la última posición estimada de ese objetivo;
- no cambia de blanco.

Si el Jammer degrada suficientemente la Precision, puede producirse esta pérdida de lock sin ninguna tirada especial de "jamming success".

La conveniencia de utilizar intercepción predictiva basada en velocidad estimada frente a una persecución más simple queda pendiente de probarse en gameplay.

### 14.2.5. Autonomía

Misiles y torpedos son **fire-and-forget**.

Una vez lanzados:

- no reciben actualizaciones de la nave;
- no existe datalink de corrección;
- no pueden retargetearse manualmente;
- no puede modificarse su configuración;
- actúan de forma completamente autónoma.

Esto hace que la calidad de la dirección inicial y, especialmente en torpedos, el momento de activación sean decisiones importantes del jugador.

### 14.2.6. Detección de la emisión del seeker

Un seeker activo es un sensor activo.

Los sensores pasivos defensivos pueden detectar que una emisión de seeker está alcanzando o buscando a la nave.

Esto puede generar una **alerta de emergencia de targeting** incluso antes de que los sensores defensivos puedan localizar físicamente el misil.

La alerta por sí sola:

- no proporciona la posición del misil;
- no permite disparar una contramedida contra él;
- informa de que un seeker activo está iluminando o buscando la nave.

La posición del arma solo se obtiene cuando su huella energética resulta suficientemente detectable para el sensor defensivo.

## 14.3. Motor y cinemática

Los motores de misiles, torpedos y naves comparten los mismos principios generales.

Como mínimo tienen:

- **Acceleration**;
- **Maneuverability**;
- **Fuel**;
- **Energy footprint**.

### 14.3.1. Acceleration

La aceleración determina principalmente:

- cuánto puede aumentar o reducir la velocidad el objeto;
- cuánto combustible consume durante la propulsión principal.

El consumo de combustible depende principalmente de acelerar o desacelerar.

No existe una velocidad máxima artificial: mientras quede combustible y el motor siga acelerando, la velocidad puede continuar aumentando.

### 14.3.2. Maneuverability

La Maneuverability determina la capacidad para cambiar la dirección del vector de movimiento y orientar la trayectoria hacia el objetivo.

Las maniobras de orientación y corrección lateral consumen muy poco combustible en comparación con la aceleración principal.

Este principio se aplica también a los motores de las naves.

Por tanto, un arma puede conocer con gran precisión dónde está un blanco y aun así fallar si no dispone de Maneuverability suficiente para modificar su trayectoria a tiempo.

### 14.3.3. Fin del combustible

Cuando el combustible se agota:

- el motor deja de acelerar;
- el arma deja de poder corregir activamente su trayectoria;
- conserva su velocidad y dirección por inercia;
- el seeker puede seguir funcionando mientras disponga de energía propia, pero ya no puede cambiar el resultado salvo que el arma estuviera casualmente encaminada hacia el blanco.

En la práctica, un misil o torpedo sin combustible suele perderse en el espacio.

## 14.4. Misiles

Un misil utiliza su motor desde el lanzamiento.

Su seeker está activo desde el principio o se activa poco después del lanzamiento según el modelo.

El retraso inicial de activación del seeker, cuando exista, es fijo para ese modelo y no lo configura el jugador.

Mientras dispone de combustible:

- acelera;
- maniobra;
- realiza mediciones con su seeker;
- corrige su trayectoria;
- persigue el blanco adquirido.

### 14.4.1. Doctrina

El misil busca:

> velocidad + persecución + saturación.

El atacante asume que será detectado y trata de superar la defensa mediante:

- velocidad alta;
- adquisición temprana;
- correcciones continuas;
- varios misiles simultáneos;
- presión sobre interceptores y defensas terminales.

### 14.4.2. Detectabilidad

Durante su vuelo activo contribuyen a su detectabilidad:

- firma física base del cuerpo;
- firma producida por la estela del motor;
- Huella energética del motor;
- Huella energética del seeker;
- cualquier otro dispositivo activo instalado.

Los componentes de un misil siguen exactamente la misma regla de Huella energética que cualquier otro dispositivo del juego.

### 14.4.3. Alcance

Su alcance útil está limitado por el combustible necesario para continuar acelerando y perseguir un blanco.

Un misil puede viajar mucho más lejos por inercia después de agotar combustible, pero deja de ser una amenaza guiada efectiva salvo coincidencia de trayectoria.

## 14.5. Torpedos

Un torpedo se lanza inicialmente inerte mediante una **catapulta electromagnética**.

La catapulta determina la velocidad inicial de lanzamiento.

Diferentes modelos de lanzador de torpedos pueden proporcionar diferentes velocidades iniciales.

### 14.5.1. Fase inerte

Durante la fase inerte:

- el torpedo conserva la velocidad inicial por inercia;
- mantiene la dirección y orientación de lanzamiento;
- el motor permanece apagado;
- el seeker permanece apagado;
- no recibe correcciones ni actualizaciones;
- no consume combustible de propulsión;
- su Huella energética propia es prácticamente nula;
- su firma física base es extremadamente pequeña por su reducido tamaño.

Un torpedo inerte es por tanto muy difícil de detectar.

Un sensor de firma extraordinariamente sensible podría detectarlo a corta distancia, pero en condiciones normales la detección antes de la activación es muy improbable.

### 14.5.2. Programación de activación

Antes del lanzamiento el jugador selecciona una **banda de distancia de activación**:

- corta;
- media;
- larga;
- extrema.

La banda representa la distancia recorrida desde el lanzamiento antes de activar el arma.

Como la velocidad proporcionada por la catapulta es conocida, el sistema puede convertir internamente esa distancia en el tiempo de vuelo correspondiente.

Cuando alcanza la distancia programada:

- se activa el seeker;
- se activa el motor;
- comienza a consumir combustible;
- empieza a acelerar y maniobrar;
- intenta adquirir un blanco válido.

Una activación temprana proporciona más tiempo para buscar y corregir.

Una activación tardía maximiza la sorpresa pero aumenta el riesgo de que el blanco ya no se encuentre dentro del cono del seeker.

### 14.5.3. Doctrina

El torpedo busca:

> aproximación silenciosa + activación tardía + sorpresa.

Su mayor alcance práctico procede de conservar el combustible durante la fase inerte.

Normalmente es más lento durante la aproximación inicial que un misil que lleva tiempo acelerando, pero puede acercarse mucho antes de producir una firma y Huella energética importantes.

## 14.6. Interfaz de disparo

La interfaz evita cálculos manuales complejos.

### Misil

El jugador:

1. selecciona el modelo de misil;
2. selecciona, si el lanzador lo permite, cuántos misiles disparará simultáneamente;
3. hace clic en la pantalla para indicar la **dirección inicial de disparo**;
4. dispara.

### Torpedo

El jugador:

1. selecciona el modelo de torpedo;
2. selecciona la banda de activación: corta, media, larga o extrema;
3. hace clic en la pantalla para indicar la **dirección inicial de disparo**;
4. dispara.

El jugador no introduce manualmente coordenadas, velocidades ni soluciones matemáticas de interceptación.

El arma debe encontrar después un blanco válido con su seeker.

## 14.7. Lanzadores

Misiles y torpedos utilizan lanzadores diferentes.

Toda arma lanzada hereda la velocidad de la nave que la dispara.

Por tanto:

- un misil parte con la velocidad actual de la nave y desde ahí comienza a acelerar con su propio motor;
- un torpedo parte con la velocidad actual de la nave más la velocidad adicional proporcionada por la catapulta electromagnética.

Esto permite que la cinemática previa de la nave influya directamente en el lanzamiento.

Los lanzadores tienen arcos físicos de disparo.

La interfaz no obliga al jugador a micromanejar estos arcos:

- una nave puede montar lanzadores orientados en direcciones complementarias para cubrir varios sectores;
- cuando exista más de un lanzador válido, el sistema utiliza automáticamente el adecuado;
- si ningún lanzador puede disparar hacia la dirección indicada, la nave puede orientarse automáticamente hasta disponer de un arco válido y efectuar el lanzamiento.

### 14.7.1. Lanzadores de misiles

Un misil necesita un silo o lanzador desde el que pueda iniciar su propio motor.

Algunos lanzadores permiten realizar varios disparos simultáneos.

Cuando el lanzador lo soporta, la interfaz permite seleccionar cuántos misiles se disparan en la salva, normalmente entre **1 y 4**.

Los misiles de una misma salva no coordinan reparto de blancos.

Si varios observan la misma nave como el blanco válido preferente, todos la atacarán.

### 14.7.2. Lanzadores de torpedos

Los torpedos necesitan una catapulta electromagnética.

La catapulta determina la velocidad inicial de salida.

### 14.7.3. Recarga

El **reload time** es una característica del lanzador, no del misil o torpedo.

Diferentes lanzadores pueden por tanto:

- recargar a velocidades distintas;
- permitir salvas de tamaños diferentes;
- en el caso de torpedos, proporcionar velocidades iniciales distintas.

## 14.8. Carga explosiva y detonación

Misiles y torpedos llevan una carga explosiva.

La carga determina:

- potencia de la explosión;
- distancia a la que esa explosión puede producir daño significativo.

La explosión se considera omnidireccional.

### 14.8.1. Condiciones de detonación

Por defecto, la ojiva detona:

- al entrar en contacto con el blanco;
- cuando una defensa destruye el misil o torpedo después de estar armado.

No existe por ahora una espoleta de proximidad estándar.

### 14.8.2. Distancia mínima de armado

Cada arma tiene una distancia mínima de armado.

Esa distancia puede depender de la potencia de su carga explosiva.

La finalidad es impedir que el arma produzca una detonación peligrosa inmediatamente junto a la nave que la lanzó.

Si el arma es destruida antes de alcanzar la distancia mínima de armado, la carga principal no detona. Puede generar restos o daños menores, pero no produce la explosión antinave completa.

### 14.8.3. Daño por detonación

Un impacto directo de un arma antinave suele ser letal o producir un mission kill.

Una detonación cercana también puede causar daños graves.

Para resolverla son suficientes, a nivel del arma:

- potencia de la carga;
- distancia entre la explosión y la nave.

El daño disminuye fuertemente con la distancia.

El blindaje puede resultar importante frente a una explosión suficientemente lejana, aunque no debe salvar una nave de una detonación directa de gran potencia.

### 14.8.4. Destrucción por contramedidas

Destruir un misil no hace desaparecer mágicamente su carga.

Si una defensa destruye un misil o torpedo armado:

- la ojiva detona;
- la explosión se produce en el punto de destrucción.

Por tanto, una defensa terminal puede destruir correctamente el arma y aun así permitir daños si la intercepción ocurre demasiado cerca.

La distancia de intercepción es especialmente importante frente a torpedos o armas con cargas explosivas grandes.

## 14.9. IFF, señuelos y fuego amigo

El seeker utiliza IFF para excluir blancos amigos.

Entre todos los blancos no amigos que detecta selecciona el más próximo al centro del cono.

Un señuelo diseñado para parecer un blanco legítimo puede ser seleccionado exactamente igual que una nave o estación real.

No existe una excepción especial de "probabilidad de caer en el señuelo": el engaño emerge del funcionamiento normal del seeker.

## 14.10. Persistencia de armas perdidas

A nivel de lore, un misil o torpedo que falla no desaparece.

Continúa desplazándose por el espacio según su posición, dirección y velocidad.

A nivel técnico no es necesario conservar indefinidamente el objeto 3D completo.

Cuando se aleje suficientemente del escenario activo puede:

- descargarse de la simulación detallada;
- desaparecer de la escena;
- conservarse únicamente como un registro ligero con posición, dirección, velocidad y demás datos necesarios.

El criterio exacto de persistencia y eliminación se decidirá durante el diseño técnico.

---

# 15. Defensa contra misiles y contramedidas

La defensa en Hullbreach se basa en evitar que una amenaza alcance el casco.

Las contramedidas principales previstas son:

- misiles interceptores;
- láser defensivo;
- defensa cinética;
- señuelos;
- Jammer;
- maniobra y control de emisiones como defensa indirecta.

No existe una defensa perfecta ni una capa capaz de detener indefinidamente todos los ataques.

## 15.1. Principio de defensa por capas

La defensa puede entenderse como una secuencia de capas:

1. evitar o degradar la solución de tiro enemiga;
2. engañar o desviar el ataque;
3. destruir amenazas a larga distancia con interceptores;
4. destruir amenazas supervivientes con defensas de última hora;
5. si todo falla, el impacto alcanza el casco.

Cada capa resuelve un problema distinto.

La fortaleza de una nave defensiva no consiste en absorber impactos, sino en reducir la probabilidad de que alguno llegue a producirse.

## 15.2. Misiles interceptores

Los misiles interceptores son la mejor defensa directa contra misiles y torpedos enemigos.

Conceptualmente son misiles de pequeño tamaño diseñados específicamente para interceptar otras armas guiadas.

Comparten con los misiles ofensivos las reglas generales de:

- motor;
- aceleración;
- maniobrabilidad;
- combustible;
- Huella energética;
- generación;
- espacio interno;
- lanzamiento;
- vuelo por inercia cuando agotan combustible.

Sin embargo, su doctrina y perfil de prestaciones son diferentes.

### 15.2.1. Perfil típico

Frente a un misil ofensivo comparable, un interceptor suele tener:

- **menor alcance**;
- **menor velocidad punta práctica**;
- **mayor Maneuverability**;
- menor carga destructiva;
- tamaño reducido.

Su objetivo no es perseguir una nave a gran distancia, sino alcanzar rápidamente una amenaza ya localizada dentro de la burbuja defensiva y ser capaz de corregir con violencia frente a un blanco pequeño y muy rápido.

La alta Maneuverability es por tanto una de sus prestaciones fundamentales.

### 15.2.2. Guiado externo

Los interceptores no dependen de un seeker propio para localizar el blanco.

Son guiados por los **sensores defensivos de la nave que los dispara**.

La nave:

1. detecta el misil o torpedo enemigo;
2. estima su posición mediante el sensor defensivo;
3. lanza el interceptor;
4. continúa actualizando la posición estimada de la amenaza;
5. transmite al interceptor las correcciones necesarias durante el vuelo.

El interceptor depende por tanto de que la nave mantenga una localización suficientemente buena del objetivo.

La posición utilizada para guiarlo es siempre la posición **estimada por el sensor defensivo**, nunca la posición real oculta del arma enemiga.

### 15.2.3. Dependencia del sensor defensivo

Esta dependencia es una limitación central.

Si los sensores defensivos:

- no detectan la amenaza;
- la detectan demasiado tarde;
- tienen una Precisión insuficiente;
- quedan cegados por la actividad de la propia nave;
- son fuertemente degradados por un Jammer;

el interceptor pierde calidad de guiado o puede resultar imposible de emplear eficazmente.

Esto refuerza la secuencia táctica del Jammer:

- mantener el Jammer activo dificulta que el seeker enemigo consiga una solución;
- pero también degrada los sensores defensivos propios;
- para utilizar interceptores con eficacia puede ser necesario apagar el Jammer y recuperar una buena solución sobre la amenaza entrante.

### 15.2.4. Ventajas

Sus principales ventajas son:

- gran eficacia contra amenazas detectadas a tiempo;
- alta capacidad de maniobra;
- posibilidad de destruir el arma enemiga lejos de la nave protegida;
- posibilidad de proteger tanto a la propia nave como a otras naves cercanas cuando el sensor defensivo y la geometría lo permitan.

### 15.2.5. Limitaciones

Sus principales limitaciones son:

- alcance relativamente corto;
- velocidad normalmente menor que la de los misiles ofensivos;
- dependencia completa de los sensores defensivos;
- necesidad de detección suficientemente temprana;
- munición limitada;
- volumen de almacenamiento considerable comparado con munición cinética;
- posibilidad de agotar la reserva ante ataques de saturación.

La principal debilidad de esta capa no es una baja eficacia individual, sino detectar demasiado tarde, perder calidad de guiado o quedarse sin interceptores.

### 15.2.6. Pérdida temporal de solución

Si los sensores defensivos pierden temporalmente la solución sobre la amenaza:

- el interceptor continúa hacia la última posición estimada conocida;
- espera nuevas actualizaciones de guiado;
- reanuda las correcciones en cuanto la nave vuelve a obtener una solución suficientemente buena.

El interceptor no dispone de un seeker autónomo equivalente al de un misil ofensivo.

### 15.2.7. Cadencia de guiado

El interceptor recibe nuevas correcciones cada vez que los sensores defensivos generan una nueva medición útil sobre la amenaza.

No existe una cadencia de guiado independiente del interceptor.

Por tanto, la frecuencia y calidad de actualización dependen directamente del sensor defensivo que mantiene el seguimiento.

### 15.2.8. Carga explosiva y detonación de proximidad

Los interceptores también llevan una carga explosiva.

Su objetivo no es necesariamente impactar físicamente contra el misil enemigo.

Cuando los sensores defensivos estiman que el interceptor ha alcanzado una distancia adecuada respecto a la amenaza:

1. calculan la separación estimada;
2. ordenan la detonación del interceptor;
3. la explosión intenta alcanzar al misil o torpedo enemigo dentro de su radio efectivo.

Cuanto mayor sea la potencia de la carga explosiva del interceptor, mayor puede ser la distancia útil de detonación.

La detonación depende de la posición **estimada** del blanco.

Por tanto, un error de detección o una Precision insuficiente de los sensores defensivos puede provocar:

- detonación demasiado temprana;
- detonación demasiado tardía;
- explosión fuera del radio eficaz;
- fallo completo de la intercepción.

La fórmula exacta de decisión de detonación se definirá durante la implementación de bajo nivel.

### 15.2.9. Efecto sobre varias amenazas

La explosión del interceptor es física y puede afectar a cualquier arma enemiga situada dentro de su radio efectivo.

Si dos o más misiles o torpedos están suficientemente próximos cuando detona:

- todos pueden resultar destruidos;
- sus propias ojivas pueden detonar si ya estaban armadas.

Esto permite que una única intercepción bien situada destruya varias amenazas de una salva compacta.

### 15.2.10. Uso contra naves

Los interceptores no están restringidos artificialmente a misiles.

Si los sensores defensivos detectan y localizan una nave enemiga suficientemente cercana, pueden guiar un interceptor contra ella.

Sin embargo:

- su carga explosiva suele ser pequeña;
- están optimizados para destruir misiles frágiles;
- normalmente son poco eficaces contra naves blindadas.

Por tanto pueden utilizarse contra naves, pero no sustituyen al armamento ofensivo dedicado.

## 15.3. Láser defensivo

El láser defensivo es una defensa de última hora guiada por los sensores defensivos de la nave.

Como regla general, todas las defensas activas de la nave dependen de los sensores defensivos para localizar y seguir amenazas. Los señuelos son la excepción principal porque, una vez lanzados, funcionan de forma autónoma.

El láser no utiliza munición física.

Esto produce dos beneficios:

- no puede quedarse sin munición;
- no necesita reservar espacio interno para almacenar proyectiles o interceptores.

Ese espacio puede utilizarse para otros sistemas.

Por esta razón es una defensa muy popular incluso en naves que ya disponen de interceptores.

### 15.3.1. Guiado y seguimiento

El láser no dispone de un sensor autónomo propio para localizar el blanco.

Los sensores defensivos proporcionan continuamente la posición estimada de la amenaza.

El láser:

1. orienta el emisor hacia esa posición estimada;
2. dispara un pulso corto;
3. debe mantener el seguimiento durante la duración del pulso;
4. repite nuevos pulsos hasta destruir el blanco o perder la solución.

Si la posición estimada es incorrecta por falta de Precision, Jammer u otras interferencias, el pulso puede fallar.

La precisión absoluta mejora naturalmente cuando el misil se acerca, por lo que el láser se convierte de forma emergente en una defensa especialmente eficaz a corta distancia.

### 15.3.2. Pulsos y daño térmico

El láser dispara **pulsos cortos**, no un haz continuo permanente.

Cada impacto deposita una cantidad de energía o calor sobre el blanco.

El láser tiene una característica de **Damage/Heat** que determina cuánto daño térmico produce cada impacto.

Los misiles y torpedos son blancos frágiles y normalmente necesitan aproximadamente **2 o 3 impactos** de un láser defensivo típico para quedar destruidos, aunque determinados modelos pueden necesitar más o menos.

El daño se acumula mediante impactos sucesivos.

Contra una nave blindada la misma cantidad de energía suele resultar muy poco eficaz, por lo que un láser defensivo puede disparar contra ella pero no está diseñado para perforar blindaje pesado.

### 15.3.3. Alcance

El láser defensivo no tiene por ahora un alcance máximo artificial propio.

Su alcance práctico depende principalmente de:

- alcance de los sensores defensivos;
- Precision de la solución;
- capacidad de seguimiento del emisor;
- movimiento del blanco.

Si el sensor defensivo no puede localizar la amenaza con suficiente calidad, el láser tampoco puede emplearse eficazmente contra ella.

### 15.3.4. Características

Un láser defensivo tiene como mínimo:

- **Damage/Heat:** energía térmica depositada por impacto;
- **Tracking speed / Mobility:** velocidad con la que puede girar y apuntar a un nuevo objetivo;
- **Active energy footprint:** huella mientras está encendido y preparado;
- **Firing energy footprint:** huella adicional o total mientras dispara;
- **Activation delay:** tiempo entre la orden de encendido y el momento en que puede disparar;
- arco físico de tiro.

La velocidad de seguimiento limita cuánto puede corregir el apuntado durante un pulso y cuánto tarda en cambiar de objetivo.

### 15.3.5. Huella energética y preparación

El láser produce Huella energética simplemente por estar activo.

Mientras dispara, la Huella energética aumenta todavía más.

Por tanto existen dos estados energéticos distintos:

- **activo/preparado:** consumo y huella elevados;
- **disparando:** consumo y huella aún mayores.

Normalmente se mantiene apagado para reducir detectabilidad.

El jugador debe activarlo con suficiente antelación para superar su Activation delay antes de que el misil entre en la ventana terminal.

### 15.3.6. Arco de tiro y orientación de la nave

El láser tiene un arco físico de tiro.

La interfaz no obliga al jugador a micromanejarlo.

Una nave puede resolver la cobertura de dos maneras:

- instalando varios láseres en posiciones opuestas o complementarias;
- orientándose automáticamente cuando ningún emisor tiene un arco válido hacia el objetivo seleccionado.

En una situación terminal, la capacidad real de la nave para completar ese giro a tiempo puede limitar la defensa.

### 15.3.7. Selección y cola de objetivos

Un emisor láser solo puede atacar **un objetivo cada vez**.

El jugador selecciona manualmente las amenazas que quiere atacar.

Puede seleccionar varios objetivos y formar una cola.

El láser los ataca en el orden en que fueron seleccionados.

Cuando destruye el objetivo actual, pierde la solución o recibe una nueva orden, pasa al siguiente objetivo de la cola, limitado por su Tracking speed / Mobility.

No existe reparto automático inteligente de blancos por defecto.

### 15.3.8. Destrucción de misiles y torpedos

Cuando el láser destruye un misil o torpedo se aplican las reglas normales de la ojiva:

- si la carga ya estaba armada o el torpedo ya estaba activo, puede detonar en el punto de destrucción;
- si un torpedo todavía estaba inerte y su carga no estaba armada, destruirlo no provoca la explosión antinave principal.

Por tanto, destruir un arma demasiado cerca puede seguir causando daños graves si su ojiva estaba activa.

### 15.3.9. Uso contra naves

Las armas defensivas no están restringidas artificialmente a misiles.

Si los sensores defensivos detectan y localizan una nave enemiga dentro de su alcance, el láser puede disparar contra ella.

Utiliza exactamente la misma mecánica:

- solución proporcionada por sensores defensivos;
- seguimiento;
- pulsos;
- Damage/Heat acumulado.

Sin embargo, un láser defensivo suele ser poco potente frente a blindaje naval y no sustituye a un armamento ofensivo dedicado.

## 15.4. Defensa cinética

La defensa cinética es también una defensa de última hora y funciona de forma muy similar al láser defensivo.

Depende de los sensores defensivos para:

- localizar la amenaza;
- mantener una solución estimada;
- orientar el arma;
- seguir el blanco durante el ataque.

Comparte además las reglas generales de:

- arco físico de tiro;
- Tracking speed / Mobility;
- Activation delay;
- selección manual de objetivos;
- cola de objetivos;
- posibilidad de atacar naves cercanas detectadas por sensores defensivos.

Su diferencia principal es que utiliza proyectiles físicos y munición limitada.

### 15.4.1. Huella energética

La defensa cinética tiene una Huella energética activa claramente inferior a la de un láser defensivo.

Mientras permanece encendida consume energía, pero su contribución a la detectabilidad energética es relativamente moderada.

Disparar apenas aumenta su Huella energética.

Por tanto no necesita una diferencia grande entre estado preparado y estado de fuego como ocurre con el láser.

Esto la convierte en una defensa terminal menos penalizante desde el punto de vista energético, a cambio de depender de munición finita.

### 15.4.2. Munición

La munición de la defensa cinética es limitada.

Cada ráfaga consume proyectiles del almacén asignado al arma.

Una nave puede por tanto agotar por completo esta capa defensiva durante un combate prolongado o ante ataques de saturación.

El consumo depende principalmente del modo de disparo seleccionado.

### 15.4.3. Modos de disparo

La defensa cinética tiene al menos dos modos de disparo.

Los modos afectan principalmente a:

- **probabilidad de impacto**;
- **consumo de munición**.

No modifican significativamente la Huella energética.

#### Modo bajo

El modo bajo:

- utiliza menos proyectiles por intento;
- consume munición lentamente;
- proporciona una probabilidad de impacto menor;
- permite mantener la defensa operativa durante más tiempo.

Está pensado para conservar munición cuando la amenaza permite asumir un riesgo mayor de fallo.

#### Modo alto

El modo alto:

- utiliza una cadencia o densidad de fuego mucho mayor;
- incrementa de forma importante la probabilidad de impacto;
- consume munición extremadamente rápido.

Está pensado para maximizar la supervivencia inmediata cuando una amenaza es crítica.

### 15.4.4. Resolución del ataque

El arma apunta utilizando la posición estimada por los sensores defensivos.

La probabilidad de impacto depende de la calidad de esa solución y del modo de disparo.

Una mala Precision, un Jammer, una alta velocidad angular del blanco o una Tracking speed insuficiente pueden reducir la eficacia.

El modo alto compensa parte de estas dificultades aumentando la densidad de fuego, pero no corrige una solución completamente inútil.

La fórmula exacta de probabilidad de impacto se definirá durante la implementación de bajo nivel.

### 15.4.5. Uso contra naves

La defensa cinética puede disparar contra naves cercanas detectadas por los sensores defensivos.

Sin embargo está optimizada para destruir misiles y torpedos frágiles.

Contra una nave blindada, sus proyectiles suelen tener una capacidad de penetración y daño muy limitada.

No sustituye al armamento ofensivo dedicado.

## 15.5. Señuelos

Los señuelos son objetos físicos reales lanzados por la nave.

No generan simplemente un eco ficticio en la interfaz.

A diferencia de interceptores, láseres y defensas cinéticas, **no dependen en absoluto de los sensores defensivos**.

Una vez lanzados son objetos autónomos.

### 15.5.1. Lanzamiento y trayectoria

El jugador los lanza de forma muy parecida a un torpedo:

1. selecciona el señuelo;
2. selecciona una banda de distancia de activación;
3. hace clic en la pantalla para indicar la dirección de lanzamiento;
4. lanza el señuelo.

El señuelo recibe una velocidad inicial y continúa desplazándose por inercia.

No dispone de motor principal.

Durante todo su vuelo:

- mantiene velocidad constante salvo efectos externos;
- conserva su trayectoria inicial;
- no acelera;
- no maniobra;
- no recibe correcciones;
- no depende de sensores defensivos ni de ninguna solución de tiro.

Al alcanzar la distancia programada se activa.

### 15.5.2. Estado inerte

Antes de activarse el señuelo es físicamente un objeto aproximadamente del tamaño de un misil.

Su firma y Huella energética reales son por tanto pequeñas mientras permanece inerte.

No pretende engañar al enemigo durante esta fase.

### 15.5.3. Imitación de nave

Al activarse comienza a emitir una combinación artificial de:

- firma física;
- Huella energética;

diseñada para parecer compatible con una **nave indeterminada**.

El señuelo no puede configurarse para imitar una nave concreta, una clase concreta ni un modelo concreto.

Su objetivo es conseguir que el sensor enemigo concluya inicialmente que está observando una nave real sin poder establecer correctamente cuál.

Aunque físicamente tenga aproximadamente el tamaño de un misil, las emisiones y características simuladas hacen que sus mediciones puedan resultar compatibles con un objetivo naval mucho mayor.

### 15.5.4. Penalización de localización

Los señuelos están diseñados para resultar más difíciles de localizar exactamente que una nave real.

Cuando un sensor obtiene mediciones sobre un señuelo activo, su **Precision efectiva recibe una penalización adicional**.

Por tanto:

- puede ser relativamente fácil detectar que existe algo;
- puede resultar considerablemente más difícil establecer su posición exacta;
- los ecos obtenidos pueden mostrar una dispersión mayor que la producida por una nave real en las mismas condiciones.

Esta penalización se suma a las demás fuentes normales de error, como distancia, geometría, entorno y Jammer.

### 15.5.5. Identificación

Un señuelo activo es deliberadamente más difícil de identificar correctamente que una nave real.

El proceso sigue utilizando las reglas generales de identificación progresiva, pero con una penalización específica del señuelo.

Durante las fases intermedias de identificación el sensor puede clasificarlo erróneamente como **cualquier nave compatible elegida al azar**.

Esta identificación provisional:

- puede cambiar con nuevas mediciones;
- no representa una identidad real subyacente;
- no implica que el señuelo esté imitando conscientemente ese modelo.

El señuelo nunca imita deliberadamente una nave concreta.

Cuando el proceso de identificación alcanza certeza suficiente, la clasificación correcta se revela como:

**DECOY / SEÑUELO**

A partir de ese momento deja de considerarse una nave real para efectos de interpretación e identificación.

### 15.5.6. Interacción con seekers

Mientras no haya sido identificado correctamente como señuelo, puede ser considerado un blanco válido por seekers enemigos exactamente igual que una nave real.

No existe una tirada especial de "engaño de señuelo".

El seeker aplica sus reglas normales:

- detecta objetos;
- utiliza su posición estimada;
- evalúa blancos válidos;
- selecciona según sus reglas de adquisición.

Si el señuelo ocupa una posición favorable respecto al cono del seeker, puede ser adquirido en lugar de la nave real.

### 15.5.7. Uso táctico

Los señuelos no sirven únicamente para defenderse de un misil ya lanzado.

Pueden utilizarse de forma ofensiva y estratégica para manipular la información del enemigo.

Ejemplos:

- hacer creer que una nave se encuentra en otra posición;
- provocar un barrido activo enemigo;
- atraer una patrulla;
- hacer gastar misiles;
- desviar seekers;
- saturar la interpretación de ecos;
- preparar una emboscada;
- simular una aproximación o retirada.

Conceptualmente equivalen a lanzar una distracción en un juego de sigilo: su valor depende mucho de dónde y cuándo se utilicen.

## 15.6. Configuraciones civiles y paramilitares

No todas las naves necesitan sensores de búsqueda ni armamento ofensivo.

Algunas naves civiles o de seguridad pueden equipar únicamente:

- sensores defensivos;
- láser defensivo;
- defensa cinética;
- otras contramedidas básicas.

Esto puede ser habitual en:

- policía;
- seguridad privada;
- piratas de baja capacidad;
- naves auxiliares;
- determinados transportes armados.

Estas naves no pueden buscar y atacar objetivos a gran distancia como una nave militar equipada con sensores activos, pero sí pueden detectar, identificar y atacar objetos que entren dentro de su corta burbuja defensiva.

Otras naves civiles pueden carecer completamente de sensores defensivos y armamento, como determinados cargueros baratos o naves diseñadas exclusivamente para transporte.

## 15.7. Jammer

El Jammer crea una zona volumétrica omnidireccional de interferencia alrededor de la nave emisora.

Protege a cualquier objeto situado dentro de esa zona, sea aliado o enemigo.

Su función defensiva principal es degradar la Precisión de sensores y seekers:

- penalización muy alta para sensores energéticos, incluidos los sensores defensivos;
- penalización moderada para sensores de firma.

Tiene potencia fija, gran Huella energética y un área de efecto determinada por el modelo instalado.

También interfiere con los sensores propios afectados.

Las áreas de varios Jammers pueden solaparse, pero sus penalizaciones no se suman.

## 15.8. Maniobra y control de emisiones

Apagar sistemas, cortar el motor principal y modificar el estado de la nave no son contramedidas instalables, pero sí forman parte directa de la defensa.

Pueden utilizarse para:

- reducir firma eliminando la estela de propelente;
- reducir huella energética;
- romper una solución de tiro;
- hacer que ecos antiguos dejen de representar bien la posición actual;
- dificultar la adquisición de un seeker;
- aprovechar cuerpos celestes, polvo u otras condiciones ambientales.

Estas mecánicas están integradas en los sistemas de sensores y entorno y no requieren una categoría de equipo separada.

## 15.9. Filosofía general de las contramedidas

Cada contramedida debe resolver un problema diferente:

- **interceptor:** máxima eficacia a distancia, limitada por detección temprana, espacio y munición;
- **láser:** defensa infinita en munición, pero limitada en eficacia y con gran huella energética;
- **cinética:** mejor defensa terminal, limitada por munición y ritmo de consumo;
- **señuelo:** manipulación de información y adquisición de blancos;
- **Jammer:** degradación extrema de precisión a costa de una enorme exposición energética;
- **maniobra y control de emisiones:** reducción de detectabilidad y ruptura de soluciones.

La nave más protegida no es la que acumula más resistencia estructural, sino la que combina correctamente varias de estas capas.

---

# 16. Maniobra

La maniobra no está pensada principalmente para esquivar físicamente un misil mediante reflejos.

Los motores tienen, entre otras propiedades, **Acceleration** y **Maneuverability**. La aceleración es el principal origen del consumo de combustible, mientras que los cambios de orientación y correcciones de maniobra son comparativamente baratos.

Sirve para:

- orientar sensores;
- orientar defensas y armas;
- evitar zonas muertas;
- mantener o perder ecos;
- aprovechar cuerpos celestes y polvo;
- modificar firma mediante uso o apagado del motor principal;
- cambiar la trayectoria esperada por el atacante;
- dificultar seekers estrechos;
- romper soluciones de tiro.

El combate tridimensional debe importar porque los sensores activos son muy direccionales y pueden ser prácticamente inútiles arriba, abajo o detrás.

---

# 17. Armas y defensas como problemas distintos

Las armas y defensas no deben diferenciarse principalmente por daño bruto.

Principio:

> Cada sistema define qué problema debe resolver el jugador para conseguir un impacto o evitarlo.

El armamento ofensivo guiado ya definido se basa en:

- **misiles:** velocidad, persecución y saturación;
- **torpedos:** aproximación inerte, activación tardía y sorpresa.

Las principales defensas ya definidas se basan en:

- **interceptores:** destrucción a distancia mediante guiado por sensores defensivos;
- **láser defensivo:** seguimiento preciso y acumulación de pulsos;
- **defensa cinética:** densidad de fuego y gestión de munición;
- **señuelos:** manipulación de detección, localización e identificación;
- **Jammer:** degradación de Precision;
- **maniobra y control de emisiones:** ruptura de soluciones y reducción de detectabilidad.

No se contempla actualmente una familia de armas cinéticas ofensivas.

Ningún misil, torpedo, defensa o nave debe ser perfecto.

---

# 18. Daño

Hullbreach no utiliza puntos de vida globales para las naves.

El daño se resuelve localmente sobre la estructura física de la nave:

> impacto o explosión -> blindaje -> penetración -> compartimentos -> componentes / tripulación / atmósfera -> capacidades operativas.

Una nave queda fuera de combate o se pierde como consecuencia de lo que ha dejado de funcionar, de la muerte de su tripulación y de la pérdida de presión, no porque una barra de HP llegue a cero.

## 18.1. Propiedades básicas de una fuente de daño

Toda fuente capaz de dañar una nave utiliza como mínimo:

- **Damage:** severidad del daño producido después de penetrar;
- **Penetration:** capacidad para atravesar blindaje;
- **Area of effect:** radio dentro del cual puede afectar a más de un punto o compartimento;
- **Breach:** capacidad para producir perforaciones, abrir el casco y provocar pérdida de atmósfera.

Breach es necesario para diferenciar efectos físicamente distintos.

Por ejemplo:

- un láser defensivo puede tener Damage suficiente para destruir componentes internos después de penetrar, pero Breach relativamente bajo;
- una defensa cinética puede tener Penetration y Breach altos aunque su Damage total sea menor;
- un misil o torpedo tiene Damage, Penetration, Breach y Area of effect muy altos.

## 18.2. Armas puntuales y explosiones

Para un ataque con **Area of effect = 0**:

- solo se resuelve el punto donde impacta;
- solo el compartimento alcanzado directamente recibe el evento de daño;
- láseres y proyectiles cinéticos defensivos utilizados contra una nave funcionan de esta forma.

Para un ataque explosivo con **Area of effect > 0**:

- la explosión puede afectar a varios compartimentos;
- Damage y Penetration disminuyen con la distancia al centro de la explosión;
- el radio de Area of effect determina hasta dónde puede existir un efecto significativo.

La función exacta de caída se ajustará durante implementación, pero debe cumplir:

- distancia 0 -> Damage y Penetration máximos;
- distancia igual al Area of effect -> efecto 0;
- caída continua y fuerte con la distancia.

Conceptualmente:

`factor = falloff(distance / area_of_effect)`

`effective_damage = Damage * factor`

`effective_penetration = Penetration * factor`

La misma explosión puede por tanto destruir un compartimento cercano, dañar otro más alejado y no conseguir penetrar el blindaje de un tercero.

## 18.3. Qué compartimentos alcanza una explosión

Cada compartimento tiene una posición y volumen físicos o una representación espacial equivalente.

Una explosión consulta qué compartimentos entran dentro de su Area of effect.

Para cada uno se calcula:

- distancia desde la explosión al volumen del compartimento;
- Damage efectivo;
- Penetration efectiva;
- blindaje exterior que debe atravesarse;
- mamparos o barreras internas relevantes entre la explosión y ese compartimento.

Esto permite que una explosión grande alcance varios compartimentos sin aplicar automáticamente el mismo daño a todos.

Los compartimentos más próximos y más expuestos reciben el efecto más fuerte.

## 18.4. Penetración y transferencia de daño

El blindaje no funciona como puntos de vida.

Se compara la Penetration efectiva del ataque con el blindaje efectivo encontrado en la trayectoria.

Regla base:

- si `Penetration <= Armor`: el ataque no penetra y el Damage transferido es 0;
- si Penetration supera Armor por poco: solo se transfiere una fracción del Damage;
- si Penetration supera ampliamente Armor: se transfiere todo el Damage.

Como fórmula inicial:

`penetration_ratio = Penetration / Armor`

Si `penetration_ratio <= 1`:

`damage_transfer = 0`

Entre 1 y 2:

`damage_transfer = penetration_ratio - 1`

A partir de 2:

`damage_transfer = 1`

Finalmente:

`local_damage = effective_damage * damage_transfer`

Por tanto:

- 1,1 veces el blindaje -> aproximadamente 10 % del Damage;
- 1,5 veces -> aproximadamente 50 %;
- 2 veces o más -> 100 %.

El umbral de 2 es un valor de diseño inicial y puede ajustarse tras probar el sistema.

## 18.5. Impactos directos de misiles y torpedos

Un impacto directo de un misil o torpedo antinave constituye una excepción deliberada a la posibilidad de que el blindaje detenga completamente el ataque.

**Ningún blindaje instalable debe poder detener un impacto directo ni siquiera del misil antinave más débil del juego.**

Un impacto directo:

- garantiza penetración catastrófica del compartimento alcanzado;
- puede destruir completamente ese compartimento;
- puede destruir todos o casi todos los componentes contenidos;
- puede matar a toda la tripulación presente;
- genera además su explosión normal y aplica Area of effect sobre compartimentos cercanos;
- tiene una probabilidad muy alta de provocar descompresión extensa o general.

El blindaje sigue siendo importante frente a:

- detonaciones cercanas;
- zonas periféricas del Area of effect;
- láseres defensivos;
- fuego cinético defensivo;
- fragmentos y daño secundario.

## 18.6. Estado de los compartimentos

Los compartimentos no tienen una barra de HP global.

Cada compartimento tiene un estado estructural discreto, como mínimo:

- **Intacto**;
- **Dañado**;
- **Destruido**.

Un evento de daño local compara `local_damage` con la resistencia estructural del compartimento y obtiene una probabilidad de:

- permanecer funcional;
- quedar dañado;
- quedar destruido.

La fórmula exacta se calibrará durante implementación.

Un compartimento destruido representa una pérdida estructural local catastrófica:

- queda inhabitable;
- pierde su estanqueidad;
- su atmósfera se pierde;
- la tripulación presente muere o queda prácticamente condenada;
- los componentes alojados en él son destruidos o quedan inutilizables.

La destrucción de un compartimento **no destruye automáticamente toda la nave**. Si el compartimento puede aislarse, el resto del casco puede sobrevivir. Esto es necesario para que la compartimentación y los mamparos estancos tengan utilidad real.

Sin embargo, destruir un compartimento crítico puede producir inmediatamente un mission kill.

## 18.7. Componentes

Cada componente pertenece físicamente a un compartimento.

Los componentes tampoco utilizan una barra de HP continua como mecanismo principal.

Tienen estados como mínimo:

- **Operativo**;
- **Dañado**;
- **Destruido**.

Cada componente puede tener una característica de **Resistance** o robustez.

Cuando su compartimento recibe un evento de daño que ha penetrado, cada componente afectado resuelve una probabilidad de quedar:

- sin daños;
- dañado;
- destruido.

La probabilidad depende de:

- Damage local;
- Resistance del componente;
- naturaleza y posición del impacto cuando sea relevante.

Un componente dañado:

- sigue existiendo;
- puede sufrir reducción de rendimiento o quedar temporalmente inutilizado según su tipo;
- puede ser reparado por control de daños.

Un componente destruido:

- deja de funcionar;
- no puede repararse durante el combate;
- necesita sustitución o reparación mayor fuera de combate.

Si el compartimento queda destruido, sus componentes se consideran destruidos salvo excepciones futuras muy específicas.

## 18.8. Brechas y descompresión

Penetrar blindaje no implica automáticamente la misma pérdida de aire para todas las armas.

Después de penetrar, la propiedad **Breach** determina la gravedad de la perforación producida en el casco.

La combinación de:

- Breach;
- Damage local;
- estado estructural del compartimento;

determina la fuga resultante.

Las brechas pueden clasificarse conceptualmente como:

- **leve:** pérdida lenta de presión;
- **grave:** pérdida rápida de presión;
- **catastrófica:** el compartimento se abre al vacío o queda estructuralmente destruido.

Un láser suele tener Breach bajo.

Puede:

- penetrar;
- calentar o destruir componentes;
- herir o matar tripulación en el punto afectado;

sin abrir necesariamente un agujero grande.

La defensa cinética tiene normalmente:

- alta Penetration;
- Damage comparativamente menor;
- Breach alto.

Por tanto puede perforar fácilmente un casco ligero, destruir un componente en su trayectoria y provocar una descompresión peligrosa aunque no transfiera una enorme cantidad de Damage global.

Los misiles y torpedos tienen Breach muy alto.

## 18.9. Atmósfera por compartimentos

Cada compartimento presurizado conserva su propia atmósfera.

La atmósfera puede representarse mediante un valor de **Pressure/Air** independiente de los HP estructurales.

Los mamparos y puertas permiten aislar compartimentos.

Un compartimento correctamente cerrado puede permanecer presurizado aunque otro compartimento cercano se haya abierto al vacío.

Una brecha reduce Pressure según:

- gravedad de la brecha;
- volumen del compartimento;
- capacidad del soporte vital para compensar pérdidas.

Una brecha leve puede tardar en vaciar el compartimento.

Una brecha grave puede reducir la presión con rapidez.

Una brecha catastrófica produce una descompresión casi inmediata.

Si puertas o mamparos permanecen abiertos, la pérdida puede propagarse a compartimentos conectados.

## 18.10. Soporte vital

El soporte vital:

- mantiene condiciones habitables;
- puede compensar pérdidas pequeñas de aire;
- puede recuperar presión en un compartimento sellado cuando exista capacidad suficiente;
- no puede compensar indefinidamente una brecha grande.

Destruir el soporte vital no vacía instantáneamente la nave.

Los compartimentos conservan el aire que ya contienen, pero:

- dejan de poder mantenerlo o recuperarlo correctamente;
- una fuga se vuelve mucho más peligrosa;
- a largo plazo la tripulación pierde condiciones habitables incluso sin una brecha nueva.

## 18.11. Tripulación y descompresión

La tripulación puede sufrir bajas por dos mecanismos independientes:

- daño directo del impacto o explosión;
- pérdida de presión.

Mientras un compartimento conserve presión suficiente, la tripulación superviviente puede seguir operando y realizando control de daños.

Cuando la presión cae:

- aumenta el riesgo de incapacitación y muerte;
- una descompresión rápida tiene una probabilidad muy alta de matar a la tripulación presente;
- un compartimento completamente descomprimido se considera normalmente inhabitable.

La fórmula exacta de supervivencia dependerá de la velocidad de descompresión y del tiempo disponible para escapar o aislar la zona.

## 18.12. Control de daños

El control de daños es principalmente automático.

Si un compartimento:

- conserva tripulación viva;
- sigue siendo accesible y suficientemente habitable;

su tripulación intenta reparar automáticamente los componentes **Dañados**.

Los componentes **Destruidos** no pueden repararse durante el combate.

Las reparaciones pueden requerir tiempo y, más adelante, recursos o repuestos según el diseño económico definitivo.

### 18.12.1. Sellado de brechas

Una brecha pequeña puede ser reparada o contenida durante el combate si:

- la pérdida de presión sigue siendo limitada;
- todavía existe tripulación capaz de trabajar en el compartimento;
- el compartimento no ha quedado destruido.

Las brechas graves o catastróficas no pueden repararse normalmente durante el combate.

La respuesta correcta es aislar el compartimento mediante mamparos estancos.

Un compartimento completamente descomprimido o destruido no puede ser recuperado durante el combate salvo que se introduzca posteriormente equipamiento especializado.

## 18.13. Mission kill

No existe un porcentaje global de integridad que determine si una nave puede combatir.

El estado emerge de las capacidades que siguen disponibles.

Una nave puede quedar fuera de combate por perder uno o dos compartimentos clave aunque el resto del casco permanezca relativamente intacto.

Ejemplos:

- pérdida de generación eléctrica suficiente;
- pérdida de propulsión o control de actitud;
- pérdida de sensores necesarios;
- pérdida de todos los sistemas ofensivos;
- pérdida del mando o de la tripulación necesaria para operar;
- descompresión de compartimentos críticos;
- combinación de varias pérdidas parciales que elimine la capacidad de continuar la misión.

La evaluación debe basarse en funciones reales disponibles, no en HP restantes.

## 18.14. Pérdida total de la nave

Una nave puede considerarse perdida de forma total por causas como:

- descompresión general no contenible;
- muerte o incapacitación de toda la tripulación;
- destrucción estructural extensa;
- destrucción de la mayoría de componentes necesarios para cualquier recuperación;
- cascadas catastróficas futuras como explosiones de munición o fallos de reactor.

Una nave puede quedar primero en mission kill y seguir existiendo físicamente como casco recuperable o derelicto.

La diferencia entre mission kill, abandono, derelicto y destrucción física podrá utilizarse posteriormente en campaña, rescate y salvamento.

## 18.15. Perfil de las armas ya definidas

### Misiles y torpedos

- Damage extremadamente alto;
- Penetration extremadamente alta;
- Breach extremadamente alto;
- Area of effect mayor que 0;
- un impacto directo no puede ser detenido por blindaje;
- incluso una detonación cercana puede afectar a varios compartimentos.

### Láser defensivo contra naves

- Area of effect = 0;
- Damage/Heat local relevante;
- Penetration limitada frente a blindaje naval;
- Breach bajo;
- puede ser peligroso para naves poco blindadas y componentes internos si consigue penetrar;
- provoca menos descompresión que un penetrador cinético comparable.

### Defensa cinética contra naves

- Area of effect = 0;
- Penetration alta;
- Breach alto;
- Damage menor que el de un arma explosiva;
- puede atravesar blindaje ligero, dañar componentes y abrir brechas con facilidad;
- es peligrosa a corta distancia pese a no estar diseñada como arma ofensiva principal.

## 18.16. Principio general

El sistema no pregunta:

> ¿Cuántos HP le quedan a la nave?

Pregunta:

- ¿qué compartimento ha sido alcanzado?;
- ¿ha penetrado el blindaje?;
- ¿cuánto daño ha llegado al interior?;
- ¿qué componentes siguen operativos?;
- ¿qué tripulación sigue viva?;
- ¿qué compartimentos conservan presión?;
- ¿qué funciones reales puede seguir realizando la nave?

El resultado debe permitir naves aparentemente intactas pero incapaces de combatir y cascos gravemente dañados que todavía conserven alguna capacidad de movimiento o supervivencia.

---

# 19. Recursos y campaña

El juego tendrá consumo básico de recursos.

Recursos previstos inicialmente:

- comida;
- agua;
- combustible;
- munición;
- repuestos, sujeto a diseño definitivo.

Su función es introducir autonomía, planificación y logística sin convertir el juego en una simulación administrativa excesiva.

---

# 20. Puertos, estaciones y puntos habitados

Los nodos habitados pueden ofrecer, según el lugar:

- comercio;
- combustible y suministros;
- munición;
- reparación;
- modificación de nave;
- reclutamiento;
- contratos;
- información sobre misiones;
- rumores e inteligencia.

No todos los lugares deben ofrecer todos los servicios.

---

# 21. Exploración

La exploración será básica y estará centrada en obtener información, no en recorrer manualmente superficies planetarias.

Puede permitir descubrir:

- cuerpos orbitales;
- estaciones;
- recursos;
- anomalías;
- señales;
- restos;
- bases ocultas;
- rutas;
- presencia militar.

Los sensores instalados condicionarán qué información puede obtenerse.

---

# 22. Misiones e historia

Existirá una historia principal y misiones secundarias.

Tipos potenciales:

- transporte;
- contrabando;
- escolta;
- búsqueda y rescate;
- reconocimiento;
- patrulla;
- interceptación;
- caza de naves;
- recuperación de cargamento;
- investigación de señales;
- entrega o venta de información;
- sabotaje.

Las misiones pueden evolucionar al descubrir nueva información.

---

# 23. Oficiales y tripulación

Los oficiales son personajes reclutables con habilidades que afectan al juego.

Puestos posibles, aún no cerrados:

- capitán;
- oficial ejecutivo;
- navegación;
- ingeniería;
- sensores;
- guerra electrónica;
- armas;
- drones;
- médico.

La tripulación genérica no se gestiona como individuos y tiene un nivel general de experiencia.

---

# 24. Interfaz táctica

## 24.1. Vista principal

Cámara 3D en tercera persona alrededor de la nave.

La escena 3D es parte del sistema de control y permite:

- orientar la cámara;
- seleccionar ecos y amenazas;
- apuntar directamente sobre el espacio;
- observar misiles, drones y naves;
- comprender la geometría del enfrentamiento.

## 24.2. Interfaz de detección

El jugador debe poder:

- elegir sensor activo;
- elegir banda de distancia;
- comprender el arco efectivo;
- ejecutar un barrido;
- ver los ecos obtenidos;
- distinguir visualmente ecos recientes y antiguos;
- consultar la información específica que proporcione cada eco.

No debe mostrarse una posición real oculta ni una correlación automática inexistente.

## 24.3. Interfaz de disparo

El disparo de armas guiadas se mantiene deliberadamente simple.

Para un misil:

1. seleccionar el modelo de misil;
2. seleccionar el número de misiles de la salva cuando el lanzador permita varios disparos simultáneos;
3. hacer clic en la pantalla para indicar la dirección inicial;
4. disparar.

Para un torpedo:

1. seleccionar el modelo de torpedo;
2. seleccionar la banda de activación: corta, media, larga o extrema;
3. hacer clic en la pantalla para indicar la dirección inicial;
4. disparar.

Para un señuelo:

1. seleccionar el modelo de señuelo;
2. seleccionar la banda de activación;
3. hacer clic en la pantalla para indicar la dirección inicial;
4. lanzar.

El seeker, su Angle y el resto de prestaciones pertenecen al modelo del arma y no se ajustan manualmente durante cada disparo.

## 24.4. Interfaz defensiva

Cuando una amenaza alcanza la calidad de detección necesaria para una defensa compatible, aparece un indicador claro.

El jugador selecciona la defensa y hace clic sobre la amenaza.

Debe evitarse abrir menús complejos durante ventanas de reacción cortas.

---

# 25. Reglas globales ya fijadas

1. Combate visual en tercera persona.
2. Ritmo lento y deliberado.
3. Control completo solo de la nave del jugador.
4. Varias naves aliadas posibles mediante órdenes de alto nivel.
5. No existen HP.
6. Un impacto antinave directo suele producir mission kill o destrucción.
7. Las naves sobreviven evitando impactos, no absorbiéndolos.
8. Detección imperfecta y basada en ecos.
9. El estado real del mundo está separado de la información conocida.
10. Los sensores activos trabajan mediante barridos discretos.
11. La detección es determinista.
12. El azar solo introduce desviación en las mediciones cuando existe detección.
13. Sensibilidad y precisión son estadísticas independientes.
14. Ningún sensor maximiza ambas.
15. La huella energética crece rápidamente con prestaciones altas.
16. La huella energética es el trade-off general por defecto de los sistemas.
17. La generación eléctrica consume espacio y limita de forma emergente la configuración de la nave.
18. Una nave puede carecer de cualquier familia concreta de sensores.
19. Existen al menos detección de firma y detección energética.
20. Firma y huella energética se comportan de forma diferente.
21. Los sensores pasivos son deliberadamente limitados.
22. Los sensores activos son direccionales y especialmente buenos hacia el morro.
23. Los ecos no se correlacionan automáticamente entre barridos.
24. Convoyes de naves similares pueden dificultar el seguimiento individual.
25. El entorno modifica tanto detección como precisión.
26. Los cuerpos celestes pueden bloquear firma y enmascarar detecciones.
27. El polvo afecta especialmente a firma.
28. Las estrellas enmascaran fuertemente la detección energética.
29. Los misiles se disparan hacia puntos elegidos por el jugador.
30. El seeker define el compromiso entre tolerancia al error y tiempo de reacción del defensor.
31. Las defensas evitan impactos; no convierten la nave en un tanque de HP.
32. Ningún sistema, arma, misil, defensa o nave debe ser perfecto.
33. Las naves muy grandes son doctrinalmente vulnerables por su enorme detectabilidad.
34. Las grandes unidades necesitan escolta y no constituyen una progresión automática hacia 'mejor nave'.
35. El Jammer aumenta de forma extrema la huella energética pero degrada fuertemente la precisión y la identificación de los sensores enemigos.
36. Los barridos activos se ejecutan tras un retardo dependiente de la distancia y evalúan el estado real del objetivo en ese momento.
37. Las bandas de distancia son intervalos discretos, estrictos y sin solapamiento.
38. Una nave puede instalar como máximo dos sensores activos, pero solo utilizar uno a la vez.
39. La identificación progresa desde objeto hasta modelo/clase exacta y no se degrada una vez alcanzada.
40. Los sensores energéticos tienen una penalización base a la identificación respecto a los sensores de firma.
41. La huella energética de un dispositivo existe mientras permanezca activo, salvo excepciones específicas definidas por el propio componente.
42. Los sensores defensivos son pasivos, energéticos y omnidireccionales en principio, pero los motores ciegan su sector trasero y los sensores activos ciegan su sector delantero.
43. La mayoría de contramedidas necesitan sensores defensivos para detectar y marcar misiles entrantes.
44. Los sensores pasivos direccionales permiten localizar huellas energéticas sin emitir, pero solo a corta distancia, con orientación casi perfecta y bajo condiciones de muy baja firma y huella propia.
45. Los sensores pasivos direccionales tienen Sensibilidad, Precisión y Huella energética y siguen la penalización de identificación de los sensores energéticos.
46. Los sensores defensivos funcionan continuamente mientras están activos y son normalmente un sistema encendido de forma permanente.
47. El motor principal crea un sector trasero completamente ciego para sensores defensivos mientras está funcionando.
48. Un sensor activo crea un sector delantero completamente ciego para sensores defensivos mientras permanece activo.
49. Los sensores defensivos identifican progresivamente los misiles detectados hasta conocer su modelo exacto al 100 %.
50. Los sensores defensivos pueden distinguir si un barrido enemigo es de firma o de energía, pero no pueden localizar al emisor.
51. Los sensores pasivos direccionales funcionan continuamente y no requieren seleccionar tipo, banda ni ejecutar barridos.
52. La firma física y la huella energética propias aplican una penalización exponencial a la Sensibilidad de los sensores pasivos direccionales.
53. Los sensores pasivos direccionales heredan las reglas ambientales, de eco e identificación de los sensores energéticos y sufren el Jammer cuando observan objetivos situados dentro de su área de efecto, aunque no pueden detectar la fuente del Jammer por sí solos.
54. Los cascos determinan los slots de sensores pasivos; no existe un máximo global adicional.
55. Los misiles interceptores son la contramedida directa más eficaz, pero necesitan detección temprana y tienen munición voluminosa y limitada.
56. El láser defensivo tiene munición infinita y ahorra espacio de almacenamiento, pero es una defensa terminal menos eficaz y aumenta mucho la huella energética mientras está activo.
57. La defensa cinética es más eficaz que el láser a corta distancia y tiene modos de fuego bajo y alto que intercambian eficacia por consumo de munición.
58. Los señuelos son objetos físicos autónomos lanzados en una dirección y programados para activarse tras recorrer una banda de distancia; pueden parecer naves hasta que la identificación suficiente revela que son señuelos.
59. Los señuelos pueden utilizarse tanto defensivamente como para engaño táctico, distracción y preparación de emboscadas.
60. Maniobra, apagado de sistemas y apagado del motor principal forman parte de la defensa indirecta mediante control de firma y huella.
61. La distancia degrada tanto la Sensibilidad como la Precisión de los sensores.
62. Los sensores defensivos tienen Precisión normalmente muy alta y deben localizar exactamente las amenazas para habilitar armas y contramedidas.
63. Los sensores defensivos pueden detectar e identificar naves y otros objetos energéticos que entren dentro de su corto alcance.
64. Las armas defensivas pueden disparar contra naves localizadas por sensores defensivos cuando el blanco se encuentra dentro de su alcance.
65. Algunas naves civiles, policiales, piratas o auxiliares pueden depender exclusivamente de sensores y armas defensivas; otras pueden carecer completamente de armamento y sensores defensivos.
66. La velocidad absoluta de una nave no aumenta su firma física.
67. El uso del motor principal durante aceleración o desaceleración aumenta fuertemente la firma mediante la estela de propelente.
68. Una nave puede acelerar, apagar motores y continuar a gran velocidad por inercia con una firma mucho menor.
69. El Jammer afecta a sensores de firma y energéticos de forma distinta: la penalización es moderada para firma y muy alta para energía.
70. El Jammer no reduce la Sensibilidad energética contra su emisor; su enorme huella hace que detectarlo con un sensor activo energético sea muy fácil aunque localizarlo con precisión sea difícil.
71. La Huella energética de un dispositivo representa también su consumo eléctrico; no existe una estadística separada de consumo para cada componente.
72. El Jammer es omnidireccional y crea un área volumétrica fija centrada en la nave emisora.
73. La interferencia del Jammer depende de estar dentro de su área de efecto, no de la distancia entre el observador y el emisor.
74. El Jammer tiene potencia fija y se define principalmente por Interference, Energy footprint y Area of effect.
75. El Jammer afecta por igual a aliados y enemigos situados dentro de su campo, incluidos los sensores de la propia nave emisora.
76. Los campos de varios Jammers pueden solaparse, pero sus penalizaciones no se acumulan.
77. Los sensores defensivos son energéticos y se ven fuertemente afectados por el Jammer.
78. Los sensores pasivos no detectan la fuente de un Jammer; para localizarla se necesitan sensores activos.
79. El Jammer puede degradar seekers activos y hacerles perder un lock, aplicando las mismas reglas de sensor sin una tirada abstracta de éxito.
80. El Jammer no reduce identificación ya obtenida ni altera ecos anteriores; solo degrada nuevas mediciones y progreso futuro.
81. Todos los dispositivos pueden tener un tiempo de activación entre la orden de encendido y el inicio efectivo de su funcionamiento.
82. Apagar el Jammer elimina inmediatamente su interferencia una vez desactivado.
83. El jugador puede necesitar apagar el Jammer cuando los misiles se aproximan para que los sensores defensivos recuperen suficiente Precisión y puedan habilitar las contramedidas.
84. Existen dos familias principales de armas ofensivas guiadas: misiles activos y torpedos de aproximación inerte.
85. Todo misil o torpedo utiliza un seeker que funciona como un pequeño sensor activo y puede ser de firma o de energía.
86. El Angle del seeker intercambia tolerancia al error por Huella energética y detectabilidad.
87. Los misiles utilizan motor desde el lanzamiento y buscan velocidad, persecución y saturación.
88. Los torpedos son lanzados inertes mediante catapulta electromagnética y no activan motor ni seeker hasta alcanzar la banda de distancia de activación programada.
89. Un torpedo inerte conserva velocidad por inercia, consume prácticamente cero energía propia y presenta una firma mínima por su pequeño tamaño.
90. El alcance útil de un arma guiada depende de su combustible disponible para acelerar, maniobrar y perseguir; una vez agotado sigue por inercia pero pierde capacidad de persecución.
91. Los torpedos suelen conseguir mayor alcance porque conservan combustible durante la fase inerte.
92. Los misiles suelen llevar cargas explosivas menores porque dedican más volumen a combustible y propulsión.
93. Un impacto directo antinave suele ser letal, pero una detonación cercana también puede causar daños graves según carga, distancia y blindaje.
94. La Precision de un seeker existe y funciona como en cualquier sensor, pero suele ser menos crítica en fase terminal porque el error absoluto disminuye fuertemente al reducirse la distancia al blanco.
95. Los seekers pueden ser de firma o de energía y heredan las interacciones ambientales y de Jammer de su familia de sensor.
96. Los seekers realizan mediciones periódicas con las mismas reglas básicas de barrido y propagación que los sensores activos.
97. El seeker usa IFF para excluir amigos y, entre los blancos válidos, selecciona el más cercano al centro de su cono.
98. Misiles y torpedos son fire-and-forget: después del lanzamiento no reciben datalink, correcciones ni retargeting manual.
99. Si un seeker pierde el lock, el arma continúa hacia la última posición conocida mientras intenta reacquirir un blanco válido.
100. Los motores tienen una característica Maneuverability independiente de Acceleration; maniobrar consume muy poco combustible comparado con acelerar o desacelerar.
101. No existe velocidad máxima artificial: un objeto puede seguir acelerando mientras disponga de combustible.
102. Los torpedos conservan dirección y orientación durante su fase inerte.
103. La velocidad inicial de un torpedo depende de su catapulta electromagnética.
104. Los sensores defensivos pueden detectar la emisión de un seeker que está buscando la nave y generar una alerta de targeting sin conocer todavía la posición del arma.
105. Un torpedo inerte tiene una firma tan pequeña que detectarlo antes de activarse requiere normalmente condiciones excepcionales y un sensor de firma muy sensible a corta distancia.
106. Los componentes de misiles y torpedos contribuyen a firma y Huella energética mediante las mismas reglas que cualquier otro dispositivo.
107. La ojiva detona por contacto o cuando el arma es destruida después de estar armada; no existe por defecto espoleta de proximidad.
108. Destruir una ojiva armada demasiado cerca puede seguir causando daños graves; la distancia de intercepción y el blindaje importan.
109. Cada arma tiene una distancia mínima de armado relacionada con la seguridad de la nave lanzadora y potencialmente con la potencia de la carga.
110. Los lanzadores determinan reload time; los de torpedos determinan además velocidad inicial, y algunos lanzadores de misiles permiten salvas normalmente de 1 a 4 armas.
111. Los modelos de misil y torpedo tienen capacidad interna para componentes, pero son configuraciones prefabricadas y no personalizables por el jugador.
112. Un arma fallida continúa por inercia y puede persistir como objeto lógico aunque deje de simularse como objeto 3D completo.
113. Misiles y torpedos heredan la velocidad de la nave lanzadora; los torpedos suman además el impulso proporcionado por su catapulta.
114. Los lanzadores tienen arcos físicos, pero la nave puede seleccionar automáticamente el lanzador adecuado o reorientarse para efectuar el disparo.
115. La adquisición del seeker utiliza posiciones estimadas, no posiciones reales ocultas, y expande progresivamente su zona angular de búsqueda hasta su Angle máximo.
116. La selección de blanco prioriza cercanía al eje del cono y después proximidad al seeker.
117. Cada arma puede definir si permite reacquisition; con ella activa puede cambiar de blanco tras perder lock, y con ella desactivada permanece comprometida con el objetivo original.
118. Scan interval es una característica del seeker.
119. Los seekers no utilizan bandas de distancia seleccionables y observan todo su cono.
120. El retraso inicial de seeker en misiles, cuando exista, es fijo por modelo.
121. Todo misil o torpedo dispone de generación energética propia suficiente para alimentar sus sistemas activos.
122. Destruir una ojiva antes de su distancia mínima de armado no provoca la detonación principal.
123. Los misiles de una misma salva no coordinan reparto de objetivos.
124. Los interceptores son misiles defensivos de menor alcance y velocidad típica, pero mayor Maneuverability que los misiles ofensivos.
125. Los interceptores son guiados externamente por los sensores defensivos de la nave lanzadora y dependen de la posición estimada que estos proporcionan.
126. La degradación o pérdida de la solución del sensor defensivo degrada directamente el guiado de los interceptores.
127. Si se pierde temporalmente la solución, el interceptor continúa hacia la última posición estimada y reanuda correcciones cuando vuelve a recibir una solución válida.
128. La cadencia de guiado del interceptor es la cadencia de medición útil del sensor defensivo que lo guía.
129. Los interceptores usan cargas explosivas de proximidad cuya detonación es ordenada por los sensores defensivos cuando estiman que el interceptor está a distancia adecuada.
130. Un error de Precision del sensor defensivo puede hacer fallar la detonación de proximidad del interceptor.
131. Una explosión de interceptor puede destruir simultáneamente varias amenazas si están dentro de su radio efectivo.
132. Los interceptores pueden atacar naves detectadas por sensores defensivos, aunque su baja potencia los hace poco eficaces contra blancos blindados.
133. Todas las defensas activas salvo los señuelos dependen de los sensores defensivos para localizar y seguir amenazas.
134. El láser defensivo dispara pulsos cortos y acumula Damage/Heat mediante impactos sucesivos.
135. Los misiles suelen necesitar aproximadamente 2 o 3 impactos de un láser defensivo típico para ser destruidos, aunque depende del modelo.
136. El alcance práctico del láser depende principalmente del sensor defensivo y no tiene por ahora un límite artificial independiente.
137. Los láseres defensivos tienen Damage/Heat, Tracking speed/Mobility, Active energy footprint, Firing energy footprint, Activation delay y arco de tiro.
138. Un emisor láser solo puede atacar un objetivo cada vez; el jugador puede crear una cola manual y se respeta el orden de selección.
139. El láser debe mantener seguimiento durante cada pulso y un error de Precision puede hacer que falle.
140. Destruir con láser un arma activa y armada puede detonar su ojiva; destruir un torpedo todavía inerte no provoca la explosión antinave principal.
141. La defensa cinética comparte guiado, Tracking speed/Mobility, Activation delay, arco de tiro y cola manual de objetivos con el láser defensivo.
142. La defensa cinética tiene una Huella energética activa menor que el láser y disparar apenas incrementa esa Huella.
143. La munición cinética es limitada.
144. La defensa cinética tiene modos de fuego que intercambian consumo de munición por probabilidad de impacto.
145. El modo alto aumenta mucho la densidad de fuego y la probabilidad de impacto, pero consume munición extremadamente rápido.
146. El modo bajo conserva munición a cambio de una probabilidad de impacto menor.
147. Los señuelos no dependen de sensores defensivos y funcionan de forma completamente autónoma después del lanzamiento.
148. Los señuelos no tienen motor principal: mantienen por inercia su velocidad y trayectoria iniciales hasta y después de activarse.
149. Al activarse, un señuelo imita firma física y Huella energética compatibles con una nave indeterminada, pero no puede imitar deliberadamente una clase o modelo concreto.
150. Los sensores sufren una penalización adicional de Precision al localizar un señuelo activo.
151. Los señuelos tienen una penalización específica a la identificación; durante la identificación parcial pueden ser clasificados aleatoriamente como distintas naves.
152. Cuando la identificación alcanza certeza suficiente, el objeto se revela como DECOY/SEÑUELO.
153. Mientras no haya sido correctamente identificado como señuelo, puede ser adquirido normalmente por seekers enemigos.
154. El armamento ofensivo definido actualmente se limita a misiles y torpedos; no existe una familia de armas cinéticas ofensivas.
155. Las naves no tienen HP globales; el daño se resuelve localmente sobre compartimentos, componentes, tripulación y atmósfera.
156. Las fuentes de daño se caracterizan como mínimo por Damage, Penetration, Area of effect y Breach.
157. Si Penetration no supera Armor no se transfiere Damage; entre penetración marginal y amplia el Damage transferido aumenta progresivamente hasta el 100 %.
158. Ningún blindaje puede detener completamente un impacto directo de un misil o torpedo antinave.
159. Los compartimentos y componentes usan estados discretos como Intacto/Operativo, Dañado y Destruido, no barras de HP globales.
160. Cada compartimento mantiene su propia atmósfera y puede aislarse mediante mamparos estancos.
161. Breach determina la capacidad de un ataque penetrante para provocar pérdida de presión; láseres suelen tener Breach bajo, cinéticas defensivas alto y misiles/torpedos muy alto.
162. El control de daños repara automáticamente componentes dañados cuando existe tripulación y condiciones habitables, pero no puede reparar componentes destruidos.
163. Las brechas leves pueden contenerse durante combate; las graves o catastróficas requieren aislar el compartimento.
164. Mission kill y pérdida total emergen de capacidades perdidas, tripulación, presión y destrucción local, no de un umbral de HP.

---

# 26. Elementos pendientes de diseño

Quedan por concretar, entre otros:

- valores y nombres de las bandas de distancia;
- fórmula definitiva de detección;
- fórmula definitiva de precisión;
- distribución estadística del error de eco;
- perfiles angulares exactos de sensores;
- modelos concretos de sensores defensivos y pasivos direccionales;
- valores exactos de Precisión de sensores defensivos;
- valores exactos de los sectores ciegos de sensores defensivos;
- curva exacta de penalización exponencial por firma y huella propia en sensores pasivos direccionales;
- retardos exactos de propagación por banda de distancia;
- progresión exacta de identificación por eco;
- penalización exacta de identificación de sensores energéticos;
- valores concretos de firma y huella energética;
- modelo de generación eléctrica;
- tamaños y espacio interno de cascos;
- curva exacta energía/rendimiento;
- movimiento y aceleración;
- duración, persistencia y magnitud exacta de la firma producida por estelas de propelente;
- tiempos de viaje y cinemática de misiles y torpedos;
- valores concretos de aceleración, combustible y velocidad inicial;
- definición exacta de las bandas de activación de torpedos;
- intervalo de medición de seekers;
- seekers concretos y sus perfiles de Angle, Sensitivity, Precision y Energy footprint;
- modelos de cargas explosivas y radios efectivos de daño;
- criterio técnico de persistencia de misiles y torpedos perdidos;
- comportamiento final de guiado: persecución simple frente a intercepción predictiva;
- valores y disponibilidad de la opción reacquisition por modelo;
- arcos concretos de lanzadores y lógica de auto-orientación de la nave;
- guerra electrónica;
- valores concretos y fórmula de Interference de Jammers;
- tamaños de área y Huella energética de modelos de Jammer;
- regla de prioridad para Jammers solapados de distinta potencia;
- tiempos de activación de dispositivos;
- fórmula exacta de detonación de proximidad del interceptor;
- radios efectivos y potencias de cargas explosivas de interceptores;
- comportamiento de detonaciones múltiples cuando una explosión alcanza varias ojivas enemigas;
- valores concretos de Damage/Heat de láseres defensivos;
- duración y cadencia de pulsos;
- valores de Tracking speed/Mobility;
- huellas Active y Firing;
- Activation delay y arcos concretos de láseres defensivos;
- fórmula exacta de probabilidad de impacto de defensa cinética;
- consumo concreto de munición por modo;
- cadencia/densidad de fuego de cada modo;
- valores de Tracking speed/Mobility y Activation delay de defensas cinéticas;
- valores concretos de penalización de Precision e identificación de señuelos;
- duración/autonomía de la imitación activa del señuelo;
- modelos concretos de señuelos y sus firmas/Huellas energéticas simuladas;
- velocidad inicial y características de sus lanzadores;
- drones;
- curva exacta de falloff de Damage y Penetration en explosiones;
- valores de resistencia estructural de compartimentos y Resistance de componentes;
- tablas o fórmulas de probabilidad de estado Dañado/Destruido;
- valores y fórmula exacta de Breach y fuga de atmósfera;
- modelo de Pressure/Air y propagación entre compartimentos conectados;
- reglas exactas de bajas por impacto y descompresión;
- velocidad y requisitos del control de daños;
- condiciones funcionales concretas para mission kill y pérdida total;
- comportamiento de IA;
- automatización permitida;
- interfaz definitiva;
- economía y progresión;
- facciones y lore detallado;
- estructura exacta de campaña y misiones.

---

# 27. Criterio de diseño para futuras decisiones

Al añadir cualquier sistema o componente deben responderse al menos estas preguntas:

1. ¿Qué problema resuelve?
2. ¿En qué condiciones es especialmente bueno?
3. ¿Qué alternativa hace algo mejor que él?
4. ¿Qué energía consume y qué huella produce?
5. ¿Qué espacio o infraestructura obliga a sacrificar?
6. ¿Qué decisiones ofrece al jugador durante el uso?
7. ¿Puede el jugador comprender por qué ha tenido éxito o ha fallado?

La prioridad es mantener un juego fácil de controlar pero con un techo de habilidad alto, en el que la profundidad provenga de información, geometría, configuración, entorno y decisiones, no de interfaces innecesariamente complejas ni de porcentajes opacos.