---
i18n-link: the-fastest-mouse-clicker-for-windows-source-code
permalink: /es/El-Clicker-de-Raton-Mas-Rapido-para-Windows/Codigo-Fuente/

alternates:
  en: /The-Fastest-Mouse-Clicker-for-Windows/Source-Code/
  pt: /pt/O-Mais-Rapido-Mouse-Clicker-para-Windows/Codigo-Fonte/

title: "El Clicker de Ratón Más Rápido para Windows | Código Fuente"
description: "El autoclicker más rápido para PC con Windows. Esta aplicación está escrita en C/C++ estándar, con llamadas a la API Win32 descritas en la documentación oficial de Microsoft"
description_rich: "El autoclicker más rápido para PC con Windows. Esta aplicación está escrita en C/C++ estándar, con llamadas a la API Win32 descritas en la documentación oficial de Microsoft"
---

## {{ page.title | default: site.t['title'][page.lang] }}

### {{ page.description_rich | default: site.t['description_rich'][page.lang] }}

> {{ site.t['updated_text'][page.lang] }} : {{ site.t['updated_month'][page.lang] }} {{ site.upd_day_year }}.

El código fuente completo con comentarios puede consultarse
en [Github](https://github.com/windows-2048/The-Fastest-Mouse-Clicker-for-Windows){:target="_blank"}
y [Gitlab](https://gitlab.com/mashanovedad/The-Fastest-Mouse-Clicker-for-Windows){:target="_blank"}.

## The Fastest Mouse Clicker v3.0.0.0 (edición multiplataforma Qt)

**Todas las futuras versiones de The Fastest Mouse Clicker para Windows serán multiplataforma y estarán desarrolladas con Qt.**

Primero, he compilado una compilación minimalista de 64 bits, estática/en tiempo de ejecución estático de Qt v5.15.5 (LTS), diseñada para Windows 7 a 11 con el compilador MSVC 2019.

Opciones de configuración:

```
C:\qt-src-5.15.5\configure -static -static-runtime -qt-zlib -qt-libjpeg -qt-libpng -qt-freetype -qt-pcre -qt-harfbuzz -no-sse4.1 -no-sse4.2 -no-avx2 -no-avx512 -no-pch -no-ssl -no-openssl -no-opengl -qpa windows -confirm-license -opensource -release -make libs -make tools -prefix c:/qt-5.15.5-static
```
Descarga [qt-5.15.5-static.zip](https://filedn.com/llBp1EbMQML0Hdv9A9SVo6b/qt-5.15.5-static.zip).

La migración a la edición multiplataforma Qt de {{ site.t['app_name'][page.lang] }} está en progreso. La nueva aplicación recibirá la versión 3.0.0.0 y se llamará "El Clicker de Ratón Más Rápido para \<OS\> (edición multiplataforma Qt)", donde \<OS\> es "Windows", "Linux" y "MacOS (M1)".
El maquillaje de QtDesigner \*.ui ya está disponible. Te invito a que veas lo agradable y hermoso que se verá el Clicker de Ratón Más Rápido v3.0.0.0 en la pantalla de tu PC. Ya está disponible la compatibilidad nativa completa con pantallas 4K y Retina. Como siempre, la aplicación está enlazada estáticamente y no requiere DLL ni componentes del sistema operativo de terceros. Mientras tanto, en el linaje de Windows, todos los sistemas, desde Windows 7 hasta Windows 11, son compatibles.
Sin embargo, tenga en cuenta que las compilaciones de sistemas operativos de 32 bits (normalmente para Windows) han quedado obsoletas. La nueva aplicación será solo de 64 bits para todas las plataformas. ¡Prepárense!

![Captura de pantalla del desarrollador del avance de El Clicker de Ratón Más Rápido v3.0.0.0 (edición multiplataforma Qt)](/The-Fastest-Mouse-Clicker-for-Windows/screenshots_new/v3.0.0.0/TheFastestMouseClickerQt.png)

Actualmente se está produciendo un gran progreso. Se ha investigado todo lo relacionado con el funcionamiento de una aplicación multiplataforma.
Se ha realizado una refactorización inicial del código. La biblioteca [libuiohook](https://github.com/kwhat/libuiohook){:target="_blank"} presenta un diseño bastante claro.

![Captura de pantalla del desarrollador del tráiler para El Clicker de Ratón Más Rápido v3.0.0.0 (edición Qt multiplataforma)](/The-Fastest-Mouse-Clicker-for-Windows/screenshots_new/v3.0.0.0/TheFastestMouseClicker.png)

### Gran actualización 1 de marzo de 2023

El Fastest Mouse Clicker v3.0.0.0 (edición Qt) utilizará la biblioteca multiplataforma libuiohook para gestionar eventos de ratón y teclado en todas las pantallas del sistema. Su interfaz gráfica se rediseñará por completo para grabar y reproducir automáticamente todos los eventos de ratón y teclado. Incluso podrá editar la secuencia grabada en profundidad y modificar su velocidad de reproducción.
Además, podrá aleatorizar cada clic del ratón o pulsación del teclado. También se admitirán eventos de rueda del ratón.

La idea para la grabación es:

* Para ejecutar la función de despacho de libuiohook en un hilo de Qt independiente:

<pre><code title="Función de despacho libuiohook ejecutándose en un hilo separado">
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

* Defina un evento Qt personalizado para transferir datos de eventos libuiohook entre subprocesos Qt (trabajador y UI):

<pre><code title="Evento Qt personalizado para transferir datos de eventos libuiohook entre subprocesos Qt (trabajador y UI)">
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

* Es útil definir postMyCustomEvent() como un método público de la clase UI principal y luego implementar su propio customEvent() virtual:

<pre><code title="Defina postMyCustomEvent() como un método público de la clase UI principal, luego implemente su propio customEvent() virtual">
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

La idea para la reproducción es:

* Implementar QApplication::notify() virtual como una forma útil de gestionar eventos Qt adecuados en un solo lugar, sin señales ni ranuras:

<pre><code title="Implemente QApplication::notify() virtual propio como una forma útil de manejar eventos Qt adecuados en un solo lugar">
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

* La idea de editar la secuencia grabada es un enfoque estándar basado en [QListWidget](https://doc.qt.io/qt-5/qlistwidget.html){:target="_blank"}.

Captura de pantalla resultante de MS Visual Studio 2019 que une Qt y libuiohook:

![Captura de pantalla resultante de MS Visual Studio 2019 que une Qt y libuiohook](/The-Fastest-Mouse-Clicker-for-Windows/screenshots_new/v3.0.0.0/qt_libuiohook.png)


#### {{ site.t['copyright_text'][page.lang] }} [{{ site.t['author_name'][page.lang] }}]({{ site.prod-url }}{{ site.t['home'][page.lang] }})
