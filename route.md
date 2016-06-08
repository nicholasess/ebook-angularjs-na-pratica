
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

### Resolve

O resolve é uma funcionalidade dos módulos de rotas, que tem como objetivo, carregar informações antes que a view seja carregada. 
Quando o usuário acessa uma rota que lista diversos itens e não queremos que essas informações sejam carregadas no momento da exibição da view, usamos o resolve.

Veja o exemplo

```
.config(function($routeProvider){
	$routeProvider	
	.when('/lista', {
		templateUrl: 'views/main.html',
		controller:'MainCtrl',
		resolve: {
		  Lista: function($http){
		    return $http.get('api/listadeitens');
		  }
		}
	});	
});

.controller('MainCtrl', function(Lista){
  $scope.itens = Lista();
});
```

Como podemos perceber na função config que define as rotas, na rota `/lista` temos o resolve, basicamente é um objeto que tem dentro, várias funções com as informações pré carregadas.

O jeito correto é não deixar a responsabilidade na resolve em retornar informações da API, ou seja, essa informação tem que vim de um serviço.

```
.factory('Api', function($http){
  var api = {};
  
  api.listadeitens = function(){
    return $http.get('api/listadeitens');
  }
  
  return api;
})

.config(function($routeProvider){
	$routeProvider	
	.when('/lista', {
		templateUrl: 'views/main.html',
		controller:'MainCtrl',
		resolve: {
		  Lista: function(Api){
		    return Api.listadeitens();
		  }
		}
	});	
});

.controller('MainCtrl', function(Lista){
  $scope.itens = Lista();
});
```

Assim caso algo mude, iremos nos preocupar apenas em mudar na factory. 

Para saber mais, baixe o repositório com um exemplo nesse [link](https://github.com/nicholasess/examples-angularjs-na-pratica/tree/master/rotas/ngRoute)

### $locationChangeStart e $locationChangeSuccess

Essas duas variaveis são eventos e usadas no `$rootScope.$on()` dentro do `.run()`, que é iniciado antes da aplicação, podemos dizer que aqui, é aonde a mágica acontece.

O `$locationChangeStart` é um evento que 'ouve' o inicio da aplicação, nesse cara que podemos criar validações para acesso de determinadas rotas, nossa regra de negócio.

O `$locationChangeSuccess` já é ao contrário, ele 'ouve' quando a aplicação já está estabilizada, quando a view está renderizada e etc.

