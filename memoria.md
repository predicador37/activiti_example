# Modelado y automatización de un proceso de gestión de tickets de incidencias de una organización

## Determinación de los elementos esenciales del proceso

### Tareas de usuario

- Apertura de ticket de primer nivel
- Apertura de ticket de segundo nivel
- Justificación de no solución
- Actualización de información en el sistema

### Tareas de servicio

- Envío de email informando de solución del problema
- Envio de email informando de la situación

### Gateways

- Gateway exclusivo de solución de ticket en primer nivel o no
- Gateway exclusivo de solución de ticket en segundo nivel o no

### Flujos

- Nodo inicial - Tarea de usuario *Apertura de ticket de primer nivel*
- Tarea de usuario *Apertura de ticket de primer nivel* - Gateway exclusivo de solución de ticket en primer nivel o no
- Gateway exclusivo de solución de ticket en primer nivel o no - Tarea de usuario *Apertura de ticket de segundo nivel*
- Gateway exclusivo de solución de ticket en primer nivel o no - Tarea de servicio *Envío de email informando de solución del problema*
- Tarea de usuario *Apertura de ticket de segundo nivel* - Gateway exclusivo de solución de ticket en segundo nivel o no
- Gateway exclusivo de solución de ticket en segundo nivel o no - Tarea de usuario *Justificación de no solución*
- Gateway exclusivo de solución de ticket en segundo nivel o no - Tarea de servicio *Envío de email informando de solución del problema*
- Tarea de usuario *Justificación de no solución* - Tarea de servicio *Envío de email informando de situación*
- Tarea de servicio *Envío de email informando de solución del problema* - Tarea de usuario *Actualización de información en el sistema*
- Tarea de servicio *Envío de email informando de situación* - Nodo final
- Tarea de usuario *Actualización de información en el sistema* - Nodo final

### Eventos

- Nodo inicial.

## Edición gráfica

Para la edición gráfica se ha optado por utilizar *Activiti Modeler* generando un fichero XML retocado manualmente y verificado importando y exportando de nuevo desde *Activiti*.

## Incorporación de formularios y datos al proceso

Para incorporar los formularios se ha utilizado el motor integrado de *Activiti* JUEL embebido en el documento XML. Se ha comprobado su validez estructural y semántica utilizando los ficheros de definición de esquema (`.xsd`) proporcionados y el editor [Jetbrains Webstorm](https://www.jetbrains.com/webstorm/).

Para dirigir los flujos de proceso se han utilizado condiciones en los gateways tomados desde los formularios. En este caso se han utilizado las variables `ResueltoPrimerNivel` y `ResueltoSegundoNivel` de los formularios asociados a cada tarea correspondientes para dirigir dichos flujos.

En el caso de los datos necesarios para el envío de e-mail, se han definido los campos obligatorios (remitente, destinatario, asunto y cuerpo del mensaje en texto plano) con contenido apropiado al efecto (notificando del cierre de los tickets o del motivo de no resolución).

El usuario asignado a todas las tareas de usuario ha sido `kermit`, a efectos de la demostración requerida en el enunciado de esta práctica. En un entorno real, deberían asignarse a sus usuarios correspondientes.

El servidor de correo electrónico y los datos de autenticación (de prueba y creados expresamente para esta práctica) se han configurado en el archivo `activiti-custom-context.xml` (proporcionado en los entregables), tal y como se ha desprendido de los [foros de *Activiti*](https://forums.activiti.org/content/external-mailserver-configuration-activiti-explorer-and-tomcat), ya que en la documentación no hace referencia a ello cuando se trata tan sólo del componente *Activity Explorer*. La cuenta y el servidor de correo externo de prueba pertenecen a `Gmail`.

