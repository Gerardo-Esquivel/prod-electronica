# Fabricación CNC con Roland MonoFab SRM-20 {#fabricacion-cnc-con-roland-monofab-srm-20}

A continuación, se presenta la documentación detallada para la correcta instalación, configuración y operación de la fresadora Roland MonoFab SRM-20, diseñada específicamente para el flujo de trabajo en la fabricación de circuitos impresos (PCBs).

---

??? abstract "Explorar esta guía"

    - [Instalación de drivers y VPanel](#instalacion-de-drivers-y-vpanel)
    - [Control de la máquina](#control-de-la-maquina)
    - [Fases y herramientas](#fases-y-herramientas)
    - [Camas de sacrificio y recursos](#camas-de-sacrificio-y-recursos)
    - [Fabricación paso a paso](#fabricacion-paso-a-paso)
    - [Evidencia en video](#evidencia-en-video)
    - [Seguridad y operación](#seguridad-y-operacion)
    - [Placas fabricadas](#placas-fabricadas)


## Instalación de drivers y VPanel {#instalacion-de-drivers-y-vpanel}

Para asegurar la correcta comunicación entre la computadora y la máquina, es indispensable contar con los controladores oficiales y el software de control **VPanel**.


=== "Paso 1 · Drivers"

    * **Drivers de la máquina:** Puedes realizar la descarga directa desde este repositorio en un archivo `.zip` o consultar la sección oficial de soporte de Roland para asegurar la compatibilidad con tu sistema operativo. Una vez descargado, sigue los pasos de instalación seleccionando la carpeta correcta para tu arquitectura:

    <p align="center">
      <a href="../recursos/archivos/monofabDriver_V180.zip" target="_blank">[monofabDriver_V180 (Zip)]</a>
    </p>


    ??? example "Instalación del driver en imágenes"

        <p align="center">
          <img src="../recursos/imgs/monofab-driver-instalacion-paso-01.png" alt="Vista previa del proceso" width="800"><br>
        </p>

        <p align="center">
          <img src="../recursos/imgs/monofab-driver-sistema-operativo.png" alt="Selección de carpeta según sistema operativo" width="800"><br>
          <sub>Figura: Selección de la carpeta según nuestro sistema operativo.</sub>
        </p>

        <p align="center">
          <img src="../recursos/imgs/monofab-driver-preparacion-instalador.png" alt="Preparación de ejecución" width="800"><br>
        </p>

        <p align="center">
          <img src="../recursos/imgs/monofab-driver-ejecucion-administrador.png" alt="Ejecución del driver como administrador" width="800"><br>
          <sub>Figura: Ejecución del driver srm-20 como administrador.</sub>
        </p>

=== "Paso 2 · VPanel"

    * **Instalación del VPanel:** El VPanel es la interfaz gráfica que nos permite manipular los ejes de la máquina, configurar velocidades y enviar los archivos de corte (`.rml`). Puedes descargar el programa desde el siguiente enlace; una vez descargado, descomprímelo y ejecuta el archivo:

    <p align="center">
      <a href="../recursos/archivos/VPanel-for-SRM-20_Installer.zip" target="_blank">[VPanel-for-SRM-20_Installer (Zip)]</a>
    </p>

## Control de la máquina {#control-de-la-maquina}

El VPanel cuenta con diferentes secciones clave para el control de movimiento y la gestión de trabajos.

<p align="center">
  <img src="../recursos/imgs/monofab-vpanel-pantalla-principal.png" alt="Menú principal del VPanel" width="800"><br>
  <sub>Figura: Menú principal del VPanel para SRM-20, mostrando las coordenadas, controles de movimiento, pasos del cursor y botones de operación.</sub>
</p>


=== "Movimiento"

    ### Controles de Movimiento y Unidades (Cursor Step) {#controles-de-movimiento-y-unidades-cursor-step}

    * 🟠 **Naranja y 🟢 Verde:** En la parte central del VPanel encontramos los botones de desplazamiento de los ejes X, Y y Z.
    * 🔵 **Azul:** Justo debajo se encuentran los selectores de **Cursor Step** (`Continue`, `x100`, `x10`, `x1`). Entre más pequeño sea el valor seleccionado (como `x1`), menor será el recorrido de la herramienta por cada clic. Esto es **extremadamente útil para la calibración fina** y ajustes de precisión.

=== "Orígenes y trabajo"

    ### Orígenes y Sistema de Coordenadas {#origenes-y-sistema-de-coordenadas}

    * 🔴 **Rojo (Guardar Orígenes):** Podemos definir y almacenar nuestros puntos de origen (ceros de trabajo en X, Y y Z) utilizando los botones de configuración de coordenadas en el panel lateral derecho.
    * 🟡 **Amarillo (Pausa y Cancelar):** En la esquina inferior derecha se encuentran los botones de control de ejecución (`PAUSE`/`RESUME` y `Cancel`), vitales para detener el proceso en caso de cualquier emergencia o imprevisto.
    * 🟤 **Café:** Muestra las coordenadas actuales.
    * 🟣 **Morado:** Mueve hacia nuestro origen guardado.
    * ⚪ **Rosa:** Comenzar un proceso de corte.

    <p align="center">
      <img src="../recursos/imgs/monofab-vpanel-panel-controles.png" alt="Vista del panel con las secciones mencionadas" width="800"><br>
      <sub>Figura: Vista del panel con las secciones mencionadas.</sub>
    </p>

    !!! warning "Antes de ejecutar Output"

        Una vez dado clic en el botón de **`Cut`** se nos desplegará el siguiente menú donde podremos subir un archivo. El fresado comenzará instantáneamente una vez que demos clic en **`Output`**. Es **muy importante** antes de empezar haber calibrado correctamente todos nuestros ejes y tener despegada la broca de nuestra placa para evitar rayones o desgastar la punta.


    <p align="center">
      <img src="../recursos/imgs/monofab-vpanel-carga-trabajo.png" alt="Vista del panel para subir archivos" width="800"><br>
      <sub>Figura: Vista del panel para subir archivos.</sub>
    </p>

## Fases y herramientas {#fases-y-herramientas}

Para la fabricación exitosa de una placa de circuito impreso (PCB), es fundamental mantener un orden riguroso y utilizar la herramienta adecuada en cada etapa:

1. **Perforaciones:** Se inicia con las perforaciones de la placa. Para esta fase utilizaremos una broca especial de **0.8 mm**.
2. **Trazado de Pistas:** En esta segunda etapa se generan las trazas del circuito. Utilizaremos un cortador en V (*V-cutter*) con un diámetro de **0.4 mm**.
3. **Contorno:** Finalmente, se realiza el corte exterior para separar la placa utilizando una herramienta de fresado de **2 mm**.

<p align="center">
  <img src="../recursos/imgs/monofab-herramientas-llave-allen.jpeg" alt="Herramientas y llave Allen" width="800"><br>
  <sub>Figura: Herramientas de sujeción, espátulas, brocas y la llave Allen indispensable para aflojar y apretar el mandril que sostiene las herramientas de corte.</sub>
</p>

---

## Camas de sacrificio y recursos {#camas-de-sacrificio-y-recursos}

* **Camas de sacrificio:** Es altamente recomendable utilizar nuestras propias camas de sacrificio (usualmente hechas de MDF o materiales similares) colocadas sobre la base de la máquina. Esto protege la estructura principal de la fresadora de posibles daños accidentales durante el fresado de contornos.
* **Descarga de Archivos:** Puedes acceder al diseño base en formato DXF desde el siguiente enlace:  
  <a href="../recursos/archivos/Sacrificio-SS.dxf" target="_blank">[Sacrificio SS (DXF)]</a>

---

## Fabricación paso a paso {#fabricacion-paso-a-paso}

!!! warning "Al cambiar de herramienta"

    **Precaución Crítica en el Cambio de Herramienta:** Procedemos a cambiar la broca por la siguiente herramienta (por ejemplo, el cortador en V para pistas) y **volvemos a calibrar únicamente en el eje Z**. Es **sumamente importante no mover los ejes X y Y**, ya que cualquier alteración en dichos ejes provocará que las pistas o perforaciones posteriores queden totalmente desfasadas.


=== "Paso 1 · Fijar"

    1. **Preparación de la Superficie:** Limpiamos la cama de sacrificio y utilizamos **cinta doble cara** para fijar nuestra placa de cobre, procurando pegarla lo más derecha y alineada posible para evitar errores de paralelismo.

    <p align="center">
      <img src="../recursos/imgs/monofab-placa-fenolica-cinta-doble-cara.jpeg" alt="Placa fenólica con cinta doble cara" width="800"><br>
      <sub>Figura: Placa fenólica con cinta doble cara.</sub>
    </p>

    <p align="center">
      <img src="../recursos/imgs/monofab-placa-alineada-mesa.jpeg" alt="Placa alineada" width="800"><br>
      <sub>Figura: Placa fenólica alineada correctamente en la cama de sacrificio.</sub>
    </p>

    <p align="center">
      <img src="../recursos/imgs/monofab-cama-sacrificio-maquina.jpeg" alt="Placa con cama de sacrificio dentro de la MonoFab" width="800"><br>
      <sub>Figura: Placa con cama de sacrificio colocada dentro de la MonoFab.</sub>
    </p>

=== "Paso 2 · Broca"

    2. **Colocación de la Broca:** Usando la herramienta de la llave Allen, aflojamos el tornillo y colocamos la broca o cortador; posteriormente volvemos a apretar para continuar con la calibración.

    <p align="center">
      <img src="../recursos/imgs/monofab-colocacion-fresa.jpeg" alt="Colocación del cortador" width="800"><br>
      <sub>Figura: Colocación del cortador.</sub>
    </p>

=== "Paso 3 · Calibrar"

    3. **Calibración de Ejes X e Y:** Movemos la máquina mediante el VPanel hasta la esquina inferior izquierda de la placa de cobre y guardamos el origen en X e Y (`X/Y` en *Set Origin Point*).

    4. **Calibración del Eje Z:** Para el eje Z, utilizamos la técnica clásica de colocar un **pequeño trozo de papel** entre la punta de la herramienta y la superficie de la placa, bajando lentamente el eje Z hasta sentir una ligera fricción al mover el papel. Una vez logrado, fijamos el origen en Z.

    <p align="center">
      <img src="../recursos/imgs/monofab-calibracion-origen.jpeg" alt="Calibración en la esquina inferior izquierda" width="800"><br>
      <sub>Figura: Calibración de la MonoFab en la esquina inferior izquierda.</sub>
    </p>

=== "Paso 4 · Ejecutar"

    5. **Ejecución del Trabajo:** Con los orígenes correctamente fijados, subimos nuestro archivo de perforaciones (`.rml`), verificamos la vista previa y presionamos *Output* para iniciar el proceso.

    6. **Inspección y Cambio de Herramienta:** Una vez finalizado el trabajo de perforación, acercamos la placa hacia nosotros utilizando el VPanel para poder aspirar los residuos y revisar el resultado.

    <p align="center">
      <img src="../recursos/imgs/monofab-placa-perforada-limpieza.jpeg" alt="Placa perforada lista para aspirar" width="800"><br>
      <sub>Figura: Placa fenólica perforada lista para aspirar residuos.</sub>
    </p>

## Evidencia en video {#evidencia-en-video}

A continuación se muestran los registros en video del comportamiento de la Roland MonoFab SRM-20 en cada una de sus fases operativas:


=== "Perforaciones"

    * **Proceso de Perforaciones:**
      <video controls width="100%">
        <source src="../recursos/imgs/monofab-perforado-placa.mp4" type="video/mp4">
        Tu navegador no soporta la reproducción de video.
      </video>
      <sub>Proceso automatizado de perforación de la placa de cobre utilizando la broca de 0.8 mm.</sub>

=== "Pistas"

    * **Proceso de Trazado de Pistas:**
      <video controls width="100%">
        <source src="../recursos/imgs/monofab-fresado-pistas.mp4" type="video/mp4">
        Tu navegador no soporta la reproducción de video.
      </video>
      <sub>Mecanizado y aislamiento de las pistas del circuito con el cortador en V de 0.4 mm.</sub>

=== "Contorno"

    * **Proceso de Contorno:**
      <video controls width="100%">
        <source src="../recursos/imgs/monofab-fresado-contorno.mp4" type="video/mp4">
        Tu navegador no soporta la reproducción de video.
      </video>
      <sub>Corte final de contorno de la placa utilizando la herramienta de 2 mm.</sub>

## Seguridad y operación {#seguridad-y-operacion}

!!! warning "Pautas de operación y supervisión"

    **Nota:** Se recomienda tener en cuenta las siguientes pautas operativas durante el uso del equipo:

    * **Prevención de suspensión de energía:** Se recomienda que durante cualquier proceso de trabajo se mantenga reproduciendo un video en segundo plano o activo en el equipo de cómputo para evitar que la computadora entre en modo de suspensión o ahorro de energía, lo cual podría interrumpir o apagar la comunicación con el equipo durante un corte o grabado crítico.
    * **Respaldo energético:** Se recomienda contar con una fuente de alimentación ininterrumpida (UPS / pila) o un contacto cercano de respaldo para mantener energizado el equipo y evitar cortes abruptos por fallas en la red eléctrica.
    * **Monitoreo inicial:** Es vital mantenernos al pendiente en los primeros segundos de cada proceso de mecanizado; una supervisión oportuna en el arranque nos permite reaccionar a tiempo para evitar colisiones, corregir errores de configuración de origen o ajustar parámetros de fabricación antes de dañar el material.

## Placas fabricadas {#placas-fabricadas}

<div class="media-grid" markdown="1">

A continuación se muestra el resultado final del trabajo realizado por el equipo:

<p align="center">
  <img src="../recursos/imgs/monofab-galeria-placa-fabricada-01.jpeg" alt="Primera placa fabricada" width="500"><br>
  <sub>Vista general de la primera PCB fabricada.</sub>
</p>

<p align="center">
  <img src="../recursos/imgs/monofab-galeria-placa-fabricada-02.jpeg" alt="Segunda placa fabricada" width="500"><br>
  <sub>Vista general de la segunda PCB fabricada.</sub>
</p>

</div>
