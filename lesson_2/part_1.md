# Parte 1

## Bloco 1 — O Problema do Versionamento Manual

O versionamento manual ocorre quando versões de um arquivo são salvas de forma manual — seja renomeando, seja copiando para pastas diferentes. É a solução mais imediata disponível, e a que a maioria das pessoas adota antes de conhecer uma alternativa.

O problema do versionamento manual tem quatro dimensões:

1. **Identidade**. O nome do arquivo é a única fonte de identidade da versão. Nome de arquivo é texto livre — não há contrato sobre o que `v2` significa em relação a `v1`, ou o que `REVISADO` significa em relação a `final`. Dois arquivos chamados `relatorio-final.docx` em pastas diferentes podem conter conteúdos completamente distintos.

2. **Diferença**. Para saber o que mudou entre duas versões, é necessário abrir os dois arquivos e comparar manualmente. Em documentos curtos isso é incômodo. Em arquivos de código com centenas de linhas, é inviável.

3. **Motivo**. O arquivo não carrega nenhuma informação sobre por que aquela versão existe. Alguém corrigiu um problema? Adicionou uma funcionalidade? Reverteu algo que não funcionou? Essa informação se perde.

4. **Autoria e tempo**. Se mais de uma pessoa trabalha no mesmo projeto, não há como saber quem fez o quê. E mesmo em trabalho individual, a data de criação do arquivo não sobrevive a uma cópia ou a uma sincronização via pen drive.

O versionamento manual não é uma solução ruim porque a pessoa é descuidada; é uma solução ruim porque o problema exige uma ferramenta que ele não é.

A ferramenta que a indústria de sistemas criou para resolver esse problema foi o **Git**.

---

## Bloco 2 — Git

### A origem

O Git foi criado em 2005 por Linus Torvalds — o mesmo engenheiro que criou o kernel Linux. O contexto importa: o kernel Linux é um dos projetos de software colaborativo mais complexos do mundo, com milhares de contribuidores ao redor do planeta trabalhando simultaneamente no mesmo código. A ferramenta que eles usavam até então foi revogada por questões de licenciamento, e nenhuma das alternativas disponíveis atendia às exigências de escala e velocidade do projeto. Torvalds escreveu o Git em algumas semanas para resolver o próprio problema.

Esse contexto explica uma característica central do Git: ele foi projetado para funcionar sem depender de um servidor central. Cada desenvolvedor tem uma cópia completa do histórico na própria máquina. Isso é o que a palavra "distribuído" significa em "controle de versão distribuído" — não existe um único ponto de verdade que todos precisam acessar para trabalhar. É possível criar versões, navegar pelo histórico, criar ramificações e reverter alterações completamente offline, sem internet, sem depender de ninguém.

Isso contrasta com modelos mais antigos, nos quais o histórico ficava num servidor central e os desenvolvedores precisavam se conectar a ele para qualquer operação de versionamento.

---

### O que o Git resolve

O Git resolve as quatro limitações identificadas:

- **Identidade**: cada ponto salvo no histórico tem um identificador único gerado automaticamente — não é um nome de arquivo inventado pelo desenvolvedor.

- **Diferença**: o Git registra exatamente o que mudou entre quaisquer dois pontos do histórico, linha a linha.

- **Motivo**: cada ponto salvo carrega uma mensagem escrita pelo desenvolvedor explicando o que aquela mudança representa.

- **Autoria e tempo**: cada ponto registra quem fez a alteração e quando, de forma automática.

---

### Distinção necessária

Nesta parte, o trabalho é feito exclusivamente com o Git — uma ferramenta que roda localmente, sem internet, sem conta. O histórico existe na máquina.

Na parte seguinte, será apresentado o **GitHub** — uma plataforma na internet que hospeda remotamente projetos versionados com Git. GitHub não é Git. Git é a ferramenta; GitHub é um dos serviços que a usa. Essa distinção será importante quando desenvolvedores usarem os dois nomes de forma intercambiável — eles não são a mesma coisa.

---

## Bloco 3 — Configuração Inicial e Inicialização

Antes de utilizar o Git, é necessário fazer duas coisas: verificar se ele está instalado e configurar a identidade do autor. A seguir, cada uma dessas etapas.

---

### Verificação da instalação

Abra o terminal e execute:

```shell
git --version
```

