## Http

O $http faz parte do core do angularjs, ele facilita a comunicação com servidores remotos via ajax ou JSONP.

Podemos usar o $http de duas formas, a primeira forma é passar num objeto, os parâmetros de onde iremos enviar ou receber os dados. O $http retorna um promise com dois metodos, success e error.

Veja o exemplo

```
$http({
 url: '/api/listaitens',
 method: 'GET',
 headers: {},
 data: {}
})
.success(fn)
.error(fn)
```
Nota: fn é abreviação de `function()`.

Essa maneira é mais verboso, ou seja, precisamos passar muitas informações para fazer algo simples, então vamos simplificar.

Podemos utilizar $http.verbo, o $http suporta os verbos `get, post, put, delete, patchs, head'.

Veja o exemplo

```
$http.get('/api/listaitens')
.success(fn)
.error(fn)
```

Conseguimos simplificar bem e aonde podemos utilizar o $http? O recomendado é sempre utilizar num serviço `factory`, para separar a responsabilidade e deixar a controller somente para receber os dados vindo da `factory()`.

Vamos criar o CRUD via $http para uma ApiRest, usaremos o `get, post, put e delete`, a url será `api.exemplo.com`.

Veja abaixo para fazer a listagem de dados, será o R do CRUD.
```
$http.get('api.exemplo.com/produtos').success(function(data){
  console.log(data) //retorna todos os produtos;
});
```
Veja abaixo para fazer cadastro de um produto, será o C do CRUD.
```
var dadosenviados = {
 nome: 'Produto a',
 quantidade: 123
};

$http.post('api.exemplo.com/produtos', dadosenviados).success(function(data){
  console.log(data) //após inserir o produto, a api irá retornar um OK
});
```
Veja abaixo para fazer a listagem de apenas um item, será o R do CRUD.
```
$http.get('api.exemplo.com/produto/1').success(function(data){
  console.log(data) //retorna apenas um item;
});
```
Veja abaixo para fazer a atualização de um array, será o R do CRUD.

```
var array = [{id: 1, nome: 'Produto C'}
$http.put('api.exemplo.com/produto/1', ).success(function(data){
  console.log(data) //retorna apenas um item;
});
```
