# WMSExpert
**Documentação de integração WMSExpert**

> As Views de cadastro tem como função principal integrar as duas bases de dados, permitindo que os cadastros sejam feitos apenas no Erp e que possam ser importados integralmente para o WMS Expert, sem retrabalho.

> ### View de cidades WMS_CIDADE

``` 
CREATE VIEW WMS_CIDADE AS 
SELECT 
codCidadeIBGE,
nomeCidade,
uf
FROM CIDADES
```

**codCidadeIBGE:** *O Campo deve ser **inteiro**, o mesmo e chave primaria.* <br />
**nomeCidade:** *O Campo deve ser **varchar(100)** e deve conter a descrição da cidade.* <br />
**uf:** *O campo deve ser **varchar(2)** e deve conter a abreviatura do estado da cidade.* <br />

> ### View de clientes WMS_CLIENTE

``` 
CREATE VIEW WMS_CLIENTE AS 
SELECT 
codCliente,
tipo,
cpfCnpj,
nomCliente,
nomFantasia,
codCidadeIbge,
endereco,
numEndereco,
bairro,
cep
FROM CLIENTES
```

**codCliente:** *Para que o codigo do WMS e do ERP sejam os mesmos o campo deve ser **inteiro**, caso seja **alfanumerico** o WMS irá gerar sua propria numeração e guardar o codigo do ERP em outro campo.* <br />
**tipo:** *O campo deve ser **inteiro** contendo 0 para pessoa fisica e 1 para pessoa juridica.* <br />
**cpfCnpj:** *O campo deve ser **varchar(14)** contendo a inscrição da pessoa fisica ou juridica.* <br />
**nomCliente:** *O campo deve ser **varchar(60)** contendo a razão social do cliente.* <br />
**nomFantasia:** *O campo deve ser **varchar(60)** contendo o nome fantasia do cliente.* <br />
**codCidadeIBGE:** *O Campo deve ser **inteiro**, o mesmo e chave primaria.* <br />
**endereco:** *O campo deve ser **varchar(60)** contendo o endereço do cliente.* <br />
**numEndereco:** *O campo deve ser **varchar(10)** contendo o numero do endereço do cliente.* <br />
**bairro:** *O campo deve ser **varchar(30)** contendo a descrição do bairro do cliente.* <br />
**cep:** *O campo deve ser **varchar(8)** contendo o contendo o codigo postal do cliente.* <br />

> ### View de embalagens WMS_EMBALAGEM

``` 
CREATE VIEW WMS_EMBALAGEM AS 
SELECT 
codEmbalagem,
codFilial,
codProduto,
aux,
und,
qtdUnit,
embalagem
FROM EMBALAGENS
```

**codEmbalagem:** *Enviar o campo como **NULL**.* <br />
**codFilial:** *O Campo deve ser **inteiro**, o mesmo e chave primaria.* <br />
**codProduto:** *O campo deve possuir a chave estrangeira do produto.* <br />
**aux:** *O campo deve ser **varchar(20)** contendo o codigo de barras do produto.* <br />
**und:** *O campo deve ser **varchar(3)** contendo a descrição reduzida da embalagem.* <br />
**qtdUnit:** *O Campo deve ser **numerico(12,2)**, contendo o fator de conversão da unidade.* <br />
**embalagem:** *O campo deve ser **varchar(20)** contendo a descrição da embalagem.* <br />

> ### View de estoque WMS_ESTOQUE

``` 
CREATE VIEW WMS_ESTOQUE AS 
SELECT 
codFilial,
codProduto,
qtdEstoque
FROM ESTOQUE
```

**codFilial:** *O Campo deve ser **inteiro**, o mesmo e chave primaria.* <br />
**nomFantasia:** *O campo deve ser **varchar(60)** contendo o nome fantasia do cliente.* <br />
**qtdEstoque:** *O Campo deve ser **numerico(18,2)**, contendo a quantidade de estoque do produto.* <br />

> ### View de filial WMS_FILIAL

``` 
CREATE VIEW WMS_FILIAL AS 
SELECT 
codFilial,
nomFilial,
cnpj,
ativo,
nomFantasia
FROM FILIAL
```

**codFilial:** *O Campo deve ser **inteiro**, o mesmo e chave primaria.* <br />
**nomFilial:** *O campo deve ser **varchar(50)** contendo o nome da filial.* <br />
**cnpj:** *O Campo deve ser **varchar(17)**, contendo o cnpj da filial.* <br />
**ativo:** *O Campo deve ser **inteiro**, contendo 1 para ativo e 0 para inativo.* <br />
**nomFantasia:** *O campo deve ser **varchar(50)** contendo a fantasia da filial.* <br />

> ### View de fornecedor WMS_FORNECEDOR

``` 
CREATE VIEW WMS_FORNECEDOR AS 
SELECT 
codFornecedor,
nomeFornecedor,
nomeFantasia,
tipo,
cnpjcpf,
endereco,
numEndereco,
bairro,
codCidadeIbge,
cep
FROM FORNECEDOR
```

