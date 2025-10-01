---
i18n-link: the-fastest-mouse-clicker-for-windows-help-how-to-use
permalink: /The-Fastest-Mouse-Clicker-for-Windows/Help-How-To-Use/

alternates:
  es: /es/El-Clicker-de-Raton-Mas-Rapido-para-Windows/Ayuda-Como-Usar/
  pt: /pt/O-Mais-Rapido-Mouse-Clicker-para-Windows/Ajuda-Como-Usar/

title: "The Fastest Mouse Clicker for Windows | Help How To Use"
description: "The fastest auto-clicker for Windows PC. A detailed guide on how to utilize the app in your everyday activities with best efficiency"
description_rich: "The fastest auto-clicker for Windows PC. A detailed guide on how to utilize the app in your everyday activities with best efficiency"
---

## {{ page.title | default: site.t['title'][page.lang] }}

### {{ page.description_rich | default: site.t['description_rich'][page.lang] }}

> {{ site.t['updated_text'][page.lang] }} : {{ site.t['updated_month'][page.lang] }} {{ site.upd_day_year }}.

YOU CAN START THE AUTO-CLICKING AT ANY MOMENT BY PRESSING THE &lt;trigger key&gt; (13 = Enter). Reading the entire Help is optional.

THE FIELDS YOU CAN NOT MODIFY.

&lt;clicking status&gt; or &lt;random clicking status&gt;, the topmost text field, is either getting 'idle' or 'clicking'.
 It is shown as &lt;random clicking status&gt; only when all the rectangle sizes to click randomly inside it are specified in the command line correctly.
 Just press the \[Batch folder\] button and see the remarks in file run_clicker_with_random_clicking.bat.

&lt;number of clicks&gt;, the top text field, indicates total number of clicks performed.

THE FIELDS YOU CAN MODIFY (CALLED THE CLICKING PARAMETERS: THEY COULD BE SET FROM THE COMMAND LINE TOO, SEE BELOW).

&lt;clicks per second&gt;, the middle text field, is the frequency of the clicks measured in clicks per second.
 This frequency can be as high as one hundred thousands (100000) clicks per second.
 FRACTIONAL frequences are supported. For example, 0.5 corresponds to 1 click every 2 seconds, 0.25 - to 1 click every 4 seconds, etc.

&lt;begin/end trigger keys&gt;, below that, are the keyboard keys to trigger the mouse events. Just click on them and press an arbitrary key (or hit a mouse button).
 That key will then trigger the mouse clicks when it remains pressed. If you just press and release the key, only few clicks should be made.
 This behavior corresponds to &lt;trigger key mode&gt; = 'press', see how it changes on 'toggle' value below.
 Default number shown in the button, 13, is the 'Enter' key code (for example, 32 is the 'Space' key code, 112 is the 'F1' key code, etc.
 For all the key codes see [Windows docs](https://docs.microsoft.com/en-us/windows/win32/inputdev/virtual-key-codes){:target="_blank"}.

&lt;stop at&gt;, the lower text field, is the number of clicks before the clicking will automatically stop.
 0 is the default and means infinity, i.e. clicking will never stop.

&lt;trigger key mode&gt; is a radio-button group, you can select either 'press' or 'toggle' mode of clicking.
 In the 'press' mode (default), the mouse events are emitted only when the corresponding trigger key is kept pressed.
 In the 'toogle' mode, the mouse events are emitted between subsequent short hits to the &lt;begin trigger key&gt; and &lt;end trigger key&gt;.

&lt;mouse button to click&gt; is a radio-button group too, you can select either 'left', 'middle' or 'right' mouse button that will generate the clicks.

Note 1: You can't have the same mouse button be the trigger and clicker.
<br/>Note 2: You can't change the &lt;trigger key&gt; if you chose the left mouse button; you must press the \[Reset to defaults\] button.
<br/>Note 3: The &lt;trigger key&gt; still works when this program is minimized. You must close the program to stop a &lt;trigger key&gt; from clicking.

*NEW* All the clicking parameters are saved automatically between application run-times.

ADDITIONAL BUTTONS AND FEATURES.

\[STOP!\] button stops toggled clicking mandatory.
<br/>\[Help\] button displays this help window.
<br/>*NEW* \[Reset to defaults\] button sets all the clicking parameters back to their default values.
<br/>*NEW* \[Batch folder\] button opens the folder in File Explorer where all the batch files reside typically.
<br/>*NEW* To get help on the command line arguments, just press the \[Batch folder\] button and see the remarks in \*.bat files you find there.
<br/>*NEW* Independent keys for &lt;trigger key mode&gt; = 'toggle': if &lt;begin trigger key&gt; begins the clicking, then &lt;end trigger key&gt; stops it.
<br/>*NEW* &lt;Window Always Top&gt; checkbox: if checked, keeps the app's main window at topmost of others.
<br/>*BRAND NEW* The 'Run group app' button: record/play the sequences of mouse clicks.

#### {{ site.t['copyright_text'][page.lang] }} [{{ site.t['author_name'][page.lang] }}]({{ site.prod-url }}{{ site.t['home'][page.lang] }})
