---
title:   Contenedores
isChild: true
anchor:  contenedores
---

## Contenedores {#contenedores_title}

Lo primero que deberías entender sobre los Contenedores de Inyección de Dependencias es que no son lo mismo que la
Inyección de Dependencias. Un contenedor es una herramienta de conveniencia que nos ayuda a implementar la Inyección
de Dependencias; sin embargo, pueden ser y a menudo se usan de forma incorrecta para implementar un anti-patrón,
Localización de Servicios. Inyectar un contenedor de DI como Localizador de Servicios en tus clases puede crear una
dependencia más fuerte en el contenedor que la dependencia que estás reemplazando. Esto además hace que tu código sea
mucho menos transparente y en última instancia más difícil de probar.

La mayoría de los frameworks modernos tienen su propio Contenedor de Inyección de Dependencias que te permite conectar
tus dependencias a través de la configuración. Lo que esto significa en la práctica es que puedes escribir código de
aplicación que sea tan limpio y desacoplado como el framework en el que se basa.
