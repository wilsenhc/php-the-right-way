---
title:   Registro de Globales
isChild: true
anchor:  registro_de_globales
---

## Registro de Globales {#registro_de_globales_title}

**NOTA:** A partir de PHP 5.4.0 el parámetro `register_globals` ha sido eliminado y ya no puede ser usado.
Esto sólo se incluye como una advertencia para cualquier persona en el proceso de actualización de una aplicación de legado.

Cuando está activada, la configuración `register_globals` hace que varios tipos de variables (incluyendo las de `$_POST`,
`$_GET` y `$_REQUEST`) estén disponibles en el ámbito global de tu aplicación. Esto puede llevar
fácilmente a problemas de seguridad ya que tu aplicación no puede saber de dónde vienen los datos.

Por ejemplo: `$_GET['foo']` estaría disponible a través de `$foo`, lo cual puede anular variables que hayan sido declaradas.

Si estás usando PHP < 5.4.0 __asegúrate__ de que `register_globals` está __desactivado__.
