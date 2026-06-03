# Parte 2

## Bloco 1 — Git e GitHub

Existe uma confusão muito comum entre desenvolvedores iniciantes, e ela vale ser eliminada agora, antes de qualquer comando.

**Git** é uma ferramenta. Ela reside na máquina local. Quando foram executados comandos como `git init`, `git add` e `git commit` nas aulas anteriores, tudo aconteceu localmente — nada saiu do computador. O Git não sabe o que é internet. Ele rastreia o histórico de um diretório. Ponto.

**GitHub** é um site. É uma plataforma na internet que hospeda repositórios Git. Pense nele como um serviço de armazenamento em nuvem especializado em repositórios Git — da mesma forma que o Google Drive armazena arquivos comuns, o GitHub armazena repositórios com todo o seu histórico de commits, branches e metadados.

A relação entre os dois é a seguinte: o Git é o mecanismo; o GitHub é um dos lugares onde esse mecanismo pode guardar uma cópia remota do trabalho. Outros serviços existem — GitLab e Bitbucket — mas o GitHub é o padrão de mercado e é o que usaremos em todo o curso.

Três finalidades justificam a existência do GitHub no fluxo de trabalho de um desenvolvedor:

**Backup**. O repositório local é vulnerável: falha de hardware, formatação acidental, roubo do equipamento. Uma cópia remota no GitHub elimina esse risco. O histórico completo existe em dois lugares independentes.

**Colaboração**. Em um time, várias pessoas trabalham no mesmo projeto. O GitHub é o ponto de encontro: cada desenvolvedor envia seu trabalho para lá e obtém o trabalho dos colegas de lá. Sem um repositório remoto compartilhado, a sincronização entre máquinas seria manual e propensa a erro.

**Portfólio**. Repositórios públicos no GitHub são visíveis para qualquer pessoa na internet. Recrutadores e empresas verificam o GitHub de candidatos como parte do processo seletivo. Os projetos construídos neste curso viverão em repositórios públicos no GitHub e comporão o portfólio profissional do desenvolvedor.

---

## Bloco 2 — Conta e Repositório Remoto

O uso do GitHub requer uma conta. O processo é direto.

Acesse **github.com** no navegador e crie uma conta — nome de usuário, e-mail e senha. O nome de usuário é público e aparecerá nas URLs dos repositórios e nos commits visíveis a outros. É recomendável escolher algo profissional; ele acompanhará o portfólio.

Após criar a conta e fazer login, o painel do GitHub estará disponível.

---

### Criação do repositório remoto

No GitHub, clique no ícone **+** no canto superior direito, depois em ***New repository***. Um formulário com algumas configurações será exibido. Cada uma delas importa:

***Repository name***. O nome do repositório remoto. Por convenção, usa-se letras minúsculas e hífens no lugar de espaços — por exemplo, `course`. Esse nome aparecerá na URL do repositório.

***Choose visibility***. **Public ou Private**. Um repositório público é visível para qualquer pessoa na internet, sem autenticação. Um repositório privado é visível apenas para o proprietário e para quem for convidado explicitamente. Para os repositórios de exemplos desta aula, usaremos **Public** — não há nada sensível e é o padrão do curso.

Há três opções logo em seguida que merecem atenção:

- *Add README* — deixe **Off** por enquanto.
- *Add .gitignore* — deixe marcado com **No .gitignore**.
- *Add license* — deixe marcado com **No license**.

Por que deixar tudo desmarcado? Porque já existe um repositório local com commits. Se o GitHub criar arquivos nesse repositório remoto antes de conectar o local, os dois repositórios terão históricos diferentes desde o início — o remoto terá commits que o local não tem. Isso gera uma divergência que exige um passo extra para resolver. Deixando o repositório remoto completamente vazio, a conexão é direta e sem conflito.

Clique em **Create repository**. O GitHub criará o repositório e exibirá uma página com instruções. Essa página é útil — ela mostra a URL do repositório e os comandos para conectá-lo a um repositório local. Ela será utilizada em breve.

---

## Bloco 3 — Personal Access Token

Quando o Git tenta se comunicar com o GitHub — para enviar ou receber atualizações — o GitHub precisa verificar a identidade de quem faz a requisição. É necessária uma prova de identidade.

