# 📚 CRUD e Consultas com MongoDB

Projeto acadêmico desenvolvido para praticar os principais conceitos de **CRUD, consultas, atualização de documentos, arrays e subdocumentos no MongoDB**, utilizando o **MongoDB Compass**.

A atividade utiliza como cenário uma biblioteca e permite praticar operações diretamente sobre uma coleção de livros.

---

## 🎯 Objetivo

Praticar os principais recursos do MongoDB, incluindo:

- Inserção de documentos
- Consultas com filtros
- Projeção de campos
- Ordenação
- Atualização de documentos
- Manipulação de arrays
- Subdocumentos
- Operadores de atualização
- Exportação de dados em JSON

---

## 🛠️ Tecnologias e Ferramentas

- MongoDB
- MongoDB Compass
- JSON
- Git
- GitHub

---

## 🗄️ Banco de Dados

Banco utilizado:

```text
biblioteca_db
```

Coleção utilizada até o momento:

```text
livros
```

---

## 📁 Estrutura do Projeto

```text
mongodb-biblioteca/
│
├── database/
│   └── livros.json
│
├── docs/
│   └── CRUD-e-Consultas-no-MongoDB.pdf
│
└── README.md
```

---

# 📖 Dados da Coleção `livros`

Foram adicionados inicialmente os seguintes livros:

| Título | Autor | Ano | Gênero | Páginas | Disponível |
|---|---|---:|---|---:|---|
| Dom Casmurro | Machado de Assis | 1899 | Romance | 256 | true |
| 1984 | George Orwell | 1949 | Distopia | 416 | true |
| O Hobbit | J.R.R. Tolkien | 1937 | Fantasia | 310 | false |
| Sapiens | Yuval Harari | 2011 | História | 464 | true |

Também foi adicionado o livro `Clean Code`, utilizando **subdocumentos e array**:

```json
{
  "titulo": "Clean Code",
  "autor": {
    "nome": "Robert Martin",
    "nacionalidade": "EUA"
  },
  "editora": {
    "nome": "Prentice Hall",
    "ano": 2008
  },
  "tags": [
    "programação",
    "boas práticas"
  ],
  "disponivel": true
}
```

Esse documento demonstra como o MongoDB permite armazenar objetos aninhados e arrays dentro de um mesmo documento.

---

# 🔎 READ — Consultas

## Filtro por Campo

Consulta realizada para localizar livros do gênero Fantasia:

```json
{
  "genero": "Fantasia"
}
```

Resultado:

```text
O Hobbit
```

---

## Filtro com Múltiplos Campos

Também foi realizado um filtro utilizando duas condições:

```json
{
  "genero": "Fantasia",
  "disponivel": true
}
```

O MongoDB aplica um **AND implícito** quando vários campos são informados no mesmo filtro.

Como `O Hobbit` estava com:

```json
{
  "disponivel": false
}
```

nenhum documento foi retornado.

---

# 📋 Projeção

Foi utilizada a opção **Project** do MongoDB Compass para definir quais campos deveriam aparecer no resultado:

```json
{
  "titulo": 1,
  "autor": 1,
  "_id": 0
}
```

Onde:

- `1` inclui o campo
- `0` exclui o campo
- `_id: 0` oculta o identificador do documento

---

# ↕️ Ordenação

Ordenação por ano em ordem crescente:

```json
{
  "ano": 1
}
```

Ordenação por ano em ordem decrescente:

```json
{
  "ano": -1
}
```

Onde:

```text
1  = ordem crescente
-1 = ordem decrescente
```

---

# ✏️ UPDATE — Atualizações

Durante a atividade foram utilizados diferentes operadores de atualização do MongoDB.

---

## `$set`

Utilizado para alterar o valor de um campo.

Exemplo:

```json
{
  "$set": {
    "disponivel": false
  }
}
```

Também foi utilizado para adicionar um novo campo aos documentos:

```json
{
  "$set": {
    "destaque": true
  }
}
```

---

## `$inc`

Utilizado para incrementar valores numéricos.

```json
{
  "$inc": {
    "paginas": 10
  }
}
```

Exemplo:

```text
256 → 266 páginas
```

---

## `$rename`

Utilizado para renomear um campo sem alterar o valor armazenado.

```json
{
  "$rename": {
    "ano": "anoPublicacao"
  }
}
```

Exemplo:

```text
ano: 1899

↓

anoPublicacao: 1899
```

---

## `$unset`

Utilizado para remover um campo de um documento.

```json
{
  "$unset": {
    "destaque": ""
  }
}
```

O campo `destaque`, criado anteriormente durante os testes, foi removido.

---

# 📦 Manipulação de Arrays

O documento `Clean Code` possui o array:

```json
{
  "tags": [
    "programação",
    "boas práticas"
  ]
}
```

Foram realizados testes utilizando diferentes operadores de arrays.

---

## `$push`

Adiciona um novo valor ao final de um array.

```json
{
  "$push": {
    "tags": "clássico"
  }
}
```

Resultado:

```json
{
  "tags": [
    "programação",
    "boas práticas",
    "clássico"
  ]
}
```

O `$push` permite valores duplicados.

---

## `$addToSet`

Adiciona um valor ao array somente se ele ainda não existir.

```json
{
  "$addToSet": {
    "tags": "clássico"
  }
}
```

Como `clássico` já estava presente no array, nenhum valor duplicado foi criado.

---

## `$pull`

Remove um valor de um array.

```json
{
  "$pull": {
    "tags": "clássico"
  }
}
```

Após a operação, o array voltou a possuir:

```json
{
  "tags": [
    "programação",
    "boas práticas"
  ]
}
```

---

# 🧠 Conceitos Praticados

Durante a atividade foram trabalhados os seguintes conceitos:

- Documentos
- Collections
- ObjectId
- JSON / BSON
- Strings
- Números
- Booleanos
- Arrays
- Subdocumentos
- Filtros
- AND implícito
- Projection
- Sort
- `$set`
- `$inc`
- `$rename`
- `$unset`
- `$push`
- `$addToSet`
- `$pull`

---

# 💾 Exportação dos Dados

A coleção foi exportada pelo MongoDB Compass no formato JSON.

Arquivo:

```text
database/livros.json
```

A exportação permite manter uma cópia dos dados utilizados na atividade e versioná-los no GitHub.

---

# 🚧 Próximas Etapas

A atividade ainda continuará com outros recursos do MongoDB, incluindo:

- Substituição completa de documentos
- Upsert
- DELETE
- Operadores de comparação
- Operadores lógicos
- Regex
- Consultas em arrays
- Consultas em subdocumentos
- Aggregation Pipeline
- Índices
- Projeto final de biblioteca

---

# 🎓 Contexto Acadêmico

Projeto desenvolvido durante os estudos de **Banco de Dados com MongoDB**, com foco no aprendizado prático de bancos de dados orientados a documentos.

---

# 👨‍💻 Autor

**Luan Araujo**

Estudante de Desenvolvimento de Sistemas.

GitHub: [Luanlhp777](https://github.com/Luanlhp777)

---

⭐ Projeto desenvolvido para estudo e prática de MongoDB.