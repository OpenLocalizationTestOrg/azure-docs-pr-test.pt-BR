---
title: dados de aaaMove do HDFS local | Microsoft Docs
description: Saiba mais sobre como toomove dados de local HDFS usando o Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3215b82d-291a-46db-8478-eac1a3219614
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 96387e5dd089099fc2e983ab26d67c2044b973b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-on-premises-hdfs-using-azure-data-factory"></a>Mover dados do HDFS local usando o Azure Data Factory
Este artigo explica como toouse hello atividade de cópia em dados do Azure Data Factory toomove do HDFS local. Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação.

Você pode copiar dados de repositório de dados de coletor do HDFS tooany com suporte. Para obter uma lista de dados de repositórios de suporte como coletores pela atividade de cópia Olá, consulte Olá [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela. Fábrica de dados atualmente oferece suporte à movimentação de dados somente de um armazenamento de dados local HDFS tooother, mas não para mover dados de outros dados tooan repositórios locais HDFS.

> [!NOTE]
> Atividade de cópia não exclui o arquivo de origem Olá depois que ele destino toohello foram copiados com êxito. Se precisar de arquivo de origem toodelete Olá após uma cópia bem-sucedida, criar um arquivo de saudação toodelete atividade personalizada e usar a atividade Olá no pipeline de saudação. 

## <a name="enabling-connectivity"></a>Habilitando a conectividade
Serviço de fábrica de dados oferece suporte à conexão HDFS local tooon usando Olá Gateway de gerenciamento de dados. Consulte [mover dados entre locais de local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) toolearn artigo sobre o Gateway de gerenciamento de dados e instruções passo a passo sobre como configurar o gateway de saudação. Use Olá gateway tooconnect tooHDFS mesmo se ele está hospedado em uma VM de IaaS do Azure.

> [!NOTE]
> Verifique Olá-se de que o Gateway de gerenciamento de dados pode acessar de forma muito**todos os** Olá [server do nó de nome]: [nome de porta de nó] e [servidores de nós de dados]: [porta de nó de dados] do cluster de Hadoop hello. A [porta do nó de nome] padrão é 50070, e a [porta do nó de dados] padrão é 50075.

Embora você possa instalar o gateway em Olá mesmo local máquina ou hello VM do Azure como Olá HDFS, recomendamos que você instale o gateway de saudação em um computador separado/Azure IaaS VM. Ter o gateway em um computador separado reduz a contenção de recursos e aprimora o desempenho. Quando você instalar o gateway de saudação em um computador separado, máquina Olá deve ser capaz de tooaccess máquina Olá Olá HDFS.

## <a name="getting-started"></a>Introdução
Você pode criar um pipeline com uma atividade de cópia que mova dados de uma origem HDFS usando diferentes ferramentas/APIs.

toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**. Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação.

Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**. Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.

Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:

1. Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.
2. Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello.
3. Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.

Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você. Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.  Para obter um exemplo com definições de JSON para entidades de fábrica de dados que são usados toocopy dados de um repositório de dados do HDFS, consulte [exemplo JSON: copiar dados de local HDFS tooAzure Blob](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) deste artigo.

Olá seções a seguir fornece detalhes sobre as propriedades JSON que são usadas toodefine Data Factory entidades específicas tooHDFS:

## <a name="linked-service-properties"></a>Propriedades do serviço vinculado
Um serviço vinculado vincula uma fábrica de dados de tooa de repositório de dados. Criar um serviço vinculado do tipo **Hdfs** toolink uma fábrica de dados local HDFS tooyour. Olá, a tabela a seguir fornece uma descrição para JSON elementos específicos tooHDFS vinculado serviço.

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| type |propriedade de tipo Hello deve ser definida como: **Hdfs** |Sim |
| Url |URL toohello HDFS |Sim |
| authenticationType |Anônimo ou Windows. <br><br> toouse **a autenticação Kerberos** para conector HDFS, consulte muito[nesta seção](#use-kerberos-authentication-for-hdfs-connector) tooset seu ambiente local adequadamente. |Sim |
| userName |Nome de usuário para a autenticação do Windows. |Sim (para a Autenticação do Windows) |
| Senha |Senha para a autenticação do Windows. |Sim (para a Autenticação do Windows) |
| gatewayName |Nome do gateway Olá Olá serviço da fábrica de dados deve usar tooconnect toohello HDFS. |Sim |
| encryptedCredential |[Novo AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) saída de credencial de acesso de saudação. |Não |

### <a name="using-anonymous-authentication"></a>Usando a autenticação anônima

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-windows-authentication"></a>Usando a autenticação do Windows

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```
## <a name="dataset-properties"></a>Propriedades do conjunto de dados
Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo. As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).

Olá **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre o local de saudação de dados Olá no repositório de dados de saudação. Olá typeProperties seção de conjunto de dados do tipo **FileShare** (que inclui o conjunto de dados HDFS) tem Olá seguintes propriedades

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| folderPath |Pasta de toohello de caminho. Exemplo: `myfolder`<br/><br/>Use o caractere de escape ' \ ' para caracteres especiais na cadeia de caracteres de saudação. Por exemplo: para pasta\subpasta, especifique a pasta\\\\subpasta e para d:\pastadeexemplo, especifique d:\\\\pastadeexemplo.<br/><br/>Você pode combinar essa propriedade com **partitionBy** toohave caminhos de pastas com base na fatia datas / horas de início/término. |Sim |
| fileName |Especifique o nome de saudação do arquivo de saudação em Olá **folderPath** se você quiser Olá tabela toorefer tooa arquivo específico na pasta hello. Se você não especificar qualquer valor para essa propriedade, a tabela de saudação aponta tooall arquivos na pasta hello.<br/><br/>Quando o nome de arquivo não for especificado para um conjunto de dados de saída, o nome de saudação do arquivo hello gerado aparecerá em Olá esse formato a seguir: <br/><br/>Data<Guid>.txt (por exemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Não |
| partitionedBy |partitionedBy pode ser usado toospecify um folderPath dinâmico, nome de arquivo para dados de série temporal. Exemplo: folderPath parametrizado para cada hora dos dados. |Não |
| formato | Olá, tipos de formato a seguir têm suporte: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Saudação de conjunto **tipo** propriedade em formato tooone desses valores. Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Se você quiser muito**copiar arquivos como-é** entre repositórios baseada em arquivo (cópia binário), ignore a seção de formato de saudação em ambas as definições de conjunto de dados de entrada e saída. |Não |
| compactação | Especifica tipo de saudação e nível de compactação de dados de saudação. Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**. Os níveis com suporte são **Ideal** e **O mais rápido**. Para saber mais, confira [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support) (Formatos de arquivo e de compactação no Azure Data Factory). |Não |

> [!NOTE]
> filename e fileFilter não podem ser usados simultaneamente.

### <a name="using-partionedby-property"></a>Usando a propriedade partionedBy
Como mencionado na seção anterior hello, você pode especificar um dinâmico folderPath e filename para dados de série temporal com hello **partitionedBy** propriedade [funções da fábrica de dados e variáveis de sistema Olá](data-factory-functions-variables.md).

toolearn mais informações sobre conjuntos de dados de série de tempo, planejamento e fatias, consulte [criando conjuntos de dados](data-factory-create-datasets.md), [de agendamento e execução](data-factory-scheduling-and-execution.md), e [criar Pipelines](data-factory-create-pipelines.md) artigos.

#### <a name="sample-1"></a>Exemplo 1:

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
Neste exemplo {Slice} é substituído pelo valor de saudação da variável de sistema SliceStart fábrica de dados no formato de saudação (AAAAMMDDHH) especificado. Olá SliceStart refere-se toostart tempo da fração de saudação. Olá folderPath é diferente para cada fatia. Por exemplo: wikidatagateway/wikisampledataout/2014100103 ou wikidatagateway/wikisampledataout/2014100104.

#### <a name="sample-2"></a>Exemplo 2:

```JSON
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

Por outro lado, as propriedades disponíveis na seção typeProperties hello atividade Olá variam com cada tipo de atividade. Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.

Para a atividade de cópia, quando a fonte é do tipo **FileSystemSource** Olá propriedades a seguir está disponível na seção de typeProperties:

**FileSystemSource** dá suporte a saudação propriedades a seguir:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| recursiva |Indica se os dados saudação é lida recursivamente de subpastas de saudação ou somente de pasta especificado hello. |True, False (padrão) |Não |

## <a name="supported-file-and-compression-formats"></a>Formatos de arquivo e de compactação com suporte
Consulte o artigo [Formatos de arquivo e de compactação no Azure Data Factory](data-factory-supported-file-and-compression-formats.md) para obter detalhes.

## <a name="json-example-copy-data-from-on-premises-hdfs-tooazure-blob"></a>Exemplo JSON: copiar dados de local HDFS tooAzure Blob
Este exemplo mostra como toocopy dados de um tooAzure HDFS local armazenamento de Blob. No entanto, os dados podem ser copiados **diretamente** tooany de Coletores Olá mencionado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.  

exemplo Hello fornece definições de JSON para Olá entidades da fábrica de dados a seguir. Você pode usar essas definições toocreate um pipeline toocopy os dados de HDFS tooAzure armazenamento de Blob usando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).

1. Um serviço vinculado do tipo [OnPremisesHdfs](#linked-service-properties).
2. Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [FileShare](#dataset-properties).
4. Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Um [pipeline](data-factory-create-pipelines.md) com a Atividade de Cópia que usa [FileSystemSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

exemplo Hello copia dados de um tooan HDFS local BLOBs do Azure a cada hora. propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.

Como uma primeira etapa, configure o gateway de gerenciamento de dados de saudação. Olá instruções Olá [mover dados entre locais de local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo.

**Serviço vinculado do HDFS:** Este exemplo usa Olá autenticação do Windows. Confira a seção [Serviço vinculado ao HDFS](#linked-service-properties) para diferentes tipos de autenticação que você pode usar.

```JSON
{
    "name": "HDFSLinkedService",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

**Serviço vinculado de armazenamento do Azure:**

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

**Conjunto de dados de entrada do HDFS:** este conjunto de dados refere-se a pasta HDFS toohello DataTransfer/UnitTest /. pipeline de saudação copia todos os arquivos de saudação nesse destino toohello de pasta.

Definindo "externo": "verdadeiro" informa serviço da fábrica de dados Olá Olá conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados hello.

```JSON
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

**Conjunto de dados de saída de Blob do Azure:**

Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1). caminho da pasta Olá blob Olá é avaliado dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada. caminho da pasta Olá usa partes de ano, mês, dia e horário da hora de início da saudação.

```JSON
{
    "name": "OutputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/hdfs/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Uma atividade de cópia em um pipeline com origem de Sistema de Arquivos e coletor Blob:**

pipeline de saudação contém uma atividade de cópia que esteja configurado toouse esses conjuntos de dados de entrada e saídos e toorun agendado a cada hora. Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**FileSystemSource** e **coletor** tipo está definido muito**BlobSink**. consulta SQL Olá especificada para Olá **consulta** propriedade seleciona dados Olá Olá após toocopy de hora.

```JSON
{
    "name": "pipeline",
    "properties":
    {
        "activities":
        [
            {
                "name": "HdfsToBlobCopy",
                "inputs": [ {"name": "InputDataset"} ],
                "outputs": [ {"name": "OutputDataset"} ],
                "type": "Copy",
                "typeProperties":
                {
                    "source":
                    {
                        "type": "FileSystemSource"
                    },
                    "sink":
                    {
                        "type": "BlobSink"
                    }
                },
                "policy":
                {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "00:05:00"
                }
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="use-kerberos-authentication-for-hdfs-connector"></a>Usar a autenticação Kerberos para o conector HDFS
Há dois tooset de opções ambiente local de saudação assim como toouse a autenticação Kerberos no conector do HDFS. Você pode escolher Olá um melhor se adapta à sua ocorrência.
* Opção 1: [Fazer com que o computador do gateway ingresse no realm Kerberos](#kerberos-join-realm)
* Opção 2: [habilitar a confiança mútua entre o domínio do Windows e o realm Kerberos](#kerberos-mutual-trust)

### <a name="kerberos-join-realm"></a>Opção 1: Fazer com que o computador do gateway ingresse no realm Kerberos

#### <a name="requirement"></a>Requisito:

* máquina de gateway Olá precisa de realm de Kerberos Olá toojoin e não pode ingressar em qualquer domínio do Windows.

#### <a name="how-tooconfigure"></a>Como tooconfigure:

**No computador do gateway:**

1.  Executar Olá **Ksetup** tooconfigure utilitário Olá servidor KDC do Kerberos e o realm.

    máquina Olá deve ser configurada como um membro de um grupo de trabalho como um realm Kerberos é diferente de um domínio do Windows. Isso pode ser feito definindo o realm de Kerberos hello e adicionar um servidor KDC da seguinte maneira. Substitua *REALM.COM* pelo seu respectivo realm, conforme a necessidade.

            C:> Ksetup /setdomain REALM.COM
            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>

    **Reiniciar** máquina Olá após executar esses comandos de 2.

2.  Verificar a configuração de saudação com **Ksetup** comando. saída de Hello deve ser como:

            C:> Ksetup
            default realm = REALM.COM (external)
            REALM.com:
                kdc = <your_kdc_server_address>

**No Azure Data Factory:**

* Configurar usando o conector Olá HDFS **autenticação do Windows** junto com o Kerberos principal nome e senha tooconnect toohello HDFS fonte de dados. Verifique a seção de [propriedades do Serviço Vinculado HDFS](#linked-service-properties) nos detalhes da configuração.

### <a name="kerberos-mutual-trust"></a>Opção 2: habilitar a confiança mútua entre o domínio do Windows e o realm Kerberos

#### <a name="requirement"></a>Requisito:
*   máquina de gateway Olá deve ingressar em um domínio do Windows.
*   Você precisar de configurações de permissão tooupdate Olá controlador de domínio.

#### <a name="how-tooconfigure"></a>Como tooconfigure:

> [!NOTE]
> Substitua REALM.COM e AD.COM em Olá tutorial com sua respectivo realm e controlador de domínio a seguir conforme necessário.

**No servidor KDC:**

1.  Edita a configuração do KDC Olá no **krb5** toolet arquivo KDC confiança referência toohello seguindo o modelo de configuração de domínio do Windows. Por padrão, a configuração de saudação está localizada em **/etc/krb5.conf**.

            [logging]
             default = FILE:/var/log/krb5libs.log
             kdc = FILE:/var/log/krb5kdc.log
             admin_server = FILE:/var/log/kadmind.log

            [libdefaults]
             default_realm = REALM.COM
             dns_lookup_realm = false
             dns_lookup_kdc = false
             ticket_lifetime = 24h
             renew_lifetime = 7d
             forwardable = true

            [realms]
             REALM.COM = {
              kdc = node.REALM.COM
              admin_server = node.REALM.COM
             }
            AD.COM = {
             kdc = windc.ad.com
             admin_server = windc.ad.com
            }

            [domain_realm]
             .REALM.COM = REALM.COM
             REALM.COM = REALM.COM
             .ad.com = AD.COM
             ad.com = AD.COM

            [capaths]
             AD.COM = {
              REALM.COM = .
             }

  **Reiniciar** Olá serviço KDC após a configuração.

2.  Preparar uma entidade nomeada  **krbtgt/REALM.COM@AD.COM**  no servidor do KDC com hello comando a seguir:

            Kadmin> addprinc krbtgt/REALM.COM@AD.COM

3.  No arquivo de configuração de serviço HDFS **hadoop.security.auth_to_local**, adicione `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.

**No controlador de domínio:**

1.  Execute seguinte Olá **Ksetup** tooadd uma entrada de realm de comandos:

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

2.  Estabelece relação de confiança de Realm de tooKerberos de domínio do Windows. [senha] é a senha de saudação para entidade Olá  **krbtgt/REALM.COM@AD.COM** .

            C:> netdom trust REALM.COM /Domain: AD.COM /add /realm /passwordt:[password]

3.  Selecione o algoritmo de criptografia usado no Kerberos.

    1. Vá tooServer Manager > Gerenciamento de diretiva de grupo > domínio > objetos de diretiva de grupo > padrão ou política de domínio do Active e editar.

    2. Em Olá **Editor de gerenciamento de política de grupo** janela pop-up, vá tooComputer Configuração > Políticas > configurações do Windows > configurações de segurança > políticas locais > Opções de segurança e configurar **rede segurança: configurar tipos de criptografia permitidos para o Kerberos**.

    3. Algoritmo de criptografia Olá selecione deseja toouse quando se conectar tooKDC. Normalmente, basta selecionar todas as opções de saudação.

        ![Configuração dos tipos de criptografia para Kerberos](media/data-factory-hdfs-connector/config-encryption-types-for-kerberos.png)

    4. Use **Ksetup** toobe comando toospecify Olá criptografia algoritmo usado em Olá TERRITÓRIO específico.

                C:> ksetup /SetEncTypeAttr REALM.COM DES-CBC-CRC DES-CBC-MD5 RC4-HMAC-MD5 AES128-CTS-HMAC-SHA1-96 AES256-CTS-HMAC-SHA1-96

4.  Crie mapeamento de saudação entre a conta de domínio hello e Kerberos principal, em ordem toouse Kerberos principal no domínio do Windows.

    1. Iniciar ferramentas administrativas hello > **computadores e usuários do Active Directory**.

    2. Configure recursos avançados clicando em **Exibir** > **Recursos Avançados**.

    3. Localizar Olá conta toowhich toocreate mapeamentos de desejado e clique tooview **mapeamentos de nome** > clique **nomes Kerberos** guia.

    4. Adicione uma entidade de território hello.

        ![Mapear identidade de segurança](media/data-factory-hdfs-connector/map-security-identity.png)

**No computador do gateway:**

* Execute seguinte Olá **Ksetup** comandos tooadd uma entrada de território.

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

**No Azure Data Factory:**

* Configurar usando o conector Olá HDFS **autenticação do Windows** junto com sua conta de domínio ou uma fonte de dados Principal Kerberos tooconnect toohello HDFS. Verifique a seção de [propriedades do Serviço Vinculado HDFS](#linked-service-properties) nos detalhes da configuração.

> [!NOTE]
> colunas de toomap de toocolumns de conjunto de dados de origem do conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).


## <a name="performance-and-tuning"></a>Desempenho e Ajuste
Consulte [guia de ajuste e desempenho de atividade de cópia](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias formas-lo.
