# Resumão SQL

Notes: Todos os comandos vistos em aula. Feito por Giovana de Brito Silva.

### Comandos DML

INSERÇÃO DE VALORES COM SQL

```sql
INSERT INTO nome_da_tabela (colunas) VALUES (valores);

INSERT INTO maes (id_mae, nome, endereco, telefone, dt_nascimento)
VALUES (10,'Rosário de Almeida', 'Rua zzz', '(11)9.00000000', '21/06/1994');

/* PARA INSERÇÃO EM TODAS AS COLUNAS AO MESMO TEMPO, NÃO É NECESSÁRIO INFORMAR AS COLUNAS. */

INSERT INTO maes 
VALUES (10, 'Rosário de Almeida', 'Rua zzz', '(11)9.00000000', '21/06/1994');

/* PARA INSERIR VÁRIOS REGISTROS AO MESMO TEMPO */

INSERT INTO maes 
VALUES (NULL, 'Rosário de Almeida', '', '(11)9.00000000', '21/06/1994'), (NULL, 'Maria Sena', '', '(11)9.00000000', '21/06/1994'), (NULL, '', '', '(11)9.00000000', '21/06/1994'), (NULL, '', '', '(11)9.00000000', '21/06/1994');
```

DELETAR OS DADOS DO BANCO DE DADOS

```sql
/* DELETA TUDO DA TABELA, PREFERENCIALMENTE NÃO USAR */

DELETE FROM nome_da_tabela;

DELETE FROM meus_amigos_instagram;

/* MANEIRA CORRETA */

DELETE FROM nome_da_tabela WHERE id_mae = 4; 

DELETE FROM nome_da_tabela WHERE nome = 'Tereza Cristina'; 

DELETE FROM nome_da_tabela WHERE id_mae = 4 OR id_mae = 5; 

DELETE FROM nome_da_tabela WHERE id_mae > 5 AND id_mae < 10;
```

ATUALIZAR OS DADOS DE UMA TABELA

```sql
UPDATE nome_da_tabela SET coluna1 = novo_valor1, coluna2 = novo_valor2, colunaN = novo_valorN WHERE condição;

UPDATE maes SET endereco = 'Rua Rouxinol Amarelo' WHERE id_mae = 4;

/* ATUALIZAR UMA OU MAIS COLUNAS DE UMA TABELA */

UPDATE maes SET endereco = 'Rua Rouxinol Amarelo', telefone = '(88)9.98988989' WHERE id_mae = 2;

UPDATE maes SET endereco = 'Rua Rouxinol Amarelo', telefone = '(88)9.98988989' WHERE id_mae = 2;
```

CONSULTA DE DADOS UTILIZANDO SELECT

```sql
/*CONSULTAR / LER / READ */

SELECT colunas FROM tabela SELECT coluna1, coluna2, coluna3, colunaN FROM tabela SELECT * FROM tabela;

/* Mostrar todos os dados de bebes */ 

SELECT * FROM bebes; 

/* Mostrar nome e data de nascimento das mães */ 

SELECT nome, dt_nasc FROM maes; 

/* Mostrar nome, crm e especialidade dos médicos */ 

SELECT nome, crm, especialidade FROM medicos; 

SELECT especialidade, nome, crm FROM medicos;

/* SELECT DISTINCT */

SELECT DISTINCT cidade FROM compras;

/* ORDER BY */ 
SELECT * FROM maes ORDER BY nome ASC; 

SELECT * FROM maes ORDER BY nome DESC;

/* MIN e MAX */ 

SELECT MIN(alt_nasc) FROM bebes;

SELECT MAX(alt_nasc) FROM bebes;

/* COUNT - Retorna Quantidade */ 

SELECT COUNT(id_bebe) FROM bebes; 

/* SUM - Retorna a Soma */

SELECT SUM(alt_nasc) FROM bebes;

/* AVG - Retorna a Média Aritmética */ 

SELECT AVG(alt_nasc) FROM bebes;

/* LIKE */ 

SELECT colunas FROM nome_tabela WHERE condição LIKE 'algum_padrão'

SELECT * FROM maes WHERE nome LIKE 'Maria%';

SELECT * FROM maes WHERE nome LIKE '%Maria%';

SELECT * FROM maes WHERE nome NOT LIKE '%Mari_%';

SELECT * FROM maes WHERE nome LIKE '%Silvi[ao]';

/* APELIDOS - ALIASES */

SELECT nome, endereco, telefone FROM maes;

SELECT nome, dt_nasc AS Data_Nascimento, AVG(alt_nasc) AS media_altura, SUM(peso_nasc) AS soma_peso FROM bebes AS b;

/* BETWEEN */

SELECT nome, peso FROM bebes WHERE peso_bebe BETWEEN 3 AND 4;

SELECT nome, peso FROM bebes WHERE dt_nasc BETWEEN '2021-01-01' AND '2022-11-30';
```