**Finalidade**. Esse comando consulta o Git para obter a versão instalada.

**Motivação**. Antes de qualquer configuração ou uso, é necessário confirmar que o Git existe no sistema. Se o comando não for reconhecido, o shell responderá com um erro indicando que `git` não é um comando conhecido — o que significa que o Git não está instalado.

**Decisão**. `--version` é uma flag universalmente adotada em ferramentas de linha de comando para retornar a versão instalada. O padrão é o mesmo de `pwsh --version`, executado na Aula 1.

**Localização**. Esse comando é executado uma vez, neste momento, para verificação. Não altera nada no sistema.

**Contrafactual**. Se o Git não estiver instalado, nenhum dos comandos desta aula funcionará. O terminal retornará algo como `git is not recognized as an internal or external command`. Nesse caso, a instalação precisa ser feita antes de continuar — o Git é baixado em https://git-scm.com.

---

### Necessidade de identificação do autor

Cada ponto salvo no histórico do Git registra automaticamente o nome e o e-mail de quem o criou. Isso não é opcional. O Git recusa-se a criar um registro sem conhecer a identidade do autor.

Essa informação não serve apenas para projetos em equipe. Mesmo em trabalho individual, ela compõe o registro permanente do histórico. E quando o projeto local for conectado ao GitHub na parte seguinte, o GitHub usará esse e-mail para associar os commits à conta correspondente.

A configuração é feita uma única vez, globalmente — válida para todos os projetos da máquina.

---

### Os três comandos de configuração

#### Comando 1:

```shell
git config --global user.name 'Your Name'
```

**Finalidade**. Define o nome que aparecerá em cada registro criado.

**Motivação**. O Git precisa de uma identidade de autor para registrar no histórico. Sem ela, a tentativa de criar um registro resulta em erro.

**Decisão**. `git config` é o comando de configuração do Git. A flag `--global` instrui o Git a gravar essa configuração no arquivo de configuração global do usuário — localizado em `C:\Users\username\.gitconfig` no Windows. Isso significa que a configuração vale para todos os projetos na máquina. O parâmetro `user.name` é a chave que o Git usa para identificar o nome do autor.

**Localização**. Essa configuração é lida automaticamente pelo Git toda vez que um registro é criado, em qualquer projeto da máquina.

**Contrafactual**. Se `--global` for omitido dentro de um projeto, a configuração valerá apenas para aquele projeto — o que exige repetir a configuração em cada novo projeto criado.

---

#### Comando 2:

```shell
git config --global user.email 'your@email.com'
```

**Finalidade**. Define o e-mail que aparecerá em cada registro criado.

**Motivação**. Junto com o nome, o e-mail compõe a identidade completa do autor no histórico. Na parte 2 desta aula, o GitHub usará esse e-mail para vincular os registros à conta — se o e-mail aqui não for o mesmo cadastrado no GitHub, os registros aparecerão como de um autor desconhecido na plataforma.

**Decisão**. Mesma lógica do comando anterior. `user.email` é a chave correspondente ao e-mail do autor no arquivo de configuração global.

**Localização**. Essa configuração é lida automaticamente pelo Git toda vez que um registro é criado, em qualquer projeto da máquina.

**Contrafactual**. Se `--global` for omitido dentro de um projeto, a configuração valerá apenas para aquele projeto — o que exige repetir a configuração em cada novo projeto criado. Um e-mail incorreto aqui gerará inconsistência visível no GitHub na aula seguinte.

---

```shell
git config --global init.defaultBranch main
```

Esse comando tem uma motivação específica que merece explicação própria — apresentada a seguir. Por ora, registre que ele também faz parte da configuração global inicial e deve ser executado junto com os dois anteriores.

---

A configuração gravada pode ser confirmada executando:

```shell
git config --global --list
```

**Finalidade**. Exibe todas as configurações globais gravadas no arquivo `.gitconfig` do usuário.

**Motivação**. Como os três comandos anteriores não produziram saída, essa é a forma de verificar que funcionaram.

**Decisão**. A flag `--list` instrui o `git config` a exibir o conteúdo atual da configuração em vez de gravar algo. Combinada com `--global`, restringe a exibição à configuração global.

**Localização**. Comando de inspeção — não altera nada. Útil sempre que for necessário confirmar o estado da configuração.

