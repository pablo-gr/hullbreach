# Hullbreach — Especificación de diseño del juego

**Estado:** Documento vivo de diseño
**Versión:** 1.1
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

Los sensores defensivos son ópticos. Los sensores pasivos direccionales detectan energía.

Ninguno necesita emitir un barrido activo para funcionar.

La detección pasiva es determinista: dadas exactamente las mismas condiciones, un objetivo se detecta o no se detecta siempre del mismo modo.

## 11.1. Sensores defensivos

Los sensores defensivos son el tipo de sensor pasivo más común y normalmente permanecen encendidos durante toda la operación de la nave.

Funcionan continuamente mientras están activos; el jugador no ejecuta barridos manuales.

Su función principal es detectar misiles que se aproximan, marcarlos y habilitar el uso de las contramedidas que requieran una amenaza detectada.

La mayoría de las contramedidas necesitan sensores defensivos para poder emplearse contra un misil.

### 11.1.1. Características

Los sensores defensivos tienen tres características principales:

- **Sensibilidad:** capacidad para detectar objetos próximos mediante el sistema óptico.
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

si estos se encuentran dentro de su corto alcance y superan el umbral de detección óptica.

Normalmente las naves enemigas no se aproximarán tanto, por lo que su uso principal sigue siendo defensivo. Pero una nave que entre en la burbuja de detección de un sensor defensivo puede ser localizada aunque la nave observadora carezca de sensores de búsqueda activos.

Una nave con mejores sensores defensivos puede marcar una amenaza antes y mantener disponibles más capas de contramedidas.

### 11.1.4. Identificación

Los objetos detectados por sensores defensivos participan en un proceso de identificación progresiva.

En el caso de un misil, mientras el sensor defensivo mantiene la detección aumenta con el tiempo un porcentaje de identificación hasta alcanzar el 100 %.

Antes del 100 % la clasificación puede ser incompleta o incorrecta.

Al alcanzar el 100 % se conoce exactamente el modelo de misil.

Las naves y otros objetos detectados a corto alcance siguen igualmente las reglas generales de identificación progresiva, sin aplicar por ello la penalización base propia de los sensores energéticos.

La detección y la identificación son independientes de la efectividad posterior de las armas o contramedidas.

### 11.1.5. Detección de barridos activos enemigos

Los sensores defensivos también pueden detectar que un barrido de sensor activo enemigo ha alcanzado o está buscando la zona donde se encuentra la nave.

Pueden distinguir si se trata de:

- un sensor de firma;
- un sensor energético.

No proporcionan ninguna otra información útil sobre el emisor:

- no localizan su posición;
- no proporcionan bearing;
- no generan un eco;
- no identifican la nave emisora.

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

Los sensores defensivos son ópticos y no pertenecen a las familias energética o de firma.

Por tanto, el Jammer no los interfiere.

Pueden seguir detectando y localizando misiles u otros objetos dentro de su corto alcance aunque la propia nave tenga el Jammer activo.

Sus limitaciones siguen siendo las ya definidas por alcance, orientación y cegamiento causado por motores o sensores activos.

## 12.7. Sensores pasivos

Los sensores pasivos no detectan la existencia de un Jammer por su emisión.

En particular:

- un sensor defensivo no genera una alerta de Jammer;
- un sensor pasivo direccional no localiza automáticamente la fuente del Jammer.

La fuente debe ser detectada mediante sensores activos.

Un sensor pasivo direccional sigue estando sujeto a la interferencia del campo cuando intenta observar objetos dentro del área del Jammer, porque funcionalmente trabaja sobre energía.

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
- perjudica también a los sensores propios afectados;
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

# 14. Ataque con misiles

## 14.1. Flujo básico

1. El jugador selecciona un eco o una zona de interés.
2. La cámara puede orientarse hacia esa dirección.
3. Selecciona un misil.
4. Configura la distancia/banda a la que se activará el seeker.
5. Configura, cuando corresponda, la apertura del seeker.
6. Hace clic directamente en un punto del espacio.
7. El misil se dirige hacia ese punto.
8. Al cumplir la condición programada activa el seeker.
9. Si encuentra un blanco válido dentro de su volumen de búsqueda, intenta adquirirlo.
10. Si no encuentra nada, el disparo falla.

El misil no conoce mágicamente la posición real del enemigo.

## 14.2. Seeker amplio

Un seeker amplio:

- tolera errores grandes de posición;
- facilita disparos con pocas observaciones;
- debe activarse en condiciones que normalmente hacen el ataque más detectable;
- proporciona más tiempo para reaccionar;
- es más vulnerable a contramedidas que dependen de tiempo.

