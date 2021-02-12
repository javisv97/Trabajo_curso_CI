# Trabajo_curso_CI
En este trabajo, aplicaremos la técnica conocida como aprendizaje por refuerzo para hacer que una red neuronal aprenda a jugar al reconocido juego de la serpiente.

## Funcionamiento
El entrenamiento se basa en que, a medida que la red va jugando partidas, ésta va aprendiendo, logrando una mejor puntuación. Esto lo hemos basado en el aprendizaje por refuerzo, donde si realizamos un buen movimiento, obtendremos una recompensa; mientras que, si realizamos un mal movimiento, obtendremos una penalización. La recompensa en nuestro caso es obtener una pieza de comida mientras que la penalización es perder el juego, ya sea tocando el borde o comiéndose a uno mismo.

La mejora o no del modelo la basaremos en el récord de puntuación. Cuanto mayor sea el récord de puntuación, mejor será el modelo.

El código está dividido en tres scripts: **game.py, agent.py y model.py**. Los cuales desempeñan diferentes funciones.


### Game.py
Este script es el que contiene el código del juego. Se ha partido del juego ya implementado para que jueguen humanos, al que hemos tenido que someter a una serie de cambios para adaptarlo de forma que sea jugable por nuestra red.

La interfaz gráfica y el reloj están deshabilitados, para así lograr una mayor velocidad a la hora de entrenar. Para reactivarlos solo tenemos que descomentar las líneas correspondientes.


### Agent.py
Es el punto de unión entre el juego y el modelo que vamos a implementar. Es en este script donde se realiza el entrenamiento del modelo. La función train() es la encargada de llevar a cabo ese entrenamiento, obteniendo los estados en los que se encuentra el juego y calculando los estados siguientes a partir de los anteriores. Además, define las acciones que realizará el modelo en cada momento, es decir, la toma de decisiones (función get_action()) y guarda la puntuación final junto con el récord al final de cada juego de entrenamiento.


### Model.py
Como su nombre indica, en este script es donde se define e implementa el modelo que vamos a usar. Podemos observar 2 clases: Linear_QNet y QTrainer.
La clase **Linear_QNet** contiene la creación e inicialización del modelo según los parámetros recibidos por el agente. Nuestro modelo tiene 11 entradas (que podemos ver en el script agent.py) y 3 salidas (3 acciones definidas en get_action()), mientras que la capa oculta es con la que podemos probar diferentes combinaciones. En nuestro caso está fijado a 256.

Usaremos una **RELU** como función de activación y guardaremos el modelo entrenado en el directorio creado ./model.

Por último, la clase **QTrainer** es donde se implementa realmente el aprendizaje por refuerzo. La función train_step() es la encargada del entrenamiento. Obtiene los valores de la matriz Q (propia de los aprendizajes por refuerzo) con el estado actual, y obtiene un estado Q nuevo a partir del anterior. Gracias a disponer del estado anterior y de la posible recompensa obtenida en ese estado, es capaz de obtener ese nuevo estado Q y aprender para así obtener aún mas recompensas. O en caso contrario, de no obtener recompensa, aprender que debe elegir otro camino diferente.
Finalmente, obtenemos la función de pérdida y realizamos lo que se conoce como “backpropagation” o propagación hacia atrás para reforzar el entrenamiento.

## Referencias
El código base del juego de la serpiente se encuentra en el siguiente repositorio: https://github.com/python-engineer/python-fun 
