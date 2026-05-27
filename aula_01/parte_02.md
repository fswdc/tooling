# Parte 02

## Bloco 1 — Editor de Código versus Editor de Texto

### O problema

A operação do shell já faz parte do repertório: navegação pelo sistema de arquivos, criação de pastas e arquivos, tudo pela linha de comando. Mas escrever um arquivo com centenas de linhas de código usando apenas o shell implica operar sem destaque de cor, sem indentação que se ajuste automaticamente, sem busca que atravesse múltiplos arquivos simultaneamente, sem sinalização em tempo real de erros de sintaxe.

O Bloco de Notas resolve o problema do arquivo de texto simples. Funciona da mesma forma que uma chave de fenda comum funciona para apertar um parafuso de fenda cruzada: é possível, mas não é a ferramenta adequada.

Para escrever código profissionalmente, existe uma categoria de ferramenta específica: o **editor de código**. O **Visual Studio Code** é o editor de código que será utilizado neste curso. Esta aula existe para que a diferença entre editor de código e editor de texto fique clara, e para que o Visual Studio Code seja operado com fluência real — não apenas com a abertura do programa, mas com o entendimento do que cada região da interface faz e por que está ali.

### A cena

Considere uma pasta chamada `project` criada pelo shell. Dentro dela, é necessário escrever um arquivo com instruções para o computador — código. O Bloco de Notas resolve: digita-se, salva-se. Funciona.

Agora considere que esse arquivo tem 400 linhas. É necessário encontrar todas as ocorrências de uma palavra específica em outros oito arquivos da mesma pasta. É necessário que o editor sinalize quando um parêntese for deixado aberto. É necessário executar um comando de shell sem sair do editor. É necessário que o código se colore automaticamente para que a estrutura seja legível de relance, sem análise caractere por caractere.

O Bloco de Notas não oferece nenhuma dessas capacidades — não por deficiência, mas por escopo. Ele foi construído para texto simples: um bilhete, uma lista, uma nota rápida. Código tem estrutura, hierarquia, regras de sintaxe e múltiplos arquivos interdependentes. São demandas completamente diferentes.

### Limitações do editor de texto comum

Cada limitação é descrita com precisão, porque entender o problema é o que torna a solução compreensível.

**Ausência de destaque de sintaxe**. No Bloco de Notas, tudo aparece em preto sobre branco. Não há distinção visual entre uma palavra reservada e um valor definido pelo desenvolvedor, ou entre um comentário e uma instrução real. Em um arquivo com estrutura complexa, cada caractere precisa ser lido com atenção total para que a estrutura seja compreendida — equivalente a ler um livro inteiro sem capítulos, sem parágrafos, sem pontuação.

**Ausência de indentação automática**. Código usa indentação para expressar hierarquia — o que está contido dentro do quê. No Bloco de Notas, ao pressionar Enter, o cursor vai para a coluna zero. A tabulação precisa ser inserida manualmente em cada linha, sem assistência. Em arquivos com múltiplos níveis de hierarquia, isso se torna fonte constante de erro.

**Ausência de busca em múltiplos arquivos**. Um projeto real não é um arquivo único — é uma pasta com dezenas ou centenas de arquivos. Localizar onde uma palavra específica aparece em qualquer um deles está fora da capacidade do Bloco de Notas. Cada arquivo precisaria ser aberto individualmente.

**Ausência de terminal integrado**. Executar comandos de shell durante a edição de código exige alternância constante entre o editor e um terminal separado. Essa alternância acumula e interrompe o raciocínio.

**Ausência de gerenciamento de projeto**. O Bloco de Notas abre arquivos — um por vez. Não há noção de que aqueles arquivos pertencem a uma pasta com estrutura de projeto. Para navegar entre arquivos, é necessário recorrer ao Explorador de Arquivos do Windows, localizar cada arquivo e abri-lo individualmente.

### A definição

Um **editor de código** é um programa construído especificamente para escrever e navegar código-fonte. Ele conhece a estrutura das linguagens de programação, apresenta o conteúdo de forma que a estrutura fica visível, e integra as ferramentas que o desenvolvedor utiliza no mesmo lugar.

