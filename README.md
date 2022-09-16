# WMSExpert
**Documentação de integração WMSExpert**

> As Views de cadastro tem como função principal integrar as duas bases de dados, permitindo que os cadastros sejam feitos apenas no Erp e que possam ser importados integralmente para o WMS Expert, sem retrabalho.

> ### View de cidades WMS_CIDADE

``` CREATE VIEW WMS_CIDADE AS 
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

``` CREATE VIEW WMS_CLIENTE AS 
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


