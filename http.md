## Http

O $http faz parte do core do angularjs, ele facilita a comunicação com servidores remotos via ajax ou JSONP.

Podemos usar o $http de duas formas, a primeira forma é passar num objeto, os parâmetros de onde iremos enviar ou receber os dados. O $http retorna um promise com dois metodos, then e catch.

Veja o exemplo

```
$http({
 url: '/api/listaitens',
 method: 'GET',
 headers: {},
 data: {}
})
.then(fn)
.catch(fn)
```
Nota: fn é abreviação de `function(){}`.

Essa maneira é mais verbosa, ou seja, precisamos passar muitas informações para fazer algo simples, então vamos simplificar.

Podemos utilizar $http.verbo, o $http suporta os verbos `get, post, put, delete, patchs, head'.

Veja o exemplo

```
$http.get('/api/listaitens')
.then(fn)
.catch(fn)
```

Conseguimos simplificar bem, e onde podemos utilizar o $http? O recomendado é sempre utilizar num serviço `factory`, para separar a responsabilidade e deixar a controller somente para receber os dados vindo da `factory()`.

Vamos criar o CRUD via $http para uma ApiRest, usaremos o `get, post, put e delete`, a url será `api.exemplo.com`.

## GET

Veja abaixo para fazer a listagem de dados, será o R do CRUD.
```
$http.get('api.exemplo.com/produtos').then(function(data){
  console.log(data) //retorna todos os produtos;
});
```

Veja abaixo para fazer a listagem de apenas um item, será o R do CRUD.
```
$http.get('api.exemplo.com/produto/1').then(function(data){
  console.log(data) //retorna apenas um item;
});
```
## POST

Veja abaixo para fazer cadastro de um produto, será o C do CRUD.
```
var dadosenviados = {
 nome: 'Produto a',
 quantidade: 123
};

$http.post('api.exemplo.com/produtos', dadosenviados).then(function(data){
  console.log(data) //após inserir o produto, a api irá retornar um OK
});
```
## PUT
Veja abaixo para fazer a atualização de um array, será o R do CRUD. Nesse caso, precisamos passar somente o id do produto que queremos alterar algo e o back end faz essa alteração

```
$http.put('api.exemplo.com/produto/1', ).then(function(data){
  console.log(data) //retorna apenas um item;
});
```
## DELETE
Veja abaixo para fazer a exclusão de um produto, será o D do CRUD.
```
$http.delete('api.exemplo.com/produto/1', ).then(function(data){
  console.log(data) //exclui apenas um item;
});
```