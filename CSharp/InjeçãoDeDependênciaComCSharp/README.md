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
