## Diretivas customizadas

Diretiva customizada veio para facilitar a criação de componentes, que muitas vezes são reutilizados em diversas páginas da aplicação.

Esses componentes são criados através da função `.directive()`, podemos gerar atributos, elementos, comentários e classes. Dentro da função, passamos dois parametros. O primeiro é o nome e o segundo é uma função. 

Uma coisa importante sobre o nome da diretiva, é entender como o angular traduz o nome composto. Se colocarmos um nome todo minusculo ('nomedadiretiva'), o angular vai entender como 'nomedadiretiva', caso o nome seja ('nomeDaDiretiva'), o angular vai entender como 'nome-da-diretiva'.

Dentro da função que passamos no `.directive()`, precisamos retornar variáveis com valores que informam ao angular, o que a tal diretiva faz.

As duas principais são `restrict` e `link`, a `restrict` é tipo da diretiva.

* 'A' para atributo.
* 'E' para elementos.
* 'C' para classes.
* 'M' para comentários.

Caso não informamos nada, o angular irá usar a diretiva como atributo `A`.

Irei explicar as duas mais utilizadas (atributo e elemento). 

### Atributo

Você conhece o atributo **class** e **id** que incluimos nas tags para estilizarmos o html? Pois bem, é nessa linha de raciocinio, mas podemos fazer muito mais do que estilizar o html, como ouvir clicks e/ou eventos do teclado.

Iremos criar um atributo chamado `ouvir-click` e ele irá escutar os clicks de um botão.

```
angular.module('App')
.directive('ouvirClick', function(){
 return {
   restrict: 'A',
   link: function(scope, element){
     element.bind('click', function(){
       console.log('clicou');
     })
   }
 }
})
```
Dentro da função do `directive()`, retornamos um objeto com as variáveis (restrict e link), repare na variável link, ela tem uma função com dois parametros (scope e element). O **scope** representa o acesso as informações da view através da expressão regular `{{}}` e o **element**, no caso de diretivas que são atributos `A`, representa a tag que a diretiva se encontra, como o exemplo abaixo.
```
<button ouvir-click>Clique Aqui</button>
```

Se fizermos um `console.log(element)`, irá retornar todas as propriedades da tag `button`.

Usamos o `.bind` para escutar os eventos que o `button` fará, neste caso, estamos escutando o evento `click`, que ao clicar, o angular fará um `console.log` com o valor `clicou`.

Veja o exemplo [neste link](http://jsbin.com/nelosi/edit?html,js,console,output).

