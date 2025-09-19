---
i18n-link: the-fastest-mouse-clicker-for-windows-source-code
permalink: /pt/O-Mais-Rapido-Mouse-Clicker-para-Windows/Codigo-Fonte/

alternates:
  es: /es/El-Clicker-de-Raton-Mas-Rapido-para-Windows/Codigo-Fuente/
  en: /The-Fastest-Mouse-Clicker-for-Windows/Source-Code/

title: "O Mais Rápido Mouse Clicker para Windows | Código Fonte"
description: "O auto-clicker mais rápido para PC com Windows. Este aplicativo foi escrito em C/C++ puro com chamadas de API Win32 descritas na documentação oficial da Microsoft"
description_rich: "O auto-clicker mais rápido para PC com Windows. Este aplicativo foi escrito em C/C++ puro com chamadas de API Win32 descritas na documentação oficial da Microsoft"
---

## {{ page.title | default: site.t['title'][page.lang] }}

### {{ page.description_rich | default: site.t['description_rich'][page.lang] }}

> {{ site.t['updated_text'][page.lang] }} : {{ site.t['updated_month'][page.lang] }} {{ site.upd_day_year }}.

O código-fonte completo com comentários é fornecido com o instalador do Windows ou pode ser assistido no
[Github](https://github.com/windows-2048/The-Fastest-Mouse-Clicker-for-Windows){:target="_blank"}
e no [Gitlab](https://gitlab.com/mashanovedad/The-Fastest-Mouse-Clicker-for-Windows){:target="_blank"}.

## The Fastest Mouse Clicker v3.0.0.0 (edição Qt multiplataforma)

**Todas as versões futuras do The Fastest Mouse Clicker para Windows serão multiplataforma e feitas em Qt.**

Primeiramente, compilei uma versão minimalista de 64 bits, estática/de tempo de execução estático, do Qt v5.15.5 (LTS), feita para Windows 7 a 11 sob o compilador MSVC 2019.

Opções de configuração:

```
C:\qt-src-5.15.5\configure -static -static-runtime -qt-zlib -qt-libjpeg -qt-libpng -qt-freetype -qt-pcre -qt-harfbuzz -no-sse4.1 -no-sse4.2 -no-avx2 -no-avx512 -no-pch -no-ssl -no-openssl -no-opengl -qpa windows -confirm-license -opensource -release -make libs -make tools -prefix c:/qt-5.15.5-static
```

Baixe [qt-5.15.5-static.zip](https://filedn.com/llBp1EbMQML0Hdv9A9SVo6b/qt-5.15.5-static.zip).

A migração para a edição Qt multiplataforma do {{ site.t['app_name'][page.lang] }} está em andamento. O novo aplicativo receberá a versão 3.0.0.0 e se chamará
"O Mouse Clicker Mais Rápido para \<OS\> (edição Qt multiplataforma)", onde \<OS\> é "Windows", "Linux", "MacOS (M1)".
A versão \*.ui do QtDesigner está pronta hoje. Convido você a conferir como o The Fastest Mouse Clicker v3.0.0.0 ficará bonito e agradável
na tela do seu PC. Suporte nativo completo para telas 4K e Retina está disponível aqui. Como sempre, o aplicativo é vinculado estaticamente e não requer DLL ou componente de sistema operacional de terceiros. Enquanto isso, na linhagem Windows, todos os sistemas, do Windows 7 ao Windows 11, são suportados.
Observe, porém, que as compilações de sistemas operacionais de 32 bits (normalmente para Windows) foram para o histórico. O novo aplicativo será apenas de 64 bits para todas as plataformas. Aguarde!

![Captura de tela do desenvolvedor do teaser para o O Mais Rápido Mouse Clicker v3.0.0.0 (edição Qt multiplataforma)](/The-Fastest-Mouse-Clicker-for-Windows/screenshots_new/v3.0.0.0/TheFastestMouseClickerQt.png)

Um grande progresso está acontecendo agora. Todos os detalhes sobre como um aplicativo multiplataforma funciona foram investigados.
A refatoração inicial do código foi realizada. A biblioteca [libuiohook](https://github.com/kwhat/libuiohook){:target="_blank"} foi projetada de forma bastante clara.

![Captura de tela do desenvolvedor do trailer para O Mais Rápido Mouse Clicker v3.0.0.0 (edição Qt multiplataforma)](/The-Fastest-Mouse-Clicker-for-Windows/screenshots_new/v3.0.0.0/TheFastestMouseClicker.png)

### Ótima atualização em 01 de março de 2023

O Fastest Mouse Clicker v3.0.0.0 (a edição Qt) usará a [biblioteca multiplataforma libuiohook](https://github.com/kwhat/libuiohook/){:target="_blank"}
para lidar com eventos de mouse e teclado em todos os monitores do sistema. Sua interface gráfica será completamente redesenhada para realizar a gravação e reprodução totalmente automáticas
de todos os eventos de mouse e teclado. Você pode até editar a sequência gravada em profundidade e modificar sua velocidade de reprodução.
Além disso, você pode randomizar cada clique do mouse ou pressionamento do teclado. Eventos de roda do mouse também serão suportados.

A ideia para a gravação é:

* Para executar a função de despacho libuiohook em uma thread Qt separada:

<pre><code title="função de despacho libuiohook em execução em um thread separado">
void dispatch_proc(uiohook_event* const event)
{
    switch (event->type)
    {
    ...
    case EVENT_MOUSE_PRESSED:
    case EVENT_MOUSE_RELEASED:
    case EVENT_MOUSE_CLICKED:
    case EVENT_MOUSE_MOVED:
    case EVENT_MOUSE_DRAGGED:
        g_tfmc->postMyCustomEvent(event->data.mouse.x, event->data.mouse.y);
        break;
    ...
    }
}

class HelloThread : public QThread
{
private:
    void run()
    {
        ...
        // Set the event callback for uiohook events.
        hook_set_dispatch_proc(&dispatch_proc);

        // Start the hook and block.
        // NOTE If EVENT_HOOK_ENABLED was delivered, the status will always succeed.
        int status = hook_run();
    }
};
</code></pre>

* Defina um evento Qt personalizado para transferir dados de eventos libuiohook entre threads Qt (worker e UI):

<pre><code title="Evento Qt personalizado para transferir dados de eventos libuiohook entre threads Qt (worker e UI)">
// Define your custom event identifier
const QEvent::Type MY_CUSTOM_EVENT = static_cast<QEvent::Type>(QEvent::User + 1);

// Define your custom event subclass
class MyCustomEvent : public QEvent
{
public:
    MyCustomEvent(const int customData1, const int customData2);
    int getCustomData1() const;
    int getCustomData2() const;
    ...
};
</code></pre>

* É útil definir postMyCustomEvent() como um método público da classe principal da interface do usuário e, em seguida, implementar seu próprio customEvent() virtual:

<pre><code title="Defina postMyCustomEvent() como um método público da classe principal da IU e, em seguida, implemente seu próprio customEvent() virtual">
class TheFastestMouseClicker : public QMainWindow
{
public:
    TheFastestMouseClicker();

    Ui_MainWindow ui;

    void postMyCustomEvent(const int customData1, const int customData2)
    {
        // This method (postMyCustomEvent) can be called from any thread
        QApplication::postEvent(this, new MyCustomEvent(customData1, customData2));
    }

protected:

    void customEvent(QEvent* event)
    {
        // When we get here, we've crossed the thread boundary and are now
        // executing in the Qt object's thread
        if (event->type() == MY_CUSTOM_EVENT)
        {
            handleMyCustomEvent(static_cast<MyCustomEvent*>(event));
        }
        // use more else ifs to handle other custom events
    }

    void handleMyCustomEvent(const MyCustomEvent* event)
    {
        // Now you can safely do something with your Qt objects.
        // Access your custom data using event->getCustomData1() etc.
        ui.leMousePosX->setText(QString("%1").arg(event->getCustomData1()));
        ui.leMousePosY->setText(QString("%1").arg(event->getCustomData2()));
    }
    ...
};
</code></pre>

A ideia para a reprodução é:

* Implementar o próprio QApplication::notify() virtualmente como uma maneira útil de manipular eventos Qt adequados em um só lugar, sem sinais e slots:

<pre><code title="Implementar o próprio QApplication::notify() virtual como uma maneira útil de manipular eventos Qt adequados em um só lugar">
class Application : public QApplication
{
public:
    ...
protected:
    bool notify(QObject* dest, QEvent* ev)
    {
        if ((g_tfmc != nullptr) && (dest == g_tfmc->ui.pbStart) && (ev->type() == QEvent::MouseButtonRelease))
        {
            // Allocate memory for the virtual events only once.
            uiohook_event*  event = (uiohook_event*)malloc(sizeof(uiohook_event));
            if (event == NULL) {
                return QApplication::notify(dest, ev);
            }

            // Playback code is here.
            for (int i = 0; i < 275; i++) {
                event->type = EVENT_MOUSE_MOVED;
                event->data.mouse.button = MOUSE_NOBUTTON;
                event->data.mouse.x = i;
                event->data.mouse.y = i;
                hook_post_event(event);
            }

            return QApplication::notify(dest, ev);
        }
        return QApplication::notify(dest, ev);
    }
    ...
};
</code></pre>

* A ideia de editar a sequência gravada é baseada na abordagem padrão [QListWidget](https://doc.qt.io/qt-5/qlistwidget.html){:target="_blank"}.

Captura de tela resultante do MS Visual Studio 2019 unindo Qt e libuiohook:

![Captura de tela resultante do MS Visual Studio 2019 unindo Qt e libuiohook](/The-Fastest-Mouse-Clicker-for-Windows/screenshots_new/v3.0.0.0/qt_libuiohook.png)


#### {{ site.t['copyright_text'][page.lang] }} [{{ site.t['author_name'][page.lang] }}]({{ site.prod-url }}{{ site.t['home'][page.lang] }})
