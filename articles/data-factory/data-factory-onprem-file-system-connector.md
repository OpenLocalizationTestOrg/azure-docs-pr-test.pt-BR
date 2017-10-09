---
title: aaaCopy dados para/de um sistema de arquivos usando o Azure Data Factory | Microsoft Docs
description: Saiba como toocopy tooand de dados de um sistema de arquivos local por meio do Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ce19f1ae-358e-4ffc-8a80-d802505c9c84
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 201b8bc3ffa639df781443aa0c3f95c975d280be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-an-on-premises-file-system-by-using-azure-data-factory"></a>Copiar dados tooand de um sistema de arquivos local usando o Azure Data Factory
Este artigo explica como toouse hello atividade de cópia em dados do Azure Data Factory toocopy de/para um sistema de arquivos local. Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação.

## <a name="supported-scenarios"></a>Cenários com suporte
Você pode copiar dados **de um sistema de arquivos local** toohello repositórios de dados a seguir:

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

Você pode copiar dados de saudação armazenamentos de dados a seguir **tooan sistema de arquivos local**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> Atividade de cópia não exclui o arquivo de origem Olá depois que ele destino toohello foram copiados com êxito. Se precisar de arquivo de origem toodelete Olá após uma cópia bem-sucedida, criar um arquivo de saudação toodelete atividade personalizada e usar a atividade Olá no pipeline de saudação. 

## <a name="enabling-connectivity"></a>Habilitando a conectividade
Fábrica de dados oferece suporte à conexão tooand de um sistema de arquivos local por meio de **Data Management Gateway**. Você deve instalar Olá Data Management Gateway em seu ambiente local para Olá Data Factory serviço tooconnect tooany com suporte no repositório de dados local incluindo o sistema de arquivos. toolearn sobre o Gateway de gerenciamento de dados e para instruções passo a passo sobre como configurar o gateway hello, consulte [mover dados entre fontes locais e na nuvem de saudação com Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md). Além de Gateway de gerenciamento de dados, nenhum outro arquivo binário necessário toobe instalado toocommunicate tooand de um sistema de arquivos local. Você deve instalar e usar Olá Gateway de gerenciamento de dados, mesmo se o sistema de arquivos Olá estiver em VM do Azure IaaS. Para obter informações detalhadas sobre o gateway hello, consulte [Data Management Gateway](data-factory-data-management-gateway.md).

