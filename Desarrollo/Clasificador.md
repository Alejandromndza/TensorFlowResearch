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

```plain
                  _________________________________________________________________
                  Layer (type)                 Output Shape              Param #   
                  =================================================================
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
                  =================================================================

```

Hicimos que nuestra red neuronal tuviera capas convolucionales crecientes 64 - 128 - 200.

La función de activación elegida fue 'relu' por su buen desempeño con las redes convolucionales y las imágenes.
Para ver todas las funciones activación disponibles en keras se encuentran en este [enlace](https://keras.io/activations/)

Como optimizador decidimos utilizar Adam, al solucionar el problema de SGD (Stochastic Gradient Descent), intentando superar el problema de fijación del ratio de aprendizaje. Su funcionalidad adapta el ratio de aprendizaje tomando como referencia la distribución de los parámetros, estos en caso de estar muy dispersos el ratio de aprendizaje se incrementara.

Para ver todos los optimizadores disponibles visitar este [enlace](https://keras.io/optimizers/)

El modelo se configuro para que en cada epoca se escriba el resultado de este mismo

```plain
Epoch 1/30   categorical_accuracy: 0.2978 - val_loss: 1.4293 - val_categorical_accuracy: 0.4765
Epoch 2/30   categorical_accuracy: 0.5604 - val_loss: 1.1482 - val_categorical_accuracy: 0.5873
Epoch 3/30   categorical_accuracy: 0.6616 - val_loss: 0.9212 - val_categorical_accuracy: 0.6894
Epoch 4/30   categorical_accuracy: 0.7298 - val_loss: 0.8640 - val_categorical_accuracy: 0.7128
Epoch 5/30   categorical_accuracy: 0.7704 - val_loss: 0.7941 - val_categorical_accuracy: 0.7318
Epoch 6/30   categorical_accuracy: 0.8015 - val_loss: 0.7175 - val_categorical_accuracy: 0.7585
Epoch 7/30   categorical_accuracy: 0.8196 - val_loss: 0.7290 - val_categorical_accuracy: 0.7679
Epoch 8/30   categorical_accuracy: 0.8419 - val_loss: 0.7633 - val_categorical_accuracy: 0.7760
Epoch 9/30   categorical_accuracy: 0.8522 - val_loss: 0.7859 - val_categorical_accuracy: 0.7663
Epoch 10/30  categorical_accuracy: 0.8655 - val_loss: 0.8127 - val_categorical_accuracy: 0.7639
Epoch 11/30  categorical_accuracy: 0.8706 - val_loss: 0.7580 - val_categorical_accuracy: 0.7734
Epoch 12/30  categorical_accuracy: 0.8767 - val_loss: 0.8691 - val_categorical_accuracy: 0.7655
Epoch 13/30  categorical_accuracy: 0.8799 - val_loss: 0.9532 - val_categorical_accuracy: 0.7721
Epoch 14/30  categorical_accuracy: 0.8848 - val_loss: 0.9586 - val_categorical_accuracy: 0.7609
Epoch 15/30  categorical_accuracy: 0.8877 - val_loss: 1.0178 - val_categorical_accuracy: 0.7553
Epoch 16/30  categorical_accuracy: 0.8879 - val_loss: 0.9500 - val_categorical_accuracy: 0.7583
Epoch 17/30  categorical_accuracy: 0.8918 - val_loss: 1.0963 - val_categorical_accuracy: 0.7643
Epoch 18/30  categorical_accuracy: 0.8890 - val_loss: 0.9957 - val_categorical_accuracy: 0.7823
Epoch 19/30  categorical_accuracy: 0.8872 - val_loss: 1.2186 - val_categorical_accuracy: 0.7509
Epoch 20/30  categorical_accuracy: 0.8908 - val_loss: 1.0767 - val_categorical_accuracy: 0.7667
Epoch 21/30  categorical_accuracy: 0.8911 - val_loss: 0.8847 - val_categorical_accuracy: 0.7649
Epoch 22/30  categorical_accuracy: 0.8913 - val_loss: 1.1043 - val_categorical_accuracy: 0.7691
Epoch 23/30  categorical_accuracy: 0.8950 - val_loss: 0.9726 - val_categorical_accuracy: 0.7659
Epoch 24/30  categorical_accuracy: 0.8882 - val_loss: 0.9773 - val_categorical_accuracy: 0.7708
Epoch 25/30  categorical_accuracy: 0.8903 - val_loss: 0.9085 - val_categorical_accuracy: 0.7549
Epoch 26/30  categorical_accuracy: 0.8932 - val_loss: 1.0280 - val_categorical_accuracy: 0.7690
Epoch 27/30  categorical_accuracy: 0.8862 - val_loss: 0.9065 - val_categorical_accuracy: 0.7718
Epoch 28/30  categorical_accuracy: 0.8885 - val_loss: 1.2105 - val_categorical_accuracy: 0.7627
Epoch 29/30  categorical_accuracy: 0.8908 - val_loss: 1.2162 - val_categorical_accuracy: 0.7633
Epoch 30/30  categorical_accuracy: 0.8880 - val_loss: 1.1426 - val_categorical_accuracy: 0.7582
```


