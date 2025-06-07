---
i18n-link: the-fastest-mouse-clicker-for-windows-technology
permalink: /pt/O-Mais-Rapido-Mouse-Clicker-para-Windows/Tecnologia/

alternates:
  es: /es/El-Clicker-de-Raton-Mas-Rapido-para-Windows/Tecnologia/
  en: /The-Fastest-Mouse-Clicker-for-Windows/Technology/

title: "O Mais Rápido Mouse Clicker para Windows | Tecnologia"
description: "O auto-clicker mais rápido para PC com Windows. Este é o único auto-clicker que utiliza matrizes em chamadas de sistema SendInput para atingir a velocidade máxima de clique"
description_rich: "O auto-clicker mais rápido para PC com Windows. Este é o único auto-clicker que utiliza matrizes em chamadas de sistema SendInput para atingir a velocidade máxima de clique"
---

## {{ page.title | default: site.t['title'][page.lang] }}

### {{ page.description_rich | default: site.t['description_rich'][page.lang] }}

> {{ site.t['updated_text'][page.lang] }} : {{ site.t['updated_month'][page.lang] }} {{ site.upd_day_year }}.

Ao contrário de outros clicadores automáticos que usam a chamada de sistema obsoleta <code><a href="https://docs.microsoft.com/en-us/windows/win32/api/winuser/nf-winuser-mouse_event" target="_blank">mouse_event()</a></code>
de código fonte C/C++ ou <code><a href="https://docs.microsoft.com/en-us/windows/win32/api/winuser/nf-winuser-sendinput" target="_blank">SendInput()</a></code> não-array de código fonte C#/.Net, o Clicker de Mouse Mais Rápido para Windows usa
<i>array</i> <code><a href="https://docs.microsoft.com/en-us/windows/win32/api/winuser/nf-winuser-sendinput" target="_blank">SendInput()</a></code> com <i>matrizes</i> de eventos do mouse:

<pre><code title="Exemplo de SendInput() em matriz">
UINT nCntExtra = (nCnt - 1) * 2; // índice reservado para BAIXO, CIMA

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

O tamanho dos <i>arrays</i> é cuidadosamente calculado com base na taxa de cliques fornecida pelo usuário final. Para evitar estouro do buffer de eventos do sistema,
o tempo em <code><a href="https://docs.microsoft.com/en-us/windows/win32/api/synchapi/nf-synchapi-sleep" target="_blank">Sleep()</a></code> é selecionado corretamente de acordo com o tamanho do <i>array</i>.

