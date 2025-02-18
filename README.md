# Documentação da API 


Este endpoint permite emissão de notas fiscais (mod 55, 65) junto à SEFAZ (Secretaria da Fazenda), com a utilização de um payload com dados da NF, o certificado digital para autenticação e as configurações da empresa emissora.


## Endpoint
`"https://homol.ofm.com.br/api/v1/emitir/notas"`

## Requisição (EXEMPLO):

```json
{
    "certificado_base64": "MIIiGwIBAzCCIecGCSqGSIb3mY=",
    "senha_certificado": "Jc33204771",
    "config": {
        "tpAmb": 2,
        "razaosocial": "Razão-Cliente",
        "cnpj": "69559765000192",
        "siglaUF": "AL",
        "schemes": "PL_009_V4",
        "versao": "4.00",
        "cUF": 27,
        "cMun": 2704302,
        "tpEmis": 1,
        "modelo": "65",
        "CSC": "7ED6730D-C0C0-7484-6DCE-ACF38B8FC875",
        "CSCid": "000001"
    },
    "nfe_data": {
        "infNFe": {
            "versao": "4.00",
            "Id": "35160812345678000123450010000012345678901234",
            "pk_nItem": null
        },
        "ide": {
            "cUF": "27",
            "cNF": "00000015",
            "natOp": "Venda",
            "mod": "65",
            "serie": "1",
            "nNF": "35",
            "dhEmi": "2025-02-18T16:39:33-03:00",
            "tpNF": "1",
            "idDest": "1",
            "cMunFG": "2704302",
            "tpImp": "1",
            "tpEmis": "4",
            "cDV": "0",
            "tpAmb": "2",
            "finNFe": "1",
            "indFinal": "1",
            "indPres": "1",
            "procEmi": "0",
            "verProc": "1.0"
        },
        "emit": {
            "CNPJ": "98659675000098",
            "xNome": "Cliente",
            "xFant" : "Cliente",
            "enderEmit": {
                "xLgr": " RUA CIRILO DE CASTRO",
                "nro": "67",
                "xBairro": "LEVADA",
                "cMun": "2704302",
                "xMun": "Maceió",
                "UF": "AL",
                "CEP": "57017050",
                "cPais": "1058",
                "xPais": "Brasil",
                "fone": "8288128818"
            },
            "IE": "247519480",
            "CRT": "3"
        },
        "dest": {
            "CPF": "09987989909",
            "xNome": "Cliente Exemplo",
            "enderDest": {
                "xLgr": "Avenida Cliente",
                "nro": "200",
                "xBairro": "Bairro Cliente",
                "cMun": "3550308",
                "xMun": "São Paulo",
                "UF": "SP",
                "CEP": "01002000",
                "cPais": "1058",
                "xPais": "Brasil",
                "fone": "1190005000"
            },
            "indIEDest": "9"
        },
        "det": [
            {
                "prod": {
                    "cProd": "001",
                    "cEAN": "SEM GTIN",
                    "xProd": "NOTA FISCAL EMITIDA EM AMBIENTE DE HOMOLOGACAO - SEM VALOR FISCAL",
                    "NCM": "61091000",
                    "CFOP": "5102",
                    "uCom": "UN",
                    "qCom": "1.0000",
                    "vUnCom": "100.00",
                    "vProd": "100.00",
                    "cEANTrib": "SEM GTIN",
                    "uTrib": "UN",
                    "qTrib": "1.0000",
                    "vUnTrib": "100.00",
                    "indTot": "1"
                },
                "imposto": {
                    "ICMS": {
                        "orig": "0",
                        "CST": "00",
                        "modBC": "3",
                        "vBC": "100.00",
                        "pICMS": "18.00",
                        "vICMS": "18.00"
                    },
                    "PIS": {
                        "CST": "07",
                        "vBC": "100.00",
                        "pPIS": "1.65",
                        "vPIS": "1.65"
                    },
                    "COFINS": {
                        "CST": "07",
                        "vBC": "100.00",
                        "pCOFINS": "7.60",
                        "vCOFINS": "7.60"
                    }
                }
            }
        ],
        "ICMSTot": {
            "vBC": "100.00",
            "vICMS": "18.00",
            "vProd": "100.00",
            "vNF": "100.00"
        },
        "transp": {
            "modFrete": "9"
        },
        "pag": {
            "vTroco": "0.00"
        },
        "detPag": {
            "tPag": "01",
            "vPag": "100.00"
        },
        "infAdic": {
            "infCpl": "Venda realizada com sucesso."
        }
    }
}


```
- ## Detalhamento de Parametrização da Requisição


