---
title: aaaMove dados de um servidor FTP por meio do Azure Data Factory | Microsoft Docs
description: Saiba mais sobre como toomove dados de um servidor FTP usando o Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: eea3bab0-a6e4-4045-ad44-9ce06229c718
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jingwang
ms.openlocfilehash: c707e29532b2a8a870603948cb6150ab857bd6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-ftp-server-by-using-azure-data-factory"></a>Mover dados de um servidor FTP usando o Azure Data Factory
Este artigo explica como toouse hello atividade de cópia de dados do Azure Data Factory toomove de um servidor FTP. Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação.

Você pode copiar dados de um repositório de dados de coletor do FTP servidor tooany com suporte. Para obter uma lista de dados de repositórios de suporte como coletores pela atividade de cópia Olá, consulte Olá [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela. Fábrica de dados atualmente suporta apenas armazena de movimentação de dados de uma data de tooother do servidor FTP, mas não movendo os dados de outros dados armazena server tooan FTP. Ele dá suporte a servidores FTP locais e em nuvem.

> [!NOTE]
> atividade de cópia de saudação não exclui o arquivo de origem Olá depois que ele destino toohello foram copiados com êxito. Se você precisar de arquivo de origem toodelete Olá após uma cópia com êxito, criar um arquivo de saudação toodelete atividade personalizada e use atividade Olá no pipeline de saudação. 

## <a name="enable-connectivity"></a>Habilitar a conectividade
Se você estiver movendo dados de um **local** armazenamento de dados de nuvem para tooa de servidor FTP (por exemplo, tooAzure armazenamento de Blob), instalar e usar o Gateway de gerenciamento de dados. Olá Gateway de gerenciamento de dados é um agente de cliente que está instalado em seu computador local e permite que o recurso de local de tooan de tooconnect de serviços de nuvem. Para ver os detalhes, consulte [Gateway de Gerenciamento de Dados](data-factory-data-management-gateway.md). Para obter instruções passo a passo de configuração de gateway hello e usá-lo, consulte [mover dados entre locais de local e nuvem](data-factory-move-data-between-onprem-and-cloud.md). Usar o servidor FTP de tooan tooconnect do gateway Olá, mesmo se o servidor de saudação estiver em uma infraestrutura do Azure como uma máquina virtual (VM) de serviço (IaaS).

É possível tooinstall Olá gateway Olá mesmo no local máquina ou VM IaaS como Olá servidor FTP. No entanto, recomendamos que você instale o gateway de saudação em um computador separado ou a contenção de recursos do IaaS VM tooavoid e para melhorar o desempenho. Quando você instalar o gateway de saudação em um computador separado, máquina Olá deve ser tooaccess capaz de servidor FTP de saudação.

## <a name="get-started"></a>Introdução
Você pode criar um pipeline com uma atividade de cópia que move dados de uma origem FTP usando diferentes ferramentas ou APIs.

toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de fábrica de dados**. Veja o [Tutorial: Criar um pipeline usando o Assistente de Cópia](data-factory-copy-data-wizard-tutorial.md) para obter um passo a passo rápido.

Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **PowerShell**, **modelo do Azure Resource Manager**, **API .NET**, e **API REST**. Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.

Se você usar ferramentas de saudação ou APIs, execute Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:

1. Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.
2. Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello.
3. Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.

Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você. Quando você usar ferramentas ou APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação. Para obter um exemplo com definições de JSON para entidades de fábrica de dados que são usados toocopy dados de um repositório de dados FTP, consulte Olá [exemplo JSON: copiar dados de blob de tooAzure do servidor FTP](#json-example-copy-data-from-ftp-server-to-azure-blob) deste artigo.

> [!NOTE]
> Para obter detalhes sobre toouse de formatos de arquivo e compactação com suporte, consulte [compactação formatos de arquivo e no Azure Data Factory](data-factory-supported-file-and-compression-formats.md).

Olá seções a seguir fornece detalhes sobre as propriedades JSON que são usadas toodefine Data Factory entidades específica tooFTP.

## <a name="linked-service-properties"></a>Propriedades do serviço vinculado
Olá, a tabela a seguir descreve o serviço FTP vinculada do JSON elementos tooan específico.

| Propriedade | Descrição | Obrigatório | Padrão |
| --- | --- | --- | --- |
| type |Defina este tooFtpServer. |Sim |&nbsp; |
| host |Especifique o nome de saudação ou endereço IP do servidor FTP hello. |Sim |&nbsp; |
| authenticationType |Especifique o tipo de autenticação de saudação. |Sim |Básica, Anônima |
| Nome de Usuário |Especifica usuário Olá que tem o servidor FTP toohello acesso. |Não |&nbsp; |
| Senha |Especifique a senha de saudação para usuário hello (nome de usuário). |Não |&nbsp; |
| encryptedCredential |Especifica servidor de saudação FTP Olá criptografado credencial tooaccess. |Não |&nbsp; |
| gatewayName |Especifique o nome de saudação do gateway Olá no servidor do Gateway de gerenciamento de dados tooconnect tooan local FTP. |Não |&nbsp; |
| porta |Especifique a porta de saudação na qual Olá FTP server está escutando. |Não |21 |
| enableSsl |Especifique se toouse FTP por um canal SSL/TLS. |Não |verdadeiro |
| enableServerCertificateValidation |Especifique se o servidor de tooenable SSL a validação de certificado quando você estiver usando o FTP por canal SSL/TLS. |Não |verdadeiro |

### <a name="use-anonymous-authentication"></a>Usar autenticação anônima

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {        
            "authenticationType": "Anonymous",
              "host": "myftpserver.com"
        }
    }
}
```

### <a name="use-username-and-password-in-plain-text-for-basic-authentication"></a>Usar nome de usuário e senha em texto sem formatação para autenticação básica

```JSON
{
    "name": "FTPLinkedService",
      "properties": {
    "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
      }
}
```

### <a name="use-port-enablessl-enableservercertificatevalidation"></a>Usar a porta, enableSsl, enableServerCertificateValidation

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

### <a name="use-encryptedcredential-for-authentication-and-gateway"></a>Usar encryptedCredential para autenticação e gateway

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "mygateway"
        }
      }
}
```

