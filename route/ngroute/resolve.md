
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