**Contrafactual**. Sem esse passo de verificação, um erro de digitação no nome ou no e-mail só seria descoberto no momento de criar o primeiro registro.

---

## Bloco 4 — Configuração da Branch Padrão

O comando `git config --global init.defaultBranch main` foi executado sem que o conceito de *branch* tivesse sido explicado. Esse conceito será desenvolvido integralmente no Bloco 8 desta parte. Por ora, o necessário é entender por que esse comando existe e por que faz parte da configuração inicial.

---

### O problema

Quando o Git foi criado em 2005, ele chamava a linha principal do histórico de registro de `master`. Esse nome era o padrão automático em todo projeto. Durante quinze anos, toda a indústria usou `master` sem questionar.

Em outubro de 2020, o GitHub — que naquela altura já era a plataforma dominante de hospedagem de projetos — mudou seu padrão de `master` para `main`. A motivação foi remover uma terminologia com conotação histórica negativa. A partir desse ponto, projetos no GitHub passaram a usar `main` como nome padrão.

O Git em si, porém, é uma ferramenta independente do GitHub. O instalador do Git para Windows não muda automaticamente o padrão local para acompanhar a decisão do GitHub. Isso cria uma inconsistência. Quando os dois forem conectados, o Git encontrará dois nomes diferentes e a sincronização falhará.

---

### O que o comando faz

```shell
git config --global init.defaultBranch main
```

**Finalidade**. Instrui o Git a usar `main` como nome da linha principal em todo projeto novo.

**Motivação**. Eliminar a inconsistência entre o padrão local e o padrão do remoto.

**Decisão**. A chave `init.defaultBranch` foi introduzida no Git 2.28, lançado em 2020, exatamente para permitir essa configuração. Versões anteriores não tinham essa chave — o nome `master` era fixo no código. Por isso a versão mínima do Git neste curso é 2.50: ferramentas modernas precisam de versões que suportem convenções modernas.

**Localização**. Essa configuração é lida pelo Git no momento em que o versionamento é inicializado. Não afeta projetos já existentes — apenas os que serão criados a partir de agora.

**Contrafactual**. Sem esse comando, o Git criará uma linha principal chamada `master`.

---

## Bloco 5 — Inicialização

### O que é um repositório

Um repositório Git é uma pasta comum do sistema de arquivos com uma diferença: ela contém uma subpasta oculta chamada `.git`. É nessa subpasta que o Git armazena todo o histórico do projeto — cada registro salvo, cada informação de autoria. Os arquivos de trabalho ficam na pasta normal, visível. O histórico fica dentro de `.git`, gerenciado exclusivamente pelo Git.

A pasta do projeto é a mesa de trabalho. A subpasta `.git` é um arquivo morto embutido na mesa, onde o Git guarda fotografias do estado da mesa em cada momento em que foi solicitado o registro.

O conteúdo de `.git` nunca é editado manualmente. Tudo que entra nela passa pelos comandos do Git.

---

### Criando um repositório

Execute os comandos abaixo no terminal, um por vez:

---

```shell
cd ~
```

**Finalidade**. Navega para o diretório inicial do usuário — o ponto de partida padrão para projetos pessoais.

**Motivação**. Garante um ponto de partida conhecido antes de criar qualquer estrutura de diretórios, independentemente de onde o terminal esteja aberto.

**Decisão**. `~` é o atalho universal para o diretório inicial do usuário atual. No Windows com PowerShell, equivale a `C:\Users\username`. Usar `~` em vez do caminho completo torna o comando portável entre usuários e sistemas.

**Localização**. Executado no início de qualquer sessão em que seja necessário criar ou acessar estruturas de projeto a partir de uma posição conhecida no sistema de arquivos.

**Contrafactual**. Se omitido, o diretório de trabalho seria criado onde quer que o terminal estivesse no momento — possivelmente em um local inesperado.

---

```shell
mkdir course
```

**Finalidade**. `mkdir` cria um novo diretório com o nome especificado dentro do diretório atual.

**Motivação**. O repositório Git precisa de uma pasta para existir. A pasta é criada antes de o repositório ser inicializado dentro dela.

**Decisão**. O nome `course` é descritivo e deixa claro o propósito da pasta. A ausência de espaços é intencional — espaços em nomes de pasta exigem aspas nos comandos e introduzem fricção desnecessária.

