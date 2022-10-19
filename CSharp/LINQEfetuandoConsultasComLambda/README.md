# LINQ e C# Efetuando consultas com Lambda Expressions
***

LINQ é um conjunto de métodos e operadores da linguagem C# cujo objetivo é permitir a realização de consultas a coleções de objetos. Por meio desse recurso é possível efetuar tarefas comuns como localizar um objeto, somar e contar dados, ordenar listas, etc.&nbsp;&nbsp;
Um dos usos mais comuns do LINQ é na realização de consultas a bancos de dados usando o Entity Framework. Uma vez que esse framework ORM abstrai a estrutura do banco (tabelas, colunas e linhas) e a representa como objetos e listas em nossa aplicação, podemos efetuar diversas operações como filtro e ordenação usando apenas funções e expressões lambda.

## Ordenação

O principal método para ordenação de listas é o __OrderBy__, que recebe como parâmetro a propriedade pela qual a coleção deve ser ordenada.

`var cursos = db.Cursos.OrderBy(c => c.DataPublicacao);`

Aqui a variável cursos está recebendo todos os registros da coleção db.Cursos, porém já ordenados pela data de publicação. É importante destacar que esse método não afeta a coleção original, ao invés disso ele retorna uma nova lista ordenada.

Para ordenar de forma decrescente podemos usar o método __OrderByDescending__.

`var cursos = db.Cursos.OrderByDescending(c => c.DataPublicacao);`

Também é possível ordenar por mais de uma propriedade. Para isso, para a primeira ordenação devemos usar o método __OrderBy__ (ou __OrderByDescending__) e em seguida os métodos __ThenBy__ ou __ThenByDescending__. Por exemplo, se desejarmos ordenar os registros pela data de publicação e em seguida pela carga horária.

```
var cursos = db.Cursos.OrderBy(c => c.DataPublicacao).ThenBy(c => c.CargaHoraria);
var cursos = db.Cursos.OrderBy(c => c.DataPublicacao).ThenByDescending(c => c.CargaHoraria);
```

## Filtros

O principal método para filtrar coleções é o __Where__, que recebe como parâmetro uma expressão representando o filtro a ser aplicado. Essa expressão representa um delegate, ou seja, uma referência para um método que espera como parâmetro um objeto do tipo armazenado pela lista (um curso, nesse caso) e retorna um booleano indicando se esse objeto atende a uma condição.

`var cursos = db.Cursos.Where(c => c.Canal == Canal.Python);`

Observe no parâmetro do método __Where__: usamos uma expressão lambda para atender ao delegate esperado. O argumento c representa cada curso na lista e à direita do operador lambda (=>) temos uma expressão booleana que deve ser atendida para que o item seja incluído na lista resultante.

Exemplos com esse método:

_cursos com carga horária maior que 10h_

`var cursos = db.Cursos.Where(c => c.CargaHoraria > 10);`

_cursos cujo título contém o termo "JSF"_

`var cursos = db.Cursos.Where(c => c.Titulo.Contains("JSF"));`

Também é possível usar os métodos do LINQ em conjunto. Por exemplo, após filtrar uma lista podemos ordená-la.

`var cursos = db.Cursos.Where(c => c.CargaHoraria > 10).OrderByDescending(c => c.DataPublicacao);`

## Funções de agregação

Funções de agregação como SUM, COUNT e AVG do SQL são muito utilizadas no contexto de bancos de dados. Com LINQ também é possível utilizá-las com coleções de objetos. Para isso temos vários métodos.

`int soma = db.Cursos.Sum(c => c.CargaHoraria);`

Aqui estamos somando a carga horária de todos os cursos.

`int total = db.Cursos.Count(c => c.Canal == Canal.EngenhariaDeSoftware);`

Neste exemplo estamos contando quantos cursos pertencem ao canal Engenharia de Software.

`double media= db.Cursos.Average(c => c.CargaHoraria);`

Com o método Average podemos calcular a média de valores. Neste caso estamos obtendo a média da carga horária dos cursos.

`int max = db.Cursos.Max(c => c.CargaHoraria);`
`int min = db.Cursos.Min(c => c.CargaHoraria);`

Aqui estamos obtendo a maior e a menor carga horária dos cursos usando para isso as funções Min e Max.

## Limitando a quantidade de registros

Muitas vezes desejamos obter apenas uma quantidade específica de registros de uma lista. Para isso podemos usar dois métodos __Take__ ou __FirstOrDefault__. O primeiro retorna uma lista contendo um determinado número de itens passado por parâmetro, enquanto o segundo retorna o primeiro item da lista ou null caso a lista não possua itens.

`var cursos = db.Cursos.OrderByDescending(c => c.DataPublicacao).Take(5);`

Nesse exemplo ordenamos a lista de cursos pela data de publicação de forma decrescente e pegamos apenas os 5 primeiros itens.

`var curso = db.Cursos.OrderByDescending(c => c.DataPublicacao).FirstOrDefault(c => c.Canal == Canal.PHP);`

Aqui estamos pegando apenas o primeiro registro da lista ordenada, mas cujo canal é PHP. Ou seja, estamos pegando o curso mais recente de PHP.

Há ainda outros métodos e combinações possíveis entre eles que podem ser feitas a fim de atender cada necessidade. Para usá-los, é importante lembrar que é necessário importar o _namespace System.Linq_, onde estão declarados.