- ## Estrutura da Configuração

| **Campo**                   | **Descrição**                                                                                         | **Tipo de Dado**        |
|-------------------------|-------------------------------------------------------------------------------------------------|---------------------|
| `certificadoDigital`     | O certificado digital, em formato Base64, é necessário para autenticação e assinatura do envio para a SEFAZ. | String (Base64)     |
| `senhaCertificacao`      | Senha de certificação necessária para autenticação na SEFAZ.                                      | String (Base64)      |

- **Exemplo**:
    ```json
    {
      "certificado_base64": "PE5GZSB4bWxucz0iaHR0cDovL3d3dy5wb3J0",
      "senha_certificado": "Jc33204771"
    }
    ```


- ## Estrutura de Dados da Empresa Emitente

| **Campo**        | **Descrição**                                                                                          | **Indicador**                      | **Exemplo**                              | **Tipo de Dado**  |
|------------------|--------------------------------------------------------------------------------------------------------|--------------------------------------------|------------------------------------------|-------------------|
| `tpAmb`          | Tipo de ambiente.                                                                                      | 1: Produção, 2: Homologação                | 2                                        | Inteiro           |
| `razaosocial`    | Razão social da empresa emissora.                                                                       | -                                          | "JOSUE CORDEIRO DE FREITAS SILVA LTDA"   | String            |
| `cnpj`           | CNPJ da empresa emissora, composto apenas por números.                                                  | -                                          | "29659954000192"                         | String            |
| `siglaUF`        | Sigla do estado da empresa emissora.                                                                   | -                                          | "AL"                                     | String            |
| `schemes`        | Código do layout do XML da NFe, de acordo com a versão do layout utilizado.                            | -                                          | "PL_009_V4"                              | String            |
| `versao`         | Versão do XML da NFe, conforme o layout.                                                               | -                                          | "4.00"                                   | String            |
| `cUF`            | Código da Unidade Federativa (UF) do emitente, conforme tabela IBGE.                                   | -                                          | 27                                       | Inteiro           |
| `cMun`           | Código do município do emitente, conforme tabela IBGE.                                                 | -                                          | 2704302                                  | Inteiro           |
| `tpEmis`         | Tipo de emissão do documento fiscal.                                                                   | 1: Emissão normal, 2: Contingência, 3: Contingência EPEC | 1                                        | Inteiro           |
| `modelo`         | O modelo da nota fiscal. Para NFe, este valor deve ser "65".                                            | -                                          | "65"                                     | String            |
| `CSC`            | Código de Segurança do Contribuinte, fornecido pela SEFAZ, utilizado para autenticação no sistema.     | -                                          | "7ED6267D-C0C0-4467-8DCE-ACF48B8FC211"   | String            |
| `CSCid`          | ID do CSC (Código de Segurança do Contribuinte).                                                       | -                                          | "000001"                                 | String            |

#### Exemplo de `config`:
```json

 "config": {
        "tpAmb": 2,
        "razaosocial": "Razão-Cliente",
        "cnpj": "69559765000192",
        "siglaUF": "AL",
        "schemes": "PL_009_V4",
        "versao": "4.00",
        "cUF": 27,
        "cMun": 2704302,
        "tpEmis": 1,
        "modelo": "65",
        "CSC": "7ED6730D-C0C0-7484-6DCE-ACF38B8FC875",
        "CSCid": "000001"
  }

```
- ## Estrutura da Nota Fiscal :


