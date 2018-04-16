# Erros

<aside class="notice">
A API da Edools segue a definição padrão do protocolo HTTP, obedecendo aos códigos de resposta.

Abaixo listaremos alguns erros comuns.
</aside>

## JSON inválido
```
HTTP/1.1 400 Bad Request
Content-Length: 35
{"message":"Problems parsing JSON"}
```
Enviar um JSON inválido resulta em um resultará em um erro 400.
## Valores com tipagem incorreta

```
HTTP/1.1 400 Bad Request
Content-Length: 40
{"message":"Body should be a JSON Hash"}
```
Enviar valores com tipagem incorreta também resulta em um erro 400.

## Unprocessable Entity
```
HTTP/1.1 422 Unprocessable Entity
Content-Length: 157

{
    "message": "Validation Failed",
    "errors": [
        {
           "resource": "SchoolProduct",
           "field": "title",
           "code": "missing_field"
        }
    ]
}
```

Em requests para criar/atualizar objetos, enviar atributos inválidos resultam em erro 422.

Respostas de código 422 sempre retornam metadados que indicam o motivo pelo qual falhou a requisição, fique atento. Os recursos que possuem validações específicas estão documentados na sua descrição.