## <a name="dataset-properties"></a>Propriedades do conjunto de dados
Para obter uma lista completa das seções e propriedades disponíveis para definir os conjuntos de dados, confira [Criando conjuntos de dados](data-factory-create-datasets.md). As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados.

Olá **typeProperties** seção é diferente para cada tipo de conjunto de dados. Ele fornece informações de tipo de conjunto de dados toohello específico. Olá **typeProperties** seção um conjunto de dados do tipo **FileShare** tem Olá propriedades a seguir:

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| folderPath |Pasta de toohello subcaminho. Use o caractere de escape ' \ ' para caracteres especiais na cadeia de caracteres de saudação. Confira [Definições de conjunto de dados e serviço vinculado de exemplo](#sample-linked-service-and-dataset-definitions) para obter exemplos.<br/><br/>Você pode combinar essa propriedade com **partitionBy** toohave caminhos de pastas com base na fatia início e término do data. |Sim |
| fileName |Especifique o nome de saudação do arquivo de saudação em Olá **folderPath** se você quiser Olá tabela toorefer tooa arquivo específico na pasta hello. Se você não especificar qualquer valor para essa propriedade, a tabela de saudação aponta tooall arquivos na pasta hello.<br/><br/>Quando **fileName** não for especificado para um conjunto de dados de saída, nome de saudação do arquivo hello gerado está em Olá formato a seguir: <br/><br/>Data.<Guid>.txt (exemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |Não |
| fileFilter |Especifique um tooselect toobe usado do filtro um subconjunto de arquivos no hello **folderPath**, em vez de todos os arquivos.<br/><br/>Os valores permitidos são: `*` (vários caracteres) e `?` (um único caractere).<br/><br/>Exemplo 1: `"fileFilter": "*.log"`<br/>Exemplo 2: `"fileFilter": 2014-1-?.txt"`<br/><br/> **fileFilter** é aplicável a um conjunto de dados FileShare de entrada. Essa propriedade não tem suporte no HDFS (Sistema de Arquivos Distribuído Hadoop). |Não |
| partitionedBy |Usado toospecify um dinâmico **folderPath** e **fileName** para dados de série temporal. Por exemplo, você pode especificar um **folderPath** que é parametrizada para cada hora dos dados. |Não |
| formato | Olá, tipos de formato a seguir têm suporte: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Saudação de conjunto **tipo** propriedade em formato tooone desses valores. Para obter mais informações, consulte Olá [formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Parquet formato ](data-factory-supported-file-and-compression-formats.md#parquet-format) seções. <br><br> Se você quiser toocopy arquivos como eles estão entre repositórios baseada em arquivo (cópia binário), ignore a seção de formato de saudação em ambas as definições de conjunto de dados de entrada e saída. |Não |
| compactação | Especifica tipo de saudação e nível de compactação de dados de saudação. Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**; e os níveis com suporte são: **Ideal** e **Mais rápido**. Para saber mais, confira [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support) (Formatos de arquivo e de compactação no Azure Data Factory). |Não |
| useBinaryTransfer |Especifique se binário de saudação toouse modo de transferência. os valores Hello são true para o modo binário (esse é o valor de padrão de saudação) e false para ASCII. Esta propriedade só pode ser usada quando hello tipo de serviço vinculado associado é do tipo: FtpServer. |Não |

> [!NOTE]
> **fileName** e **fileFilter** não podem ser usados simultaneamente.

### <a name="use-hello-partionedby-property"></a>Usar a propriedade partionedBy Olá
Como mencionado na seção anterior hello, você pode especificar um dinâmico **folderPath** e **fileName** para dados de série temporal com hello **partitionedBy** propriedade.

toolearn sobre conjuntos de dados de série de tempo, planejamento e fatias, consulte [criando conjuntos de dados](data-factory-create-datasets.md), [de agendamento e execução](data-factory-scheduling-and-execution.md), e [criar pipelines](data-factory-create-pipelines.md).

#### <a name="sample-1"></a>Exemplo 1

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
Neste exemplo, {Slice} é substituído pelo valor de saudação de variável SliceStart de fábrica de dados do sistema, Olá formato (AAAAMMDDHH) especificado. Olá SliceStart refere-se toostart tempo da fração de saudação. caminho da pasta Olá é diferente para cada fatia. (Por exemplo, wikidatagateway/wikisampledataout/2014100103 ou wikidatagateway/wikisampledataout/2014100104.)

#### <a name="sample-2"></a>Exemplo 2

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
Neste exemplo, ano hello, mês, dia e hora de SliceStart são extraídos em variáveis separadas que são usadas por Olá **folderPath** e **fileName** propriedades.

## <a name="copy-activity-properties"></a>Propriedades da atividade de cópia
Para obter uma lista completa das seções e propriedades disponíveis para definir as atividades, consulte [Criando pipelines](data-factory-create-pipelines.md). As propriedades, como nome, descrição, tabelas de entrada e saída, e políticas, estão disponíveis para todos os tipos de atividade.

As propriedades disponíveis no hello **typeProperties** seção hello atividade em Olá outro lado, variam de acordo com cada tipo de atividade. Para a atividade de cópia hello, propriedades de tipo hello variam dependendo Olá tipos de fontes e coletores.

Atividade de cópia, quando a fonte de saudação é do tipo **FileSystemSource**, Olá propriedade a seguir está disponível em **typeProperties** seção:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| recursiva |Indica se os dados saudação é lida recursivamente de subpastas de saudação ou somente de pasta especificado hello. |True, False (padrão) |Não |

## <a name="json-example-copy-data-from-ftp-server-tooazure-blob"></a>Exemplo JSON: copiar dados do servidor FTP tooAzure Blob
Este exemplo mostra como toocopy dados de um servidor FTP tooAzure armazenamento de Blob. No entanto, os dados podem ser copiados diretamente tooany de saudação coletores Olá indicado em [suporte para armazenamentos de dados e formatos](data-factory-data-movement-activities.md#supported-data-stores-and-formats), usando a atividade de cópia de saudação na fábrica de dados.  

Olá, exemplos a seguir fornecem as definições de JSON de exemplo que você pode usar toocreate um pipeline usando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), ou [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):

* Um serviço vinculado do tipo [FtpServer](#linked-service-properties)
* Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
* Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [FileShare](#dataset-properties)
* Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)
* Um [pipeline](data-factory-create-pipelines.md) com a atividade de cópia que usa [FileSystemSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)

exemplo Hello copia dados de um servidor FTP tooan BLOBs do Azure a cada hora. propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.

### <a name="ftp-linked-service"></a>Serviço vinculado de FTP

Este exemplo usa autenticação básica, com o nome de usuário de saudação e a senha em texto sem formatação. Você também pode usar uma saudação maneiras a seguir:

* Autenticação anônima
* Autenticação básica com credenciais criptografadas
* FTPS (FTP sobre SSL/TLS)

Consulte Olá [serviço vinculado do FTP](#linked-service-properties) seção para diferentes tipos de autenticação que você pode usar.

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
    "type": "FtpServer",
    "typeProperties": {
        "host": "myftpserver.com",           
        "authenticationType": "Basic",
        "username": "Admin",
        "password": "123456"
    }
  }
}
```
### <a name="azure-storage-linked-service"></a>Serviço vinculado de armazenamento do Azure

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
### <a name="ftp-input-dataset"></a>Conjunto de dados de entrada de FTP

Este conjunto de dados se refere a pasta toohello FTP `mysharedfolder` e o arquivo `test.csv`. pipeline de saudação copia o destino de toohello arquivo hello.

Configuração **externo** muito**true** informa ao serviço da fábrica de dados Olá Olá conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados de saudação.

```JSON
{
  "name": "FTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "FTPLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv",
      "useBinaryTransfer": true
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

### <a name="azure-blob-output-dataset"></a>Conjunto de dados de saída de Blob do Azure

Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1). caminho da pasta Olá blob Olá é avaliado dinamicamente, com base na hora de início de saudação da fatia Olá que está sendo processada. caminho da pasta Olá usa partes de ano, mês, dia e horário Olá Olá da hora de início.

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/ftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="a-copy-activity-in-a-pipeline-with-file-system-source-and-blob-sink"></a>Uma atividade de cópia em um pipeline com origem no sistema de arquivos e coletor de blobs

Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora. Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**FileSystemSource**e hello **coletor** tipo está definido muito**BlobSink**.

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
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
        "start": "2016-08-24T18:00:00Z",
        "end": "2016-08-24T19:00:00Z"
    }
}
```
> [!NOTE]
> colunas de toomap de toocolumns de conjunto de dados de origem do conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).

## <a name="next-steps"></a>Próximas etapas
Consulte Olá artigos a seguir:

* toolearn sobre a chave de fatores que afetam o desempenho de movimentação de dados (Copiar atividade) na fábrica de dados e toooptimize de várias maneiras, consulte Olá [Copiar atividade guia de desempenho e ajuste](data-factory-copy-activity-performance.md).

* Para obter instruções passo a passo para criar um pipeline com uma atividade de cópia, consulte Olá [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
