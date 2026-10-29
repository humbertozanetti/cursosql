# Aula 03: Aprofundando nos comandos `SELECT` 

Nessa uala vamos ver mais sobre **`SELECT`**, explorando filtros avançados, operadores lógicos, ordenação, limitação e agregação de dados usando o nosso sistema de **Agenda de Contatos**.

## 1. Refinando Filtros com a Cláusula `WHERE`

Vimos como usar o `=` básico, mas o `WHERE` aceita uma gama enorme de operadores de comparação e condicionais:

* **Operadores de Comparação:** `=`, `!=` (ou `<>`), `>`, `<`, `>=`, `<=`.

### Operadores especiais:
* **`BETWEEN` (intervalos):** Ideal para datas ou faixas numéricas.
  ```sql
  -- Contatos nascidos na década de 90
  SELECT * FROM contatos 
  WHERE data_nascimento BETWEEN '1990-01-01' AND '1999-12-31';
  ```

* **`IN` (Múltiplos valores):** Substitui vários `OR` em cadeia.
  ```sql
  -- Busca contatos com IDs específicos
  SELECT * FROM contatos 
  WHERE id IN (1, 3, 5, 8);
  ```

* **`LIKE` (Busca por padrão/texto parcial):** Usa coringas como o `%` (qualquer sequência de caracteres) ou `_` (um caractere exato).
  ```sql
  -- Contatos cujo e-mail termina com '@email.com'
  SELECT * FROM contatos 
  WHERE email LIKE '%@email.com';
  ```

* **`IS NULL` / `IS NOT NULL` (Tratando dados vazios):**
  ```sql
  -- Contatos que não possuem e-mail cadastrado
  SELECT * FROM contatos 
  WHERE email IS NULL;
  ```

---

## 2. Combinando Condições com Operadores Lógicos (`AND`, `OR`, `NOT`)

Podemos juntar múltiplas regras para refinar o resultado:

```sql
-- Contatos que são favoritos E nasceram a partir do ano 2000
SELECT nome, telefone, data_nascimento, favorito 
FROM contatos 
WHERE favorito = 1 AND data_nascimento >= '2000-01-01';
```

---

## 3. Ordenando Resultados com `ORDER BY`

Por padrão, o MySQL retorna as linhas na ordem de inserção. O `ORDER BY` organiza a saída:
* `ASC`: Crescente (padrão)
* `DESC`: Decrescente

```sql
-- Organiza os contatos em ordem alfabética (A-Z)
SELECT * FROM contatos 
ORDER BY nome ASC;

-- Mostra os aniversariantes mais novos primeiro (data decrescente)
SELECT nome, data_nascimento 
FROM contatos 
ORDER BY data_nascimento DESC;
```

---

## 4. Controlando o Volume com `LIMIT` e `OFFSET`

Em aplicações reais, tabelas contêm milhares ou milhões de registros. O `LIMIT` restringe a exibição.

```sql
-- Traz apenas os 5 primeiros registros cadastrados
SELECT * FROM contatos 
LIMIT 5;

-- Paginação básica: pula os 5 primeiros e traz os próximos 5
SELECT * FROM contatos 
LIMIT 5 OFFSET 5;
```

---

## 5. Agrupando e Resumindo Dados (`GROUP BY` e Funções de Agregação)

As funções de agregação calculam métricas sobre um conjunto de linhas:
* `COUNT()`: Conta a quantidade de registros.
* `SUM()`: Soma valores numéricos.
* `AVG()`: Calcula a média.
* `MAX()` / `MIN()`: Identifica o maior e menor valor.

### Exemplos práticos:
```sql
-- Quantos contatos temos cadastrados no total?
SELECT COUNT(*) AS total_contatos 
FROM contatos;

-- Quantos contatos temos divididos entre favoritos e não favoritos?
SELECT favorito, COUNT(*) AS quantidade 
FROM contatos 
GROUP BY favorito;
```

---

* **`LIMIT`**: Controla o volume de linhas retornadas.
* **`GROUP BY` + Funções de Agregação (`COUNT`, `SUM`, etc.)**: Cria relatórios resumidos e estatísticas dos dados.