O **VSCode** — abreviação de Visual Studio Code — é o editor de código utilizado neste curso. É desenvolvido pela Microsoft, de código aberto, gratuito, e é atualmente o editor mais utilizado por desenvolvedores web no mundo.

Uma precisão importante antes de avançar: o nome "Visual Studio Code" pode causar confusão com outro produto da Microsoft chamado "Visual Studio" — sem o "Code". São ferramentas distintas. O Visual Studio é uma *IDE* (Integrated Development Environment — Ambiente de Desenvolvimento Integrado) pesada, usada principalmente para desenvolvimento em C# e .NET. O VSCode é um editor leve e extensível, utilizado para praticamente qualquer linguagem. Quando este curso menciona "VSCode", refere-se sempre ao Visual Studio Code — o editor leve.

## Bloco 2 — Instalação e Primeira Abertura

### O problema

O VSCode não vem instalado no Windows. Antes de qualquer operação, ele precisa estar disponível na máquina. Este bloco cobre onde obter o instalador, por que a fonte importa, e o que esperar na primeira abertura.

### Origem do instalador

O endereço oficial é `code.visualstudio.com`.

Há uma razão específica para enfatizar o site oficial em detrimento de outras fontes. Ao buscar "download VSCode" em um mecanismo de busca, os primeiros resultados podem incluir sites de terceiros que redistribuem instaladores. Esses instaladores podem estar desatualizados, modificados ou conter software adicional não solicitado. O site oficial garante o download exato do que a Microsoft publica, na versão mais recente, sem adições.

No site, há um botão de download em destaque. Ele detecta automaticamente o sistema operacional e oferece o instalador correspondente — o arquivo `.exe` para Windows 64 bits, padrão para qualquer máquina Windows moderna.

### O processo de instalação

Após o download do `.exe`, a execução segue o fluxo padrão de qualquer instalador do Windows: clique duplo, aceite do contrato de licença, avanço pelas telas.

Há uma tela específica que merece atenção: a tela de tarefas adicionais. Ela apresenta opções com caixas de seleção. Duas delas devem ser marcadas:

1. "**Adicionar ao PATH**". O **PATH** é uma lista que o Windows consulta quando um comando é digitado no shell — ele percorre essa lista procurando o programa correspondente. Marcar essa opção significa que, após a instalação, o comando `code` pode ser digitado diretamente no shell para abrir o VSCode. Sem essa opção, o comando `code` não funcionará no terminal.

2. "**Adicionar ação 'Abrir com Code' ao menu de contexto de diretórios**". Essa opção adiciona a entrada "Abrir com Code" ao menu de contexto do botão direito em qualquer pasta no Explorador de Arquivos do Windows, abrindo aquela pasta diretamente como projeto no VSCode. É um atalho de fluxo de trabalho de uso frequente.

Após o avanço por todas as telas e o clique em instalar, o processo leva cerca de um minuto. Ao final, o instalador oferece a opção de abrir o VSCode imediatamente.

### A primeira abertura

Na primeira abertura, o VSCode exibe uma tela de boas-vindas — uma aba chamada "Welcome" ou "Bem-vindo", dependendo do idioma do sistema. Essa tela contém atalhos para abrir pastas recentes, criar novos arquivos, acessar documentação e instalar extensões.

Essa aba pode ser fechada. Ela não é a interface de trabalho — é apenas uma porta de entrada. O que importa está por baixo dela, e é o que o próximo bloco cobre.

## Bloco 3 — Anatomia da Interface

### O problema

Abrir o VSCode pela primeira vez sem orientação prévia é equivalente a entrar numa cabine de avião sem saber o que cada instrumento faz. Tudo parece relevante, nada é autoevidente. Este bloco nomeia cada região, explica sua função operacional e explica por que ela existe onde existe.

### A estrutura

A interface do VSCode é dividida em cinco regiões. Cada uma tem uma responsabilidade distinta e não se sobrepõe à outra.

#### Região 1 — Barra de Atividades

É a faixa vertical estreita na extremidade esquerda da janela, contendo ícones empilhados verticalmente.

