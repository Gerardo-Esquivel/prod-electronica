# Diseño de circuitos y PCB con Altium Designer

Esta guía desarrolla el recorrido desde la organización del proyecto hasta la preparación de los archivos de fabricación de una placa en **Altium Designer**. Sigue las mismas etapas de aprendizaje de la guía de KiCad y utiliza las herramientas y nombres propios de Altium.

!!! info "Borrador de la práctica"

    El texto describe los pasos que debemos registrar y comprobar sobre la nueva placa. Todavía falta incorporar la versión utilizada, la función del circuito, sus parámetros reales y las capturas de cada etapa. Los procedimientos siguientes no constituyen un reporte de verificaciones ya realizadas.

??? abstract "Explorar esta guía"

    - [Datos de la placa](#datos-de-la-placa)
    - [Instalación y entorno](#instalacion-y-entorno)
    - [Proyecto y documentos](#proyecto-y-documentos)
    - [Bibliotecas y componentes](#bibliotecas-y-componentes)
    - [Editor de esquemas](#editor-de-esquemas)
    - [Validación eléctrica](#validacion-electrica)
    - [Transferencia a la PCB](#transferencia-a-la-pcb)
    - [Preparación de la placa](#preparacion-de-la-placa)
    - [Diseño y ruteo](#diseno-y-ruteo)
    - [Perforaciones y planos de cobre](#perforaciones-y-planos-de-cobre)
    - [Verificación final](#verificacion-final)
    - [Archivos de fabricación](#archivos-de-fabricacion)
    - [Plan de capturas](#plan-de-capturas)

## Datos de la placa {#datos-de-la-placa}

Antes de describir el diseño terminado, debemos registrar la información de esta práctica. Los anchos, separaciones y diámetros se tomarán del diseño y del proceso de fabricación elegido.

| Dato | Información por completar |
| --- | --- |
| Nombre y función del circuito | Qué hace la placa y cuáles son sus entradas y salidas. |
| Versión de Altium Designer | Versión y compilación usadas por el equipo. |
| Alimentación y componentes principales | Tensiones previstas, dispositivos y conectores. |
| Forma y dimensiones | Tamaño final y características del contorno. |
| Capas de cobre utilizadas | Una cara, dos caras u otra estructura. |
| Bibliotecas empleadas | Archivos locales o componentes de un Workspace. |
| Fabricación | Fresado en laboratorio o proveedor de PCB. |
| Reglas aplicadas | Anchos, aislamiento, perforaciones y distancia al borde. |

En la carpeta local de Altium se identificaron `proyecto45.SchDoc`, `PCB1.PcbDoc` y `PCB_Project45.BomDoc`. Es necesario incorporar o identificar el archivo `.PrjPcb` que organiza estos documentos y confirmar que pertenecen a la misma revisión del circuito.

??? note "Equivalencias con el recorrido de KiCad"

    | Etapa | En Altium Designer |
    | --- | --- |
    | Proyecto y archivos asociados | Proyecto `.PrjPcb`, esquema `.SchDoc` y placa `.PcbDoc`. |
    | Símbolos y huellas | Bibliotecas de esquema y PCB, o componentes de un Workspace. |
    | Revisión eléctrica del esquema | Validación del proyecto y panel **Messages**. |
    | Actualización de la placa | **Update PCB Document** y órdenes de cambio **ECO**. |
    | Contorno y capas | **Board Shape**, capas de señal y capas mecánicas. |
    | Reglas y comprobación física | Restricciones de diseño y comprobación **DRC**. |

## Instalación y entorno {#instalacion-y-entorno}

=== "Acceso al programa"

    1. Instalar Altium Designer con el instalador oficial autorizado para la práctica, si todavía no está disponible en el equipo.
    2. Iniciar el programa y comprobar el acceso a una licencia válida desde **License Management**.
    3. Registrar la versión utilizada. Esta información permitirá relacionar las capturas con los menús de esa instalación.
    4. Abrir un documento de prueba o el proyecto de la práctica y comprobar que los editores de esquema y PCB estén disponibles.

    Referencias: [instalación de Altium](https://www.altium.com/documentation/altium-designer/installation-management/installing) y [gestión de licencias](https://www.altium.com/documentation/altium-designer/installation-management/licensing).

=== "Reconocer la interfaz"

    Identificar los espacios que utilizaremos durante el diseño:

    - **Projects:** organiza los documentos asociados al proyecto.
    - **Properties:** permite editar las características del objeto seleccionado o del documento activo.
    - **Components:** permite buscar y colocar los componentes disponibles.
    - **Messages:** presenta los resultados de la validación del proyecto.
    - **Área de trabajo:** muestra el esquema o la PCB, según el documento activo.

    La captura general debe mostrar el panel de proyectos y el documento de la placa que desarrolló el equipo.

## Proyecto y documentos {#proyecto-y-documentos}

=== "Crear el proyecto"

    1. Seleccionar **File → New → Project**.
    2. Elegir un proyecto de PCB y la ubicación disponible: carpeta local o Workspace del equipo.
    3. Asignar un nombre que identifique la placa.
    4. Guardar el proyecto `.PrjPcb` y comprobar su aparición en **Projects**.

    El proyecto reúne los documentos y sus ajustes. Abrir por separado un esquema y una PCB no demuestra que ambos estén asociados al mismo proyecto.

=== "Incorporar los documentos"

    1. Desde **Projects**, agregar un esquema y un documento PCB al proyecto, o incorporar los archivos existentes mediante **Add Existing to Project**.
    2. Guardar el esquema como `.SchDoc` y la placa como `.PcbDoc`.
    3. Comprobar que aparecen debajo del mismo proyecto y guardar los cambios.
    4. Registrar qué archivos contienen el circuito y la placa finales de la práctica.

    El archivo `.BomDoc`, si forma parte de esta revisión, se utilizará para organizar la información de componentes.

Referencia: [creación de proyectos y documentos](https://www.altium.com/documentation/altium-designer/creating-projects-documents).

## Bibliotecas y componentes {#bibliotecas-y-componentes}

=== "Bibliotecas locales"

    1. Identificar las bibliotecas utilizadas: `.SchLib` para símbolos, `.PcbLib` para huellas o `.IntLib` para componentes integrados.
    2. Agregarlas al proyecto o hacerlas disponibles mediante las preferencias de bibliotecas del panel **Components**.
    3. Buscar un componente conocido y comprobar que puede colocarse en el esquema.
    4. Revisar el modelo de huella asociado y la correspondencia entre números de pin y pad.

    Referencias: [bibliotecas basadas en archivos](https://www.altium.com/documentation/altium-designer/components-libraries/file-based-libraries) y [disponibilidad de bibliotecas](https://www.altium.com/documentation/altium-designer/schematic/components-file-based-database-libraries).

=== "Componentes de Workspace"

    1. Conectarse al Workspace utilizado por el equipo, cuando corresponda.
    2. Abrir **Components**, localizar el componente y revisar sus datos y modelos antes de colocarlo.
    3. Registrar el nombre y la revisión del componente empleado.

    Esta alternativa se documentará únicamente si fue la utilizada en la práctica. La biblioteca `fablib` de KiCad no debe darse por instalada o equivalente en Altium sin comprobar su origen y compatibilidad.

    Referencia: [captura del esquema y componentes](https://www.altium.com/documentation/altium-designer/tutorial/capturing-schematic).

## Editor de esquemas {#editor-de-esquemas}

El esquema representa las conexiones lógicas del circuito. Conviene dividirlo por función: alimentación, control, entradas, salidas y conectores, según lo que realmente incluya la placa.

=== "Colocar componentes"

    1. Activar el documento `.SchDoc` y configurar la hoja y la rejilla de trabajo.
    2. Buscar cada componente en **Components** y colocarlo en el área de diseño.
    3. Revisar designadores, valores, orientación y modelos de huella desde **Properties**.
    4. Abrir **Tools → Annotation → Annotate Schematics**, revisar los designadores propuestos, aplicar los cambios y guardar el documento.

    La evidencia debe permitir relacionar los símbolos con los componentes físicos elegidos.

    Referencias: [fundamentos de captura esquemática](https://www.altium.com/documentation/altium-designer/schematic) y [anotación de componentes](https://www.altium.com/documentation/altium-designer/schematic/annotating-design-components).

=== "Conectar y etiquetar"

    1. Utilizar **Place → Wire** para realizar conexiones eléctricas entre pines.
    2. Comprobar que los extremos del cable coincidan con los puntos de conexión.
    3. Colocar etiquetas mediante **Place → Net Label** sobre los cables que deban identificarse.
    4. Usar nombres consistentes para alimentación, tierra y señales relevantes.
    5. Revisar visualmente los cruces y las uniones del circuito.

    Las etiquetas pueden conectar puntos separados de una misma hoja. En proyectos de varias hojas debe comprobarse el alcance de los identificadores y la estructura de puertos del proyecto.

    !!! tip "Conexiones y elementos gráficos"

        Un objeto **Wire** crea una conexión eléctrica. Un objeto **Line** sirve para dibujar y no sustituye al cableado del circuito.

    Referencias: [conectividad del esquema](https://www.altium.com/documentation/altium-designer/schematic/creating-circuit-connectivity) y [cables y etiquetas](https://www.altium.com/documentation/altium-designer/capturing-your-design-idea-as-a-schematic-overview).

=== "Organizar la lectura"

    1. Separar los bloques funcionales con espacio suficiente.
    2. Alinear símbolos, valores y etiquetas para reducir cruces y facilitar el seguimiento de señales.
    3. Añadir títulos y notas gráficas que expliquen cada bloque.
    4. Obtener una vista completa y detalles de las partes más importantes del circuito.

## Validación eléctrica {#validacion-electrica}

Antes de transferir el circuito, debemos revisar la coherencia eléctrica del esquema y sus ajustes de comprobación.

=== "Configurar"

    1. Abrir **Project Options** desde el proyecto.
    2. Revisar **Error Reporting** y **Connection Matrix**.
    3. Comprobar que la severidad de las verificaciones corresponda al circuito y a los tipos eléctricos de sus pines.

=== "Validar y corregir"

    1. Desde el proyecto en **Projects**, ejecutar **Validate PCB Project**.
    2. Abrir **Messages** y revisar los errores y advertencias.
    3. Localizar cada incidencia, corregirla en el esquema y repetir la validación.
    4. Guardar la revisión y conservar una captura o reporte de los resultados.

    !!! info "Qué demuestra la comprobación"

        La validación evalúa las reglas configuradas. Un resultado sin errores no sustituye la revisión del circuito, sus valores ni la correspondencia con las hojas de datos. Las advertencias aceptadas deben tener una justificación documentada.

Referencia: [validación del proyecto](https://www.altium.com/documentation/altium-designer/schematic/design-validation).

## Transferencia a la PCB {#transferencia-a-la-pcb}

La sincronización se realiza mediante una **Engineering Change Order (ECO)**, que reúne los cambios necesarios para actualizar la PCB desde el esquema.

=== "Generar los cambios"

    1. Guardar el esquema y comprobar que la PCB pertenece al mismo proyecto.
    2. Desde el editor de esquemas, seleccionar **Design → Update PCB Document** y elegir el documento correspondiente.
    3. Revisar la lista de componentes, huellas y conexiones que muestra el diálogo ECO.

=== "Aplicar y comprobar"

    1. Pulsar **Validate Changes**.
    2. Si aparecen incidencias de huella o correspondencia de pines, corregir su causa antes de continuar.
    3. Ejecutar **Execute Changes** cuando la propuesta sea correcta.
    4. Abrir la PCB y comprobar las huellas y líneas de conexión transferidas.

Referencias: [transferencia del esquema](https://www.altium.com/documentation/altium-designer/tutorial/creating-configuring-pcb-document) y [gestión de cambios entre esquema y PCB](https://www.altium.com/documentation/altium-designer/sch-pcb).

## Preparación de la placa {#preparacion-de-la-placa}

=== "Unidades y capas"

    1. Confirmar las unidades y configurar una rejilla adecuada para los componentes utilizados.
    2. Revisar la estructura física desde **Design → Layer Stack Manager**.
    3. Identificar **Top Layer** y **Bottom Layer** para cobre, **Top/Bottom Overlay** para serigrafía y las capas mecánicas utilizadas para documentación.
    4. Registrar qué capas se fabricarán realmente.

    Para una placa fresada de una sola cara, el ruteo debe respetar esa limitación. No se asumirá que las vías o los agujeros tendrán metalización.

    Referencias: [preparación del entorno PCB](https://www.altium.com/documentation/altium-designer/pcb/environment-setup) y [estructura de capas](https://www.altium.com/documentation/altium-designer/pcb/defining-layer-stack).

=== "Definir el contorno"

    1. Establecer la forma final con las herramientas de **Board Shape**.
    2. Si el borde se dibujó con líneas o arcos en una capa mecánica, comprobar que formen un contorno cerrado.
    3. Seleccionar únicamente esos objetos y utilizar **Design → Board Shape → Define Board Shape from Selected Objects**, cuando sea el procedimiento elegido.
    4. Comprobar las dimensiones y la forma resultante antes de distribuir los componentes.

    El **Board Shape** establece la extensión de la placa. Una línea mecánica, por sí sola, no demuestra que ese límite físico haya quedado definido.

    Referencia: [definición de la forma de la placa](https://www.altium.com/documentation/altium-designer/pcb/defining-board-shape).

=== "Distribuir componentes"

    1. Colocar conectores y elementos sujetos a restricciones mecánicas.
    2. Agrupar los demás componentes por función y proximidad eléctrica.
    3. Comprobar orientación, acceso y espacio para soldadura.
    4. Revisar las líneas de conexión para reducir recorridos largos o cruces evitables.

    Referencia: [colocación de componentes en la PCB](https://www.altium.com/documentation/altium-designer/pcb).

## Diseño y ruteo {#diseno-y-ruteo}

=== "Configurar restricciones"

    1. Identificar si el proyecto utiliza **Constraint Manager** o **PCB Rules and Constraints Editor**.
    2. Configurar el ancho de pistas, aislamiento entre redes, dimensiones de vías y restricciones al borde que correspondan.
    3. Registrar los valores realmente utilizados y su relación con el método de fabricación.
    4. Comprobar el alcance de cada regla: una regla general y una regla específica pueden aplicarse a grupos distintos.

    Los valores de la placa de KiCad no se copiarán automáticamente a esta placa. Deben corresponder a su circuito y a las capacidades del proceso elegido.

    Referencia: [restricciones de ruteo](https://www.altium.com/documentation/altium-designer/pcb/design-rule-types/routing).

=== "Trazar conexiones"

    1. Activar la capa de cobre prevista e iniciar **Route → Interactive Routing**.
    2. Seleccionar un pad de la red que se desea conectar.
    3. Guiar la pista hasta el destino respetando las restricciones activas.
    4. Comprobar anchos, separación y continuidad de cada recorrido.
    5. Resolver las conexiones pendientes y revisar que el diseño use únicamente las capas fabricables.

    Si se necesita un puente físico, debe representarse correctamente en el esquema y actualizarse mediante ECO. Un cambio de capa mediante una vía sólo es válido si la fabricación y el montaje lo contemplan.

    Referencia: [ruteo interactivo](https://www.altium.com/documentation/altium-designer/pcb/routing/interactive).

=== "Añadir identificación"

    1. Colocar nombre, versión y etiquetas útiles con **Place → String** o **Place → Text Frame**.
    2. Elegir la capa según el propósito del texto: serigrafía, cobre o documentación.
    3. Ajustar tamaño y ubicación para que las leyendas sean legibles y no invadan pads ni zonas críticas.
    4. Comprobar su orientación en las salidas de fabricación.

    Referencia: [objetos de texto en PCB](https://www.altium.com/documentation/altium-designer/pcb/text-objects).

## Perforaciones y planos de cobre {#perforaciones-y-planos-de-cobre}

=== "Configurar perforaciones"

    1. Revisar los agujeros de las huellas y los puntos de montaje de la placa.
    2. Seleccionar el pad correspondiente y comprobar **Hole Size** y la opción **Plated** en sus propiedades.
    3. Para un agujero mecánico, definir su diámetro, ubicación y condición no metalizada cuando corresponda.
    4. Comprobar las distancias a pistas, componentes y borde.

    El diámetro del agujero y el diámetro exterior del pad son medidas diferentes. Un círculo dibujado para documentación no sustituye la definición de una perforación en las salidas NC Drill.

    Referencia: [pads, agujeros y conectividad](https://www.altium.com/documentation/altium-designer/pcb/understanding-connectivity).

=== "Crear un plano de cobre"

    1. Colocar un **Polygon Pour** en la capa de cobre seleccionada.
    2. Definir el contorno del polígono y asignar la red prevista, por ejemplo `GND` si así lo requiere el circuito.
    3. Revisar aislamiento, conexión térmica y posibles islas de cobre.
    4. Recalcular el relleno mediante **Repour** después de los cambios.
    5. Comprobar la conexión real del plano con la red asignada.

    Un polígono sin red no equivale a un plano de tierra. Su función debe justificarse en el diseño.

    Referencia: [polígonos en capas de señal](https://www.altium.com/documentation/altium-designer/pcb/signal-layer-polygons).

## Verificación final {#verificacion-final}

=== "Ejecutar DRC"

    1. Recalcular los polígonos y guardar la PCB.
    2. Abrir **Tools → Design Rule Check**.
    3. Activar las comprobaciones y el reporte correspondientes al proyecto.
    4. Ejecutar el análisis y localizar las violaciones reportadas.
    5. Corregir las incidencias y repetir el DRC hasta obtener un resultado aceptable documentado.

    No debe declararse que la placa pasó la comprobación hasta incorporar el reporte de esta revisión.

=== "Inspección del diseño"

    - Confirmar correspondencia entre el esquema y la PCB.
    - Revisar las conexiones pendientes, polaridades y orientación de conectores.
    - Comprobar contorno, perforaciones, bordes y textos.
    - Revisar la vista 3D y el acceso físico a los componentes disponibles en el diseño.
    - Guardar la revisión final antes de generar los archivos de fabricación.

Referencias: [comprobación DRC](https://www.altium.com/documentation/altium-designer/pcb/drc) y [verificación de la placa](https://www.altium.com/documentation/altium-designer/tutorial/verifying-board-design).

## Archivos de fabricación {#archivos-de-fabricacion}

=== "Gerber y perforaciones"

    1. Desde la PCB activa, generar las capas requeridas mediante **File → Fabrication Outputs → Gerber Files** o la opción Gerber correspondiente a la instalación.
    2. Seleccionar sólo las capas necesarias, incluyendo la información de contorno que solicite el proceso de fabricación.
    3. Generar los agujeros mediante **File → Fabrication Outputs → NC Drill Files**.
    4. Comprobar unidades, precisión y origen compatibles entre las salidas.
    5. Revisar los archivos en un visor CAM: cobre, contorno y perforaciones deben coincidir.

    Referencia: [preparación de datos de fabricación](https://www.altium.com/documentation/altium-designer/preparing-for-manufacture/output-jobs/fabrication-data).

=== "Guardar la configuración"

    1. Incorporar un archivo **Output Job** (`.OutJob`) si se requiere repetir la generación de salidas.
    2. Configurar los generadores de fabricación, documentación y reportes necesarios.
    3. Identificar el documento de origen y la carpeta de salida.
    4. Generar los archivos de la revisión final y comprobar su contenido.

    La carpeta entregada al fabricante debe contener las salidas que solicita. El esquema, la PCB editable y el proyecto se conservarán además como fuentes del diseño.

    Referencia: [configuración de Output Jobs](https://www.altium.com/documentation/altium-designer/preparing-for-manufacture/output-jobs).

=== "Continuar hacia Mods"

    Si esta placa se fabricará con MonoFab, habrá que documentar la conversión desde las salidas reales de Altium al formato de entrada utilizado en Mods.

    Antes de calcular trayectorias se comprobarán escala, dimensiones, orientación, origen y separación entre pistas, contorno y perforaciones. La ruta de conversión se completará cuando el equipo confirme los archivos exportados y el procedimiento empleado.

    No se describirá una exportación directa a SVG sin comprobar que esté disponible en la instalación y que haya sido utilizada en esta práctica.

## Plan de capturas {#plan-de-capturas}

Las capturas se tomarán del proyecto real, conservando el mismo nombre de placa y la misma revisión. Esta tabla organiza la evidencia pendiente sin insertar imágenes vacías.

| Evidencia | Qué debe mostrar |
| --- | --- |
| Entorno y versión | Instalación utilizada y vista general con el proyecto abierto. |
| Proyecto | Árbol de documentos con esquema y PCB asociados. |
| Bibliotecas | Origen de componentes y ejemplo de símbolo con su huella. |
| Esquema general | Circuito completo con bloques identificables. |
| Detalles del esquema | Colocación, propiedades, cables y etiquetas de red. |
| Validación eléctrica | Ajustes relevantes y resultado del panel Messages. |
| ECO | Lista de cambios, validación y ejecución. |
| PCB inicial | Huellas transferidas, capas y unidades. |
| Contorno y colocación | Dimensiones, forma y distribución de componentes. |
| Restricciones | Anchos, aislamiento, agujeros y distancia al borde. |
| Ruteo | Conexiones durante el proceso y placa terminada. |
| Identificación | Texto y orientación de las leyendas. |
| Perforaciones | Diámetros, ubicación y condición de metalización. |
| Polígono | Red asignada y resultado del relleno. |
| DRC y vista 3D | Resultado comprobado de la revisión final. |
| Fabricación | Configuración de Gerber, NC Drill y archivos superpuestos en el visor. |

??? note "Datos necesarios para cerrar la documentación"

    Confirmar la versión del programa, función de la placa, componentes principales, dimensiones, capas, biblioteca y método de fabricación. Después se incorporarán los valores medidos, las decisiones del equipo y las capturas de cada etapa para convertir este procedimiento en la bitácora de la práctica.