**Localização**. Essa pasta será o repositório de treino desta aula, criada exclusivamente para fins de prática.

**Contrafactual**. Se a pasta já existir, o `mkdir` retornará um erro informando isso. Não é um problema grave — é possível navegar para a pasta existente com `cd course` e continuar.

---

```shell
cd course
```

**Finalidade**. Posiciona o terminal dentro do diretório de trabalho da aula.

**Motivação**. O comando de inicialização do Git age sobre o diretório atual. É necessário estar dentro da pasta que se quer transformar em repositório.

**Decisão**. `cd` seguido do nome da pasta é o comando de navegação praticado na Aula 1. A familiaridade é intencional.

**Localização**. Após esse comando, todos os comandos Git executados neste terminal operarão sobre essa pasta.

**Contrafactual**. Se o comando de inicialização for executado no diretório errado — por exemplo, no diretório inicial em vez de dentro da pasta de treino — um repositório Git será inicializado na raiz do diretório pessoal, transformando-o inteiro em um repositório. Isso não é catastrófico, mas é confuso e exige desfazimento manual.

---

```shell
git init
```

**Finalidade**. Inicializa um repositório Git na pasta atual, criando a subpasta oculta `.git`.

**Motivação**. Sem esse comando, a pasta `course` é apenas uma pasta comum. O Git não rastreia nada dentro de pastas que não foram inicializadas como repositórios.

**Decisão**. `init` vem de *initialize* — inicializar. É o ponto zero de qualquer repositório Git local. Esse comando é executado exatamente uma vez por repositório, no momento da criação.

**Localização**. Após `git init`, todos os outros comandos Git passam a funcionar dentro dessa pasta. O Git começa a monitorar alterações a partir deste momento.

**Contrafactual**. Se um comando Git for executado em uma pasta não inicializada, o Git retorna um erro informando que não está dentro de um repositório: `fatal: not a git repository`.

---

Para confirmar que a subpasta `.git` existe, execute:

```shell
ls -Force
```

**Finalidade**. Lista o conteúdo do diretório atual incluindo itens ocultos.

**Motivação**. A pasta `.git` é oculta por padrão no Windows — o explorador de arquivos não a exibe, e o `ls` simples também não. A flag `-Force` instrui o PowerShell a exibir todos os itens, incluindo os ocultos.

**Decisão**. No Windows, arquivos e pastas cujo nome começa com ponto não são automaticamente ocultos — o que os torna ocultos é um atributo do sistema de arquivos definido pelo Git no momento da criação. A flag `-Force` ignora esse atributo e exibe tudo. No macOS e Linux, `ls -a` cumpre a mesma função por uma razão diferente: lá, o ponto no início do nome é suficiente para tornar o item oculto.

**Localização**. Útil sempre que houver suspeita de arquivos ocultos em um diretório.

**Contrafactual**. Se apenas `ls` for executado sem `-Force`, a pasta `.git` não aparecerá na listagem. A conclusão errônea seria que o `git init` não funcionou.

---

## Bloco 5 — As Três Áreas do Git

Este é o modelo mental mais importante desta parte. Todos os comandos do Git fazem sentido a partir deste modelo. Sem ele, os comandos parecem arbitrários. Com ele, cada comando tem uma razão clara de existir.

---

### A analogia

Imagine um fotógrafo documentando o progresso de uma obra. Três espaços de trabalho estão disponíveis:

1. A obra em si — onde as coisas acontecem. Paredes sendo levantadas, pintura sendo aplicada, móveis sendo movidos. É o estado atual, bruto, em transformação contínua.

2. A mesa de seleção — onde são colocadas as fotos que entrarão no próximo relatório. Apenas os registros relevantes para aquele documento específico são selecionados. Nem tudo que aconteceu na obra precisa entrar no relatório — só o que for colocado nessa mesa.

3. O arquivo permanente — onde os relatórios finalizados são guardados para sempre, com data, assinatura e descrição. Uma vez arquivado, o relatório não muda. Qualquer relatório de qualquer data pode ser consultado.

O Git funciona exatamente assim, com três áreas correspondentes.

---

### As três áreas

#### Working directory

É a pasta do projeto no sistema de arquivos — no caso, a pasta `course`. É onde arquivos são criados, editados e apagados normalmente. O Git observa o que acontece aqui, mas não registra nada automaticamente. Tudo que existe no working directory é provisório até que uma decisão seja tomada sobre ele.

