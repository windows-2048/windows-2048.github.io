---
i18n-link: the-fastest-mouse-clicker-for-windows-help-how-to-use
permalink: /pt/O-Mais-Rapido-Mouse-Clicker-para-Windows/Ajuda-Como-Usar/

alternates:
  es: /es/El-Clicker-de-Raton-Mas-Rapido-para-Windows/Ayuda-Como-Usar/
  en: /The-Fastest-Mouse-Clicker-for-Windows/Help-How-To-Use/

title: "O Mais Rápido Mouse Clicker para Windows | Ajuda Como Usar"
description: "O auto-clicker mais rápido para PC com Windows. Um guia detalhado sobre como utilizar o aplicativo em suas atividades diárias com a melhor eficiência"
description_rich: "O auto-clicker mais rápido para PC com Windows. Um guia detalhado sobre como utilizar o aplicativo em suas atividades diárias com a melhor eficiência"
---

## {{ page.title | default: site.t['title'][page.lang] }}

### {{ page.description_rich | default: site.t['description_rich'][page.lang] }}

> {{ site.t['updated_text'][page.lang] }} : {{ site.t['updated_month'][page.lang] }} {{ site.upd_day_year }}.

VOCÊ PODE INICIAR O CLIQUE AUTOMÁTICO A QUALQUER MOMENTO PRESSIONANDO A &lt;tecla de gatilho&gt; (13 = Enter). A leitura de toda a Ajuda é opcional.

OS CAMPOS QUE VOCÊ NÃO PODE MODIFICAR.

&lt;clicking status&gt; ou &lt;random clicking status&gt;, o campo de texto mais acima, está ficando 'ocioso' ou 'clicando'.
Ele é exibido como &lt;status de clique aleatório&gt; somente quando todos os tamanhos de retângulo para clicar aleatoriamente dentro dele são especificados corretamente na linha de comando.
Basta pressionar o botão \[Batch folder\] e ver as observações no arquivo run_clicker_with_random_clicking.bat.

&lt;number of clicks&gt;, o campo de texto mais acima, indica o número total de cliques realizados.

OS CAMPOS QUE VOCÊ PODE MODIFICAR (CHAMADOS DE PARÂMETROS DE CLIQUE: ELES TAMBÉM PODEM SER CONFIGURADOS NA LINHA DE COMANDO, VEJA ABAIXO).

&lt;clicks per second&gt;, o campo de texto do meio, representa a frequência dos cliques, medida em cliques por segundo.
Essa frequência pode chegar a cem mil (100.000) cliques por segundo.
Frequências FRACIONÁRIAS são suportadas. Por exemplo, 0,5 corresponde a 1 clique a cada 2 segundos, 0,25 a 1 clique a cada 4 segundos, etc.

&lt;begin/end trigger keys&gt;, abaixo delas, estão as teclas do teclado para acionar os eventos do mouse. Basta clicar nelas e pressionar uma tecla arbitrária (ou pressionar um botão do mouse).
Essa tecla acionará os cliques do mouse enquanto permanecer pressionada. Se você apenas pressionar e soltar a tecla, apenas alguns cliques deverão ser feitos.
Este comportamento corresponde a &lt;trigger key mode&gt; = 'press'; veja como ele muda no valor 'toggle' abaixo.
O número padrão mostrado no botão, 13, é o código da tecla 'Enter' (por exemplo, 32 é o código da tecla 'Espaço', 112 é o código da tecla 'F1', etc.
Para todos os códigos de tecla, consulte a [documentação do Windows](https://docs.microsoft.com/en-us/windows/win32/inputdev/virtual-key-codes){:target="_blank"}.

&lt;stop at&gt;, o campo de texto inferior, indica o número de cliques antes que o clique pare automaticamente.
0 é o padrão e significa infinito, ou seja, o clique nunca para.

&lt;trigger key mode&gt; é um grupo de botões de opção; você pode selecionar o modo de clique "press" ou "toggle".
No modo "press" (padrão), os eventos do mouse são emitidos somente quando a tecla de gatilho correspondente é mantida pressionada.
No modo "toogle", os eventos do mouse são emitidos entre pressionamentos curtos subsequentes de &lt;begin trigger key&gt; e &lt;end trigger key&gt;.

&lt;mouse button to click&gt; também é um grupo de botões de opção; você pode selecionar o botão 'left', 'middle' ou 'right' do mouse que gerará os cliques.

Observação 1: Não é possível usar o mesmo botão do mouse como gatilho e clique.
<br/>Nota 2: Você não pode alterar a tecla &lt;trigger key&gt; se tiver escolhido o &lt;trigger key&gt; você deve pressionar o botão \[Reset to defaults\].
<br/>Nota 3: A tecla &lt;trigger key&gt; ainda funciona quando este programa está minimizado. Você deve fechar o programa para impedir que uma tecla &lt;trigger key&gt; clique.

*NOVO* Todos os parâmetros de clique são salvos automaticamente entre os tempos de execução do aplicativo.

BOTÕES E RECURSOS ADICIONAIS.

O botão \[STOP!\] impede que o clique alternado seja obrigatório.
<br/>O botão \[Help\] exibe esta janela de ajuda.
<br/>*NOVO* O botão \[Reset to defaults\] restaura todos os parâmetros de clique aos seus valores padrão.
<br/>*NOVO* O botão \[Batch folder\] abre a pasta no Explorador de Arquivos onde normalmente residem todos os arquivos de lote.
<br/>*NOVO* Para obter ajuda sobre os argumentos da linha de comando, basta pressionar o botão \[Batch folder\] e ver as observações nos arquivos \*.bat que você encontrar lá.
<br/>*NOVO* Teclas independentes para &lt;trigger key mode&gt; = 'toggle': se &lt;begin trigger key&gt; iniciar o clique, então &lt;end trigger key&gt; o interrompe.
<br/>*NOVO* &lt;Window Always Top&gt; Caixa de seleção: se marcada, mantém a janela principal do aplicativo acima das demais.
<br/>*NOVÍSSIMO* Botão "Run group app": grava/reproduz as sequências de cliques do mouse.

#### {{ site.t['copyright_text'][page.lang] }} [{{ site.t['author_name'][page.lang] }}]({{ site.prod-url }}{{ site.t['home'][page.lang] }})
