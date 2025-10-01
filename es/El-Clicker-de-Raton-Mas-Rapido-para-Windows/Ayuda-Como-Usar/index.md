---
i18n-link: the-fastest-mouse-clicker-for-windows-help-how-to-use
permalink: /es/El-Clicker-de-Raton-Mas-Rapido-para-Windows/Ayuda-Como-Usar/

alternates:
  en: /The-Fastest-Mouse-Clicker-for-Windows/Help-How-To-Use/
  pt: /pt/O-Mais-Rapido-Mouse-Clicker-para-Windows/Ajuda-Como-Usar/

title: "El Clicker de Ratón Más Rápido para Windows | Ayuda Cómo Usar"
description: "El autoclic más rápido para PC con Windows. Una guía detallada sobre cómo utilizar la aplicación en sus actividades diarias con la mayor eficiencia"
description_rich: "El autoclic más rápido para PC con Windows. Una guía detallada sobre cómo utilizar la aplicación en sus actividades diarias con la mayor eficiencia"
---

## {{ page.title | default: site.t['title'][page.lang] }}

### {{ page.description_rich | default: site.t['description_rich'][page.lang] }}

> {{ site.t['updated_text'][page.lang] }} : {{ site.t['updated_month'][page.lang] }} {{ site.upd_day_year }}.

PUEDE INICIAR EL CLIC AUTOMÁTICO EN CUALQUIER MOMENTO PRESIONANDO LA <tecla de activación> (13 = Intro). Leer la Ayuda completa es opcional.

CAMPOS QUE NO SE PUEDEN MODIFICAR.

&lt;clicking status&gt; o &lt;random clicking status&gt;, el campo de texto superior, se muestra como "inactivo" o "haciendo clic".
Se muestra como &lt;estado de clic aleatorio&gt; solo cuando todos los tamaños de rectángulo para hacer clic aleatorio dentro de él se especifican correctamente en la línea de comandos.
Simplemente presione el botón \[Batch folder\] y vea las observaciones en el archivo run_clicker_with_random_clicking.bat.

&lt;number of clicks&gt;, el campo de texto superior, indica el número total de clics realizados.

CAMPOS QUE PUEDE MODIFICAR (PARÁMETROS DE CLIC: TAMBIÉN SE PUEDEN CONFIGURAR DESDE LA LÍNEA DE COMANDOS, VER A CONTINUACIÓN).

&lt;clicks per second&gt;, el campo de texto central, indica la frecuencia de los clics, medida en clics por segundo.
Esta frecuencia puede alcanzar cien mil (100000) clics por segundo.
Se admiten frecuencias FRACCIONALES. Por ejemplo, 0,5 corresponde a 1 clic cada 2 segundos, 0,25 a 1 clic cada 4 segundos, etc.

&lt;begin/end trigger keys&gt;, debajo, se encuentran las teclas del teclado que activan los eventos del ratón. Simplemente haga clic en ellas y presione una tecla arbitraria (o presione un botón del ratón).
Esa tecla activará los clics del ratón cuando permanezca presionada. Si simplemente presiona y suelta la tecla, solo se deberían realizar unos pocos clics.
Este comportamiento corresponde al &lt;modo de tecla de activación&gt;. = 'presionar', vea cómo cambia el valor de 'alternar' a continuación.
El número predeterminado que se muestra en el botón, 13, corresponde al código de la tecla 'Intro' (por ejemplo, 32 corresponde a la tecla 'Espacio', 112 a la tecla 'F1', etc.).
Para consultar todos los códigos de tecla, consulte la [documentación de Windows](https://docs.microsoft.com/en-us/windows/win32/inputdev/virtual-key-codes){:target="_blank"}.

El campo de texto inferior, &lt;stop at&gt;, indica el número de clics antes de que el clic se detenga automáticamente.
0 es el valor predeterminado y significa infinito, es decir, el clic nunca se detendrá.

&lt;trigger key mode&gt; es un grupo de botones de opción; puede seleccionar el modo de clic "press" o "toggle".
En el modo "press" (predeterminado), los eventos del ratón se emiten solo cuando se mantiene pulsada la tecla de activación correspondiente.
En el modo "toogle", los eventos del ratón se emiten entre pulsaciones cortas posteriores de la &lt;begin trigger key&gt; y la &lt;end trigger key&gt;.

&lt;mouse button to click&gt; es un grupo de botones de opción; puede seleccionar el botón 'left', 'middle' o 'right' del ratón para generar los clics.

Nota 1: No se puede usar el mismo botón del ratón como disparador y clicker.
<br/>Nota 2: No se puede cambiar la tecla de activación si se selecciona el &lt;trigger key&gt; debe presionar el botón \[Reset to defaults\].
<br/>Nota 3: &lt;trigger key&gt; sigue funcionando al minimizar el programa. Debe cerrar el programa para que la &lt;trigger key&gt; deje de hacer clic.

*NUEVO* Todos los parámetros de clic se guardan automáticamente entre cada ejecución de la aplicación.

BOTONES Y FUNCIONES ADICIONALES.

El botón \[STOP!\] detiene la pulsación obligatoria de alternancia.
<br/>El botón \[Help\] muestra esta ventana de ayuda.
<br/>*NUEVO* El botón \[Reset to defaults\] restablece todos los parámetros de pulsación a sus valores predeterminados.
<br/>*NUEVO* El botón \[Batch folder\] abre la carpeta del Explorador de archivos donde suelen residir todos los archivos por lotes.
<br/>*NUEVO* Para obtener ayuda sobre los argumentos de la línea de comandos, simplemente presione el botón \[Batch folder\] y consulte las observaciones en los archivos \*.bat que encontrará allí.
<br/>*NUEVO* Teclas independientes para &lt;trigger key mode&gt; = 'toggle': si &lt;begin trigger key&gt; inicia la pulsación, &lt;end trigger key&gt; la detiene.
<br/>*NUEVO* &lt;Window Always Top&gt; Casilla de verificación: si está marcada, mantiene la ventana principal de la aplicación en la parte superior.
<br/>*NUEVO* Botón "Run group app": graba/reproduce las secuencias de clics del mouse.

#### {{ site.t['copyright_text'][page.lang] }} [{{ site.t['author_name'][page.lang] }}]({{ site.prod-url }}{{ site.t['home'][page.lang] }})
