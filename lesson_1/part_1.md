# Parte 1

## Bloco 1 — Interface Gráfica e Linha de Comando

### O problema

A operação básica do sistema operacional já faz parte do repertório cotidiano: criar pastas, mover arquivos, instalar programas, navegar em janelas. Tudo isso funciona por meio de uma interface que responde a cliques. Botões, ícones e menus são apresentados visualmente e interagidos da mesma forma.

Essa interface tem um nome técnico: **GUI**, do inglês *Graphical User Interface* (Interface Gráfica do Usuário).

A GUI foi projetada para ser intuitiva. Não é necessário saber o nome técnico: o elemento é visto, reconhecido e clicado. Essa é uma vantagem considerável para uso cotidiano — mas para desenvolvimento de software, a GUI apresenta limitações concretas que a tornam inadequada como ferramenta principal de trabalho.

---

### O problema concreto da GUI para desenvolvedores

Considere esta situação: é necessário renomear 200 arquivos de imagem, trocando o prefixo `image_` por `photo_` em todos eles. Na GUI do Windows, isso exigiria clicar em cada arquivo individualmente, editar o nome, confirmar. 200 vezes.

Considere uma segunda situação: é necessário conectar a máquina a um serviço remoto para executar um comando. Esse serviço não possui tela, não possui mouse, não possui interface gráfica. A única forma de interagir com ele é enviando e recebendo textos.

Esses dois casos expõem limites fundamentais da GUI para quem desenvolve sistemas:

1. **Ausência de automação.** A GUI foi projetada para interação humana, um clique por vez. Não há mecanismo nativo para repetir uma sequência de ações de forma programática. Tudo que exige repetição se torna trabalho manual.

2. **Dependência de representação visual.** A GUI pressupõe que há uma tela, um cursor e um humano, mas em alguns serviços a única interface disponível é texto.

---

### A solução

A alternativa à GUI é a **CLI**, do inglês *Command Line Interface* (Interface de Linha de Comando).

Na CLI, não há clique. Um comando é enviado em texto, o sistema executa e retorna uma resposta também em texto.

A CLI pode parecer uma regressão à primeira vista — afinal, a GUI surgiu exatamente para substituir as interfaces de texto dos anos 80. Mas a CLI não é um passo atrás. Ela resolve precisamente os dois limites que a GUI não consegue superar:

1. **Automação.** Um comando escrito uma vez pode ser colocado dentro de um script e executado 200 vezes, 2000 vezes, no horário definido, em múltiplas máquinas simultaneamente. A CLI é, por natureza, programável.

2. **Acesso remoto.** Como tudo é texto, a CLI funciona em qualquer ambiente — inclusive em serviços sem interface gráfica. O ferramental inteiro do ecossistema de desenvolvimento foi construído sobre ela.

---

### Justificativa de adoção da CLI

Não se trata de preferência estética ou tradição, mas de capacidade operacional. As ferramentas utilizadas neste curso são operadas pela CLI. Elas não possuem GUI. A instalação, a configuração e o uso ocorrem escrevendo comandos em texto. Não há alternativa.

Além disso, todo o fluxo profissional de desenvolvimento acontece na linha de comando. Dominar a CLI não é um simples detalhe de configuração inicial — é uma habilidade central da profissão.

---

## Bloco 2 — Terminal e Shell

### Diferenciação conceitual

Ao abrir uma janela preta e digitar comandos, duas coisas distintas estão em operação simultaneamente. A maioria das pessoas trata como uma coisa só. Para trabalhar com desenvolvimento de forma precisa, é necessário distinguir as duas.

Essas duas coisas têm nomes: **terminal** e **shell**.

---

### Terminal

O terminal é a janela. É o componente visual que exibe texto na tela e captura o que é digitado. Ele não entende comandos — é um intermediário. Ele recebe os caracteres pressionados no teclado e os repassa para outra coisa; recebe o texto que essa outra coisa devolve e exibe na tela.

