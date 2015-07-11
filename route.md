## Rotas

As rotas são responsáveis por informar ao angular, qual template html e controller serão responsáveis por uma determinada rota que o usuário acessar.

Para utlizar um módulo de rotas especifico, precisamos colocar o nome do módulo dentro das dependencias do módulo principal da aplicação.

Ele será inicializado e utilizado dentro da função .config(), do módulo principal da aplcação.

Na versão 1.3 do angular, temos dois módulos focados em rotas, um é o ngRoute e o outro é o ui-route.

### ngRoute

O módulo responsável pelas rotas, se chama `ngRoute`, ele é uma dependência, ou seja, um módulo externo que precisa ser inserido no arquivo principal.

A variável que precisa ser chama na função `.config()`, se chama `$routeProvider`, essa variável tem a função `.when()`, que seta as rotas e suas configurações e o `otherwise()`, que indica qual rota que a aplicação deve redirecionar, caso tentem acessar uma rota inexistente.

A função `.when()` recebe dois parâmetros, o primeiro parâmetro é a rota e o segundo é um objeto que contém dois campos, o primeiro é o campo indica o template HTML e o segundo indica a controller.

Veja o exemplo abaixo.
```
.config(function($routeProvider){
	$routeProvider
	.when('/', {
		template: '<h1>Oi Galera</h1>',
		controller:'MainCtrl'
	});	
})
```

O primeiro parâmetro da função `.when()` é o '/', indicando a rota principal da aplicação e o segundo parâmetro com o campo template e controller. O campo template recebe tags htmls, mas como fazemos pra indicar o caminho até um arquivo HTML?

Precisamos trocar esse campo pelo templateUrl, ficando assim:

```
.config(function($routeProvider){
	$routeProvider
	.when('/', {
		templateUrl: 'views/main.html',
		controller:'MainCtrl'
	});	
})
```

Você verá o template ou templateUrl nos módulos de rotas e no uso de diretiva.

A função `otherwise` recebe um `objeto` que contém o campo redirectTo, o valor desse campo será a rota que a aplicação ira redirecionar, caso tentem acessar uma rota inexsistente.

Veja o exemplo:

```
.config(function($routeProvider){
	$routeProvider	
	.when('/', {
		templateUrl: 'views/main.html',
		controller:'MainCtrl'
	});	

	.otherwise({redirectTo:'/'});
})
```

Nota: Não é de responsabilidade do módulo de rotas, redirecionar para rotas, caso haja erros https (404, 500, 400 e etc). No capítulo `Http` iremos tratar isso de forma correta.

Para funcionar, precisamos setar no arquivo html principal da aplicação a diretiva chamada `ng-view`, onde essa diretiva estiver, será carregado os arquivos html que estão setados no templateUrl de cada rota.

Somente o arquivo principal precisa conter as tags `html` e `body`, os arquivos que compõem cada rota, basta somente as tags `html referente ao funcionamento da view.

#### $routeParams

O $routeParams é uma funcionaldade muito importante para a utilização de rotas. A aplicação não é composta somente por rotas que fazem listagem de dados, ela tem também rotas que indicam a visualização de apenas um item, e como fazemos isso?

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
	});

	.otherwise({redirectTo:'/'});
})
```
#### Resolve

O resolve é uma funcionalidade dos módulos de rotas, que tem como objetivo, carregar informações através de promises, antes que a rota seja trocada. 
Quando o usuário acessa uma rota que lista diversos itens e não queremos que essas informações sejam carregadas no momento da exibibição da view, usamos o resolve.

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

Como podemos perceber na função config que define as rotas, na rota `/lista` depois da controller, temos o resolve, a forma dele ser usado, é somente dessa maneira, sempre abaixo da controller. O resolve basicamente é um objeto que tem dentro, várias funções com os promises resolvidos, então quando estivermos na view, as informações já estarão carregadas.

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

Assim caso algo mude, iremos nos preocupamos apenas em mudar na factory.