### Comandos DDL

VISUALIZAR QUAIS BANCOS DE DADOS EXISTEM

```sql
SHOW DATABASES;
```

CRIAR BANCO DE DADOS

```sql
CREATE DATABASE nome_do_banco;
```

FAZER BACKUP DO BANCO DE DADOS

```sql
BACKUP DATABASE nome_do_banco
TO DISK = 'url'
```

EXCLUIR BANCO DE DADOS

```sql
DROP DATABASE nome_do_banco;
```

DEFINIR QUAL BANCO EU QUERO UTILIZAR

```sql
USE nome_do_banco;
```

VISUALIZAR TABELAS QUE EXISTEM

```sql
SHOW TABLES;
```

CRIAR TABELAS

```sql
CREATE TABLE nome_da_tabela (
atributo1 tipo,
atributo2 tipo,
.
.
atributoN tipoN
);
```

VERIFICAR SCHEMA DA TABELA

```sql
DESCRIBE nome_da_tabela;
```

EXCLUIR TABELA

```sql
DROP TABLE nome_da_tabela;
```

EXCLUIR OS DADOS DA TABELA, SEM EXCLUIR A TABELA

```sql
TRUNCATE TABLE nome_da_tabela;
```

ALTERAR AS TABELAS

```sql
ALTER TABLE nome_da_tabela;

/* ADICIONAR UMA NOVA COLUNA */

ALTER TABLE nome_da_tabela
ADD nome_da_coluna tipo;

ALTER TABLE medicos
ADD especialidade VARCHAR(100);

/* EXCLUIR UMA COLUNA */

ALTER TABLE nome_da_tabela
DROP COLUMN nome_da_coluna;

ALTER TABLE medicos
DROP COLUMN especialidade;

/* MODIFICAR TIPO DE DADOS DE UMA COLUNA - SQL SERVER */

ALTER TABLE nome_da_tabela
ALTER COLUMN nome_da_coluna novo_tipo;

/* MODIFICAR TIPO DE DADOS DE UMA COLUNA - MYSQL */

ALTER TABLE nome_da_tabela
MODIFY COLUMN nome_da_coluna novo_tipo;

/* MODIFICAR TIPO DE DADOS DE UMA COLUNA - ORACLE */

ALTER TABLE nome_da_tabela
MODIFY nome_da_coluna novo_tipo;
```

EXCLUIR UMA COLUNA DA TABELA

```sql
ALTER TABLE carros
DROP COLUMN modelo_carro;
```

CONSTRAINT

```sql
CREATE TABLE maes (
id_mae INT AUTO_INCREMENT,
nome VARCHAR(200) NOT NULL,
endereco VARCHAR(200),
telefone VARCHAR(20),
dt_nasc DATE NOT NULL,
CONSTRAINT pk_idMae PRIMARY KEY (id_mae)
);

/* OUTRA FORMA */

CREATE TABLE maes (
id_mae INT AUTO_INCREMENT PRIMARY KEY,
nome VARCHAR(200) NOT NULL,
endereco VARCHAR(200),
telefone VARCHAR(20),
dt_nasc DATE NOT NULL
);

/* OUTROS TIPOS DE CONSTRAINTS*/

--NOT NULL

CREATE TABLE carros (
	id_carro INT(11) NOT NULL,
  	nome_carro VARCHAR(200) NOT NULL,
  	placa_carro varchar(10) NOT NULL
);

--UNIQUE

CREATE TABLE carros (
	id_carro INT(11) NOT NULL UNIQUE,
  	nome_carro VARCHAR(200) NOT NULL,
  	placa_carro varchar(10) NOT NULL UNIQUE
);

CREATE TABLE carros (
	id_carro INT(11) NOT NULL,
  	nome_carro VARCHAR(200) NOT NULL,
  	placa_carro varchar(10) NOT NULL,
  	UNIQUE(placa_carro),
  	UNIQUE(id_carro),
  	UNIQUE(nome_carro)
);

CREATE TABLE carros (
	id_carro INT(11) NOT NULL,
  	nome_carro VARCHAR(200) NOT NULL,
  	placa_carro varchar(10) NOT NULL,
  	CONSTRAINT uni_carros UNIQUE(id_carro, placa_carro)
 
);
```