Cada ícone é uma porta de entrada para um painel lateral diferente. Os ícones padrão são: Explorador de Arquivos, Busca, Controle de Versão, Execução e Depuração, e Extensões.

A razão de existir como barra vertical separada — e não como menu no topo — é que essas são as ações alternadas com frequência durante o trabalho. O acesso com um único clique, sem abertura de menus, reduz a interrupção do fluxo.

Clicar em um ícone abre o painel lateral correspondente. Clicar no mesmo ícone novamente fecha o painel. O painel lateral nunca ocupa a área de edição — ele aparece ao lado dela.

#### Região 2 — Painel Lateral

É a área que aparece à direita da Barra de Atividades ao clicar em algum de seus ícones. Por padrão, o ícone ativo é o Explorador de Arquivos — representado por dois retângulos sobrepostos.

O Explorador de Arquivos exibe a estrutura de pastas e arquivos do projeto aberto. É por ele que se navega entre arquivos, criam-se novos arquivos dentro do projeto, criam-se subpastas, renomeia-se e deleta-se.

A palavra "projeto" aqui é precisa: o Explorador só exibe conteúdo quando uma pasta é aberta no VSCode — não um arquivo solto. Ao abrir apenas um arquivo, o Explorador permanece vazio. Essa distinção reaparece no Bloco 4, por ser uma das fontes de confusão mais comuns no início.

#### Região 3 — Área de Edição

É a região central e maior da interface — onde o código é efetivamente escrito.

Ela opera com abas. Cada arquivo aberto aparece como uma aba no topo da área de edição. É possível ter vários arquivos abertos simultaneamente e alternar entre eles clicando nas abas, da mesma forma que se alterna entre abas no navegador.

O VSCode também permite dividir a área de edição em colunas — dois ou mais arquivos lado a lado. Isso é útil quando é necessário consultar um arquivo enquanto se edita outro. Essa divisão não afeta nenhuma outra região da interface.

#### Região 4 — Painel Inferior

É a área que aparece na parte inferior da janela. Pode estar fechada por padrão — abre-se pelo menu `View > Terminal` ou pelo atalho apresentado no Bloco 5.

O Painel Inferior contém cinco abas: Problems, Output, Debug Console, Terminal e Ports. A aba Terminal é a de uso mais frequente, com larga margem — e é exatamente o assunto do Bloco 5.

#### Região 5 — Barra de Status

É a faixa horizontal fina na extremidade inferior da janela, abaixo do Painel Inferior.

Ela exibe informações contextuais sobre o estado atual do editor: problemas detectados, posição do cursor no arquivo (linha e coluna), quantidade de colunas de indentação, codificação do arquivo, tipo de quebra de linha, linguagem do arquivo em foco, entre outros.

Essas informações são passivas — não há interação direta com a Barra de Status na maior parte do tempo. Ela é útil para diagnóstico: quando algo parece incorreto, a Barra de Status frequentemente revela o motivo. Por exemplo, se o destaque de sintaxe não funciona como esperado, o campo de linguagem na Barra de Status indica se o VSCode identificou corretamente o tipo do arquivo.

### A Paleta de Comandos

Há um elemento que não é uma região visual, mas que conecta todas elas: a **Paleta de Comandos**.

O acesso é pelo atalho `Ctrl + Shift + P` no Windows.

A Paleta de Comandos é uma barra de busca que dá acesso a qualquer funcionalidade do VSCode pelo nome. Em vez de memorizar onde cada opção está em qual menu, abre-se a Paleta, digita-se o que se quer fazer, e o VSCode localiza. Trocar o shell padrão do terminal, mudar a linguagem do arquivo, formatar o documento, abrir configurações — tudo acessível pela Paleta.

Ela existe porque editores de código possuem centenas de funcionalidades. Exigir a memorização da localização de cada uma nos menus seria inviável. A Paleta inverte a lógica: em vez de navegar até a função, chama-se a função pelo nome.

## Bloco 4 — Abertura e Edição de Projetos

### O problema