O terminal é, em essência, uma interface de exibição e entrada de texto. Somente isso.

No Windows, o programa que faz esse papel atualmente é o **Windows Terminal**. Ele é apenas a janela — a moldura visual. O que acontece dentro dela depende do shell que está sendo executado.

---

### Shell

O **shell** é o interpretador. É ele que lê o comando digitado, entende o que significa, executa a operação correspondente no sistema operacional e devolve o resultado.

Quando um comando é digitado, é o shell que interpreta, que identifica, que faz a chamada ao sistema operacional e que devolve o controle ao terminal após a execução. O terminal nunca soube o que estava acontecendo — ele apenas exibiu o que foi digitado e depois exibiu o que o shell devolveu.

---

### A distinção

A melhor forma de tornar essa distinção concreta é observar que o mesmo terminal pode executar shells diferentes. No Windows Terminal, é possível abrir abas com shells distintos: uma aba com PowerShell 7, outra com o PowerShell 5, outra com o Prompt de Comando. A janela é a mesma. O que muda é o interpretador — e com ele, a sintaxe dos comandos disponíveis.

Essa distinção tem uma consequência prática direta: quando um comando não funciona, o problema pode estar no shell errado, não no comando em si.

---

### Os shells nativos por sistema operacional

Cada sistema operacional tem seus shells padrão:

- Windows possui dois shells relevantes para desenvolvimento. O **PowerShell 5**, que vem pré-instalado e usa a extensão `.ps1` para scripts, é o shell legado — presente em todo Windows, mas com limitações que o tornaram obsoleto para desenvolvimento moderno. O **PowerShell 7** é o shell atual: multiplataforma, ativamente mantido pela Microsoft, com capacidades superiores. O Prompt de Comando — o `cmd.exe` — existe, mas não é utilizado em desenvolvimento moderno e não é abordado neste curso.

- macOS usa o **zsh** como shell padrão desde 2019, quando substituiu o **bash**. É o shell nativo de todos os Macs atuais.

- Linux usa tipicamente **bash** ou **zsh**, dependendo da distribuição. Ubuntu usa **bash** por padrão; algumas distribuições já adotam **zsh**.

A razão de mencionar os três sistemas aqui, mesmo que o ambiente de trabalho seja o Windows, é que ao longo do curso haverá leitura de documentação, tutoriais e mensagens de erro escritos para qualquer um dos três. Saber identificar para qual shell um comando foi escrito — e se ele se aplica ao ambiente em uso — é uma habilidade operacional necessária.

---

### Justificativa de adoção do PowerShell 7

O PowerShell 5 está presente em todo Windows e abre quando se pesquisa *"PowerShell"* no menu Iniciar sem qualificação. O PowerShell 7 precisa ser buscado pelo nome `pwsh` ou pelo nome completo *"PowerShell 7"*.

A distinção importa por duas razões concretas:

1. Alguns comandos têm comportamento diferente entre as versões — ou não existem em uma delas.

2. Ferramentas modernas de desenvolvimento testam compatibilidade com PowerShell 7, não com o 5.

Durante o curso, sempre que houver uma instrução para abrir o terminal, significa: abrir o Windows Terminal e garantir que a aba está executando PowerShell 7. O PowerShell 7 exibe `PS` seguido do caminho atual, e a versão pode ser confirmada a qualquer momento com o comando `pwsh --version`.

---

## Bloco 3 — Navegação pelo Sistema de Arquivos

### Contexto: sistema de arquivos via GUI

A navegação pelo sistema de arquivos é uma operação cotidiana — realizada pelo Windows Explorer. Pastas são vistas, acessadas com duplo clique, o retorno acontece pela seta, e o caminho completo aparece na barra de endereço no topo da janela.

A CLI executa exatamente as mesmas operações. A diferença é que, em vez de clicar, escrevem-se comandos. E em vez de ícones, vê-se texto. A estrutura de arquivos subjacente é idêntica — o mesmo diretório visível no Explorer é o que a CLI manipula.

