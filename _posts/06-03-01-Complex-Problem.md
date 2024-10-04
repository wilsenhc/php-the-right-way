---
title:   Problema Complejo
isChild: true
anchor:  problema_complejo
---

## Problema Complejo {#problema_complejo_title}

Si alguna vez has leído sobre Inyección de Dependencias es probable que hayas visto los términos *"Inversión de control"* o 
*"Principio de Inversión de Dependencias"*. Estos son los problemas complejos que resuelve la Inyección de Dependencias.

### Inversión de Control

Inversión de Control, como su nombre lo indica, es "invertir el control" de un sistema al mantener el control organizacional completamente separado de nuestros objetos. En términos de Inyección de Dependencias, esto significa desacoplar nuestras dependencias al controlarlas e instanciarlas en otras partes del sistema.

Durante años, los frameworks PHP han estado logrando la Inversión de Control, sin embargo, surge la pregunta, ¿qué parte del control estamos invirtiendo y hacia dónde? Por ejemplo, los frameworks MVC generalmente proveen un superobjeto o controlador base que otros controladores deben extender para obtener acceso a sus dependencias. Esto **es** Inversión de Control, sin embargo, en lugar de desacoplar las dependencias, este método simplemente las mueve.

La Inyección de Dependencia nos permite resolver este problema de una forma mas elegante al inyectar solamente las dependencias que necesitamos, cuando la necesitamos sin la necesidad de tener dependencias en duro.

### S.O.L.I.D.

#### Principio de Responsabilidad Única

El Principio de Responsabilidad Única (en inglés _Single Responsibility Principle_) se refiere a
los actores y a la arquitectura de alto nivel.
Establece que “Una clase debería tener solo una razón para cambiar”.
Esto significa que cada clase debería _solo_ tener responsabilidad sobre una única parte de la
funcionalidad proporcionada por el software. El mayor beneficio de este enfoque es que permite una mejor
_reutilización_ del código. Al diseñar nuestras clases para que hagan solo una cosa, podemos utilizar (o reutilizarlas) en cualquier otro programa sin cambiarlas.

#### Principio Abierto/Cerrado

El Principio abierto/cerrado (_Open/Closed Principle_) se refiere al diseño de clases y la
extensión de funcionalidades. Establece que "Las entidades de software (clases,
módulos, funciones, etc.) deben estar abiertas a la extensión, pero cerradas a la modificación".
Esto significa que debemos diseñar nuestros módulos, clases y funciones de manera que cuando se
necesite una nueva funcionalidad, no deberíamos modificar nuestro código existente sino que
escribamos código nuevo que será utilizado por el código existente. En términos prácticos,
esto significa que deberíamos escribir clases que implementen y respeten las _interfaces_,
luego hacer sugerencias de tipos hacía esas interfaces en lugar de clases específicas.

El mayor beneficio de este enfoque es que podemos extender nuestro código muy fácilmente con soporte para algo nuevo sin tener que modificar el código existente, lo que significa que podemos reducir el tiempo de Control de Calidad (QA) y el riesgo de un impacto negativo a la aplicación se reduce considerablemente. Podemos desplegar nuevo código más rápido y con más confianza.

#### Principio de Sustitución de Liskov

El Principio de Sustitución de Liskov (_Liskov Substitution Principle_) se refiere a la subtipificación y la herencia.
Establece que “Las clases hijas nunca deben romper las definiciones de tipo de la clase padre”. O, en palabras de Robert C. Martin,
“Los subtipos deben ser sustituibles por sus tipos base”.

Por ejemplo, si tenemos una interfaz `FileInterface` que define un método `embed()`, y contamos con las clases `Audio` y `Video`
las cuales implementan esta interfaz `FileInterface`, podemos esperar que el uso del método `embed()` siempre haga lo que pretendemos.
Si más adelante creamos una clase `PDF` o una clase `Gist` que también implementen la interfaz `FileInterface`, ya sabremos
y entenderemos lo que hará el método `embed()`. El mayor beneficio de este enfoque es que tenemos la capacidad de construir
programas flexibles y fácilmente configurables, ya que cuando cambiamos un objeto de un tipo (por ejemplo, `FileInterface`)
por otro, no necesitamos modificar más nada en nuestro programa.

#### Principio de Segregación de Interfaces

El Principio de Segregación de Interfaces (_Interface Segregation Principle_, ISP
por sus siglas en inglés) trata sobre la comunicación entre la _lógica de negocio_ y los _clientes_.
Establece que “Ningún cliente debería verse obligado a depender de métodos que no utiliza”.
Esto quiere decir que en lugar de tener una única interfaz monolítica que todas las clases
conformantes deben implementar, deberíamos en su lugar proporcionar un conjunto de interfaces
más pequeñas y específicas por concepto que una clase conformante implemente una o más de ellas.

Por ejemplo, una clase `Car` o `Bus` estaría interesada en un método `steeringWheel()`, pero una
clase `Motorcycle` o `Tricycle` no lo estaría. Por otro lado, una clase `Motorcycle` o `Tricycle`
se interesaría en un método `handlebars()`, mientras que una clase `Car` o `Bus` no. No es necesario
que todos estos tipos de vehículos implementen soporte tanto para `steeringWheel()` como para `handlebars()`,
por lo que deberíamos descomponer la interfaz original.

#### Principio de Inversión de Dependencias

El Principio de Inversión de Dependencias (_Dependency Inversion Principle_) trata sobre eliminar los vínculos rígidos entre
clases discretas para que se pueda aprovechar nueva funcionalidad al pasar una clase diferente.
Establece que se debe *"depender de abstracciones. No depender de implementaciones"*.
En términos simples, esto significa que nuestras dependencias deberían ser interfaces/contratos
o clases abstractas en lugar de implementaciones concretas. Podemos fácilmente refactorizar
el ejemplo anterior para seguir este principio.

{% highlight php %}
<?php
namespace Database;

class Database
{
    public function __construct(protected AdapterInterface $adapter)
    {
    }
}

interface AdapterInterface {}

class MysqlAdapter implements AdapterInterface {}
{% endhighlight %}

Hay varios beneficios al hacer que la clase `Database` ahora dependa de una interfaz en lugar de una implementación concreta.

Consideremos que estamos trabajando en un equipo y el adaptador está siendo desarrollado por un colega.
En nuestro primer ejemplo, tendríamos que esperar a que dicho colega termine el adaptador antes de poder
simularlo adecuadamente para nuestras pruebas unitarias. Ahora que la dependencia es una interfaz/contrato,
podemos simular esa interfaz sin problemas, sabiendo que nuestro colega construirá el adaptador basado en ese contrato.

Un beneficio incluso aún mayor de este enfoque es que nuestro código ahora es mucho más escalable. Si dentro de
un año decidimos que queremos migrar a un tipo diferente de base de datos, podemos escribir un adaptador que implemente
la interfaz original e inyectar eso en su lugar, no se requeriría más refactorización ya que podemos asegurar que el
adaptador sigue el contrato establecido por la interfaz.