Conhecer o VSCode e reconhecer sua interface não é suficiente para trabalhar. É necessário saber como trazer um projeto para dentro do editor, como criar arquivos dentro dele e — criticamente — entender a diferença entre abrir um arquivo solto e abrir uma pasta como projeto. Essa diferença parece pequena e não é.

### Arquivo solto versus pasta como projeto

Ao abrir um arquivo solto no VSCode — pelo menu `File > Open File` ou arrastando um arquivo para a janela — o VSCode exibe o conteúdo daquele arquivo na área de edição. Só isso. O Explorador de Arquivos permanece vazio. O VSCode não tem contexto de projeto: não sabe que aquele arquivo pertence a uma pasta com outros arquivos relacionados. Ele vê apenas aquele documento isolado.

Ao abrir uma pasta como projeto — pelo menu `File > Open Folder` — o VSCode carrega a pasta inteira. O Explorador de Arquivos passa a exibir todos os arquivos e subpastas dentro dela. A busca em projeto passa a operar sobre todos esses arquivos. O terminal integrado abre já posicionado dentro dessa pasta.

A distinção é a mesma que existe entre abrir uma única foto em um visualizador e abrir o álbum inteiro. No primeiro caso, vê-se uma imagem. No segundo, há contexto, navegação e acesso a tudo que pertence àquele conjunto.

Em desenvolvimento web, o trabalho acontece sempre com pastas — nunca com arquivos isolados. Um projeto web é uma pasta com estrutura: arquivos de código, subpastas, arquivos de configuração. Abrir o arquivo solto em vez da pasta é o erro mais comum no início, e ele se manifesta exatamente desta forma: Explorador vazio, nenhum contexto de projeto.

### Abertura de pasta no Windows

Há três formas, e as três chegam ao mesmo resultado:

1. Pelo menu: `File > Open Folder`, navegação até a pasta desejada e confirmação.

2. Pelo atalho `Ctrl + K, Ctrl + O` — duas combinações em sequência. Pressiona-se `Ctrl + K`, solta-se, pressiona-se `Ctrl + O`. Isso abre a mesma janela de seleção de pasta.

3. Pelo menu de contexto do Windows: clique com o botão direito em qualquer pasta no Explorador de Arquivos do Windows e seleção de "Abrir com Code" — opção disponível apenas se a caixa correspondente foi marcada durante a instalação.

No curso, o fluxo padrão será diferente dos três acima. O terminal do sistema é aberto, navega-se até a pasta do projeto pelo shell, e digita-se `code .` — um comando que abre o VSCode já com aquela pasta carregada como projeto. O ponto após `code` significa "a pasta atual". Esse fluxo funciona porque o VSCode foi adicionado ao PATH durante a instalação. Esse fluxo será aprendido naturalmente quando aparecer no contexto de uso real, nas próximas aulas.

### Criação de arquivos dentro do projeto

Com uma pasta aberta no Explorador de Arquivos, novos arquivos podem ser criados de duas formas.

A primeira é pelo Explorador: posicionar o cursor sobre o nome da pasta no painel lateral e clicar no ícone de novo arquivo — um retângulo com um sinal de adição. Digita-se o nome do arquivo incluindo a extensão e pressiona-se Enter.

A segunda é pela Paleta de Comandos: `Ctrl + Shift + P`, digitar "New File" e confirmar.

A extensão do arquivo é relevante. O VSCode usa a extensão para identificar a linguagem e aplicar o destaque de sintaxe correto.

### Edição e salvamento

A edição é direta: clica-se no arquivo no Explorador, ele abre na área de edição, e o conteúdo é digitado. O VSCode aplica indentação automática, destaque de sintaxe e fecha pares de caracteres automaticamente — parênteses, colchetes, aspas.

O salvamento é pelo atalho `Ctrl + S`. Quando um arquivo tem alterações não salvas, o VSCode exibe um ponto na aba do arquivo — um círculo pequeno no lugar do ícone de fechar. Enquanto esse ponto estiver visível, o arquivo no disco não reflete o que está na tela. Esse detalhe é relevante: ao recarregar uma página no navegador para verificar mudanças no código, o navegador lê o arquivo do disco — não o que está na memória do VSCode. Um arquivo não salvo resulta em exibição da versão anterior.

