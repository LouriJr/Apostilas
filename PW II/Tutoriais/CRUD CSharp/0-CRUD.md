# CRUD — conceito e mapeamento

**CRUD** é o conjunto das quatro operações básicas sobre dados em um sistema:

**Create, Read, Update, Delete**.

O acrônimo CRUD é uma forma simples de decorar e compreender as operações básicas de dados e suas características.

Cada letra mapeia diretamente para o SQL (INSERT, SELECT, UPDATE e DELETE) e para a API HTTP (POST, GET, PUT e DELETE), o que facilita o desenho das rotas, a comunicação entre times e a previsão de respostas comuns.

## Tabela: Acrônimo × SQL × HTTP

| Letra | Ação (português) | SQL (banco de dados) | HTTP (API) | Respostas comuns |
|---|---|---|---|---|
| **C** | **Create** (criar) | `INSERT` | **POST** | `200 OK` |
| **R** | **Read** (ler) | `SELECT` | **GET** | `200 OK` |
| **U** | **Update** (atualizar) | `UPDATE` | **PUT** | `200 OK` |
| **D** | **Delete** (excluir) | `DELETE` | **DELETE** | `200 OK` |

### Exemplos de rotas REST típicas

- **POST** `/usuarios` (criar)
- **GET** `/usuarios/{id}` (ler)
- **PUT** `/usuarios/{id}` (atualizar)
- **DELETE** `/usuarios/{id}` (excluir)