**codFornecedor:** *Para que o codigo do WMS e do ERP sejam os mesmos o campo deve ser **inteiro**, caso seja **alfanumerico** o WMS irá gerar sua propria numeração e guardar o codigo do ERP em outro campo.* <br />
**nomeFornecedor:** *O campo deve ser **varchar(60)** contendo a razão social do fornecedor.* <br />
**nomeFantasia:** *O campo deve ser **varchar(50)** contendo o nome fantasia do fornecedor.* <br />
**tipo:** *O campo deve ser **inteiro** contendo 0 para pessoa fisica e 1 para pessoa juridica.* <br />
**cpfCnpj:** *O campo deve ser **varchar(14)** contendo a inscrição da pessoa fisica ou juridica.* <br />
**endereco:** *O campo deve ser **varchar(60)** contendo o endereço do fornecedor.* <br />
**numEndereco:** *O campo deve ser **varchar(10)** contendo o numero do endereço do fornecedor.* <br />
**bairro:** *O campo deve ser **varchar(30)** contendo a descrição do bairro do fornecedor.* <br />
**codCidadeIBGE:** *O Campo deve ser **inteiro**, o mesmo e chave primaria.* <br />
**cep:** *O campo deve ser **varchar(8)** contendo o contendo o codigo postal do fornecedor.* <br />

> ### View de funcionario WMS_FUNCIONARIO

``` 
CREATE VIEW WMS_FUNCIONARIO AS 
SELECT 
codFuncionario,
nomefuncionario,
cpf,
codCidIbge,
ativo,
codSeparadorErp,
endereco,
complemento,
numero,
cep,
bairro
FROM FUNCIONARIO
```

**codFuncionario:** *Para que o codigo do WMS e do ERP sejam os mesmos o campo deve ser **inteiro**, caso seja **alfanumerico** o WMS irá gerar sua propria numeração e guardar o codigo do ERP em outro campo.* <br />
**nomefuncionario:** *O campo deve ser **varchar(60)** contendo o nome do funcionario.* <br />
**cpf:** *O campo deve ser **varchar(50)** contendo o cpf do funcionario.* <br />
**codCidIbge:** *O Campo deve ser **inteiro**, o mesmo e chave primaria.* <br />
**ativo:** *O campo deve ser **inteiro** contendo 0 para inativo e 1 para ativo.* <br />
**codSeparadorErp:** *O campo deve ser **varchar(50)** contendo o código de separador do funcionário, caso não possua deixar
como NULL.* <br />
**endereco:** *O campo deve ser **varchar(60)** contendo o endereço do funcionario.* <br />
**complemento:** *O campo deve ser **varchar(30)** contendo o complemento do endereco.* <br />
**numero:** *O campo deve ser **varchar(10)** contendo o numero do endereço do funcionario.* <br />
**cep:** *O campo deve ser **varchar(8)** contendo o contendo o codigo postal do funcionario.* <br />
**bairro:** *O campo deve ser **varchar(30)** contendo a descrição do bairro do funcionario.* <br />

> ### View de grupo de produto WMS_GRUPO

``` 
CREATE VIEW WMS_GRUPO AS 
SELECT 
codGrupo,
desGrupo,
ativo
FROM GRUPO
```

**codGrupo:** *Para que o codigo do WMS e do ERP sejam os mesmos o campo deve ser **inteiro**, caso seja **alfanumerico** o WMS irá gerar sua propria numeração e guardar o codigo do ERP em outro campo.* <br />
**desGrupo:** *O campo deve ser **varchar(50)** contendo o nome do funcionario.* <br />
**ativo:** *O campo deve ser **inteiro** contendo 0 para inativo e 1 para ativo.* <br />

> ### View de produto WMS_PRODUTO

``` 
CREATE VIEW WMS_PRODUTO AS 
SELECT 
codProduto,
descProd,
situacao,
refProd,
revenda,
vlrUltimaCompra,
codFornecedor,
codGrupo
FROM PRODUTO
```

**codProduto:** *Para que o codigo do WMS e do ERP sejam os mesmos o campo deve ser **inteiro**, caso seja **alfanumerico** o WMS irá gerar sua propria numeração e guardar o codigo do ERP em outro campo.* <br />
**descProd:** *O campo deve ser **varchar(50)** contendo a descrição do produto.* <br />
**situacao:** *O campo deve ser **inteiro** contendo 0 para inativo e 1 para ativo.* <br />
**refProd:** *O campo deve ser **varchar(10)** contendo a referencia do produto.* <br />
**revenda:** *O campo deve ser **inteiro** contendo 0 para inativo e 1 para ativo.* <br />
**vlrUltimaCompra:** *O campo deve ser **numerico(10,2)** contendo o preço de custo do produto.* <br />
**codFornecedor:** *O Campo deve conter o codigo do fornecedor do produto.* <br />
**codGrupo:** *O campo deve conter o codigo do grupo do produto.* <br />