## Bloco 5 — Terminal Integrado

### O problema

A operação do terminal do Windows já está estabelecida. Durante o desenvolvimento, porém, há alternância constante entre escrever código e executar comandos — iniciar um serviço, instalar um pacote. Com o terminal em janela separada, cada alternância é uma interrupção: sai-se do VSCode, clica-se no terminal, executa-se o comando, retorna-se ao VSCode. Isso acumula. O terminal integrado resolve esse problema mantendo tudo no mesmo lugar.

### O que é o terminal integrado

O terminal integrado do VSCode é um terminal completo e funcional dentro do Painel Inferior do editor. Ele executa o mesmo shell configurado na Aula 1. Não é uma simulação nem uma versão limitada: é o mesmo ambiente de linha de comando, acessível sem sair do VSCode.

### Como abrir

O atalho no Windows é `Ctrl + J`. Pressionar essa combinação abre o Painel Inferior com o terminal ativo. Pressionar novamente fecha o painel.

O terminal também pode ser aberto pelo menu: `View > Terminal`.

### Diferença em relação ao terminal do sistema

Há uma diferença relevante que não é óbvia na primeira utilização: o diretório de trabalho inicial.

Ao abrir o terminal do sistema operacional — o Prompt de Comando ou o PowerShell pela barra de tarefas — ele abre no diretório padrão do usuário. É necessário navegar até a pasta do projeto com comandos de shell.

Ao abrir o terminal integrado do VSCode com uma pasta de projeto aberta, ele já começa posicionado dentro dessa pasta. O terminal sabe onde o projeto está porque o VSCode sabe — a pasta foi aberta como projeto. Não é necessário navegar.

Essa diferença é operacionalmente significativa. Ao longo do curso, dezenas de comandos precisam ser executados de dentro da pasta do projeto. Um terminal posicionado no lugar errado faz esses comandos falharem ou produzirem efeitos no local incorreto. O terminal integrado elimina essa fonte de erro ao iniciar sempre no lugar certo.

### Escolha do shell padrão

O VSCode pode utilizar diferentes shells no terminal integrado. No Windows, as opções comuns são o Prompt de Comando (`cmd.exe`) e o PowerShell. O VSCode escolhe um padrão automaticamente, mas a troca é possível.

A troca é feita pela Paleta de Comandos: `Ctrl + Shift + P`, digitar `Terminal: Select Default Profile`, e escolher o shell desejado na lista exibida. A partir desse momento, todo novo terminal integrado aberto utilizará o shell escolhido.

No curso, o shell utilizado é o mesmo configurado na Aula 1. A consistência importa mais do que a escolha em si — trocar de shell no meio do curso sem razão técnica cria inconsistências desnecessárias.

### Múltiplos terminais

O terminal integrado suporta mais de uma instância aberta simultaneamente. No canto superior direito do Painel Inferior, há um ícone de adição que abre um novo terminal. Cada terminal é independente — tem seu próprio processo de shell, seu próprio histórico de comandos, sua própria posição no sistema de arquivos.

Isso é útil quando é necessário manter um processo em execução em um terminal enquanto outros comandos são executados em outro. Esse recurso será utilizado nas próximas partes do curso. Por enquanto, um terminal é suficiente.

## Bloco 6 — Atalhos Fundamentais

### O problema

O VSCode tem centenas de funcionalidades. Acessar cada uma pelo menu é possível, mas lento — e lentidão acumulada ao longo de horas de trabalho é custo real. Atalhos de teclado eliminam essa fricção para as operações mais frequentes. Este bloco cobre os atalhos de uso diário, sem exceção.

### Paleta de Comandos — `Ctrl + Shift + P`

**O que este comando faz**: abre a barra de busca que dá acesso a qualquer funcionalidade do VSCode pelo nome.

**Por que ele existe**: o VSCode tem mais funcionalidades do que qualquer menu consegue exibir de forma navegável. A Paleta inverte a lógica — em vez de procurar a função nos menus, chama-se pelo nome.

