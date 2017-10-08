---
title: aaaMove dados de uma fonte de HTTP - Azure | Microsoft Docs
description: Saiba mais sobre como toomove de um local ou uma nuvem HTTP da fonte de dados usando o Azure Data Factory.
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
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: e39b9cbff870aef4be91938cacff39a2fd12d64a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-http-source-using-azure-data-factory"></a>Mover dados de uma origem HTTP usando o Azure Data Factory
Este artigo descreve como toouse hello atividade de cópia em dados do Azure Data Factory toomove de um tooa de ponto de extremidade HTTP no local/em nuvem suporte para armazenamento de dados do coletor. Este artigo aproveita Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo que apresenta uma visão geral de movimentação de dados com Copiar atividade e hello lista de repositórios de dados têm suportada como/coletores de fontes.

Fábrica de dados atualmente suporta apenas os dados movidos de um HTTP tooother repositórios de dados de origem, mas não movendo os dados de outros dados armazena o destino tooan HTTP.

## <a name="supported-scenarios-and-authentication-types"></a>Cenários com suporte e tipos de autenticação
Você pode usar esses dados de tooretrieve do conector HTTP do **ponto de extremidade HTTP/s de nuvem e local** usando HTTP **obter** ou **POST** método. Olá, tipos de autenticação a seguir têm suporte: **anônimo**, **básica**, **Digest**, **Windows**, e  **ClientCertificate**. Observe a diferença de saudação entre esse conector e Olá [Conector Web de tabela](data-factory-web-table-connector.md) é: Olá este último é a tabela de tooextract usado conteúda da página HTML de web.

Ao copiar dados de um ponto de extremidade HTTP do local, você precisa instalar um Gateway de gerenciamento de dados no ambiente do local de saudação/Azure VM. Consulte [mover dados entre locais de local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) toolearn artigo sobre o Gateway de gerenciamento de dados e instruções passo a passo sobre como configurar o gateway de saudação.

## <a name="getting-started"></a>Introdução
Você pode criar um pipeline com uma atividade de cópia que mova dados de uma origem HTTP usando ferramentas/APIs diferentes.

- toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**. Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação.

- Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**. Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia. Para exemplos de JSON toocopy dados de origem HTTP tooAzure armazenamento de Blob, consulte [exemplos JSON](#json-examples) seção neste artigo.

## <a name="linked-service-properties"></a>Propriedades do serviço vinculado
Olá, a tabela a seguir fornece uma descrição para JSON elementos específicos tooHTTP vinculado serviço.

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| type | propriedade de tipo Hello deve ser definida como: `Http`. | Sim |
| url | Base de URL toohello servidor Web | Sim |
| authenticationType | Especifica o tipo de autenticação de saudação. Os valores permitidos são: **Anônimo**, **Básico**, **Digest**, **Windows** e **ClientCertificate**. <br><br> Consulte toosections abaixo da tabela em mais propriedades e exemplos JSON para esses tipos de autenticação, respectivamente. | Sim |
| enableServerCertificateValidation | Especifique se tooenable servidor SSL a validação de certificado se origem for o servidor da Web HTTPS | Não, o padrão é true |
| gatewayName | Nome da saudação Data Management Gateway tooconnect tooan origem HTTP no local. | Sim se estiver copiando dados de uma origem HTTP local. |
| encryptedCredential | Credencial criptografada tooaccess Olá ponto de extremidade HTTP. Gerado automaticamente quando você configura as informações de autenticação de saudação no diálogo de pop-up de ClickOnce de assistente ou saudação de cópia. | Não. Aplique somente quando estiver copiando dados de um servidor HTTP local. |

Consulte [mover dados entre fontes locais e na nuvem de saudação com Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) para obter detalhes sobre como configurar credenciais locais HTTP conector fonte de dados.

### <a name="using-basic-digest-or-windows-authentication"></a>Usando a autenticação Básica, Digest ou Windows

Definir `authenticationType` como `Basic`, `Digest`, ou `Windows`e especifique Olá seguintes propriedades além Olá conector HTTP genérico aqueles introduzido acima:

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| Nome de Usuário | Nome de usuário tooaccess Olá ponto de extremidade HTTP. | Sim |
| Senha | Senha do usuário da saudação (nome de usuário). | Sim |

#### <a name="example-using-basic-digest-or-windows-authentication"></a>Exemplo: usando a autenticação Básica, Digest ou Windows

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "basic",
            "url" : "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

### <a name="using-clientcertificate-authentication"></a>Usando a autenticação ClientCertificate

Definir toouse a autenticação básica, `authenticationType` como `ClientCertificate`e especifique Olá seguintes propriedades além Olá conector HTTP genérico aqueles introduzido acima:

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| embeddedCertData | conteúdo codificado com Base64 Olá de dados binários do arquivo de troca de informações pessoais (PFX) hello. | Especifique a saudação `embeddedCertData` ou `certThumbprint`. |
| certThumbprint | Olá a impressão digital do certificado Olá foi instalado no repositório de certificados do computador do gateway. Aplique somente ao copiar dados de uma origem HTTP local. | Especifique a saudação `embeddedCertData` ou `certThumbprint`. |
| Senha | Senha associada com o certificado de saudação. | Não |

Se você usar `certThumbprint` para certificado de autenticação e hello está instalado no repositório pessoal de saudação do computador local hello, você precisa que o serviço de gateway do toogrant Olá permissão de leitura toohello:

1. Iniciar o MMC (Console de Gerenciamento Microsoft). Adicionar Olá **certificados** snap-in que Olá destinos **computador Local**.
2. Expanda **Certificados**, **Pessoal** e clique em **Certificados**.
3. Certificado de saudação do armazenamento pessoal hello e selecione **todas as tarefas**->**gerenciar chaves particulares...**
3. Em Olá **segurança** guia, adicione a conta de usuário Olá sob a qual o serviço de Host do Gateway de gerenciamento de dados está em execução com certificado de toohello Olá acesso de leitura.  

#### <a name="example-using-client-certificate"></a>Exemplo: usando o certificado do cliente
Isso vinculado links serviço seu servidor de web data factory tooan locais HTTP. Ele usa um certificado de cliente é instalado na máquina de saudação com Gateway de gerenciamento de dados instalado.

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"

        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a>Exemplo: usando o certificado do cliente em um arquivo
Isso vinculado links serviço seu servidor de web data factory tooan locais HTTP. Ele usa um arquivo de certificado de cliente no computador de saudação com Gateway de gerenciamento de dados instalado.

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

## <a name="dataset-properties"></a>Propriedades do conjunto de dados
Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo. As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).

Olá **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre o local de saudação de dados Olá no repositório de dados de saudação. Olá typeProperties seção de conjunto de dados do tipo **Http** tem Olá seguintes propriedades

| Propriedade | Descrição | Obrigatório |
|:--- |:--- |:--- |
| type | Tipo de saudação do conjunto de dados de saudação especificado. deve ser definido muito`Http`. | Sim |
| relativeUrl | Um relativa URL toohello de recursos que contém dados de saudação. Quando não for especificado, somente URL Olá especificado na definição de serviço vinculada de saudação é usado. <br><br> URL do tooconstruct dinâmico, você pode usar [funções da fábrica de dados e variáveis de sistema](data-factory-functions-variables.md), por exemplo, "relativeUrl": "$$Text.Format (' Meu/relatório? mês = {0:yyyy}-{0:MM} & fmt = csv', SliceStart)". | Não |
| requestMethod | Método Http. Os valores permitidos são **GET** ou **POST**. | Não. O padrão é `GET`. |
| additionalHeaders | Cabeçalhos de solicitação HTTP adicionais. | Não |
| requestBody | O corpo da solicitação HTTP. | Não |
| formato | Se você quiser toosimply **recuperar dados de saudação do ponto de extremidade HTTP como-é** sem analisá-lo, ignore essa configuração de formato. <br><br> Se você quiser resposta HTTP de saudação tooparse conteúdo durante a cópia, Olá tipos de formato a seguir têm suporte: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**. Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). |Não |
| compactação | Especifica tipo de saudação e nível de compactação de dados de saudação. Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**. Os níveis com suporte são **Ideal** e **O mais rápido**. Para saber mais, confira [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support) (Formatos de arquivo e de compactação no Azure Data Factory). |Não |

