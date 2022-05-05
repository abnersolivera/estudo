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

Para estudarmos essas quatro metodologias, vamos tomar como exemplo um cenário muito comum em projetos. Vamos pensar em cadastro de empresas. Neste cenário, sempre existe uma classe que irá refletir a entidade Empresa e dentro da classe Empresa muitas vezes encontramos uma referência a outra classe - Endereço, pois uma empresa possui um ou mais endereços.

Eis aqui o que geralmente encontramos na classe Empresa:

```
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
```

Analisando o código acima observamos que a classe Empresa possui uma propriedade do tipo Endereco. Neste modelo, utilizamos uma classe concreta para apontar o tipo de nossa propriedade. Isso é um exemplo de um alto acoplamento de componentes, pois criamos aqui uma interdependência e uma referência dentro da classe Empresa que pode nos resultar em problemas.

Vamos resolver esse problema de alto grau de acoplamento utilizando Dependency Injection nos seus 4 modos de implementação:

## Constructor Methodology

Nesta metodologia, passamos a referência de objeto no próprio construtor. Deste modo, quando criarmos uma instância da classe Empresa, podemos definir o tipo do objeto que queremos para nossa propriedade Endereco.

Veja agora como ficaria o construtor da classe utilizando essa metodologia.

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

Imaginemos agora que nosso projeto é um site, e este site utiliza uma class library, contendo as classes Empresa, Endereco e a Interface IObjetoEndereco. Pois bem, com essa mudança na classe Endereço, utilizando essa metodologia, nós teríamos que modificar apenas os códigos que instanciam a classe Empresa, além claro, de modificar a classe endereço, não sendo necessário modificar a classe Empresa dentro da class library. Antes da modificação da classe nossas chamadas seriam assim:

```
Endereco objEnd = new Endereco();
Empresa = new Empresa(objEnd);
```

Com a mudança solicitada as chamadas ficariam assim:

```
EnderecoPlus objEndPlus = new EnderecoPlus();
Empresa = new Empresa(objEndPlus);
```

Ou seja, não precisaríamos modificar nossa classe base “Empresa”, pois seu construtor espera um objeto que implemente a Interface IObjetoEndereco, e tanto a classe Endereco quanto a classe EnderecoPlus são implementações da Interface IObjetoEndereco, ou seja, o construtor da classe Empresa pode receber qualquer um dos dois.

Essa metodologia não é recomendada para sistemas em que as classes só possam definir construtores vazios, ou seja, onde os construtores das classes não possam receber parâmetros.

## Getter e Setter

Essa metodologia é mais comumente usada para implementar Dependency Injection (DI). Nela a dependência dos objetos é exposta nas propriedades Get e Set das classes. Essa metodologia possui alguns pontos negativos, pois a injeção de dependência nas propriedades Get e Set quebra alguns conceitos e regras do encapsulamento, ou seja, iremos realizar algo que vai contra os preceitos da orientação a objetos.

Segue um exemplo de como implementar essa metodologia:

```
public class Empresa
{
    private IObjetoEndereco _endereco;

    public IObjetoEndereco Endereco
    {
        get { return _endereco; }
        set { _endereco = value; }
    }

}
```

Vejam que a propriedade Endereco, trabalha com a Interface IObjetoEndereco para realizar o Get e Set.

Como dito anteriormente, utilizando essa metodologia, deixamos a classe base Empresa livre de referências a classes concretas. Em uma suposta manutenção precisaríamos modificar apenas a classe Empresa e os trechos de código que instanciam e utilizam as propriedades de Empresa.

## Interface Implementation

Nesta metodologia nós implementamos uma interface que ficará em um repositório dentro da camada de IOC (Inversion of Control). Essa Interface declara um método para injetar o objeto na classe principal.

Vamos então criar uma nova Interface chamada IObjetoEnderecoDI, a qual irá declarar um método chamado setEndereco:

```
public interface IObjetoEnderecoDI
    {
        void setEndereco(IObjetoEndereco obj);
    }
```

Essa Interface será implementada na classe Empresa. Os códigos clientes que irão instanciar um objeto Empresa poderão utilizar o método setEndereco para injetar o objeto Endereco no objeto Empresa.

Agora vamos modificar nossa classe Empresa para codificar o que foi dito acima.

```
public class Empresa :IObjetoEnderecoDI
{
    private IObjetoEndereco _endereco;

    #region IObjetoEnderecoDI Members

    public void setEndereco(IObjetoEndereco obj)
    {
        _endereco = obj;
    }

    #endregion
}
```

Vejam que a classe Empresa agora herda da nossa nova Interface IObjetoEnderecoDI. Agora ela precisa implementar o método setEndereco, e neste método recebemos como parâmetro um objeto do tipo IObjetoEndereco que será utilizado para setar o campo privado _endereco.

## Service Locator

Nesta metodologia a classe que irá agregar um objeto filho utiliza uma classe “Localizadora de Objetos”, para obter a instância correta do objeto filho. Essa classe Localizadora não cria instâncias do objeto filho, ela provê uma metodologia para registrar e achar os serviços que ajudam na criação do objeto.

Vamos ao exemplo. Primeiramente vamos criar a classe que será a Localizadora de Objetos.

```
static class LocalizadorEndereco
{
    public static IObjetoEndereco getEndereco()
    {
        throw new NotImplementedException();
    }
}
```

Agora vamos utiliza - lá na classe Empresa

```
public class Empresa
{
    private IObjetoEndereco _endereco;

    public Empresa()
    {
        this._endereco = LocalizadorEndereco.getEndereco();
    }
}
```

Veja o leitor que agora nossa classe empresa possui um construtor que chama o Service Locator, para obter a instância do objeto Endereco.

A maior vantagem desta metodologia é a possibilidade de modificarmos o nosso Service Locator a qualquer momento para definirmos os nossos objetos sempre que precisarmos.
