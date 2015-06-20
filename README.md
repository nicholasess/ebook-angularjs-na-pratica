## Introdução

O objetivo desse e-book, é mostrar como o AngularJs é um fácil de se aprender e quão poderoso ele é.

O AngularJs é um framework JavaScript para o front end, o design pattern dele é MVC ou MVVM. 

Nesse e-book iremos utilizar o MVC como padrão, para quem não conhece, MVC significa Model View Control. O model é responsável por se comunicar com o mundo externo, seja acessando Apis ou arquivos, ele é representado pelos services no angular. O view é responsável pela exibição dos dados que são enviados pela controller, a view é representada pelo html. A control é responsável por gerenciar os dados que são enviados pela view ou retornados da model, é representada pelas controllers.

Esse ecossistema de inicio pode ser complexo pra quem não sabe como funciona na prática o MVC, mas com o tempo a lógica vai fluindo, pois o fluxo de informações sempre será para a maioria das coisas que fazemos em um sistema, ou seja, sempre fazemos o CRUD (Create, Read, Update e Delete) das informações.

Com o MVC iremos utilizar rotas, elas são responsáveis por ditar qual será o arquivo html e controller que irão conversar numa determinada rota. Digamos estamos fazendo um sistema de escola e precisamos listar todos os alunos, certamente precisamos de um arquivo html com uma tabela, na controller teremos uma lista (array) para listarmos esse conteúdo na tabela ou essa lista é retornada de um service.

