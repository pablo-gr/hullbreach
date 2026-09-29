# Hullbreach — Especificación de diseño del juego

**Estado:** Documento vivo de diseño
**Versión:** 0.4
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

> Cuanto más capaz es un sistema, más energía consume y mayor huella energética produce.

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
- velocidad.

La tripulación puede reducirla principalmente reduciendo velocidad. No puede apagarla.

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
- el objetivo puede reducir su firma principalmente reduciendo velocidad;
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

## 11.1. Cobertura

Los sensores pasivos son eficaces en prácticamente todas las direcciones excepto hacia atrás, donde existe una zona muy degradada o ciega.

## 11.2. Alcance limitado

Los sensores pasivos son deliberadamente poco eficaces.

Deben permitir que una nave enemiga bien manejada se aproxime sin ser detectada, de forma análoga al combate submarino.

Su función no es crear una burbuja perfecta de conocimiento alrededor de la nave.

## 11.3. Misiles

Los pasivos pueden detectar misiles entrantes, pero normalmente cuando ya están relativamente cerca.

El momento de detección determina qué capas defensivas siguen disponibles.

## 11.4. Pulsos de sensores activos

Los pasivos pueden advertir de que un sensor activo está buscando en la zona donde se encuentra la propia nave.

Esta detección no proporciona necesariamente la posición de la nave emisora.

En condiciones normales puede limitarse a indicar que existe actividad de sensor activo y quizá una dirección aproximada.

Triangular la posición del emisor debe ser difícil.

Utilizar un sensor activo no debe equivaler automáticamente a revelar una posición precisa al enemigo.

---

# 12. Jammer e interferencia de sensores

El Jammer es una contramedida electrónica destinada a degradar la precisión de los sensores enemigos.

## 12.1. Funcionamiento general

Cuando se activa, el Jammer emite interferencias en todas direcciones.

Su efecto principal no es impedir que la nave sea detectada. Hace exactamente lo contrario: incrementa de forma extrema la huella energética de la nave.

Una nave utilizando un Jammer debe resultar extraordinariamente fácil de detectar mediante sensores energéticos y, en condiciones normales, incluso los sensores pasivos deben poder ubicarla con mucha más facilidad de lo habitual.

La contrapartida es que la interferencia degrada enormemente la precisión de las mediciones enemigas.

Por tanto, el Jammer crea una situación deliberadamente paradójica:

> El enemigo sabe que estás ahí, pero le resulta mucho más difícil saber exactamente dónde estás.

## 12.2. Efecto sobre los ecos

El Jammer no debe convertir la detección en una tirada aleatoria ni ocultar artificialmente la existencia de la nave.

Cuando un sensor consigue detectar una nave bajo interferencia, sigue generando un eco, pero el radio máximo de error de la medición aumenta considerablemente.

Conceptualmente:

- detección: puede seguir siendo muy fácil;
- identificación de presencia: muy fácil;
- precisión de posición: muy degradada;
- progreso de identificación de clase: degradado;
- construcción de una solución de tiro: mucho más difícil.

Esto encaja con la separación fundamental entre capacidad de detección y precisión de medición.

## 12.3. Coste táctico

Activar un Jammer implica aceptar voluntariamente una huella energética enorme.

En términos de doctrina:

- no sirve para permanecer oculto;
- sirve para sobrevivir cuando el enemigo ya puede buscarte o cuando se espera un ataque;
- puede permitir romper o degradar soluciones de tiro;
- puede facilitar la supervivencia frente a misiles que dependan de una posición inicial precisa;
- puede delatar la nave a enemigos que antes no sabían dónde estaba.

Debe considerarse una herramienta de emergencia o de guerra electrónica activa, no una forma de stealth.

## 12.4. Relación con sensores pasivos

El Jammer es una de las excepciones importantes a la baja eficacia general de los sensores pasivos.

Su emisión es tan intensa que puede permitir a receptores pasivos obtener una localización mucho mejor que la que normalmente conseguirían frente a una nave discreta.

Esto no significa necesariamente una posición exacta: el propio Jammer está diseñado para contaminar las mediciones.

La relación concreta entre intensidad del Jammer, sensores pasivos, triangulación y precisión se definirá en el apartado detallado de contramedidas electrónicas.

## 12.5. Diseño pendiente

Más adelante deberán definirse:

- tipos de Jammer;
- potencia e intensidad;
- consumo energético;
- huella energética generada;
- efecto exacto sobre precisión de sensores de firma;
- efecto exacto sobre precisión de sensores energéticos;
- efecto sobre seekers de misiles;
- interacción con sensores pasivos;
- posibilidad de localizar la fuente mediante triangulación;
- modos de funcionamiento;
- arcos o carácter omnidireccional definitivo;
- contramedidas contra el Jammer;
- interacción con varias fuentes de interferencia.

Por ahora queda fijado únicamente su principio de funcionamiento: enorme exposición energética a cambio de una fuerte degradación de la precisión enemiga.

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

# 15. Defensa contra misiles

La defensa utiliza el mismo lenguaje visual que el ataque:

> mirar, detectar, seleccionar, actuar.

Un misil puede ser visualmente perceptible antes de que los sensores hayan obtenido una solución suficiente para utilizar una defensa.

El jugador puede colocar el cursor sobre la amenaza y esperar a que aparezca el indicador de detección/adquisición.

Las defensas previstas incluyen:

- misiles interceptores;
- guerra electrónica;
- señuelos;
- láseres defensivos;
- defensa puntual.

Cada sistema defensivo tendrá:

- requisitos de detección;
- una ventana temporal;
- posibles arcos de cobertura;
- limitaciones de munición, energía o capacidad;
- fortalezas frente a determinados tipos de amenaza.

No existe una defensa capaz de detener indefinidamente todos los ataques.

---

# 16. Maniobra

La maniobra no está pensada principalmente para esquivar físicamente un misil mediante reflejos.

Sirve para:

- orientar sensores;
- orientar defensas y armas;
- evitar zonas muertas;
- mantener o perder ecos;
- aprovechar cuerpos celestes y polvo;
- modificar firma mediante velocidad;
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

---

# 26. Elementos pendientes de diseño

Quedan por concretar, entre otros:

- valores y nombres de las bandas de distancia;
- fórmula definitiva de detección;
- fórmula definitiva de precisión;
- distribución estadística del error de eco;
- perfiles angulares exactos de sensores;
- tipos concretos de sensores pasivos;
- retardos exactos de propagación por banda de distancia;
- progresión exacta de identificación por eco;
- penalización exacta de identificación de sensores energéticos;
- valores concretos de firma y huella energética;
- modelo de generación eléctrica;
- tamaños y espacio interno de cascos;
- curva exacta energía/rendimiento;
- movimiento y aceleración;
- tiempos de viaje y cinemática de misiles;
- seekers concretos;
- guerra electrónica;
- diseño detallado de Jammers e interferencia;
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