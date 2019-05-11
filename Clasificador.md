# Clasificador

Investigación
--------

En esta sección llevamos a cabo varios experimentos para entender como funcionan las redes neuronales convolucionales, para ello realizamos un diseño de un modelo para un clasificador de objetos utilizando keras como libreria principal.

Se llevo a cabo mediante colaboraty, se trata de un entorno de ejecución que se lleva a cabo en la nube. 
Es muy interesante ya que te permite ejecutar tu código con una gpu Tesla K80.

Para más información sobre google colab esta disponible en el siguiente [enlace](https://colab.research.google.com/notebooks/welcome.ipynb)

Se puede encontrar el código en el siguiente enlace: [Modelo](https://drive.google.com/open?id=1OcOGwLL2juSK3s4SVTmZ1DYQ-a6yyHh7)

Desarrollo
--------

Desarrollamos un modelo para clasificar las diferentes clases del dataset [cifar](https://www.cs.toronto.edu/~kriz/cifar.html)

El modelo se compone en lo siguiente:

------------------------------------------------------------------------------------------------------------------------------
Layer (type)                 Output Shape              Param #   
_________________________________________________________________
input_20 (InputLayer)        (None, 32, 32, 3)         0         
_________________________________________________________________
conv2d_134 (Conv2D)          (None, 32, 32, 64)        1792      
_________________________________________________________________
conv2d_135 (Conv2D)          (None, 32, 32, 64)        36928     
_________________________________________________________________
max_pooling2d_58 (MaxPooling (None, 16, 16, 64)        0         
_________________________________________________________________
conv2d_136 (Conv2D)          (None, 16, 16, 128)       73856     
_________________________________________________________________
conv2d_137 (Conv2D)          (None, 16, 16, 128)       147584    
_________________________________________________________________
max_pooling2d_59 (MaxPooling (None, 8, 8, 128)         0         
_________________________________________________________________
conv2d_138 (Conv2D)          (None, 8, 8, 200)         230600    
_________________________________________________________________
conv2d_139 (Conv2D)          (None, 8, 8, 200)         360200    
_________________________________________________________________
conv2d_140 (Conv2D)          (None, 8, 8, 200)         360200    
_________________________________________________________________
max_pooling2d_60 (MaxPooling (None, 4, 4, 200)         0         
_________________________________________________________________
flatten_20 (Flatten)         (None, 3200)              0         
_________________________________________________________________
dense_39 (Dense)             (None, 10)                32010     
_________________________________________________________________
dense_40 (Dense)             (None, 10)                110       


Hicimos que nuestra red neuronal tuviera capas convolucionales crecientes 64 - 128 - 200.

La función de activación elegida fue 'relu' por su buen desempeño con las redes convolucionales y las imágenes.
Para ver todas las funciones activación disponibles en keras se encuentran en este [enlace](https://keras.io/activations/)

Como optimizador decidimos utilizar Adam, al solucionar el problema de SGD (Stochastic Gradient Descent), intentando superar el problema de fijación del ratio de aprendizaje. Su funcionalidad adapta el ratio de aprendizaje tomando como referencia la distribución de los parámetros, estos en caso de estar muy dispersos el ratio de aprendizaje se incrementara.

Para ver todos los optimizadores disponibles visitar este [enlace](https://keras.io/optimizers/)





