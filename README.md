# Detección de Llamaradas Solares
Valentina Vásques y Amelia Hoyos.

[Dataset de Erupciones solares](https://deepblue.lib.umich.edu/data/concern/data_sets/6w924c02q)

## Introducción
El Sol, especialmente en lugares donde se ubican sus manchas, es muy activo, emitiendo radiación en todas direcciones. Una erupción o llamarada solar es una de estas intensas y repentinas ráfagas de radiación. Estas varían de acuerdo con el ciclo solar de once años. Se cree que una erupción solar ocurre cuando un depósito de energía magnética acelera a gran velocidad iones presentes en el plasma solar, lo que produce radiación. Esta radiación es absorbida por la ionosfera de la Tierra. No representa un peligro directo para la vida en el planeta, sin embargo, sí provoca que la atmósfera superior se ionice, lo que puede interferir con las comunicaciones por radio, dependiendo de la energía de la llamarada solar.

Algunas veces, las llamaradas solares son acompañadas por eyecciones de masa coronal (CME), ondas de radiación y viento solar. Esto puede causar una tormenta geomagnética en la tierra, lo puede producir un efecto desastroso en las telecomunicaciones terrestres. Como estas tormentas están generalmente asociadas a erupciones solares pueden detectarse antes de que sucedan. En 1859, ocurrió algo llamado el evento Carrington, durante el cual el sol liberó una CME tan grande que en la Tierra las comunicaciones telegráficas fallaron y aparecieron auroras en toda la tierra, provocando una conmoción generalizada. En Montería, Colombia, se dio el siguiente testimonio:

<blockquote>
En Marzo de 1859 los habitantes de la ciudad contemplaron estupefactos un fenómeno celeste que semejaba un incendio de vastas proporciones. Negros nubarrones surcados a cada instante por candilejas y extraños fulgores; inmensas lenguas de llamas y deslumbrantes globos luminosos que deshacían para volver a condensarse segundos después, daban la impresión de cien volcanes en erupción. Y en el centro de aquellos inmensos espacios se formó, claramente dibujada, una enorme S que allí permaneció mientras duraba el fantástico espectáculo causado por la madrugada. Tan intensa era la claridad que podía confundirse con una aurora boreal y penetraba hasta el interior de las casas.
<br><br>
Impresionadas y temerosas las gentes se precipitaron hacia la iglesia y postradas de hinojos ante la Majestad Divina pedían, a grandes voces, que se alejaran las calamidades presagiadas por el raro fenómeno. El Padre José Luis Pezzati públicamente tomó en llamada Oración de los Siete Derramamientos de Sangre de Nuestro Señor Jesucristo queriendo explicar: “Sangre preciosa por mi amor vertida…Purifica mi alma de toda malicia.” 
<br><br> 
J. Exbrayat, Historia de Montería
Imprenta Departamental de Córdoba (1971), pp. 150-151
</blockquote>
Si algo así sucediera en la actualidad, toda la tecnología de la que dependemos dejaría momentáneamente de funcionar. Por lo tanto, es importante prepararse para un evento así y saber con anticipación si sucederá en algún momento determinado. Aquí entra en juego la detección de llamaradas solares, que como ya sabemos, son un indicador de una posible tormenta geomagnética.

## Definiciones
**Atenuador**: Un atenuador es un dispositivo que reduce la intensidad de una señal sin alterar su forma de onda. Cuando está en un estado "grueso", significa que se utiliza una configuración que reduce significativamente la intensidad de la señal. En cambio, un estado "delgado" no la reduce tanto. Si está en "ambos" estados, significa que se están utilizando estos dos tipos de configuraciones en diferentes atenuadores al realizar mediciones.

## Entendimiento del área de estudio
Los datos que usaremos son tomados de [Kaggle, Solar Flares from RHESSI Mission](https://www.kaggle.com/datasets/khsamaha/solar-flares-rhessi/data). Estos datos provienen de RHESSI, un observatorio de erupciones solares de la NASA. 

Fecha: Datos recolectados de  2002 - 2018
Tamaño: 116143 x 18

| Columna      | Tipo de dato | Tamaño máximo del dato | Descripción |
|--------------|--------------|------------------------|-------------|
| Flare        | int64        | 28                     | Un número de identificación, (y)ymmddnn, por ejemplo, 2021213 es el treceavo destello encontrado el 12 de febrero de 2002. |
| Date         |datetime64[ns]| 59                     | La fecha en que ocurrió el destello |
| Start time   |datetime64[ns]| 57                     | Hora de inicio del destello |
| Peak time    |datetime64[ns]| 57                     | Hora pico del destello |
| End time     |datetime64[ns]| 57                     | Hora de finalización del destello |
| Duration     | int64        | 28                     | Duración del destello en segundos |
| Peak counts  | int64        | 28                     | Tasa de conteos o picos de radiación por segundo detectados en un rango de energía de 6 a 12 kiloelectronvoltios (keV) durante la duración de la llamarada solar, promediados sobre todos los detectores, incluido el fondo |
| Total Counts | float64      | 24                     | Número total de conteos o picos de radiación detectados un rango de energía de 6 a 12 kiloelectronvoltios (keV) durante la duración de la llamarada solar, sumados sobre todos los detectores, incluido el fondo |
| Energy       | object       | 59                     | La banda de energía en KeV más alta en la que se observó el destello. |
| X pos        | int64        | 28                     | Posición del destello en segundos de arco desde el centro del sol |
| Y pos        | int64        | 28                     | Posición del destello en segundos de arco desde el centro del sol |
| Radial       | int64        | 28                     | Distancia radial en segundos de arco desde el centro del sol |
| Active region| int64        | 28                     | Número para la región activa más cercana, si esta disponible |
| Flags        | object       | 69                     | Códigos de calidad de la medición, sin ningún orden en particular |

**Códigos de Calidad de cada Destello:**

- a0 - En estado de atenuador 0 (Ninguno) en algún momento durante el destello
- a1 - En estado de atenuador 1 (Delgado) en algún momento durante el destello
- a2 - En estado de atenuador 2 (Grueso) en algún momento durante el destello
- a3 - En estado de atenuador 3 (Ambos) en algún momento durante el destello
- An - Estado del atenuador (0=Ninguno, 1=Delgado, 2=Grueso, 3=Ambos) en el pico del destello
- DF - Las mediciones del segmento frontal fueron decimadas en algún momento durante el destello
- DR - Las mediciones del segmento trasero fueron decimadas en algún momento durante el destello
- ED - Eclipse del vehículo espacial (noche) en algún momento durante el destello
- EE - El destello terminó en el eclipse del vehículo espacial (noche)
- ES - El destello comenzó en el eclipse del vehículo espacial (noche)
- FE - Destello en curso al final del archivo
- FR - En Modo de Tasa Rápida
- FS - Destello en curso al comienzo del archivo
- GD - Brecha de datos durante el destello
- GE - El destello terminó en una brecha de datos
- GS - El destello comenzó en una brecha de datos
- MR - Nave espacial en zona de altas latitudes durante el destello
- NS - Evento no solar
- PE - Evento de partículas: Partículas presentes
- PS - Posible destello solar; en detectores frontales, pero sin posición
- Pn - Calidad de la posición: P0 = Posición no válida, P1  = Posición válida
- Qn - Calidad de los Datos: Q0 = Calidad más Alta, Q11 = Calidad más Baja
- SD - La Nave Espacial Estaba en SAA en Algún Momento Durante el Destello
- SE - El Destello Terminó Cuando la Nave Espacial Estaba en SAA
- SS - El Destello Comenzó Cuando la Nave Espacial Estaba en SAA
