---
i18n-link: the-fastest-mouse-clicker-for-windows-features
permalink: /pt/O-Mais-Rapido-Mouse-Clicker-para-Windows/Caracteristicos/

alternates:
  es: /es/El-Clicker-de-Raton-Mas-Rapido-para-Windows/Caracteristicas/
  en: /The-Fastest-Mouse-Clicker-for-Windows/Features/

title: O Mais Rápido Mouse Clicker para Windows | Característicos
description: O auto-clicker mais rápido para PC Windows. 100000 cliques por segundo. Lista abrangente dos recursos do programa
description_rich: O auto-clicker mais rápido para PC Windows. 100000 cliques por segundo. Lista abrangente dos recursos do programa
---

## {{ page.title | default: site.t['title'][page.lang] }}

### {{ page.description_rich | default: site.t['description_rich'][page.lang] }}

> {{ site.t['updated_text'][page.lang] }} : {{ site.t['updated_month'][page.lang] }} {{ site.upd_day_year }}.

Esta não é uma lista completa de todos os recursos do programa. Acabei de selecionar alguns deles, os mais importantes
do ponto de vista dos nossos usuários.
Como o texto de Ajuda ainda não está completo e não reflete todos os recursos implementados, sinta-se à vontade para criar
um [issue]({{ site.source_issues_url }}){:target="_blank"} para solicitar um recurso de sua preferência.

* A melhor taxa de cliques do mundo, de até 100.000 cliques por segundo, aumentada em 10 vezes em comparação com o aplicativo predecessor "Fast Mouse Clicker". A versão mais recente com problema de desempenho corrigido é 100 vezes mais rápida!

* Utiliza o recurso de matriz em lote de <code><a href="https://docs.microsoft.com/en-us/windows/win32/api/winuser/nf-winuser-sendinput" target="_blank">SendInput()</a></code> e manipula com <code><a href="https://docs.microsoft.com/en-us/windows/win32/api/synchapi/nf-synchapi-sleep" target="_blank">Sleep()</a></code> para atingir o melhor desempenho possível de cliques do mouse no Windows.

* Os botões esquerdo, do meio e direito do mouse são suportados e podem ser acionados para clique por uma tecla no teclado em um modo de pressionar ou alternar.

* Uma tecla arbitrária do teclado pode ser selecionada para disparar o processo de clique. Além disso, outro botão do mouse pode desempenhar o papel de uma tecla de disparo.

* Diferentes teclas de gatilho independentes para iniciar/terminar o clique no modo de alternância.

* O programa funciona bem mesmo se minimizado e também opera em uma área de trabalho arbitrária. O programa pode parar de clicar automaticamente, se um certo número de cliques for dado pelo usuário final.

* Este é um aplicativo gratuito e de código aberto, sem anúncios, vírus, trojans, malware, etc., para sempre.

* O programa tem um serviço de atualização integrado em construção que pode executar tarefas científicas adicionais quando sua CPU estiver ociosa com uso muito pequeno de CPU e Internet. Veja o código-fonte do instalador. O aplicativo desinstala claramente e NÃO é um vírus ou malware. Você pode alternar para os instaladores sem serviço de atualização e voltar com [a qualquer momento](https://github.com/windows-2048/The-Fastest-Mouse-Clicker-for-Windows/blob/master/InnoSetupDownloader/README.md){:target="_blank"}.

* O aplicativo pode ser usado em um sistema básico, não depende do .NET Framework ou de qualquer outra biblioteca externa como "Speed ​​AutoClicker", "Fast Clicker", etc.

* A linha de comando foi suportada: TheFastestMouseClicker.exe -c <cliques por segundo> -t <tecla de gatilho> -s <parar em> -m <modo de tecla de gatilho> -b <botão do mouse para clicar>, onde <modo de tecla de gatilho> pode ser 'pressionar' ou 'alternar' e <botão do mouse para clicar> pode ser 'esquerda', 'meio' ou 'direita'. Pode-se especificar qualquer parte dos argumentos; valores não especificados ou não reconhecidos serão tratados como padrões (veja-os executando o aplicativo e pressionando o botão 'Redefinir para padrões').

* O botão "Pasta em lote" foi adicionado para abrir um diretório com arquivos \*.bat rapidamente; ele simplifica muito o uso da linha de comando.

* Valores fracionários para o parâmetro clicks/s são suportados. Por exemplo, 0,5 clicks/s equivale a 1 clique a cada 2 segundos.

* O clique aleatório foi implementado. Basta clicar no botão "Pasta de lote" e ver as observações nos arquivos \*.bat que residem lá para saber como usar argumentos de linha de comando e habilitar o clique aleatório.

* Clique em grupo (gravar/reproduzir as sequências de cliques) suportado via aplicativo adicional desde a v.2.5.3.2. Você pode alternar rapidamente entre os aplicativos clicando no botão "Executar aplicativo de grupo"/"Executar aplicativo único".

* Caixa de seleção Janela Sempre no Topo para manter a janela do aplicativo na posição mais alta.

* Edição manual de opções/configurações como bônus para salvamento automático: basta abrir C: \ Usuários \ \<SeuUsuárioDoWindows\> \ AppData \ Roaming \ TheFastestMouseClicker \ TheFastestMouseClicker \ settings.dat
em qualquer editor de texto simples (você pode alterar o subcaminho TheFastestMouseClicker durante a instalação).


#### {{ site.t['copyright_text'][page.lang] }} [{{ site.t['author_name'][page.lang] }}]({{ site.prod-url }}{{ site.t['home'][page.lang] }})