EXCLUIR CONSTRAINT

```sql
ALTER TABLE carros
DROP INDEX uni_carros;

ALTER TABLE carros
DROP CONSTRAINT uni_carros;
```

CRIAR CONSTRAINT PARA CHAVE PRIMÁRIA

```sql
CREATE TABLE carros(
	id_carro INT PRIMARY KEY,
  	nome_carro VARCHAR(200),
  	placa_carro varchar(10) NOT NULL,
);

CREATE TABLE carros(
	id_carro INT,
  	nome_carro VARCHAR(200),
  	placa_carro varchar(10) NOT NULL,
  	PRIMARY KEY(id_carro)
);

CREATE TABLE carros(
	id_carro INT,
  	nome_carro VARCHAR(200),
  	placa_carro varchar(10) NOT NULL,
  	CONSTRAINT pk_carro PRIMARY KEY(id_carro)
);

CREATE TABLE carros(
	id_carro INT,
  	nome_carro VARCHAR(200),
  	placa_carro varchar(10) NOT NULL,
  	CONSTRAINT pk_carro PRIMARY KEY(id_carro, placa_carro)
);
```

ADICIONAR UMA CHAVE PRIMÁRIA EM UMA TABELA JÁ CRIADA

```sql
ALTER TABLE carros
ADD CONSTRAINT pk_carro PRIMARY KEY(id_carro);

ALTER TABLE carros
ADD PRIMARY KEY(id_carro);
```

EXCLUIR UMA CHAVE PRIMÁRIA

```sql
ALTER TABLE carros
DROP PRIMARY KEY;

ALTER TABLE carros
DROP CONSTRAINT pk_carro;
```

CRIAR UMA CONSTRAINT PARA CHAVE ESTRANGEIRA

```sql
CREATE TABLE marcas(
	id_marca INT PRIMARY KEY AUTOINCREMENT,
  	descricao_marca VARCHAR(100)
);

CREATE TABLE carros (
 	id_carro INT,
  	nome_carro VARCHAR(200),
  	placa_carro varchar(10) NOT NULL,
  	id_marca INT,
  	CONSTRAINT pk_carro PRIMARY KEY(id_carro),
  	FOREIGN KEY (id_marca) REFERENCES marcas(id_marca)
);

CREATE TABLE marcas(
	id_marca INT PRIMARY KEY AUTOINCREMENT,
  	descricao_marca VARCHAR(100)
);

CREATE TABLE carros (
 	id_carro INT AUTOINCREMENT,
  	nome_carro VARCHAR(200),
  	placa_carro varchar(10) NOT NULL,
  	id_marca INT,
  	CONSTRAINT pk_carro PRIMARY KEY (id_carro),
  	CONSTRAINT fk_carro_marca FOREIGN KEY (id_marca)
  	REFERENCES marcas(id_marca)
);
```

ADICIONAR UMA CHAVE ESTRANGEIRA EM UMA TABELA JÁ CRIADA

```sql
ALTER TABLE medicos
ADD FOREIGN KEY(email_medicos) 
REFERENCES email_medicos(id_medico);

ALTER TABLE tabela
ADD CONSTRAINT fk_nome_da_constraint
FOREIGN KEY(atributo_chave)
REFERENCES tabela(atributo_chave)
ON UPDATE CASCADE
ON DELETE CASCADE;
```

EXCLUIR UMA CHAVE ESTRANGEIRA

```sql
ALTER TABLE carros
DROP FOREIGN KEY fk_carro_marca;

ALTER TABLE carros
DROP CONSTRAINT fk_carro_marca;
```

DEFAULT

