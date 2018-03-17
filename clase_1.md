# 14 / 03 / 2018

## Introducción a la materia

### Link Útiles

 - Sitio de la materia: https://sites.google.com/site/programacionhm/unq
 - Github con Tps anteriores, bitácoras y algunos enunciados de semestres anteriores https://github.com/unq-objetos3-alumnos
 - Github con ejemplos de la materia https://github.com/orgs/uqbar-paco (tip: filren por "obj3")
 - Canal de youtube (algo viejo pero puede tener cosas útiles): https://www.youtube.com/channel/UC20rhT1zAZyVRZuRqukk74Q/videos
 
### Forma de evaluación

 - 3 trabajos prácticos, dos instancias de recuperación para cada TP.
 - 3 integrantes por TP.

### Qué vimos

 - Se repasaron brevemente conceptos vistos en materias anteriores (clases, interfaces, polimorfismo, etc.)
  - Se comentó que la materia tiene tres pilares: 
     - 1) Extensiones al paradigma de objetos (Mixins).
     - 2) Influencias de programación funcional en POO.
     - 3) Metaprogramación.
 - Dimos una introducción al lenguaje Scala
 - Mostramos opciones de building tools: Eclipse config, Gradle y SBT. Recomendamos usar Gradle por ser la más sencilla y que probablemente hayan usado con anterioridad o usen en el futuro.
 - Se introdujo el concepto de tipado estructural y se lo comparó con el tipado nominal.
 - Presentamos el ejercicio "Age of Empires" y planteamos diferentes soluciones. Una planteada con herencia simple, otra con composición y finalmemte otra introduciendo la idea de mixins. En este repositorio pueden encontrar lo que hicimos en clase https://github.com/unq-objetos3-alumnos/2018s1-clase1-age-scala
 - Se explicó brevemente la diferencia entre herencia múltiple y mixins. Se introdujo el concepto de linearización como un sistema resolución automática de conflictos.


## Para la clase siguiente

 - Completar el formulario de grupos para TPs (se enviará el link por mail).
 - Leer el paper de [Mixins](https://d8a0dde1-a-62cb3a1a-s-sites.googlegroups.com/site/programacionhm/conceptos/mixins/Paper%20-%20Bracha%2C%20Cook%20-%20Mixin-Based%20Inheritance.pdf?attachauth=ANoY7cqbcrZ3pmTTzR7PWq9dJQqoJERPbWgsN1HOkIl5vHo7Z8YFAS2khfzq3v-M8rHTsGGl9NT4LW87Z6evHTc_1g7oCfGw0SQG_VyjVZtyIC5utmPvI-c10Y_l2tTCfNxxkckw9OGDFJt9nARVAhUTfHSp9RulcrVxCfAncjES63FC6XTzuVtUp-DQXtKJac-fzFcpxaFApQmwFkGI2gAXF9JdZpSie6ov4LlGtDjEGcP-nkNzeHvAGo45sMNnJxncfTUK9ndQDLiSXIeWjlq-7FKr5sYK8mpfYlUKNQBI7oatfpkUHHA%3D&attredirects=0)
 - Opcional: para aquellos que necesiten practicar uso de bloques y colecciones, pueden resolver los ejercicios que aparecen a continuación.

### Algunos ejercicios para repasar uso de colecciones:

En [el sitio de la materia](https://sites.google.com/site/programacionhm/te/scala/introduccin-a-scala) pueden encontrar material útil.

Dadas las clases:

```scala
class Casa(val direccion:String, val ambientes:Int) {
    override def toString = s"\n  ${this.getClass().getSimpleName}(direccion=$direccion, ambientes=$ambientes)"
}

class Departamento(dir:String, val piso:Int, val numero:Int, cantidadAmbientes:Int) 
extends Casa(s"$dir, piso $piso, departamento $numero", cantidadAmbientes) 

class Edificio(val departamentos:Seq[Departamento]) {
    override def toString = s"\n  Edificio( departamentos=$departamentos )"
}

``` 

Donde la cantidad de pisos de un edificio está dada por mayor número de piso entre sus departamentos.

Y dadas las colecciones

```scala
val casas = List(
    new Casa("Calle falsa 1234", 5),
    new Casa("Lalala 23", 2),
    new Casa("Chiquita 44", 1),
    new Casa("Mediana 98", 3)
)

val edificios = List( 
    new Edificio(List( new Departamento(dir="Calle falsa 1111", piso=1, numero=1, cantidadAmbientes=3)))
) // Completar con casos representativos 

```

Obtener:

 - La cantidad de casas con más de 2 ambientes
 - Las casas con un ambiente
 - La cantidad de edificios con más de 10 departamentos
 - Todos los departamentos
 - Las direcciones de todos los departamentos de un edificio
 - El edificio con el departamento con más ambientes (si hay varios con la misma cantidad basta con obtener uno de ellos)
 - Los edificios con más de 3 pisos
 - Todos los departamentos que son monoambientes.
 - La cantidad total de departamentos
 - Las direcciones de los departamentos de más de un ambiente que se encuentran en edificios de menos de 3 pisos
 - Los edificios con departamentos que tengan cantidad de ambientes par, ordenados de mayor a menor según cantidad de pisos.

------

## Cómo usar los repositorios de cada grupo

Una vez completado el formulario de los grupos, a cada grupo se le asignará un team de github y 3 repositorios privados (uno para cada TP).
Para el primer TP (y para las clases), van a necesitar tener instalado el entorno de Scala, para esto los pasos serían:

 - Tener instalado JDK 8 (esto lo tienen de Objetos 2 así que no voy a ahondar en eso, si tienen dudas pregunten por la lista)
 - IDE Intellij:
     - Descargar el [Intellij](https://www.jetbrains.com/idea/#chooseYourEdition) community edition
     - Tildar la opcion de usar plugin de Scala durante el wizard de instalación o bien instalar el plugin de Scala: abren el Intellij y en la pantalla de bienvenida: Configure -> PLugins -> Buscan Scala -> instalar
 - IDE Eclipse:
     - Descargar el [ScalaIDE](http://scala-ide.org/)
     - Instalar el [plugin de Gradle](https://projects.eclipse.org/projects/tools.buildship) si deciden usarlo como building tool (o bien pueden usar SBT)
 - Al crear un proyecto scala, agreguen como framework de testing [ScalaTest](http://www.scalatest.org/).
     
