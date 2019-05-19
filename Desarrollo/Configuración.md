
# Configuración

Keep aspect ratio resizer
---------
Este parámetro sirve para el cambio de tamaño en las imagenes. Para que las imagenes resultantes siempre tengan la misma relación de aspecto. Con **min_dimension** especificaremos el tamaño del borde más pequeño permitido y con **max_dimension** el máximo permitido.

Feature extractor
---------
Con este parámetro de configuración se especifica en primer lugar que tipo de extractor se escogera para el modelo mediante **type**

![alt text](https://github.com/Alejandromndza/TensorFlowResearch/blob/master/img/comparative.png)

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
  
Initializer
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
  4. first_stage_localization_loss_weight : Perdida de peso por localización
  5. first_stage_objectness_loss_weight : Pérdida de peso por objetivo
  
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

![alt text](https://github.com/Alejandromndza/TensorFlowResearch/blob/master/img/dropout.png)

Se recomienda no utilizar el dropout, debido a las relaciones codificadas en los mapas de características, las activaciones pueden ser altamente correlacionadas. Actualmente se utiliza batch normalization para estabilizar la red neuronal. 

**dropout keep probability**: Se utiliza para calcular si la neurona tendra deserción o no, es decir se calcula la contribución de cada neurona con la probabilidad que indiquemos en este parámetro.

**Regulizer**: 
Cuando utilizamos regularizadores, estos actuan de manera que evitan el sobreajuste(overfitting) suavizando los resultados. Evitando que la máquina intente adaptarse lo máximo posible a los datos de entranamiento, ya que no da abstracción a sus predicciones, tenemos que conseguir resultados lo más genericos posibles.

Están disponibles los siguientes: 

  1. L1_regularizer Agrega el valor absoluto del coeficiente de peso como término a la función de perdida.
  2. L2_regularizer Agrega el cuadrado del coeficiente de peso como término de penalización en la función de perdida.
  
La función de pérdida mide con los resultados de las predicciones y la respuesta correcta que tan buenas son las predicciones. Existen varias funciones de perdida como el error cuadrático medio o la entropía cruzada.

El error cuadrático medio **MSE**, es la media de la diferencia entre los puntos reales y la salida predicha al cuadrado. Este método penaliza las diferencias mayores.

![alt text](https://github.com/Alejandromndza/TensorFlowResearch/blob/master/img/MSE.png)

**Initializer**

Al inicializar una red profunda, puede resultar favorable mantener constante la escala de la varianza de entrada, para que no disminuya al alcanzar la capa final.

**Variance scaling initializer** 

Este inicializador está diseñado para mantener la escala de los gradientes aproximadamente al mismo valor durante todas las capas. 

**Pesos** inicialmente los pesos son inicializados, la red implementa una serie de transformaciones que son aleatorias. Por ello tendremos en la función de perdida unos valores muy altos. A medida que la red va procesando nuevos casos esta se va ajustando. Para la segunda capa se puede indicar el factor de perdida de peso por localización y por clasificación mediante **second_stage_localization** y **second_stage_classification_loss_weight**


ROI Polling (Region of interest)
---------
Esta capa forma parte de la red neuronal, nos permite reutilizar el mapa de características de la red convolucional con esto se logra una acceleración importante en el entrenamiento, ya que tenemos una forma abstracta de representación que reduce el número de parámetros a aprender.

![alt text](https://github.com/Alejandromndza/TensorFlowResearch/blob/master/img/ROI.png)

**Initial crop Size**: Corte ROI basado en la interpolación bilineal, esta es una técnica para calcular valores de una ubicación de una malla basada en celdas de cuadrículas cercanas. Se usa un promedio de distancia para estimar celdas más cercanas a las que se les dan pesos más altos.

**Maxpool Kernel size**: Se trata de la dimensión del núcleo de la capa de agrupación, se recomienda que esta no tiene que ser demasiada grande ya que se pierde información o características imporantes.

**Maxpool Stride**: Paso de la operación de grupo máximo durante la agrupación ROI

Second Stage post processing
---------
Tras el paso de la segunda que actua de clasificador, entramos en un post procesamiento.

**Batch normalization** Es un método que normaliza cada paquete del batch, esto se realiza para evitar que los datos tengan distancias muy diferentes. Además ayuda a la red neuronal a trabajar con mas eficiencia. Esta normalización se va perdiendo con el paso de los datos por las redes ocultas. Por ello es necesario aplicar esto en el post procesamiento antes de que los datos vuelvan a entrar. Por ejemplo si tienes un objeto con dos colores distintos, es necesario que la red tenga de entrada ejemplos con ambos colores en el batch. Ya que tiene que generalizar y no entrenar a algo especifico para no tener futuros problemas en todo el proceso de entrenamiento.

En este apartado se definen varios parámetros para regularizar los datos:
  1. iou_treshold con el coeficiente de IOU explicado anteriormente.
  2. max detections per class con esto se puede regularizar los datos de entrada por cada clase.
  3. max total detections se regulariza las detecciones totales en el batch.
  



 


---------
---------
---------
---------
---------
---------
---------
