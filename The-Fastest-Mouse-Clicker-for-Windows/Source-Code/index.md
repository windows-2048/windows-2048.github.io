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

**That is already in [production](/The-Fastest-Mouse-Clicker-for-Windows/).**

I have compiled a 64-bit minimalistic, static/static-runtime build of Qt v5.15.5 (LTS) made for Windows 7 to 11 under MSVC 2019 compiler.

Configure options:

```
C:\qt-src-5.15.5\configure -static -static-runtime -qt-zlib -qt-libjpeg -qt-libpng -qt-freetype -qt-pcre -qt-harfbuzz -no-sse4.1 -no-sse4.2 -no-avx2 -no-avx512 -no-pch -no-ssl -no-openssl -no-opengl -qpa windows -confirm-license -opensource -release -make libs -make tools -prefix c:/qt-5.15.5-static
```

Download [qt-5.15.5-static.zip](https://filedn.com/llBp1EbMQML0Hdv9A9SVo6b/qt-5.15.5-static.zip).

Resulting MS Visual Studio 2019 screenshot joining Qt and libuiohook:

![Resulting MS Visual Studio 2019 screenshot joining Qt and libuiohook](/The-Fastest-Mouse-Clicker-for-Windows/screenshots_new/v3.0.0.0/qt_libuiohook_2025.png)


#### {{ site.t['copyright_text'][page.lang] }} [{{ site.t['author_name'][page.lang] }}]({{ site.prod-url }}{{ site.t['home'][page.lang] }})
