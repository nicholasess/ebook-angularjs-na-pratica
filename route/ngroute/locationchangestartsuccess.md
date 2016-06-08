### $locationChangeStart e $locationChangeSuccess

Essas duas variaveis são eventos e usadas no `$rootScope.$on()` dentro do `.run()`, que é iniciado antes da aplicação, podemos dizer que aqui, é aonde a mágica acontece.

O `$locationChangeStart` é um evento que 'ouve' o inicio da aplicação, nesse cara que podemos criar validações para acesso de determinadas rotas, nossa regra de negócio.

O `$locationChangeSuccess` já é ao contrário, ele 'ouve' quando a aplicação já está estabilizada, quando a view está renderizada e etc.

