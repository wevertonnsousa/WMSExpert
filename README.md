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
codClienteErp,
tipo,
cpfCnpj,
nomCliente,
nomFantasia,
codCidadeIbge,
endereco,
numEndereco,
bairro,
cep,
celular,
email,
codRota,
desRota,
latitude,
longitude,
shelf
FROM CLIENTES
```

**codCliente:** *Somente enviar se o codigo do cliente for **inteiro**, contendo o codigo do cliente do ERP* <br />
**codClienteErp:** *Somente enviar se o codigo do cliente for **varchar(20)**, contendo o codigo do cliente do ERP* <br />
**tipo:** *O campo deve ser **inteiro** contendo 0 para pessoa fisica e 1 para pessoa juridica o campo e **obrigatorio**.* <br />
**cpfCnpj:** *O campo deve ser **varchar(14)** contendo a inscrição da pessoa fisica ou juridica o campo e **obrigatorio**.* <br />
**nomCliente:** *O campo deve ser **varchar(60)** contendo a razão social do cliente o campo e **obrigatorio**.* <br />
**nomFantasia:** *O campo deve ser **varchar(60)** contendo o nome fantasia do cliente o campo e **obrigatorio**.* <br />
**codCidadeIBGE:** *O campo deve ser **inteiro**, o mesmo e chave primaria o campo e **obrigatorio**.* <br />
**endereco:** *O campo deve ser **varchar(60)** contendo o endereço do cliente o campo e **obrigatorio**.* <br />
**numEndereco:** *O campo deve ser **varchar(10)** contendo o numero do endereço do cliente o campo e **obrigatorio**.* <br />
**bairro:** *O campo deve ser **varchar(30)** contendo a descrição do bairro do cliente o campo e **obrigatorio**.* <br />
**cep:** *O campo deve ser **varchar(8)** contendo o contendo o codigo postal do cliente o campo e **obrigatorio**.* <br />
**celular:** *O campo deve ser **varchar(10)** contendo o telefone do cliente.* <br />
**email:** *O campo deve ser **varchar(50)** contendo o e-mail do cliente.* <br />
**codRota:** *O campo deve ser **inteiro** contendo o codigo da rota.* <br />
**desRota:** *O campo deve ser **varchar(60)** contendo a descrição da rota.* <br />
**latitude:** *O campo deve ser **numeric(18,7)** contendo a latitudo do cliente.* <br />
**longitude:** *O campo deve ser **numeric(18,7)** contendo a longitude do cliente.* <br />
**shelf:** *O campo deve ser **inteiro** contendo a quantidade de dias do shelf do cliente.* <br /><br />

**Se o código do cliente for inteiro o campo codCliente e obrigatório se não o codClienteErp e obrigatório, somente preencher um dos 2.** <br />

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
embalagem,
pesoLiquido,
pesoBruto,
volume
FROM EMBALAGENS
```