---

### Diretório atual

Quando o shell está aberto, ele sempre está "dentro" de algum lugar do sistema de arquivos. Esse lugar é chamado de **diretório atual** — também referido como *working directory* (diretório de trabalho) em inglês.

Toda operação executada no shell acontece em relação ao diretório atual. A criação de uma pasta ocorre dentro do diretório atual. A listagem de arquivos retorna os arquivos do diretório atual.

O PowerShell 7 mostra o diretório atual diretamente no prompt, antes do cursor. O prompt exibe o seguinte formato:

```shell
PS C:\Users\directory>
```

O trecho `C:\Users\directory` é o diretório atual. Sempre que o prompt aparecer em uma demonstração, o caminho que precede `>` indica onde o shell está naquele momento.

Para exibir o diretório atual explicitamente como um comando — útil quando o prompt está configurado para não mostrar o caminho completo — usa-se:

```shell
pwd
```

**Finalidade.** `pwd` exibe o caminho completo do diretório onde o shell está posicionado no momento.

**Motivação.** Em ambientes onde o prompt foi personalizado e não mostra o caminho, ou em scripts que precisam registrar o diretório de trabalho, `pwd` é a forma programática de obter essa informação.

**Decisão.** `pwd` é um **alias** — um nome alternativo — para o cmdlet nativo do PowerShell `Get-Location`. O PowerShell 7 mantém `pwd` porque esse nome vem do Unix e é universal entre shells. Usar `pwd` em vez de `Get-Location` é idiomático e funciona no PowerShell, zsh e bash igualmente. No curso, usa-se `pwd`.

**Localização.** O comando é utilizado toda vez que for necessário confirmar onde o shell está antes de executar uma operação sensível à localização.

**Contrafactual.** Se omitido quando há dúvida sobre o diretório atual, comandos podem ser executados no lugar errado — criando arquivos onde não se deveria, deletando o conteúdo de uma pasta incorreta. É um hábito de segurança.

---

### Listagem de conteúdo

Para ver o que existe dentro do diretório atual, o comando é:

```shell
ls
```

**Finalidade.** `ls` lista todos os arquivos e diretórios presentes no diretório atual.

**Motivação.** Navegar pelo sistema de arquivos sem conseguir ver o conteúdo de onde o shell está seria operar às cegas. `ls` é o equivalente em CLI de abrir uma pasta no Windows Explorer e ver os itens dentro dela.

**Decisão.** `ls` é alias para o cmdlet nativo `Get-ChildItem`. O PowerShell 7 também aceita `dir`, que vem do Prompt de Comando legado. No curso usa-se `ls` pelo mesmo motivo de `pwd`: é o nome universal entre shells, presente no PowerShell, zsh e bash. Aprender o alias universal reduz o custo de transição entre ambientes.

**Localização.** O comando é utilizado toda vez que for necessário confirmar o conteúdo de um diretório antes de criar, mover ou deletar algo. Também é usado para verificar se uma operação anterior produziu o resultado esperado — por exemplo, após criar um arquivo, `ls` confirma que ele está lá.

**Contrafactual.** Sem `ls`, a operação ocorreria sem visibilidade do estado atual do diretório. Em desenvolvimento, isso leva a erros frequentes: criar arquivos duplicados, referenciar nomes incorretos, trabalhar no diretório errado sem perceber.

---

### Deslocamento entre diretórios

Para se mover de um diretório para outro, o comando é `cd`, do inglês *change directory* (mudar de diretório):

```shell
cd path
```

**Finalidade.** `cd` reposiciona o shell dentro do sistema de arquivos, tornando o diretório de destino o novo diretório atual. Todas as operações subsequentes passam a acontecer em relação ao novo local.

**Motivação.** O shell sempre está em algum lugar. `cd` é o mecanismo de locomoção — o equivalente ao duplo clique em uma pasta no Windows Explorer.