```sql
CREATE TABLE carros(
	id_carro INT AUTOINCREMENT,
  	nome_carro VARCHAR(200) DEFAULT 'Nenhum',
  	placa_carro varchar(10) NOT NULL,
  	id_marca INT,
  	CONSTRAINT pk_carro PRIMARY KEY (id_carro),
);
```

FORMATOS DE DATAS

```sql
/*
DATE - yyyy-mm-dd
DATETIME - yyyy-mm-dd hh:mm:ss 
TIMESTAMP - yyyy-mm-dd hh:mm:ss 
YEAR - YYYY ou yy 
*/

FORMAT_DATE('formato_da_data', coluna_data)
'%d%m%Y'
EXTRACT(year from data)
EXTRACT(month from data)
EXTRACT(day from data)
```

CONCATENAÇÃO DE VALORES

```sql
CONCAT(valor1, valor2, valor3, valorN)

SELECT concat(format_date('%Y',data), format_date('%m',data)) as ano_mes
FROM `aulasbc26-suzana.dados_covid.dados_covid_nacional`;
```

CHAR_LENGHT 

```sql
CHAR_LENGHT(retorna o tamanho da string);
```

REPLACE

```sql
SELECT replace(coluna, 'caractere que quer mudar', 'caracter que irá substituir') 
FROM tabela;
```

JOIN

```sql
SELECT * 
FROM tabela1 INNER JOIN tabela2
ON tabela1.atributo = tabela2.atributo;
```

CASE WHEN

```sql
SELECT *
CASE WHEN coluna = valor THEN faça isso
ELSE faça isso END 
FROM tabela
```

### Exercício 1:

```sql
SHOW DATABASES;
```

```sql
CREATE DATABASE hospital;
```

```sql
USE hospital;
```

```sql
SHOW TABLES;
```

```sql
CREATE TABLE maes (
    id_mae INT AUTO_INCREMENT,
    nome VARCHAR(100) NOT NULL,
    endereco VARCHAR(200),
    telefone VARCHAR(50),
    dt_nasc DATE NOT NULL,
    CONSTRAINT pk_id_mae PRIMARY KEY(id_mae)
);
```

```sql
DESCRIBE maes;
```

```sql
CREATE TABLE medicos (
    id_medico INT AUTO_INCREMENT,
    crm VARCHAR(20) NOT NULL,
    nome VARCHAR(100) NOT NULL,
    especialidade VARCHAR(100) NOT NULL,
    CONSTRAINT pk_id_medico PRIMARY KEY(id_medico)
);
```

```sql
DESCRIBE medicos;
```

```sql
CREATE TABLE medicos_celular (
    id INT AUTO_INCREMENT,
    numero_celular VARCHAR(20) NOT NULL,
    id_medico INT,
    CONSTRAINT pk_id_medicos_celular PRIMARY KEY(id),
    CONSTRAINT fk_medicos_celular FOREIGN KEY(id_medico) REFERENCES medicos(id_medico)
);
```

```sql
DESCRIBE medicos_celular;
```

```sql
SHOW DATABASES;
```

```sql
CREATE DATABASE hospital;
```

```sql
USE hospital;
```

```sql
SHOW TABLES;
```

```sql
CREATE TABLE bebes (
		id_bebe INT AUTO_INCREMENT,
		nome VARCHAR(100) NOT NULL,
		dt_nasc DATE NOT NULL,
		peso_nasc FLOAT NOT NULL,
		alt_nasc INT NOT NULL,
		id_medico INT,
		id_mae INT,    
		CONSTRAINT pk_id_bebe PRIMARY KEY(id_bebe),
		CONSTRAINT fk_bebes_medicos FOREIGN KEY(id_medico) REFERENCES medicos(id_medico),
		CONSTRAINT fk_bebes_maes FOREIGN KEY(id_mae) REFERENCES maes(id_mae)
);
```

```sql
DESCRIBE maes;
```

```sql
INSERT INTO medicos VALUES (NULL, '65973624', 'Marcos Santana de Araújo', 'Obstetra');
```

```sql
SELECT * FROM medicos;
```

```sql
INSERT INTO medicos VALUES (NULL, '35998745', 'Eliana Martins de Lima', 'Obstetra');
```

```sql
SELECT id_medico, nome FROM medicos;
```

```sql
ALTER TABLE medicos
DROP COLUMN especialidade;
```