**Decisão técnica**: a Paleta de Comandos é um padrão adotado por editores modernos para resolver o problema de descoberta de funcionalidades em ferramentas com grande superfície de capacidades. No VSCode, ela é o ponto de entrada universal — qualquer funcionalidade acessível por menu também é acessível pela Paleta. No curso, ela é o caminho preferencial para operações que não têm atalho direto.

**Onde é usado**: para acessar funcionalidades sem atalho memorizado, trocar configurações do editor, executar operações pontuais como mudança de linguagem do arquivo ou formatação do documento.

**Contrafactual**: sem a Paleta, cada funcionalidade exigiria navegação por menus aninhados cuja localização muda dependendo do contexto. Para operações executadas dezenas de vezes por dia, isso acumula em interrupção de fluxo.

### Busca em arquivo — `Ctrl + F`

**O que este comando faz**: abre uma barra de busca dentro do arquivo em foco na área de edição, destacando todas as ocorrências do termo buscado e posicionando o cursor na primeira.

**Por que ele existe**: arquivos de código crescem. Localizar onde uma palavra específica aparece em um arquivo de 300 linhas sem busca implica percorrer linha por linha.

**Decisão técnica**: `Ctrl + F` é o atalho de busca padrão na maioria dos programas do Windows — navegadores, editores de texto, leitores de PDF. O VSCode adota o mesmo atalho por consistência com o ambiente operacional. A busca dentro do arquivo é distinta da busca em projeto (`Ctrl + Shift + F`); cada uma opera em escopo diferente.

**Onde é usado**: para localizar uma variável, uma função ou um valor específico dentro do arquivo atualmente em edição; para verificar quantas vezes um termo aparece antes de uma refatoração.

**Contrafactual**: sem `Ctrl + F`, a alternativa é rolagem manual ou uso de `Ctrl + Shift + End` para ir ao fim do arquivo e tentar localizar visualmente. Para arquivos pequenos, funciona. Para arquivos reais, não.

### Busca em projeto — `Ctrl + Shift + F`

**O que este comando faz**: abre o painel de busca no Painel Lateral, permitindo buscar um termo em todos os arquivos da pasta de projeto aberta simultaneamente.

**Por que ele existe**: projetos têm múltiplos arquivos interdependentes. Localizar onde um determinado nome aparece — em quantos arquivos, em quais linhas — é uma operação recorrente em desenvolvimento.

**Decisão técnica**: a busca em projeto opera sobre todos os arquivos da pasta aberta, não apenas sobre o arquivo em foco. Esse escopo mais amplo é o que distingue `Ctrl + Shift + F` de `Ctrl + F`. O resultado é exibido no Painel Lateral como lista de ocorrências agrupadas por arquivo, com visualização do trecho de contexto de cada ocorrência.

**Onde é usado**: para localizar todas as referências a uma função ou variável antes de renomeá-la; para verificar em quais arquivos um determinado valor de configuração aparece; para rastrear onde um comportamento específico está implementado.

**Contrafactual**: sem a busca em projeto, seria necessário abrir cada arquivo individualmente e executar `Ctrl + F` em cada um. Para um projeto com dez arquivos, isso já é inviável na prática.

### Duplicar linha — `Shift + Alt + Down`

**O que este comando faz**: copia a linha onde o cursor está e insere a cópia imediatamente abaixo, posicionando o cursor na cópia.

**Por que ele existe**: em código, é frequente escrever uma linha e precisar de uma variação dela na linha seguinte — mesma estrutura, valor diferente. Duplicar e editar é mais rápido do que redigitar.

**Decisão técnica**: o atalho duplica especificamente para baixo (`Down`). Existe a variante `Shift + Alt + Up` para duplicar para cima, mas o fluxo natural de escrita é descendente — a cópia editável fica abaixo do original, que serve de referência visual imediata.

**Onde é usado**: ao criar múltiplos elementos com estrutura similar em sequência; ao escrever pares de linhas simétricas onde a segunda é variação da primeira.

**Contrafactual**: sem esse atalho, a operação exige seleção da linha inteira, cópia, descida de uma linha e colagem — quatro operações onde uma bastaria.

