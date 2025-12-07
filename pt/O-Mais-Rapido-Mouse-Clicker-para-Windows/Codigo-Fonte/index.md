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

O código-fonte completo com comentários pode ser assistido no
[Github](https://github.com/windows-2048/The-Fastest-Mouse-Clicker-for-Windows){:target="_blank"}
e no [Gitlab](https://gitlab.com/mashanovedad/The-Fastest-Mouse-Clicker-for-Windows){:target="_blank"}.

## O Mais Rápido Mouse Clicker para Windows v3.0.0.0 (edição Qt multiplataforma)

**Isso já está em [produção](/pt/O-Mais-Rapido-Mouse-Clicker-para-Windows/).**

Primeiramente, compilei uma versão minimalista de 64 bits, estática/de tempo de execução estático, do Qt v5.15.5 (LTS), feita para Windows 7 a 11 sob o compilador MSVC 2019.

Opções de configuração:

```
C:\qt-src-5.15.5\configure -static -static-runtime -qt-zlib -qt-libjpeg -qt-libpng -qt-freetype -qt-pcre -qt-harfbuzz -no-sse4.1 -no-sse4.2 -no-avx2 -no-avx512 -no-pch -no-ssl -no-openssl -no-opengl -qpa windows -confirm-license -opensource -release -make libs -make tools -prefix c:/qt-5.15.5-static
```

Baixe [qt-5.15.5-static.zip](https://filedn.com/llBp1EbMQML0Hdv9A9SVo6b/qt-5.15.5-static.zip).

Captura de tela resultante do MS Visual Studio 2019 unindo Qt e libuiohook:

![Captura de tela resultante do MS Visual Studio 2019 unindo Qt e libuiohook](/The-Fastest-Mouse-Clicker-for-Windows/screenshots_new/v3.0.0.0/qt_libuiohook_2025.png)


#### {{ site.t['copyright_text'][page.lang] }} [{{ site.t['author_name'][page.lang] }}]({{ site.prod-url }}{{ site.t['home'][page.lang] }})