A interface gráfica do usuário (GUI) do aplicativo parece arcaica, mas é feita por chamadas de sistema Win32 muito básicas
para evitar degradação de desempenho causada por
bibliotecas de terceiros de alto nível, como [Qt](https://www.qt.io/){:target="_blank"} ou código gerenciado lento em frameworks como C#/.Net.

Por exemplo, <code><a href="https://docs.microsoft.com/en-us/windows/win32/api/winuser/nf-winuser-getasynckeystate" target="_blank">GetAsyncKeyState()</a></code> é usado para detectar as teclas de gatilho pressionadas pelo usuário final:

<pre><code title="Exemplo base de GetAsyncKeyState()">
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

Outro benefício dessa abordagem é um executável compacto, estaticamente vinculado e sem dependências externas.

Quando o usuário final seleciona baixas taxas de cliques, o tamanho real da <i>matriz</i> de eventos do mouse em <code><a href="https://docs.microsoft.com/en-us/windows/win32/api/winuser/nf-winuser-sendinput" target="_blank">SendInput()</a></code>
é definido como 1 e o número de cliques por segundo é regulado apenas por <code><a href="https://docs.microsoft.com/en-us/windows/win32/api/synchapi/nf-synchapi-sleep" target="_blank">Sleep()</a></code>.
Mas quando o usuário final seleciona altas taxas de cliques, o tamanho da <i>matriz</i> se torna significativo. Em raras circunstâncias, isso pode levar ao congelamento de toda a interface gráfica do usuário (GUI) do Windows.
Para evitar isso, a thread auxiliar é criada para escanear <code><a href="https://docs.microsoft.com/en-us/windows/win32/api/winuser/nf-winuser-getasynckeystate" target="_blank">GetAsyncKeyState()</a></code> independentemente, para que o usuário final solicite a interrupção do clique
e forçar <code><a href="https://docs.microsoft.com/en-us/windows/win32/api/winuser/nf-winuser-blockinput" target="_blank">BlockInput()</a></code>, pois o buffer de eventos do mouse pode estar cheio:

<pre><code title="Helper thread com exemplo de BlockInput()">
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

Para ser mais compatível com versões mais antigas do Windows, {{ site.t['app_name'][page.lang] }} utiliza a API base do Win32 para a criação de widgets.
Ele usa a abordagem tradicional do Windows para redesenhar todos os widgets em um loop de eventos do Windows.
Para atualizar a visualização de um widget específico, um evento é enviado para esse widget na thread principal e
a chamada de entrada é passada para o manipulador do loop de eventos, onde o redesenho real ocorre.

Primeiro, declaramos uma função de retorno de chamada <code><a href="https://docs.microsoft.com/en-us/previous-versions/windows/desktop/legacy/ms633573(v=vs.85)" target="_blank">WindowProc()</a></code>.
Em segundo lugar, registramos uma classe de janela principal com esse retorno de chamada por <code><a href="https://learn.microsoft.com/en-us/windows/win32/api/winuser/nf-winuser-registerclassa" target="_blank">RegisterClassA()</a></code>.
E, finalmente, entramos em um loop infinito dentro da função de retorno de chamada de evento.

<pre><code title="Loop de eventos do Windows para redesenhar os widgets">
LRESULT CALLBACK winCallBack(
HWND hWin
, UINT msg
, WPARAM wp
, LPARAM lp
);

...

// Inicializando a classe de janela
windClass.style = CS_HREDRAW | CS_VREDRAW;
windClass.lpfnWndProc = winCallBack;
windClass.cbClsExtra = 0;
windClass.cbWndExtra = 0;
windClass.hInstance = instanceH;
windClass.hIcon = LoadIcon(
windClass.hInstance
, MAKEINTRESOURCE(101)
);
windClass.hCursor = LoadCursor(
NULL
, IDC_ARROW
);
windClass.hbrBackground = (HBRUSH)GetStockObject(
WHITE_BRUSH
);
windClass.lpszClassName = "O mouse mais rápido para Windows"

//Registrando a classe de janela
RegisterClass(&windClass);

...

RETORNO DE CHAMADA LRESULT winCallBack(
HWND hWin
, UINT msg
, WPARAM wp
, LPARAM lp
)
{
HDC dc;
PAINTSTRUCT ps;
int status_local = 0;
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

Por outro lado, para maior compatibilidade com as versões mais recentes do Windows e hardwares mais recentes, como monitores profissionais
<a href="https://www.pcmag.com/picks/the-best-4k-monitors" target="_blank">4K</a>
e monitores gamer,
o ajuste do tamanho da fonte é realizado na inicialização do aplicativo, utilizando tamanho de fonte variável e manifesto XML incorporado
<a href="https://docs.microsoft.com/en-us/windows/win32/hidpi/setting-the-default-dpi-awareness-for-a-process" target="_blank">high DPI</a>.

<pre><code title="Suporte para monitores 4K em código C++">
struct _Sc
{
int factor;
_Sc() : fator(1)
{
int h, v;
ObterResoluçãoDeDesktop(h, v);
if (v > 1440)
fator = 2;
}
} _sc;

int Sc(int x)
{
return x * _sc.fator;
}

...

statusText = CreateWindow(
"Estático"
, "status do clique: inativo"
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

O manifesto XML incorporado do aplicativo contém uma seção com alta percepção de DPI.

<pre><code title="Suporte para monitores 4K no manifesto XML">
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

Há muitos outros truques programáticos que usei para obter desempenho, compatibilidade e aparência excelentes.
Se você quiser descobri-los, terá que estudar o código-fonte por si mesmo.


#### {{ site.t['copyright_text'][page.lang] }} [{{ site.t['author_name'][page.lang] }}]({{ site.prod-url }}{{ site.t['home'][page.lang] }})
