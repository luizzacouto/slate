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

## <img src="/images/get.png"> Listagem de todas as atividades de um curso

Get a list of course's activities
### HTTP Request

`GET /courses/:course_id/activities or /school_products/:school_product_id/activities or /enrollments/:enrollment_id/activities`

```ruby
EXEMPLO DE CHAMADA UTILIZANDO RUBY
```

```python
EXEMPLO DE CHAMADA UTILIZADO PHYTON
```

```javascript
EXEMPLO DE CHAMADA UTILIZANDO JS
```

> The above command returns JSON structured like this:

```json
[
  EXEMPLO DE JSON
]
```

### Parâmetros obrigatórios

Nome | Tipo | Descrição
--------- | ------- | -----------
course_id | Integer | Identifier of the course

## <img src="/images/get.png"> Exibição de uma atividade

View a activity

### HTTP Request

`GET /activities/:id /school_products/:school_product_id/activities/:id or /enrollments/:enrollment_id/activities/:id`

```ruby
EXEMPLO DE CHAMADA UTILIZANDO RUBY
```

```python
EXEMPLO DE CHAMADA UTILIZADO PHYTON
```

```javascript
EXEMPLO DE CHAMADA UTILIZANDO JS
```

> The above command returns JSON structured like this:

```json
[
  EXEMPLO DE JSON
]
```

### Parâmetros obrigatórios

Nome | Tipo | Descrição
--------- | ------- | -----------
activity_id | Integer | Identifier the activity

## <img src="/images/post.png"> Criar atividades

Create activity.

### HTTP Request

`POST /activities`

```ruby
EXEMPLO DE CHAMADA UTILIZANDO RUBY
```

```python
EXEMPLO DE CHAMADA UTILIZADO PHYTON
```

```javascript
EXEMPLO DE CHAMADA UTILIZANDO JS
```

> The above command returns JSON structured like this:

```json
[
  EXEMPLO DE JSON
]
```

### Parâmetros obrigatórios

Nome | Tipo | Descrição
--------- | ------- | -----------
activity | Hash | The activity to create
activity[title] | String | Title of the activity
activity[type] | String | Type of the activity
activity[show_comments] | String | Accept "always" and "approved". It is a view helper.
activity[title] | exam_lesson_id | Lesson of the activity

## <img src="/images/delete.png"> Excluir atividade

Delete activity.

### HTTP Request

`DELETE /activities/:id`

```ruby
EXEMPLO DE CHAMADA UTILIZANDO RUBY
```

```python
EXEMPLO DE CHAMADA UTILIZADO PHYTON
```

```javascript
EXEMPLO DE CHAMADA UTILIZANDO JS
```

> The above command returns JSON structured like this:

```json
[
  EXEMPLO DE JSON
]
```

### Parâmetros obrigatórios

Nome | Tipo | Descrição
--------- | ------- | -----------
id | Integer | Id of an activity

# Matrículas

## <img src="/images/get.png"> Listar a matrícula

View an enrollment.

### HTTP Request

`GET /enrollments/:id or /enrollments/:code?find_by=code`

```ruby
EXEMPLO DE CHAMADA UTILIZANDO RUBY
```

```python
EXEMPLO DE CHAMADA UTILIZADO PHYTON
```

```javascript
EXEMPLO DE CHAMADA UTILIZANDO JS
```

> The above command returns JSON structured like this:

```json
[
  EXEMPLO DE JSON
]
```

### Parâmetros obrigatórios

Nome | Tipo | Descrição
--------- | ------- | -----------
id | Integer | The identifier of the enrollment

## <img src="/images/get.png"> Listar todas as matrículas

View an enrollment.

### HTTP Request

`GET /enrollments or /students/:student_id/enrollments or /course_classes/:course_class_id/enrollments or /school_products/:school_product_id/enrollments`

```ruby
EXEMPLO DE CHAMADA UTILIZANDO RUBY
```

```python
EXEMPLO DE CHAMADA UTILIZADO PHYTON
```

```javascript
EXEMPLO DE CHAMADA UTILIZANDO JS
```

> The above command returns JSON structured like this:

```json
[
  EXEMPLO DE JSON
]
```

### Parâmetros obrigatórios

