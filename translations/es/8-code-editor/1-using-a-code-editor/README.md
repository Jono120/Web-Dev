<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "1ba61d96a11309a2a6ea507496dcf7e5",
  "translation_date": "2025-08-29T13:59:46+00:00",
  "source_file": "8-code-editor/1-using-a-code-editor/README.md",
  "language_code": "es"
}
-->
# Usando un editor de código

Esta lección cubre los conceptos básicos de cómo usar [VSCode.dev](https://vscode.dev), un editor de código basado en la web, para que puedas realizar cambios en tu código y contribuir a un proyecto sin necesidad de instalar nada en tu computadora.

## Objetivos de aprendizaje

En esta lección, aprenderás a:

- Usar un editor de código en un proyecto de programación
- Rastrear cambios con control de versiones
- Personalizar el editor para el desarrollo

### Prerrequisitos

Antes de comenzar, necesitarás crear una cuenta en [GitHub](https://github.com). Dirígete a [GitHub](https://github.com/) y crea una cuenta si aún no lo has hecho.

### Introducción

Un editor de código es una herramienta esencial para escribir programas y colaborar en proyectos de programación existentes. Una vez que entiendas los conceptos básicos de un editor y cómo aprovechar sus funciones, podrás aplicarlos al escribir código.

## Comenzando con VSCode.dev

[VSCode.dev](https://vscode.dev) es un editor de código en la web. No necesitas instalar nada para usarlo, es como abrir cualquier otro sitio web. Para comenzar con el editor, abre el siguiente enlace: [https://vscode.dev](https://vscode.dev). Si no has iniciado sesión en [GitHub](https://github.com/), sigue las indicaciones para iniciar sesión o crear una cuenta nueva y luego inicia sesión.

Una vez que se cargue, debería verse similar a esta imagen:

![VSCode.dev por defecto](../../../../translated_images/default-vscode-dev.5d06881d65c1b3234ce50cd9ed3b0028e6031ad5f5b441bcbed96bfa6311f6d0.es.png)

Hay tres secciones principales, comenzando desde la izquierda y moviéndose hacia la derecha:

1. La _barra de actividad_, que incluye algunos íconos, como la lupa 🔎, el engranaje ⚙️ y algunos otros.
2. La barra de actividad expandida, que por defecto muestra el _Explorador_, llamada la _barra lateral_.
3. Y finalmente, el área de código a la derecha.

Haz clic en cada uno de los íconos para mostrar un menú diferente. Una vez que termines, haz clic en el _Explorador_ para volver al punto de inicio.

Cuando empieces a crear código o modificar código existente, esto sucederá en el área más grande a la derecha. Usarás esta área para visualizar código existente también, lo cual harás a continuación.

## Abrir un repositorio de GitHub

Lo primero que necesitarás es abrir un repositorio de GitHub. Hay múltiples formas de abrir un repositorio. En esta sección verás dos maneras diferentes de abrir un repositorio para comenzar a trabajar en los cambios.

### 1. Con el editor

Usa el propio editor para abrir un repositorio remoto. Si vas a [VSCode.dev](https://vscode.dev), verás un botón de _"Abrir repositorio remoto"_:

![Abrir repositorio remoto](../../../../translated_images/open-remote-repository.bd9c2598b8949e7fc283cdfc8f4050c6205a7c7c6d3f78c4b135115d037d6fa2.es.png)

También puedes usar la paleta de comandos. La paleta de comandos es un cuadro de entrada donde puedes escribir cualquier palabra que sea parte de un comando o acción para encontrar el comando correcto para ejecutar. Usa el menú en la parte superior izquierda, luego selecciona _Ver_ y elige _Paleta de comandos_, o utiliza el siguiente atajo de teclado: Ctrl-Shift-P (en MacOS sería Command-Shift-P).

![Menú de paleta](../../../../translated_images/palette-menu.4946174e07f426226afcdad707d19b8d5150e41591c751c45b5dee213affef91.es.png)

Una vez que se abra el menú, escribe _abrir repositorio remoto_ y selecciona la primera opción. Aparecerán múltiples repositorios de los que formas parte o que has abierto recientemente. También puedes usar una URL completa de GitHub para seleccionar uno. Usa la siguiente URL y pégala en el cuadro:

```
https://github.com/microsoft/Web-Dev-For-Beginners
```

✅ Si es exitoso, verás todos los archivos de este repositorio cargados en el editor de texto.

### 2. Usando la URL

También puedes usar directamente una URL para cargar un repositorio. Por ejemplo, la URL completa del repositorio actual es [https://github.com/microsoft/Web-Dev-For-Beginners](https://github.com/microsoft/Web-Dev-For-Beginners), pero puedes reemplazar el dominio de GitHub con `VSCode.dev/github` y cargar el repositorio directamente. La URL resultante sería [https://vscode.dev/github/microsoft/Web-Dev-For-Beginners](https://vscode.dev/github/microsoft/Web-Dev-For-Beginners).

## Editar archivos

Una vez que hayas abierto el repositorio en el navegador/vscode.dev, el siguiente paso será realizar actualizaciones o cambios en el proyecto.

### 1. Crear un archivo nuevo

Puedes crear un archivo dentro de una carpeta existente o en el directorio/carpeta raíz. Para crear un archivo nuevo, abre una ubicación/directorio donde quieras guardar el archivo y selecciona el ícono _'Nuevo archivo ...'_ en la barra de actividad _(izquierda)_, dale un nombre y presiona enter.

![Crear un archivo nuevo](../../../../translated_images/create-new-file.2814e609c2af9aeb6c6fd53156c503ac91c3d538f9cac63073b2dd4a7631f183.es.png)

### 2. Editar y guardar un archivo en el repositorio

Usar vscode.dev es útil cuando quieres realizar actualizaciones rápidas a tu proyecto sin tener que cargar ningún software localmente.  
Para actualizar tu código, haz clic en el ícono 'Explorador', también ubicado en la barra de actividad, para ver los archivos y carpetas en el repositorio.  
Selecciona un archivo para abrirlo en el área de código, realiza tus cambios y guarda.

![Editar un archivo](../../../../translated_images/edit-a-file.52c0ee665ef19f08119d62d63f395dfefddc0a4deb9268d73bfe791f52c5807a.es.png)

Una vez que hayas terminado de actualizar tu proyecto, selecciona el ícono _`control de origen`_, que contiene todos los nuevos cambios que has realizado en tu repositorio.

Para ver los cambios que realizaste en tu proyecto, selecciona los archivos en la carpeta `Cambios` en la barra de actividad expandida. Esto abrirá un 'Árbol de trabajo' para que visualices los cambios realizados en el archivo. El color rojo muestra una omisión en el proyecto, mientras que el verde indica una adición.

![Ver cambios](../../../../translated_images/working-tree.c58eec08e6335c79cc708c0c220c0b7fea61514bd3c7fb7471905a864aceac7c.es.png)

Si estás satisfecho con los cambios realizados, pasa el cursor sobre la carpeta `Cambios` y haz clic en el botón `+` para preparar los cambios. Preparar simplemente significa que estás preparando tus cambios para confirmarlos en GitHub.

Si no estás cómodo con algunos cambios y deseas descartarlos, pasa el cursor sobre la carpeta `Cambios` y selecciona el ícono `deshacer`.

Luego, escribe un `mensaje de confirmación` _(Una descripción del cambio que realizaste en el proyecto)_, haz clic en el ícono de verificación para confirmar y enviar tus cambios.

Una vez que hayas terminado de trabajar en tu proyecto, selecciona el ícono del `menú hamburguesa` en la parte superior izquierda para regresar al repositorio en github.com.

![Preparar y confirmar cambios](../../../../8-code-editor/images/edit-vscode.dev.gif)

## Usando extensiones

Instalar extensiones en VSCode te permite agregar nuevas funciones y opciones de personalización al entorno de desarrollo en tu editor para mejorar tu flujo de trabajo. Estas extensiones también te ayudan a agregar soporte para múltiples lenguajes de programación y suelen ser extensiones genéricas o basadas en lenguajes.

Para explorar la lista de todas las extensiones disponibles, haz clic en el ícono _`Extensiones`_ en la barra de actividad y comienza a escribir el nombre de la extensión en el campo de texto etiquetado como _'Buscar extensiones en el Marketplace'_.  
Verás una lista de extensiones, cada una con **el nombre de la extensión, el nombre del editor, una descripción breve, el número de descargas** y **una calificación por estrellas**.

![Detalles de extensiones](../../../../translated_images/extension-details.9f8f1fd4e9eb2de5069ae413119eb8ee43172776383ebe2f7cf640e11df2e106.es.png)

También puedes ver todas las extensiones previamente instaladas expandiendo la carpeta _`Instaladas`_, extensiones populares utilizadas por la mayoría de los desarrolladores en la carpeta _`Populares`_ y extensiones recomendadas para ti, ya sea por usuarios en el mismo espacio de trabajo o basadas en tus archivos abiertos recientemente en la carpeta _`Recomendadas`_.

![Ver extensiones](../../../../translated_images/extensions.eca0e0c7f59a10b5c88be7fe24b3e32cca6b6058b35a49026c3a9d80b1813b7c.es.png)

### 1. Instalar extensiones

Para instalar una extensión, escribe el nombre de la extensión en el campo de búsqueda y haz clic en ella para ver información adicional sobre la extensión en el área de código una vez que aparezca en la barra de actividad expandida.

Puedes hacer clic en el _botón azul de instalar_ en la barra de actividad expandida para instalarla o usar el botón de instalar que aparece en el área de código una vez que seleccionas la extensión para cargar información adicional.

![Instalar extensiones](../../../../8-code-editor/images/install-extension.gif)

### 2. Personalizar extensiones

Después de instalar la extensión, es posible que necesites modificar su comportamiento y personalizarla según tus preferencias. Para hacerlo, selecciona el ícono de Extensiones, y esta vez, tu extensión aparecerá en la carpeta _Instaladas_, haz clic en el _**ícono de engranaje**_ y navega a _Configuración de extensiones_.

![Modificar configuración de extensiones](../../../../translated_images/extension-settings.21c752ae4f4cdb78a867f140ccd0680e04619d0c44bb4afb26373e54b829d934.es.png)

### 3. Administrar extensiones

Después de instalar y usar tu extensión, vscode.dev ofrece opciones para administrar tu extensión según diferentes necesidades. Por ejemplo, puedes elegir:

- **Deshabilitar:** _(Puedes deshabilitar temporalmente una extensión cuando ya no la necesites pero no quieras desinstalarla completamente)_

    Selecciona la extensión instalada en la barra de actividad expandida > haz clic en el ícono de engranaje > selecciona 'Deshabilitar' o 'Deshabilitar (Espacio de trabajo)' **O** abre la extensión en el área de código y haz clic en el botón azul Deshabilitar.

- **Desinstalar:** Selecciona la extensión instalada en la barra de actividad expandida > haz clic en el ícono de engranaje > selecciona 'Desinstalar' **O** abre la extensión en el área de código y haz clic en el botón azul Desinstalar.

---

## Tarea

[Crear un sitio web de currículum usando vscode.dev](https://github.com/microsoft/Web-Dev-For-Beginners/blob/main/8-code-editor/1-using-a-code-editor/assignment.md)

## Revisión y autoestudio

Lee más sobre [VSCode.dev](https://code.visualstudio.com/docs/editor/vscode-web?WT.mc_id=academic-0000-alfredodeza) y algunas de sus otras características.

---

**Descargo de responsabilidad**:  
Este documento ha sido traducido utilizando el servicio de traducción automática [Co-op Translator](https://github.com/Azure/co-op-translator). Si bien nos esforzamos por lograr precisión, tenga en cuenta que las traducciones automáticas pueden contener errores o imprecisiones. El documento original en su idioma nativo debe considerarse como la fuente autorizada. Para información crítica, se recomienda una traducción profesional realizada por humanos. No nos hacemos responsables de malentendidos o interpretaciones erróneas que puedan surgir del uso de esta traducción.