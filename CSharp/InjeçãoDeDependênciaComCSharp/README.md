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

`public interface IObjetoEndereco
    {
        #region Declarar Propriedades e Métodos

        #endregion
    }`
   
`public class Empresa
    {
        private IObjetoEndereco _endereco;

        public Empresa(IObjetoEndereco objeto)
        {
            _endereco = objeto;
        }

    }`