---

#### Staging area

É uma área intermediária, invisível como pasta, que existe dentro do `.git`. Quando uma alteração está pronta para ser registrada, ela é movida para a staging area. Ela funciona como uma lista de intenções: *"essas são as mudanças que quero incluir no próximo registro"*.

A staging area existe por uma razão precisa: nem sempre é desejável registrar tudo que foi alterado de uma vez. Imagine que um bug foi corrigido e, ao mesmo tempo, uma nova funcionalidade começou a ser escrita — as duas coisas estão no working directory. A staging area permite registrar apenas a correção do bug agora, deixando a funcionalidade incompleta de fora, para registrar depois quando estiver pronta.

---

#### Repository

É o histórico completo do projeto, armazenado dentro de `.git`. Cada registro permanente é chamado de **commit**. Um commit é uma fotografia do estado dos arquivos que estavam na staging area no momento em que foi registrado, acompanhada de uma mensagem descritiva, a identidade do autor e um timestamp.

---

### Os estados de um arquivo

Um arquivo dentro de um repositório Git sempre está em um dos seguintes estados:

**Untracked** — o arquivo existe no working directory, mas o Git nunca foi instruído a rastreá-lo. É um arquivo novo que o Git conhece mas ignora deliberadamente até ser orientado o contrário.

**Staged** — o arquivo foi movido para a staging area e está pronto para ser registrado.

**Committed** — o arquivo está registrado no histórico. O conteúdo em disco é idêntico ao conteúdo do último registro. Nenhuma alteração pendente.

**Modified** — o arquivo já foi rastreado pelo Git em algum registro anterior e, desde então, foi alterado no working directory. O Git percebe a diferença entre o que está em disco e o que está registrado no histórico.

---

### O fluxo

O caminho que um arquivo percorre é sempre nessa direção:

```
Working directory (untracked/modified) → Staging area (staged) → Repository (committed)
```

Etapas não são puladas. Um arquivo não vai do working directory direto para o repository sem passar pela staging area. Essa obrigatoriedade existe porque a staging area é onde o controle sobre o que entra em cada registro é exercido — ela é o mecanismo de precisão do Git.

---

## Bloco 6 — Ciclo Básico

### Criando o primeiro arquivo

```shell
New-Item -ItemType File -Name notes.txt
```

**Finalidade**. Cria um arquivo vazio chamado `notes.txt` no diretório atual.

**Motivação**. O repositório precisa de um arquivo para que os estados do Git possam ser observados. Um repositório sem arquivos não tem nada para rastrear.

**Decisão**. `New-Item -ItemType File -Name` é o comando nativo do PowerShell para criar arquivos — apresentado na Aula 1. O Git não tem um comando para criar arquivos; criação de arquivos é responsabilidade do sistema operacional. O Git apenas observa o que acontece no working directory.

**Localização**. Esse arquivo representa qualquer arquivo de projeto — poderia ser um arquivo de código, um documento, qualquer coisa. O nome e a extensão não têm significado especial para o Git.

**Contrafactual**. Se determinados comandos forem executados em um repositório completamente vazio, sem nenhum arquivo, o Git indicará que não há nada para rastrear. O comportamento é válido, mas não permite observar os estados.

---

### Inspecionando o estado

```shell
git status
```

**Finalidade**. Exibe o estado atual do repositório — quais arquivos estão em qual área e em qual estado.

**Motivação**. Antes de qualquer ação, é necessário saber onde as coisas estão. O `git status` é o comando de orientação — ele responde à pergunta *"o que está acontecendo agora neste repositório?"*.

**Decisão**. `status` não altera nada. É um comando de leitura pura, executável quantas vezes for necessário sem efeito colateral. Por isso é o primeiro comando a executar em qualquer situação de dúvida.

**Localização**. O `git status` é usado constantemente — antes de adicionar arquivos à staging area, depois de adicionar, antes de criar um registro, depois de criar. É o comando de verificação universal do Git.

**Contrafactual**. Sem `git status`, o trabalho é feito às cegas. O risco é criar um registro com conteúdo diferente do pretendido.

---

### Movendo para a área de preparação

```shell
git add notes.txt
```

**Finalidade**. Move o arquivo `notes.txt` para a staging area, marcando-o como pronto para entrar no próximo registro.

