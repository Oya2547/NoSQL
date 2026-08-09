# Prof. Jefté Goes
## Introdução - NoSQL / Mongo DB

### Definição

#### O que é NoSQL?
* NoSQL é um paradigma de banco de dados que engloba diversos tipos de bancos de dados não relacionais.
* Projetados para oferecer:
  * Flexibilidade
  * Escalabilidade
  * Alto desempenho

---

### Definição

*(Comparativo visual de tipos de bancos de dados)*
* **SQL:** Relational
* **NoSQL:**
  * Key-Value
  * Column Store
  * Graph
  * Document

---

### Definição

Os quatro principais paradigmas de bancos de dados NoSQL são:
* Bancos de dados orientados a documentos (ex.: MongoDB)
* Bancos de dados chave-valor (ex.: Redis)
* Bancos de dados de famílias de colunas (wide-column) (ex.: Cassandra)
* Bancos de dados orientados a grafos (ex.: Neo4j)

---

### O que é MongoDB?

#### O que significa "Mongo"?
**Humongous (Gigante)** — o MongoDB foi projetado para armazenar e gerenciar grandes volumes de dados de forma eficiente.

MongoDB é um banco de dados NoSQL de código aberto, orientado a documentos, projetado para armazenar e gerenciar grandes quantidades de dados de maneira eficiente.

Diferentemente dos bancos de dados relacionais tradicionais (como MySQL ou PostgreSQL), o MongoDB armazena os dados em documentos, em vez de linhas em tabelas.

---

### Como o MongoDB funciona?

* Um servidor MongoDB pode hospedar múltiplos bancos de dados.
* Cada banco de dados contém coleções (collections), e cada coleção armazena documentos (documents).

```text
Database: book_store
├── Collections: Users
│   ├── Documents: { name: "Jefté", age: 33 }
│   └── Documents: { name: "Brenno" } ──> Schemaless structure
└── Collections: Books
    ├── Documents: { ... }
    └── Documents: { ... }
