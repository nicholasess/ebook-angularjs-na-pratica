## ngRoute

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

O primeiro parâmetro da função `.when()` é o `'/'`, indicando a rota principal da aplicação e o segundo parâmetro com o campo template e controller. O campo template recebe tags htmls, mas como fazemos pra indicar o caminho até um arquivo HTML?

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

A função `otherwise` recebe um `objeto` que contém o campo `redirectTo`, o valor desse campo será a rota que a aplicação ira redirecionar, caso tentem acessar uma rota inexsistente.

Veja o exemplo:

```
.config(function($routeProvider){
	$routeProvider	
	.when('/', {
		templateUrl: 'views/main.html',
		controller:'MainCtrl'
	})	

	.otherwise({redirectTo:'/'});
})
```

Nota: Não é de responsabilidade do módulo de rotas, redirecionar para rotas, caso haja erros https (404, 500, 400 e etc). No capítulo `Http` iremos tratar isso de forma correta.

Para funcionar, precisamos setar no arquivo html principal da aplicação a diretiva chamada `ng-view`, onde essa diretiva estiver, será carregado via ajax os arquivos html que estão setados no templateUrl de cada rota.

Geralmente utilizamos o arquivo `index.html` como arquivo príncipal para a aplicação `angular`, como modelo `SPA` (Single Page Aplication).
Para utilizarmos o `ngRoute`, precisamos inicializa-lo dentro do `body` do arquivo `index.html` sendo uma tag `<ng-view></ng-view>` ou um atributo numa tag `<div ng-view></div>`. Se você bootstrap por exemplo, poderia adicionar o atributo `ng-view` dentro de uma `div` que deixará  centralizado as views, veja abaixo:

```

<!DOCTYPE html>
<html>
<head>
    <title></title>
</head>
<body>
<div class="container" ng-view></div>
</body>
</html>
``` 

Somente o arquivo principal precisa conter as tags `html` e `body`, os arquivos que compõem cada rota, basta somente as tags `html referente ao funcionamento da view.