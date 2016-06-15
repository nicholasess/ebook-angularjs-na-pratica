# Diretivas customizadas

Diretiva customizada veio para facilitar a criação de componentes, que muitas vezes são reutilizados em diversas páginas da aplicação.

As diretivas são criadoa através da função `.directive()`, podendo gerar atributos, elementos, comentários e classes. Dentro da função, passamos dois parametros. O primeiro é o nome e o segundo é uma função que retorna a regra de negócio da diretiva.

Uma coisa importante sobre o nome da diretiva, é entender como o angular traduz o nome composto. Se colocarmos um nome todo minusculo ('nomedadiretiva'), o angular vai entender como 'nomedadiretiva', caso o nome seja ('nomeDaDiretiva'), o angular vai entender como 'nome-da-diretiva'.

Dentro da função que passamos no `.directive()`, precisamos retornar variáveis com valores que informam ao angular, o que a tal diretiva faz.

## Variáveis da Diretiva

Como existem carros para determinados tipos de pessoas, existem diretivas para determinadas necessidades. Veja abaixo as opções utilizadas para compor uma diretiva.

```
.directive('nomedadiretiva', function(){
 return {
   restrict:null,
   link: null,
   template: null,
   templateUrl: null,
   transclude: null,
   scope: null
 }
})
```
### Restrict

A variável `restrict` tem como objetivo, informar ao angular qual é o tipo de diretiva que iremos criar, veja os tipos abaixo.

* 'A' para atributo.
* 'E' para elementos.

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
<button diretiva-a>Clique</button>
```

#### Tipo E - Diretiva Componente
```
.directive('nomedadiretiva', function(){
 return {
   restrict: 'E'
 }
})
```
Essa diretiva é usada como tag com abertura e fechamento `<nomedadiretiva></nomedadiretiva>`, nessa diretiva usamos o `template` ou `templateUrl`, que será explicado mais a frente.

### Link

O link é uma função que tem três parametros importantes, caso queiramos manipular a view.

```
.directive('nomedadiretiva', function(){
 return {
   link: function(scope, element, attribute){}
 }
})
```

* **scope**: Se ao olhar o scope, lembrar do $scope da `controller`, fica tranquilo que o `scope` da diretiva tem a mesma responsabilidade.
    O `scope` da diretiva consegue acessar o `$scope` da controller, mas a controller não consegue acessar o `scope` da diretiva. O que tem de bom nisso? Conseguimos isolar variáveis da diretiva e trabalhar num ambiente que não tenha conflitos.
* **element**: O element é usado para acessar o html em forma de objeto, se estivermos usando a diretiva como atributo `restrict: 'A'`, quando damos `console.log`, retornamos o exatamente os dados da tag que adicionamos a diretiva. Na diretiva `restrict: 'E'`, iremos retorna todo o html que setamos no campo `template` ou `templateUrl`.
* **attribute**: O attribute é responsável por acessar os atributos da tag que estamos manipulando com o `restrict: 'A'`, podemos acessar o id através de `attribute.id`, class `attribute.class` e etc.