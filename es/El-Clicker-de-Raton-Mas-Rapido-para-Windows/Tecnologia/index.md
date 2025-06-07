---
i18n-link: the-fastest-mouse-clicker-for-windows-technology
permalink: /es/El-Clicker-de-Raton-Mas-Rapido-para-Windows/Tecnologia/

alternates:
  en: /The-Fastest-Mouse-Clicker-for-Windows/Technology/
  pt: /pt/O-Mais-Rapido-Mouse-Clicker-para-Windows/Tecnologia/

title: "El Clicker de Ratón Más Rápido para Windows | Tecnología"
description: "El autoclic más rápido para PC con Windows. Este es el único clicker automático que utiliza matrices en las llamadas del sistema SendInput para alcanzar la máxima velocidad de clic"
description_rich: "El autoclic más rápido para PC con Windows. Este es el único clicker automático que utiliza matrices en las llamadas del sistema SendInput para alcanzar la máxima velocidad de clic"
---

## {{ page.title | default: site.t['title'][page.lang] }}

### {{ page.description_rich | default: site.t['description_rich'][page.lang] }}

> {{ site.t['updated_text'][page.lang] }} : {{ site.t['updated_month'][page.lang] }} {{ site.upd_day_year }}.

A diferencia de otros clickers automáticos que usan obsoletos <code><a href="https://learn.microsoft.com/es-es/windows/win32/api/winuser/nf-winuser-mouse_event" target="_blank">mouse_event()</a></code>
llamada del sistema desde la fuente C/C++ o <code><a href="https://learn.microsoft.com/es-es/windows/win32/api/winuser/nf-winuser-sendinput" target=" _blank">SendInput()</a></code> de fuente C#/.Net, {{ site.t['app_name'][page.lang] }} utiliza
<i>arreglo</i> <code><a href="https://learn.microsoft.com/es-es/windows/win32/api/winuser/nf-winuser-sendinput" target="_blank">SendInput()</a></code> con <i>matrices</i> especialmente preparadas de eventos del ratón:

<pre><code title="Arrayed SendInput() example">
UINT nCntExtra = (nCnt - 1) * 2; // reserved index for DOWN, UP

for (UINT iExtra = 0; iExtra < nCntExtra; iExtra += 2)
{
    input[1 + iExtra].type = INPUT_MOUSE;

    input[1 + iExtra].mi.dx = dx;
    input[1 + iExtra].mi.dy = dy;

    input[1 + iExtra].mi.mouseData = dwData;
    input[1 + iExtra].mi.time = 0;
    input[1 + iExtra].mi.dwExtraInfo = dwExtraInfo;

    ...
}

...

UINT ret = SendInput(1 + nCntExtra, input, sizeof(INPUT));
</code></pre>

El tamaño de las <i>matrices</i> se calcula cuidadosamente en función de la tasa de clics proporcionada por el usuario final. Para evitar el búfer de eventos del sistema
overflow, el tiempo en <code><a href="https://learn.microsoft.com/es-es/windows/win32/api/synchapi/nf-synchapi-sleep" target="_blank">Sleep()</a></code> se selecciona correctamente según el tamaño de la <i>matriz</i>.

