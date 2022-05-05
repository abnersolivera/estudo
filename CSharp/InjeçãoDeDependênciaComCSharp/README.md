# Injeção de Dependência com C#

## O que é Dependency Injection?

É um padrão de implementação de um outro padrão Iversão de Controle.

Devemos utilizar esse padrão quando temos a necessidade de desenvolver sistemas em que o nível de acoplamento entre seus diferentes módulos precisem ser extremamente baixos. Para quem não conhece este termo, acoplamento é uma conexão ou dependência ou até mesmo interação entre diversos módulos/sistemas de um projeto de software.

## Meios de Implementação de Dependency Injection

Ao projetar uma aplicação orientada a objeto, devemos sempre nos preocupar em deixar a aplicação bastante flexível, de modo a facilitar manutenções e criar novas funcionalidades.

* _Constructor_ - Modo em que implementamos a injeção de dependência na definição dos construtores das classes;
* _Getter and Setter_ - Modo em que implementamos a injeção de dependência na definição dos Gets e Sets das classes;
* _Interface Implementation_ - Modo em que se usa a definição de Interfaces para realizar a injeção de dependência;
* _Service Locator_ - Modo em que construímos classes que servem como “localizadoras” de objetos que iremos instanciar em nossas outras classes.

![figura](https://arquivo.devmedia.com.br/REVISTAS/easynet/imagens/34/1/1.png)

## Constructor Methodology

Nesta metodologia, passamos a referência de objeto no próprio construtor. Deste modo, quando criarmos uma instância da classe Empresa, podemos definir o tipo do objeto que queremos para nossa propriedade __Endereco__.

Exemplo como utilizaria o construtor da classe utilizando a metodologia.
```
public interface IObjetoEndereco
    {
        #region Declarar Propriedades e Métodos

        #endregion
    }
   
public class Empresa
    {
        private IObjetoEndereco _endereco;

        public Empresa(IObjetoEndereco objeto)
        {
            _endereco = objeto;
        }

    }
```

FAVORITAR
CONCLUÍDO
39GOSTEI
39

Suporte ao aluno

Anotar

Marcar como concluído
Artigos
.NET
Design Patterns - Injeção de Dependência com C#
Hoje falaremos sobre algo bastante interessante e útil na área de Desenvolvimento de Sistemas. Vamos falar sobre Design Patterns.

Design Patterns ou Padrões de Projetos, de um modo geral, consiste numa série de modelos de resolução de problemas recorrentes em projetos de desenvolvimento de softwares.

Suas raízes se encontram na obra do engenheiro Chistopher Alexander, que redigiu uma série de textos sobre suas experiências em resolução de problemas em sua área de atuação, a Engenharia Civil. Segundo ele, cada Pattern descreve um problema recorrente em projetos, e a partir disso, descreve a solução para tal problema de maneira tal, que essa solução sirva para outros projetos semelhantes.

Esses princípios foram adaptados para a Engenharia de Software e culminou na publicação da obra “Design Patterns: Elements of Reusable Object - Oriented Softwares” em 1995, de autoria de Eric Gamma, Richard Helm, Ralph Johnson e John Vlissides. Ainda hoje esse livro é a maior referência no assunto e sem dúvida alguma é a principal base para a evolução dos Patterns. Esta obra descreve 23 Patterns, sendo que com o passar do tempo muitos outros foram documentados e catalogados, porém, os 23 Patterns iniciais são ainda os mais utilizados.

Agora que sabemos o que são e como surgiram os Design Patterns, vamos estudar uma forma de implementação de um deles. Vamos ver o padrão Dependency Injection ou Injeção de Dependência.

O que é Dependency Injection?
É um dos Patterns catalogados. Em linhas gerais este padrão é uma das formas de implementar um outro padrão - Inversão de Controle. Devemos utilizar esse padrão quando temos a necessidade de desenvolver sistemas em que o nível de acoplamento entre seus diferentes módulos precisem ser extremamente baixos. Para quem não conhece este termo, acoplamento é uma conexão ou dependência ou até mesmo interação entre diversos módulos/sistemas de um projeto de software. Quanto maior for o acoplamento entre os diversos módulos de um sistema, maior a coesão deste. Porém quanto maior o nível de dependência dos módulos, mais difícil e trabalhosa é a manutenção dos mesmos, pois dar manutenção em sistemas altamente coesos é como tirar uma carta de um castelo de baralhos para dar uma polidinha nela, sem deixar o castelo ruir. E mais, depois de polir a carta, devemos colocá-la de volta, sem abalar a estrutura do castelo. A função principal deste Pattern é oferecer uma estrutura de baixo acoplamento, visando os seguintes benefícios:

Oferecer reusabilidade de componentes, uma vez que criamos componentes interdependentes, eles podem ser facilmente implementados em sistemas diversos.
Facilitar a manutenção de Sistemas, fazendo com que as manutenções em módulos não afetem o restante do sistema.
Criar códigos altamente “testáveis”. Uma vez que temos códigos implementados seguindo esse Pattern, podemos testá-los mais facilmente utilizando os “mock tests”.
Criar códigos mais legíveis, o que torna mais fácil a compreensão do sistema como um todo.
Meios de Implementação de Dependency Injection
Ao projetar uma aplicação orientada a objeto, devemos sempre nos preocupar em deixar a aplicação bastante flexível, de modo a facilitar manutenções e criar novas funcionalidades. Na prática, isso significa que os objetos que iremos criar na aplicação devem ter o mínimo possível de dependência. Esses objetos devem ter apenas as dependências necessárias para realizarem suas tarefas. Todas as dependências devem ser minimizadas, e é ai que entra o Pattern Dependency Injection. Existem quatro maneiras de implementar Dependency Injection. São elas:

Constructor - Modo em que implementamos a injeção de dependência na definição dos construtores das classes;
Getter and Setter - Modo em que implementamos a injeção de dependência na definição dos Gets e Sets das classes;
Interface Implementation - Modo em que se usa a definição de Interfaces para realizar a injeção de dependência;
Service Locator - Modo em que construímos classes que servem como “localizadoras” de objetos que iremos instanciar em nossas outras classes.
Abaixo segue uma ilustração que explica como funcionam os conceitos de Inversion of Control (IOC), Dependency Injection (DI) e as quatro maneiras de implementar DI.

img
Para estudarmos essas quatro metodologias, vamos tomar como exemplo um cenário muito comum em projetos. Vamos pensar em cadastro de empresas. Neste cenário, sempre existe uma classe que irá refletir a entidade Empresa e dentro da classe Empresa muitas vezes encontramos uma referência a outra classe - Endereço, pois uma empresa possui um ou mais endereços.

Eis aqui o que geralmente encontramos na classe Empresa:

public class Empresa
{
    private int _cod;

    public int Cod
    {
        get { return _cod; }
        set { _cod = value; }
    }
    private string _razaoSocial;

    public string RazaoSocial
    {
        get { return razaoSocial; }
        set { razaoSocial = value; }
    }

    private Endereco _endereco;

    public Endereco Endereco
    {
        get { return _endereco; }
        set { _endereco = value; }
    }

}
Analisando o código acima observamos que a classe Empresa possui uma propriedade do tipo Endereco. Neste modelo, utilizamos uma classe concreta para apontar o tipo de nossa propriedade. Isso é um exemplo de um alto acoplamento de componentes, pois criamos aqui uma interdependência e uma referência dentro da classe Empresa que pode nos resultar em problemas.

Vamos resolver esse problema de alto grau de acoplamento utilizando Dependency Injection nos seus 4 modos de implementação:

## Constructor Methodology

Nesta metodologia, passamos a referência de objeto no próprio construtor. Deste modo, quando criarmos uma instância da classe Empresa, podemos definir o tipo do objeto que queremos para nossa propriedade Endereco.

Veja agora como ficaria o construtor da classe utilizando essa metodologia.

public interface IObjetoEndereco
    {
        #region Declarar Propriedades e Métodos

        #endregion
    }

public class Empresa
    {
        private IObjetoEndereco _endereco;

        public Empresa(IObjetoEndereco objeto)
        {
            _endereco = objeto;
        }

    }
Note o leitor, que não estamos mais utilizando uma propriedade do tipo __Endereco__ na classe Empresa. Nós criamos uma Interface e agora ela é o tipo da propriedade __Endereco__. Vejam que o construtor da classe, recebe um parâmetro do tipo __IObjetoEndereco__, e seta a propriedade privada *_endereco* com o valor deste parâmetro.

A vantagem de utilizar esta metodologia, o cliente que está instanciando um objeto Empresa, decidir qual será o tipo da propriedade Endereço. Vamos supor que no primeiro release do sistema, nossa classe Endereço seja da seguinte forma:

```
public class Endereco : IObjetoEndereco
    {
        private string _logradouro;
        private int _numero;
        public string Logradouro
        {
            get { return _logradouro; }
            set { _logradouro = value; }
        }

        public int Numero
        {
            get { return _numero; }
            set { _numero = value; }
        }

    }
```

Nesta situação a classe Endereço herda a Interface IObjetoEndereco e define duas propriedades.

Agora imaginemos que a classe Endereço terá mais que duas propriedades, por exemplo:

```
public class EnderecoPlus : IObjetoEndereco
{
    private string _tipoLogradouro;
    private string _logradouro;
    private int _numero;

    public string TipoLogradouro
    {
        get { return _tipoLogradouro; }
        set { _tipoLogradouro = value; }
    }

    public string Logradouro
    {
        get { return _logradouro; }
        set { _logradouro = value; }
    }

    public int Numero
    {
        get { return _numero; }
        set { _numero = value; }
    }
}
```
