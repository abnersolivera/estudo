# Fluxo de desenvolvimento com GitFlow
***

## Introdução

O GitFlow utiliza uma metodologia moderna para desenvolver sistema e gerenciar as etapas do processo, como requesitos do sistema, arquitetura, padrões de codificações etc...
O GitFlow é um framework que trabalha junto com o controle de versão do Git, podendo melhorar o controle e desenvolvimento do seu projeto.

## Workflows (fluxos de trabalho)

Centralized Workflow: Esse fluxo se assemelha muito a quem já está acostumado a trabalhar com VCSscentralizados. Como o SVN, ele utiliza um servidor central como repositório que serve como um ponto único para mudanças e ele tem uma linha chamada master. Esse tipo de fluxo não precisa de nenhum outro branch, a não ser o master. O problema desse fluxo é a grande possibilidade de existir conflitos constantes.

![Centralized Workflow](https://static.imasters.com.br/wp-content/uploads/2015/04/git-workflow-svn-push-local-230x300.png)

Feature Branch Workflow: É extremamente parecido com o workflow anterior; a diferença é que nesse podemos ter diversos branches para criação de novas funcionalidades. Os desenvolvedores devem criar um branch para cada funcionalidade nova no projeto, além disso, o nome do branch deve ser bem descritivos. A grande vantagem desse tipo de fluxo é que podemos fazer uma estratégia de revisão de código através de Pull Requests (PR). Os PR são muito utilizados em projetos de código aberto, onde nem todo mundo tem permissão de comitar no repositório; mas através de um PR, ele pode modificar o código e enviar uma sugestão ou correção para ser analisada. Se a proposta for aprovada, é feito o merge com o repositório central. Uma grande empresa que utiliza esse fluxo é o Github (GitHubFlow).

![Feature Branch Workflow](https://static.imasters.com.br/wp-content/uploads/2015/04/git-workflow-feature-branch-1-300x262.png)

Forked Workflow: Esse fluxo é totalmente diferente dos outros citados até agora. Ao invés de termos um repositório central em um servidor, cada desenvolvedor terá um repositório que será seu servidor. Como nos outros fluxos de trabalho, esse fluxo começa com um repositório público oficial armazenado em um servidor. Mas quando um novo desenvolvedor quer começar a trabalhar no projeto, eles não clonam diretamente do repositório oficial. Ao invés disso, eles fazem um fork do repositório oficial e criam uma cópia no servidor. Esta nova cópia serve como seu repositório público pessoal, outros desenvolvedores não têm permissão para comitar nele, mas eles podem receber as mudanças a feitas nele (vamos ver por que isso é importante em um próximo momento). Depois de ter criado a sua cópia do no servidor, o desenvolvedor faz um clone para obter uma cópia do seu repositório em sua máquina local. Isto serve como seu ambiente de desenvolvimento privado.

![Forked Workflow](https://static.imasters.com.br/wp-content/uploads/2015/04/git-workflows-forking-300x258.png)

## Gitflow

Como afirma Vincent Driessen (2010), o Gitflow foi criado em 2010 e considerado um ótimo modelo de branching. Para entendermos melhor, um branch é uma ramificação da árvore principal do seu código; por exemplo, para quem trabalha com SVN existe o trunk e o branch. Já para quem utiliza GIT, tudo é branches, mas por convenção, novos branches são criados a partir do master, que seria a raiz do seu código.
Driessen (2010) afirma que o Gitflow é um modelo fortemente baseado em branches, mas focados em entregas de projetos. Apesar dele ser um pouco mais complexo que outros workflows, ele disponibiliza um framework robusto para gerenciar projetos mais complexos ou de grande porte.
Esse workflow não traz nenhum conceito novo para o Git, ele define os papéis de cada branch e como eles devem interagir. Mas como tudo isso funciona? O Gitflow ainda utiliza um repositório centralizado (lembrando que ele é um DVCS) como o centro de comunicação entre todos os desenvolvedores.

![figura](https://static.imasters.com.br/wp-content/uploads/2015/04/git-workflow-release-cycle-4maintenance.png)

Historic Branches: Ao invés de trabalhar apenas com o branch master, esse workflow utiliza dois branches principais para guardar histórico do projeto. O branch master guarda o histórico oficial das entregas, já o branch develop serve como integração entre todos os branches de funcionalidades (feature branches).

**Feature Branches:** Cada funcionalidade deve ter seu próprio branch, e ele deve ser criado a partir do branch develop. Quando uma funcionalidade for concluída, ela é mesclada (merged) novamente com o seu branch pai. As features nunca devem interagir diretamente com o master.

**Release Branches:** Quando o branch develop estiver com funcionalidades suficientes para uma entrega, nós criamos um branch de entrega (release branch). Com isso, nós damos início ao próximo ciclo de entrega, ou seja, nenhuma nova funcionalidade pode ser incluída a partir desse momento. Quando estivermos prontos para realizar a entrega, o release é mesclada com os branches master e develop.

**Maintenance Branches:** Também conhecidos como hotfix. Eles são usados para corrigir rapidamente algum problema em produção. Este é o único branch que deve ser criado a partir do master. Assim que a correção for finalizada, o branch é fechado e mesclado com o master e develop, mantendo assim as linhas completamente atualizadas.