Nome | Tipo | Descrição
--------- | ------- | -----------
student_id | Integer | Identifier of the Student object (route dependence)
course_class_id | Integer | Identifier of the CourseClass object (route dependence)
school_product_id | Integer | Identifier of the SchoolProduct object (route dependence)

## <img src="/images/post.png"> Criar matrículas

Create an enrollment

### HTTP Request

`POST /enrollments`

```ruby
EXEMPLO DE CHAMADA UTILIZANDO RUBY
```

```python
EXEMPLO DE CHAMADA UTILIZADO PHYTON
```

```javascript
EXEMPLO DE CHAMADA UTILIZANDO JS
```

> The above command returns JSON structured like this:

```json
[
  EXEMPLO DE JSON
]
```

### Parâmetros obrigatórios

Nome | Tipo | Descrição
--------- | ------- | -----------
enrollment | Hash | The enrollment to create
enrollment[registration_id] | Integer | The identifier of the Registration object
enrollment[school_product_id] | Integer | The identifier of the SchoolProduct object
enrollment[max_attendance_type] | Integer | Enrollment type, can be indeterminate, time or attempts

Para criar um array de matrículas:

`POST /enrollments/batch`

## <img src="/images/put.png"> Atualizar matrículas

Create an enrollment

### HTTP Request

`PUT /enrollments/:id or /enrollments/:code?find_by=code`

```ruby
EXEMPLO DE CHAMADA UTILIZANDO RUBY
```

```python
EXEMPLO DE CHAMADA UTILIZADO PHYTON
```

```javascript
EXEMPLO DE CHAMADA UTILIZANDO JS
```

> The above command returns JSON structured like this:

```json
[
  EXEMPLO DE JSON
]
```

### Parâmetros obrigatórios

Nome | Tipo | Descrição
--------- | ------- | -----------
enrollment | Hash | The enrollment to create
enrollment[registration_id] | Integer | The identifier of the Registration object
enrollment[school_product_id] | Integer | The identifier of the SchoolProduct object
enrollment[max_attendance_type] | Integer | Enrollment type, can be indeterminate, time or attempts

### Parâmetros opcionais

Nome | Tipo | Descrição
--------- | ------- | -----------
enrollment[max_attendance_length] | Integer | Attendance length. Required if enrollment[max_attendance_type] is time or attempts
enrollment[status] |  String | Enrollment status, can be pending, active, expired, deactivated or canceled
enrollment[available_until] | DateTime | Date of enrollment's expiration. Required if enrollment[unlimited] is false
enrollment[created_at] |  DateTime | Date of enrollment's creation.
enrollment[activated_at] |  DateTime | Date of enrollment's activation.
enrollment[unlimited] | Boolean | Says if the enrollment is unlimited [true, false]
enrollment[code] |  String | Representation code of enrollment (uniq)
enrollment[time_spent] |  Integer | This param will be permitted by using an App's credential
enrollment[course_class_ids] |  Array<Integer> |An array of course classes ids to associate to the enrollment

# Usuários

## <img src="/images/get.png"> Listar alunos ou colaboradores

View list of all students or collaborators. This list is paginated and filtered if needed.

### HTTP Request

`GET /students or /collaborators`

```ruby
EXEMPLO DE CHAMADA UTILIZANDO RUBY
```

```python
EXEMPLO DE CHAMADA UTILIZADO PHYTON
```

```javascript
EXEMPLO DE CHAMADA UTILIZANDO JS
```

> The above command returns JSON structured like this:

```json
[
  EXEMPLO DE JSON
]
```

### Parâmetros opcionais