| Campo                           | Descrição                                                                                                                                               | Tipo de Dado |
|---------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|
| `nfe_data.infNFe.versao`        | Versão do layout do XML da Nota Fiscal Eletrônica (NFe). Exemplo: `4.00`.                                                                               | String       |
| `nfe_data.infNFe.Id`            | Identificador único da NFe.                               | String |
| `nfe_data.infNFe.pk_nItem`      | Regra de validação do item de detalhe da NF-e, campo de controle do Schema XML, o contribuinte não deve se preocupar com o preenchimento deste campo.    | String      |
| `nfe_data.ide.cUF`              | Código da UF onde a nota fiscal foi emitida.                                                                                                             | String       |
| `nfe_data.ide.cNF`              | Código único gerado para cada nota fiscal.                                                                                                              | String       |
| `nfe_data.ide.natOp`            | Natureza da operação, indicando o tipo de transação (ex: "Venda", "Compra", etc.).                                                                     | String       |
| `nfe_data.ide.mod`              | 55 = NF-e emitida em substituição ao modelo 1 ou 1A; 65 = NFC-e, utilizada nas operações de venda no varejo (a critério da UF aceitar este modelo de documento)                                                                                  | String       |
| `nfe_data.ide.serie`            | Série da nota fiscal, geralmente um número sequencial.                                                                                                 | String       |
| `nfe_data.ide.nNF`              | Número da nota fiscal, utilizado para identificação única dentro da série.                                                                             | String       |
| `nfe_data.ide.dhEmi`            | Data e hora de emissão da nota fiscal. Formato: `YYYY-MM-DDTHH:MM:SS-03:00`.                                                                          | String       |
| `nfe_data.ide.tpNF`             | 0=Entrada; 1=Saída | String       |
| `nfe_data.ide.idDest`           | Identificação do destinatário, que pode ser 1 para destinatário dentro do estado ou 2 para destinatário fora do estado.                                | String       |
| `nfe_data.ide.cMunFG`           | Código do município onde a operação foi realizada.                                                                                                    | String       |
| `nfe_data.ide.tpImp`            | 0=Sem geração de DANFE; 1=DANFE normal, Retrato; 2=DANFE normal, Paisagem; 3=DANFE Simplificado; 4=DANFE NFC-e;5=DANFE NFC-e em mensagem eletrônica | String       |
| `nfe_data.ide.tpEmis`           | Tipo de emissão da nota fiscal: `1` para emissão normal, `2` para contingência, etc.                                                                  | String       |
| `nfe_data.ide.cDV`              | Dígito verificador da chave de acesso da NFe.                                                                                                           | String       |
| `nfe_data.ide.tpAmb`            | Tipo de ambiente: `1` para produção e `2` para homologação.                                                                                           | String       |
| `nfe_data.ide.finNFe`           | Finalidade da nota fiscal: `1` para venda, `2` para devolução, etc.                                                                                  | String       |
| `nfe_data.ide.indFinal`         | 0 = Normal ; 1 = Consumidor Final.                                                                  | String       |
| `nfe_data.ide.indPres`          | 0=Não se aplica (por exemplo, Nota Fiscal complementar ou de ajuste); 1=Operação presencial ; 2=Operação não presencial, pela Internet;              | String       |
| `nfe_data.ide.procEmi`          | Código do processo de emissão da NFe.                                                                                                                  | String       |
| `nfe_data.ide.verProc`          | Versão do processo de emissão da NFe.                                                                                                                  | String       |
| `nfe_data.emit.CNPJ`            | CNPJ do emitente da nota fiscal.                                                                                                                        | String       |
| `nfe_data.emit.xNome`           | Razão social ou nome completo do emitente.                                                                                                             | String       |
| `nfe_data.emit.xFant`           | Nome fantasia do emitente.                                                                                                                             | String       |
| `nfe_data.emit.enderecoEmit`    | Endereço completo do emitente, incluindo logradouro, número, bairro, cidade, estado, CEP, país e telefone.                                            | Object       |
| `nfe_data.emit.IE`              | Inscrição estadual do emitente.                                                                                                                        | String       |
| `nfe_data.emit.CRT`             | Código do regime de tributação do emitente.                                                                                                           | String       |
| `nfe_data.dest.CPF`             | CPF do destinatário da nota fiscal.                                                                                                                   | String       |
| `nfe_data.dest.xNome`           | Nome do destinatário da nota fiscal.                                                                                                                  | String       |
| `nfe_data.dest.enderecoDest`    | Endereço completo do destinatário, incluindo logradouro, número, bairro, cidade, estado, CEP, país e telefone.                                       | Object       |
| `nfe_data.dest.indIEDest`       | Indicação de inscrição estadual do destinatário, indicando se o destinatário tem ou não inscrição estadual.                                           | String       |
| `nfe_data.det.prod`             | Detalhes do produto ou serviço na nota fiscal, incluindo código do produto (`cProd`), descrição (`xProd`), unidade de medida, quantidade, valor, etc.  | Object       |
| `nfe_data.det.imposto`          | Detalhes dos impostos aplicados ao produto, como ICMS, PIS e COFINS.                                                                                 | Object       |
| `nfe_data.ICMSTot`              | Totais de impostos da nota fiscal, incluindo base de cálculo e valor total de ICMS, PIS, COFINS e valor total da nota fiscal.                           | Object       |
| `nfe_data.transp.modFrete`      | Modalidade de frete, indicando a responsabilidade pelo pagamento do frete (ex: 1 para emitente, 9 para por conta do destinatário).                     | String       |
| `nfe_data.pag.vTroco`           | Valor do troco a ser devolvido ao comprador, caso aplicável.                                                                                          | String       |
| `nfe_data.detPag.tPag`          | Tipo de pagamento realizado (ex: `01` para pagamento à vista).                                                                                       | String       |
| `nfe_data.detPag.vPag`          | Valor pago na transação.                                                                                                                              | String       |
| `nfe_data.infAdic.infCpl`       | Informações complementares que podem ser incluídas na nota fiscal, como observações gerais (ex: "Venda realizada com sucesso.").                      | String       |