## 14.3. Seeker estrecho

Un seeker estrecho:

- exige una estimación precisa de posición y movimiento;
- permite activación más tardía;
- es más difícil de detectar a tiempo;
- deja menos margen para contramedidas;
- castiga mucho un mal cálculo del disparo.

Principio:

> Mayor tolerancia al error implica mayor exposición. Menor tolerancia al error permite mayor sorpresa.

## 14.4. Habilidad del jugador

El jugador puede disparar tras uno o dos ecos usando un seeker amplio o esperar varios barridos para estimar mejor el centro de la nube y utilizar un seeker más estrecho.

El ordenador puede ofrecer ayudas, pero no debe eliminar la posibilidad de que un jugador experimentado interprete mejor las observaciones.

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

Los misiles interceptores son la mejor defensa directa contra misiles enemigos.

Son más pequeños que los misiles ofensivos, pero aun así ocupan mucho espacio comparados con la munición de otras contramedidas.

Sus principales ventajas son:

- gran eficacia;
- capacidad para destruir amenazas cuando aún están lejos;
- posibilidad de proteger tanto a la propia nave como a otras naves cercanas, según la configuración futura.

Sus principales limitaciones son:

- necesitan que el misil enemigo haya sido detectado con suficiente antelación;
- requieren sensores defensivos capaces de marcar la amenaza;
- la munición es limitada;
- cada interceptor ocupa un volumen relevante de almacenamiento;
- una nave puede quedarse sin capacidad defensiva después de gastar sus interceptores.

Por ello son especialmente apropiados para escoltas defensivas especializadas.

La principal debilidad de esta capa no es una baja eficacia individual, sino el agotamiento de munición y la posibilidad de que una amenaza sea detectada demasiado tarde.

## 15.3. Láser defensivo

El láser defensivo es una defensa de última hora.

Su principal ventaja es que no utiliza munición física.

Esto produce dos beneficios:

- no puede quedarse sin munición;
- no necesita reservar espacio interno para almacenar proyectiles o interceptores.

Ese espacio puede utilizarse para otros sistemas.

Por esta razón es una defensa muy popular incluso en naves que ya disponen de interceptores.

### 15.3.1. Limitaciones

El láser es menos efectivo que los misiles interceptores.

Está pensado para destruir uno o varios misiles que hayan atravesado las capas anteriores, no para defender por sí solo una nave frente a una salva importante.

Algunas naves con poca capacidad defensiva pueden utilizarlo como única defensa directa.

### 15.3.2. Huella energética y preparación

Mientras está activo, el láser defensivo incrementa mucho la huella energética de la nave.

Por esta razón normalmente se mantiene apagado y se activa cuando existe una amenaza.

El jugador debe recordar encenderlo con suficiente antelación para que pueda utilizarse cuando el misil entre en su ventana defensiva.

Esto convierte su uso en una decisión táctica:

- mantenerlo apagado favorece el sigilo;
- encenderlo permite defenderse pero incrementa significativamente la detectabilidad energética.

## 15.3.3. Uso contra naves

Las armas defensivas no están restringidas artificialmente a misiles.

Si los sensores defensivos detectan y localizan una nave enemiga dentro de su alcance, las armas defensivas capaces de alcanzarla pueden disparar contra ella.

Esto permite que una nave sin sensores activos pueda combatir a muy corta distancia utilizando únicamente:

- sensores defensivos;
- láser defensivo;
- defensa cinética;
- otras armas defensivas compatibles que se definan más adelante.

Estas armas siguen estando optimizadas para defensa terminal y no sustituyen a un armamento ofensivo dedicado a distancias tácticas normales.

## 15.4. Defensa cinética

La defensa cinética es también una defensa de última hora.

Es más efectiva que el láser defensivo, pero consume munición.

Tiene dos modos de disparo.

### 15.4.1. Modo bajo

El modo bajo:

- consume munición lentamente;
- permite mantener la defensa activa durante más tiempo;
- ofrece una eficacia similar o solo moderadamente superior a la del láser.

Está pensado para conservar munición cuando la amenaza no justifica el máximo consumo.

### 15.4.2. Modo alto

El modo alto:

- utiliza una cadencia de fuego muy elevada;
- puede destruir misiles con gran eficacia;
- consume la munición extremadamente rápido.

Durante un periodo corto puede convertirse en una defensa antimisil muy potente, pero una salva prolongada o varias oleadas pueden vaciar rápidamente sus reservas.

La elección de modo permite al jugador intercambiar conservación de munición por capacidad inmediata de supervivencia.

## 15.5. Señuelos

