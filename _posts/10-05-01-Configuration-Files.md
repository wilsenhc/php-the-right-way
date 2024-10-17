---
title:   Archivos de Configuración
isChild: true
anchor:  archivos_de_configuracion
---

## Archivos de Configuración {#archivos_de_configuracion_title}

Al crear archivos de configuración para sus aplicaciones, las mejores prácticas recomiendan que se siga uno de los siguientes métodos
siguientes:

- Se recomienda almacenar la información de configuración en un lugar al que no se pueda acceder directamente
y al que no se pueda acceder a través del sistema de archivos.
- Si debe almacenar los archivos de configuración en la raíz del documento, nómbrelos con la extensión `.php`. Esto garantiza que,
aunque se acceda directamente al script, no se mostrará como texto sin formato.
- La información de los archivos de configuración debe protegerse en consecuencia, ya sea mediante cifrado o permisos de grupo/usuario en el sistema de archivos.
- Es una buena idea asegurarse de no confirmar (del inglés _commit_) archivos de configuración que contengan información sensible, por ejemplo, contraseñas o tokens de API al control de código fuente.
