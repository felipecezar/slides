Criar um Banco de Dados
============================
```sql  
CREATE DATABASE meu_bd; 
```

Selecionar o Banco de Dados 
================================
```sql
USE meu_bd;
```

Apagar o Banco de Dados
=============================
```sql
DROP DATABASE meu_bd;
```



Criar uma tabela
=====================
```sql
CREATE TABLE minha_tabela(
    id INT AUTO_INCREMENT,
    nome VARCHAR(40) NOT NULL,
    ano YEAR,
    altura DECIMAL(5,2)    
);
```

Apagar uma tabela
======================
```sql
DROP TABLE minha_tabela;
```
> A estrutura da tabela é apagada juntamente com os dados



Tipos de Dados no MySQL 
=======================

Dados Numéricos
------------------------

| Tipo     | Descrição                                               |
|:---------|:--------------------------------------------------------|
|TINYINT   | número inteiro muito pequeno (tiny)                     |
|MALLINT   | número inteiro pequeno                                  |
|MEDIUMINT | número inteiro de tamanho médio                         |
|INT       | número inteiro de tamanho comum                         |
|BIGINT    | número inteiro de tamanho grande                        |
|DECIMAL   | número decimal, de ponto fixo                           |
|FLOAT     | número de ponto flutuante de precisão simples (32 bits) |
|DOUBLE    | número de ponto flutuante de precisão dupla (64 bits)   |
|BIT       | um campo de um bit                                      |


Dados Strings
------------------------

| Tipo     | Descrição                                               |
|:---------|:--------------------------------------------------------|
|CHAR | uma cadeia de caracteres (string), de tamanho fixo e não-binária|
|VARCHAR | uma string de tamanho variável e não-binária|
|BINARY | uma string binária de tamanho fixo|
|VARBINARY | uma string binária de tamanho variável|
|BLOB | um BLOB (Binary Large OBject – OBjeto Grande Binário) pequeno|
|TINYBLOB | um BLOB muito pequeno|
|MEDIUMBLOB | um BLOB de tamanho médio|
|LONGBLOB | um BLOB grande|
|TINYTEXT | uma string não-binária e de tamanho bem reduzido|
|TEXT | uma string não-binária e pequena|
|MEDIUMTEXT | uma string de tamanho comum e não-binária|
|LONGTEXT | uma string não-binária de tamanho grande|
|ENUM | de acordo com o manual do MySQL, é uma string, com um valor que precisa ser selecionado de uma lista predefinida na criação da tabela|
|SET | é um objeto que pode ter zero ou mais valores – cada um dos quais precisa ser escolhido de uma lista de valores predeterminados quando da criação da tabela|


Dados Strings
------------------------

| Tipo     | Descrição                                               |
|:---------|:--------------------------------------------------------|
|DATE | o valor referente a uma data no formato 'CCYY-MM-DD'. Por exemplo 1985-11-25 (ano-mês-dia). O 'CC' se refere aos dois dígitos do século (Century, em inglês)|
|TIME | um valor horário no formato 'hh:mm:ss' (hora:minutos:segundos)|
|TIMESTAMP | timestamp é uma sequência de caracteres ou informação codificada que identifica uma marca temporal ou um dado momento em que um evento ocorreu. No MySQL, ele tem o formato 'CCYY-MM-DD hh:mm:ss' – neste caso, seguem a padronização ISO 8601|
|YEAR | armazena um ano no formato 'CCYY' ou 'YY'|



Inserindo Dados
===============

Um único registro
-----------------
```sql
INSERT INTO minha_tabela
    (nome, ano, altura)
VALUES
    ('João',1998,1.78);
```
Vários registros
-----------------
```sql
INSERT INTO minha_tabela
    (nome, ano, altura)
VALUES
    ('Maria',1991,1.65),
    ('Paulo',2002,1.87),
    ('Lucia',2010,1.10),
    ('Geraldo',1980,1.70);
```



Consultas
=========

Todos campos
---------------
```sql
SELECT * 
FROM minha_tabela;
```

Nem todos os campos
--------------------
```sql
SELECT nome, altura 
FROM minha_tabela;
```


Retringindo os resultados
-----------------------------
```sql
SELECT nome, altura 
FROM minha_tabela
WHERE ano == 1980;
```
```sql
SELECT nome, ano 
FROM minha_tabela
WHERE altura < 1.70;
```
```sql
SELECT nome, ano 
FROM minha_tabela
WHERE ano != 2010;
```


Combinando Condições
--------------------
```sql
SELECT nome, ano 
FROM minha_tabela
WHERE ano == 2010 AND altura > 1.70;
```

```sql
SELECT nome, altura 
FROM minha_tabela
WHERE ano == 1991 OR altura < 1.6 ;
```

```sql
SELECT nome, altura 
FROM minha_tabela
WHERE NOT ano == 2001;
```


Intervalo
---------
```sql
SELECT nome, altura 
FROM minha_tabela
WHERE altira BETWEEN 1.60 AND 1.80;
```

Pertencentre a uma lista
------------------------
```sql
SELECT nome, altura 
FROM minha_tabela
WHERE ano IN (1991,1997,2001);
```


Pesquisar por um padrão
------------------------
```sql
SELECT nome, altura 
FROM minha_tabela
WHERE nome LIKE '%Silva';
```

```sql
SELECT nome, altura 
FROM minha_tabela
WHERE nome LIKE '_r';
```


Evitando resultados repetidos
=============================
```sql
SELECT DISTINCT nome, altura 
FROM minha_tabela;
```



Funções em consultas
==============================

Contar
------
```sql
SELECT COUNT(nome)
FROM minha_tabela
WHERE altura < 1.6;
```

Média
------
```sql
SELECT AVG(altura)
FROM minha_tabela
WHERE ano < 2000;
```

Somar
------
```sql
SELECT SUM(altura)
FROM minha_tabela
WHERE ano < 2000;
```


Maior valor encontrado
---------------------
```sql
SELECT MAX(altura)
FROM minha_tabela;
```

Menor valor encontrado
---------------------
```sql
SELECT MIN(altura)
FROM minha_tabela;
```



Criando um apelido
==================

```sql
SELECT nome , altura AS alt  
FROM minha_tabela;
```

```sql
SELECT nome , altura   
FROM minha_tabela AS tb;
```



Testando se um valor e nulo
===========================
Retorna quando for nulo
-----------------------
```sql
SELECT nome , altura   
FROM minha_tabela
WHERE ano IS NULL;
```

Retorna quando não for nulo
---------------------------
```sql
SELECT nome , altura   
FROM minha_tabela
WHERE ano IS NOT NULL;
```



Ordernar os resultados
======================

```sql
SELECT nome, ano
FROM minha_tabela
ORDER BY ano, nome DESC;
```

```sql
SELECT nome, ano
FROM minha_tabela
ORDER BY ano, nome ASC;
```


Limitando as resposta
=====================

```sql
SELECT * 
FROM minha_tabela
ORDER BY altura DESC
LIMIT 3;
```



Agrupando valores
=================
```sql
SELECT ano, COUNT(nome)
FROM minha_tabela
GROUP BY ano;
```


Restrições em grupos
====================
```sql
SELECT ano, COUNT(nome) AS qt
FROM minha_tabela
GROUP BY ano
HAVING qt > 3;
```