instalar toouse um compartilhamento de arquivo do Linux, [Samba](https://www.samba.org/) no servidor Linux e instalar o Gateway de gerenciamento de dados em um servidor Windows. Não há suporte para a instalação do Gateway de Gerenciamento de Dados em um servidor Linux.

## <a name="getting-started"></a>Introdução
Você pode criar um pipeline com uma atividade de cópia que mova dados bidirecionalmente de/para um sistema de arquivos usando ferramentas/APIs diferentes.

toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**. Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação.

Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**. Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.

Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:

1. Criar uma **data factory**. Um data factory pode conter um ou mais pipelines. 
2. Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica. Por exemplo, se você estiver copiando dados de um sistema de arquivos do blob do Azure storage tooan local, você criar duas toolink de serviços vinculados seu sistema de arquivos local e a fábrica de dados de tooyour de conta de armazenamento do Azure. Para propriedades de serviço vinculado que sistema de arquivos local tooan específicos, consulte [vinculado propriedades do serviço](#linked-service-properties) seção.
3. Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello. O exemplo hello mencionado na última etapa do hello, você criará um contêiner de blob do conjunto de dados toospecify hello e a pasta que contém os dados de entrada hello. E, então, criar outro conjunto de dados toospecify Olá pasta e nome de arquivo (opcional) no sistema de arquivos. Para propriedades de conjunto de dados que são específicos de local de tooon sistema de arquivos, consulte [propriedades de conjunto de dados](#dataset-properties) seção.
4. Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída. Exemplo hello mencionado anteriormente, você usar BlobSource como uma origem e FileSystemSink como um coletor de atividade de cópia de saudação. Da mesma forma, se você estiver copiando de tooAzure de sistema de arquivos local armazenamento de Blob, use FileSystemSource e BlobSink na atividade de cópia de saudação. Para o sistema de arquivos de propriedades de atividade de cópia local tooon específico, consulte [copiar as propriedades de atividade](#copy-activity-properties) seção. Para obter detalhes sobre como toouse um repositório de dados como uma origem ou um coletor, clique em Olá link na seção anterior de saudação para seu armazenamento de dados.

Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você. Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.  Para obter exemplos com definições de JSON para entidades de fábrica de dados que são usados toocopy dados para/de um sistema de arquivos, consulte [exemplos JSON](#json-examples-for-copying-data-to-and-from-file-system) deste artigo.

Olá seções a seguir fornece detalhes sobre as propriedades JSON que são usadas toodefine Data Factory entidades toofile específico sistema:

## <a name="linked-service-properties"></a>Propriedades do serviço vinculado
Você pode vincular uma fábrica de dados do Azure local arquivo sistema tooan com hello **o servidor de arquivos local** serviço vinculado. Olá a tabela a seguir fornece descrições dos elementos JSON que são específico toohello serviço vinculado de servidor de arquivos local.

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| type |Verifique se a propriedade de tipo hello está definida muito**OnPremisesFileServer**. |Sim |
| host |Especifica o caminho de raiz de saudação da pasta Olá que você deseja toocopy. Use o caractere de escape de saudação ' \ ' para caracteres especiais na cadeia de caracteres de saudação. Confira [Definições de conjunto de dados e serviço vinculado de exemplo](#sample-linked-service-and-dataset-definitions) para obter exemplos. |Sim |
| userid |Especifique a ID de saudação do usuário de saudação que tem acesso toohello server. |Não (se você escolher encryptedcredential) |
| Senha |Especifique a senha de saudação para usuário hello (userid). |Não (se você escolher encryptedcredential |
| encryptedCredential |Especifique credenciais Olá criptografado que você pode obter executando Olá AzureRmDataFactoryEncryptValue novo cmdlet. |Não (se você escolher toospecify ID de usuário e senha em texto sem formatação) |
| gatewayName |Especifica o nome de saudação do gateway de saudação que Data Factory deve usar o servidor de arquivos tooconnect toohello local. |Sim |


### <a name="sample-linked-service-and-dataset-definitions"></a>Definições de conjunto de dados e serviço vinculado de exemplo
| Cenário | Host em definição de serviço vinculado | folderPath em definição de conjunto de dados |
| --- | --- | --- |
| Pasta local no computador do Gateway de Gerenciamento de Dados  <br/><br/>Exemplos: D:\\\* ou D:\pasta\subpasta\\* |D:\\\\ (para o Gateway de Gerenciamento de Dados 2.0 e versões posteriores) <br/><br/> localhost (para versões anteriores do Gateway de Gerenciamento de Dados 2.0) |.\\\\ ou pasta\\\\subpasta (para o Gateway de Gerenciamento de Dados 2.0 e versões posteriores) <br/><br/>D:\\\\ ou D:\\\\pasta\\\\subpasta (para a versão de gateway abaixo de 2.0) |
| Pasta compartilhada remota:  <br/><br/>Exemplos: \\\\meuservidor\\compartilhar\\\* ou \\\\meuservidor\\compartilhar\\pasta\\subpasta\\* |\\\\\\\\meuservidor\\\\compartilhar |.\\\\ ou pasta\\\\subpasta |


### <a name="example-using-username-and-password-in-plain-text"></a>Exemplo: usando username e password em texto sem formatação

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

### <a name="example-using-encryptedcredential"></a>Exemplo: usando encryptedcredential

```JSON
{
  "Name": " OnPremisesFileServerLinkedService ",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "D:\\",
      "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
      "gatewayName": "mygateway"
    }
  }
}
```

## <a name="dataset-properties"></a>Propriedades do conjunto de dados
Para obter uma lista completa das seções e propriedades disponíveis para definir os conjuntos de dados, confira [Criando conjuntos de dados](data-factory-create-datasets.md). As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados.

seção de typeProperties Olá é diferente para cada tipo de conjunto de dados. Ele fornece informações como Olá local e o formato dos dados Olá no repositório de dados de saudação. Olá typeProperties seção de conjunto de dados de saudação do tipo **FileShare** tem Olá propriedades a seguir:

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| folderPath |Especifica a pasta de toohello subcaminho hello. Use o caractere de escape de saudação ' \' para caracteres especiais na cadeia de caracteres de saudação. Confira [Definições de conjunto de dados e serviço vinculado de exemplo](#sample-linked-service-and-dataset-definitions) para obter exemplos.<br/><br/>Você pode combinar essa propriedade com **partitionBy** toohave caminhos de pastas com base na fatia datas / horas de início/término. |Sim |
| fileName |Especifique o nome de saudação do arquivo de saudação em Olá **folderPath** se você quiser Olá tabela toorefer tooa arquivo específico na pasta hello. Se você não especificar qualquer valor para essa propriedade, a tabela de saudação aponta tooall arquivos na pasta hello.<br/><br/>Quando **fileName** não for especificado para um conjunto de dados de saída e **preserveHierarchy** não for especificado no coletor de atividade, nome de saudação do arquivo hello gerado está em Olá formato a seguir: <br/><br/>`Data.<Guid>.txt` (Exemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |Não |
| fileFilter |Especifique um filtro toobe usado tooselect um subconjunto de arquivos no hello folderPath em vez de todos os arquivos. <br/><br/>Os valores permitidos são: `*` (vários caracteres) e `?` (um único caractere).<br/><br/>Exemplo 1: "fileFilter": "*.log"<br/>Exemplo 2: "fileFilter": 2014-1-?.txt"<br/><br/>Observe que fileFilter é aplicável a um conjunto de dados FileShare de entrada. |Não |
| partitionedBy |Você pode usar partitionedBy toospecify um dinâmico folderPath/nome do arquivo de dados da série temporal. Um exemplo é folderPath parametrizado para cada hora dos dados. |Não |
| formato | Olá, tipos de formato a seguir têm suporte: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Saudação de conjunto **tipo** propriedade em formato tooone desses valores. Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Se você quiser muito**copiar arquivos como-é** entre repositórios baseada em arquivo (cópia binário), ignore a seção de formato de saudação em ambas as definições de conjunto de dados de entrada e saída. |Não |
| compactação | Especifica tipo de saudação e nível de compactação de dados de saudação. Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**. Os níveis com suporte são **Ideal** e **O mais rápido**. confira [Formatos de arquivo e de compactação no Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Não |

> [!NOTE]
> Você não pode usar fileName e fileFilter simultaneamente.

### <a name="using-partitionedby-property"></a>Usando a propriedade partitionedBy
Como mencionado na seção anterior hello, você pode especificar um dinâmico folderPath e filename para dados de série temporal com hello **partitionedBy** propriedade [funções da fábrica de dados e variáveis de sistema Olá](data-factory-functions-variables.md).

toounderstand obter mais detalhes sobre conjuntos de dados de série temporal, agendamento e fatias, consulte [criando conjuntos de dados](data-factory-create-datasets.md), [de agendamento e execução](data-factory-scheduling-and-execution.md), e [criar pipelines](data-factory-create-pipelines.md).

#### <a name="sample-1"></a>Exemplo 1:

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

Neste exemplo, {Slice} é substituído pelo valor de saudação da variável de sistema de fábrica de dados Olá SliceStart no formato de saudação (AAAAMMDDHH). SliceStart refere-se toostart tempo da fração de saudação. Olá folderPath é diferente para cada fatia. Por exemplo: wikidatagateway/wikisampledataout/2014100103 ou wikidatagateway/wikisampledataout/2014100104.

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

Neste exemplo, ano, mês, dia e hora de SliceStart são extraídos em variáveis separadas que usam as propriedades folderPath e fileName hello.

## <a name="copy-activity-properties"></a>Propriedades da atividade de cópia
Para obter uma lista completa das seções e propriedades disponíveis para a definição de atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo. As propriedades, como nome, descrição, conjuntos de dados de entrada e saída, e políticas, estão disponíveis para todos os tipos de atividade. Por outro lado, as propriedades disponíveis no hello **typeProperties** seção de atividade Olá variam de acordo com cada tipo de atividade.

Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores. Se você estiver movendo dados de um sistema de arquivos local, você defina o tipo de fonte de saudação na atividade de cópia de saudação muito**FileSystemSource**. Da mesma forma, se você estiver movendo dados tooan sistema de arquivos local, você definir o tipo de coletor Olá na atividade de cópia de saudação muito**FileSystemSink**. Esta seção fornece uma lista das propriedades às quais FileSystemSource e FileSystemSink dão suporte.

**FileSystemSource** dá suporte a saudação propriedades a seguir:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| recursiva |Indica se os dados saudação é lida recursivamente de subpastas de saudação ou somente de pasta especificado hello. |True, False (padrão) |Não |

**FileSystemSink** dá suporte a saudação propriedades a seguir:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| copyBehavior |Define o comportamento de cópia de saudação quando origem Olá é BlobSource ou sistema de arquivos. |**PreserveHierarchy:** preserva a hierarquia de arquivo hello na pasta de destino de saudação. Ou seja, caminho relativo do Olá Olá arquivo toohello origem da pasta de origem é Olá igual Olá o caminho relativo da pasta de destino toohello do arquivo de destino hello.<br/><br/>**FlattenHierarchy:** todos os arquivos da pasta de origem Olá são criados no primeiro nível saudação da pasta de destino. arquivos de destino de saudação são criados com um nome gerado automaticamente.<br/><br/>**MergeFiles:** mescla todos os arquivos Olá pasta tooone do arquivo de origem. Se o nome do blob/nome de arquivo hello for especificado, o nome mesclado Olá é nome especificado da saudação. Caso contrário, ele será um nome de arquivo gerado automaticamente. |Não |

### <a name="recursive-and-copybehavior-examples"></a>exemplos de recursive e copyBehavior
Esta seção descreve o comportamento resultante de saudação da operação de cópia de saudação para diferentes combinações de valores de propriedades de saudação recursiva e copyBehavior.

| valor de recursive | valor de copyBehavior | Comportamento resultante |
| --- | --- | --- |
| verdadeiro |preserveHierarchy |Para uma pasta de origem Pasta1 com hello estrutura, a seguir<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5<br/><br/>pasta de destino Olá Pasta1 é criada com hello mesma estrutura como fonte de saudação:<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5 |
| verdadeiro |flattenHierarchy |Para uma pasta de origem Pasta1 com hello estrutura, a seguir<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5<br/><br/>destino de saudação Pasta1 é criado com hello estrutura a seguir: <br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nome gerado automaticamente para o Arquivo1<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo2<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo3<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo4<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo5 |
| verdadeiro |mergeFiles |Para uma pasta de origem Pasta1 com hello estrutura, a seguir<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5<br/><br/>destino de saudação Pasta1 é criado com hello estrutura a seguir: <br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Os conteúdos de Arquivo1 + Arquivo2 + Arquivo3 + Arquivo4 + Arquivo5 são mesclados em um arquivo com um nome de arquivo gerado automaticamente. |
| false |preserveHierarchy |Para uma pasta de origem Pasta1 com hello estrutura, a seguir<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5<br/><br/>pasta de destino Olá Pasta1 é criada com hello estrutura a seguir:<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2<br/><br/>A Subpasta1 com Arquivo3, Arquivo4 e Arquivo5 não é selecionada. |
| false |flattenHierarchy |Para uma pasta de origem Pasta1 com hello estrutura, a seguir<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5<br/><br/>pasta de destino Olá Pasta1 é criada com hello estrutura a seguir:<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nome gerado automaticamente para o Arquivo1<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo2<br/><br/>A Subpasta1 com Arquivo3, Arquivo4 e Arquivo5 não é selecionada. |
| false |mergeFiles |Para uma pasta de origem Pasta1 com hello estrutura, a seguir<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5<br/><br/>pasta de destino Olá Pasta1 é criada com hello estrutura a seguir:<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Os conteúdos de Arquivo1 + Arquivo2 são mesclados em um arquivo com um nome de arquivo gerado automaticamente.<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nome gerado automaticamente para o Arquivo1<br/><br/>A Subpasta1 com Arquivo3, Arquivo4 e Arquivo5 não é selecionada. |

## <a name="supported-file-and-compression-formats"></a>Formatos de arquivo e de compactação com suporte
Consulte o artigo [Formatos de arquivo e de compactação no Azure Data Factory](data-factory-supported-file-and-compression-formats.md) para obter detalhes.

## <a name="json-examples-for-copying-data-tooand-from-file-system"></a>Exemplos JSON para copiar dados tooand do sistema de arquivos
Olá, exemplos a seguir fornecem as definições de JSON de exemplo que você pode usar toocreate um pipeline usando Olá [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Eles mostram como toocopy tooand de dados de um sistema de arquivos local e o armazenamento de BLOBs do Azure. No entanto, você pode copiar dados *diretamente* de qualquer um dos Olá fontes tooany de Coletores Olá listados na [suporte para origens e coletores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando a atividade de cópia na fábrica de dados do Azure.

### <a name="example-copy-data-from-an-on-premises-file-system-tooazure-blob-storage"></a>Exemplo: Copiar dados de um tooAzure de sistema de arquivos local armazenamento de Blob
Este exemplo mostra como toocopy dados de um tooAzure de sistema de arquivos local armazenamento de Blob. exemplo Hello tem Olá entidades da fábrica de dados a seguir:

* Um serviço vinculado do tipo [OnPremisesFileServer](#linked-service-properties).
* Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [FileShare](#dataset-properties).
* Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* Um [pipeline](data-factory-create-pipelines.md) com a Atividade de Cópia que usa [FileSystemSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

saudação de exemplo a seguir copia dados de série temporal de um tooAzure de sistema de arquivos local armazenamento de Blob a cada hora. propriedades JSON Olá usados nesses exemplos são descritas nas seções de saudação após exemplos de saudação.

Como uma primeira etapa, configurar o Gateway de gerenciamento de dados de acordo com as instruções de saudação do [mover dados entre fontes locais e na nuvem de saudação com Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).

**Serviço vinculado do Servidor de Arquivos Local:**

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

É recomendável usar Olá **encryptedCredential** Olá em vez disso, a propriedade **userid** e **senha** propriedades. Confira [File Server linked service](#linked-service-properties) (Serviço vinculado do Servidor de Arquivos) para obter detalhes sobre este serviço vinculado.

**Serviço vinculado de armazenamento do Azure:**

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

**Conjunto de dados de entrada do sistema de arquivos local:**

Dados são coletados de um novo arquivo a cada hora. Olá folderPath e fileName propriedades são determinadas com base na hora de início de saudação da fatia hello.  

Configuração `"external": "true"` informa a fábrica de dados Olá conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados hello.

```JSON
{
  "name": "OnpremisesFileSystemInput",
  "properties": {
    "type": " FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
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
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

**Conjunto de dados do Armazenamento de Blobs do Azure:**

Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1). caminho da pasta Olá blob Olá é avaliado dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada. caminho da pasta Olá usa partes de ano, mês, dia e hora Olá Olá da hora de início.

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**Uma atividade de cópia em um pipeline com origem de Sistema de Arquivos e coletor Blob:**

Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora. Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**FileSystemSource**, e **coletor** tipo está definido muito**BlobSink**.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T19:00:00",
    "description":"Pipeline for copy activity",
    "activities":[  
      {
        "name": "OnpremisesFileSystemtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "OnpremisesFileSystemInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
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
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```

### <a name="example-copy-data-from-azure-sql-database-tooan-on-premises-file-system"></a>Exemplo: Copiar dados do sistema de arquivos do banco de dados do Azure SQL tooan local
Olá mostra de exemplo a seguir:

* Um serviço vinculado do tipo [AzureSqlDatabase.](data-factory-azure-sql-connector.md#linked-service-properties)
* Um serviço vinculado do tipo [OnPremisesFileServer](#linked-service-properties).
* Um conjunto de dados de entrada do tipo [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).
* Um conjunto de dados de saída do tipo [FileShare](#dataset-properties).
* Um pipeline com a atividade de cópia que usa [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) e [FileSystemSink](#copy-activity-properties).

exemplo Hello copia dados de série temporal de um sistema de arquivos local do SQL Azure tabela tooan a cada hora. propriedades JSON Olá usados nesses exemplos são descritas nas seções após exemplos hello.

**Serviço vinculado para o Banco de Dados SQL do Azure:**

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```

**Serviço vinculado do Servidor de Arquivos Local:**

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

É recomendável usar Olá **encryptedCredential** propriedade em vez de usar o hello **userid** e **senha** propriedades. Confira [File System linked service](#linked-service-properties) (Serviço vinculado do Sistema de Arquivos) para obter detalhes sobre este serviço vinculado.

**Conjunto de dados de entrada do SQL Azure:**

exemplo Hello pressupõe que você criou uma tabela "MyTable" no SQL Azure, e ele contém uma coluna chamada "timestampcolumn" para os dados de série temporal.

Configuração ``“external”: ”true”`` informa a fábrica de dados Olá conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados hello.

```JSON
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

**Conjunto de dados de saída do sistema de arquivos local:**

Dados são copiados tooa novo arquivo a cada hora. Olá folderPath e fileName blob Olá são determinados com base na hora de início de saudação da fatia hello.

```JSON
{
  "name": "OnpremisesFileSystemOutput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
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
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

**Uma atividade de cópia em um pipeline com origem SQL e coletor de Sistema de Arquivos:**

Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora. Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**SqlSource**e hello **coletor** tipo está definido muito**FileSystemSink**. consulta SQL Olá especificado para Olá **SqlReaderQuery** propriedade seleciona dados Olá Olá após toocopy de hora.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T20:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoOnPremisesFile",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
          }
        ],
        "outputs": [
          {
            "name": "OnpremisesFileSystemOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "FileSystemSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 3,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```


Você também pode mapear colunas de origem toocolumns de conjunto de dados do conjunto de coletor de dados na definição de atividade de cópia de saudação. Para obter detalhes, confira [Mapear colunas de conjunto de dados no Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Desempenho e ajuste
 toolearn sobre a chave de fatores que afetam o desempenho de saudação de movimentação de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias maneiras, consulte Olá [atividade de cópia guia de desempenho e ajuste](data-factory-copy-activity-performance.md).
