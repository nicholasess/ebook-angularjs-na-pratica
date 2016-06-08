
### $routeParams

O $routeParams é uma funcionaldade muito importante para a utilização de rotas. A aplicação não é composta somente por rotas que fazem listagem de dados, ela tem também rotas que indicam a visualização de apenas um item e como fazemos isso?

Veja o exemplo

```
.config(function($routeProvider){
	$routeProvider	
	.when('/itens', {
		templateUrl: 'views/itens.html',
		controller:'ItensCtrl'
	})
	
	.when('/item/:id', {
		templateUrl: 'views/item.html',
		controller:'ItemCtrl'
	})

	.otherwise({redirectTo:'/'});
})
```
Na rota `/itens` listamos todos os itens e na rota `/item/:id` iremos listar somente um item. O `:id`representa um id referente ao item da lista e é possivel pegar através do $routeParams.id.

Veja o exemplo

```
.config(function($routeProvider){
	$routeProvider	
	.when('/itens', {
		templateUrl: 'views/itens.html',
		controller:'ItensCtrl'
	})
	
	.when('/item/:id', {
		templateUrl: 'views/item.html',
		controller:'ItemCtrl'
	})

	.otherwise({redirectTo:'/'});
})

.controller('ItemCtrl', function($routeParams){
  console.log($routeParams.id);
})
```
Se acessarmos a rota `/item/1`, irá aparecer 1 no console do browser.