**Decisão.** `cd` é alias para o cmdlet `Set-Location`. É o comando de navegação universal — funciona com o mesmo nome no PowerShell, zsh e bash. No curso usa-se `cd` por essa razão.

**Localização.** O comando é utilizado toda vez que for necessário operar em um diretório diferente do atual. Em desenvolvimento, `cd` é usado dezenas de vezes por sessão de trabalho.

**Contrafactual.** Sem `cd`, o shell ficaria preso no diretório onde abriu. Toda operação em outro lugar exigiria especificar o caminho completo em cada comando — verboso, lento e sujeito a erro.

---

### Caminhos absolutos e relativos

Quando se escreve `cd path`, o que vai no lugar de `path` pode ser de dois tipos. Essa distinção é uma das mais importantes da operação em CLI.

**Caminho absoluto.** Começa da raiz do sistema de arquivos e descreve o trajeto completo até o destino, sem depender de onde o shell está no momento.

No Windows, a raiz é uma letra de unidade seguida de `:\`. Um caminho absoluto tem sempre essa forma:

```shell
C:\Users\directory
```

Independente de onde o shell estiver, `cd C:\Users\directory` leva exatamente para esse diretório. Sempre. O resultado é previsível porque o ponto de partida está fixo na raiz.

**Caminho relativo.** Descreve o trajeto a partir do diretório atual. Ele não começa com letra de unidade — começa diretamente com o nome do próximo passo.

Se o shell está em `C:\Users\directory` e o destino é `C:\Users\directory\project`, o caminho relativo é simplesmente:

```shell
project
```

Porque `project` existe dentro de onde o shell já está. O shell completa o trajeto juntando o diretório atual com o fragmento fornecido.

Há dois atalhos de caminho relativo que aparecem constantemente:

`.` — representa o diretório atual. `cd .` não move o shell a lugar nenhum. Mas `.` é usado em outros contextos para significar *"aqui"* — por exemplo, ao referenciar o diretório atual como destino de uma operação de cópia ou instalação.

`..` — representa o diretório pai, ou seja, um nível acima. Se o shell está em `C:\Users\directory\project`, então `cd ..` leva para `C:\Users\directory`.

**Por que a distinção importa.** Caminhos absolutos são seguros quando é necessária precisão independente do contexto — em scripts, por exemplo. Caminhos relativos são mais rápidos de digitar durante o trabalho interativo, mas dependem de saber onde o shell está. O hábito de confirmar o diretório atual com `pwd` antes de usar caminhos relativos elimina a principal fonte de erro.

---

### Diretório inicial

Todo usuário no Windows tem um diretório pessoal — o diretório inicial. No Windows, ele fica em `C:\Users\username`. É onde estão as pastas `Documents`, `Downloads`, `Desktop` e assim por diante.

No PowerShell 7, o atalho `~` representa o caminho completo do diretório inicial do usuário atual. Para ir diretamente para esse diretório de qualquer lugar do sistema de arquivos:

```shell
cd ~
```

**Finalidade.** `cd ~` leva o shell para o diretório inicial do usuário, independente de onde ele estiver no momento.

**Motivação.** O diretório inicial é o ponto de referência central do usuário no sistema. Em vez de digitar o caminho completo — que varia de usuário para usuário e de máquina para máquina — `~` é uma referência portável que funciona em qualquer ambiente.

**Decisão.** `~` é alias para a variável de ambiente `$HOME`. É o atalho de caminho universal — funciona com o mesmo nome no PowerShell, zsh e bash. No curso usa-se `~`.

**Localização.** O atalho é utilizado para retornar rapidamente ao ponto de partida e para referenciar o diretório inicial em scripts sem fixar o nome do usuário no código.

**Contrafactual.** Sem `~`, navegar de volta ao diretório pessoal exigiria digitar o caminho completo com o nome do usuário — o que quebra em scripts usados por pessoas diferentes ou em máquinas com nomes de usuário distintos.

---

## Bloco 4 — Manipulação de Arquivos e Diretórios

A localização no sistema de arquivos está estabelecida e a navegação entre diretórios está coberta. A seguir: criação, escrita e leitura — as operações realizadas centenas de vezes ao longo do curso.

### Criação de diretório

```shell
mkdir course
```

**Finalidade.** `mkdir` cria um novo diretório com o nome especificado dentro do diretório atual.

**Motivação.** Toda estrutura de projeto começa com a criação de diretórios. Em desenvolvimento, código e configurações são organizados em pastas separadas. `mkdir` é o mecanismo de CLI para essa operação.

**Decisão.** `mkdir` é alias para o cmdlet `New-Item -ItemType Directory`. O nome `mkdir` vem do Unix e é universal entre shells — funciona em PowerShell, zsh e bash com o mesmo nome. No curso usa-se `mkdir` por essa razão.

**Localização.** O comando é utilizado toda vez que for necessário criar uma nova pasta — ao iniciar um projeto, ao organizar subdiretórios, ao criar estruturas de pastas para demonstração.

**Contrafactual.** Sem `mkdir`, criar diretórios pela CLI exigiria o cmdlet completo `New-Item -ItemType Directory -Name course` — verboso e específico do PowerShell. O alias torna a operação rápida e portável.

---

### Criação de arquivo vazio

Entrar no diretório:

```shell
cd course
```

Criar um arquivo vazio:

```shell
New-Item -ItemType File -Name notes.txt
```

**Finalidade.** `New-Item -ItemType File -Name` cria um arquivo vazio com o nome especificado no diretório atual.

**Motivação.** Em desenvolvimento, é frequente a necessidade de criar arquivos antes de preenchê-los — um arquivo de configuração, um arquivo de código. `New-Item` é o cmdlet nativo do PowerShell para essa operação.

**Decisão.** No macOS e Linux, o comando equivalente é `touch notes.txt`. O PowerShell 7 não possui `touch` nativo. Essa é uma das divergências reais entre sistemas antecipadas no Bloco 2. Em tutoriais escritos para macOS ou Linux, `touch` aparecerá com frequência. No ambiente Windows, o equivalente é `New-Item -ItemType File -Name`.

**Localização.** O comando é utilizado para criar arquivos de configuração e arquivos de código inicialmente vazios — toda vez que o arquivo precisa existir antes de ser preenchido.

**Contrafactual.** Sem esse comando, não é possível criar um arquivo vazio pela CLI no PowerShell. A alternativa seria abrir um editor, criar o arquivo por lá e salvá-lo — o que quebra o fluxo de trabalho inteiramente em linha de comando.

---

### Escrita em arquivo

```shell
Add-Content notes.txt "First line of text."
```

**Finalidade.** `Add-Content` escreve o texto especificado dentro do arquivo indicado. Se o arquivo já tiver conteúdo, o texto é adicionado ao final — não substitui o que existe.

**Motivação.** Criar um arquivo vazio é apenas o primeiro passo. Em desenvolvimento, é frequente a necessidade de escrever conteúdo em arquivos diretamente pela CLI — configurações iniciais, conteúdo de demonstração — sem abrir um editor.

**Decisão.** No macOS e Linux, a operação equivalente usa redirecionamento: `echo "text" >> file`. O `>>` redireciona a saída do comando `echo` para o arquivo, anexando ao final. O PowerShell 7 também aceita essa sintaxe, mas o comportamento do `echo` no PowerShell tem particularidades de codificação que podem gerar caracteres inesperados em alguns contextos. `Add-Content` é o cmdlet nativo e se comporta de forma previsível. No curso usa-se `Add-Content` no Windows por essa razão.

**Localização.** O comando é utilizado para criar conteúdo inicial em arquivos de configuração, para adicionar linhas a arquivos de log em scripts, para qualquer situação em que seja necessário escrever em arquivo sem abrir um editor.

**Contrafactual.** Sem `Add-Content`, escrever em arquivo pela CLI exigiria abrir um editor, navegar até o arquivo, digitar o conteúdo e salvar — quebrando o fluxo de trabalho em linha de comando. Em scripts automatizados, abrir um editor é impossível.

---

### Exibição de conteúdo de arquivo

```shell
cat notes.txt
```

**Finalidade.** `cat` lê o conteúdo do arquivo especificado e o exibe na tela, linha por linha.

**Motivação.** Após escrever em um arquivo, é necessário verificar o que está lá. Em desenvolvimento, arquivos de configuração e resultados de operações são lidos com frequência — tudo sem abrir um editor.

**Decisão.** `cat` é alias para o cmdlet nativo do PowerShell `Get-Content`. No curso usa-se `cat` porque é mais rápido de digitar e é o nome que aparece em toda documentação e tutorial do ecossistema.

**Localização.** O comando é utilizado para inspecionar arquivos de configuração e verificar o conteúdo de arquivos gerados — toda vez que for necessário ver o conteúdo de um arquivo sem abrir um editor.

**Contrafactual.** Sem `cat`, inspecionar um arquivo exigiria abrir um editor ou o Windows Explorer — operações que tiram do fluxo da CLI e interrompem sequências de comandos em scripts.

---

### Limpeza do que foi criado

```shell
cd ..
```

```shell
Remove-Item -Recurse -Force course
```

**Finalidade.** `Remove-Item -Recurse -Force` remove o diretório especificado e todo o seu conteúdo recursivamente — incluindo `notes.txt`.

**Motivação.** Ao trabalhar com demonstrações e experimentos em CLI, é necessário desfazer o que foi criado sem deixar resíduos no sistema de arquivos. `Remove-Item` é o cmdlet nativo do PowerShell para remoção de arquivos e diretórios.

**Decisão.** As flags `-Recurse` e `-Force` são necessárias em conjunto para remover diretórios com conteúdo. Sem `-Recurse`, o PowerShell recusa remover um diretório que tem conteúdo dentro. Sem `-Force`, o PowerShell solicita confirmação interativa para cada item. No macOS e Linux, o equivalente é `rm -rf course` — mais conciso, mas com o mesmo comportamento destrutivo e irreversível.

**Localização.** O comando é utilizado para limpar estruturas de diretório criadas em demonstrações, remover projetos descartados ou desfazer experimentos de forma completa e não interativa.

**Contrafactual.** Sem `-Recurse` e `-Force`, o comando falharia com erro de diretório não vazio, ou exigiria confirmação manual para cada arquivo — impraticável em diretórios com muitos itens.

---

### Limpeza da tela

```shell
clear
```

**Finalidade.** `clear` limpa todo o texto exibido na janela do terminal, deixando apenas o prompt vazio no topo.

**Motivação.** Após muitos comandos, a tela acumula saída e fica difícil de ler. `clear` reseta a visualização sem encerrar o shell nem alterar nenhum estado — o diretório atual, as variáveis e o histórico de comandos permanecem intactos.

**Decisão.** `clear` é alias para o cmdlet nativo do PowerShell `Clear-Host`. O nome `clear` vem do Unix e é universal entre shells — funciona em PowerShell, zsh e bash com o mesmo nome. No curso usa-se `clear` por essa razão.

**Localização.** O comando é utilizado durante sessões longas de trabalho, quando a saída acumulada dificulta a leitura; antes de demonstrações em que se quer exibir apenas o resultado do próximo comando; em scripts que produzem saída estruturada e precisam de tela limpa como ponto de partida.

**Contrafactual.** Sem `clear`, a única alternativa seria fechar o terminal e abrir um novo — o que encerraria a sessão atual, perdendo o histórico de comandos e exigindo navegar novamente até o diretório de trabalho.
