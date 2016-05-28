# Diretivas customizadas

Diretiva customizada veio para facilitar a criação de componentes, que muitas vezes são reutilizados em diversas páginas da aplicação.

Esses componentes são criados através da função `.directive()`, podemos gerar atributos, elementos, comentários e classes. Dentro da função, passamos dois parametros. O primeiro é o nome e o segundo é uma função. 

Uma coisa importante sobre o nome da diretiva, é entender como o angular traduz o nome composto. Se colocarmos um nome todo minusculo ('nomedadiretiva'), o angular vai entender como 'nomedadiretiva', caso o nome seja ('nomeDaDiretiva'), o angular vai entender como 'nome-da-diretiva'.

Dentro da função que passamos no `.directive()`, precisamos retornar variáveis com valores que informam ao angular, o que a tal diretiva faz.

## Variáveis da Diretiva

Como existem carros para determinados tipos de pessoas, existem diretivas para determinadas necessidades. Veja abaixo as opções utilizadas para compor uma diretiva.

```
.directive('nomedadiretiva', function(){
 return {
   restrict:null,
   link: null,
   transclude: null,
   scope: null
   template: null,
   templateUrl: null
 }
})
```
### Restrict

A variável `restrict` tem como objetivo, informar ao angular qual é o tipo de diretiva que iremos criar, veja os tipos abaixo.

* 'A' para atributo.
* 'E' para elementos.
* 'C' para classes.
* 'M' para comentários.


#### Tipo A - Diretiva Atributo

```
.directive('nomedadiretiva', function(){
 return {
   restrict: 'A'
 }
})
```
Essa diretiva é usada em tags html, ela é usada geralmente para escutar eventos de mouse **(click,doubleclick, mouseenter, mouseleave, mousemove)** e teclado **(keyup, keypress, keydown)**.

O nome de exemplo da nossa diretiva, será `diretivaA`, veja como usamos numa tag html.

```
<button diretiva-a>Clique<button>
```


Podemos escutar esses eventos através da variável `link`, que iremos abordar no próximo subcapitulo '**Variáveis da Diretiva - Link**'. 





Caso não informamos nada, o angular usará a diretiva como atributo `A`.

A variável `link` é uma função importante, quando estamos lidando com uma diretiva que tem interação do usuário.

Na função, temos três parametros de retorno (scope, element, attr), são os mais 