**codEmbalagem:** *Enviar o campo como **NULL**.* <br />
**codFilial:** *O campo deve ser **inteiro**, o mesmo e chave primaria o campo e **obrigatorio**.* <br />
**codProduto:** *O campo deve possuir a chave estrangeira do produto o campo e **obrigatorio**.* <br />
**aux:** *O campo deve ser **varchar(20)** contendo o codigo de barras do produto o campo e **obrigatorio**.* <br />
**und:** *O campo deve ser **varchar(3)** contendo a descrição reduzida da embalagem o campo e **obrigatorio**.* <br />
**qtdUnit:** *O campo deve ser **numerico(12,2)**, contendo o fator de conversão da unidade o campo e **obrigatorio** e tem de ser diferente de zero.* <br />
**embalagem:** *O campo deve ser **varchar(20)** contendo a descrição da embalagem o campo e **obrigatorio**.* <br />
**pesoLiquido:** *O campo deve ser **numeric(18,4)** contendo o peso liquido da embalagem.* <br />
**pesoBruto:** *O campo deve ser **numeric(18,4** contendo o peso bruto da embalagem.* <br />
**volume:** *O campo deve ser **numeric(18,2)** contendo a o volume em **m3** da embalagem.* <br />

> ### View de estoque WMS_ESTOQUE

``` 
CREATE VIEW WMS_ESTOQUE AS 
SELECT 
codFilial,
codProduto,
qtdEstoque
FROM ESTOQUE
```

**codFilial:** *O campo deve ser **inteiro**, o mesmo e chave primaria o campo e **obrigatorio**.* <br />
**codProduto:** *Chave estrangeira do codigo do produto o campo e **obrigatorio**.* <br />
**qtdEstoque:** *O campo deve ser **numerico(18,2)**, contendo a quantidade de estoque do produto o campo e **obrigatorio**.* <br />

> ### View de filial WMS_FILIAL

``` 
CREATE VIEW WMS_FILIAL AS 
SELECT 
codFilial,
codFilialWs,
nomFilial,
nomFantasia,
cnpj,
ativo,
codCidadeIbge
FROM FILIAL
```

**codFilial:** *O campo deve ser **inteiro**, o mesmo e chave primaria.* <br />
**codFilialWs:** *O campo deve ser **varchar(100)** contendo o codigo da filial se o valor não for inteiro.* <br />
**nomFilial:** *O campo deve ser **varchar(50)** contendo o nome da filial o campo e **obrigatorio**.* <br />
**nomFantasia:** *O campo deve ser **varchar(50)** contendo a fantasia da filial o campo e **obrigatorio**.* <br />
**cnpj:** *O campo deve ser **varchar(17)**, contendo o cnpj da filial o campo e **obrigatorio**.* <br />
**ativo:** *O campo deve ser **inteiro**, contendo 1 para ativo e 0 para inativo o campo e **obrigatorio**.* <br />
**codCidadeIbge:** *O campo deve ser **inteiro**, contendo o codigo da cidadeIbge.* <br /><br />

**Se o código da filial for inteiro o campo codFilial e obrigatório, caso contrário, o campo codFilialWs será o campo obrigatório.** <br />

> ### View de fornecedor WMS_FORNECEDOR

``` 
CREATE VIEW WMS_FORNECEDOR AS 
SELECT 
codFornecedor,
codFornecedorErp,
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

**codFornecedor:** *O campo deve ser **inteiro**, contendo o codigo do fornecedor.* <br />
**codFornecedorErp:** *O campo deve ser **varchar(20)**, contendo o codigo do fornecedor se o mesmo for **alfanumerico**.* <br />
**nomeFornecedor:** *O campo deve ser **varchar(60)** contendo a razão social do fornecedor o campo e **obrigatorio**.* <br />
**nomeFantasia:** *O campo deve ser **varchar(50)** contendo o nome fantasia do fornecedor o campo e **obrigatorio**.* <br />
**tipo:** *O campo deve ser **inteiro** contendo 0 para pessoa fisica e 1 para pessoa juridica o campo e **obrigatorio**.* <br />
**cpfCnpj:** *O campo deve ser **varchar(14)** contendo a inscrição da pessoa fisica ou juridica o campo e **obrigatorio**.* <br />
**endereco:** *O campo deve ser **varchar(60)** contendo o endereço do fornecedor.* <br />
**numEndereco:** *O campo deve ser **varchar(10)** contendo o numero do endereço do fornecedor.* <br />
**bairro:** *O campo deve ser **varchar(30)** contendo a descrição do bairro do fornecedor.* <br />
**codCidadeIBGE:** *O campo deve ser **inteiro**, o mesmo e chave primaria o campo e **obrigatorio**.* <br />
**cep:** *O campo deve ser **varchar(8)** contendo o contendo o codigo postal do fornecedor.* <br /><br />

**Se o código do fornecedor for inteiro o campo codFornecedor e obrigatório, caso contrário, o campo codFornecedorErp será o campo obrigatório.** <br />

> ### View de funcionario WMS_FUNCIONARIO

``` 
CREATE VIEW WMS_FUNCIONARIO AS 
SELECT 
codFuncionario,
nomefuncionario,
cpf,
codCidIbge,
ativo,
endereco,
complemento,
numero,
cep,
bairro
FROM FUNCIONARIO
```

**codFuncionario:** *Para que o codigo do WMS e do ERP sejam os mesmos o campo deve ser **inteiro**, caso seja **alfanumerico** o WMS irá gerar sua propria numeração e guardar o codigo do ERP em outro campo o campo e **obrigatorio**.* <br />
**nomefuncionario:** *O campo deve ser **varchar(60)** contendo o nome do funcionario o campo e **obrigatorio**.* <br />
**cpf:** *O campo deve ser **varchar(50)** contendo o cpf do funcionario.* <br />
**codCidIbge:** *O campo deve ser **inteiro**, o mesmo e chave primaria.* <br />
**ativo:** *O campo deve ser **inteiro** contendo 0 para inativo e 1 para ativo o campo e **obrigatorio**.* <br />
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
codGrupoExt,
desGrupo,
ativo
FROM GRUPO
```

**codGrupo:** *O campo deve ser **inteiro**, contendo o codigo do grupo se o mesmo for **inteiro**.* <br />
**codGrupoExt:** *O campo deve ser **varchar(25)**, contendo o codigo do grupo se o mesmo for **alfanumerico**.* <br />
**desGrupo:** *O campo deve ser **varchar(50)** contendo o nome do funcionario o campo e **obrigatorio**.* <br />
**ativo:** *O campo deve ser **inteiro** contendo 0 para inativo e 1 para ativo o campo e **obrigatorio**.* <br /><br />

**Se o código do grupo for inteiro o campo codGrupo e obrigatório, caso contrário, o campo codGrupoExt será o campo obrigatório.** <br />

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
codGrupo,
fracionado,
qtdPallet,
qtdCx,
controlaLote,
controlaValidade,
controlaFabricacao,
controlaNumSerie,
Shelf
FROM PRODUTO
```

**codProduto:** *Para que o codigo do WMS e do ERP sejam os mesmos o campo deve ser **inteiro**, caso seja **alfanumerico** o WMS irá gerar sua propria numeração e guardar o codigo do ERP em outro campo.* <br />
**descProd:** *O campo deve ser **varchar(50)** contendo a descrição do produto o campo e **obrigatorio**.* <br />
**situacao:** *O campo deve ser **inteiro** contendo 0 para inativo e 1 para ativo o campo e **obrigatorio**.* <br />
**refProd:** *O campo deve ser **varchar(10)** contendo a referencia do produto.* <br />
**revenda:** *O campo deve ser **inteiro** contendo 0 para inativo e 1 para ativo.* <br />
**vlrUltimaCompra:** *O campo deve ser **numerico(10,2)** contendo o preço de custo do produto.* <br />
**codFornecedor:** *O Campo deve conter o codigo do fornecedor do produto.* <br />
**codGrupo:** *O campo deve conter o codigo do grupo do produto o campo e **obrigatorio**.* <br />
**fracionado:** *O campo deve ser **inteiro**, contendo 1 se o produto permitir quantidade fracionadas e 0 para não.* <br />
**qtdPallet:** *O campo deve ser **numerico(10,2)**, contendo a quantidade que o palete suporta da menor unidade de estoque do produto.* <br />
**qtdCx:** *O campo deve ser **numerico(10,2)**, contendo a quantidade da embalagem master do produto.* <br />
**controlaLote:** *O campo deve ser **inteiro**, contendo 1 para controla e 0 para não controla.* <br />
**controlaValidade:** *O campo deve ser **inteiro**, contendo 1 para controla e 0 para não controla.* <br />
**controlaFabricacao:** *O campo deve ser **inteiro**, contendo 1 para controla e 0 para não controla.* <br />
**controlaNumSerie:** *O campo deve ser **inteiro**, contendo 1 para controla e 0 para não controla.* <br />
**Shelf:** *O campo deve ser **inteiro**, contendo a quantidade de dias de shelf do produto.* <br /><br /><br />

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

**Somente deve conter essa View em caso de possuir o processo de agrupamentos de notas de entrada** <br />

**codBonusCab:** *O campo deve ser **inteiro**, contendo o numero do bonus o campo e **obrigatorio**..* <br />
**codFilial:** *O campo deve conter a chave da filial o campo e **obrigatorio**..* <br />
**data:** *O campo deve ser **data** e deve conter a data de montagem do bonus o campo e **obrigatorio**..* <br />

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

**Somente colocar o campo codBonusCab se a importação for por bonus.** <br />

**codNotaFiscal:** *O campo deve ser **NULL**.* <br />
**codFilial:** *O campo deve conter a chave da filial, o campo e **obrigatorio**..* <br />
**codFilialIntegracao:** *O campo deve conter a chave da filial de origem (somente usar em casos de multi filial).* <br />
**codBonusCab:** *O campo deve ser **inteiro**, contendo o numero do bonus, o campo e **obrigatorio**.* <br />
**numNotaFiscal:** *O campo deve ser **inteiro**, contendo o numero da nota fiscal, o campo e **obrigatorio**.* <br />
**codFornecedor:** *O Campo deve conter o codigo do fornecedor da nota, o campo e **obrigatorio**.* <br />
**tipo:** *O campo deve ser **inteiro**, contendo o modelo do documento: Compra = 55, Devolução = 9, Transferencia = 8 e Produção = 11, o campo e **obrigatorio**.* <br />
**dtEmissao:** *O campo deve ser **data** e deve conter a data de entrada da nota, campo e **obrigatorio**.* <br />
**valTotProduto:** *O campo deve ser **numerico(18,2)** contendo a soma do valor total dos produtos, o campo e **obrigatorio**.* <br />
**valTotNotaFiscal:** *O campo deve ser **numerico(15,2)** contendo o valor total da nota fiscal de entrada, o campo e **obrigatorio**.* <br />

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

**Somente colocar o campo codBonusCab se a importação for por bonus.** <br />

**codNotaFiscalItem:** *O campo deve ser **NULL**.* <br />
**codNotaFiscal:** *O campo deve ser **inteiro**, contendo o numero da nota fiscal, o campo e **obrigatorio**.* <br />
**codFilial:** *O campo deve conter a chave da filial, o campo e **obrigatorio**.* <br />
**codFilialIntegracao:** *O campo deve conter a chave da filial de origem (somente usar em casos de multi filial).* <br />
**codBonusCab:** *O campo deve ser **inteiro**, contendo o numero do bonus, o campo e **obrigatorio**.* <br />
**codFornecedor:** *O Campo deve conter o codigo do fornecedor da nota, o campo e **obrigatorio**.* <br />
**tipo:** *O campo deve ser **inteiro**, contendo o modelo do documento: Compra = 55, Devolução = 9, Transferencia = 8 e Produção = 11, o campo e **obrigatorio**.* <br />
**codProduto:** *Chave estrangeira do codigo do produto, o campo e **obrigatorio**.* <br />
**unidade:** *O campo deve ser **varchar(3)** contendo a abreviação da embalagem.* <br />
**quantidade:** *O campo deve ser **numerico(12,4)** contendo a quantidade do produto, o campo e **obrigatorio**.* <br />
**valUnitario:** *O campo deve ser **numerico(16,2)** contendo o valor unitario do produto, o campo e **obrigatorio**.* <br />

> As Views de saída de produtos são todas as que compreendem processos aonde a mercadoria será separada para entrega, como por exemplo: Pedidos de venda, pedidos de
devolução de produtos a fornecedores, pedidos de demonstração.

> ### View de pedidos WMS_PEDIDOSCAB

``` 
CREATE VIEW WMS_PEDIDOSCAB AS 
SELECT 
codPedidoCab,
numDoc,
codFilial,
codFilialIntegracao,
codCliente,
codVendedor,
numDoc,
tipoPedido,
odemPedido,
dtGeracao,
qtdTotalItens,
valorTotal,
obs,
codRota
FROM PEDIDOSCAB
```

**codPedidoCab:** *O campo so deve ser preenchido se o valor for **inteiro**, caso o contrario o campo deve ser **NULL**.* <br />
**numDoc:** *O campo so deve ser preenchido se o valor do pedido for **NULL**, contendo o numero do pedido.* <br />
**codFilial:** *O campo deve conter a chave da filial, o campo e **obrigatorio**.* <br />
**codFilialIntegracao:** *O campo deve conter a chave da filial de origem (somente usar em casos de multi filial).* <br />
**codCliente:** *O Campo deve conter o codigo do cliente do pedido, o campo e **obrigatorio**.* <br />
**codVendedor:** *O Campo deve conter o codigo do funcionario da pedido, o campo e **obrigatorio**.* <br />
**tipoPedido:** *O campo deve ser **varchar(20)**, contendo a descrição do tipo do pedido EX: Venda, Balcão, Bonificação, etc, o campo e **obrigatorio**.* <br />
**odemPedido:** *O campo deve ser **inteiro**, contendo o nivel de prioridade do pedido, 0 – Urgente, 1 – Alta, 2 -Media, 3 – Baixa.* <br />
**dtGeracao:** *O campo deve ser **data** e deve conter a data de emissão do pedido.* <br />
**qtdTotalItens:** *O campo deve ser **inteiro** contendo a quantidade de itens no documento, o campo e **obrigatorio**.* <br />
**valTotProduto:** *O campo deve ser **numerico(16,2)** contendo o valor total do documento, o campo e **obrigatorio**.* <br />
**obs:** *O campo deve ser **nvarchar(1000)**, contendo a observação do pedido.* <br />
**codRota:** *O campo deve ser **inteiro**, contendo o codigo da rota do pedido.* <br /><br />

**Se o campo codigo do pedido for inteiro então o campo codPedidoCab e obrigatorio, se não o campo numDoc e obrigatorio.** <br />

> ### View de itens dos pedidos WMS_PEDIDOSITEM

``` 
CREATE VIEW WMS_PEDIDOSITEM AS 
SELECT 
codPedidoItem,
itemPedido,
codPedidoCab,
codFilial,
codProduto,
valorUnitario,
qtdProduto,
valorTotal,
lote
FROM PEDIDOSITEM
```

**codPedidoItem:** *O campo deve ser **inteiro**, conter o codigo sequencial dos itens.* <br />
**itemPedido:** *O campo deve ser **vatchar(10)**, conter o sequencial do item no pedido Ex: 0, 1, 2, 3, o campo e **obrigatorio**.* <br />
**codPedidoCab:** *O campo deve conter a chave estrangeira do pedido, o campo e **obrigatorio**.* <br />
**codFilial:** *O campo deve conter a chave da filial, o campo e **obrigatorio**.* <br />
**codProduto:** *Chave estrangeira do codigo do produto, o campo e **obrigatorio**.* <br />
**valorUnitario:** *O campo deve ser **numerico(12,2)** contendo o valor unitario do produto, o campo e **obrigatorio**.* <br />
**qtdProduto:** *O campo deve ser **numerico(12,4)** contendo a quantidade do produto, o campo e **obrigatorio**.* <br />
**valorTotal:** *O campo deve ser **numerico(12,2)** contendo o valor total do produto, o campo e **obrigatorio**.* <br />
**lote:** *O campo deve ser **varchar(15)**, conter a informação do lote que deve ser separado.* <br />

**O campo lote somente deve ser preenchido se o produto controlar lote e se somente puder ser separado o lote informado do produto.** <br />
