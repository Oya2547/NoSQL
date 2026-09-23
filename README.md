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


# MongoDB: Modelagem & Schemas

## 1. Visão Geral do MongoDB
* **Banco de Dados NoSQL:** Orientado a documentos no formato BSON (Binary JSON).
* **Flexibilidade:** Suporta *Schema-less* (estrutura dinâmica por documento).
* **Escalabilidade & Disponibilidade:** Suporte nativo a *Replica Sets* (alta disponibilidade) e *Sharding* (escala horizontal).

---

## 2. Estratégias de Modelagem

### Embutimento (Embedding / Denormalization)
Documentos relacionados ficam dentro do próprio documento principal.
* **Vantagens:** Alta performance em leitura e operações atômicas.
* **Uso:** Relações 1:1, 1:Poucos e dados lidos conjuntamente.
* **Atenção:** Respeite o limite de 16 MB por documento.

### Referenciamento (Referencing / Normalization)
Armazena referências (`ObjectId`) apontando para outras coleções.
* **Vantagens:** Evita duplicação e reduz o tamanho dos documentos.
* **Uso:** Relações 1:Muitos, N:M ou dados que mudam frequentemente.
* **Atenção:** Pode exigir o uso de `$lookup` (JOIN) na aplicação.

---

## 3. Padrões de Projeto (Design Patterns)
* **Extended Reference:** Copia os campos mais consultados da referência para evitar `$lookup`.
* **Subset Pattern:** Mantém apenas os itens mais acessados no documento (ex.: 10 comentários recentes).
* **Attribute Pattern:** Transforma atributos variáveis em arrays de chave/valor.
* **Bucket Pattern:** Agrupa dados por intervalos de tempo (ideal para Séries Temporais/IoT).

---

## 4. Validação de Schemas (`$jsonSchema`)
Garante integridade e regras de negócio direto na coleção:

```javascript
db.createCollection("usuarios", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["nome", "email"],
      properties: {
        nome: { bsonType: "string" },
        email: { bsonType: "string", pattern: "^.+@.+\\..+$" }
      }
    }
  }
});
