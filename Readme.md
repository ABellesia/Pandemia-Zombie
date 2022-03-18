# Simulación de una epidemia Zombie

## Tabla de contendo

* [Información general ](#informacion-general)
* [Información previa](#indormacion-previa) 
  * [Modelo SIR](#modelo-sir)
  * [Modelo con infección latente (SIRZ)](#modelo-con-infección-latente)
  * [Modelo con cuarentena](#modelo-con-cuarentena)
  * [Modelo con tratamiento](#modelo-con-tratamiento)
* [Implementación](#implementacion)
  * [Librerías necesarias para la implementación](#librerias-necesarias-para-la-implementacion)
  
  * [Códigos base para los modelos](#codigos-base-para-los-modelos) 
  
  * [Simulaciones](#simulaciones) 
* [Conclusiones y resulatados ](#conclusiones-y-resultados)
* [Autores](#autores)

## Información general

Este proyecto busca mostrar el cambio en la demografía y el comportamiento de la población en el caso de que se diera una epidemia zombie. Los resultados obtenidos en este proyecto se mostrarán como gráficas o como animaciones dentro de un archivo .py. 

## Información previa

Los diferentes modelos utilizados y representados pueden encontrarse en los siguientes documentos:

* **Philip Munz, Ioan Hudea, Joe Imad, Robert J. Smith?** *WHEN ZOMBIES ATTACK!: MATHEMATICAL MODELLING OF AN OUTBREAK OF ZOMBIE INFECTION* In: **Infectious Disease Modelling Research Progress** `2009 Nova Science Publishers`

* [Zombie infection simulator](https://asymptote.wordpress.com/2008/01/13/asymptotes-zombie-infection-simulator/)

* [The Tortoise's Lense](http://thetortoiseslens.blogspot.com/2010/03/agent-based-computational-model-of.html)

El proyecto que realizamos se basa mayoritariamente en los modelos desarrolados por Munz, Hudea, Imad y Smith, los cuales son: 

* el modelo SIR, 

* el modelo con infección latente o SIRZ, 

* el modelo con cuarentena y 

* el modelo con tratamiento. 

### Modelo SIR

En el modelo básico, también llamado "Modelo SIR", se consideran tres categorías o tres tipos de agentes diferentes: 

* Susceptibles [S]: aquellas personas sanas que podrían ser infectadas

* Zombie [Z]: zombies

* Removidos [I]: personas muertas que puden regresar como zombies 

A partir de estos tres factores podemos optener tres ecuaciones que serán la base del modelo: 

$$
S'= \pi-\beta SZ-\delta S 


$$

$$
Z' = \beta SZ + \zeta R -\alpha SZ
$$

$$
R' = \delta S+ \alpha SZ - \zeta R
$$

En este modelo, $\alpha$ describe la capacidad de los Zombies para ser transferidos a la categoría de *Removidos*, esto es, ser eliminados completamente, lo cual únicmente se logra si se destruye su cerebro. Por otro lado, el parámetro $\beta$ corresponde a a probabilidad de que los *Susceptibles* se infecten y se conviertan en zombies. En este modelo, la probabilidad de que los *Susceptibles* puedan coonvertirse en *Removidos* por causas naturales está representada por el parámetro $\delta$, mientras que $\zeta$ son aquellos *Removidos* que podrán revivir como *Zombies*. Finalmente, es necesario agregar al modelo una constante que represente la tasa de nacimiento ($\pi$).  

En la FIgura 1 se muestra la relación entre cada tipo de agente y bajo qué parametros los agentes pueden pasar de un estado a otro. 

<img title="" src="file:///C:/Users/andyb/AppData/Roaming/marktext/images/2022-03-17-21-32-03-image.png" alt="" data-align="center">

### Modelo con infección latente (SIRZ)

En el modelo con infección latente se considera un cuarto caso en el que los humanos, después de ser mordidos por un zombie, pasan al menos 24 horas infectados antes de convertirse en *zombies*. En este caso, aparece un nuevo parámetro $\rho$ para mostrar la tasa de personas que se convertirá en *Infectados*. Esta nueva categoría es la de los *Infectados* [I]. De esta forma se obtienen nuevas ecuaciones para el modelo: 

$$
S' = \pi-\beta SZ-\delta S
$$

$$
I' =\beta SZ - \rho I-\delta I
$$

$$
Z' = \rho I + \zeta R - \alpha SZ
$$

$$
R' = \delta S + \delta I+ \alpha SZ - \zeta R
$$

Nuevamente mostramos la relación entre cada agente con ayuda de la Figura 2. 

<img src="file:///C:/Users/andyb/AppData/Roaming/marktext/images/2022-03-17-20-54-46-image.png" title="" alt="" data-align="center">

### Modelo con cuarentena

El modelo con cuarentena considera el caso en el que se pudiera separar a la población infecrada para que no propaguen la infección. Por este motivo, se le deben hacer unos cambios a los modelos anteriores: 

* el área de cuarentena sólo contiene miembros infectados o zombies, cuyas tasas de entrada corresponden a los parámetros $\kappa $ y $\sigma$ respectivamente;

* existe una posibilidad de que algunos miembros intenten escapar de la cuarentena, pero los matarán antes de que lo logren (parámetro $\gamma$);

* los individuos asesinados entrarán en la clase de removisos y podrán convertirse posteriormente en zombies.

A partir de esta nueva información se pueden plantear las ecuaciones del nuevo modelo de la siguiente manera: 

$$
S'=\pi -\beta SZ-\delta S
$$

$$
I'=\beta SZ - \rho I - \delta I -\kappa I
$$

$$
Z'=\rho =+ \zeta R - \alpha SZ - delta Z
$$

$$
R'=\delta S+ \delta I+\alpha SZ-\zeta R+\gamma Q
$$

$$
Q'=\kappa I+\delta Z-\gamma Q
$$

En la Figura 3 se ilustran las relaciones entre los diferentes agentes y sus parámetros de cambio. 

<img src="file:///C:/Users/andyb/AppData/Roaming/marktext/images/2022-03-17-21-38-48-image.png" title="" alt="" data-align="center">

### Modelo con tratamiento

Si se asume que se puede producir un tratamiento para el "zombie-ismo", entonces ya no sería necesaria la cuarentena y todos los individuos infectados podrían regresar a la categoría de susceptibles. Este modelo, sin embargo, no considera la posibilidad de que una persona pueda generar inmunidad frente a la infección zombie, por lo que en cualquier momento podría volver a infectarse. 

Tomando en cuenta la información anterior, obtenemos las siguientes ecuaciones: 

$$
S'=\pi -\beta SZ -\delta S+ cZ
$$

$$
I'=\beta SZ-\rho I - \delta I
$$

$$
Z'=\rho I + \zeta R - \alpha SZ-cZ
$$

$$
R' = \delta S +\delta I+ \alpha SZ -\zeta R
$$

Una representación gráfica de este modelo se puede ver en la Figura 4. 

<img src="file:///C:/Users/andyb/AppData/Roaming/marktext/images/2022-03-17-21-44-27-image.png" title="" alt="" data-align="center">

### Otros modelos

Adicionalmente, decidimos representar otros modelos a través de simulaciones. Uno de ellos, por ejemplo, es el caso en el que no sólo existan humanos y zombies, sino que se agreguen dos categorías más: humanos que luchan y humanos apanicados. En este modelos adicional se asume que habrá humanos que decidan luchar activamente contra los zombies (humanos que luchan) y otros que únicamente se apanicarán en presencia de un zombie

## Implementación

Nosotros decidimos realizar el proyecto utilizando Python, específicamente, Jupyter Notebook. 

### Librerías necesarias para la implementación

Es importante mencionar que, para poder correr el código del proyecto, son necesarias varias librerías que nos permitirán graficar e, incluso, animar el modelo de la epidemia zombie. Estas librerías se pueden ver en el bloque de código C.1.

```python
# C.1: Librerías necesarias para que funcione el código

```

### Códigos base para los modelos

Existen muchos modelos parecidos a los que se presentan en este proyecto, por lo que ya hay un código que se utiliza como base para, a partir de él, poder desarrollar el modelo específico que se desee. 

### Simulaciones

## Conclusiones y resultados

En cada uno de los diferentes modelos se obtuvo el mismo resultado: sin importar cuál sea la forma de lucha, tratamiento o evasión, o cuál sea la proporcionalidad entre los humanos y los zombies, la población zombie siempre ganará sobre la humana. Este comportamiento no sólo se ve en las gráficas sino también en las simulaciones, en las cuales podemos ver cómo cada persona se va convirtiendo en zombie o, en su defecto, cómo cada zombie va siendo eliminado. 

## Autores del proyecto

- Andrea Bellesia 

- Rubén Robles 

- Sebastián Ibarra 

- Alexei Murguia 

- Juan Jesús 