**Motivação**. O Git não rastreia arquivos automaticamente. A decisão do que entra em cada registro é feita explicitamente. O `git add` é o mecanismo dessa decisão — é o ato de colocar algo na mesa de seleção.

**Decisão**. O comando aceita um nome de arquivo específico, como neste caso, ou um ponto — `git add .` — que adiciona tudo que está modificado ou untracked no diretório atual. Usar o nome específico é mais preciso; usar `.` é mais rápido quando se quer adicionar tudo. Neste momento o nome específico é usado para que a correspondência entre o comando e o arquivo seja explícita.

**Localização**. Executado sempre que alterações precisam ser preparadas para um registro. Pode ser executado múltiplas vezes antes de um registro — cada `git add` acrescenta mais itens à staging area.

**Contrafactual**. Se o comando de registro for executado sem que `git add` tenha sido feito antes, o Git responde `nothing to commit` — a staging area está vazia e não há nada para registrar. O registro não é criado.

---

### Registrando o histórico

```shell
git commit -m 'register notes.txt'
```

**Finalidade**. Cria um commit — um registro permanente no histórico — com o conteúdo que está na staging area neste momento.

**Motivação**. A staging area é temporária. Ela acumula intenções. O `git commit` é o ato de concretizar essas intenções em um registro imutável no histórico. Após o commit, o estado do arquivo está salvo permanentemente dentro de `.git`.

**Decisão**. A flag `-m` permite fornecer a mensagem do commit diretamente na linha de comando, entre aspas. Sem `-m`, o Git abre o editor de texto padrão do sistema para que a mensagem seja digitada. A mensagem *"register notes.txt"* descreve o que esta mudança representa. Mensagens de commit são escritas no infinitivo — *"adicionar"*, *"corrigir"*, *"remover"* — porque descrevem o que o commit fará ao ser aplicado, não o que foi feito.

**Localização**. Executado sempre que um conjunto coerente de alterações está pronto para ser registrado. A granularidade correta é um commit por unidade lógica de mudança — não um commit por arquivo alterado, não um commit por dia de trabalho.

**Contrafactual**. Sem a flag `-m`, o Git abre o editor padrão. Se o editor for o Vim — comum em instalações do Git para Windows — o terminal parece travar porque o Vim tem modos de operação não intuitivos.

---

### Inspecionando o histórico

```shell
git log
```

**Finalidade**. Exibe o histórico de commits do repositório em ordem cronológica inversa — o mais recente aparece primeiro.

**Motivação**. O histórico é o produto central do Git. O `git log` é a forma de consultá-lo — ver o que foi registrado, quando, por quem e com qual mensagem.

**Decisão**. `git log` sem flags exibe o formato completo: identificador, autor, data e mensagem. Para históricos longos existe `git log --oneline`, que comprime cada commit em uma única linha. O formato completo é mais informativo; o compacto é mais navegável.

**Localização**. Executado sempre que o histórico precisa ser consultado — para entender o que foi feito, para encontrar um commit específico, para verificar se o último commit foi criado corretamente.

**Contrafactual**. Sem `git log`, não há visibilidade sobre o histórico. Sabe-se que commits existem, mas não é possível inspecioná-los. É como ter um arquivo morto trancado sem chave.

---

Agora, adicione conteúdo ao arquivo para observar o estado modified. Execute:

```shell
Add-Content notes.txt 'First line of text.'
```

**Finalidade**. Escreve o texto `First line of text.` dentro do arquivo `notes.txt`.

**Motivação**. O arquivo estava vazio no commit anterior. Para observar o estado modified, é necessário alterar um arquivo que o Git já rastreia — ou seja, um arquivo que já apareceu em algum commit.

**Decisão**. `Add-Content` é o comando do PowerShell para escrever conteúdo em arquivo — apresentado na Aula 1. O Git não tem comando para editar arquivos; edição é responsabilidade do sistema operacional ou do editor. O Git apenas detecta que o arquivo mudou.

**Localização**. Em projetos reais, arquivos são editados no VSCode. Aqui o `Add-Content` é usado para manter tudo no terminal e tornar a sequência de comandos contínua e observável.

**Contrafactual**. Se `git status` for executado sem que nenhum arquivo tenha sido alterado após o commit, o Git responderá `nothing to commit, working tree clean` — o working directory está idêntico ao último commit e não há nada a registrar.