### Mover linha para cima — `Alt + Up`

**O que este comando faz**: move a linha onde o cursor está uma posição acima, trocando de lugar com a linha anterior.

**Por que ele existe**: a ordem das linhas em código frequentemente tem consequência funcional. Reordenar sem esse atalho exige recortar, reposicionar o cursor e colar — com risco de perda de conteúdo se a sequência for executada incorretamente.

**Decisão técnica**: o atalho troca as duas linhas de posição sem afetar nenhuma outra parte do arquivo. Não há operação de área de transferência envolvida — o conteúdo das linhas é invertido diretamente. O cursor acompanha a linha movida.

**Onde é usado**: para reordenar declarações, ajustar a sequência de instruções, mover uma linha de configuração para uma posição mais lógica no arquivo.

**Contrafactual**: sem `Alt + Up`, a operação requer `Ctrl + X` na linha, subida do cursor com seta, `Ctrl + V` — três operações com margem de erro na reposição do cursor.

### Mover linha para baixo — `Alt + Down`

**O que este comando faz**: move a linha onde o cursor está uma posição abaixo, trocando de lugar com a linha seguinte.

**Por que ele existe**: razão idêntica ao `Alt + Up` — reordenação de linhas sem operação de área de transferência.

**Decisão técnica**: os dois atalhos de movimentação de linha (`Alt + Up` e `Alt + Down`) formam um par simétrico. A direção é determinada pela tecla de seta. O comportamento é idêntico em ambos os casos: troca direta das duas linhas envolvidas.

**Onde é usado**: nos mesmos contextos de `Alt + Up`, na direção oposta.

**Contrafactual**: sem `Alt + Down`, a reordenação para baixo exige `Ctrl + X`, descida do cursor, `Ctrl + V` — mesma sequência de três operações com mesma margem de erro.

### Comentar linha — `Ctrl + /`

**O que este comando faz**: transforma a linha atual em comentário, ou remove o comentário se a linha já for um. Um comentário é uma linha que o interpretador ignora durante a execução do código.

**Por que ele existe**: durante o desenvolvimento, é frequente a necessidade de desativar temporariamente uma linha para testar o comportamento do código sem ela, sem apagá-la. Comentar e descomentar é esse mecanismo.

**Decisão técnica**: o VSCode detecta a linguagem do arquivo e usa o caractere de comentário correto para cada uma — `//` para JavaScript, `#` para Python, `<!-- -->` para HTML, entre outros. O mesmo atalho funciona em qualquer linguagem suportada, sem necessidade de memorizar a sintaxe de comentário de cada uma.

**Onde é usado**: para desativar uma instrução durante a depuração de código; para deixar anotações no código que não afetam a execução; para isolar um trecho problemático sem apagá-lo.

**Contrafactual**: sem esse atalho, seria necessário posicionar o cursor no início da linha, digitar o caractere de comentário correto para a linguagem, e repetir para cada linha. Para descomentar, o processo seria inverso. Em blocos com múltiplas linhas, isso acumula.

### Abrir terminal integrado — `Ctrl + J`

**O que este comando faz**: abre o Painel Inferior com a aba Terminal ativa. Se o Painel Inferior já estiver aberto, fecha-o.

**Por que ele existe**: a alternância entre área de edição e terminal é uma das operações mais frequentes do fluxo de desenvolvimento. Um atalho de teclado elimina a necessidade de clicar no menu ou na interface para essa transição.

**Decisão técnica**: `Ctrl + J` alterna a visibilidade do Painel Inferior como um todo, não apenas da aba Terminal. Se outras abas do Painel Inferior estiverem abertas (Problems, Output), elas permanecem no estado em que estavam. O terminal é a aba padrão exibida ao abrir. No curso, o Painel Inferior é utilizado quase exclusivamente para o terminal, de forma que `Ctrl + J` e "abrir o terminal" são equivalentes na prática.

**Onde é usado**: sempre que for necessário executar um comando de shell sem sair da área de edição; para verificar saída de processos em execução; para alternar entre escrita de código e linha de comando durante o desenvolvimento.

