# Aula 02 - Comandos de Manipulação e Consulta de Dados (DML e SELECT)

Nessa ula vamos ver o conjunto de **Data Manipulation Language (DML)** em MySQL (`INSERT`, `UPDATE`, `DELETE`) e expande o estudo para as consultas avançadas usando **DQL/SELECT**, utilizando a nossa tabela de **Agenda de Contatos**.

## 1. Introdução: O que é DML?
* **Definição:** DML (*Data Manipulation Language*) engloba os comandos responsáveis por **inserir, modificar e remover os dados** (linhas/registros) armazenados dentro das tabelas do banco de dados.
* **A diferença para DDL:** Enquanto o DDL altera a *estrutura* (as colunas e tabelas), o DML mexe no *conteúdo* (as informações guardadas).
* **Principais Comandos:** `INSERT`, `UPDATE` e `DELETE` (além do `SELECT`, que veremos a fundo logo adiante).

---

## 2. O Comando `INSERT` (Adicionando Dados)
O `INSERT` é utilizado para cadastrar novas linhas na tabela.

```sql
-- Inserindo um contato completo
INSERT INTO contatos (nome, telefone, email, data_nascimento, endereco, favorito) 
VALUES ('Ana Souza', '(11)98765-4321', 'ana@email.com', '1995-05-15', 'Rua das Flores, 123', 1);

-- Inserindo um contato apenas com os campos obrigatórios
INSERT INTO contatos (nome, telefone) 
VALUES ('Carlos Silva', '(11)91234-5678');
```

---

## 3. O Comando `UPDATE` (Atualizando Dados)
O `UPDATE` altera informações de registros que já existem na tabela.

```sql
-- Atualiza o telefone de um contato específico
UPDATE contatos 
SET telefone = '(11)99999-9999' 
WHERE id = 1;
```

> **Cuidado com o `UPDATE`:** 
> Nunca se esqueça da cláusula **`WHERE`**. Se você rodar um `UPDATE` sem o `WHERE`, o MySQL vai alterar aquela coluna para **todos** os registros da tabela de uma só vez!

---

## 4. O Comando `DELETE` (Excluindo Dados)
O `DELETE` remove linhas inteiras da tabela.

```sql
-- Exclui um contato específico usando seu ID
DELETE FROM contatos 
WHERE id = 2;
```

> **Cuidado com o `DELETE`:** 
> Assim como no `UPDATE`, rodar um `DELETE` sem a cláusula **`WHERE`** apagará **todos** os dados da sua tabela permanentemente. Cuidado redobrado!

---

## 5. Mergulho Fundo: Operações com `SELECT` (Consultas)
O `SELECT` é o comando mais utilizado no SQL. Ele serve para recuperar e filtrar os dados da base de acordo com as nossas necessidades.

### A. Consultas Básicas
```sql
-- Traz todas as colunas e todos os registros da tabela
SELECT * FROM contatos;

-- Traz apenas colunas específicas para otimizar a visualização
SELECT nome, telefone FROM contatos;
```

### B. Filtrando com a Cláusula `WHERE`
Para não trazer tudo, usamos o `WHERE` com operadores relacionais (`=`, `>`, `<`, `<>`, etc.) e lógicos (`AND`, `OR`).
```sql
-- Busca contatos marcados como favoritos (favorito = 1)
SELECT * FROM contatos WHERE favorito = 1;

-- Busca contatos cujo nome contenha partes específicas (usando LIKE e curinga %)
SELECT * FROM contatos WHERE nome LIKE '%Ana%';
```

### C. Ordenando Resultados com `ORDER BY`
Podemos organizar a ordem de exibição dos dados.
```sql
-- Ordena os contatos por nome em ordem alfabética (ASC = ascendente)
SELECT * FROM contatos ORDER BY nome ASC;

-- Ordena do mais recente para o mais antigo pelo ID (DESC = descendente)
SELECT * FROM contatos ORDER BY id DESC;
```

### D. Limitando Registros com `LIMIT`
Em tabelas grandes, muitas vezes não precisamos de todas as linhas de uma vez.
```sql
-- Traz apenas os 5 primeiros contatos cadastrados
SELECT * FROM contatos LIMIT 5;
```

---
