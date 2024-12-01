# DDL (Data Definition Language) no SQL

A Data Definition Language (DDL) no SQL é usada para definir e gerenciar estruturas de dados, como bancos de dados, tabelas, índices, e constraints. Este guia abordará os principais comandos DDL: `CREATE`, `ALTER`, `DROP`, `TRUNCATE`, `RENAME`, e `COMMENT`.

## CREATE

### CREATE DATABASE
Cria um novo banco de dados.

```sql
CREATE DATABASE nome_do_banco;
```

### CREATE TABLE
Cria uma nova tabela.

```sql
CREATE TABLE nome_da_tabela (
    coluna1 tipo_de_dado restrições,
    coluna2 tipo_de_dado restrições,
    ...
);
```

#### Exemplo:
```sql
CREATE TABLE clientes (
    id INT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE,
    data_nascimento DATE
);
```

### CREATE INDEX
Cria um índice para uma tabela.

```sql
CREATE INDEX nome_do_indice ON nome_da_tabela (coluna1, coluna2, ...);
```

#### Exemplo:
```sql
CREATE INDEX idx_nome ON clientes (nome);
```

## ALTER

### ALTER TABLE
Modifica uma tabela existente, permitindo adicionar, modificar ou remover colunas e constraints.

#### Adicionar Coluna
```sql
ALTER TABLE nome_da_tabela ADD coluna tipo_de_dado restrições;
```

##### Exemplo:
```sql
ALTER TABLE clientes ADD telefone VARCHAR(20);
```

#### Modificar Coluna
```sql
ALTER TABLE nome_da_tabela MODIFY coluna tipo_de_dado restrições;
```

##### Exemplo:
```sql
ALTER TABLE clientes MODIFY telefone VARCHAR(15) NOT NULL;
```

#### Remover Coluna
```sql
ALTER TABLE nome_da_tabela DROP COLUMN coluna;
```

##### Exemplo:
```sql
ALTER TABLE clientes DROP COLUMN telefone;
```

#### Adicionar Constraint
```sql
ALTER TABLE nome_da_tabela ADD CONSTRAINT nome_da_constraint tipo_da_constraint (coluna);
```

##### Exemplo:
```sql
ALTER TABLE clientes ADD CONSTRAINT chk_idade CHECK (data_nascimento < '2003-01-01');
```

## DROP

### DROP DATABASE
Remove um banco de dados.

```sql
DROP DATABASE nome_do_banco;
```

### DROP TABLE
Remove uma tabela.

```sql
DROP TABLE nome_da_tabela;
```

### DROP INDEX
Remove um índice.

```sql
DROP INDEX nome_do_indice;
```

### DROP COLUMN
Remove uma coluna de uma tabela.

```sql
ALTER TABLE nome_da_tabela DROP COLUMN coluna;
```

## TRUNCATE

### TRUNCATE TABLE
Remove todos os registros de uma tabela, mas mantém sua estrutura.

```sql
TRUNCATE TABLE nome_da_tabela;
```

## RENAME

### RENAME TABLE
Renomeia uma tabela.

```sql
ALTER TABLE nome_da_tabela RENAME TO novo_nome_da_tabela;
```

## COMMENT

### COMMENT ON
Adiciona um comentário a um objeto do banco de dados (como tabelas ou colunas).

```sql
COMMENT ON TABLE nome_da_tabela IS 'comentário';
COMMENT ON COLUMN nome_da_tabela.coluna IS 'comentário';
```

## Conclusão

Os comandos DDL são fundamentais para a definição e gerenciamento da estrutura de dados em um banco de dados SQL. Eles permitem criar, alterar e remover bancos de dados, tabelas, índices e outras estruturas essenciais. Este guia fornece uma visão geral dos principais comandos e casos de uso comuns para ajudar a entender e aplicar DDL no SQL.