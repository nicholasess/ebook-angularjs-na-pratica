## Controllers

No angular, controller é um meio de comunicação entre a view e toda a regra de negócio que temos numa tela.

Para criarmos uma controller, precisamos chamar a função `.controller()` e adicionar dois parametros dentro. O primeiro é o nome da controller entre aspas e o segundo é uma função.

```
angular.module('App')
.controller('nome_da_controller', function($scope){})
```
O parametro `$scope` dentro da função, é um ponteiro para as variáveis que iremos adicionar dentro do escopo referente a controller.

Ex:

```
<div ng-controller="nome_da_controller">
<p>Olá {{name}}</p>
</div>
```
```
angular.module('App')
.controller('nome_da_controller', function($scope){
  $scope.name = "Nicholas";
})
```
O resultado esperado é `Olá Nicholas`



