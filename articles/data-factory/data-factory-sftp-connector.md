---
title: aaaMove dados do servidor SFTP usando o Azure Data Factory | Microsoft Docs
description: Saiba mais sobre como toomove dados de um local ou um servidor SFTP de nuvem usando o Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jingwang
ms.openlocfilehash: b976289e2c1b1899634bb5565b375499077fa554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-sftp-server-using-azure-data-factory"></a>Mover dados de um servidor SFTP usando o Azure Data Factory
Este artigo descreve como toouse hello atividade de cópia em dados do Azure Data Factory toomove de um tooa de servidor SFTP no local/em nuvem suporte para armazenamento de dados do coletor. Este artigo aproveita Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo que apresenta uma visão geral de movimentação de dados com Copiar atividade e hello lista de repositórios de dados têm suportada como/coletores de fontes.

Fábrica de dados atualmente suporta apenas mover armazena dados de um servidor de SFTP tooother dados, mas não para mover dados de outros dados armazena o servidor SFTP tooan. Ele dá suporte a servidores SFTP tanto locais quanto na nuvem.

> [!NOTE]
> Atividade de cópia não exclui o arquivo de origem Olá depois que ele destino toohello foram copiados com êxito. Se precisar de arquivo de origem toodelete Olá após uma cópia bem-sucedida, criar um arquivo de saudação toodelete atividade personalizada e usar a atividade Olá no pipeline de saudação. 

## <a name="supported-scenarios-and-authentication-types"></a>Cenários com suporte e tipos de autenticação
Você pode usar dados SFTP conector toocopy de **ambos os servidores SFTP e SFTP local na nuvem**. **Básico** e **parâmetros SshPublicKey** tipos de autenticação com suporte ao conectar-se o servidor SFTP toohello.

