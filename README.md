# Taller de Periodismo de Datos
Materiales para el Taller de Periodismo de Datos de El País en colaboración con la Fundación BBVA. Este módulo contempla la utilización de mapas como herramienta en el Periodismo. A lo largo de dos sesiones aprenderemos a utilizar dos de las herramientas más populares para realizar mapas: [CARTO](https://carto.com/) y [QGIS](http://www.qgis.com/).

La metodología del módulo consistirá en ir conociendo las posibilidades que nos ofrecen las herramientas GIS para realizar análisis, manipulación y creación de nuevos campos y variables que nos sirvan para representar información sobre un mapa. Iremos cambiando de una herramienta a otra con el objetivo de ir conociendo el potencial y las posibilidades que nos ofrece cada una. A lo largo de las dos sesiones vamos a tratar aspectos como:
* [**El Color**](#color): la utilización del color es fundamental a la hora de dar estilo a un mapa. La elección de una paleta de colores adecuada, así como de la escala correcta es fundamental a la hora de comunicar la información.
* [**Fuentes de información**](#sources): dónde podemos encontrar datos GIS para crear mapas: IGN, Natural Earth, OSM y Geofabrik entre otros.
* Ser capaces de crear **mapas de puntos**. Nos sirven para geolocalizar acontecimientos como estaciones de servicio, de bicicleta pública, un accidente o un acontecimiento de última hora.
* Realizar procesos de **análisis geoespacial** y manipulación de archivos de tipo Shape (shp) o filtrado en base a atributos.
* [**Conversión**](#conversion) entre sistemas de coodenadas diferentes.

## <a name="color">Color</a>
- A la hora de escoger una escala de color existente, [Colorbrewer](http://colorbrewer2.org/) es una muy buena herramienta para acceder a una paleta de colores adecuada. Los colores que nos ofrece pertenecen al estudio científico de la Dr. Cynthia A. Brewer y nos permite seleccionar escalas de color secuenciales, qualitativas o divergentes. Nos permite exportar los colores como una paleta de colores para GIMP (Software libre para trabajo vectorial), clases CSS, un array JavaScript con los colores en formato rgb.

- Pero, ¿y si estas escalas no nos convencen o estamos cansados de verlas replicadas en todos los mapas? Podemos crear nuestra propia escala de color. A la hora de crear una escala existen multitud de factores a tener en cuenta, como son la interpolación de los colores, la manera en que aplicamos los propios colores en función de una determinada escala, o la corrección automática de la luminosidad. Ambas exceden los límites de este módulo pero a quien le interese puede echar un ojo a [este post](https://www.vis4.net/blog/2013/09/mastering-multi-hued-color-scales/) de Gregor Aisch o directamente a [esta herramienta](http://gka.github.io/palettes/#colors=lightyellow,orange,deeppink,darkred|steps=7|bez=1|coL=1) que él mismo desarrolló.
  - [Gregor Aisch](https://twitter.com/driven_by_data) es el responsable de [Chroma.js](https://github.com/gka/chroma.js), una librería JavaScript llamada que permite crear escalas de color corregidas y ajustadas.
  
- Para conocer más sobre escalas de color podeis visitar [este post](https://roadtolarissa.com/blog/2015/01/04/coloring-maps-with-d3/) de [Adam Pearce](https://twitter.com/adamrpearce) en el que explica las diferencias entre una escala de color lineal, quantitativa o quantil.

## <a name="sources">Fuentes de información</a>
En las siguientes páginas se pueden descargar shapefiles y archivos _raster_ de carácter político, natural o cultural:
- Centro de descargas del [CNIG](http://centrodedescargas.cnig.es/CentroDescargas/index.jsp). Tiene una interfaz un poco compleja al principio hasta que averiguamos cómo encontrar los datos que nos interesan. Es el centro de referencia a nivel nacional para descargar datos SIG. Tiene todos los vuelos con sus correspondientes ortofotos, datos ráster, modelos de elevación del terreno (incluso generados con lidar de 2x2m) o datos de tipo vectorial: información sobre carreteras, puertos, estaciones, etc.

-  Ministerio de Agricultura y Pesca, Alimentación y Medio Ambiente ([Magrama](http://www.mapama.gob.es/es/cartografia-y-sig/ide/descargas/default.aspx)). Datos sobre Agricultura, Biodiversidad, Calidad y evaluación ambiental, Agua y muchos más. Aquí podemos acceder de una manera sencilla a datos sobre parques naturales, cuencas hidrográficas o zonas con riesgo de inundación. Los datos suelen estar en formato shp o kmz/kml.

- [Natura Earth Data](http://www.naturalearthdata.com/). Natural Earth es un proyecto open source donde podemos encontrar mucha información tanto de tipo vectorial como ráster. A pesar de que es un proyecto serio y consolidado, siempre debemos intentar acudir a las fuentes de datos oficiales. Aunque en Natural Earth encontramos archivos shape con códigos o datos sobre población, por ejemplo, estos no se actualizan con la frecuencia que lo hacen los diferentes organismos competentes.

- [Diva-gis.org](http://www.diva-gis.org/gdata) nos ofrece datos GIS de cualquier país del mundo. Aunque son datos sin mucho nivel de detalle, nos pueden salvar cuando estamos realizando un mapa de algún país concreto y no encontramos datos sobre su contorno, ríos, carretas o límites administrativos.

## Mapshaper
[Mapshaper](http://mapshaper.org/) es una herramienta open source desarrollada por [Mathew Bloch](https://github.com/mbloch). Además de una aplicación por [línea de comandos](https://github.com/mbloch/mapshaper/wiki/Introduction-to-the-Command-Line-Tool) que nos permite manipular archivos Shapefile, GeoJSON, TopoJSON, CSV entre otros formatos, también cuenta con una interfaz web. Podemos utilizar Mapshaper para reducir el peso de los archivos shapefile.   

Cuando estamos trabajando en un mapa que va ser publicado en la web, el peso de los archivos es muy importante. Además, servicios como CARTO tienen un límite de almacenamiento gratuito.

## <a name="conversion">Conversión entre sistemas de coordenadas</a>
La complejidad que supone representar una esfera sobre un plano ha supuesto la creación de diferentes maneras de representar un punto sobre un plano. Aunque existen varios sistemas para representar la información sobre un plano, vamos a centrarnos en dos de los principales sistemas de coordenadas en metros (UTM) y en grados (Lon/Lat).

En esta parte del módulo vamos a ver cómo convertir coordenadas del sistema **UTM** (`433743.5,4480432`) a **Lon/Lat** (`40.471927,-3.781607`) que es el sistema con el que tradicionalmente trabajan los servicios de representación de datos como CARTO. Carto también permite realizar conversiones entre coordenadas pero necesitamos realizar algunas consultas SQL.

- Vamos a trabajar con el dataset de todas las paradas de la **EMT** que la empresa ofrece en su portal de datos abiertos. Hacemos click en [este](http://opendata.emtmadrid.es/Datos-estaticos/Datos-generales) enlace y descargamos el xlsx de la **pestaña Paradas**. **Convertimos el archivo a csv** para poder abrirlo con QGIS.

- Creamos un **nuevo proyecto** en QGIS. Accedemos a propiedades del proyecto y seleccionamos el **Sistema de Referencia de Coordenadas** en coordenadas **UTM**, podemos buscar el correspondiente código `EPSG:25830`.

- Cargamos el archivo csv de las paradas de la EMT. Es posible que QGIS nos avise de que la capa no tiene un CRS definido. Hacemos click derecho sobre la capa y pulsamos sobre **Establecer SRC de la capa**. En el desplegable seleccionamos el mismo sistema de coordenadas del proyecto: **EPSG:25830** o **ETRS89 / UTM zone 30N**.

- A continuación vamos a **guardar esta capa como shapefile**: botón derecho sobre la capa y **guardar como** En este paso, también vamos a generar la nueva capa bajo el sistema de coordenadas WGS84. **Es importante** que al salvar el archivo como shapefile seleccionemos en el apartado SRC el sistema **WGS84** o  **EPSG:4326**.

- Añadimos la nueva capa al proyecto **sólo si no se ha añadido automáticamente**.

- A continuación vamos a crear dos nuevos campos, uno correspondiente a la Longitud y otro a la Latitud en grados. Para ello necesitamos la calculadora de campos. Esta herramienta nos permite generar nuevos campos en base a los cmapos de la tabla de atributos o en base a su **geometría** como nos interesa ahora mismo.

- Pulsamos sobre la `calculadora de campos` ![field_calculator_icon](https://raw.githubusercontent.com/LuisSevillano/QGIS-choropleth-workshow/master/img/field_calculator_icon.png). Creamos u nuevo campo que cumpla las siguientes caracteristicas:
  - **Nombre del campo**: `longitud`.
  - **Tipo del campo de salida***: `Numero decimal (real)`.
  - **Longitud del campo de salida***: seleccionamos una precisión de 6 decimales.
  - Ahora vamos a utilizar una función del apartado **Geometría**. Podemos utilizar el buscador para encontrar la función **$x**.
  - Acemos doble click sobre $x y nos aseguramos de que se añade a la caja de la izquierda llamada **Expresión** como se muestra en la imagen:
  
  ![field-calculator](img/field-calculator.png)
  - Podemos asegurarnos de que estamos realizando bien todos los pasos comprobando que en el apartado inferior `Vista preliminar de la salida` vemos un valor parecido a `-3.78160697225065` para la longitud y que no nos aparece un `null` o algún otro valor erróneo.
  - Pulsamos sobre aceptar para generar este nuevo campo.
  - Repetimos los mismos pasos para calcular la latitud:
    - **Nombre del campo**: `latitud`.
    - En el apartado **Geometría** buscamos la función **$y**.
    - Comprobamos que en el apartado inferior `Vista preliminar de la salida` vemos un valor parecido a `40.4719271557661` para la latitud y que no nos aparece un `null` o algún otro valor erróneo.
    - Pulsamos sobre aceptar para generar este nuevo campo.
    
  - Por último, salvamos los cambios en el icono salimos del modo edición haciendo click sobre el icono `Commutar edición` que se activa cuando accedemos a la calculadora de campos.
  
  - Si queremos exportar estos resultados a un formato **csv** tenemos que hacer click derecho sobre la capa y **guardar como**. En formato seleccionamos **Valores separados por comas [CSV]**.
  
  - Ya hemos realizado la conversión entre un sistema de coordenadas en metros UTM a un sistema de coordenadas en grados Lon/Lat!.
  
  
