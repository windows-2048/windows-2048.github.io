---
i18n-link: the-fastest-mouse-clicker-for-windows-features
permalink: /The-Fastest-Mouse-Clicker-for-Windows/Features/

alternates:
  es: /es/El-Clicker-de-Raton-Mas-Rapido-para-Windows/Caracteristicas/
  pt: /pt/O-Mais-Rapido-Mouse-Clicker-para-Windows/Caracteristicos/

title: The Fastest Mouse Clicker for Windows | Features
description: The fastest auto-clicker for Windows PC. 100000 clicks per second. Comprehensive list of the program features
description_rich: The fastest auto-clicker for Windows PC. 100000 clicks per second. Comprehensive list of the program features
---

## {{ page.title | default: site.t['title'][page.lang] }}

### {{ page.description_rich | default: site.t['description_rich'][page.lang] }}

> {{ site.t['updated_text'][page.lang] }} : {{ site.t['updated_month'][page.lang] }} {{ site.upd_day_year }}.

This is not a complete list of all the features of the program. I have just selected several of them most important
from the point of view of our users.
Because the Help text is not yet complete and does not reflect all the features implemented, feel free to create
an [issue]({{ site.source_issues_url }}){:target="_blank"} to request a feature of your desire.

* The world's best click rate up to 100 000 clicks per second, increased by 10 times comparing with the predecessor application "Fast Mouse Clicker". The latest version with fixed performance issue is 100 times faster!

* Utilizes batch-array feature of <code><a href="https://docs.microsoft.com/en-us/windows/win32/api/winuser/nf-winuser-sendinput" target="_blank">SendInput()</a></code> and manipulates with <code><a href="https://docs.microsoft.com/en-us/windows/win32/api/synchapi/nf-synchapi-sleep" target="_blank">Sleep()</a></code> to reach the ultimate possible performance of mouse clicks on Windows.

* The Left, Middle, and Right mouse buttons are supported, they can be triggered for clicking by a key on the keyboard in a press or toggle mode.

* Arbitrary keyboard key can be selected to trigger the clicking process. Furthermore, an another mouse button can play a role of a trigger key.

* Different independent trigger keys to begin/end the clicking in toggle mode.

* The program works fine even if it is minimized and also it operates on an arbitrary desktop area. The program can stop to click automatically, if a certain number of clicks is given by end-user.

* This is free, open source application without ads, viruses, trojans, malware, etc. forever.

* The program has built-in updater service under construction that may perform additional scientific tasks when your CPU is idle with very tiny CPU and Internet usage. See source code of the installer. The application uninstalls clearly and is NOT a virus or malware. You may switch to the installers without update service and back with [in any moment](https://github.com/windows-2048/The-Fastest-Mouse-Clicker-for-Windows/blob/master/InnoSetupDownloader/README.md){:target="_blank"}.

* The application can be used on a bare system, it does not depend on .NET Framework or any other external library as "Speed AutoClicker", "Fast Clicker", etc.

* Command line has been supported: TheFastestMouseClicker.exe -c <clicks per second> -t <trigger key> -s <stop at> -m <trigger key mode> -b <mouse button to click>, where <trigger key mode> can be 'press' or'toggle' and <mouse button to click> can be 'left', 'middle', or 'right'. One may specify any part of arguments; unspecified or unrecognized values will be treated as defaults (see them by running the app and pressing 'Reset to defaults' button.

* Button "Batch folder" has been added to open a directory with \*.bat files quickly; it simplifies command line usage a lot.

* Fractional values for clicks/s parameter are supported. For example, 0.5 clicks/s equals to 1 click every 2 seconds.

* Random clicking has been implemented. Just click the "Batch folder" button and see remarks in the \*.bat files reside there in order how to use command line arguments and to enable random clicking.

* Group clicking (record/play the sequences of clicks) supported via additional application since v.2.5.3.2. You can quickly switch between the applications by clicking the "Run group app"/"Run single app" button.

* Window Always Top checkbox to keep the app's window topmost.

* Manual options/settings editing as a bonus to automatic saving: just open C: \ Users \ \<YourWindowsUser\> \ AppData \ Roaming \ TheFastestMouseClicker \ TheFastestMouseClicker \ settings.dat
in any plain text editor (you might change sub-path TheFastestMouseClicker during installation).


#### {{ site.t['copyright_text'][page.lang] }} [{{ site.t['author_name'][page.lang] }}]({{ site.prod-url }}{{ site.t['home'][page.lang] }})
