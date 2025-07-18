---
i18n-link: the-fastest-mouse-clicker-for-windows-click-speed-test
permalink: /The-Fastest-Mouse-Clicker-for-Windows/Click-Speed-Test/

alternates:
  es: /es/El-Clicker-de-Raton-Mas-Rapido-para-Windows/Prueba-de-Velocidad-de-Clic/
  pt: /pt/O-Mais-Rapido-Mouse-Clicker-para-Windows/Teste-de-Velocidade-de-Clique/

title: "The Fastest Mouse Clicker for Windows | Click Speed Test"
description: "The fastest auto-clicker for Windows PC. Accurate and precise test for your clicking speed suitable for both human hands and auto-clicker software"
description_rich: "The fastest auto-clicker for Windows PC. Accurate and precise test for your clicking speed suitable for both human hands and auto-clicker software"
---

## {{ page.title | default: site.t['title'][page.lang] }}

### {{ page.description_rich | default: site.t['description_rich'][page.lang] }}

> {{ site.t['updated_text'][page.lang] }} : {{ site.t['updated_month'][page.lang] }} {{ site.upd_day_year }}.

Here is the cutting-edge click speed test or CPS test. "CPS" is an abbreviation for "Clicks Per Second". No prelude. No multiple and terrible ads. No ads at all. No blah-blah-blah.
Test is absolutely cross-platform: Windows, Linux, macOS, iPhone, Android or any device that supports the Internet browser's standard.
Just put your hand on the mouse and click or tap your phone by finger or apply your click emulation software to the Great Grey Area below for 5 seconds. And you see the results!


<p id="clickContainer">
<script>
var nClicks = 0;
var nTimer = null;
var clickButon = null;
var clickDivStars = null;
var clickDivStarsText = null;
window.onload = function() {
    clickButon = document.getElementById("clickTest");
    clickDivStars = document.getElementById("clickStars");
    clickDivStarsText = document.getElementById("clickStarsText");
}
repeatClickTest = function () {
    nClicks = 0;
    if (nTimer != null) {
        clearTimeout(nTimer);
        nTimer = null;
    }
    clickButon.textContent = "Click here as fast as you can for 5 seconds!";
    clickButon.onclick = beginClickTest;
    clickDivStars.setAttribute("class", "stars");
    clickDivStars.setAttribute("style", "--rating: 0.0;");
    clickDivStarsText.textContent = "Your clicking rating: 0.0 of 5.";
}
endClickTest = function() {
    clickButon.onclick = null;
    clickButon.textContent = "Your clicking rate is " + (nClicks / 5.0) + " Clicks Per Second (CPS).";
    var fStars = (nClicks / 5.0) / 10.0 * 4;
    if (fStars > 5.0)
        fStars = 5.0;
    fStars = fStars.toFixed(1);
    clickDivStars.setAttribute("class", "stars");
    clickDivStars.setAttribute("style", "--rating: " + fStars + ";");
    clickDivStarsText.textContent = "Your clicking rating: " + fStars + " of 5.";
}
beginClickTest = function() {
    ++nClicks;
    clickButon.textContent = "" + nClicks;

    if (nClicks == 1) {
        nTimer = setTimeout(endClickTest, 5000);
    }
}
</script>

    <button id="clickTest" onclick="beginClickTest()">Click here as fast as you can for 5 seconds!</button>
    <br/><br/><button id="repeatTest" onclick="repeatClickTest()">Restart the test</button>
</p>

<p>
<div id="clickStars" class="stars" style="--rating: 0.0;" ></div>
<div id="clickStarsText" class="stars-alt">Your clicking rating: 0.0 of 5.</div>
</p>

#### Records

<div class="video-container">
    <iframe
        src="https://www.youtube.com/embed/Vyrtd4s5E5s?rel=0&modestbranding=1"
        title="I Became The Fastest Mouse Clicker in the World 2025"
        frameborder="0"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
        allowfullscreen
        loading="lazy" >
    </iframe>
</div>

I became the fastest mouse clicker in the world.
The goal is to get as many mouse clicks as you can
within just 5 seconds.
The test starts automatically on your first click or tap
and yes you can test not only your mouse on PC but also your finger on iPhone.
And since I pride myself in my fast Twitch muscle fibers and dexterity
I figured I'd give it a try.
Imagine, I was told the record is 100 clicks per second
which seem unreachable so I've began my quest.
I was doing better than I expected getting 76 and 93
on my first two attempts but I still needed more speed.
So I tried a new technique deploying 3 fingers simultaneously
to increase my clicks per second.
Here comes a dramatic difference compared to Sambucha, the previous winner.
He returned to 1 finger but I could utilize all 3 ones.
After tens of training attempts I've reached 273 clicks per second!

#### Education behind the stage

* [Browser-side JavaScript code example for beginners: the Click Speed Test for your mouse](https://www.reddit.com/r/learnjavascript/comments/1lj86qy/browserside_javascript_code_example_for_beginners/){:target="_blank"}

#### {{ site.t['copyright_text'][page.lang] }} [{{ site.t['author_name'][page.lang] }}]({{ site.prod-url }}{{ site.t['home'][page.lang] }})