```sql
ALTER TABLE bebes
MODIFY COLUMN alt_nasc FLOAT;
```

```sql
ALTER TABLE bebes
CHANGE alt_nasc altura_nasc INT;
```

```sql
ALTER TABLE medicos
ADD email_medicos VARCHAR(100);
```

```sql
ALTER TABLE medicos
ADD FOREIGN KEY(email_medicos) REFERENCES email_medicos(id_medico);
```

```sql
ALTER TABLE medicos
ADD CONSTRAINT pk_id_medico PRIMARY KEY(id_medico);
```

```sql
INSERT INTO maes VALUES (NULL, 'Maria da Silva', 'Rua 12 de Agosto, 123', '(21)931110000', '1992-09-23'), (NULL, 'Juliana Santos', 'Rua Apolonio de Souza, 33', '(21)33339999', '1996-01-12'), (NULL, 'Priscila Sales', 'Avenida Paulista, 1910', '(88)999990000', '1999-04-15'), (NULL, 'Tereza Cristina', 'Rua Zeca Teles de Meneses', '(31)31111111', '1997-07-14');
```

```sql
INSERT INTO medicos_celular VALUES (NULL, '(11)9.00000000', 1), (NULL, '(11)9.11111111', 2), (NULL, '(11)9.22222222', 2), (NULL, '(11)9.22222223', 1);
```

```sql
INSERT INTO bebes VALUES (NULL, 'Joaquim da Silva', '2020-05-01', 3.250, 49, 2, 1), (NULL, 'Mariana Sales', '2021-07-26', 3.600, 51, 1, 3);
```

```sql
TRUNCATE TABLE bebes;
```

```sql
SELECT * FROM medicos;
```

```sql
SELECT nome, dt_nasc FROM bebes;
```

```sql
SELECT nome, dt_nasc AS data_nascimento FROM bebes;
```

Mostrar todos os bebês que nasceram com mais de 50 cm.

```sql
SELECT * FROM bebes WHERE alt_nasc > 50;
```

Mostrar nome e telefone de todas as mães.

```sql
SELECT nome, telefone FROM maes;
```

Mostrar todos os médicos em que a especialidade é Obstetra.

```sql
SELECT * FROM medicos WHERE especialidade = 'Obstetra';
```

Mostrar todas as mães que nasceram nos anos de 1996 e 1997.

```sql
SELECT * FROM maes WHERE dt_nasc BETWEEN '1996-01-01' AND '1997-12-31';

/* OUTRA FORMA */

SELECT * FROM maes WHERE YEAR(dt_nasc) = 1996 OR YEAR(dt_nasc) = 1997;

/* OUTRA FORMA */

SELECT * FROM maes WHERE YEAR(dt_nasc) BETWEEN 1996 AND 1997;
```

Mostrar todos os bebês que possuam menos de 3,300kg.

```sql
SELECT * FROM bebes WHERE peso_nasc < 3.3;
```

Mostrar o nome, crm e número de celular da Médica Eliana Martins de Lima.

```sql
SELECT medicos.nome, medicos.crm, medicos_celular.numero_celular
FROM medicos INNER JOIN medicos_celular
ON medicos.id_medico = medicos_celular.id_medico
WHERE medicos.id_medico = 2;

/* FORMA ENXUTA */

SELECT m.nome, m.crm, mc.numero_celular
FROM medicos AS m INNER JOIN medicos_celular AS mc
ON m.id_medico = mc.id_medico
WHERE m.id_medico = 2;
```

Mostrar o nome do bebê, nome da mãe do bebê e o nome do médico que fez o parto.

```sql
SELECT b.nome AS nome_bebe, ma.nome AS nome_mae, m.nome AS nome_medico
FROM bebes AS b
INNER JOIN maes AS ma
ON b.id_mae = ma.id_mae
INNER JOIN medicos AS m
ON b.id_medico = m.id_medico;
```

### Exercício 2:

```sql
CREATE DATABASE loja;
```

```sql
USE loja;
```

```sql
CREATE TABLE clientes (
id_cli INT AUTO_INCREMENT,
rg_cli VARCHAR(20) NOT NULL,
nome_cli VARCHAR(100) NOT NULL,
tel_cli VARCHAR(50),
rua VARCHAR(100),
num INT,
bairro VARCHAR(100), 
cep VARCHAR(20),   
CONSTRAINT pk_id_cli PRIMARY KEY(id_cli)
);
```

