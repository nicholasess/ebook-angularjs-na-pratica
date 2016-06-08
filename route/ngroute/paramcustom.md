#### Parametros Customizados

Sabe quando precisamos adicionar parametros na rota que usam essa sintaxe `?param1&param2`?

A solução é adicionar na `url:` os valores depois que setamos a estrutura dela, veja abaixo:

```
```
.config(function($routeProvider){
	$routeProvider	
	.when('/itens?param1&param2', {
		templateUrl: 'views/itens.html',
		controller:'ItensCtrl'
	})

	.otherwise({redirectTo:'/'});
})

.controller('ItensCtrl', function($routeParams){
  console.log($routeParams.param1, $routeParams.param2);
})
```
Se acessarmos a rota `/itens?param1=1&param2=2`, o retorno no consoel será `1` referente ao param1 e `2` referente ao param2.
