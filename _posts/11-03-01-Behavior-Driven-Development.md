---
title:   Desarrollo Guiado por Comportamiento
isChild: true
anchor:  behavior_driven_development
---

## Desarrollo Guiado por Comportamiento {#behavior_driven_development_title}

Existen dos tipos diferentes de Desarrollo Guiado por Comportamiento (BDD): SpecBDD y StoryBDD. SpecBDD se centra
en el comportamiento técnico del código, mientras que StoryBDD se centra en los comportamientos o interacciones del negocio
o de las características. PHP tiene frameworks para ambos tipos de BDD.

Con StoryBDD, se escriben historias legibles que describen el comportamiento de la aplicación. Estas historias se pueden ejecutar
como pruebas reales contra su aplicación. El framework utilizado en aplicaciones PHP para StoryBDD es [Behat], que está inspirado
en el proyecto [Cucumber] de Ruby e implementa el DSL Gherkin para describir el comportamiento de las características.

Con SpecBDD, se escriben especificaciones que describen cómo debe comportarse el código real. En lugar de probar una función o método,
usted está describiendo cómo esa función o método debe comportarse. PHP ofrece el framework [PHPSpec] para este propósito.
Este framework está inspirado en el [proyecto RSpec][Rspec] para Ruby.

### Enlaces de BDD

* [Behat], el framework StoryBDD para PHP, inspirado en el proyecto [Cucumber] de Ruby;
* [PHPSpec], el framework SpecBDD para PHP, inspirado en el proyecto [RSpec] de Ruby;
* [Codeception] es un marco de pruebas de pila completa que utiliza los principios de BDD.


[Behat]: https://behat.org/
[Cucumber]: https://cucumber.io/
[PHPSpec]: https://www.phpspec.net/
[RSpec]: https://rspec.info/
[Codeception]: https://codeception.com/
