# 21 / 03 / 2018

## Mixins

En esta clase continuamos explicando mixins.

### Deuda técnica

Como un side topic, incluimos una breve explicacin de [deuda técnica](https://www.agilealliance.org/wp-content/uploads/2016/05/IntroductiontotheTechnicalDebtConcept-V-02.pdf)

### Clases anónimas y traits anónimos

Así como en Java era posible tomar una interfaz `OnClickListener` y escribir algo como:

```java
OnClickListener someListener = new OnClickListener() {
    public void onClick() {
        // Do something
    }
}
```

En Scala también pueden instanciarse mixins anónimos.
Por ejemplo, si tenemos un mixin con un método implementado y otro requerido:

```scala
trait OnClickListener {
    def onClick():Unit
    
    def onLongClick():Unit = ??? // Do nothing
}
```

Podemos instanciarlo de forma anónima:

```scala

val someListener = new OnClickListener {
    override def onClick():Unit = ??? // Do something
}

```

### Stackable trait pattern

Explicamos el stackable trait pattern con el siguiente ejemplo:

```scala
package holascala

object ConsolaDeCafe {
  abstract class ConPrecio {
    def precio: Double
  }

  class Cafe extends ConPrecio {
    def precio: Double = 10
  }

  trait Leche extends ConPrecio {
    abstract override def precio: Double = super.precio + cantidadLeche * 20
    def porcentajeLeche: Double
    def cantidadLeche: Double = porcentajeLeche * tamañoRecipiente
    
    def tamañoRecipiente: Double
  }

  trait Chocolate extends ConPrecio {
    abstract override def precio: Double = super.precio + 5
  }
  
  trait Tamaño extends ConPrecio {
    abstract override def precio: Double = super.precio * multiplicador
    def multiplicador: Double
    def tamañoRecipiente: Double
  }

  trait Chico extends Tamaño {
    val multiplicador = 0.75
    val tamañoRecipiente: Double = 0.150
  }
  
  trait Mediano extends Tamaño {
    val multiplicador = 1.00
    val tamañoRecipiente: Double = 0.200
  }
  
  trait Descuento extends ConPrecio {
    abstract override def precio: Double = aplicarDescuento(super.precio)
    def descuento: Double
    def aplicarDescuento(valor: Double) = valor * (1 - descuento)
  }

  trait DescuentoEstudiante extends Descuento {
    val descuento = 0.1
  }
  
  trait HappyHour extends Descuento {
    val descuento = 0.2
  }

  def promo1 =
    new Cafe with Leche with Chico with DescuentoEstudiante {
      val porcentajeLeche = 0.1
    }

  def promo2 =
    new Cafe with Leche with Mediano {
      val porcentajeLeche = 0.9
    }

  def promo3 =
    new Cafe with Leche with Chocolate with Mediano with DescuentoEstudiante {
      val porcentajeLeche = 0.44
    }
}

object ConsolaApp extends App {
  println(ConsolaDeCafe.promo3.precio)
}
```

Más material en el sitio oficial de la materia: https://sites.google.com/site/programacionhm/conceptos/mixins#TOC-Stackable-Traits-Pattern
