# Clasificación de entidades nombradas con una RNN 🧠
Entrenamos una RNN para clasificar entidades nombradas (texto) en categorías (**PERSON**, **LOCATION**, **ORGANIZATION**, **OTHER**).


> - "Lionel Messi" -> **PERSON**
> - "Argentina" -> **LOCATION**
> - "Comisión Nacional de Actividades Espaciales" -> **ORGANIZATION**

El objetivo fue entrenar el modelo desde cero curando un dataset propio y aprendiendo PyTorch en el medio. No me permití usar `torch.nn.RNN` para realmente entender el funcionamiento interno de una RNN. 

Esto surgió como proyecto de fin de semana, fue completado en ~6 horas. Es posible que hayan errores (es mi primera vez usando PyTorch!). 

El código está basado en un tutorial de [Patrick Loeber](https://www.youtube.com/watch?v=WEV61GmmPrk), a su vez basado en este blog de [pytorch.org](https://pytorch.org/tutorials/intermediate/char_rnn_classification_tutorial.html)

<img src="images/pytorch-vanilla-rnn.png" alt="drawing" width="350"/>

*imagen 1, [link](https://pytorch.org/tutorials/intermediate/char_rnn_classification_tutorial.html)*


Para armar el dataset, escribimos ejemplos de cada categoría y generamos el resto con GPT 3.5 (ChatGPT free).

## Estructura del repositorio
- `notebook.ipynb`: cuaderno de Google Colab. Acá se realizó el entrenamiento y se encuentra todo el código relevante. 
- `model.pth`: el modelo ya entrenado. Al final del archivo `notebook.ipynb` se demuestra cómo cargarlo y probarlo.
- `/dataset/*.txt`: archivos de texto con ejemplos no procesados para cada categoría
- `/images`: imágenes ilustrativas

## Proceso 
- Armar dataset de categorías **PERSON**, **LOCATION**, **ORGANIZATION** usando ChatGPT
- Normalizar dataset
- Definir el encoding del input (en este caso, usamos _one-hot_)
- Definir la clase RNN con su _forward pass_ en base a la imagen (1)
- Instanciar un modelo y hacer un paso de entrenamiento manualmente
- Setear hiperparámetros y entrenar
- Probar el modelo con datos nuevos
- Guardar el modelo

## Dataset
El dataset fue generado "a mano" con la ayuda de ChatGPT. Los archivos base están en el directorio `./dataset`. Cada archivo de texto tiene el nombre de una categoría y contiene ejemplos no procesados (y con entries repetidas).

## Hyperparameters
El modelo se entrenó en `n_iters = 50000`,  `learning_rate = 0.001`, `n_hidden = 128`.

## Importante ❗
Este cuaderno sólo fue testeado en Google Colab. 

El código se conecta a Google Drive y busca la carpeta `My Drive/nn-category-classification/training-data`, donde debe haber un archivo para cada categoría (person, location, organization) conteniendo los datos de entrenamiento. 

Pueden obtener usar los mismos datos que yo, copiá [esta carpeta](https://drive.google.com/drive/folders/1N4FA62g0iQAnIEg0I84xHip02sX10lGx?usp=sharing) a tu carpeta prinicipal (My Drive) de Google Drive. 