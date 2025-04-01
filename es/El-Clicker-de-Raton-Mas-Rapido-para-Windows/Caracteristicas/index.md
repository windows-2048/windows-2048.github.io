---
i18n-link: the-fastest-mouse-clicker-for-windows-features
permalink: /es/El-Clicker-de-Raton-Mas-Rapido-para-Windows/Caracteristicas/

alternates:
  en: /The-Fastest-Mouse-Clicker-for-Windows/Features/
  pt: /pt/O-Mais-Rapido-Mouse-Clicker-para-Windows/Caracteristicos/

title: El Clicker de Ratón Más Rápido para Windows | Características
description: El autoclic más rápido para PC con Windows. 100000 clics por segundo. Lista completa de funciones del programa
description_rich: El autoclic más rápido para PC con Windows. 100000 clics por segundo. Lista completa de funciones del programa
---

## {{ page.title | default: site.t['title'][page.lang] }}

### {{ page.description_rich | default: site.t['description_rich'][page.lang] }}

> {{ site.t['updated_text'][page.lang] }} : {{ site.t['updated_month'][page.lang] }} {{ site.upd_day_year }}.

Esta no es una lista completa de todas las funciones del programa. Solo he seleccionado algunas de las más importantes desde el punto de vista de nuestros usuarios.
Dado que el texto de ayuda aún no está completo
y no refleja todas las funciones implementadas, no dude en crear
un [issue]({{ site.source_issues_url }}){:target="_blank"} para solicitar la función que desee.

* La mejor tasa de clics del mundo: hasta 100 000 clics por segundo, 10 veces superior a la de su predecesora, "Fast Mouse Clicker". ¡La última versión, con un problema de rendimiento corregido, es 100 veces más rápida!

* Utiliza la función de matriz por lotes de <code><a href="https://docs.microsoft.com/en-us/windows/win32/api/winuser/nf-winuser-sendinput" target="_blank">SendInput()</a></code> y manipula con <code><a href="https://docs.microsoft.com/en-us/windows/win32/api/syncchapi/nf-syncchapi-sleep" target="_blank">Sleep()</a></code> para alcanzar el máximo rendimiento posible de los clics del mouse en Windows.

* Se admiten los botones izquierdo, central y derecho del mouse, y se pueden activar para hacer clic con una tecla del teclado en modo de presión o alternancia.

* Se puede seleccionar cualquier tecla del teclado para activar el clic. Además, otro botón del ratón puede actuar como tecla de activación.

* Diferentes teclas de activación independientes para iniciar/finalizar el clic en el modo de alternancia.

* El programa funciona correctamente incluso minimizado y opera en cualquier área del escritorio. Puede dejar de hacer clic automáticamente si el usuario final establece un número determinado de clics.

* Esta es una aplicación gratuita, de código abierto, sin anuncios, virus, troyanos, malware, etc. para siempre.

* El programa cuenta con un servicio de actualización integrado en desarrollo que puede realizar tareas científicas adicionales cuando la CPU está inactiva con un uso mínimo de la misma y de Internet. Consulte el código fuente del instalador. La aplicación se desinstala fácilmente y NO es un virus ni malware. Puede cambiar a los instaladores sin servicio de actualización y volver a [en cualquier momento](https://github.com/windows-2048/The-Fastest-Mouse-Clicker-for-Windows/blob/master/InnoSetupDownloader/README.md){:target="_blank"}.

* La aplicación se puede utilizar en un sistema básico, no depende de .NET Framework ni de ninguna otra biblioteca externa como "Speed ​​AutoClicker", "Fast Clicker", etc.

* Se ha admitido la línea de comandos: TheFastestMouseClicker.exe -c <clics por segundo> -t <tecla de activación> -s <detenerse en> -m <modo de la tecla de activación> -b <botón del ratón para hacer clic>, donde <modo de la tecla de activación> puede ser 'pulsar' o 'alternar' y <botón del ratón para hacer clic> puede ser 'izquierdo', 'central' o 'derecho'. Se puede especificar cualquier parte de los argumentos; los valores no especificados o no reconocidos se considerarán predeterminados (para consultarlos, ejecute la aplicación y pulse el botón "Restablecer valores predeterminados").

* Se ha añadido el botón "Carpeta por lotes" para abrir rápidamente un directorio con archivos \*.bat; simplifica mucho el uso de la línea de comandos.

* Se admiten valores fraccionarios para el parámetro de clics/s. Por ejemplo, 0,5 clics/s equivalen a 1 clic cada 2 segundos.

* Se han implementado los clics aleatorios. Simplemente haga clic en el botón "Carpeta de lotes" y consulte las observaciones en los archivos \*.bat que se encuentran allí para saber cómo usar los argumentos de la línea de comandos y habilitar los clics aleatorios.

* La función de clics grupales (grabar/reproducir secuencias de clics) es compatible con aplicaciones adicionales desde la versión v.2.5.3.2. Puede cambiar rápidamente entre aplicaciones haciendo clic en el botón "Ejecutar aplicación grupal" o "Ejecutar aplicación individual".

* Casilla de verificación Ventana siempre arriba para mantener la ventana de la aplicación en la parte superior.

* Edición manual de opciones/configuraciones como beneficio adicional al guardado automático: simplemente abra C: \ Users \ \<YourWindowsUser \> \ AppData \ Roaming \ TheFastestMouseClicker \ TheFastestMouseClicker \ settings.dat
en cualquier editor de texto simple (puede cambiar la subruta TheFastestMouseClicker durante la instalación).


#### {{ site.t['copyright_text'][page.lang] }} [{{ site.t['author_name'][page.lang] }}]({{ site.prod-url }}{{ site.t['home'][page.lang] }})