La GUI de la aplicación parece arcaica, pero está hecha con llamadas al sistema Win32 muy básicas.
para evitar la degradación del rendimiento causada por
bibliotecas de terceros de alto nivel como [Qt](https://www.qt.io/){:target="_blank"} o código administrado lento en marcos como C#/.Net.
Por ejemplo, <code><a href="https://learn.microsoft.com/es-es/windows/win32/api/winuser/nf-winuser-getasynckeystate" target="_blank">GetAsyncKeyState()</a></code> se utiliza para detectar las teclas de activación presionadas por el usuario final:

<pre><code title="Base GetAsyncKeyState() example">
if (!doToggle)
{
    if (toggleState == 0 && GetAsyncKeyState(atoi(triggerText)))
        toggleState = 1;
    ...
}
else
{
    if (toggleState == 0 && GetAsyncKeyState(atoi(triggerText)))
        toggleState = 1;
    ...
}
</code></pre>

Otro beneficio de este enfoque es un ejecutable compacto y vinculado estáticamente sin dependencias externas.

Cuando el usuario final selecciona tasas de clic bajas, el tamaño real de la <i>matriz</i> de eventos del mouse en <code><a href="https://learn.microsoft.com/es-es/windows/win32/api/winuser/nf-winuser-sendinput" target="_blank">SendInput()</a></code>
está configurado en 1 y la cantidad de clics por segundo está regulada por el objetivo <code><a href="https://learn.microsoft.com/es-es/windows/win32/api/synchapi/nf-synchapi-sleep" target="_blank">Sleep()</a></code> solamente.
Pero cuando el usuario final selecciona altas tasas de clics, el tamaño de la <i>matriz</i> se vuelve significativo. En circunstancias excepcionales, puede provocar la congelación de toda la GUI de Windows.
Para evitarlo, se crea el subproceso auxiliar para escanear <code><a href="https://learn.microsoft.com/es-es/windows/win32/api/winuser/nf-winuser-getasynckeystate" target="_blank">GetAsyncKeyState()</a></code> de forma independiente para que el usuario final haya solicitado detener el clic
y fuerza <code><a href="https://learn.microsoft.com/es-es/windows/win32/api/winuser/nf-winuser-blockinput" target="_blank">BlockInput()</a></code> porque el búfer de eventos del mouse puede estar lleno:

<pre><code title="Helper thread with BlockInput() example">
DWORD WINAPI MyThreadFunction(LPVOID lpParam)
{
    while (true)
    {
        if (GetAsyncKeyState(atoi(triggerText2)))
        {
            ...
            BlockInput(TRUE);
            Sleep(100);
            BlockInput(FALSE);
            ...
            SetMsgStatus(hWnd, GetDlgCtrlID(statusText)
                , "idle");
        }

        Sleep(10);
    }

    return 0;
}
</code></pre>

Para ser más compatible con las versiones anteriores de Windows, {{ site.t['app_name'][page.lang] }} utiliza la API básica de Win32 para la creación de widgets.
Utiliza el enfoque tradicional de Windows para volver a dibujar todos los widgets en un bucle de eventos de Windows.
Para actualizar la vista de un widget en particular, se envía un evento a ese widget en el hilo principal y
la llamada entrante se pasa al controlador de bucle de eventos donde se produce el redibujado real.

Primero, declaramos un <code><a href="https://learn.microsoft.com/es-es/windows/win32/api/winuser/nc-winuser-wndproc" target="_blank ">WindowProc()</a></code> función de devolución de llamada.
En segundo lugar, registramos una clase de ventana principal con esa devolución de llamada mediante <code><a href="https://learn.microsoft.com/es-es/windows/win32/api/winuser/nf-winuser-registerclassa" target= "_blank">RegisterClassA</a></code>.
Y finalmente ingresamos un bucle infinito dentro de la función de devolución de llamada del evento.

<pre><code title="Windows event loop to re-draw the widgets">
LRESULT CALLBACK winCallBack(
    HWND hWin
    , UINT msg
    , WPARAM wp
    , LPARAM lp
    );

...

// Initializing the window class
windClass.style         = CS_HREDRAW | CS_VREDRAW;
windClass.lpfnWndProc       = winCallBack;
windClass.cbClsExtra        = 0;
windClass.cbWndExtra        = 0;
windClass.hInstance     = instanceH;
windClass.hIcon         = LoadIcon(
                            windClass.hInstance
                            , MAKEINTRESOURCE(101)
                            );
windClass.hCursor           = LoadCursor(
                            NULL
                            , IDC_ARROW
                            );
windClass.hbrBackground = (HBRUSH)GetStockObject(
                            WHITE_BRUSH
                            );
windClass.lpszClassName = "The Fastest Mouse Clicker "
                            "for Windows";

//Registering the window class
RegisterClass(&windClass);

...

LRESULT CALLBACK winCallBack(
    HWND hWin
    , UINT msg
    , WPARAM wp
    , LPARAM lp
    )
{
    HDC dc;
    PAINTSTRUCT ps;
    int local_status = 0;
    switch (msg)
    {
    case WM_COMMAND:
        switch(LOWORD(wp))
        {
        case RESET_BTN:

        ...
    ...
}
</code></pre>

Por otro lado, para ser más compatible con las últimas versiones de Windows y el hardware más nuevo, como el profesional
<a href="https://www.pcmag.com/picks/the-best-4k-monitors" target="_blank">pantallas 4K</a>
y monitores de juegos,
El ajuste del tamaño de fuente se realiza al iniciar la aplicación utilizando tanto el tamaño de fuente variable como el incrustado.
<a href="https://learn.microsoft.com/es-es/windows/win32/hidpi/setting-the-default-dpi-awareness-for-a-process" target="_blank">alta DPI</a> manifiesto xml.

<pre><code title="Support for 4K displays in C++ code">
struct _Sc
{
    int factor;
    _Sc() : factor(1)
    {
        int h, v;
        GetDesktopResolution(h, v);
        if (v > 1440)
            factor = 2;
    }
} _sc;

int Sc(int x)
{
    return x * _sc.factor;
}

...

statusText = CreateWindow(
    "Static"
    , "clicking status: idle"
    , WS_VISIBLE | WS_CHILD
    , Sc(5)
    , Sc(1)
    , Sc(410)
    , Sc(35)
    , hWnd
    , 0
    , 0
    , 0
    );
</code></pre>

El manifiesto xml incrustado de la aplicación contiene una sección con alto reconocimiento de DPI.

<pre><code title="Support for 4K displays in xml manifest">
  ...

&lt;asmv3:application&gt;
  &lt;asmv3:windowsSettings&gt;
    &lt;dpiAware xmlns="http://schemas.microsoft.com/SMI/2005/WindowsSettings"&gt;
        true
    &lt;/dpiAware&gt;
    &lt;dpiAwareness xmlns="http://schemas.microsoft.com/SMI/2016/WindowsSettings"&gt;
        system
    &lt;/dpiAwareness&gt;
  &lt;/asmv3:windowsSettings&gt;
&lt;/asmv3:application&gt;

  ...
</code></pre>

Hay muchos más trucos programáticos que utilicé para lograr un rendimiento, una compatibilidad y una apariencia sobresalientes.
Si quieres descubrirlos, tienes que estudiar el código fuente tú mismo.


#### {{ site.t['copyright_text'][page.lang] }} [{{ site.t['author_name'][page.lang] }}]({{ site.prod-url }}{{ site.t['home'][page.lang] }})
