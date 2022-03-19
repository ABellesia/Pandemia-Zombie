# Simulación de una epidemia Zombie
## Tabla de contendo
* [Descripción](#descripcion)
* [Información previa](#indormacion-previa) 
  * [Modelo SIR](#modelo-sir)
  * [Modelo con infección latente (SIRZ)](#modelo-con-infección-latente)
  * [Modelo con cuarentena](#modelo-con-cuarentena)
  * [Modelo con tratamiento](#modelo-con-tratamiento)
* [Implementación](#implementacion)
* [Conclusiones y resultados ](#conclusiones-y-resultados)
* [Autores](#autores)
* [Referencias](#referencias)
## Descripción
Actualmente es muy común ver películas, leer libros o jugar videojuegos que de alguna forma involucren *zombies*. A lo largo de los años, los *zombies* han ganado popularidad, causando que muchas personas se planteen una pregunta: ¿qué pasaría si realmente se diera una epidemia zombie?

Este proyecto busca mostrar el cambio y el comportamiento de la población en el caso de que el mundo sufirera una *apocalipsis zombie* utillizando ODE's y *agentes* en Python. Tomamos como *zombies* a todos aquellos seres que comen cerebros humanos e incluso pueden convertir a los humanos en nuevos *zombies* con una sola mordida. Igualmente, siguiendo las ideas que se han generado alrededor de las apocalipsis zombies, consideramos que el propósito de los humanos será escapar de los zombies y sobrevivir el mayor tiempo posible. 
## Información previa
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
A partir de estos tres factores podemos optener tres ecuaciones que son la base del modelo: 
![image](https://user-images.githubusercontent.com/88466180/159106513-0b974680-9715-4243-9502-fd4a2a5ba7b2.png)

En este modelo, $\alpha$ describe la capacidad de los Zombies para ser transferidos a la categoría de *Removidos*, esto es, ser eliminados completamente, lo cual únicmente se logra si se destruye su cerebro. Por otro lado, el parámetro $\beta$ corresponde a a probabilidad de que los *Susceptibles* se infecten y se conviertan en zombies. En este modelo, la probabilidad de que los *Susceptibles* puedan coonvertirse en *Removidos* por causas naturales está representada por el parámetro $\delta$, mientras que $\zeta$ son aquellos *Removidos* que podrán revivir como *Zombies*. Finalmente, es necesario agregar al modelo una constante que represente la tasa de nacimiento ($\pi$) para poder simular una sociedad lo mejor posible.   

En la *FIgura 1* se muestra la relación que existe entre cada tipo de agente y bajo qué parametros los agentes pueden pasar de un estado a otro. 

![fig1](https://user-images.githubusercontent.com/88466180/159106557-4c21282a-3184-4a2c-8b61-63cbc2456925.PNG)

### Modelo con infección latente (SIRZ)
En el modelo con infección latente se considera un cuarto caso en el que los humanos, después de ser mordidos por un zombie, pasan al menos 24 horas infectados antes de convertirse en *zombies*. En este caso, aparece un nuevo parámetro $\rho$ para mostrar la tasa de personas que se convertirá en *Infectados [I]*. De esta forma se obtienen nuevas ecuaciones para el modelo: 
![image](https://user-images.githubusercontent.com/88466180/159106583-cfd38768-56b4-413f-aae6-0b8857496d5a.png)

Nuevamente mostramos la relación entre cada agente con ayuda de la Figura 2. 

![fig2](https://user-images.githubusercontent.com/88466180/159106601-f650a581-fd24-448a-ab4e-01a2a3db18c1.PNG)

### Modelo con cuarentena
El modelo con cuarentena considera el caso en el que se pudiera separar a la población infecrada para que no propaguen la infección. Por este motivo, se le deben hacer unos cambios a los modelos anteriores: 
* el área de cuarentena sólo contiene miembros infectados o zombies, cuyas tasas de entrada corresponden a los parámetros $\kappa $ y $\sigma$ respectivamente;
* existe una posibilidad de que algunos miembros intenten escapar de la cuarentena, pero los matarán antes de que lo logren (parámetro $\gamma$);
* los individuos asesinados entrarán en la clase de removisos y podrán convertirse posteriormente en zombies.
A partir de esta nueva información se pueden plantear las ecuaciones del nuevo modelo de la siguiente manera: 

![image](https://user-images.githubusercontent.com/88466180/159106633-9c984544-e48b-4ddc-88ee-29b48f18cad9.png)

En la Figura 3 se ilustran las relaciones entre los agentes y sus parámetros de transición entre estados. 

![fig3](https://user-images.githubusercontent.com/88466180/159106641-b9266c57-a4c1-46ea-8362-9a3eba0882b1.PNG)

### Modelo con tratamiento
Si se asume que se puede producir un tratamiento para el "zombie-ismo", entonces ya no sería necesaria la cuarentena y todos los individuos infectados podrían regresar a la categoría de susceptibles. Este modelo, sin embargo, no considera la posibilidad de que una persona pueda generar inmunidad frente a la infección zombie, por lo que en cualquier momento podría volver a infectarse. 

Tomando en cuenta la información anterior, obtenemos las siguientes ecuaciones: 

![image](https://user-images.githubusercontent.com/88466180/159106662-1d2c9793-4861-4c6f-bb1c-ca446a40e397.png)

Una representación gráfica de este modelo se puede ver en la Figura 4. 

![fig4](https://user-images.githubusercontent.com/88466180/159106674-09cad219-e7b8-4f2c-820d-240ccad2b5ed.PNG)

### Otros modelos
Adicionalmente, decidimos representar otros modelos a través de *simulaciones de mundo*. Uno de ellos, por ejemplo, es el caso en el que no sólo existan humanos y zombies, sino que se agreguen dos categorías más: *humanos que luchan* y *humanos apanicados*. En este modelos adicional se asume que habrá humanos que decidan luchar activamente contra los zombies y los logren matar (*humanos que luchan*), y otros que únicamente se apanicarán en presencia de un zombie (*humanos apanicados*); sin embargo, esto no significa que deban permanecer en estas categorías hasta ser convertidos en zombies. Un *humano que lucha* puede convertirse en un *humano apanicado* si está rodeado de muchos agentes del segundo tipo, y viceversa: si un *humano apanicado* está rodeado de muchos *humanos que luchan*, podrá tomar valor y decidir luchar. 
## Implementación
Este programa se desarrolló utilizando Python en Jupyter Notebook. Para resolver los sistemas de ecuaciones utilizamos el método de Euler para ODE's. Este método se repitió para cada uno de los diferentes modelos de la epidemia. Adicionalmente se agregaron algunas funciones que nos ayudaron a graficar el cambio en el población en el tiempo. 
Además de los modelos presentados en el artículo de Munz, realizamos dos simulaciones del mundo con una epidemia zombie. Para esto nos apoyamos en el concepto de *agentes* en Pyhton, el cual consta de crear un *mundo*, y un *agente* que se moverá dentro de ese mundo. 

```python
#Definición general de la clase Mundo
class Mundo:
    def __init__(self, agentes, ancho=8, alto=8, steps = 20):
        self.agentes = agentes
        self.num_zombie = len([agente for agente in self.agentes if agente.tipo == 'Zombie'])
        self.num_humano = len([agente for agente in self.agentes if agente.tipo == 'Humano'])
        self.list_zombie = []
        self.list_humano = []
        self.ancho = ancho
        self.alto = alto
        self.steps = steps
        self.init_anim()

    def init_anim(self):
        self.fig = plt.figure(figsize=(self.ancho, self.alto))
        self.ax = plt.axes(xlim=(0, 1), ylim=(0, 1))
        plot_args = {'markersize' : 8, 'alpha' : 0.6}
        self.puntos, = self.ax.plot([], [], 'o', **plot_args)
def dibujar(self, step):
        x_values_0, y_values_0 = [], []
        for agente in self.agentes:
            x, y = agente.locacion
            x_values_0.append(x)
            y_values_0.append(y)

        self.puntos.set_data(x_values_0, y_values_0)

        self.ax.set_title('Paso {}'.format(step))

        return self.puntos,

    def actualizar(self, step):   
        self.dibujar(step) # Dibuja el mundo

        for agente in self.agentes:
            agente.actualizar(self.agentes)

        self.list_zombie.append(self.num_zombie)
        self.list_humano.append(self.num_humano)
        self.num_zombie = len([agente for agente in self.agentes if agente.tipo == 'Zombie'])
        self.num_humano = len([agente for agente in self.agentes if agente.tipo == 'Humano'])

    def clean_screen(self):
        self.puntos.set_data([], [])
        return self.puntos,

    def simular(self):
        anim = animation.FuncAnimation(self.fig, self.actualizar, init_func=self.clean_screen, frames=self.steps, interval=1000, blit=False)
        return anim
```

```python
#Definición general de la clase Agente
class Agente:
    """ Agente general """
    def __init__(self, tipo):
        self.tipo = tipo
    def distancia(self, otro):
        pass
    def actuar(self, agentes):
        pass
    def decidir(self, agentes):
        pass
    def actualizar(self, agentes):
        pass
```

Posteriormente, creamos clases derivadas del *Mundo* y del *Agente*, las cuales representarían al *Mundo apocalíptico*, a los humanos y a los zombies. En estas clases se definieron las características de cada uno de los agentes y su comportamiento al enfrentarse o acercarse a otros agentes de tipos diferentes. Esas clases adicionales las nombramos: 
- Mundo_apocaliptico
- Zombie
- Human
- Mundo_Zombie
- Fighting_Human
- Panicked_Human
## Conclusiones y resultados
En cada uno de los diferentes modelos se obtuvo el mismo resultado: sin importar cuál sea la forma de lucha, tratamiento o evasión, o cuál sea la proporcionalidad entre los humanos y los zombies, la población zombie siempre ganará sobre la humana. Este comportamiento no sólo se ve en las gráficas sino también en las simulaciones, en las cuales podemos ver cómo cada persona se va convirtiendo en zombie o, en su defecto, cómo cada zombie va siendo eliminado. En las gráficas 1 a 4 se muestra cómo van cambiando, tanto la población humana, como la población zombie. 

![Gráfica1](https://user-images.githubusercontent.com/88466180/159106714-f107be94-c463-4da5-bcdc-3f2e15f8105b.PNG) 
![Gráfica2](https://user-images.githubusercontent.com/88466180/159106718-2f3e0ddc-741b-4397-89fe-32a8bb0a38c4.PNG)
![Gráfica3](https://user-images.githubusercontent.com/88466180/159106729-667333db-643b-471d-85a4-b4ed78467076.PNG)
![Gráfica4](https://user-images.githubusercontent.com/88466180/159106732-b120d2ab-2fef-47aa-82cb-b84de2701d4c.PNG)

El mismo comportamiento se puede observar en los resultados obtenidos por la simulación del modelo básico, el cual se presenta en la Gráfica 5.

![Gráfica5](https://user-images.githubusercontent.com/88466180/159106745-36bbfc4f-7cac-47f1-ad07-de4fa452ea65.PNG)

Sin embargo, el segundo modelo representado a través de *agentes* muestra un resultado diferente al de los demás modelos, pues asume que algunos humanos podrán matar o eliminar completamente a un zombie. Por lo tanto, en este modelo la población zombie no termina por reemplazar por completo a la población humana, sino que disminuye con el tiempo. En la Gráfica 6 podemos observar cómo la cantidad o la existencia de cada tipo de agente tiende a cero mientras más tiempo pase. 

![Gráfica6](https://user-images.githubusercontent.com/88466180/159106748-1c4b827e-f80f-40ae-8c4c-1c1c3137efea.PNG)

## Autores del proyecto
- Andrea Bellesia 
- Rubén Robles 
- Sebastián Ibarra 
- Alexei Murguia 
- Juan Jesús Rodríguez
## Referencias
- **Philip Munz, Ioan Hudea, Joe Imad, Robert J. Smith?** *WHEN ZOMBIES ATTACK!: MATHEMATICAL MODELLING OF AN OUTBREAK OF ZOMBIE INFECTION* In: **Infectious Disease Modelling Research Progress** `2009 Nova Science Publishers`
- [Zombie infection simulator](https://asymptote.wordpress.com/2008/01/13/asymptotes-zombie-infection-simulator/)
- [The Tortoise's Lense](http://thetortoiseslens.blogspot.com/2010/03/agent-based-computational-model-of.html)