#### Exemplo de `nfe_data`:

```json
"nfe_data": {
        "infNFe": {
            "versao": "4.00",
            "Id": "35160812345678000123450010000012345678901234",
            "pk_nItem": null
        },
        "ide": {
            "cUF": "27",
            "cNF": "00000015",
            "natOp": "Venda",
            "mod": "65",
            "serie": "1",
            "nNF": "35",
            "dhEmi": "2025-02-18T16:39:33-03:00",
            "tpNF": "1",
            "idDest": "1",
            "cMunFG": "2704302",
            "tpImp": "1",
            "tpEmis": "4",
            "cDV": "0",
            "tpAmb": "2",
            "finNFe": "1",
            "indFinal": "1",
            "indPres": "1",
            "procEmi": "0",
            "verProc": "1.0"
        },
        "emit": {
            "CNPJ": "98659675000098",
            "xNome": "Cliente",
            "xFant" : "Cliente",
            "enderEmit": {
                "xLgr": " RUA CIRILO DE CASTRO",
                "nro": "67",
                "xBairro": "LEVADA",
                "cMun": "2704302",
                "xMun": "Maceió",
                "UF": "AL",
                "CEP": "57017050",
                "cPais": "1058",
                "xPais": "Brasil",
                "fone": "8288128818"
            },
            "IE": "247519480",
            "CRT": "3"
        },
        "dest": {
            "CPF": "09987989909",
            "xNome": "Cliente Exemplo",
            "enderDest": {
                "xLgr": "Avenida Cliente",
                "nro": "200",
                "xBairro": "Bairro Cliente",
                "cMun": "3550308",
                "xMun": "São Paulo",
                "UF": "SP",
                "CEP": "01002000",
                "cPais": "1058",
                "xPais": "Brasil",
                "fone": "1190005000"
            },
            "indIEDest": "9"
        },
        "det": [
            {
                "prod": {
                    "cProd": "001",
                    "cEAN": "SEM GTIN",
                    "xProd": "NOTA FISCAL EMITIDA EM AMBIENTE DE HOMOLOGACAO - SEM VALOR FISCAL",
                    "NCM": "61091000",
                    "CFOP": "5102",
                    "uCom": "UN",
                    "qCom": "1.0000",
                    "vUnCom": "100.00",
                    "vProd": "100.00",
                    "cEANTrib": "SEM GTIN",
                    "uTrib": "UN",
                    "qTrib": "1.0000",
                    "vUnTrib": "100.00",
                    "indTot": "1"
                },
                "imposto": {
                    "ICMS": {
                        "orig": "0",
                        "CST": "00",
                        "modBC": "3",
                        "vBC": "100.00",
                        "pICMS": "18.00",
                        "vICMS": "18.00"
                    },
                    "PIS": {
                        "CST": "07",
                        "vBC": "100.00",
                        "pPIS": "1.65",
                        "vPIS": "1.65"
                    },
                    "COFINS": {
                        "CST": "07",
                        "vBC": "100.00",
                        "pCOFINS": "7.60",
                        "vCOFINS": "7.60"
                    }
                }
            }
        ],
        "ICMSTot": {
            "vBC": "100.00",
            "vICMS": "18.00",
            "vProd": "100.00",
            "vNF": "100.00"
        },
        "transp": {
            "modFrete": "9"
        },
        "pag": {
            "vTroco": "0.00"
        },
        "detPag": {
            "tPag": "01",
            "vPag": "100.00"
        },
        "infAdic": {
            "infCpl": "Venda realizada com sucesso."
        }
    }
```