Ao copiar dados de um servidor SFTP local, você precisa instalar um Gateway de gerenciamento de dados no ambiente do local de saudação/Azure VM. Consulte [Data Management Gateway](data-factory-data-management-gateway.md) para obter detalhes sobre o gateway de saudação. Consulte [mover dados entre locais de local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo para instruções passo a passo de configuração de gateway hello e usá-lo.

## <a name="getting-started"></a>Introdução
Você pode criar um pipeline com uma atividade de cópia que mova dados de uma origem SFTP usando diferentes ferramentas/APIs.

- toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**. Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação.

- Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**. Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia. Para exemplos de JSON toocopy dados do servidor SFTP tooAzure armazenamento de Blob, consulte [exemplo JSON: copiar dados de blob de tooAzure servidor SFTP](#json-example-copy-data-from-sftp-server-to-azure-blob) deste artigo.

## <a name="linked-service-properties"></a>Propriedades do serviço vinculado
Olá, a tabela a seguir fornece uma descrição para JSON elementos específicos tooFTP vinculado serviço.

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- | --- |
| type | propriedade do tipo Hello deve ser definida muito`Sftp`. |Sim |
| host | Nome ou endereço IP do servidor SFTP hello. |Sim |
| porta |Porta na qual Olá SFTP server está escutando. valor padrão de saudação é: 21 |Não |
| authenticationType |Especifique o tipo de autenticação. Valores permitidos: **Básica**, **SshPublicKey**. <br><br> Consulte também[usando a autenticação básica](#using-basic-authentication) e [usando SSH autenticação de chave pública](#using-ssh-public-key-authentication) seções em mais propriedades e exemplos JSON, respectivamente. |Sim |
| skipHostKeyValidation | Especifique se tooskip validação de chave do host. | Não. Olá valor padrão: false |
| hostKeyFingerprint | Especifique a impressão digital de saudação da chave de host hello. | Sim se hello `skipHostKeyValidation` é definido toofalse.  |
| gatewayName |Nome da saudação Data Management Gateway tooconnect tooan local do servidor SFTP. | Sim se estiver copiando dados de um servidor SFTP local. |
| encryptedCredential | Servidor SFTP saudação do tooaccess credencial criptografada. Gerado automaticamente quando você especificar a autenticação básica (nome de usuário + senha) ou parâmetros SshPublicKey (nome de usuário + caminho da chave privado ou conteúdo) no diálogo de pop-up de ClickOnce de assistente ou saudação de cópia. | Não. Aplique somente quando estiver copiando dados de um servidor SFTP local. |

### <a name="using-basic-authentication"></a>Usando a autenticação Básica

Definir toouse a autenticação básica, `authenticationType` como `Basic`e especifique Olá seguintes propriedades além Olá conector SFTP genérico aqueles introduzidos na última seção do hello:

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- | --- |
| Nome de Usuário | Usuário que possui o servidor do acesso toohello SFTP. |Sim |
| Senha | Senha do usuário da saudação (nome de usuário). | Sim |

#### <a name="example-basic-authentication"></a>Exemplo: autenticação Básica
```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a>Exemplo: autenticação Básica com credencial criptografada

```JSON
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
      }
}
```

### <a name="using-ssh-public-key-authentication"></a>Usando a autenticação de chave pública SSH

Definir toouse SSH autenticação de chave pública, `authenticationType` como `SshPublicKey`e especifique Olá seguintes propriedades além Olá conector SFTP genérico aqueles introduzidos na última seção do hello:

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- | --- |
| Nome de Usuário |Usuário que tem acesso toohello SFTP servidor |Sim |
| privateKeyPath | Especifique o caminho absoluto toohello arquivo de chave privada pode acessar o gateway. | Especifique a saudação `privateKeyPath` ou `privateKeyContent`. <br><br> Aplique somente quando estiver copiando dados de um servidor SFTP local. |
| privateKeyContent | Uma cadeia de caracteres serializada de conteúdo da chave privada hello. Olá Assistente para cópia pode ler o arquivo de chave privada hello e extrair o conteúdo da chave privada Olá automaticamente. Se você estiver usando qualquer outra ferramenta/SDK, use a propriedade de privateKeyPath de saudação em vez disso. | Especifique a saudação `privateKeyPath` ou `privateKeyContent`. |
| Senha | Especifique Olá senha/frase toodecrypt Olá privada chave de acesso de se o arquivo de chave Olá estiver protegido por uma frase secreta. | Sim, se o arquivo de chave privada Olá é protegido por uma frase secreta. |

> [!NOTE]
> O conector SFTP somente suporta a chave OpenSSH. Verifique se que o arquivo de chave está no formato adequado hello. Você pode usar a ferramenta Putty tooconvert *.ppk tooOpenSSH formato.

#### <a name="example-sshpublickey-authentication-using-private-key-filepath"></a>Exemplo: autenticação de SshPublicKey usando o filePath da chave privada

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a>Exemplo: autenticação de SshPublicKey usando o conteúdo da chave privada

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

## <a name="dataset-properties"></a>Propriedades do conjunto de dados
Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo. As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados.

Olá **typeProperties** seção é diferente para cada tipo de conjunto de dados. Ele fornece informações de tipo de conjunto de dados toohello específico. Olá typeProperties seção um conjunto de dados do tipo **FileShare** conjunto de dados tiver Olá propriedades a seguir:

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| folderPath |Subpasta toohello mais recente para o caminho. Use o caractere de escape ' \ ' para caracteres especiais na cadeia de caracteres de saudação. Confira [Definições de conjunto de dados e serviço vinculado de exemplo](#sample-linked-service-and-dataset-definitions) para obter exemplos.<br/><br/>Você pode combinar essa propriedade com **partitionBy** toohave caminhos de pastas com base na fatia datas / horas de início/término. |Sim |
| fileName |Especifique o nome de saudação do arquivo de saudação em Olá **folderPath** se você quiser Olá tabela toorefer tooa arquivo específico na pasta hello. Se você não especificar qualquer valor para essa propriedade, a tabela de saudação aponta tooall arquivos na pasta hello.<br/><br/>Quando o nome de arquivo não for especificado para um conjunto de dados de saída, o nome de saudação do arquivo hello gerado aparecerá em Olá esse formato a seguir: <br/><br/>Data.<Guid>.txt (por exemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Não |
| fileFilter |Especifique um filtro toobe usado tooselect um subconjunto de arquivos no hello folderPath em vez de todos os arquivos.<br/><br/>Os valores permitidos são: `*` (vários caracteres) e `?` (um único caractere).<br/><br/>Exemplo 1: `"fileFilter": "*.log"`<br/>Exemplo 2: `"fileFilter": 2014-1-?.txt"`<br/><br/> fileFilter é aplicável a um conjunto de dados FileShare de entrada. Essa propriedade não tem suporte com HDFS. |Não |
| partitionedBy |partitionedBy pode ser usado toospecify um folderPath dinâmico, nome de arquivo para dados de série temporal. Por exemplo, folderPath parametrizado para cada hora dos dados. |Não |
| formato | Olá, tipos de formato a seguir têm suporte: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Saudação de conjunto **tipo** propriedade em formato tooone desses valores. Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Se você quiser muito**copiar arquivos como-é** entre repositórios baseada em arquivo (cópia binário), ignore a seção de formato de saudação em ambas as definições de conjunto de dados de entrada e saída. |Não |
| compactação | Especifica tipo de saudação e nível de compactação de dados de saudação. Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**. Os níveis com suporte são **Ideal** e **O mais rápido**. Para saber mais, confira [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support) (Formatos de arquivo e de compactação no Azure Data Factory). |Não |
| useBinaryTransfer |Especifique se deve usar o modo de transferência Binário. True para o modo binário e ASCII false. Valor padrão: True. Essa propriedade só pode ser usada quando o tipo de serviço vinculado associado for do tipo: FtpServer. |Não |

> [!NOTE]
> filename e fileFilter não podem ser usados simultaneamente.

### <a name="using-partionedby-property"></a>Usando a propriedade partionedBy
Como mencionado na seção anterior hello, você pode especificar um folderPath dinâmico, o nome de arquivo para dados de série temporal com partitionedBy. Você pode fazer isso com macros de fábrica de dados hello e variável de sistema Olá SliceStart, SliceEnd que indicam Olá período lógico para uma fatia de dados fornecido.

toolearn sobre conjuntos de dados de série de tempo, planejamento e fatias, consulte [criando conjuntos de dados](data-factory-create-datasets.md), [de agendamento e execução](data-factory-scheduling-and-execution.md), e [criar Pipelines](data-factory-create-pipelines.md) artigos.

#### <a name="sample-1"></a>Exemplo 1:

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
Neste exemplo {Slice} é substituído pelo valor de saudação da variável de sistema SliceStart fábrica de dados no formato de saudação (AAAAMMDDHH) especificado. Olá SliceStart refere-se toostart tempo da fração de saudação. Olá folderPath é diferente para cada fatia. Por exemplo: wikidatagateway/wikisampledataout/2014100103 ou wikidatagateway/wikisampledataout/2014100104.

#### <a name="sample-2"></a>Exemplo 2:

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
Neste exemplo, ano, mês, dia e hora do SliceStart são extraídos em variáveis separadas que são usadas pelas propriedades folderPath e fileName.

## <a name="copy-activity-properties"></a>Propriedades da atividade de cópia
Para obter uma lista completa das seções e propriedades disponíveis para a definição de atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo. As propriedades, como nome, descrição, tabelas de entrada e saída, e políticas, estão disponíveis para todos os tipos de atividade.

Por outro lado, Olá as propriedades disponíveis na seção typeProperties hello atividade Olá variam com cada tipo de atividade. Para a atividade de cópia, propriedades de tipo hello variam dependendo Olá tipos de fontes e coletores.

[!INCLUDE [data-factory-file-system-source](../../includes/data-factory-file-system-source.md)]

## <a name="supported-file-and-compression-formats"></a>Formatos de arquivo e de compactação com suporte
Consulte o artigo [Formatos de arquivo e de compactação no Azure Data Factory](data-factory-supported-file-and-compression-formats.md) para obter detalhes.

## <a name="json-example-copy-data-from-sftp-server-tooazure-blob"></a>Exemplo JSON: Copiar dados de blob de tooAzure servidor SFTP
Olá, exemplo a seguir fornece definições de JSON de exemplo que você pode usar toocreate um pipeline usando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Eles mostram como fonte de dados toocopy de SFTP tooAzure armazenamento de Blob. No entanto, os dados podem ser copiados **diretamente** de qualquer uma das fontes tooany de Coletores Olá mencionado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.

> [!IMPORTANT]
> Este exemplo fornece trechos de JSON. Ele não inclui instruções passo a passo para criar a fábrica de dados hello. Confira o artigo [Mover dados entre fontes locais e a nuvem](data-factory-move-data-between-onprem-and-cloud.md) para obter instruções passo a passo.

exemplo Hello tem Olá entidades da fábrica de dados a seguir:

* Um serviço vinculado do tipo [sftp](#linked-service-properties).
* Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [FileShare](#dataset-properties).
* Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* Um [pipeline](data-factory-create-pipelines.md) com a Atividade de Cópia que usa [FileSystemSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

exemplo Hello copia dados de um servidor SFTP tooan BLOBs do Azure a cada hora. propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.

**Serviço vinculado SFTP**

Este exemplo usa a autenticação básica Olá com nome de usuário e senha em texto sem formatação. Você também pode usar uma saudação maneiras a seguir:

* Autenticação básica com credenciais criptografadas
* Autenticação de chave pública SSH

Confira a seção [Serviço FTP vinculado](#linked-service-properties) para ver os diferentes tipos de autenticação que você pode usar.

```JSON

{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "myuser",
            "password": "mypassword",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```
**Serviço vinculado de armazenamento do Azure**

```JSON
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
**Conjunto de dados de entrada do SFTP**

Este conjunto de dados refere-se a pasta SFTP toohello `mysharedfolder` e o arquivo `test.csv`. pipeline de saudação copia o destino de toohello arquivo hello.

Definindo "externo": "verdadeiro" informa serviço da fábrica de dados Olá Olá conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados hello.

```JSON
{
  "name": "SFTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "SftpLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**Conjunto de dados de saída de Blob do Azure**

Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1). caminho da pasta Olá blob Olá é avaliado dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada. caminho da pasta Olá usa partes de ano, mês, dia e horário da hora de início da saudação.

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
            "partitionedBy": [
                {
                    "name": "Year",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "yyyy"
                    }
                },
                {
                    "name": "Month",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "MM"
                    }
                },
                {
                    "name": "Day",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "dd"
                    }
                },
                {
                    "name": "Hour",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "HH"
                    }
                }
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Pipeline com Atividade de cópia**

Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora. Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**FileSystemSource** e **coletor** tipo está definido muito**BlobSink**.

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2017-02-20T18:00:00Z",
        "end": "2017-02-20T19:00:00Z"
    }
}
```

## <a name="performance-and-tuning"></a>Desempenho e Ajuste
Consulte [guia de ajuste e desempenho de atividade de cópia](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias formas-lo.

## <a name="next-steps"></a>Próximas etapas
Consulte Olá artigos a seguir:

* [Tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter instruções passo a passo para criação de um pipeline com uma Atividade de cópia.
