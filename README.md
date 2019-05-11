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