Durante muitos anos, essa prova era simples: usuário e senha da conta do GitHub. Em agosto de 2021, o GitHub descontinuou essa forma de autenticação para operações via Git. O motivo é segurança: uma senha é um segredo único que abre tudo. Se vazar, toda a conta está comprometida. Um token é um segredo específico, com permissões limitadas e que pode ser revogado a qualquer momento sem afetar a senha principal.

O mecanismo que substituiu a senha é o **Personal Access Token** — em português, *Ficha de Acesso Pessoal*. É uma sequência de caracteres gerada pelo GitHub que funciona como uma senha de uso específico. As permissões e o prazo de validade são definidos no momento da geração.

---

### Geração do token

No GitHub, siga este caminho:

1. Clique na foto do perfil no canto superior direito
2. ***Settings*** (Configurações)
3. No menu lateral esquerdo, desça até o final e clique em ***Developer settings***
4. ***Personal access tokens*** → ***Tokens (classic)***
5. ***Generate new token*** → ***Generate new token (classic)***

Um formulário com três campos relevantes será exibido:

***Note***. Um nome descritivo para o token — algo como `fullstack-course`. Serve apenas para identificar a finalidade do token. Não afeta o funcionamento.

***Expiration***. O prazo de validade do token. Após esse prazo, o token para de funcionar e um novo precisará ser gerado. Para o curso, selecione ***No expiration*** — sem prazo de validade. Em ambientes profissionais reais, tokens têm prazo definido por política de segurança; no contexto de aprendizado, o prazo indeterminado evita interrupções.

***Select scopes***. Esta é a parte mais importante. O token só executa operações dentro das permissões definidas aqui. Marque a caixa ***repo*** — ela concede acesso completo a repositórios: criar, ler, escrever, deletar. É a permissão mínima necessária para as operações deste curso.

Clique em ***Generate token***.

---

**Atenção crítica ao que acontece a seguir**.

O GitHub exibirá o token uma única vez. Ele começa com `ghp_` seguido de uma sequência de caracteres. Após sair dessa página ou recarregá-la, o token nunca mais será exibido. O GitHub armazena apenas um hash do token, não o token em si — pelo mesmo motivo que sites não guardam senhas, apenas versões criptografadas delas.

Copie o token e guarde em um local seguro e acessível — um gerenciador de senhas ou um arquivo de texto em local privado. Se perdido, não há como recuperar: será necessário revogar o token atual e gerar um novo.

---

## Bloco 4 — Conexão entre repositório local e remoto

Há dois repositórios que ainda não se conhecem: o local, com commits, e o remoto, no GitHub, completamente vazio.

---

### O comando de conexão

```shell
git remote add origin YOUR_REPOSITORY_URL
```

Antes de executar, é necessária a URL do repositório. No GitHub, acesse o repositório `course` criado anteriormente. Em ***Quick setup***, certifique-se de que a opção HTTPS está selecionada — não SSH. Copie a URL exibida. Ela terá o formato `https://github.com/your-user/course.git`.

**Finalidade**. `git remote add origin YOUR_REPOSITORY_URL` é o comando que registra um repositório remoto na configuração do repositório local, associando um nome a um endereço. A partir desse registro, o Git local passa a conhecer a existência do repositório remoto.

**Motivação**. O Git opera exclusivamente no repositório local por padrão. Para que seja possível enviar ou receber commits por meio de um repositório remoto, o endereço desse repositório precisa estar registrado. Sem esse registro, os dois repositórios são invisíveis um para o outro.

**Decisão**. O nome `origin` poderia ser qualquer string, mas é a convenção universal do ecossistema Git. Ferramentas, documentações e outros desenvolvedores esperam encontrar `origin` como nome do remoto principal. Usar outro nome sem motivo técnico contraria essa convenção sem nenhum ganho prático. O curso adota `origin` como padrão. O subcomando `add` instrui `git remote` a registrar uma nova entrada; outros subcomandos do mesmo comando permitem listar, renomear ou remover remotos.

**Localização**. Este comando é executado uma única vez por repositório local, no momento em que se estabelece a primeira conexão com um repositório remoto. Após o registro, as operações de envio e recebimento referenciam `origin` automaticamente.