Nome | Tipo | Descrição
--------- | ------- | -----------
school_product_id | Array<Integer> | Student filter. Filter by school_product_id. Only users that have relations with some object with the id passed in the school_product_id will be in the list.
course_class_id | Array<Integer> | Student filter. Filter by course_class_id. Only users that have relations with some object with the id passed in the course_class_id will be in the list.
uninitiated_lesson_id | Array<Integer> | Student filter. Filter by uninitiated_leson_id. Only users that have relations with some object with the id passed in the uninitiated_leson_id will be in the list.
course_id | Array<Integer> | Student filter. Filter by course_id. Only users that have relations with some object with the id passed in the course_id will be in the list.
enrollment_status | Array<String> | Student filter. Filter by enrollmen_status. The available statuses are pending, active, expired, deactivated and canceled.
status  | Array<String> | Student filter. Filter by status
progress | Float | Student filter. Filter by progress. If used together with school_product_idòr it will return only students that have that progress in the products selected. *Important*: when this filter is used theprogress>=andprogress<=` will be ignored!
progress>= | Float | Student filter. Filter students that have progress equal or greater than the progress given. If used together with school_product_id it will return only students that have that progress in the products selected. This filter can be used together with progress<=.
progress<= | Float | Student filter. Filter students that have progress equal or less than the progress given. If used together with school_product_id it will return only students that have that progress in the products selected. This filter can be used together with progress<=.
completed_progress_at>= | DateTime | Student filter. Filter students that have completed the progress at the given DateTime or after that. If used together with school_product_id it will filter by students that completed the progress in those courses.
completed_progress_at<= | DateTime | Student filter. Filter students that have completed the progress at the given DateTime or before that. If used together with school_product_id it will filter by students that completed the progress in those courses.
enrolled_at>= | DateTime | Student filter. Filter students that have activated an enrollment at the given DateTime or after that. If used together with school_product_id it will filter by students that activated an enrollment in those courses.
enrolled_at<= | DateTime | Student filter. Filter students that have activated an enrollment at the given DateTime or before that. If used together with school_product_id it will filter by students that activated an enrollment in those courses.
last_progress_updated_at>=  | DateTime | Student filter. Filter students that have did some progress at the given DateTime or after that. ps: Some school's actions does not generate progress. If used together with school_product_id it will filter by students that have progresses in those courses.
last_progress_updated_at<=  | DateTime | Student filter. Filter students that have did some progress at the given DateTime or before that. ps: Some school's actions does not generate progress. If used together with school_product_id it will filter by students that have progresses in those courses.
ids | String | Filter by id. Return the users with the passed ids.
full_name | String | Filter by full_name. This is an espcial filter, with it you can pass any group of chars, the filter will select the users that the fullname or the email includes those chars.
sort  | String |Filter to sort the users by an attribute
direction | String |Filter to indicate the sort direction. It can be asc ou desc

## <img src="/images/post.png"> Criar alunos ou colaboradores

Create student or collaborator

### HTTP Request

`POST /students/ or /collaborators/`

```ruby
EXEMPLO DE CHAMADA UTILIZANDO RUBY
```

```python
EXEMPLO DE CHAMADA UTILIZADO PHYTON
```

```javascript
EXEMPLO DE CHAMADA UTILIZANDO JS
```

> The above command returns JSON structured like this:

```json
[
  EXEMPLO DE JSON
]
```

### Parâmetros obrigatórios

Nome | Tipo | Descrição
--------- | ------- | -----------
user | Hash | The user to create
user[first_name] | String | User first name
user[email] | String | User email that should be uniq
user[password] | String | Should be greater than 6 chars
user[password_confirmation] | String | Should be equal the password


### Parâmetros opcionais

Nome | Tipo | Descrição
--------- | ------- | -----------
user[last_name] | String | User last name
user[username]  | String | Nickname
user[cpf] | String | CPF
user[rg]  | String | RG
user[phone] | String
user[extra_phone] | String
user[skype] | String
user[twitter] | String
user[facebook]  | String
user[company_name]  | String
user[company_position]  | String
user[born_at] | DateTime
user[biography] | String
user[cover_image_url] | String
user[created_at] | DateTime | Exists only for Student. It overwrites the default created_at, normally used to migrate old students.
user[last_sign_in_at] | DateTime | Exists only for Student
user[role_ids]  | Array<Integer> | Roles to associate to the User
user[address_attributes] | Hash
user[address_attributes][id] | Integer |If not present it will create a new address
user[address_attributes][street]  | String | It will update the attribute if the user[address_attributes][id] is present
user[address_attributes][number] | Integer | It will update the attribute if the user[address_attributes][id] is present
user[address_attributes][complement]  | String | It will update the attribute if the user[address_attributes][id] is present
user[address_attributes][city]  | String | It will update the attribute if the user[address_attributes][id] is present
user[address_attributes][state] | String | It will update the attribute if the user[address_attributes][id] is present
user[address_attributes][zip_code]  | String | It will update the attribute if the user[address_attributes][id] is present
user[address_attributes][district]  | String | It will update the attribute if the user[address_attributes][id] is present

## <img src="/images/post.png"> Atualizando um aluno ou colaborador

Update student or collaborator

### HTTP Request

`PUT /students/:id or /collaborators/:id`

```ruby
EXEMPLO DE CHAMADA UTILIZANDO RUBY
```

```python
EXEMPLO DE CHAMADA UTILIZADO PHYTON
```

```javascript
EXEMPLO DE CHAMADA UTILIZANDO JS
```

> The above command returns JSON structured like this:

```json
[
  EXEMPLO DE JSON
]
```

### Parâmetros obrigatórios

Nome | Tipo | Descrição
--------- | ------- | -----------
user | Hash | The user to create
user[first_name] | String | The identifier of the Registration object
user[email] | String | The identifier of the Registration object
user[password] | String | The identifier of the SchoolProduct object
user[password_confirmation] | String | Enrollment type, can be indeterminate, time or attempts

## <img src="/images/delete.png"> Excluir aluno ou colaborador

Destroy a student or collaborator

### HTTP Request

`DELETE /students/:id or /collaborators/:id
`

```ruby
EXEMPLO DE CHAMADA UTILIZANDO RUBY
```

```python
EXEMPLO DE CHAMADA UTILIZADO PHYTON
```

```javascript
EXEMPLO DE CHAMADA UTILIZANDO JS
```

> The above command returns JSON structured like this:

```json
[
  EXEMPLO DE JSON
]
```

### Parâmetros obrigatórios

Nome | Tipo | Descrição
--------- | ------- | -----------
id | Integer | Id of user

# Produtos

## <img src="/images/get.png"> Listar produtos

Get a list of school_products

### HTTP Request

`GET /school_products`

```ruby
EXEMPLO DE CHAMADA UTILIZANDO RUBY
```

```python
EXEMPLO DE CHAMADA UTILIZADO PHYTON
```

```javascript
EXEMPLO DE CHAMADA UTILIZANDO JS
```

> The above command returns JSON structured like this:

```json
[
  EXEMPLO DE JSON
]
```

## <img src="/images/post.png"> Criar produtos

Create new school_product

### HTTP Request

`POST /school_products`

```ruby
EXEMPLO DE CHAMADA UTILIZANDO RUBY
```

```python
EXEMPLO DE CHAMADA UTILIZADO PHYTON
```

```javascript
EXEMPLO DE CHAMADA UTILIZANDO JS
```

> The above command returns JSON structured like this:

```json
[
  EXEMPLO DE JSON
]
```
### Parâmetros obrigatórios

Nome | Tipo | Descrição
--------- | ------- | -----------
school_product | Hash | The school_product to create
school_product[title] | String | Title of the school_product

### Parâmetros opcionais

Nome | Tipo | Descrição
--------- | ------- | -----------
school_product[description] | String | Status of the school_product
school_product[subtitle]  | String
school_product[logo]  | String
school_product[video_url] | String
school_product[video_title] | String
school_product[video_description] | String
school_product[published] | Boolean
school_product[hidden]  | Boolean
school_product[restricted]  | Boolean
school_product[certification] | Boolean
school_product[classes_auto_generation] | Boolean
school_product[certification_min_progress]  | Integer |
school_product[meta_title]  | String |
school_product[meta_description]  | Text
school_product[meta_keys] | Text
school_product[available_time_type] | String |
school_product[available_time_length] | Integer | Required if available_time_type == 'time'
school_product[available_time_unit] | String | Required if available_time_type == 'time'
school_product[expire_date] | DateTime | Required if available_time_type == 'date'
school_product[library_resource_id] | Integer | Required if published == true
school_product[max_attendance_type] | String
school_product[max_attendance_length] | Integer | Required if max_attendance_type is 'time' or 'attempts'
school_product[allowed_emails]  | String |
school_product[class_teacher_ids] | Array<Integer> | Array
school_product[category_ids] | Array<Integer> | Array
school_product[gallery_media_ids] | Array<Integer> | Array