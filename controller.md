## Controladores

No angular, controller é um meio de comunicação entre a view e toda a regra de negócio que temos numa tela.

Para criarmos uma controller, precisamos chamar a função `.controller()` e adicionar dois parametros dentro. O primeiro é o nome da controller entre aspas e o segundo é uma função.

```
angular.module('App')
.controller('nome_da_controller', function($scope){})
```
### Variável

O parametro `$scope` dentro da função, é um ponteiro que liga as variáveis que iremos adicionar, dentro do escopo referente a controller.

Ex:

```
angular.module('App')
.controller('nome_da_controller', function($scope){
  $scope.name = "Nicholas";
})
```
```
<div ng-app="App" ng-controller="nome_da_controller">
<p>Olá {{name}}</p>
</div>
```
O resultado esperado é `Olá Nicholas`, 
Para visualizar o exemplo em funcionamento, basta clicar [nesse link](http://jsbin.com/jededitiqi/edit?html,js).


### Função

Podemos criar funções no angular, com o objetivo de ser executado depois de uma ação do usuário.

Para fazer essa proesa, basta criar uma variavel e adicionar uma função nela.

```
angular.module('App')
.controller('nome_da_controller', function($scope){
  $scope.olaMundo = function(){
     console.log('Ola Mundo');
  }
})
```
```
<div ng-app="App" ng-controller="nome_da_controller">
<button ng-click="olaMundo()">Clique</button>
</div>
```
Quando iniciar a página, clique no botão chamado **clicar** e veja o console do **browser**.
O resultado está [neste link](http://jsbin.com/yofeqi/edit?html,js,console,output).

PS: o ng-click é uma diretiva do angular que executa funções e lógica que estive dentro do escopo `="olaMundo()"` ou `="name = 'Nicholas'"` dela.






