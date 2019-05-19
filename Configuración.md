
# Configuración

Keep aspect ratio resizer
---------
Este parámetro sirve para el cambio de tamaño en las imagenes. Para que las imagenes resultantes siempre tengan la misma relación de aspecto. Con **min_dimension** especificaremos el tamaño del borde más pequeño permitido y con **max_dimension** el máximo permitido.

Feature extractor
---------
Con este parámetro de configuración se especifica en primer lugar que tipo de extractor se escogera para el modelo mediante **type**

![alt text](https://github.com/Alejandromndza/TensorFlowResearch/blob/master/comparative.png)

Como se observa hay diferentes tipos para escoger, en nuestro tfg nos hemos decantado por el tipo inception. Ya que es el que mejores resultados ha dado.

En segundo lugar, el parámetro configurable se trata del **first_stage_features_stride** significa cuánto va a profundizar hablando en términos de convolución para extraer características.

First stage anchor generator
---------
Los cuadros de anclaje se utilizan en algoritmos de detección para ayudar a identificar objetos de diferentes formas.
Para ello mediante **grid_anchor_generator** se puede modificar opciones como :

  Scales: se definen para usar un conjunto de escalas explícitamente definido.
  Aspect ratios: Relación de aspectos para los cuadros de anclajes en cada punto de rejilla. Esto es un atributo de proyección   de imagen que describe la relación proporcional entre el ancho de una imagen y su altura.
  Height stride: La altura de pixeles para cada cuadro de anclaje.
  Widht stride: La anchura de pixeles para cada cuadro de anclaje.
  
Initizalizer
---------
Se selecciona el inicializador, **truncated_normal_initializer** selecciona números aleatorios de una distribución normal cuya media ronda cerca del 0. Se denomina truncado porque esta cortando las colas de la distribución normal, se especifica mediante **stddev**

First stage , Second stage
---------

Faster RCNN se compone de dos redes, la primera propone regiones en las cuales se puede encontrar objetos (RPN). 
La segunda red intenta detectar objetos en las propuestas dadas por la primera. 
Por convención a la primera red se le denomina first stage y a la segunda second stage.

First stage
----------

Parámetros para la primera etapa:

  1. first_stage_nms_score_threshold: El umbral de puntución de no supresión máxima
  2. first_stage_nms_iou_threshold: El umbral de IOU sin supresión máxima
  3. first_stage_max_proposals: El máximo de propuestas permitidas para la primera red
  4. first_stage_localization_loss_weight : El error permitido para la localización
  5. first_stage_localization_loss_weight : Localización por perdida de peso
  6. first_stage_objectness_loss_weight : Pérdida de peso objetivo
  
El umbral de no supresión máxima se utiliza para evitar que los cuadros de anclaje delimitadores se suporpongan señalando el mismo objeto. Para que no existan varias detecciones sobre un mismo objetivo.

El índice de Jaccard mide el grado de similitud entre dos conjuntos.

                                        T= Nc / (Na + Nb - Nc)
                    donde
                                Na - cantidad de elementos en el conjunto А
                                Nb - cantidad de elementos en el conjunto B
                                Nc - cantidad de elementos en el conjunto que intercepta

Umbral IOU, durante el entrenamiento se procede a juntar el cuadro real con el predicho sobre intersección over union que es el índice de Jaccard. Los mejores cuadros se etiquetaran como positivos si están por encima del umbral IOU.

Second Stage
---------
**mask rcnn box predictor** Se encarga de predecir clases, opcionalmente permite de predicción de máscaras o puntos clave dentro de las cajas de detección.

Los parámetros de configuración de este mismo son los siguientes:

**use dropout**: Generalmente se utiliza cuando la red esta en riesgo de sobrealimentación, es decir cuando la red es demasiado grande, entrenas durante mucho tiempo o si no tienes suficientes datos.

![alt text](https://github.com/Alejandromndza/TensorFlowResearch/blob/master/dropout.png)

Se recomienda no utilizar el dropout, debido a las relaciones codificadas en los mapas de características, las activaciones pueden ser altamente correlacionadas. Actualmente se utiliza batch normalization para estabilizar la red neuronal. 

ROI Polling (Region of interest)
---------
Esta capa forma parte de la red neuronal, nos permite reutilizar el mapa de características de la red convolucional con esto se logra una acceleración importante en el entrenamiento, ya que tenemos una forma abstracta de representación que reduce el número de parámetros a aprender.

![alt text](https://github.com/Alejandromndza/TensorFlowResearch/blob/master/ROI.png)

**Initial crop Size**: Corte ROI basado en la interpolación bilineal, esta es una técnica para calcular valores de una ubicación de una malla basada en celdas de cuadrículas cercanas. Se usa un promedio de distancia para estimar celdas más cercanas a las que se les dan pesos más altos.

**Maxpool Kernel size**: Se trata de la dimensión del núcleo de la capa de agrupación, se recomienda que esta no tiene que ser demasiada grande ya que se pierde información o características imporantes.

**Maxpool Stride**: Paso de la operación de grupo máximo durante la agrupación ROI.

---------
---------
---------
---------
---------
---------
---------
---------
