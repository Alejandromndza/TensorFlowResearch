# TensorFlowResearch

# Experimento de detección de objetos utilizando TensorFlow

Este análisis y estudio del funcionamiento de la detección de objetos en imagenes o videos se ha llevado a cabo gracias al API oficial de TensorFlow disponible en el siguiente enlace: [API](https://github.com/tensorflow/models/tree/master/research/object_detection)

Para entender mejor el desarrollo del detector de objetos se hizo una investigación previa de un clasificador de objetos. 
[Clasificador de objetos](https://github.com/Alejandromndza/TensorFlowResearch/blob/master/Clasificador.md)

## Nota previa Protocol buffers
Este API utiliza protobufs para configurar el modelo y los parámetros de entrenamiento. Por lo tanto se deben de compilar estas librerias, en adelante se detalla como hacerlo.

Estas librerias tienen un lenguaje y plataforma neutral, para serializar datos estructurados.

Para más información acerca de los protobufs [documentación](https://developers.google.com/protocol-buffers/).

## Como se ha llevado a cabo

Hadware Utilizado:

  1. Procesador Intel Core i7-8750H CPU 2.21GHz
  2. Memoria RAM 16Gb
  3. NVIDIA GeForce GTX 1050 
 
Para llevar a cabo este experimento ha sido necesario el siguiente software:

  1. Python 3.6
  2. Anaconda
  3. CUDA Tool Kit v8 (v9 no compatible con tensorflow v1.4)
  4. CuDNN v6
  5. TensorFlow-GPU v1.4
  6. Pillow
  7. lxml
  8. Cython
  9. Matplotlib
  10. Pandas
  11. OpenCv

Para más detalle sobre la instalación de los diferentes paquetes se puede consultar el siguiente enlace:
[Instalación](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/installation.md)

## Dataset

Se llevo a cabo tres experimentos con diferentes datasets para comprobar la calidad de las imágenes siempre distribuyendo el 80% en entrenamiendo y 20% en test. Cada imágen ha sido procesada recuadrando la pistola mediante [OpenLabeling](https://github.com/Cartucho/OpenLabeling)

El primer dataset constaba de 3000 imágenes obtenidas de la siguiente página [web](https://sci2s.ugr.es/weapons-detection) , tras el entrenamiento no se obtuvo los resultados esperados.

Tras el segundo dataset de 4500 imágenes se selecciono imagenes en videos donde aparecieran pistolas como en atracos, tiroteos...
Al entrenar con este dataset con la misma configuración con la que se llevo a cabo con el primero, se obtuvo mejores resultados pero seguía sin tener bastantes aciertos por la falta de variedad de imágenes. 

El tercer dataset surge de la unión de los dos datasets anteriores con las siguientes consideraciones:

  1. El primer dataset se somete a un filtrado de imágenes una por una y se eliminan las imágenes que consideramos que no tienen         relevancia y no aportan beneficios al entrenamiento. (1200 imágenes)
  2. El segundo dataset se somete al mismo filtrado que el primero, para evitar imágenes repeditas que afecten al entrenamiento.
  3. Se seleccionan 120 imágenes para aportar variedad al dataset.
  4. Se seleccionan 30 videos en principio de los cuales solo 6 tendran cabida en el dataset tomando imágenes y recuadrandolas.
  