- ## Respostas da API


| Campo         | Tipo                | Descrição                                                                                                                                                     | Exemplo                                                                 |
|---------------|---------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| `sucesso`     | Booleano (true/false) | Indica se a operação foi bem-sucedida ou não. `true`: A operação foi bem-sucedida. `false`: A operação falhou.                                                | `true` ou `false`                                                      |
| `mensagem`    | String              | Contém uma mensagem explicativa sobre o status da nota fiscal.                                                                                                 | `Autorizado o uso da NF-e`, `Rejeição: NFC-e com Data-Hora atrasada`  |
| `status`      | String              | Refere-se ao status da nota fiscal. Possíveis valores: `Emitida` ou `Rejeitada`.                                                                              | `Emitida` ou `Rejeitada`                                               |
| `cStat`       | String (numérico)   | Código de status da NF-e. Indica se a nota fiscal foi autorizada ou rejeitada. Alguns exemplos de códigos: `100`, `704`.                                      | `100`, `704`                                                           |
| `xml_enviado` | String              | Contém o XML da nota fiscal enviado à SEFAZ. O XML é codificado em base64 para transporte seguro.                                                             | `PD94bWwgdmVyc2lvbj0iMS4wIj8+...` (codificado em base64)             |
| `chave_nfe`   | String              | A chave única da Nota Fiscal Eletrônica (NF-e). Composta por 44 caracteres alfanuméricos, identifica a nota fiscal.                                            | `27250229659954000192650010000000551000000158`                       |
| `protocolo`   | String ou null      | O número do protocolo de autorização gerado pela SEFAZ quando a NF-e é autorizada. Se a nota for rejeitada, o campo pode ser `null`.                           | `327250000001198` ou `null`                                            |

  

#### Exemplo de Retorno com Sucesso na Requisição ✅ :
```json
{
    "sucesso": true,
    "mensagem": "Autorizado o uso da NF-e",
    "status": "Emitida",
    "cStat": "100",
    "xml_enviado": "PE5GZSB4bWxucz0iaHR0cDovL3d3dy5wb3J0",
    "chave_nfe": "24560229659954000192650010986000101000000156",
    "protocolo": "327250000001198"
}
```
#### Exemplo de Retorno com falha na Requisição ⛔ :

```json
{
    "sucesso": false,
    "mensagem": "Rejeicao: NFC-e com Data-Hora de emissao atrasada",
    "status": "Rejeitada",
    "cStat": "704",
    "xml_enviado": "PE5GZSB4bWxucz0iaHR0cDovL3d3dy5wb3J0" ,
    "chave_nfe": "24560229659954000192650010986000101000000156",
    "protocolo": "327250000001198"
}

```