**Contrafactual**. Sem este comando, o repositório local não sabe da existência do repositório remoto. Qualquer tentativa de executar `git push` ou `git pull` retornará um erro indicando que nenhum remoto está configurado.

---

### Verificação da conexão

```shell
git remote -v
```

**Finalidade**. `git remote -v` é o comando que lista os repositórios remotos registrados no repositório local, exibindo o nome e a URL associada a cada um, tanto para operações de envio quanto de recebimento.

**Motivação**. Após executar `git remote add`, é necessário confirmar que o registro foi realizado corretamente — com o nome esperado e a URL exata do repositório remoto. Sem verificação, uma URL digitada incorretamente passaria despercebida até a primeira tentativa de envio.

**Decisão**. A flag `-v` significa *verbose* — detalhado. Sem ela, `git remote` lista apenas os nomes dos remotos registrados, sem exibir as URLs. Com ela, cada remoto aparece em duas linhas: uma marcada como `fetch` e outra como `push`. A distinção existe porque o Git permite, em configurações avançadas, que o endereço de envio seja diferente do endereço de recebimento. Para o curso, as duas URLs serão sempre iguais.

**Localização**. Utilizado sempre que for necessário inspecionar quais remotos estão registrados e confirmar que as URLs estão corretas — em especial após `git remote add` e ao diagnosticar falhas de conexão.

**Contrafactual**. Sem a flag `-v`, a saída seria apenas `origin` — sem URL, sem contexto suficiente para verificação. Não seria possível confirmar se o endereço registrado está correto.

A saída esperada é:

```shell
origin  https://github.com/alexgeracaotech/course.git (fetch)
origin  https://github.com/alexgeracaotech/course.git (push)
```

---

## Bloco 5 — Sincronização

---

### Envio de commits ao remoto

```shell
git push -u origin main
```

O Git solicitará autenticação abrindo um modal com duas abas: ***Browser/Device*** e ***Token***. Selecione a aba ***Token*** e cole o *Personal Access Token* gerado e salvo anteriormente.

**Finalidade**. `git push -u origin main` é o comando que envia os commits da branch `main` local para o repositório remoto `origin`, criando a branch `main` no remoto caso ela ainda não exista, e registra o vínculo entre a branch local e a remota.

**Motivação**. Os commits existem apenas localmente até que sejam enviados ao repositório remoto. O envio é necessário para que o trabalho esteja disponível no GitHub — seja para backup, seja para colaboração.

**Decisão**. A flag `-u` significa *set upstream* — definir o upstream. **Upstream** é o nome técnico para o remoto e a branch remota que correspondem a uma branch local. Ao usar `-u` na primeira execução, o Git registra que `origin main` é o destino padrão desta branch. A partir desse registro, todos os envios futuros desta branch podem ser feitos com `git push` sem argumentos — o destino já está memorizado. Sem `-u`, o Git envia os commits normalmente nesta execução, mas não registra o upstream; na execução seguinte sem argumentos, o Git retornará um erro solicitando que o destino seja especificado explicitamente. `origin` é o nome do remoto registrado com `git remote add`; `main` é o nome da branch local cujos commits serão enviados e o nome que essa branch terá no remoto.

**Localização**. O `-u` é utilizado apenas na primeira vez que uma branch local é enviada ao remoto. Nas execuções seguintes, `git push` sem argumentos é suficiente.

**Contrafactual**. Sem `git push`, os commits permanecem exclusivamente no repositório local. O repositório remoto continua vazio, sem histórico e sem os arquivos do projeto.

Após a execução bem-sucedida, acesse o repositório no GitHub e recarregue a página. Os arquivos e o histórico de commits que existiam apenas na máquina local agora estão visíveis no GitHub.

---

### Obtenção de commits do remoto

O `git push` resolve metade do fluxo: enviar o trabalho ao remoto. A outra metade é obter trabalho do remoto — seja trabalho que outra pessoa enviou, seja uma alteração feita diretamente pela interface web do GitHub.

Para simular isso, vá ao GitHub, abra o repositório, clique em qualquer arquivo existente, clique no ícone de lápis para editar, faça uma alteração pequena em qualquer linha e clique em ***Commit changes***. Um commit foi criado diretamente no remoto — um commit que não existe na máquina local.

Agora, execute:

```shell
git pull
```

**Finalidade**. `git pull` é o comando que busca os commits do repositório remoto que ainda não existem localmente e os integra à branch atual.

**Motivação**. Commits criados no remoto — por outro desenvolvedor ou diretamente pela interface web do GitHub — não chegam automaticamente ao repositório local. É necessário buscá-los explicitamente para que a branch local reflita o estado atual do remoto.

**Decisão**. Como o upstream já está definido graças ao `-u` do push anterior, não é necessário especificar `origin main` — o Git sabe de onde buscar. O resultado é que a branch local avança para incluir os commits que existiam apenas no remoto.

**Localização**. Utilizado sempre que for necessário atualizar o repositório local com commits que existem no remoto — no início de uma sessão de trabalho colaborativo ou após alterações feitas diretamente pela interface do GitHub.

**Contrafactual**. Sem `git pull`, o repositório local permanece desatualizado em relação ao remoto. Ao tentar executar `git push` com commits locais enquanto o remoto tem commits que o local não possui, o Git rejeitará o envio com uma mensagem de erro.

---

## Bloco 6 — Clonagem

Até agora, o fluxo praticado foi: criar repositório local com `git init`, fazer commits, criar repositório remoto no GitHub vazio, conectar os dois com `git remote add`, enviar com `git push`.

Existe um segundo fluxo, e ele é o padrão profissional adotado em todo o restante deste curso.

---

### Clone

Neste fluxo, a ordem se inverte: o repositório nasce no GitHub primeiro. O repositório remoto é criado pela interface web, e só então uma cópia é trazida para a máquina local. O comando responsável por isso é o `git clone`.

```shell
git clone YOUR_REPOSITORY_URL
```

**Finalidade**. `git clone YOUR_REPOSITORY_URL` é o comando que cria uma cópia completa de um repositório remoto na máquina local. *Completa* significa que ele copia não apenas os arquivos no estado atual, mas todo o histórico de commits e todas as branches, e já configura automaticamente o `origin` apontando para o repositório de origem.

**Motivação**. Quando o repositório já existe no remoto — criado pelo próprio desenvolvedor, por um colega ou pelo time de infraestrutura — o ponto de partida do trabalho local é obter uma cópia desse repositório. O clone realiza essa operação em um único comando, eliminando os passos manuais de `git init` e `git remote add`.

**Decisão**. O endereço utilizado é o HTTPS do repositório remoto, o mesmo formato usado anteriormente. O clone cria um novo diretório com o nome do repositório dentro do diretório atual do terminal. Se o terminal estiver em `C:\Users\username` e o repositório clonado for `https://github.com/your-user/course.git`, o Git criará `C:\Users\username\course` com todo o conteúdo do repositório dentro. Não é necessário executar `git remote add` após o clone — ele já registra o `origin` automaticamente.

**Localização**. Utilizado sempre que for necessário obter uma cópia local de um repositório que já existe no remoto — ao iniciar o trabalho em um projeto existente ou ao adotar o fluxo profissional de criação de projetos.

**Contrafactual**. Sem `git clone`, seria necessário criar o repositório local com `git init`, adicionar o remoto manualmente com `git remote add` e buscar os commits existentes em passos separados. O clone consolida essas operações em um único comando.

---

### Padrão profissional

A diferença entre os dois fluxos não é apenas de ordem — é de consequência prática.

No fluxo anterior, o repositório remoto nasce vazio e só recebe conteúdo após o primeiro push. Há uma janela de tempo em que o projeto existe apenas localmente. O passo de conexão com `git remote add` é manual e pode ser esquecido ou configurado incorretamente.

No fluxo atual, o repositório remoto existe desde o primeiro momento. Ao clonar e iniciar o trabalho, a conexão com o `origin` já está configurada. O primeiro commit feito localmente pode ser enviado com `git push` imediatamente, sem nenhuma configuração adicional. O projeto nunca existiu apenas na máquina local — desde o início ele tem um endereço remoto.

Em ambientes profissionais, o fluxo é invariavelmente esse: o repositório é criado na plataforma remota — seja pelo próprio desenvolvedor, seja por um colega de time ou pelo time de infraestrutura — e cada pessoa que vai trabalhar nele executa `git clone` para obter sua cópia local.