Los señuelos son objetos físicos reales lanzados por la nave.

No generan simplemente un eco ficticio en la interfaz.

El jugador los utiliza de forma similar a un misil:

1. selecciona un punto del espacio;
2. configura una distancia o condición de activación;
3. lanza el señuelo;
4. el señuelo viaja hasta la posición programada;
5. al activarse comienza a simular las características de una nave.

Una vez activo, el señuelo debe ser especialmente difícil de identificar correctamente.

Los sensores pueden detectarlo como un objeto real y comenzar su proceso normal de identificación.

Durante ese proceso puede parecer:

- un objeto desconocido;
- una nave;
- un tipo de nave plausible.

Solo al alcanzar suficiente identificación puede descubrirse que en realidad es un señuelo.

### 15.5.1. Uso táctico

Los señuelos no sirven únicamente para defenderse de un misil ya lanzado.

Pueden utilizarse de forma ofensiva y estratégica para manipular la información del enemigo.

Ejemplos:

- hacer creer que una nave se encuentra en otra posición;
- provocar un barrido activo enemigo;
- atraer una patrulla;
- hacer gastar misiles;
- saturar la interpretación de ecos;
- preparar una emboscada;
- simular una aproximación o retirada.

Conceptualmente equivalen a lanzar una distracción en un juego de sigilo: su valor depende mucho de dónde y cuándo se utilicen.

El diseño detallado de qué firma y huella pueden imitar, cuánto dura el engaño y cómo interactúan con seekers se definirá en el apartado específico de contramedidas.

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

- penalización muy alta para sensores energéticos;
- penalización moderada para sensores de firma;
- sin efecto sobre sensores defensivos ópticos.

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

Las armas no deben diferenciarse principalmente por daño.

Principio:

> Cada arma define qué problema debe resolver el jugador para conseguir un impacto.

Ejemplos todavía preliminares:

- misiles: estimación, programación y seeker;
- armas cinéticas: adelanto y tiempo de vuelo;
- láseres: solución precisa, línea de visión y mantenimiento del seguimiento;
- drones: posicionamiento, sensores, control espacial, saturación o designación.

Ningún misil, defensa o arma debe ser perfecto.

---

# 18. Daño

Un impacto se resuelve físicamente sobre la nave:

impacto -> blindaje -> penetración -> compartimento -> sistemas/tripulación/estructura.

Posibles consecuencias:

- perforación;
- despresurización;
- incendios;
- bajas;
- destrucción de sensores;
- destrucción de armas;
- pérdida de propulsión;
- pérdida de generación;
- explosión de munición;
- daño de reactor;
- mission kill;
- destrucción completa.

Un impacto antinave directo suele ser catastrófico.

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

Flujo objetivo:

1. seleccionar eco/zona;
2. seleccionar misil;
3. ajustar seeker;
4. ajustar condición de activación;
5. hacer clic sobre el punto de espacio deseado;
6. disparar.

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
42. Los sensores defensivos son pasivos, ópticos y omnidireccionales en principio, pero los motores ciegan su sector trasero y los sensores activos ciegan su sector delantero.
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
58. Los señuelos son objetos físicos lanzables a una posición y condición de activación; pueden parecer naves hasta que la identificación suficiente revela que son señuelos.
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
77. Los sensores defensivos son ópticos y no se ven afectados por el Jammer.
78. Los sensores pasivos no detectan la fuente de un Jammer; para localizarla se necesitan sensores activos.
79. El Jammer puede degradar seekers activos y hacerles perder un lock, aplicando las mismas reglas de sensor sin una tirada abstracta de éxito.
80. El Jammer no reduce identificación ya obtenida ni altera ecos anteriores; solo degrada nuevas mediciones y progreso futuro.
81. Todos los dispositivos pueden tener un tiempo de activación entre la orden de encendido y el inicio efectivo de su funcionamiento.
82. Apagar el Jammer elimina inmediatamente su interferencia una vez desactivado.

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
- tiempos de viaje y cinemática de misiles;
- seekers concretos;
- guerra electrónica;
- valores concretos y fórmula de Interference de Jammers;
- tamaños de área y Huella energética de modelos de Jammer;
- regla de prioridad para Jammers solapados de distinta potencia;
- tiempos de activación de dispositivos;
- comportamiento exacto de interceptores;
- parámetros y arcos de láseres defensivos;
- parámetros, cadencia y munición de defensa cinética;
- tipos, persistencia e imitación de firma/energía de señuelos;
- enlaces de datos;
- drones;
- defensas concretas;
- armas no misilísticas;
- resolución detallada de daño;
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