# Fluxo de desenvolvimento com GitFlow
***

## Introdução

O GitFlow utiliza uma metodologia moderna para desenvolver sistema e gerenciar as etapas do processo, como requesitos do sistema, arquitetura, padrões de codificações etc...
O GitFlow é um framework que trabalha junto com o controle de versão do Git, podendo melhorar o controle e desenvolvimento do seu projeto.

## O que é Git Flow?

É um fluxo de trabalho para o Git criado para facilitar o processo de desenvolvimento com uma série de comandos novos. O nome por trás desse modelo é Vincent Driessen que, em 2010, escreveu em seu blog pessoal a maneira que ele pensou ser a mais simples de se trabalhar com o Git em larga escala.

Mesmo sendo um método que auxilia o nosso trabalho devemos ter algumas ressalvas diante de como é aplicado: se usado de maneira inadequada, o Git Flow pode se tornar bastante ineficiente e gerar uma experiência não muito agradável.

## Workflows (fluxos de trabalho)

Centralized Workflow:

Esse fluxo se assemelha muito a quem já está acostumado a trabalhar com VCSscentralizados. Como o SVN, ele utiliza um servidor central como repositório que serve como um ponto único para mudanças e ele tem uma linha chamada master. Esse tipo de fluxo não precisa de nenhum outro branch, a não ser o master. O problema desse fluxo é a grande possibilidade de existir conflitos constantes.

