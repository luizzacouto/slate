---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - ruby
  - python
  - javascript

includes:
  - errors
  - suporte

search: true
---

# Olá, desenvolvedor.

## O que dá para fazer com a API?

Com a nossa API você será capaz de integrar qualquer sistema externo ao Edools, realizar migrações de dados de plataformas antigas de maneira simples e direta, e construir aplicativos para estender uma funcionalidade existente ou até mesmo criar novas funcionalidades com sua lógica própria.

Através da API você tem toda a flexibilidade necessária para adaptar o Edools às suas regras de negócio, tendo uma plataforma de ensino online que se encaixe perfeitamente às suas necessidades.

## Representação dos dados

A API tem em seu cerne o fato de ser uma API JSON, ou seja, JSON é único formato suportado. Em seguido iremos expor os principais padrões adotados que suportam o esquema da API.

### Representação de Listas

Ao requisitar uma lista de um determinado produto, a resposta inclui um subconjunto dos atributos daquele recurso. Isso é o que chamamos de representação resumida do recurso. O principal motivo é o fato de alguns atributos serem computacionalmente caros de serem fornecidos em grandes quantidades. Então, visando a performance como um todo, esse formato reduzido exclui esses atributos. Para obtê-los, basta requisitar a representação detalhada.

Por exemplo, ao realizar um requisição para obter a lista de produtos, você receberá a representação resumida dos produtos.

### Representação Detalhada

No caso de requisitar um objeto específico de um recurso, a resposta irá retornar por padrão a representação detalhada desse recurso. Tal formato inclui todos os atributos daquele recurso. A única observação é que alguns atributos podem ser escondidos por motivos de permissões.

Ao descrevermos cada método da API, será fornecida os atributos da representação detalhada dos recursos.

### Campos vazios

Campos vazios, ou nulos, são retornados como null ao invés de serem omitidos.

### Timestamps

Todas as timestamps são retornadas no seguinte formato: `YYYY-MM-DDTHH:MM:SSZ`

## Paginação

Requisições que retornam múltiplos items são paginadas por padrão para retornar apenas `10 itens`. Você pode especificar as páginas através do parâmetro `page`.

Para alguns recursos você também pode especificar o tamanho da página até o limite de 100 itens, usando o parâmetro `per_page`.

Observe que por razões técnicas, nem todos os recursos aceitam o parâmetro `per_page`.

Abaixo um exemplo:

`
$ curl 'https://sua-escola.myedools.com/api/school_products?page=2&per_page=100'
`

<aside class="notice">
A paginação é 1-based, ou seja, a primeira página é a 1. Ao omitir o parâmetro page, sempre será retornado a primeira página.
</aside>


## Endpoint

A URL base onde se encontra a raiz da nossa API é:

`https://sua-escola.myedools.com/api`

Todo o acesso à nossa API é feito usando o protocolo HTTPS, sem exceção, com dados criptografados para maior segurança.


## Versionamento

Por padrão, todas as requisições para a API que não especificarem um versão serão redirecionadas para a última versão da API, que no momento é a v1.

Por esse motivo, nós recomendamos que sempre explicite a versão que você deseja, mesmo se estiver usando a última versão. Dessa forma, quando futuras atualizações ocorrerem, sua aplicação estará requisitando a versão correta. Basta informar a versão no header da requisição:

`Accept: application/vnd.edools.core.v1+json`

## Autorização

> Para realizar a autorização utilize:

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('Token token="CREDENTIALS"')
```

```python
import kittn

api = kittn.authorize('Token token="CREDENTIALS"')
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('Token token="CREDENTIALS"');
```

Ao fazer um requisição para a API, ela irá passar por um processo de autenticação e autorização. A primeira verifica se as credencias que você tem são válidas para ter acesso à API. A segunda verifica se tais credenciais tem permissão para acessar o dado, ou conjunto de dados, solicitado.

O modelo responsável por gerenciar essa lógica na API é o `ApiKey`. Cada ApiKey possui um `token` e um `secret`, que são gerados automaticamente na sua criação, e combinados formam o que chamamos de `credentials`.

Além deles, a ApiKey possui um Owner e um Realm.

Owner | Realm
--------- | ------- | -----------
O owner define o User ou App a quem pertence àquela chave. | O Realm indica qual o domínio da API a chave terá acesso, que no geral são sempre Organization ou School.

No momento o único formato aceito para se autenticar na API é passando o seguinte header na chamada:

`Authorization: Token token="CREDENTIALS"`

<aside class="notice">
Você deve substituir <code>CREDENTIALS</code> pela sua chave de API.
</aside>

# Atividades

## [GET] Listagem de todas as atividades de um curso

Get a list of course's activities
### HTTP Request

`GET /courses/:course_id/activities or /school_products/:school_product_id/activities or /enrollments/:enrollment_id/activities`

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

### Parâmetros

Nome | Tipo | Descrição
--------- | ------- | -----------
course_id | Integer | Identifier of the course

## [GET] Exibição de uma atividade

View a activity

### HTTP Request

`GET /activities/:id /school_products/:school_product_id/activities/:id or /enrollments/:enrollment_id/activities/:id`

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

### Parâmetros

Nome | Tipo | Descrição
--------- | ------- | -----------
activity_id | Integer | Identifier the activity

## [POST] Criar atividades

Create activity.

### HTTP Request

`POST /activities`

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

### Parâmetros

Nome | Tipo | Descrição
--------- | ------- | -----------
activity | Hash | The activity to create
activity[title] | String | Title of the activity
activity[type] | String | Type of the activity
activity[show_comments] | String | Accept "always" and "approved". It is a view helper.
activity[title] | exam_lesson_id | Lesson of the activity
