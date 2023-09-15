# Rocketseat - Jornada Ignite - NodeJs - Projeto 02

Esse é um projeto didático, desenvolvido com o apoio do material do módulo de NodeJs do bootcamp Ignite, que foi produzido pela Rocketseat.

O escopo do projeto está relacionado ao gerenciamento de transações financeiras.



# Documentação da API

## Rotas da aplicação
### Criando uma nova transação
```http
  POST /transactions
```
| Parâmetro   | Tipo       | Descrição                           |
| :---------- | :--------- | :---------------------------------- |
| `title`  | `string` | **Obrigatório**. O título da transação   |
| `amount` | `number` | **Obrigatório**. O valor da transação    |
| `type`   | `string` | **Obrigatório**. O tipo da transação (aceita somente os tipos `credit` e `debit`)                                        |
||
|Retorno de Sucesso| `201`|Se tudo ocorrer bem, vai ser criado um cookie que deve ser passado nas requisições abaixo|


### Retorna a lista de transações

```http
  GET /transactions
```

| Requisitos   |        |
| :---------- | :--------- |
| `cookie`  |  **Obrigatório**. Deve ser passado o cookie que foi criado na rota POST|

#### Retorno
Sucesso: Status Code `200`
```json
{
	"transactions": [
		{
			"id": "00a21ad9-0097-4103-980c-13d05c34b50c",
			"title": "Freelancer",
			"amount": "9000.00",
			"created_at": "2023-09-15T02:14:10.389Z",
			"session_id": "e7b8dec2-6301-4189-8e09-c35f30b95f81"
		},
		{
			"id": "7b3d2d78-350d-43d5-8f8d-9f3f77a4cc39",
			"title": "Freelancer - Backend",
			"amount": "12000.00",
			"created_at": "2023-09-15T02:14:30.789Z",
			"session_id": "e7b8dec2-6301-4189-8e09-c35f30b95f81"
		},
		{
			"id": "cc7fc09a-3923-451c-8981-e82bc837e184",
			"title": "Aluguel",
			"amount": "-2000.00",
			"created_at": "2023-09-15T02:14:46.212Z",
			"session_id": "e7b8dec2-6301-4189-8e09-c35f30b95f81"
		}
	]
}
 ```
### Retorna a um resumo dos valores das transações do usuário

```http
  GET /transactions/summary
```

| Requisitos   |        |
| :---------- | :--------- |
| `cookie`  |  **Obrigatório**. Deve ser passado o cookie que foi criado na rota POST|

#### Retorno
Sucesso: Status Code `200`
```json
{
	"summary": {
		"amount": "19000.00"
	}
}
 ```

### Resgata as informação de uma transação específica

```http
  GET /transactions/:id
```

| Parâmetro   | Tipo       | Descrição                              |
| :---------- | :--------- | :----------------------------------    |
| `id`  | `String (uuid)` | **Obrigatório**. O id da transação      |
| `cookie` | |  **Obrigatório**. Deve ser passado o cookie que foi   criado na rota POST                                                 |

#### Retorno
Sucesso: Status Code `200`
```json
{
	"transaction": {
		"id": "816edb55-ef93-49db-8e6b-0f1e0b4c7c14",
		"title": "Aluguel",
		"amount": "-2000.00",
		"created_at": "2023-09-15T02:25:51.583Z",
		"session_id": "2671fbe8-05ae-43c4-b3e7-5056c08ae6f9"
	}
}
 ```

## Retorno de falha

Falha de autorização: Status Code `401`
```json
{
	"error": "Unauthorized"
}`
 ```
Ocorre quando o Cookie passado não possui transações.
## Stack utilizada

**Back-end:** Node, Fastify e Knex

**Database:** Sqlite3