```sql
CREATE TABLE produtos (
id_prod INT AUTO_INCREMENT,
nome_prod VARCHAR(100) NOT NULL,
tipo_prod VARCHAR(100) NOT NULL,
preço_prod FLOAT NOT NULL,
estoque_prod INT,
CONSTRAINT pk_id_prod PRIMARY KEY(id_prod)
);
```

```sql
CREATE TABLE compras (
id_compra INT AUTO_INCREMENT,
data_compra DATE NOT NULL,
valor_compra FLOAT NOT NULL,
id_cli INT,   
CONSTRAINT pk_id_compra PRIMARY KEY(id_compra),
CONSTRAINT fk_compra_cliente FOREIGN KEY(id_cli) REFERENCES clientes(id_cli)
);
```

```sql
CREATE TABLE compras_contem_produtos (
id INT AUTO_INCREMENT,
id_compra INT,
id_prod INT,
quantidade INT NOT NULL,   
CONSTRAINT pk_id_compra_produtos PRIMARY KEY(id),
CONSTRAINT fk_ccp_compra FOREIGN KEY(id_compra) REFERENCES compras(id_compra),
CONSTRAINT fk_ccp_produto FOREIGN KEY(id_prod) REFERENCES produtos(id_prod)
);
```

```sql
ALTER TABLE clientes
ADD cidade VARCHAR(100);
```

```sql
ALTER TABLE clientes
ADD estado VARCHAR(100);
```

```sql
ALTER TABLE compra
DROP CONSTRAINT fk_compras_clientes;
```

```sql
ALTER TABLE tabela
ADD CONSTRAINT fk_nome_da_constraint
FOREIGN KEY(atributo_chave)
REFERENCES tabela(atributo_chave)
ON UPDATE CASCADE
ON DELETE CASCADE;
```

```sql
INSERT INTO clientes
VALUES 
(NULL,'42.515.012-4','Leonardo Diego das Neves','(68)9.8106-8326','Avenida Santos Dumont',160,'Centro','69934-970','Epitaciolândia','AC'),
(NULL,'35.993.799-8','Vallentina Jenniffer Livia','(64) 98941-7452','Avenida 11 de Novembro',729,'Setor Central','75619-970','Aloândia','GO'),
(NULL,'14.594.456-6','Benedito Henry Teixeira','(88) 99690-4161','Rua Eduardo Mota',640,'Centro','62420-970','Chaval','CE'),
(NULL,'11.946.174-2','Mariah Jaqueline Aparício','(88) 3753-8770','Rua Santa Isabel',539,'São Miguel','63010-555','Juazeiro do Norte','CE'),
(NULL,'27.722.583-8','Alice Pietra Ramos','(31) 99404-8773','Rua Doutor Álvaro Lobo Leite',521,'Centro','36419-970','Lobo Leite','MG'),
(NULL,'38.895.346-9','Mário Márcio Ruan Pinto','(13) 98485-6954','Rua Rubião Júnior',418,'Centro','11013-210','Santos','SP');
```

```sql
INSERT INTO compras
VALUES 
(NULL,'2022-10-05',58.8,4),
(NULL,'2022-10-05',110,1),
(NULL,'2022-10-07',81.7,3),
(NULL,'2022-10-07',51,6);
```

```sql
INSERT INTO produtos
VALUES 
(NULL,'Energético TNT 269ML','Bebidas',5.5,35),
(NULL,'Arroz Juliano Parboilizado','Arroz',4.5,150),
(NULL,'Arroz Juliano Branco','Arroz',4.2,122),
(NULL,'Coca Cola 1 litro','Bebidas',8.5,36),
(NULL,'Biscoito Recheado Bolão Morango','Doces',2.7,45),
(NULL,'Água Mineral sem Gás','Bebidas',2,266),
(NULL,'Chocolate Gutti Gutti 50g','Doces',1.9,61),
(NULL,'Suco de Laranja Laranjinha','Bebidas',3,16);
```

```sql
INSERT INTO compras_contem_produtos
VALUES 
(NULL,1,3,10),
(NULL,1,5,4),
(NULL,1,8,2),
(NULL,2,2,20),
(NULL,2,6,10),
(NULL,3,1,4),
(NULL,3,3,10),
(NULL,3,7,3),
(NULL,3,8,4),
(NULL,4,4,6);
```

