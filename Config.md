
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

Parámetros para la primera etapa.
  **first_stage_nms_score_threshold**: El umbral de puntución de NO supresión máxima
  **first_stage_nms_iou_threshold**: El umbral de IOU sin supresión máxima
  

---------
---------
---------
---------
---------
---------
---------
---------
---------
---------
