# 🚀 SQL vs NoSQL

---

## 🗄️ Bases Relacionais (SQL)

| Conceito | TL;DR |
| -------- | ----- |
| **Modelo** | Tabelas + linhas + colunas (esquema fixo). |
| **Integridade** | Regras ACID: Atomicidade, Consistência, Isolamento, Durabilidade. |
| **Linguagem** | SQL padrão (SELECT, JOIN, etc.). |
| **Escalabilidade** | Vertical (scale‑up). |
| **Casos Clássicos** | OLTP, finanças, legado corporativo, relatórios consistentes. |
| **Ferramentas** | PostgreSQL, MySQL, SQL Server, Oracle, MariaDB. |

---

## 🗃️ Bases Não Relacionais (NoSQL)

Existem quatro famílias principais:

| Família | Exemplo | Quando brilha |
| ------- | ------- | ------------- |
| **Document** | MongoDB, Couchbase | Dados semi‑estruturados (JSON), agilidade dev, alto volume de leitura. |
| **Key‑Value** | Redis, DynamoDB | Cache insano, sessões, feature flags. |
| **Columnar** | Cassandra, HBase | Write pesado, petabytes, time‑series. |
| **Graph** | Neo4j, JanusGraph | Relações complexas (redes sociais, recomendação). |

**BASE > ACID?**  
NoSQL geralmente segue o mantra **BASE** (Basically Available, Soft state, Eventual consistency). 💤 Consistência eventual assusta, mas entrega escala horizontal sem choro.

---

## ⚔️ Comparação Rápida SQL x NoSQL

| 🔥 | **SQL** | **NoSQL** |
|---|---------|-----------|
| **Esquema** | Estrito | Flexível ou ausente |
| **Consistência** | Forte (ACID) | Eventual (BASE) |
| **Escala** | Vertical + sharding manual | Horizontal nativo |
| **Query** | SQL padrão | APIs/DSL específico |
| **Use‑cases** | OLTP, reporting | Big Data, tempo real |

---

## 🧠 Critérios de Escolha — SQL ou NoSQL?

1. **Consistência inegociável?** Vai de SQL.  
2. **Mudança de esquema frenética?** NoSQL te abraça.  
3. **Leitura 10× mais que escrita?** Document ou Columnar (NoSQL) + indexing.  
4. **Relacionamentos n:n profundos?** Graph salva o rolê (ou vai de SQL).

> 80% dos projetos cabem num PostgreSQL ou MongoDB bem configurado.

---

## 🔧 Modelagem & Exemplos

### 1. SQL (PostgreSQL)

```sql
-- Criar tabela produtos
CREATE TABLE produtos (
  id SERIAL PRIMARY KEY,
  nome TEXT NOT NULL,
  preco NUMERIC(10,2) CHECK (preco > 0),
  estoque INT DEFAULT 0
);

-- Query: top 5 produtos mais caros em estoque
SELECT nome, preco
FROM produtos
WHERE estoque > 0
ORDER BY preco DESC
LIMIT 5;
```

### 2. NoSQL (MongoDB)

```js
// Document example
{
  _id: ObjectId("..."),
  nome: "Mouse RGB",
  preco: 199.90,
  variacoes: [
    { cor: "preto", estoque: 42 },
    { cor: "branco", estoque: 17 }
  ]
}

// Aggregation: preço médio por cor
db.produtos.aggregate([
  { $unwind: "$variacoes" },
  { $group: { _id: "$variacoes.cor", avgPrice: { $avg: "$preco" } } }
])
```

### 3. Graph (Cypher – Neo4j)

```cypher
// Amizades mútiplas em até 2 níveis
MATCH (u:User {id: 'lucas'})-[:FRIEND*1..2]-(friend)
RETURN DISTINCT friend.name;
```

---

## 🛡️ Boas Práticas

- **Versione schemas** (Migrations).  
- **Backup & Restore**
- **Index = super‑poder**

---

<br>

> Bons estudos — e #KeepCoding! 😉
