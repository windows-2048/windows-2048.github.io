---
i18n-link: the-fastest-mouse-clicker-for-windows-click-speed-test
permalink: /pt/O-Mais-Rapido-Mouse-Clicker-para-Windows/Teste-de-Velocidade-de-Clique/

alternates:
  es: /es/El-Clicker-de-Raton-Mas-Rapido-para-Windows/Prueba-de-Velocidad-de-Clic/
  en: /The-Fastest-Mouse-Clicker-for-Windows/Click-Speed-Test/

title: "O Mais Rápido Mouse Clicker para Windows | Teste de Velocidade de Clique"
description: "O auto-clicker mais rápido para PC com Windows. Teste preciso e exato para sua velocidade de clique, adequado tanto para mãos humanas quanto para software de clique automático"
description_rich: "O auto-clicker mais rápido para PC com Windows. Teste preciso e exato para sua velocidade de clique, adequado tanto para mãos humanas quanto para software de clique automático"
---

## {{ page.title | default: site.t['title'][page.lang] }}

### {{ page.description_rich | default: site.t['description_rich'][page.lang] }}

> {{ site.t['updated_text'][page.lang] }} : {{ site.t['updated_month'][page.lang] }} {{ site.upd_day_year }}.

Aqui está o teste de velocidade de clique de última geração, ou teste CPS. "CPS" é uma abreviação de "Cliques por Segundo". Sem prelúdio. Sem anúncios múltiplos e terríveis. Sem anúncios. Sem blá-blá-blá.
O teste é totalmente multiplataforma: Windows, Linux, macOS, iPhone, Android ou qualquer dispositivo compatível com o padrão do navegador de internet.
Basta colocar a mão no mouse e clicar ou tocar com o dedo no celular ou aplicar seu software de emulação de clique na Grande Área Cinzenta abaixo por 5 segundos. E você verá os resultados!


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
    clickButon.textContent = "Clique aqui o mais rápido que puder por 5 segundos!";
    clickButon.onclick = beginClickTest;
    clickDivStars.setAttribute("class", "stars");
    clickDivStars.setAttribute("style", "--rating: 0.0;");
    clickDivStarsText.textContent = "Sua classificação de cliques: 0.0 of 5.";
}
endClickTest = function() {
    clickButon.onclick = null;
    clickButon.textContent = "Sua taxa de cliques é " + (nClicks / 5.0) + " Cliques Por Segundo (CPS).";
    var fStars = (nClicks / 5.0) / 10.0 * 4;
    if (fStars > 5.0)
        fStars = 5.0;
    fStars = fStars.toFixed(1);
    clickDivStars.setAttribute("class", "stars");
    clickDivStars.setAttribute("style", "--rating: " + fStars + ";");
    clickDivStarsText.textContent = "Sua classificação de cliques: " + fStars + " of 5.";
}
beginClickTest = function() {
    ++nClicks;
    clickButon.textContent = "" + nClicks;

    if (nClicks == 1) {
        nTimer = setTimeout(endClickTest, 5000);
    }
}
</script>

    <button id="clickTest" onclick="beginClickTest()">Clique aqui o mais rápido que puder por 5 segundos!</button>
    <br/><br/><button id="repeatTest" onclick="repeatClickTest()">Reinicie o teste</button>
</p>

<p>
<div id="clickStars" class="stars" style="--rating: 0.0;" ></div>
<div id="clickStarsText" class="stars-alt">Sua classificação de cliques: 0.0 of 5.</div>
</p>


#### {{ site.t['copyright_text'][page.lang] }} [{{ site.t['author_name'][page.lang] }}]({{ site.prod-url }}{{ site.t['home'][page.lang] }})
