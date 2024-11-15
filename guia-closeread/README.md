# ℹ️ Guía Closeread

{% hint style="info" %}
Toda la información presentada en este blog ha sido extraída y adaptada de la página[ CloseRead](https://closeread.dev/). La idea de este blog es ilustrar y explicar su uso en español. Los ejemplos tienen fines ilustrativos y no reemplazan el contenido original.\
Se recomienda consultar la fuente orginal.
{% endhint %}

Antes de arrancar es importante:

* Tener instalado <mark style="color:blue;">**RStudio**</mark> (obvio)
* Instalar <mark style="color:blue;">**Quarto**</mark>: esto no es tan obvio (o por lo menos para mí), ya que es posible visualizar documentos .qmd sin tener instalado Quarto como aplicación. Para verificar si tenemos instalado Quarto, debemos revisar en nuestro directorio, en  `Archivos del programa`  si existe una carpeta Quarto. En caso de no encontrarla, significa que debemos descargarlo en esta [web](https://quarto.org/docs/download/).
* Descargar el paquete de closeread: para empezar a trabajar con los documentos Closeread, necesitamos descargar el paquete ejecutando el siguiente comando en la terminal de R o en la consola en el directorio en el que deseamos trabajar

```
quarto add qmd-lab/closeread

```

Una vez instalada la extensión, en el YAML de un documento quarto podemos utilizar el formato `closeread-html`

```yaml
---
title: My First Closeread
format: closeread-html
---
```

## <mark style="color:blue;">Componentes de un documento Closeread</mark>

Antes de crear un documento closeread es importante entender los elementos disponibles:&#x20;

* Secciones: las secciones del tipo closeread son partes del documento que se designan para mostrar el contenido interactivo. En estas secciones, los elementos destacados (imágenes o textos) se mostrarán de forma fija a medida que el lector scrollea. Estas secciones sirven para centrar la atención.
* &#x20;Sitcky: pegajoso en españo, lo que hace referencia a que es un elemento que queda fijo, pegado, mientras el lector se desplaza por la sección del tipo closeread. Puede ser una imagen, un gráfico, un texto.&#x20;
* Trigger: este elemento suele ser por lo general un párrafo o un bloque de texto, que activa (triggers) la aparición de un sticky en la sección principal. Cuando el lector llega a esta parte del contenido, el sticky aparece o bien cambia, ayudando a guiar la atención y a coordinar la narrativa del documento.

{% hint style="success" %}
_**Ejemplo: supongamos que estamos escribiendo un artículo interactivo sobre Shakira y su carrera musical.**_ \
\
La sección closeread será una sección dedicada a mostrar estadísticas: discos vendidos, premios ganados, cantidad de oyentes, etc.\
\
Tendremos un **sticky** con una estadística fija que muestra la cantidad total de ventas de discos de Shakira. Este elemento permanecerá visible en pantalla mientras el lector explora la sección.\


A medida que avanzamos en el artículo, aparecen diferentes párrafos que describen cada álbum de la carrera de Shakira. Cada uno de estos párrafos actúa como un **trigger**: al llegar a un párrafo sobre un álbum específico, el gráfico en el sticky se actualiza para mostrar las ventas específicas de ese álbum en particular.
{% endhint %}

### _<mark style="color:blue;">Secciones closeread</mark>_

Para crear una sección closeread, debemos abrir un bloque `div` y agregar la clase especil `cr-section`

```markdown
:::{.cr-section}
Dentro de esta sección habrá párrafos, imágnes, chunks de código
:::

```

La sección actúa como una "caja" especial que convierte el contenido que esté dentro en una lectura interactiva.  Todo lo que esté dentro de la caja se mostrará como parte de una historia con efectos interactivos, elementos stickys, trigger. Lo que esté por fuera aparecerá normal como en cualquier otro documento HTML.

### _<mark style="color:blue;">Stickies</mark>_

Como hemos visto, un sticky es un elemento que queda fijo a medida que scrolleamos.&#x20;

Para marcar un elemento como sticky necesitamos envolverlo en un bloque `div` y asignarle un identificador especial que comience con `cr-`.

{% hint style="success" %}
**Ejemplo: queremos dejar fija una imagen de Shakira**\
:::{#cr-myimage}  :::\
!\[] (ruta/imagen\_shakira.png)\
:::
{% endhint %}

En este ejemplo tenemos una imagen, pero podría ser texto, una fórmula, una tabla o un gráfico.

Los elementos sticky se colocan en la columa princpal de la sección de closeread y por defecto serán transparentes. Para hacer que aparezcan necesitamos un trigger que active al sticky en el momento que lo necesitamos.

### _<mark style="color:blue;">Triggers</mark>_

Cualquier elemento dentro de una sección de closeread que no sea un sticky se colocará en la columna de narrativa (por lo general suele ser texto).

Se puede configurar un párrafo para activar un stciky específico utilizando la sintaxis de referencia cruzada de Quarto: `@cr-my_sticky`

{% hint style="success" %}
**Ejemplo: queremos crear un trigger que active la imagen de shakira**
{% endhint %}

```
:::{.cr-section}
Este párrafo activará la aparición de la imagen de Shakira al desplazarse
hasta aquí. @cr-imagen_shakira
:::

:::{#cr-imagen_shakira}
![](ruta/a/tu/imagen_de_shakira.jpg)
:::
```

Arriba tenemos la referencia al sticky, una vez que el usuario haga el scroll hasta ese punto, aparecerá la imagen sticky.

Los triggers también se pueden utilizar para activar efectos de enfoque, que veremos en la próxima sección.
