## Http

O $http faz parte do core do angularjs, ele facilita a comunicação com servidores remotos via ajax ou JSONP.

Podemos usar o $http de duas formas, a primeira forma é passar num objeto, os parâmetros de onde iremos enviar ou receber os dados. O $http um promise com dois metodos, success e error.

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

Podemos utilizar $http.verbo, o $http suporte os verbos `get, post, put, delete, patchs, head'.

Veja o exemplo

```
$http.get('/api/listaitens')
.success(fn)
.error(fn)
```

Conseguimos simplificar bem e aonde podemos utilizar o $http? O recomendado é sempre utilizar num serviço `factory` para separar a responsabilidade e deixar a controller somente para receber os dados vindo da `factory()`.