**Contrafactual**: sem `Ctrl + J`, abrir o terminal exige `View > Terminal` pelo menu ou clique na região do Painel Inferior. Para uma operação executada dezenas de vezes por sessão, isso acumula em fricção.

### Abrir pasta como projeto — `Ctrl + K, Ctrl + O`

**O que este comando faz**: abre a janela de seleção de pasta do sistema operacional para escolha da pasta a ser carregada como projeto no VSCode.

**Por que ele existe**: abrir pastas como projeto é o ponto de entrada de qualquer sessão de trabalho no VSCode. Um atalho de teclado para essa operação elimina a necessidade de navegar pelo menu `File > Open Folder` a cada início de trabalho.

**Decisão técnica**: o atalho é uma sequência de dois passos — `Ctrl + K` seguido de `Ctrl + O` — porque `Ctrl + K` é um prefixo de atalhos no VSCode (usado para múltiplas operações). A sequência com dois passos é o padrão do editor para atalhos que envolvem esse prefixo. No curso, o fluxo predominante para abrir projetos será `code .` no terminal, mas o atalho é útil quando o VSCode já está aberto e é necessário trocar de projeto.

**Onde é usado**: para abrir uma pasta de projeto quando o VSCode já está em execução; para trocar de projeto sem fechar e reabrir o editor.

**Contrafactual**: sem esse atalho, a abertura de pasta exige navegação pelo menu `File > Open Folder` ou uso do menu de contexto do Explorador de Arquivos do Windows — ambos dependentes de mouse.

## Bloco 7 — Extensões: Conceito e Acesso

### O problema

O VSCode, na instalação padrão, já é um editor funcional e capaz. Mas ele foi projetado para ser extensível — ou seja, para receber componentes adicionais que ampliam suas capacidades. Este bloco explica o que são essas extensões, onde ficam, e por que nenhuma será instalada durante este módulo. Essa última parte tem uma razão pedagógica precisa.

### O que é uma extensão

Uma **extensão** é um componente desenvolvido por terceiros — não pela Microsoft — que se instala dentro do VSCode e adiciona funcionalidades ausentes na instalação padrão.

Extensões existem para praticamente tudo: temas visuais, suporte a linguagens adicionais, integrações com serviços externos, ferramentas de formatação automática, assistentes de código. O *marketplace* do VSCode tem dezenas de milhares delas.

### Localização

O acesso ao *marketplace* de extensões está na Barra de Atividades — o ícone que parece quatro quadrados, com um deles levemente deslocado. Clicar nesse ícone abre o painel de extensões no Painel Lateral, com uma barra de busca no topo. Digita-se o nome ou a categoria, exibem-se os resultados, clica-se em instalar.

### Restrição durante este módulo

Essa restrição é inegociável, e tem uma justificativa pedagógica específica.

Extensões automatizam coisas. Algumas formatam o código automaticamente ao salvar. Algumas completam estruturas inteiras com um atalho. Algumas detectam erros e sugerem correções antes mesmo de o desenvolvedor entender por que aquilo é um erro.

O problema não é que essas automações sejam inadequadas. O problema é a ordem: automatizar o que ainda não foi compreendido significa que a compreensão nunca ocorre. O código produzido pode estar correto, mas sem saber por que está correto — e quando algo der errado, não há base mental para o diagnóstico.

A analogia é direta: aprender a dirigir em um carro que freia automaticamente antes de qualquer obstáculo impede o desenvolvimento do cálculo de distância de frenagem e do reflexo correspondente. O sistema funciona até o dia em que falha — e nesse dia, não há o recurso nem a habilidade.

No curso, cada capacidade é construída manualmente antes de qualquer ferramenta que a automatize. Quando a automação chegar, o que ela faz por baixo já terá sido feito à mão. Essa sequência não é arbitrária: é o que distingue um desenvolvedor que compreende o sistema de um desenvolvedor que depende de ferramentas que não compreende.

A restrição se aplica a extensões, temas, assistentes de código, ferramentas de tradução — qualquer componente de terceiros instalável no VSCode. Apenas recursos nativos da plataforma são utilizados neste módulo.