---

### Inspecionando diferenças

```shell
git diff
```

**Finalidade**. Exibe as diferenças entre o working directory e o último commit — ou seja, o que foi alterado mas ainda não está na staging area.

**Motivação**. Saber que um arquivo está modified é útil, mas não suficiente. O `git diff` responde à pergunta mais precisa: o que exatamente mudou? Linha por linha, adição por adição, remoção por remoção.

**Decisão**. `git diff` sem flags compara o working directory com o último commit, mostrando apenas o que ainda não foi adicionado à staging area. Existe uma variação — `git diff --staged` — que compara a staging area com o último commit, mostrando o que já foi adicionado e está pronto para entrar no próximo commit. Os dois comandos cobrem momentos diferentes do fluxo e ambos serão usados nesta aula.

**Localização**. Executado antes do `git add` para revisar o que está prestes a ser estagiado, e antes do `git commit` para confirmar o que está na staging area. É o comando de revisão do fluxo.

**Contrafactual**. Sem `git diff`, alterações são adicionadas e registradas sem revisão. Em projetos reais isso leva a registros com conteúdo indesejado.

---

## Bloco 7 — Arquivo `.gitignore`

### O problema

Nem todo arquivo que existe na pasta do projeto deve entrar no histórico do Git. Existem três categorias de arquivos que não pertencem ao repositório:

**Arquivos temporários do sistema operacional**. O Windows cria automaticamente um arquivo chamado `Thumbs.db` em pastas que contêm imagens. O macOS cria `.DS_Store` em todo diretório aberto no Finder. Esses arquivos não têm nenhuma relação com o projeto — são resíduos do sistema operacional.

**Diretórios de dependências**. Em projetos futuros do curso, serão instalados conteúdos de códigos externos. Esses conteúdos ficam numa pasta dentro do projeto e podem conter milhares de arquivos. Não pertencem ao histórico porque qualquer pessoa, ao fazer uma cópia do repositório, pode reinstalá-los com um único comando — carregá-los no Git seria desperdício de espaço e tornaria o repositório lento.

**Arquivos com credenciais**. Senhas, chaves, tokens. Esses arquivos jamais devem entrar no histórico — um repositório público com credenciais expostas é uma vulnerabilidade de segurança grave, e remover um arquivo do histórico do Git após ele ter sido commitado é um processo trabalhoso.

O `.gitignore` é o mecanismo que instrui o Git a ignorar arquivos e pastas específicos — eles continuam existindo no working directory, mas o Git se comporta como se não os enxergasse.

---

### Criando o arquivo

```shell
New-Item -ItemType File -Name .gitignore
```

**Finalidade**. Cria o arquivo `.gitignore` no diretório raiz do repositório.

**Motivação**. O `.gitignore` precisa existir como arquivo antes de receber conteúdo. O Git o reconhece pelo nome exato — `.gitignore` — sem extensão adicional.

**Decisão**. O ponto no início do nome não tem significado especial no Windows como tem no macOS e Linux — no Windows, o que torna o arquivo oculto é um atributo do sistema de arquivos, não o ponto. O Git reconhece o nome `.gitignore` por convenção, não por causa do ponto.

**Localização**. O `.gitignore` na raiz do repositório vale para todo o projeto. Pode ser registrado no histórico — é parte da configuração do projeto, não um arquivo temporário.

**Contrafactual**. Sem o `.gitignore`, todo arquivo que o Git encontrar no working directory aparecerá como untracked no `git status`. Em projetos reais, isso polui a saída do `git status` com dezenas de arquivos irrelevantes e aumenta o risco de registrar algo que não deveria.

---

Abrindo o `.gitignore` no Bloco de Notas:

```shell
notepad .gitignore
```

**Finalidade**. Abre o arquivo `.gitignore` no Bloco de Notas para edição.

**Motivação**. O conteúdo do `.gitignore` é texto — padrões que o Git usará para filtrar arquivos. Editar no Bloco de Notas é mais confortável do que via terminal para um arquivo com múltiplas linhas.

**Decisão**. `notepad` seguido de um nome de arquivo abre aquele arquivo específico no Bloco de Notas.

**Localização**. Após esse comando, o Bloco de Notas abrirá o arquivo. O terminal continua disponível — `notepad` não bloqueia o terminal.

