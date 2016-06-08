# Rotas

As rotas são responsáveis por informar ao angular, qual template html e controller serão responsáveis por uma determinada rota que o usuário acessar.

Para utilizar um módulo de rotas especifico, precisamos colocar o nome do módulo dentro das dependencias do módulo principal da aplicação.

Veja abaixo

```
angular.module('App', ['ngRoute']);
```

O módulo será inicializado e utilizado dentro da função .config(), do módulo principal da aplicação.