---
title: aaaCopy dados para/do armazenamento de BLOBs do Azure | Microsoft Docs
description: 'Saiba como toocopy blob dados no Azure Data Factory. Usar nosso exemplo: como toocopy tooand de dados do armazenamento de BLOBs do Azure e banco de dados do SQL Azure.'
keywords: "dados de blob, cópia de blobs do azure"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: bec8160f-5e07-47e4-8ee1-ebb14cfb805d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 8428c64e8e8b1084b3f2f680c4e1819559e4ffa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooor-from-azure-blob-storage-using-azure-data-factory"></a>Copiar dados tooor do armazenamento de BLOBs do Azure usando o Azure Data Factory
Este artigo explica como toouse hello atividade de cópia no Azure Data Factory toocopy dados tooand do armazenamento de BLOBs do Azure. Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação.

## <a name="overview"></a>Visão geral
Você pode copiar dados de qualquer fonte com suporte de dados armazenam tooAzure armazenamento de Blob ou em dados de coletor do armazenamento de BLOBs do Azure tooany suporte para armazenam. Olá tabela a seguir fornece uma lista de repositórios de dados com suporte como fontes ou coletores pela atividade de cópia de saudação. Por exemplo, você pode mover dados **de** um banco de dados SQL Server ou um de banco de dados SQL do Azure **para** um armazenamento de blobs do Azure. Além disso, é possível copiar dados **de** um armazenamento de Blobs do Azure **para** um SQL Data Warehouse do Azure ou uma coleção do Azure Cosmos DB. 

## <a name="supported-scenarios"></a>Cenários com suporte
Você pode copiar dados **do armazenamento de BLOBs do Azure** toohello repositórios de dados a seguir:

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

Você pode copiar dados de saudação armazenamentos de dados a seguir **tooAzure armazenamento de Blob**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]
 
> [!IMPORTANT]
> Copiar atividade suporta copiando dados de / tooboth contas de armazenamento do Azure para fins gerais e Hot/interessantes armazenamento de Blob. Hello atividade dá suporte a **ler de bloco, acrescentar ou blobs de página**, mas oferece suporte a **gravando blobs de bloco tooonly**. Não há suporte para armazenamento Premium do Azure como um coletor porque ele é feito por blobs de página.
> 
> Atividade de cópia não exclui os dados de origem Olá depois Olá dados com êxito são copiado toohello destino. Se você precisar de dados de origem toodelete após uma cópia bem-sucedida, criar um [atividade personalizada](data-factory-use-custom-activities.md) toodelete Olá dados e usar a atividade de saudação no pipeline de saudação. Para obter um exemplo, consulte Olá [excluir exemplo de blob ou pasta no GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity). 

## <a name="get-started"></a>Introdução
Você pode criar um pipeline com uma atividade de cópia que mova dados de um armazenamento de Blobs do Azure usando ferramentas/APIs diferentes.

toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**. Este artigo possui uma [passo a passo](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) para criar dados de toocopy um pipeline de um local de armazenamento de BLOBs do Azure tooanother local de armazenamento de BLOBs do Azure. Para obter um tutorial sobre como criar dados de toocopy um pipeline de um banco de dados SQL do tooAzure de armazenamento de BLOBs do Azure, consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md).

Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**. Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.

Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:

1. Criar uma **data factory**. Um data factory pode conter um ou mais pipelines. 
2. Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica. Por exemplo, se você estiver copiando dados de um banco de dados de SQL do Azure de tooan do armazenamento de BLOBs do Azure, você criar duas toolink de serviços vinculados sua conta de armazenamento do Azure e a fábrica de dados de tooyour de banco de dados do SQL Azure. Para propriedades de serviço vinculado que específico tooAzure armazenamento de Blob, consulte [vinculado propriedades do serviço](#linked-service-properties) seção. 
2. Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello. O exemplo hello mencionado na última etapa do hello, você criará um contêiner de blob do conjunto de dados toospecify hello e a pasta que contém os dados de entrada hello. E, você cria outra tabela do conjunto de dados toospecify Olá SQL no banco de dados de SQL do Azure de saudação que contém dados Olá copiados saudação do armazenamento de blob. Para propriedades de conjunto de dados que são específico tooAzure armazenamento de Blob, consulte [propriedades de conjunto de dados](#dataset-properties) seção.
3. Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída. Exemplo hello mencionado anteriormente, você usar BlobSource como uma origem e do SqlSink como um coletor de atividade de cópia de saudação. Da mesma forma, se você estiver copiando de banco de dados do Azure SQL tooAzure armazenamento de Blob, use SqlSource e BlobSink na atividade de cópia de saudação. Para propriedades de atividade de cópia que específico tooAzure armazenamento de Blob, consulte [copiar as propriedades de atividade](#copy-activity-properties) seção. Para obter detalhes sobre como toouse um repositório de dados como uma origem ou um coletor, clique em Olá link na seção anterior de saudação para seu armazenamento de dados.  

Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você. Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.  Para obter exemplos com definições de JSON para entidades de fábrica de dados que são usados toocopy dados para/de um armazenamento de BLOBs do Azure, consulte [exemplos JSON](#json-examples-for-copying-data-to-and-from-blob-storage  ) deste artigo.

Olá seções a seguir fornece detalhes sobre as propriedades JSON que são usadas toodefine Data Factory entidades específica tooAzure armazenamento de Blob.

## <a name="linked-service-properties"></a>Propriedades do serviço vinculado
Há dois tipos de serviços vinculados, você pode usar toolink uma fábrica de dados do Azure de tooan de armazenamento do Azure. São eles: o serviço vinculado **AzureStorage** e o serviço vinculado **AzureStorageSas**. Olá serviço vinculado do armazenamento do Azure fornece a fábrica de dados Olá com acesso global toohello armazenamento do Azure. Enquanto o hello Azure armazenamento SAS (assinatura de acesso compartilhado) vinculado serviço fornece a fábrica de dados Olá com acesso restrito/tempo-limite toohello armazenamento do Azure. Não há outras diferenças entre esses dois serviços vinculados. Escolha o serviço de saudação vinculado que atenda às suas necessidades. Olá seções a seguir fornecem mais detalhes sobre esses dois serviços vinculados.

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a>Propriedades do conjunto de dados
toospecify toorepresent um conjunto de dados dados de entrada ou saídos em um armazenamento de BLOBs do Azure, defina propriedade de tipo de saudação do conjunto de dados Olá para: **AzureBlob**. Saudação de conjunto **linkedServiceName** serviço vinculado de propriedade de nome de toohello Olá dataset de saudação armazenamento do Azure ou SAS de armazenamento do Azure.  Propriedades de tipo de saudação do conjunto de dados Olá especificam Olá **contêiner de blob** e hello **pasta** no armazenamento de blob hello.

Para obter uma lista completa de seções JSON e propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo. As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).

Fábrica de dados oferece suporte a saudação seguindo os valores de tipo compatível com CLS .NET com base para fornecer informações de tipo em "structure" para fontes de dados de esquema na leitura como BLOBs do Azure: Int16, Int32, Int64, Single, Double, Decimal, Byte [], Bool, String, Guid, Datetime, DateTimeOffset, Timespan. Fábrica de dados executa automaticamente conversões de tipo ao mover o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados.

Olá **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre local hello, etc., formato de dados Olá no repositório de dados de saudação. Olá typeProperties seção de conjunto de dados do tipo **AzureBlob** conjunto de dados tiver Olá propriedades a seguir:

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| folderPath |Contêiner de toohello do caminho e a pasta no armazenamento de blob hello. Exemplo: myblobcontainer\myblobfolder\ |Sim |
| fileName |Nome do blob hello. fileName é opcional e diferencia maiúsculas de minúsculas.<br/><br/>Se você especificar um nome de arquivo, hello atividade (incluindo cópia) funciona em Olá Blob específico.<br/><br/>Quando o nome de arquivo não for especificado, cópia inclui todos os Blobs no folderPath Olá para o conjunto de dados de entrada.<br/><br/>Quando **fileName** não for especificado para um conjunto de dados de saída e **preserveHierarchy** não for especificado no coletor de atividade, nome de saudação do arquivo hello gerado estaria em Olá seguindo este formato: dados.<Guid>. txt (por exemplo:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Não |
| partitionedBy |partitionedBy é uma propriedade opcional. Você pode usar-ele toospecify um dinâmico folderPath e filename para dados de série temporal. Por exemplo, folderPath pode ser parametrizado para cada hora dos dados. Consulte Olá [usando a seção de propriedade partitionedBy](#using-partitionedBy-property) para obter detalhes e exemplos. |Não |
| formato | Olá, tipos de formato a seguir têm suporte: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Saudação de conjunto **tipo** propriedade em formato tooone desses valores. Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Se você quiser muito**copiar arquivos como-é** entre repositórios baseada em arquivo (cópia binário), ignore a seção de formato de saudação em ambas as definições de conjunto de dados de entrada e saída. |Não |
| compactação | Especifica tipo de saudação e nível de compactação de dados de saudação. Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**. Os níveis com suporte são **Ideal** e **O mais rápido**. Para saber mais, confira [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support) (Formatos de arquivo e de compactação no Azure Data Factory). |Não |

### <a name="using-partitionedby-property"></a>Usando a propriedade partitionedBy
Como mencionado na seção anterior hello, você pode especificar um dinâmico folderPath e filename para dados de série temporal com hello **partitionedBy** propriedade [funções da fábrica de dados e variáveis de sistema Olá](data-factory-functions-variables.md).

Para saber mais sobre conjuntos de dados de série temporal, agendamento e fatias, veja os artigos [Criando conjuntos de dados](data-factory-create-datasets.md) e [Agendamento e execução](data-factory-scheduling-and-execution.md).

#### <a name="sample-1"></a>Exemplo 1

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

Neste exemplo, {Slice} é substituído pelo valor de saudação da variável de sistema SliceStart fábrica de dados no formato de saudação (AAAAMMDDHH) especificado. Olá SliceStart refere-se toostart tempo da fração de saudação. Olá folderPath é diferente para cada fatia. Por exemplo: wikidatagateway/wikisampledataout/2014100103 ou wikidatagateway/wikisampledataout/2014100104

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

Neste exemplo, ano, mês, dia e hora do SliceStart são extraídos em variáveis separadas que são usadas pelas propriedades folderPath e fileName.

## <a name="copy-activity-properties"></a>Propriedades da atividade de cópia
Para obter uma lista completa das seções e propriedades disponíveis para a definição de atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo. As propriedades, como nome, descrição, conjuntos de dados de entrada e saída, e políticas, estão disponíveis para todos os tipos de atividade. Por outro lado, as propriedades disponíveis no hello **typeProperties** seção de atividade Olá variam de acordo com cada tipo de atividade. Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores. Se você estiver movendo dados de um armazenamento de BLOBs do Azure, você defina o tipo de fonte de saudação na atividade de cópia de saudação muito**BlobSource**. Da mesma forma, se você estiver movendo dados tooan armazenamento de BLOBs do Azure, você definir o tipo de coletor Olá na atividade de cópia de saudação muito**BlobSink**. Esta seção fornece uma lista das propriedades compatíveis com BlobSource e BlobSink.

**BlobSource** dá suporte a saudação seguintes propriedades em Olá **typeProperties** seção:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| recursiva |Indica se os dados saudação é lida recursivamente de subpastas de saudação ou somente de pasta especificado hello. |True (valor padrão), False |Não |

**BlobSink** dá suporte a saudação seguintes propriedades **typeProperties** seção:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| copyBehavior |Define o comportamento de cópia de saudação quando origem Olá é BlobSource ou sistema de arquivos. |<b>PreserveHierarchy</b>: preserva Olá hierarquia de arquivos na pasta de destino de saudação. caminho relativo do Hello arquivo toosource da pasta de origem é idêntico toohello o caminho relativo da pasta de tootarget do arquivo de destino.<br/><br/><b>FlattenHierarchy</b>: todos os arquivos da pasta de origem Olá estão em Olá primeiro níveis da pasta de destino. os arquivos de destino de saudação têm nome gerado automaticamente. <br/><br/><b>MergeFiles</b>: mescla todos os arquivos Olá pasta tooone do arquivo de origem. Se Olá nome de arquivo/Blob for especificado, o nome de arquivo mesclado de Olá seria nome especificado do hello. Caso contrário, seriam nome de arquivo gerado automaticamente. |Não |

**BlobSource** também oferece suporte a essas duas propriedades para compatibilidade com versões anteriores.

* **treatEmptyAsNull**: Especifica se tootreat uma cadeia nula ou vazia como valor nulo.
* **skipHeaderLineCount** - Especifica quantas linhas precisam ser ignoradas. É aplicável somente quando o conjunto de dados de entrada usa TextFormat.

Da mesma forma, **BlobSink** dá suporte a saudação de propriedade para compatibilidade com versões anteriores a seguir.

* **blobWriterAddHeader**: Especifica se tooadd um cabeçalho de definições de coluna ao gravar tooan gerar conjunto de dados.

Saudação de suporte agora de conjuntos de dados seguintes propriedades que implementam Olá a mesma funcionalidade: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.

Olá tabela a seguir fornece orientação sobre como usar as novas propriedades de conjunto de dados Olá no lugar dessas propriedades de fonte/coletor do blob.

| Propriedade de Atividade de Cópia | Propriedade de Conjunto de Dados |
|:--- |:--- |
| skipHeaderLineCount em BlobSource |skipLineCount e firstRowAsHeader. Linhas são ignoradas primeiro e, em seguida, a primeira linha de saudação é lido como um cabeçalho. |
| treatEmptyAsNull em BlobSource |treatEmptyAsNull no conjunto de dados de entrada |
| blobWriterAddHeader em BlobSink |firstRowAsHeader no conjunto de dados de saída |

Confira a seção [Especificar TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) para obter informações detalhadas sobre essas propriedades.    

### <a name="recursive-and-copybehavior-examples"></a>exemplos de recursive e copyBehavior
Esta seção descreve o comportamento resultante de saudação da operação de cópia de saudação para diferentes combinações de valores recursiva e copyBehavior.

| recursiva | copyBehavior | Comportamento resultante |
| --- | --- | --- |
| verdadeiro |preserveHierarchy |Para uma pasta de origem Pasta1 com hello estrutura a seguir: <br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5<br/><br/>pasta de destino de Olá Pasta1 é criada com hello mesma estrutura como fonte de saudação<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5. |
| verdadeiro |flattenHierarchy |Para uma pasta de origem Pasta1 com hello estrutura a seguir: <br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5<br/><br/>destino de saudação Pasta1 é criado com hello estrutura a seguir: <br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nome gerado automaticamente para o Arquivo1<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo2<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo3<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo4<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo5 |
| verdadeiro |mergeFiles |Para uma pasta de origem Pasta1 com hello estrutura a seguir: <br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5<br/><br/>destino de saudação Pasta1 é criado com hello estrutura a seguir: <br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Os conteúdos dos Arquivo1 + Arquivo2 + Arquivo3 + Arquivo4 + Arquivo5 são mesclados em um único arquivo com um nome de arquivo gerado automaticamente |
| false |preserveHierarchy |Para uma pasta de origem Pasta1 com hello estrutura a seguir: <br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5<br/><br/>pasta de destino de saudação Pasta1 é criada com hello estrutura a seguir<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2<br/><br/><br/>Subpasta1 com Arquivo3, Arquivo4 e Arquivo5 não são selecionados. |
| false |flattenHierarchy |Para uma pasta de origem Pasta1 com hello estrutura a seguir:<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5<br/><br/>pasta de destino de saudação Pasta1 é criada com hello estrutura a seguir<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nome gerado automaticamente para o Arquivo1<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo2<br/><br/><br/>Subpasta1 com Arquivo3, Arquivo4 e Arquivo5 não são selecionados. |
| false |mergeFiles |Para uma pasta de origem Pasta1 com hello estrutura a seguir:<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5<br/><br/>pasta de destino de saudação Pasta1 é criada com hello estrutura a seguir<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Os conteúdos dos Arquivo1 + Arquivo2 são mesclados em um único arquivo com um nome de arquivo gerado automaticamente. Nome gerado automaticamente para o Arquivo1<br/><br/>Subpasta1 com Arquivo3, Arquivo4 e Arquivo5 não são selecionados. |

## <a name="walkthrough-use-copy-wizard-toocopy-data-tofrom-blob-storage"></a>Passo a passo: Dados de toocopy usar o Assistente para cópia para/do armazenamento de Blob
Vamos examinar como o armazenamento de blob tooquickly copiar dados de um Azure. Neste passo a passo, os armazenamentos de dados de origem e de destino do tipo: Armazenamento de Blobs do Azure. Olá pipeline neste passo a passo copia dados de uma pasta tooanother pasta Olá mesmo contêiner de blob. Este passo a passo é intencionalmente simple tooshow configurações ou propriedades ao usar o armazenamento de Blob como uma fonte ou coletor. 

### <a name="prerequisites"></a>Pré-requisitos
1. Crie uma **Conta de Armazenamento do Azure** de uso geral caso não tenha uma. Usar o armazenamento de blob de Olá como ambas **fonte** e **destino** repositório de dados neste passo a passo. Se você não tiver uma conta de armazenamento do Azure, consulte Olá [criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) artigo para toocreate etapas um.
2. Criar um contêiner de blob denominado **adfblobconnector** na conta de armazenamento hello. 
4. Crie uma pasta chamada **entrada** em Olá **adfblobconnector** contêiner.
5. Crie um arquivo chamado **emp.txt** com hello a seguir de conteúdo e carregá-lo toohello **entrada** pasta usando ferramentas como [Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/)
    ```json
    John, Doe
    Jane, Doe
    ```
### <a name="create-hello-data-factory"></a>Criar hello fábrica de dados
1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Clique em **+ novo** no canto superior esquerdo de saudação, clique em **Intelligence + análise**e clique em **Data Factory**.
3. Em Olá **nova fábrica de dados** folha:   
    1. Digite **ADFBlobConnectorDF** para Olá **nome**. nome de Olá Olá do Azure da fábrica de dados deve ser globalmente exclusivo. Se você receber o erro Olá: `*Data factory name “ADFBlobConnectorDF” is not available`, altere o nome de Olá Olá da fábrica de dados (por exemplo, yournameADFBlobConnectorDF) e tente criar novamente. Consulte o tópico [Data Factory - regras de nomenclatura](data-factory-naming-rules.md) para ver as regras de nomenclatura para artefatos de Data Factory.
    2. Selecione sua **assinatura**do Azure.
    3. Para o grupo de recursos, selecione **usar existente** tooselect um existente recurso grupo (ou) selecione **criar novo** tooenter um nome para um grupo de recursos.
    4. Selecione um **local** Olá fábrica de dados.
    5. Selecione **toodashboard Pin** caixa de seleção na parte inferior da saudação da folha de saudação.
    6. Clique em **Criar**.
3. Após a conclusão da criação de saudação, você ver Olá **Data Factory** folha conforme Olá a imagem a seguir: ![homepage de fábrica de dados](./media/data-factory-azure-blob-connector/data-factory-home-page.png)

### <a name="copy-wizard"></a>Assistente de Cópia
1. Na home page do hello fábrica de dados, clique em Olá **copiar dados [visualização]** bloco toolaunch **o Assistente para cópia de dados** em uma guia separada.    
    
    > [!NOTE]
    >    Se você vir esse navegador da web hello está preso em "Autorizar...", desabilitar/desmarque **bloquear cookies de terceiros e dados do site** configuração (ou) manter habilitado e criar uma exceção para **login.microsoftonline.com**e tente iniciar o Assistente de saudação novamente.
2. Em Olá **propriedades** página:
    1. Insira **CopyPipeline** para **Nome da tarefa**. nome de tarefa Olá é saudação do pipeline de saudação em sua fábrica de dados.
    2. Insira um **descrição** para tarefas de saudação (opcional).
    3. Para **cadência de tarefa ou o Agendador de tarefas**, lembre-Olá **executado regularmente em agenda** opção. Se você desejar toorun essa tarefa somente uma vez, em vez de executar repetidamente em um agendamento, selecione **executar uma vez agora**. Se você selecionar a opção **Executar uma vez agora**, um [pipeline avulso](data-factory-create-pipelines.md#onetime-pipeline) será criado. 
    4. Manter configurações de saudação para **padrão recorrente**. Essa tarefa é executada diariamente entre hello começar e terminar vezes você especificar na próxima etapa de saudação.
    5. Saudação de alteração **data/hora inicial** muito**21/04/2017**. 
    6. Saudação de alteração **data hora de término** muito**25/04/2017**. Talvez você queira data de saudação tootype em vez de navegar por meio de calendário hello.     
    8. Clique em **Avançar**.
      ![Ferramenta de Cópia – Página Propriedades](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png) 
3. Em Olá **repositório de dados de origem** , clique em **armazenamento de BLOBs do Azure** lado a lado. Você pode usar esse repositório de dados de origem do página toospecify Olá para tarefas de cópia de saudação. Você pode usar um serviço de repositório de dados vinculado existente ou especificar um novo repositório de dados. serviço vinculado de toouse existente, selecione **de existente serviços vinculados** e selecione Olá serviço vinculado à direita. 
    ![Ferramenta de Cópia – Página do armazenamento de dados de origem](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)
4. Em Olá **especificar conta de armazenamento de BLOBs do Azure Olá** página:
   1. Manter o nome gerado automaticamente para Olá **nome de Conexão**. nome da conexão de saudação é o nome de saudação do serviço vinculado de saudação do tipo: o armazenamento do Azure. 
   2. Confirme se a opção **De assinaturas do Azure** foi selecionada em **Método de seleção de conta**.
   3. Selecione sua assinatura do Azure ou mantenha **Selecionar tudo** para **Assinatura do Azure**.   
   4. Selecione um **conta de armazenamento do Azure** de saudação lista de armazenamento do Azure contas disponível na assinatura de saudação selecionada. Você também pode escolher tooenter configurações de conta de armazenamento manualmente selecionando **inserir manualmente** opção Olá **método de seleção de conta**.
   5. Clique em **Avançar**. 
      ![Copie a ferramenta - especificar conta de armazenamento de BLOBs do Azure Olá](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)
5. Em **pasta ou escolha o arquivo de entrada hello** página:
   1. Clique duas vezes em **adfblobcontainer**.
   2. Selecione **input** e clique em **Escolher**. Neste passo a passo, você deve selecionar pasta de entrada hello. Também é possível selecionar arquivo de emp.txt Olá na pasta Olá em vez disso. 
      ![Copie a ferramenta - escolha a pasta ou arquivo de entrada hello](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)
6. Em Olá **pasta ou escolha o arquivo de entrada hello** página:
    1. Confirme que Olá **arquivo ou pasta** está definido muito**adfblobconnector/entrada**. Se os arquivos de saudação em subpastas, por exemplo, 01/04/2017 2017/04/02 e assim por diante, insira adfblobconnector/entrada / {year} / {month} / {day} para o arquivo ou pasta. Quando você pressionar TAB fora da caixa de texto de saudação, você verá três formatos de tooselect listas suspensas para year (AAAA), month (MM) e dia (dd). 
    2. Não defina a opção **Copiar arquivo recursivamente**. Selecione completa de toorecursively essa opção através de pastas para arquivos toobe toohello copiado destino. 
    3. Olá não **cópia binária** opção. Selecione essa opção tooperform uma cópia do binária do destino de toohello do arquivo de origem. Não selecione para este passo a passo para que você possa ver mais opções na página seguinte hello. 
    4. Confirme que Olá **tipo de compactação** está definido muito**nenhum**. Selecione um valor para essa opção se os arquivos de origem são compactados em um dos formatos de saudação com suporte. 
    5. Clique em **Avançar**.
    ![Copie a ferramenta - escolha a pasta ou arquivo de entrada hello](./media/data-factory-azure-blob-connector/chose-input-file-folder.png) 
7. Em Olá **as configurações de formato de arquivo** página, consulte delimitadores hello e esquema de saudação que é detectada automaticamente pelo Assistente de saudação Analisando arquivo hello. 
    1. Confirmar Olá as opções a seguir: um. Olá **formato de arquivo** está definido muito**formato de texto**. Você pode ver todos os formatos de saudação com suporte na lista suspensa de saudação. Por exemplo: JSON, Avro, ORC, Parquet.
        b. Olá **delimitador de coluna** está definido muito`Comma (,)`. Você pode ver Olá outros delimitadores de coluna que tem suportados pela fábrica de dados na lista suspensa de saudação. Você também pode especificar um delimitador personalizado.
        c. Olá **delimitador de linha** está definido muito`Carriage Return + Line feed (\r\n)`. Você pode ver Olá outros delimitadores de linha com suporte pela fábrica de dados na lista suspensa de saudação. Você também pode especificar um delimitador personalizado.
        d. Olá **Ignorar contagem de linhas** está definido muito**0**. Se você quiser alguns toobe de linhas ignorado na parte superior de saudação do arquivo hello, insira o número de saudação aqui.
        e.  Olá **primeira linha de dados contém nomes de coluna** não está definido. Se os arquivos de origem de saudação contêm nomes de coluna na primeira linha de saudação, selecione essa opção.
        f. Olá **tratar o valor de coluna vazia como null** opção é definida.
    2. Expanda **configurações avançadas** toosee avançado opção disponível.
    3. Final Olá Olá página, consulte Olá **visualização** de dados de arquivo de emp.txt hello.
    4. Clique em **esquema** guia esquema de Olá Olá inferior toosee esse assistente para cópia de saudação inferido observando Olá dados no arquivo de origem de saudação.
    5. Clique em **próximo** Após examinar delimitadores hello e visualizar dados.
    ![Ferramenta de Cópia – Configurações de formato de arquivo](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)  
8. Em Olá **página de repositório de dados de destino**, selecione **armazenamento de BLOBs do Azure**e clique em **próximo**. Você está usando Olá armazenamento de BLOBs do Azure como os dois Olá origem e destino armazenamentos de dados neste passo a passo.    
    ![Ferramenta de Cópia – selecionar o armazenamento de dados de destino](media/data-factory-azure-blob-connector/select-destination-data-store.png)
9. Em **especificar conta de armazenamento de BLOBs do Azure Olá** página:
   1. Digite **AzureStorageLinkedService** para Olá **nome de Conexão** campo.
   2. Confirme se a opção **De assinaturas do Azure** foi selecionada em **Método de seleção de conta**.
   3. Selecione sua **assinatura**do Azure.  
   4. Selecione sua conta de armazenamento do Azure. 
   5. Clique em **Avançar**.     
10. Em Olá **Olá Escolher arquivo ou pasta de saída** página: 
    6. especifique **Caminho da pasta** como **adfblobconnector/output/{year}/{month}/{day}**. Insira **GUIA**.
    7. Para Olá **ano**, selecione **aaaa**.
    8. Para Olá **mês**, confirme se ele está definido muito**MM**.
    9. Para Olá **dia**, confirme se ele está definido muito**dd**.
    10. Confirme que Olá **tipo de compactação** está definido muito**nenhum**.
    11. Confirme que Olá **Copiar comportamento** está definido muito**mesclar arquivos**. Se Olá saída arquivo com hello mesmo nome já existir, hello novo conteúdo é adicionado toohello mesmo arquivo final hello.
    12. Clique em **Avançar**.
    ![Ferramenta de Cópia – Escolher o arquivo ou a pasta de saída](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)
11. Em Olá **as configurações de formato de arquivo** , examine as configurações de saudação e, em **próximo**. Uma das opções adicionais Olá aqui é tooadd um arquivo de saída de toohello de cabeçalho. Se você selecionar essa opção, uma linha de cabeçalho é adicionada com nomes de colunas de saudação do esquema de saudação da fonte de saudação. Você pode renomear nomes de coluna padrão Olá ao exibir o esquema de saudação para fonte de saudação. Por exemplo, você pode alterar Olá tooFirst primeiro da coluna Nome e tooLast da segunda coluna nome. Em seguida, o arquivo de saída Olá é gerado com um cabeçalho com esses nomes como nomes de coluna. 
    ![Ferramenta de Cópia – Configurações de formato de arquivo para o destino](media/data-factory-azure-blob-connector/file-format-destination.png)
12. Em Olá **as configurações de desempenho** , confirme que **unidades em nuvem** e **paralelo cópias** são definidos de forma muito**automática**e clique em Avançar. Para obter detalhes sobre essas configurações, consulte [Guia de desempenho e ajuste da atividade de cópia](data-factory-copy-activity-performance.md#parallel-copy).
    ![Ferramenta de Cópia – Configurações de desempenho](media/data-factory-azure-blob-connector/copy-performance-settings.png) 
14. Em Olá **resumo** página, examine todas as configurações (Propriedades da tarefa, as configurações de origem e de destino e as configurações de cópias) e clique em **próximo**.
    ![Ferramenta de Cópia – Página Resumo](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)
15. Revise informações Olá **resumo** página e, em seguida, clique em **concluir**. Assistente de saudação cria um pipeline, dois conjuntos de dados (de entrada e saída) e dois serviços vinculados na fábrica de dados de saudação (a partir de onde você iniciou Olá Assistente para copiar).
    ![Ferramenta de Cópia – Página Implantação](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)

### <a name="monitor-hello-pipeline-copy-task"></a>Pipeline de saudação do Monitor (tarefas de cópia)

1. Clique em link Olá `Click here toomonitor copy pipeline` em Olá **implantação** página. 
2. Você deve ver Olá **monitorar e gerenciar aplicativos** em uma guia separada.  ![Aplicativo Monitorar e Gerenciar](media/data-factory-azure-blob-connector/monitor-manage-app.png)
3. Saudação de alteração **iniciar** de tempo na parte superior da saudação muito`04/19/2017` e **final** muito tempo`04/27/2017`e, em seguida, clique em **aplicar**. 
4. Você deve ver cinco janelas de atividade no hello **atividade WINDOWS** lista. Olá **WindowStart** vezes devem abranger todos os dias de horas de término de toopipeline de início do pipeline. 
5. Clique em **atualizar** botão para Olá **atividade WINDOWS** lista algumas vezes até que você veja o status de saudação de todos os períodos de atividade de saudação é definida tooReady. 
6. Agora, verifique se que os arquivos de saída de hello são gerados na pasta de saída de saudação do contêiner adfblobconnector. Você deve ver Olá estrutura de pastas na pasta de saída de hello a seguir: 
    ```
    2017/04/21
    2017/04/22
    2017/04/23
    2017/04/24
    2017/04/25    
    ```
Para obter informações detalhadas sobre como monitorar e gerenciar data factories, consulte o artigo [Monitorar e gerenciar o pipeline do Data Factory](data-factory-monitor-manage-app.md). 
 
### <a name="data-factory-entities"></a>Entidades de Data Factory
Agora, alterne toohello back guia com hello Data Factory home page. Observe que agora há dois serviços vinculados, dois conjuntos de dados e um pipeline no data factory. 

![Home page do Data Factory com entidades](media/data-factory-azure-blob-connector/data-factory-home-page-with-numbers.png)

Clique em **criar e implantar** toolaunch Editor da fábrica de dados. 

![Editor Data Factory](media/data-factory-azure-blob-connector/data-factory-editor.png)

Você deve ver Olá entidades da fábrica de dados em sua fábrica de dados a seguir: 

 - Dois serviços vinculados. Um para origem hello e Olá outro destino hello. Ambos os serviços vinculado de saudação consulte toohello mesma conta de armazenamento do Azure neste passo a passo. 
 - Dois conjuntos de dados. Um conjunto de dados de entrada e um conjunto de dados de saída. Neste passo a passo, ambos usam Olá mesmo contêiner de blob, mas consulte toodifferent pastas (entrada e saída).
 - Um pipeline. pipeline de saudação contém uma atividade de cópia que usa um blob de origem e um blob coletor toocopy os dados de um local de blob do Azure tooanother local de blob do Azure. 

Olá seções a seguir fornecem mais informações sobre essas entidades. 

#### <a name="linked-services"></a>Serviços vinculados
Você deverá ver dois serviços vinculados. Um para origem hello e Olá outro destino hello. Neste passo a passo, ambas as definições de aparência Olá mesmo, exceto para nomes de saudação. Olá **tipo** Olá serviço vinculado está definido muito**AzureStorage**. Propriedade mais importante da definição de serviço vinculada de saudação é hello **connectionString**, que é usada pela fábrica de dados tooconnect tooyour conta de armazenamento do Azure em tempo de execução. Ignore a propriedade de hubName Olá na definição de saudação. 

##### <a name="source-blob-storage-linked-service"></a>Serviço vinculado do armazenamento de blobs do Azure
```json
{
    "name": "Source-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

##### <a name="destination-blob-storage-linked-service"></a>Serviço vinculado do armazenamento de blobs de destino

```json
{
    "name": "Destination-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

Para obter mais informações sobre o serviço vinculado do Armazenamento do Azure, consulte a seção [Propriedades do serviço vinculado](#linked-service-properties). 

#### <a name="datasets"></a>Conjunto de dados
Há dois conjuntos de dados: um conjunto de dados de entrada e um conjunto de dados de saída. tipo de saudação do conjunto de dados hello está definido muito**AzureBlob** para ambos. 

conjunto de dados de entrada Hello pontos toohello **entrada** pasta da saudação **adfblobconnector** contêiner de blob. Olá **externo** propriedade for definida muito**true** para este conjunto de dados como Olá dados não são produzidos pelo pipeline de saudação com atividade de cópia de saudação que usa esse conjunto de dados como entrada. 

Olá toohello de pontos de conjunto de dados de saída **saída** pasta da saudação mesmo contêiner de blob. Olá conjunto de dados de saída também usa Olá ano, mês e dia da saudação **SliceStart** toodynamically de variável de sistema avaliar caminho Olá Olá arquivo de saída. Para obter uma lista de funções e variáveis de sistema com suporte no Data Factory, consulte [Funções e variáveis de sistema do Data Factory](data-factory-functions-variables.md). Olá **externo** propriedade for definida muito**false** (valor padrão) porque este conjunto de dados é produzido pelo pipeline de saudação. 

Para obter mais informações sobre as propriedades com suporte no conjunto de dados de Blobs do Azure, consulte a seção [Propriedades do conjunto de dados](#dataset-properties).

##### <a name="input-dataset"></a>Conjunto de dados de entrada

```json
{
    "name": "InputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Source-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/input/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

##### <a name="output-dataset"></a>Conjunto de dados de saída

```json
{
    "name": "OutputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Destination-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/output/{year}/{month}/{day}",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            },
            "partitionedBy": [
                { "name": "year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } }
            ]
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

#### <a name="pipeline"></a>Pipeline
pipeline de saudação tem apenas uma atividade. Olá **tipo** hello atividade está definida muito**cópia**.  Propriedades do tipo hello atividade hello, há duas seções, uma para origem e hello outro para o coletor. tipo de origem de saudação é definido muito**BlobSource** como atividade hello está copiando dados de um armazenamento de blob. Olá tipo de coletor é definido muito**BlobSink** como atividade Olá copiando o armazenamento de blob de tooa de dados. atividade de cópia de saudação usa InputDataset z4y como entrada hello e OutputDataset-z4y como saída de hello. 

Para obter mais informações sobre as propriedades com suporte na BlobSource e no BlobSink, consulte a seção [Propriedades da atividade de cópia](#copy-activity-properties). 

```json
{
    "name": "CopyPipeline",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "MergeFiles",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-z4y"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-z4y"
                    }
                ],
                "policy": {
                    "timeout": "1.00:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "style": "StartOfInterval",
                    "retry": 3,
                    "longRetry": 0,
                    "longRetryInterval": "00:00:00"
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "Activity-0-Blob path_ adfblobconnector_input_->OutputDataset-z4y"
            }
        ],
        "start": "2017-04-21T22:34:00Z",
        "end": "2017-04-25T05:00:00Z",
        "isPaused": false,
        "pipelineMode": "Scheduled"
    }
}
```

## <a name="json-examples-for-copying-data-tooand-from-blob-storage"></a>Exemplos JSON para copiar dados tooand do armazenamento de Blob  
Olá, exemplos a seguir fornecem as definições de JSON de exemplo que você pode usar toocreate um pipeline usando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Eles mostram como toocopy tooand de dados do armazenamento de BLOBs do Azure e banco de dados do SQL Azure. No entanto, os dados podem ser copiados **diretamente** de qualquer uma das fontes tooany de Coletores Olá mencionado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.

### <a name="json-example-copy-data-from-blob-storage-toosql-database"></a>Exemplo JSON: Copiar dados de armazenamento de Blob tooSQL banco de dados
Olá mostra de exemplo a seguir:

1. Um serviço vinculado do tipo [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).
2. Um serviço vinculado do tipo [AzureStorage](#linked-service-properties).
3. Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureBlob](#dataset-properties).
4. Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).
5. Um [pipeline](data-factory-create-pipelines.md) com Atividade de cópia que usa [BlobSource](#copy-activity-properties) e [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).

exemplo Hello copia dados de série de tempo de uma tabela do SQL Azure tooan BLOBs do Azure por hora. propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.

**Serviço vinculado do SQL Azure:**

```json
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
**Serviço vinculado de armazenamento do Azure:**

```json
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
O Azure Data Factory dá suporte a dois tipos de serviços vinculados do Armazenamento do Azure: **AzureStorage** e **AzureStorageSas**. Para Olá primeiro, você especificar a cadeia de caracteres de conexão de saudação que inclui a chave da conta hello e hello mais recente, você especificar Olá Uri de assinatura de acesso compartilhado (SAS). Confira a seção [Serviços vinculados](#linked-service-properties) para obter detalhes.  

**Conjunto de dados de entrada de Blob do Azure:**

Os dados são coletados de um novo blob a cada hora (frequência: hora, intervalo: 1). Olá pasta caminho e nome de arquivo para blob Olá são avaliados dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada. caminho da pasta Olá usa year, month e parte do dia da hora de início da saudação e nome do arquivo usa a parte de hora Olá Olá da hora de início. "externo": "verdadeira" configuração informa fábrica de dados tabela Olá toohello externo fábrica de dados e não é produzida por uma atividade na fábrica de dados hello.

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
      }
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
**Conjunto de dados de saída do SQL Azure:**

exemplo Hello copiará a tabela de tooa de dados denominada "MyTable" em um banco de dados do SQL Azure. Criar tabela de saudação do banco de dados SQL do Azure com hello mesmo número de colunas, conforme o esperado toocontain de arquivo CSV de Blob hello. Novas linhas são adicionadas a tabela de toohello a cada hora.

```json
{
  "name": "AzureSqlOutput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
**Uma atividade de cópia em um pipeline com origem de Blob e coletor SQL:**

Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora. Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**BlobSource** e **coletor** tipo está definido muito**SqlSink**.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink"
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
### <a name="json-example-copy-data-from-azure-sql-tooazure-blob"></a>Exemplo JSON: Copiar dados do SQL Azure tooAzure Blob
Olá mostra de exemplo a seguir:

1. Um serviço vinculado do tipo [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).
2. Um serviço vinculado do tipo [AzureStorage](#linked-service-properties).
3. Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).
4. Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](#dataset-properties).
5. Um [pipeline](data-factory-create-pipelines.md) com Atividade de Cópia que usa [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) e [BlobSink](#copy-activity-properties).

exemplo Hello copia dados de série temporal de um tooan de tabela do SQL Azure BLOBs do Azure por hora. propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.

**Serviço vinculado do SQL Azure:**

```json
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
**Serviço vinculado de armazenamento do Azure:**

```json
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
O Azure Data Factory dá suporte a dois tipos de serviços vinculados do Armazenamento do Azure: **AzureStorage** e **AzureStorageSas**. Para Olá primeiro, você especificar a cadeia de caracteres de conexão de saudação que inclui a chave da conta hello e hello mais recente, você especificar Olá Uri de assinatura de acesso compartilhado (SAS). Confira a seção [Serviços vinculados](#linked-service-properties) para obter detalhes.  

**Conjunto de dados de entrada do SQL Azure:**

exemplo Hello supõe que você criou uma tabela "MyTable" no SQL Azure e contém uma coluna chamada "timestampcolumn" para dados de série temporal.

Definindo "externo": "verdadeiro" informa o serviço de fábrica de dados tabela Olá toohello externo fábrica de dados e não é produzida por uma atividade na fábrica de dados hello.

```json
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

**Conjunto de dados de saída de Blob do Azure:**

Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1). caminho da pasta Olá blob Olá é avaliado dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada. caminho da pasta Olá usa partes de ano, mês, dia e horário da hora de início da saudação.

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}/",
      "partitionedBy": [
        {
          "name": "Year",
          "value": { "type": "DateTime",  "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
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

**Uma atividade de cópia em um pipeline com origem SQL e coletor de Blob:**

Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora. Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**SqlSource** e **coletor** tipo está definido muito**BlobSink**. consulta SQL Olá especificada para Olá **SqlReaderQuery** propriedade seleciona dados Olá Olá após toocopy de hora.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureSQLtoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureSQLInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureBlobOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "SqlSource",
                        "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