### Exercício 3:

Mostrar todos os dados de Clientes.

```sql
SELECT * FROM clientes;
```

Mostrar nome, rg e telefone dos Clientes.

```sql
SELECT rg_cli, nome_cli, tel_cli FROM clientes;
```

Mostrar nome e preço de Todos os Produtos.

```sql
SELECT nome_prod, preço_prod FROM produtos;
```

Mostrar Nome, preço e estoque das Bebidas.

```sql
SELECT nome_prod, preço_prod, estoque_prod 
FROM produtos 
WHERE tipo_prod = 'bebidas';
```

Mostrar todos os produtos com preço acima de 5 reais.

```sql
SELECT * FROM produtos WHERE preço_prod > 5;
```

Mostrar a quantidade total de produtos em estoque.

```sql
SELECT SUM(estoque_prod) FROM produtos;
```

Mostrar a soma de todas as compras.

```sql
SELECT SUM(valor_compra) FROM compras;
```

Mostrar todos os produtos ordenados pelo nome (A-Z).

```sql
SELECT * FROM produtos ORDER BY nome_prod;
```

Mostrar o nome e o valor total da compra realizada pela cliente Mariah Jaqueline Aparício.

```sql
SELECT cl.nome_cli, co.valor_compra
FROM clientes AS cl INNER JOIN compras AS co
ON cl.id_cli = co.id_cli
WHERE cl.nome_cli = 'Mariah Jaqueline Aparício';
```

Mostrar todos os clientes que são do estado de SP ou do  CE.

```sql
SELECT * FROM clientes 
WHERE estado = 'SP' OR estado = 'CE';
```

Mostrar todos os clientes que são do estado do CE e do bairro Centro.

```sql
SELECT * FROM clientes 
WHERE estado = 'CE' AND bairro = 'centro';
```

Mostrar a lista de produtos ordenados pelo preço do menor para o maior.

```sql
SELECT * FROM produtos ORDER BY preço_prod;
```

Mostrar uma lista dos produtos que foram comprados pelo cliente Benedito Henry Teixeira, bem como seu nome e endereço completo.

```sql
SELECT p.nome_prod, cl.nome_cli, cl.rua, cl.num, cl.bairro, cl.cep, cl.cidade, cl.estado
FROM produtos AS p
INNER JOIN compras_contem_produtos AS ccp
ON p.id_prod = ccp.id_prod
INNER JOIN compras AS co
ON ccp.id_compra = co.id_compra
INNER JOIN clientes AS cl
ON cl.id_cli = co.id_cli
WHERE cl.nome_cli = 'Benedito Henry Teixeira';
```

Mostrar a quantidade de clientes que são do estado do CE.

```sql
SELECT COUNT(*) FROM clientes WHERE estado = 'CE';
```

Mostrar a soma dos estoques de todas as bebidas do estabelecimento.

```sql
SELECT SUM(estoque_prod) FROM produtos WHERE tipo_prod = 'bebidas';
```

### Consultas utilizadas no BigQuery

Renomear as colunas _regiao*_* e _estado_ para regiao e estado respectivamente.

```sql
SELECT _regiao_ AS regiao, _estado_ AS estado 
FROM `aulas-bc26-giovana.dados_covid.dados_covid_nacional`;
```

Substituir as aspas simples em regiao e estado por caractere vazio.

```sql
SELECT replace(_regiao_, "'", '') AS regiao, replace(_estado_, "'", '') AS estado 
FROM `aulas-bc26-giovana.dados_covid.dados_covid_nacional`;
```

Verificar a quantidade de registros por região.

```sql
SELECT _regiao_ AS regiao, count(*) AS qtde_por_regiao 
FROM aulas-bc26-giovana.dados_covid.dados_covid_nacional
WHERE _regiao_ != "Brasil" group by regiao;
```

Verificar a quantidade de registros por estado.

```sql
SELECT _estado_ AS estado, count(*) AS qtde_por_estado 
FROM aulas-bc26-giovana.dados_covid.dados_covid_nacional
WHERE _estado_ != "Brasil" group by estado;
```

Verificar dados de estado que estão nulos.

