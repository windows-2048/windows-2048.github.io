---
i18n-link: the-fastest-mouse-clicker-for-windows-technology
permalink: /The-Fastest-Mouse-Clicker-for-Windows/Technology/

alternates:
  es: /es/El-Clicker-de-Raton-Mas-Rapido-para-Windows/Tecnologia/
  pt: /pt/O-Mais-Rapido-Mouse-Clicker-para-Windows/Tecnologia/

title: "The Fastest Mouse Clicker for Windows | Technology"
description: "The fastest auto-clicker for Windows PC. This is the only auto-clicker utlizing arrays in SendInput system calls to reach ultimate clicking speed"
description_rich: "The fastest auto-clicker for Windows PC. This is the only auto-clicker utlizing arrays in SendInput system calls to reach ultimate clicking speed"
---

## {{ page.title | default: site.t['title'][page.lang] }}

### {{ page.description_rich | default: site.t['description_rich'][page.lang] }}

> {{ site.t['updated_text'][page.lang] }} : {{ site.t['updated_month'][page.lang] }} {{ site.upd_day_year }}.

Unlike other auto-clickers that use obsolete <code><a href="https://docs.microsoft.com/en-us/windows/win32/api/winuser/nf-winuser-mouse_event" target="_blank">mouse_event()</a></code>
system call from C/C++ source or un-arrayed <code><a href="https://docs.microsoft.com/en-us/windows/win32/api/winuser/nf-winuser-sendinput" target="_blank">SendInput()</a></code> from C#/.Net source, The Fastest Mouse Clicker for Windows uses
<i>arrayed</i> <code><a href="https://docs.microsoft.com/en-us/windows/win32/api/winuser/nf-winuser-sendinput" target="_blank">SendInput()</a></code> with specially prepared <i>arrays</i> of mouse events:

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

The size of the <i>arrays</i> is carefully computed based on the click rate given by end-user. To avoid system event buffer
overflow, the time in <code><a href="https://docs.microsoft.com/en-us/windows/win32/api/synchapi/nf-synchapi-sleep" target="_blank">Sleep()</a></code> is selected properly according the size of the <i>array</i>.

The GUI of the application seems archaic, but it is made by very base Win32 system calls
to avoid performance degradation caused by
high-level third-side libraries such as [Qt](https://www.qt.io/){:target="_blank"} or slow managed code in frameworks like C#/.Net.
For example, <code><a href="https://docs.microsoft.com/en-us/windows/win32/api/winuser/nf-winuser-getasynckeystate" target="_blank">GetAsyncKeyState()</a></code> is used to detect the trigger keys pressed by end-user:

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

Another benefit of such an approach is compact, statically-linked executable without any external dependencies.

When end-user selects low click rates, actual size of the <i>array</i> of mouse events in <code><a href="https://docs.microsoft.com/en-us/windows/win32/api/winuser/nf-winuser-sendinput" target="_blank">SendInput()</a></code>
is set to 1 and number of clicks per second is regulated by <code><a href="https://docs.microsoft.com/en-us/windows/win32/api/synchapi/nf-synchapi-sleep" target="_blank">Sleep()</a></code> only.
But when end-user selects high click rates, the size of the <i>array</i> becomes significant. In rare circumstances, it may lead to freeze the whole Windows GUI.
To avoid that, the helper thread is created to scan <code><a href="https://docs.microsoft.com/en-us/windows/win32/api/winuser/nf-winuser-getasynckeystate" target="_blank">GetAsyncKeyState()</a></code> independently in order end-user has requested to stop the clicking
and force <code><a href="https://docs.microsoft.com/en-us/windows/win32/api/winuser/nf-winuser-blockinput" target="_blank">BlockInput()</a></code> because mouse event buffer may be full:

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

To be more compatible with older versions of Windows, {{ site.t['app_name'][page.lang] }} utilizes base Win32 API for widget creation.
It uses traditional Windows approach to re-draw all the widgets in a Windows event loop.
To update the view of a particular widget, an event is being sent to that widget in the main thread and
incoming call is being passed to event loop handler where actual re-draw occurs.

First, we declare a <code><a href="https://docs.microsoft.com/en-us/previous-versions/windows/desktop/legacy/ms633573(v=vs.85)" target="_blank">WindowProc()</a></code> callback function.
Second, we register a main window class with that callback by <code><a href="https://learn.microsoft.com/en-us/windows/win32/api/winuser/nf-winuser-registerclassa" target="_blank">RegisterClassA()</a></code>.
And finally we enter an infinite loop inside event callback function.

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

From the other hand, to be more compatible with latest versions of Windows and newest hardware such as professional
<a href="https://www.pcmag.com/picks/the-best-4k-monitors" target="_blank">4K displays</a>
and gaming monitors,
font size adjusting is performed on application start utilizing both variable font size and embedded
<a href="https://docs.microsoft.com/en-us/windows/win32/hidpi/setting-the-default-dpi-awareness-for-a-process" target="_blank">high DPI</a> xml manifest.

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

The application embedded xml manifest contains a section with high DPI awareness.

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

There are much more programmatic tricks I used to achieve outstanding performance, compatibility and look-n-feel.
If you want to discover them, you have to study source code yourself.


#### {{ site.t['copyright_text'][page.lang] }} [{{ site.t['author_name'][page.lang] }}]({{ site.prod-url }}{{ site.t['home'][page.lang] }})