**Contrafactual**. Sem abrir o arquivo para edição, ele permanece vazio e não ignora nada.

---

Adicionando o conteúdo a ser ignorado:

```text
Thumbs.db
.DS_Store
*.log
```

`Thumbs.db` e `.DS_Store` — nomes exatos dos arquivos. O Git ignorará qualquer arquivo com esses nomes exatos em qualquer lugar do repositório.

`*.log` — padrão com curinga. O asterisco `*` representa qualquer sequência de caracteres. Isso instrui o Git a ignorar todo arquivo cuja extensão seja `.log`, independentemente do nome.

---

## Bloco 8 — Branches

### A analogia

Imagine a escrita de um livro. O manuscrito principal está num caderno. Em determinado momento, surge a necessidade de experimentar uma versão alternativa de um capítulo — mas sem alterar o manuscrito principal enquanto a experiência não estiver concluída e aprovada.

Um caderno novo é tomado, o estado atual do manuscrito é copiado nele, e a versão alternativa começa a ser escrita no caderno novo. O caderno original permanece intacto. Se a experiência funcionar, as alterações são transferidas para o original. Se não funcionar, o caderno novo é descartado sem que o principal tenha sido tocado.

No Git, cada caderno é uma **branch** — uma linha do tempo independente do projeto.

---

### O que é uma branch

Uma branch é um ponteiro para um commit. Nada mais do que isso.

Quando uma branch nova é criada, o Git não copia todos os arquivos do projeto — ele apenas cria um novo ponteiro apontando para o mesmo commit em que o trabalho está no momento. A partir daí, os commits criados nessa branch avançam o ponteiro dela sem afetar o ponteiro da branch original.

Isso tem uma consequência importante: branches no Git são baratas. Criar uma branch é uma operação instantânea que ocupa pouquíssimo espaço — é apenas um ponteiro, não uma cópia do projeto inteiro.

---

### Por que branches existem

O uso central de branches é isolar trabalho em progresso do estado estável do projeto. A branch `main` representa o estado consolidado — o que está funcionando, o que foi revisado, o que está pronto. Quando uma funcionalidade nova precisa ser adicionada ou algo precisa ser corrigido, cria-se uma branch separada, trabalha-se nela, e a integração de volta à `main` ocorre apenas quando o trabalho estiver concluído.

Isso protege a `main` de estados intermediários — código pela metade, experimentos que não funcionaram, alterações que precisam de revisão.

---

### Os comandos de branch

#### Listagem das branches existentes

```shell
git branch
```

**Finalidade**. Lista todas as branches existentes no repositório.

**Motivação**. Antes de criar uma branch nova, é útil saber quais já existem. Em repositórios com muitas branches, esse comando orienta o trabalho.

**Decisão**. `git branch` sem argumentos é um comando de leitura — não cria nem altera nada. O asterisco `*` na saída indica a branch atual.

**Localização**. Executado sempre que uma visão geral das branches do repositório for necessária.

**Contrafactual**. Sem saber quais branches existem, é possível criar uma branch com um nome que já existe — o Git retornaria um erro informando que a branch já existe.

---

#### Criação de nova branch

```shell
git switch -c new
```

**Finalidade**. Cria uma nova branch chamada `new` e imediatamente alterna para ela.

**Motivação**. Uma branch separada é necessária para trabalhar sem afetar a `main`. O `-c` combina duas operações em uma — criar e alternar — porque na prática sempre se quer estar na branch que acabou de ser criada.

**Decisão**. `-c` vem de *create*. Existe uma forma mais antiga de fazer a mesma coisa — `git checkout -b name` — mas `git switch` foi introduzido no Git 2.23 exatamente para separar as responsabilidades: `git switch` lida exclusivamente com alternância entre branches, enquanto `git checkout` acumulava múltiplas funções não relacionadas. O curso usa `git switch` porque é a forma moderna e semanticamente clara.

**Localização**. Executado sempre que um trabalho novo deve ser isolado da branch principal. Em projetos profissionais, é raro registrar diretamente na `main` — o fluxo padrão é criar uma branch, trabalhar nela, e integrar depois.

**Contrafactual**. Se `-c` for omitido e apenas `git switch new` for executado, o Git tentará alternar para uma branch chamada `new` já existente. Como ela não existe, retornará um erro: `fatal: invalid reference: new`.
