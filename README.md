# WMSExpert
**Documentação de integração WMSExpert**

# Importação de dados cadastrais <br />

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

**codCidadeIBGE:** *O campo deve ser **inteiro**, o mesmo e chave primaria.* <br />
**nomeCidade:** *O campo deve ser **varchar(100)** e deve conter a descrição da cidade.* <br />
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
**codCidadeIBGE:** *O campo deve ser **inteiro**, o mesmo e chave primaria.* <br />
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
**codFilial:** *O campo deve ser **inteiro**, o mesmo e chave primaria.* <br />
**codProduto:** *O campo deve possuir a chave estrangeira do produto.* <br />
**aux:** *O campo deve ser **varchar(20)** contendo o codigo de barras do produto.* <br />
**und:** *O campo deve ser **varchar(3)** contendo a descrição reduzida da embalagem.* <br />
**qtdUnit:** *O campo deve ser **numerico(12,2)**, contendo o fator de conversão da unidade.* <br />
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

**codFilial:** *O campo deve ser **inteiro**, o mesmo e chave primaria.* <br />
**nomFantasia:** *O campo deve ser **varchar(60)** contendo o nome fantasia do cliente.* <br />
**qtdEstoque:** *O campo deve ser **numerico(18,2)**, contendo a quantidade de estoque do produto.* <br />

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

**codFilial:** *O campo deve ser **inteiro**, o mesmo e chave primaria.* <br />
**nomFilial:** *O campo deve ser **varchar(50)** contendo o nome da filial.* <br />
**cnpj:** *O campo deve ser **varchar(17)**, contendo o cnpj da filial.* <br />
**ativo:** *O campo deve ser **inteiro**, contendo 1 para ativo e 0 para inativo.* <br />
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
**codCidadeIBGE:** *O campo deve ser **inteiro**, o mesmo e chave primaria.* <br />
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
**codCidIbge:** *O campo deve ser **inteiro**, o mesmo e chave primaria.* <br />
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
**codGrupo:** *O campo deve conter o codigo do grupo do produto.* <br /><br /><br />

# Importação de movimentos <br />

> As Views de entrada de produtos são todas as que compreendem processos aonde a mercadoria será recebida, como por exemplo: Recebimento de notas fiscais de fornecedores, devoluções de clientes, devoluções de garantia.

> ### View do bonus de entrada WMS_BONUSCAB

``` 
CREATE VIEW WMS_BONUSCAB AS 
SELECT 
codBonusCab,
codFilial,
data
FROM BONUSCAB
```

**Somente deve conter essa View em caso de possuir o processo de agrupamentos de notas de entrada**

**codBonusCab:** *O campo deve ser **inteiro**, contendo o numero do bonus.* <br />
**codFilial:** *O campo deve conter a chave da filial.* <br />
**data:** *O campo deve ser **data** e deve conter a data de montagem do bonus.* <br />

> ### View de notas fiscais de entrada WMS_NOTAFISCALENTRADA

``` 
CREATE VIEW WMS_NOTAFISCALENTRADA AS 
SELECT 
codNotaFiscal,
codFilial,
codFilialIntegracao,
codBonusCab,
numNotaFiscal,
codFornecedor,
tipo,
dtEmissao,
valTotProduto,
valTotNotaFiscal
FROM NOTAFISCALENTRADA
```

**codNotaFiscal:** *O campo deve ser **NULL**.* <br />
**codFilial:** *O campo deve conter a chave da filial.* <br />
**codFilialIntegracao:** *O campo deve conter a chave da filial de origem (somente usar em casos de multi filial).* <br />
**codBonusCab:** *O campo deve ser **inteiro**, contendo o numero do bonus.* <br />
**numNotaFiscal:** *O campo deve ser **inteiro**, contendo o numero da nota fiscal.* <br />
**codFornecedor:** *O Campo deve conter o codigo do fornecedor da nota.* <br />
**tipo:** *O campo deve ser **inteiro**, contendo o modelo do documento: Compra = 55, Devolução = 9, Transferencia = 8.* <br />
**dtEmissao:** *O campo deve ser **data** e deve conter a data de montagem do bonus.* <br />
**valTotProduto:** *O campo deve ser **numerico(18,2)** contendo a soma do valor total dos produtos.* <br />
**valTotNotaFiscal:** *O campo deve ser **numerico(15,2)** contendo o valor total da nota fiscal de entrada.* <br />

> ### View de notas fiscais de entrada WMS_NOTAFISCALITEMENTRADA

