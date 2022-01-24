# Fake API Hamburgueria

Essa é o repositório de uma fake API criada pelo JSON-Server + JSON-Server-Auth , com o objetivo de explorar as funcionalidades do JSON-server criando um site onde o usuário pode adicionar produtos em seu carrinho.

## **Endpoints**

A API tem um total de 9 endpoints, tendo uma atenção para o usuário, que poderá cadastrar seu perfil,visualizar a listagem de produtos e podendo adicionar ao carrinho.

Url base da API: https://hamburgueria-kenzie-matheus.herokuapp.com/

<h2 align = 'center'> Listar produtos </h2>

Nessa API o usuário consegue visualizar todos os produtos disponíveis, se estiver logado e com autenticação.
Pode-se visualizar desta forma:

`GET /products - FORMATO DA RESPOSTA - STATUS 200`

```json
[
  {
    "id": 1,
    "name": "Hamburguer",
    "category": "Sanduíches",
    "price": 14,
    "img": "https://i.ibb.co/fpVHnZL/hamburguer.png"
  },
  {
    "id": 2,
    "name": "X-Burguer",
    "category": "Sanduíches",
    "price": 16,
    "img": "https://i.ibb.co/djbw6LV/x-burgue.png"
  }
]
```

Podemos acessar um produto em específico utilizando o endpoint:
`GET /products/:id FORMATO DA RESPOSTA - STATUS 200`

```json
{
  "id": 2,
  "name": "X-Burguer",
  "category": "Sanduíches",
  "price": 16,
  "img": "https://i.ibb.co/djbw6LV/x-burgue.png"
}
```

<h2 align ='center'>Criação de usuário</h2>

### Cadastro

`POST /register - FORMATO DA REQUISIÇÃO`

Para a criação de usuário, é necessário os campos e-mail e password.

```json
{
  "email": "teste@mail.com",
  "name": "matheus",
  "password": "123456"
}
```

### Login

`POST /login - FORMATO DA REQUISIÇÃO`

```json
{
  "email": "teste@mail.com",
  "password": "123456"
}
```

<h2 align = 'center'>Carrinho</h2>

## Listagem do carrinho

É necessário que o usuário esteja logado e tenha o token de autorização no cabeçalho da requisição.
A listagem do carrinho incluíra os produtos adicionados por todos os usuários.
`GET /cart - FORMATO DA REQUISIÇÃO`

```json
[
  {
    "id": 1,
    "name": "X-Burguer",
    "category": "Sanduíches",
    "price": 16,
    "img": "https://i.ibb.co/djbw6LV/x-burgue.png",
    "quantity": 2,
    "userId": 6
  },
  {
    "id": 2,
    "name": "Milk Shake",
    "category": "Sobremesa",
    "price": 6,
    "img": "https://i.ibb.co/djbw6LV/milk-shake.png",
    "quantity": 6,
    "userId": 2
  }
]
```

## Listagem de carrinho específico

É necessário que o usuário esteja logado,tenha o token de autorização no cabeçalho da requisição, e o id do usuário na utilização do querys params.

`GET /cart?userId=:userId - FORMATO DA REQUISIÇÃO`

```json
[
  {
    "id": 1,
    "name": "X-Burguer",
    "category": "Sanduíches",
    "price": 16,
    "img": "https://i.ibb.co/djbw6LV/x-burgue.png",
    "quantity": 2,
    "userId": 6
  },
  {
    "id": 2,
    "name": "Big Kenzie",
    "category": "Sanduíches",
    "price": 13,
    "img": "https://i.ibb.co/djbw6LV/big-kenzie.png",
    "quantity": 1,
    "userId": 6
  }
]
```

## Adicionar ao carrinho

`POST /cart - FORMATO DA REQUISIÇÃO`
Primeiramente é necessário que o usuário esteja logado, com o token no cabeçalho da requisição.
É obrigatório um campo onde contenha o id do usuário.

```json
{
  "name": "X-Burguer",
  "category": "Sanduíches",
  "price": 16,
  "img": "https://i.ibb.co/djbw6LV/x-burgue.png",
  "userId": 6
}
```

## Editar produto no carrinho

Primeiramente é necessário que o usuário esteja logado, com o token no cabeçalho da requisição, este endpoint é para atualizar quaisquer informações que foram inseridas na postagem de um produto ao carrinho.

`PATCH /cart/:id - FORMATO DA REQUISIÇÃO`

É obrigatório que tenha um campo fornecendo o id do usuário:

```json
{
  "quantity": 2,
  "userId": 5
}
```

## Deletar produto do carrinho

Primeiramente é necessário que o usuário esteja logado, com o token no cabeçalho da requisição, este endpoint é para deletar um produto do carrinho.

`DELETE /cart/:id - FORMATO DA REQUISIÇÃO`