### <a name="example-using-hello-get-default-method"></a>Exemplo: usando o método do hello GET (padrão)

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

### <a name="example-using-hello-post-method"></a>Exemplo: usando o método POST de saudação

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
           "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a>Propriedades da atividade de cópia
Para obter uma lista completa das seções e propriedades disponíveis para a definição de atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo. As propriedades, como nome, descrição, tabelas de entrada e saída, e política, estão disponíveis para todos os tipos de atividades.

As propriedades disponíveis no hello **typeProperties** seção de atividade Olá Olá outro lado variam de acordo com cada tipo de atividade. Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.

Atualmente, quando a fonte de saudação na atividade de cópia é do tipo **HttpSource**, Olá propriedades a seguir têm suporte.

| Propriedade | Descrição | Obrigatório |
| -------- | ----------- | -------- |
| httpRequestTimeout | Olá tempo limite (TimeSpan) para tooget de solicitação HTTP Olá uma resposta. É Olá timeout tooget uma resposta não Olá timeout tooread dados de resposta. | Não. Valor padrão: 00:01:40 |

## <a name="supported-file-and-compression-formats"></a>Formatos de arquivo e de compactação com suporte
Consulte o artigo [Formatos de arquivo e de compactação no Azure Data Factory](data-factory-supported-file-and-compression-formats.md) para obter detalhes.

## <a name="json-examples"></a>Exemplos de JSON
saudação de exemplo a seguir fornece as definições de JSON de exemplo que você pode usar toocreate um pipeline usando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Eles mostram como tooAzure armazenamento de Blob da fonte de dados de toocopy de HTTP. No entanto, os dados podem ser copiados **diretamente** de qualquer uma das fontes tooany de Coletores Olá mencionado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.

### <a name="example-copy-data-from-http-source-tooazure-blob-storage"></a>Exemplo: Copiar dados de origem HTTP tooAzure armazenamento de Blob
Olá solução da fábrica de dados para este exemplo contém Olá entidades da fábrica de dados a seguir:

1. Um serviço vinculado do tipo [HTTP](#linked-service-properties).
2. Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [Http](#dataset-properties).
4. Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Um [pipeline](data-factory-create-pipelines.md) com a Atividade de Cópia que usa [HttpSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

exemplo Hello copia dados de uma origem HTTP tooan BLOBs do Azure a cada hora. propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.

### <a name="http-linked-service"></a>Serviço vinculado HTTP
Este exemplo usa Olá HTTP vinculado de serviço com a autenticação anônima. Confira a seção [Serviço vinculado HTTP](#linked-service-properties) para ver os diferentes tipos de autenticação que você pode usar.

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
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

### <a name="http-input-dataset"></a>Conjunto de dados de entrada HTTP
Configuração **externo** muito**true** informa o serviço da fábrica de dados Olá Olá conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados hello.

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}

```

### <a name="azure-blob-output-dataset"></a>Conjunto de dados de saída de Blob do Azure

Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1).

```JSON
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/Movies"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

### <a name="pipeline-with-copy-activity"></a>Pipeline com Atividade de cópia

Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora. Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**HttpSource** e **coletor** tipo está definido muito**BlobSink**.

Consulte [HttpSource](#copy-activity-properties) para lista de saudação de propriedades com suporte pelo Olá HttpSource.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "HttpSourceToAzureBlob",
        "description": "Copy from an HTTP source tooan Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "HttpSourceDataInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "HttpSource"
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
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```

> [!NOTE]
> colunas de toomap de toocolumns de conjunto de dados de origem do conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Desempenho e Ajuste
Consulte [guia de ajuste e desempenho de atividade de cópia](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias formas-lo.