![Centralized Workflow](https://static.imasters.com.br/wp-content/uploads/2015/04/git-workflow-svn-push-local-230x300.png)

Feature Branch Workflow:

É extremamente parecido com o workflow anterior; a diferença é que nesse podemos ter diversos branches para criação de novas funcionalidades. Os desenvolvedores devem criar um branch para cada funcionalidade nova no projeto, além disso, o nome do branch deve ser bem descritivos. A grande vantagem desse tipo de fluxo é que podemos fazer uma estratégia de revisão de código através de Pull Requests (PR). Os PR são muito utilizados em projetos de código aberto, onde nem todo mundo tem permissão de comitar no repositório; mas através de um PR, ele pode modificar o código e enviar uma sugestão ou correção para ser analisada. Se a proposta for aprovada, é feito o merge com o repositório central. Uma grande empresa que utiliza esse fluxo é o Github (GitHubFlow).

![Feature Branch Workflow](https://static.imasters.com.br/wp-content/uploads/2015/04/git-workflow-feature-branch-1-300x262.png)

Forked Workflow:

Esse fluxo é totalmente diferente dos outros citados até agora. Ao invés de termos um repositório central em um servidor, cada desenvolvedor terá um repositório que será seu servidor. Como nos outros fluxos de trabalho, esse fluxo começa com um repositório público oficial armazenado em um servidor. Mas quando um novo desenvolvedor quer começar a trabalhar no projeto, eles não clonam diretamente do repositório oficial. Ao invés disso, eles fazem um fork​ do repositório oficial e criam uma cópia no servidor. Esta nova cópia serve como seu repositório público pessoal, outros desenvolvedores não têm permissão para comitar nele, mas eles podem receber as mudanças a feitas nele (vamos ver por que isso é importante em um próximo momento). Depois de ter criado a sua cópia do no servidor, o desenvolvedor faz um clone para obter uma cópia do seu repositório em sua máquina local. Isto serve como seu ambiente de desenvolvimento privado.

![Forked Workflow](https://static.imasters.com.br/wp-content/uploads/2015/04/git-workflows-forking-300x258.png)

## Gitflow

Como afirma Vincent Driessen (2010), o Gitflow foi criado em 2010 e considerado um ótimo modelo de branching. Para entendermos melhor, um branch é uma ramificação da árvore principal do seu código; por exemplo, para quem trabalha com SVN existe o trunk e o branch. Já para quem utiliza GIT, tudo é branches, mas por convenção, novos branches são criados a partir do master, que seria a raiz do seu código.
Driessen (2010) afirma que o Gitflow é um modelo fortemente baseado em branches, mas focados em entregas de projetos. Apesar dele ser um pouco mais complexo que outros workflows, ele disponibiliza um framework robusto para gerenciar projetos mais complexos ou de grande porte.
Esse workflow não traz nenhum conceito novo para o Git, ele define os papéis de cada branch e como eles devem interagir. Mas como tudo isso funciona? O Gitflow ainda utiliza um repositório centralizado (lembrando que ele é um DVCS) como o centro de comunicação entre todos os desenvolvedores.

![figura](https://lh3.googleusercontent.com/70jaEZnESXQ6SssU5uI4yO62JBz6xq2sNrrz8bW_ap2CuWUaQlbKs3j6NyRJnvcvYwAugkW8WzNJX21dZ2SMd9O_1TTpKZT-FsBkYSPy4rUSpJSo2C-WPTaLc2jQ8ancyj1TetXQ)

## Como funciona e quais os branches do fluxo Git Flow?

O primeiro passo para entender o Git Flow é compreender o funcionamento das branches (ramos) que são estabelecidas por padrão. Com elas, além de conseguirmos uma nomenclatura simples e arranjada, temos a categorização que as torna mais objetivas e de fácil entendimento para pessoas de fora do projeto.

### Branch Main/Master

Principal branch, contém associadas a ela as versões de publicação para facilitar o acesso e a busca por versões mais antigas. Também entendemos que é o espelho do programa que está no ar, já que o último código dessa branch deve sempre estar em produção. Além do mais, a única maneira de interagir com essa branch é através de uma Hotfix ou de uma nova Release.

### Branch Develop

É uma das principais branches e serve como uma linha com os últimos desenvolvimentos. Como visto na imagem, é uma cópia da branch principal contendo algumas funcionalidades que ainda não foram publicadas. Sendo assim, é a base para o desenvolvimento de novas features.

### Branch Feature

Uma das branches temporárias e auxiliares do nosso fluxo, sendo a branch que contém uma nova funcionalidade específica para a nossa aplicação. Nela temos a convenção do nome feature/nome_do_recurso que será utilizada no nosso fluxo de trabalho. Não podemos esquecer que toda nova Feature começa e termina obrigatoriamente a partir da develop.

### Branch Hotfix

Também é uma branch auxiliar e temporária, utilizada quando ocorre algum problema no ambiente de produção no qual a correção deve ser feita imediatamente. Conseguimos com isso solucionar o erro e fazer a mesclagem da solução para as branches main/master e develop para que não ocorra a perda do nosso código.

### Branch Release

Por fim, a branch de lançamento do nosso programa. Nela unimos o que está pronto em nossa branch de desenvolvimento e “jogamos” para a branch principal. No mais, é criado uma nova versão etiquetada no nosso projeto para que possamos ter um histórico completo do desenvolvimento.

## Comandos do Git Flow

`Init`

É o comando inicial do Git Flow e serve para configurar o repositório com as branches do fluxo padrão. Da mesma forma que você tem que inicializar o git em um novo diretório, esse comando tem o mesmo propósito.

## Feature

Dentro desse comando temos algumas ramificações possíveis, como por exemplo:

`start nome_feature`

Comando que inicia uma nova feature, nela temos a criação de uma branch com a nomenclatura feature/nome_feature.

`finish nome_feature`

Comando para encerrar uma feature anteriormente criada, além disso será feito um merge para a branch Develop.

`publish nome_feature`

Se você está trabalhando em equipe e deseja compartilhar a sua nova funcionalidade, esse comando publica no servidor remoto que está configurado no seu Git local.

`pull nome_feature`

Ao contrário da anterior, essa serve para obter uma feature do servidor remoto.

## Release

Com a terminologia parecida, veremos os comandos referentes ao lançamento:

`start nome_release [BASE]`

Utilize esse comando para iniciar uma versão baseada na branch de desenvolvimento, aqui você pode passar opcionalmente o código de algum commit para usar como base.

`publish nome_release`

É aconselhável publicar a branch de release após criá-la para permitir commits de outras pessoas desenvolvedoras. O comando é semelhante à publicação de uma nova feature.

`release track nome_release`

Novamente, se você quiser acompanhar alguma versão remota da release, existe esse comando.

`finish nome_release`

Com esse comando você finaliza e cria uma nova versão, logo em seguida é executada uma série de ações:

* junta a branch na Main/Master;
* cria uma tag com o nome da branch;
* também junta a branch com a Develop;
* por último, apaga a própria branch.

## Hotfix
Por fim temos os comandos da Hotfix:

`hotfix start nome_hotfix [BASENAME]`

A partir do último commit da branch Main/Master cria-se uma branch com a nomenclatura de hotfix/nome_hotfix. É obrigatório que seja passado o nome da hotfix e opcionalmente você pode passar um BASENAME.

`hotfix finish nome_hotfix`

Temos novamente o comando para a finalização da hotfix. Quando terminado o processo final vemos que é feito uma mesclagem da hotfix nas branches main/master e develop e também temos a criação de uma etiqueta na main/master.