```sql
SELECT _regiao_ AS regiao, _estado_ AS estado 
FROM aulas-bc26-giovana.dados_covid.dados_covid_nacional
WHERE _estado_ IS NULL;
```

Substituir valores nulos.

```sql
SELECT CASE 
WHEN _estado_ IS NULL 
THEN "ND" 
ELSE replace(_estado_, "'", "") END AS estado, count(*) as qtde_por_estado 
FROM dados_covid.dados_covid_nacional 
GROUP BY estado;
```

```sql
SELECT CASE WHEN _regiao_ IS NULL THEN "ND" 
ELSE replace(_regiao_, "'", "") END AS regiao, 
CASE WHEN _estado_ IS NULL THEN "ND" 
ELSE replace(_estado_, "'", "") END AS estado,
CASE WHEN _municipio_ IS NULL THEN "ND" 
ELSE replace(_municipio_, "'", "") END AS municipio,
CASE WHEN _coduf_ IS NULL THEN "ND" 
ELSE replace(_coduf_, "'", "") END AS coduf,
_codmun_ AS codmun,
_codRegiaoSaude_ AS codregiaosaude,
CASE WHEN _nomeRegiaoSaude_ IS NULL THEN "ND" 
ELSE replace(_nomeRegiaoSaude_, "'", "") END AS nomeregiaosaude,
_semanaEpi_ AS semanaepi,
CASE WHEN _populacaoTCU2019_ IS NULL THEN "ND" 
ELSE replace(_populacaoTCU2019_, "'", "") END AS poptcu2019,
_casosAcumulado_ AS casosacumulado,
_casosNovos_ AS casosnovos,
_obitosAcumulado_ AS obitosacumulado,
_obitosNovos_ AS obitosnovos,
_Recuperadosnovos_ AS recuperadosnovos,
_emAcompanhamentoNovos_ AS emacompanhamentonovos,
_FgMetro_ AS fgmetro,
FROM dados_covid.dados_covid_nacional;
```

Criando uma tabela usando outra.

```sql
CREATE OR REPLACE TABLE dados_covid.dados_covid_nacional_2 AS (
SELECT CASE WHEN _regiao_ IS NULL THEN "ND" 
ELSE replace(_regiao_, "'", "") END AS regiao, 
CASE WHEN _estado_ IS NULL THEN "ND" 
ELSE replace(_estado_, "'", "") END AS estado,
CASE WHEN _municipio_ IS NULL THEN "ND" 
ELSE replace(_municipio_, "'", "") END AS municipio,
CASE WHEN _coduf_ IS NULL THEN "ND" 
ELSE replace(_coduf_, "'", "") END AS coduf,
_codmun_ AS codmun,
_codRegiaoSaude_ AS codregiaosaude,
CASE WHEN _nomeRegiaoSaude_ IS NULL THEN "ND" 
ELSE replace(_nomeRegiaoSaude_, "'", "") END AS nomeregiaosaude,
_semanaEpi_ AS semanaepi,
CASE WHEN _populacaoTCU2019_ IS NULL THEN "ND" 
ELSE replace(_populacaoTCU2019_, "'", "") END AS poptcu2019,
_casosAcumulado_ AS casosacumulado,
_casosNovos_ AS casosnovos,
_obitosAcumulado_ AS obitosacumulado,
_obitosNovos_ AS obitosnovos,
_Recuperadosnovos_ AS recuperadosnovos,
_emAcompanhamentoNovos_ AS emacompanhamentonovos,
_FgMetro_ AS fgmetro,
FROM dados_covid.dados_covid_nacional);
```

Extraindo datas em diferentes formatos.

```sql
/* ANOMES - 6 dígitos (202205) */

SELECT concat(format_date('%Y',data), format_date('%m',data)) as ano_mes
FROM dados_covid.dados_covid_nacional;

/* OUTRA FORMA */

SELECT CASE WHEN CHAR_LENGTH(CAST(EXTRACT(month FROM _data_) as string)) = 1
THEN CONCAT(EXTRACT(year FROM _data_), '0',EXTRACT(month FROM _data_))
ELSE CONCAT(EXTRACT(year FROM _data_),EXTRACT(month FROM _data_))
END AS ano_mes FROM dados_covid.dados_covid_nacional;
```