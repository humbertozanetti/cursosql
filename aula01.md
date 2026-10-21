# Aula 01 - Comandos DDL no MySQL 

---

## 1. O que são comandos DDL?

* **Definição:** DDL significa *Data Definition Language* (Linguagem de Definição de Dados).
* **Para que servem:** São os comandos SQL responsáveis por **definir, alterar e excluir a estrutura** de um banco de dados (tabelas, colunas, chaves), e não os dados armazenados nelas.
* **Principais comandos:** 
  * `CREATE`: Cria estruturas (bancos de dados, tabelas).
  * `ALTER`: Modifica estruturas existentes.
  * `DROP`: Exclui estruturas por completo.

---

## 2. Criando o Banco de Dados

O primeiro passo prático é criar o ambiente onde as tabelas vão estar, ou seja, criar o Banco de Dados em que as tabelas estarão associadas. Para o exemplo de aula vamos criar uma Agenda de Contato.

```sql
-- Cria o banco de dados para a nossa agenda
CREATE DATABASE agenda_db;

-- Seleciona o banco de dados recém-criado para uso nas próximas instruções (é importante para o SGBD saber em qual lugar vai rodar os script!)
USE agenda_db;
```

---

## 3.  Tipos de Dados e Atributos no MySQL

### Principais Tipos de Dados

* **Numéricos:**
  * `INT`: Números inteiros padrão (ex: IDs, quantidades).
  * `BIGINT`: Números inteiros grandes (para alto volume de registros).
  * `DECIMAL(p, s)`: Números exatos com casas decimais (valores monetários, ex: `DECIMAL(10,2)`).
  * `TINYINT`: Número inteiro pequeno (muito usado como booleano: `0` para falso, `1` para verdadeiro).

* **Textos e Strings:**
  * `VARCHAR(tamanho)`: Texto de tamanho variável e otimizado (ideal para nomes, e-mails).
  * `CHAR(tamanho)`: Texto de tamanho fixo.
  * `TEXT` / `LONGTEXT`: Para textos longos e descrições extensas.

* **Datas e Horas:**
  * `DATE`: Apenas data no formato `AAAA-MM-DD`.
  * `TIME`: Apenas hora no formato `HH:MM:SS`.
  * `DATETIME`: Data e hora combinadas (`AAAA-MM-DD HH:MM:SS`).
  * `TIMESTAMP`: Data e hora com fuso horário, muito usado para auditoria de registros.

* **Outros:**
  * `ENUM('val1', 'val2')`: Lista restrita de valores pré-definidos (ex: status `'Ativo'`, `'Inativo'`).
  * `BLOB`: Para dados binários (imagens, arquivos).

### Principais Atributos e Restrições (*Constraints*)

* `PRIMARY KEY`: Torna o campo a chave primária da tabela (identificador único e obrigatório).
* `AUTO_INCREMENT`: Incrementa automaticamente o valor numérico a cada nova linha inserida.
* `NOT NULL`: Impede que o campo aceite valores nulos (torna o preenchimento obrigatório).
* `UNIQUE`: Garante que não haja valores duplicados nessa coluna em linhas diferentes (ex: CPF ou e-mail único).
* `DEFAULT valor`: Define um valor padrão automático caso nenhum dado seja informado.
* `CHECK (condição)`: Limita os valores aceitos baseados em uma regra lógica (ex: `CHECK (idade >= 18)`).
* `FOREIGN KEY`: Cria um relacionamento (chave estrangeira) com a chave primária de outra tabela.

---

## 4. Criando a Tabela do Sistema de Agenda

Agora colocamos a mão na massa criando a tabela de **contatos**.

```sql
CREATE TABLE contatos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    telefone VARCHAR(20) NOT NULL,
    email VARCHAR(100) UNIQUE,
    data_nascimento DATE
);
```

### Tipos de Dados
* `INT`: Números inteiros (ex: `10, 1990`). Usado para IDs e contadores.
* `VARCHAR(tamanho)`: Textos de tamanho variável (ex: `João Silva, contato@email.com`). O número define o limite máximo de caracteres.
* `DATE`: Datas no formato AAAA-MM-DD (ex: `2026-10-21`).
* `TINYINT`: Números inteiros muito pequenos. Muito utilizado para representar valores booleanos/lógicos ( `0` para falso, `1` para verdadeiro).

### Principais Atributos e Restrições (*Constraints*)
* `PRIMARY KEY`: Define a chave primária, identificando de forma única cada registro (linha) da tabela.
* `AUTO_INCREMENT`: Faz o MySQL preencher o campo numérico automaticamente, somando 1 a cada novo registro.
* `NOT NULL`: Garante que o campo é obrigatório, ou seja, não pode ficar vazio.
* `DEFAULT` valor: Define um valor padrão caso nenhum dado seja informado no momento do cadastro.

---

## 5. Alteração nos campos

Pensem o seguinte: *"Acabamos de colocar o sistema no ar. Logo em seguida, os usuários pediram para salvar também o **endereço** e marcar se o contato é **favorito**."*

Podemos utilizar **`ALTER TABLE`** para mudar (alterar) a estrutura sem perder os dados já existentes.

```sql
-- Adicionando a coluna de endereço
ALTER TABLE contatos ADD COLUMN endereco VARCHAR(150);

-- Adicionando a coluna para marcar se é favorito (0 para não, 1 para sim)
ALTER TABLE contatos ADD COLUMN favorito TINYINT DEFAULT 0;
```

---