A partir do módulo seguinte deste curso, todo projeto começa com este fluxo: o repositório é criado no GitHub primeiro, clonado localmente, e só então o desenvolvimento tem início.

---

## Bloco 7 — Merge

Nas aulas anteriores foram apresentadas a criação de branches e a alternância entre elas. Uma branch é uma linha do tempo independente — o trabalho nela não afeta a `main`. Em algum momento, o trabalho feito nessa branch precisa ser incorporado de volta. O mecanismo que faz isso é o **merge**.

---

### Definição de merge

Merge significa mesclar. Ao fazer merge de uma branch em outra, instrui-se o Git a: *"pegue todos os commits que existem naquela branch e que ainda não existem nesta, e traga-os para cá"*.

Considere a seguinte analogia: um documento está sendo escrito e decide-se testar uma nova seção em uma folha separada para não comprometer o original. Quando a seção fica satisfatória, o conteúdo da folha separada é recortado e colado no documento original. O merge é exatamente esse recorte-e-cola — mas executado pelo Git, com todo o histórico preservado.

O comando é executado a partir da branch que vai receber o trabalho:

```shell
git merge branch-name
```

**Finalidade**. `git merge branch-name` é o comando que incorpora os commits de uma branch especificada à branch atual, unificando os históricos das duas linhas de desenvolvimento.

**Motivação**. O trabalho desenvolvido em uma branch isolada precisa ser reintegrado à branch principal quando estiver concluído. O merge é o mecanismo que realiza essa reintegração, preservando o histórico completo de ambas as linhas.

**Decisão**. O comando é executado a partir da branch de destino — aquela que vai receber o trabalho. Para incorporar o trabalho da branch `functionality` na branch `main`, é necessário primeiro alternar para a `main` com `git checkout main` e, a partir dela, executar `git merge functionality`. Essa direção é fixa: o merge sempre traz commits para a branch atual, nunca o contrário.

**Localização**. Utilizado ao final do desenvolvimento de uma funcionalidade, correção ou qualquer trabalho realizado em branch isolada, quando esse trabalho está pronto para ser integrado à branch principal.

**Contrafactual**. Sem `git merge`, o trabalho realizado em branches isoladas permaneceria permanentemente separado da branch principal. Não haveria mecanismo para reunir as linhas de desenvolvimento divergentes.

---

### Fast-forward

Essa expressão apareceu na saída do `git pull` anteriormente. A seguir, a explicação completa.

**Fast-forward** — em português, *avanço rápido* — é o caso mais simples de merge. Ele ocorre quando a branch de destino não teve nenhum commit novo desde o momento em que a outra branch foi criada.

Visualize assim: a `main` estava no commit A quando a branch `functionality` foi criada. Os commits B e C foram feitos na `functionality`. Enquanto isso, a `main` ficou parada no commit A — nenhum commit foi feito nela.

```text
main:         A
               \
functionality:  B - C
```

Ao fazer merge de `functionality` na `main`, o Git percebe que a `main` simplesmente ficou para trás. Não há nada na `main` que a `functionality` não tenha. O Git não precisa criar um commit de fusão — ele apenas move o ponteiro da `main` para frente, direto para o commit C:

```text
main:          A - B - C
```

Isso é o fast-forward: a `main` *avança rapidamente* para alcançar a branch incorporada. É o cenário mais comum no trabalho individual com branches sequenciais.

---

### Noção de conflito de merge

Existe um cenário diferente do fast-forward, e é importante conhecer seu nome e sua causa — mesmo que a resolução prática não faça parte desta aula.

Um conflito de merge ocorre quando duas branches modificaram a mesma parte do mesmo arquivo de formas diferentes. O Git não consegue decidir sozinho qual versão é a correta — essa é uma decisão humana. Ele interrompe o merge, marca os trechos conflitantes no arquivo e aguarda edição manual para resolver.

O conflito não é um erro do Git — é uma situação esperada em trabalho colaborativo. A resolução prática de conflitos será exercitada em momento posterior do curso, quando o desenvolvimento ocorrer em projetos com múltiplas branches ativas. Por ora, o que importa é saber que conflitos existem, por que ocorrem, e que o Git os sinaliza em vez de tomar decisões arbitrárias.
