---
i18n-link: the-fastest-mouse-clicker-for-windows-source-code
permalink: /The-Fastest-Mouse-Clicker-for-Windows/Source-Code/

alternates:
  es: /es/El-Clicker-de-Raton-Mas-Rapido-para-Windows/Codigo-Fuente/
  pt: /pt/O-Mais-Rapido-Mouse-Clicker-para-Windows/Codigo-Fonte/

title: "The Fastest Mouse Clicker for Windows | Source Code"
description: "The fastest auto-clicker for Windows PC. This app has been written in vanilla C/C++ with Win32 API calls described in official Microsoft documentation"
description_rich: "The fastest auto-clicker for Windows PC. This app has been written in vanilla C/C++ with Win32 API calls described in official Microsoft documentation"
---

## {{ page.title | default: site.t['title'][page.lang] }}

### {{ page.description_rich | default: site.t['description_rich'][page.lang] }}

> {{ site.t['updated_text'][page.lang] }} : {{ site.t['updated_month'][page.lang] }} {{ site.upd_day_year }}.

Complete source code with comments can be found on
[Github](https://github.com/windows-2048/The-Fastest-Mouse-Clicker-for-Windows){:target="_blank"}
and [Gitlab](https://gitlab.com/mashanovedad/The-Fastest-Mouse-Clicker-for-Windows){:target="_blank"}.

## The Fastest Mouse Clicker v3.0.0.0 (cross-platform Qt edition)

**All future versions of The Fastest Mouse Clicker for Windows will be cross-platform and made with Qt.**

First, I have compiled a 64-bit minimalistic, static/static-runtime build of Qt v5.15.5 (LTS) made for Windows 7 to 11 under MSVC 2019 compiler.

Configure options:

```
C:\qt-src-5.15.5\configure -static -static-runtime -qt-zlib -qt-libjpeg -qt-libpng -qt-freetype -qt-pcre -qt-harfbuzz -no-sse4.1 -no-sse4.2 -no-avx2 -no-avx512 -no-pch -no-ssl -no-openssl -no-opengl -qpa windows -confirm-license -opensource -release -make libs -make tools -prefix c:/qt-5.15.5-static
```

Download [qt-5.15.5-static.zip](https://filedn.com/llBp1EbMQML0Hdv9A9SVo6b/qt-5.15.5-static.zip).

Migration to cross-platform Qt edition of {{ site.t['app_name'][page.lang] }} is in successive progress. New application will get version 3.0.0.0 and will be called
"The Fastest Mouse Clicker for \<OS\> (cross-platform Qt edition)", where \<OS\> is "Windows", "Linux", "MacOS (M1)".
QtDesigner \*.ui makeup is ready today. I tease you to look how pleasant and beautiful The Fastest Mouse Clicker v3.0.0.0 will appear
on your PC screen. Full native support of 4K and Retina displays is here. As always, the application is statically linked and does not
require 3rd-party DLL or OS component. Meanwhile, among Windows lineage, all the systems from Windows&nbsp;7 to Windows&nbsp;11 are supported.
Note though, 32-bit OS builds (typically for Windows) have gone to the history. New app will be 64-bit only for all the platforms. Standby!

![Teaser developer's screenshot for The Fastest Mouse Clicker v3.0.0.0 (cross-platform Qt edition)](/The-Fastest-Mouse-Clicker-for-Windows/screenshots_new/v3.0.0.0/TheFastestMouseClickerQt.png)

A great progress is undergoing right now. All the things about how does a cross-platform app function have been investigated.
Initial code refactoring has been performed. The library [libuiohook](https://github.com/kwhat/libuiohook){:target="_blank"} is found to be pretty clearly designed.

![Trailer developer's screenshot for The Fastest Mouse Clicker v3.0.0.0 (cross-platform Qt edition)](/The-Fastest-Mouse-Clicker-for-Windows/screenshots_new/v3.0.0.0/TheFastestMouseClicker.png)

### Great update Mar 01 2023

The Fastest Mouse Clicker v3.0.0.0 (the Qt edition) will use [cross-platform libuiohook library](https://github.com/kwhat/libuiohook/){:target="_blank"}
to handle system all-displays-wide mouse and keyboard events. Its graphical UI will be completely re-designed to perform fully automatic
recording and playback all the mouse and keyboard events. You can even edit the sequence recorded in depth and modify its playback speed.
Furthermore you can randomize every mouse click or keyboard press. Mouse wheel events will be also supported.

The idea for recording is:

* To run libuiohook dispatch function in a separate Qt thread:

<pre><code title="libuiohook dispatch function running in a separate thread">
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

* Define custom Qt event to transfer libuiohook event data between Qt threads (worker and UI):

<pre><code title="Custom Qt event to transfer libuiohook event data between Qt threads (worker and UI)">
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

* It is useful to define postMyCustomEvent() as a public method of main UI class, then implement virtual own customEvent():

<pre><code title="Define postMyCustomEvent() as a public method of main UI class, then implement virtual own customEvent()">
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

The idea for playback is:

* Implement virtual own QApplication::notify() as a useful way to handle proper Qt events in one place without signals and slots:

<pre><code title="Implement virtual own QApplication::notify() as a useful way to handle proper Qt events in one place">
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

* The idea of editing sequence recorded is standard [QListWidget](https://doc.qt.io/qt-5/qlistwidget.html){:target="_blank"}-based approach.

Resulting MS Visual Studio 2019 screenshot joining Qt and libuiohook:

![Resulting MS Visual Studio 2019 screenshot joining Qt and libuiohook](/The-Fastest-Mouse-Clicker-for-Windows/screenshots_new/v3.0.0.0/qt_libuiohook.png)


#### {{ site.t['copyright_text'][page.lang] }} [{{ site.t['author_name'][page.lang] }}]({{ site.prod-url }}{{ site.t['home'][page.lang] }})