``` 
CREATE VIEW WMS_NOTAFISCALITEMENTRADA AS 
SELECT 
codNotaFiscalItem,
codNotaFiscal,
codFilial,
codFilialIntegracao,
codBonusCab,
codFornecedor,
tipo,
codProduto,
unidade,
quantidade,
valUnitario
FROM NOTAFISCALITEMENTRADA
```

**codNotaFiscalItem:** *O campo deve ser **NULL**.* <br />
**codNotaFiscal:** *O campo deve ser **inteiro**, contendo o numero da nota fiscal.* <br />
**codFilial:** *O campo deve conter a chave da filial.* <br />
**codFilialIntegracao:** *O campo deve conter a chave da filial de origem (somente usar em casos de multi filial).* <br />
**codBonusCab:** *O campo deve ser **inteiro**, contendo o numero do bonus.* <br />
**codFornecedor:** *O Campo deve conter o codigo do fornecedor da nota.* <br />
**tipo:** *O campo deve ser **inteiro**, contendo o modelo do documento: Compra = 55, Devolução = 9, Transferencia = 8.* <br />
**codProduto:** *Chave estrangeira do codigo do produto* <br />
**unidade:** *O campo deve ser **varchar(3)** contendo a abreviação da embalagem.* <br />
**quantidade:** *O campo deve ser **numerico(12,4)** contendo a quantidade do produto.* <br />
**valUnitario:** *O campo deve ser **numerico(16,2)** contendo o valor unitario do produto.* <br />

> As Views de saída de produtos são todas as que compreendem processos aonde a mercadoria será separada para entrega, como por exemplo: Pedidos de venda, pedidos de
devolução de produtos a fornecedores, pedidos de demonstração.

> ### View de pedidos WMS_PEDIDOSCAB

``` 
CREATE VIEW WMS_PEDIDOSCAB AS 
SELECT 
codPedidoCab,
codFilial,
codFilialIntegracao,
codCliente,
codVendedor,
numNota,
tipoPedido,
odemPedido,
dtGeracao,
qtdTotalItens,
valorTotal
FROM PEDIDOSCAB
```

**codPedidoCab:** *O campo so deve ser preenchido se o valor for **inteiro**, caso o contrario o campo deve ser **NULL**.* <br />
**codFilial:** *O campo deve conter a chave da filial.* <br />
**codFilialIntegracao:** *O campo deve conter a chave da filial de origem (somente usar em casos de multi filial).* <br />
**codCliente:** *O Campo deve conter o codigo do cliente do pedido.* <br />
**codVendedor:** *O Campo deve conter o codigo do funcionario da pedido.* <br />
**numNota:** *O campo so deve ser preenchido se o valor do pedido for **NULL**, contendo o numero do pedido.* <br />
**tipoPedido:** *O campo deve ser **varchar(20)**, contendo a descrição do tipo do pedido EX: Venda, Balcão, Bonificação, etc..* <br />
**odemPedido:** *O campo deve ser **inteiro**, contendo o nivel de prioridade do pedido, 0 – Urgente, 1 – Alta, 2 -Media, 3 – Baixa.* <br />
**dtGeracao:** *O campo deve ser **data** e deve conter a data de montagem do bonus.* <br />
**qtdTotalItens:** *O campo deve ser **inteiro** contendo a quantidade de itens no documento.* <br />
**valTotProduto:** *O campo deve ser **numerico(16,2)** contendo o valor total do documento.* <br />

> ### View de itens dos pedidos WMS_PEDIDOSITEM

``` 
CREATE VIEW WMS_PEDIDOSITEM AS 
SELECT 
codPedidoItem,
codPedidoCab,
codFilial,
codProduto,
valorUnitario,
qtdProduto,
valorTotal
FROM PEDIDOSITEM
```

**codPedidoItem:** *O campo deve ser **inteiro**, conter o codigo sequencial dos itens.* <br />
**codPedidoCab:** *O campo deve conter a chave estrangeira do pedido.* <br />
**codFilial:** *O campo deve conter a chave da filial.* <br />
**codProduto:** *Chave estrangeira do codigo do produto* <br />
**valorUnitario:** *O campo deve ser **numerico(12,2)** contendo o valor unitario do produto.* <br />
**qtdProduto:** *O campo deve ser **numerico(12,4)** contendo a quantidade do produto.* <br />
**valorTotal:** *O campo deve ser **numerico(12,2)** contendo o valor total do produto.* <br />
