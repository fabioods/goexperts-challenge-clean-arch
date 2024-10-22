# Desafio Go Experts - Clean Arch

## Proposta

Desafio do módulo de Clean Arch do Go Experts.

A proposta é criar um use case para retornar os pedidos criados e ter a possibilidade de visualizar por REST, gRPC e GraphQL.

## Setup inicial

Clone o repositório com o comando abaixo:

```bash
git clone https://github.com/fabioods/goexperts-challenge-clean-arch.git
```

Nesse projeto está configurado para usar imagens compatíveis com arquitetura arm64, no caso da image do rabbitmq é `arm64v8/rabbitmq:3-management` caso use arquiteura amd64, altere para `rabbitmq:3-management`.

Para executar o projeto, é necessário ter o docker e o docker-compose instalados. E execute o comando abaixo para subir as imagens:

```bash
docker-compose up -d
```

## Como executar o projeto

Dentro da pasta do projeto execute o comando abaixo para instalar as dependências:

```bash
go mod tidy
```

Agora iremos executar nossa aplicação:

```bash
make start
```

Caso ocorra tudo bem, os serviços estarão rodando nos endereços:

- Rest em http://localhost:8000:

  - Use os arquivos na pasta `/api` para interagir;
  - Para executar diretamente no VSCode pode instalar a extensão [httpYac - Yet another Client](https://marketplace.visualstudio.com/items?itemName=anweber.vscode-httpyac)

- GraphQL em http://localhost:8080:

  - Use o template abaixo:

    ```graphql
    mutation createOrder {
      createOrder(input: { id: "change-id", Price: 10.0, Tax: 0.5 }) {
        id
        Price
        Tax
        FinalPrice
      }
    }

    query orders {
      listOrders {
        id
        Price
        Tax
        FinalPrice
      }
    }
    ```

- gRPC na porta 50051:
  - Será necessário ter o [evans](https://github.com/ktr0731/evans?tab=readme-ov-file#installation) instalado.
  - Feito isso pode executar os comando a seguir:
    ```bash
    evans -r repl
    package pb
    service OrderService
    call CreateOrder // criar 1 pedido
    call ListOrders // lista os pedidos criados
    ```
