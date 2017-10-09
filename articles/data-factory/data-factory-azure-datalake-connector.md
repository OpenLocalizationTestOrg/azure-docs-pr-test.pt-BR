---
title: "aaaCopy tooand de dados do repositório Azure Data Lake | Microsoft Docs"
description: "Saiba como toocopy tooand de dados do repositório Data Lake por meio do Azure Data Factory"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 25b1ff3c-b2fd-48e5-b759-bb2112122e30
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 2e78f75f3821738332dacf70f6bf2c16f0136408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-data-lake-store-by-using-data-factory"></a>Copiar dados tooand do repositório Data Lake usando a fábrica de dados
Este artigo explica como toouse atividade de cópia no Azure Data Factory toomove dados tooand do repositório Azure Data Lake. Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) do artigo, uma visão geral de movimentação de dados com a atividade de cópia.

## <a name="supported-scenarios"></a>Cenários com suporte
Você pode copiar dados **do repositório Azure Data Lake** toohello repositórios de dados a seguir:

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

Você pode copiar dados de saudação armazenamentos de dados a seguir **tooAzure repositório Data Lake**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> Crie uma conta do Data Lake Store antes de criar um pipeline com a Atividade de Cópia. Para obter mais informações, consulte [Introdução ao Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).

## <a name="supported-authentication-types"></a>Tipos de autenticação com suporte
conector do repositório Data Lake Olá dá suporte a esses tipos de autenticação:
* Autenticação de entidade de serviço
* Autenticação de credencial do usuário (OAuth) 

É recomendável que você use a autenticação de entidade de serviço, especialmente para uma cópia de dados agendada. O comportamento de expiração do token pode ocorrer com autenticação de credenciais do usuário. Para obter detalhes de configuração, consulte Olá [vinculado propriedades do serviço](#linked-service-properties) seção.

## <a name="get-started"></a>Introdução
Você pode criar um pipeline com uma atividade de cópia que mova dados bidirecionalmente em um Azure Data Lake Store usando diferentes ferramentas/APIs.

toocreate de maneira mais fácil de saudação dados de toocopy um pipeline é Olá toouse **Assistente para cópia de**. Para obter um tutorial sobre como criar um pipeline usando o Assistente para cópia de saudação, consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md).

Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**. Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.

Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:

1. Criar uma **data factory**. Um data factory pode conter um ou mais pipelines. 
2. Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica. Por exemplo, se você estiver copiando dados de um armazenamento de BLOBs do Azure tooan repositório Azure Data Lake, você criar duas toolink de serviços vinculados sua conta de armazenamento do Azure e a fábrica de dados de tooyour de armazenamento do Azure Data Lake. Para propriedades de serviço vinculado que específico tooAzure repositório Data Lake, consulte [vinculado propriedades do serviço](#linked-service-properties) seção. 
2. Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello. O exemplo hello mencionado na última etapa do hello, você criará um contêiner de blob do conjunto de dados toospecify hello e a pasta que contém os dados de entrada hello. E, então, criar outro conjunto de dados toospecify Olá pasta e o caminho no armazenamento do Data Lake Olá que contém dados Olá copiados saudação do armazenamento de blob. Para propriedades de conjunto de dados que são específico tooAzure repositório Data Lake, consulte [propriedades de conjunto de dados](#dataset-properties) seção.
3. Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída. Exemplo hello mencionado anteriormente, você usar BlobSource como uma origem e AzureDataLakeStoreSink como um coletor de atividade de cópia de saudação. Da mesma forma, se você está copiando do repositório Azure Data Lake tooAzure armazenamento de Blob, use AzureDataLakeStoreSource e BlobSink na atividade de cópia de saudação. Para propriedades de atividade de cópia que específico tooAzure repositório Data Lake, consulte [copiar as propriedades de atividade](#copy-activity-properties) seção. Para obter detalhes sobre como toouse um repositório de dados como uma origem ou um coletor, clique em Olá link na seção anterior de saudação para seu armazenamento de dados.  

Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você. Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.  Para obter exemplos com definições de JSON para entidades de fábrica de dados que são usados toocopy dados para/de um repositório Azure Data Lake, consulte [exemplos JSON](#json-examples-for-copying-data-to-and-from-data-lake-store) deste artigo.

Olá seções a seguir fornece detalhes sobre propriedades JSON que são usada toodefine Data Factory entidades específicas tooData Lake repositório.

## <a name="linked-service-properties"></a>Propriedades do serviço vinculado
Um serviço vinculado vincula uma fábrica de dados de tooa de repositório de dados. Criar um serviço vinculado do tipo **AzureDataLakeStore** toolink sua fábrica de dados do repositório Data Lake dados tooyour. Olá, a tabela a seguir descreve os serviços de repositório de Lake tooData vinculado JSON elementos específicos. Você pode escolher entre a entidade de serviço e a autenticação de credenciais de usuário.

| Propriedade | Descrição | Obrigatório |
|:--- |:--- |:--- |
| **tipo** | propriedade do tipo Hello deve ser definida muito**AzureDataLakeStore**. | Sim |
| **dataLakeStoreUri** | Informações sobre Olá conta do repositório Azure Data Lake. Essas informações tem um dos formatos a seguir de saudação: `https://[accountname].azuredatalakestore.net/webhdfs/v1` ou `adl://[accountname].azuredatalakestore.net/`. | Sim |
| **subscriptionId** | Saudação de toowhich ID de assinatura do Azure conta do repositório Data Lake pertence. | Obrigatório para coletor |
| **resourceGroupName** | Saudação de toowhich de nome do recurso do Azure grupo conta do repositório Data Lake pertence. | Obrigatório para coletor |

### <a name="service-principal-authentication-recommended"></a>Autenticação de entidade de serviço (recomendada)
autenticação principal do serviço toouse, registre uma entidade de aplicativo no Azure Active Directory (AD do Azure) e conceda ele Olá acessar tooData Lake repositório. Para encontrar as etapas detalhadas, consulte [Autenticação de serviço a serviço](../data-lake-store/data-lake-store-authenticate-using-active-directory.md). Anote Olá valores, que você usar a seguir toodefine Olá vinculado de serviço:
* ID do aplicativo
* Chave do aplicativo 
* ID do locatário

> [!IMPORTANT]
> Se você estiver usando pipelines de dados de tooauthor Olá Assistente para cópia, certifique-se de que você conceda a entidade de serviço Olá pelo menos um **leitor** função no controle de acesso (gerenciamento de identidade e acesso) para a conta do repositório Data Lake hello. Além disso, conceder a entidade de serviço Olá pelo menos **leitura + Execute** raiz de repositório Data Lake de tooyour permissão ("/") e seus filhos. Caso contrário, você poderá ver a mensagem de saudação "hello credenciais fornecidas são inválidas."<br/><br/>
Depois de criar ou atualizar uma entidade de serviço no AD do Azure, pode levar alguns minutos para Olá alterações tootake efeito. Verifique a entidade de serviço hello e configurações de ACL (lista) de controle de acesso de repositório Data Lake. Se você ainda vir a mensagem "hello credenciais fornecidas são inválidas", aguarde um pouco e tente novamente.

Use autenticação principal do serviço especificando Olá propriedades a seguir:

| Propriedade | Descrição | Obrigatório |
|:--- |:--- |:--- |
| **servicePrincipalId** | Especifique a ID do cliente. do aplicativo hello | Sim |
| **servicePrincipalKey** | Especifique a chave de aplicativo hello. | Sim |
| **tenant** | Especifique as informações de locatário hello (ID de locatário ou de nome de domínio) em que o aplicativo reside. Você pode recuperá-la por focalização mouse Olá no canto superior direito Olá Olá portal do Azure. | Sim |

**Exemplo: autenticação de entidade de serviço**
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

### <a name="user-credential-authentication"></a>Autenticação de credenciais de usuário
Como alternativa, você pode usar toocopy de autenticação de credenciais de usuário de ou repositório de Lake tooData especificando Olá propriedades a seguir:

| Propriedade | Descrição | Obrigatório |
|:--- |:--- |:--- |
| **authorization** | Clique em Olá **autorizar** botão no hello Editor da fábrica de dados e insira suas credenciais que atribui a propriedade toothis de URL de autorização do hello gerado automaticamente. | Sim |
| **sessionId** | ID de sessão do OAuth da sessão de autorização de OAuth hello. Cada ID da sessão é exclusiva e pode ser usada somente uma vez. Essa configuração é gerada automaticamente quando você usa Olá Editor da fábrica de dados. | Sim |

**Exemplo: autenticação de credenciais do usuário**
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

#### <a name="token-expiration"></a>Expiração do token
Olá código de autorização que você gerar usando Olá **autorizar** botão expira após um determinado período de tempo. mensagem de saudação significa que esse token de autenticação de saudação expirou:

Erro na operação de credencial: invalid_grant – AADSTS70002: Erro ao validar as credenciais. AADSTS70008: Olá fornecido a concessão de acesso expirou ou foi revogado. ID do rastreamento: d18629e8-af88-43c5-88e3-d8419eb1fca1 ID de correlação: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Carimbo de data/hora: 2015-12-15 21-09-31Z.

Olá tabela a seguir mostra os tempos de expiração de saudação de diferentes tipos de contas de usuário:


| Tipo de usuário | Expira após |
|:--- |:--- |
| Contas de usuário *não* gerenciadas pelo Azure Active Directory (por exemplo, @hotmail.com ou @live.com) |12 horas |
| Contas de usuários gerenciadas pelo Azure Active Directory |14 dias após a última fatia de saudação executar <br/><br/>90 dias, se uma fatia com base em serviços vinculados do OAuth for executada pelo menos uma vez a cada 14 dias |

Se você alterar sua senha antes de tempo de expiração do token de saudação, token Olá expira imediatamente. Você verá a mensagem de saudação mencionada anteriormente nesta seção.

Você pode autorizar a conta hello usando Olá **autorizar** serviço vinculado do botão quando o token de saudação expira tooredeploy hello. Você também pode gerar valores para Olá **sessionId** e **autorização** Olá propriedades programaticamente, usando o seguinte código:


```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```
Para obter detalhes sobre classes de fábrica de dados Olá usados no código hello, consulte Olá [AzureDataLakeStoreLinkedService classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), e [ Classe AuthorizationSessionGetResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) tópicos. Adicionar uma referência tooversion `2.9.10826.1824` de `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` para Olá `WindowsFormsWebAuthenticationDialog` classe usada no código de saudação.

## <a name="dataset-properties"></a>Propriedades do conjunto de dados
toospecify um dados de entrada de toorepresent do conjunto de dados em um repositório Data Lake, definir Olá **tipo** propriedade de conjunto de dados de saudação muito**AzureDataLakeStore**. Saudação de conjunto **linkedServiceName** serviço vinculado de propriedade de nome de toohello Olá dataset de saudação repositório Data Lake. Para obter uma lista completa de seções JSON e as propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo. As seções de um conjunto de dados no JSON, como **structure**, **availability** e **policy** são similares para todos os tipos de conjunto de dados (Banco de Dados SQL do Azure, Blob do Azure e tabela do Azure, por exemplo). Olá **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações como o local e o formato de dados Olá no repositório de dados de saudação. 

Olá **typeProperties** seção um conjunto de dados do tipo **AzureDataLakeStore** contém Olá propriedades a seguir:

| Propriedade | Descrição | Obrigatório |
|:--- |:--- |:--- |
| **folderPath** |Contêiner de toohello do caminho e a pasta no repositório Data Lake. |Sim |
| **fileName** |Nome do arquivo hello no repositório Azure Data Lake. Olá **fileName** propriedade é opcional e diferencia maiusculas de minúsculas. <br/><br/>Se você especificar **fileName**, atividade de saudação (incluindo cópia) funciona em arquivos específicos da saudação.<br/><br/>Quando **fileName** não for especificado, cópia inclui todos os arquivos em **folderPath** no conjunto de dados de entrada hello.<br/><br/>Quando **fileName** não for especificado para um conjunto de dados de saída e **preserveHierarchy** não for especificado no coletor de atividade, nome de saudação do arquivo hello gerado está no formato de saudação dados. _GUID_. txt '. Por exemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt. |Não |
| **partitionedBy** |Olá **partitionedBy** propriedade é opcional. Você pode usá-lo toospecify um caminho dinâmico e o nome do arquivo de dados da série temporal. Por exemplo, **folderPath** pode ser parametrizado para cada hora dos dados. Para obter detalhes e exemplos, consulte [Olá partitionedBy propriedade](#using-partitionedby-property). |Não |
| **format** | Olá, tipos de formato a seguir têm suporte: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, e  **ParquetFormat**. Saudação de conjunto **tipo** propriedade em **formato** tooone desses valores. Para obter mais informações, consulte Olá [formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [formato JSON](data-factory-supported-file-and-compression-formats.md#json-format), [formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [formato ORC](data-factory-supported-file-and-compression-formats.md#orc-format), e [Parquet formato ](data-factory-supported-file-and-compression-formats.md#parquet-format) seções Olá [formatos de arquivo e compactação com suporte do Azure Data Factory](data-factory-supported-file-and-compression-formats.md) artigo. <br><br> Se você deseja que os arquivos de toocopy "como-é" entre repositórios baseada em arquivo (cópia binário), ignore Olá `format` seção em ambas as definições de conjunto de dados de entrada e saída. |Não |
| **compression** | Especifica tipo de saudação e nível de compactação de dados de saudação. Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**. Os níveis de suporte são **Ideal** e **Mais rápido**. Para saber mais, confira [Formatos de arquivo aos quais o Azure Data Factory dá suporte](data-factory-supported-file-and-compression-formats.md#compression-support). |Não |

### <a name="hello-partitionedby-property"></a>propriedade de partitionedBy Olá
Você pode especificar dinâmico **folderPath** e **fileName** propriedades de dados de série temporal com hello **partitionedBy** propriedade, funções da fábrica de dados e do sistema variáveis. Para obter detalhes, consulte Olá [do Azure Data Factory - funções e variáveis de sistema](data-factory-functions-variables.md) artigo.


Em Olá seguinte exemplo, `{Slice}` é substituído pelo valor de saudação da variável de sistema de fábrica de dados Olá `SliceStart` no formato de saudação especificado (`yyyyMMddHH`). nome da saudação `SliceStart` refere-se toohello a hora de início da fatia hello. Olá `folderPath` propriedade é diferente para cada fatia, como em `wikidatagateway/wikisampledataout/2014100103` ou `wikidatagateway/wikisampledataout/2014100104`.

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

Em Olá seguindo o exemplo, ano hello, mês, dia e hora do `SliceStart` são extraídos em variáveis separadas que são usadas por Olá `folderPath` e `fileName` propriedades:
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
Para obter mais detalhes sobre conjuntos de dados de série temporal, agendamento e fatias, consulte Olá [conjuntos de dados no Azure Data Factory](data-factory-create-datasets.md) e [fábrica de dados de agendamento e execução](data-factory-scheduling-and-execution.md) artigos. 


## <a name="copy-activity-properties"></a>Propriedades da atividade de cópia
Para obter uma lista completa de seções e propriedades disponíveis para a definição de atividades, consulte Olá [criar pipelines](data-factory-create-pipelines.md) artigo. As propriedades, como nome, descrição, tabelas de entrada e saída, e política, estão disponíveis para todos os tipos de atividades.

Olá propriedades disponíveis no hello **typeProperties** seção de uma atividade variam de acordo com cada tipo de atividade. Para uma atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.

**AzureDataLakeStoreSource** dá suporte a saudação propriedade Olá a seguir **typeProperties** seção:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| **recursive** |Indica se os dados saudação é lida recursivamente de subpastas de saudação ou somente de pasta especificado hello. |True (valor padrão), False |Não |


**AzureDataLakeStoreSink** dá suporte a saudação seguintes propriedades em Olá **typeProperties** seção:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| **copyBehavior** |Especifica o comportamento de cópia de saudação. |<b>PreserveHierarchy</b>: preserva a hierarquia de arquivo hello na pasta de destino de saudação. caminho relativo do Hello arquivo toosource da pasta de origem é idêntico toohello o caminho relativo da pasta de tootarget do arquivo de destino.<br/><br/><b>FlattenHierarchy</b>: todos os arquivos da pasta de origem Olá são criados no primeiro nível saudação da pasta de destino de saudação. arquivos de destino de saudação são criados com nomes gerados automaticamente.<br/><br/><b>MergeFiles</b>: mescla todos os arquivos Olá pasta tooone do arquivo de origem. Se hello nome de arquivo ou blob for especificado, o nome do arquivo mesclado de Olá é nome especificado da saudação. Caso contrário, o nome do arquivo hello é gerado automaticamente. |Não |

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

## <a name="supported-file-and-compression-formats"></a>Formatos de arquivo e de compactação com suporte
Para obter detalhes, consulte Olá [compactação formatos de arquivo e no Azure Data Factory](data-factory-supported-file-and-compression-formats.md) artigo.

## <a name="json-examples-for-copying-data-tooand-from-data-lake-store"></a>Exemplos JSON para copiar dados tooand do repositório Data Lake
Olá exemplos a seguir fornece as definições de JSON de exemplo. Você pode usar essas definições de exemplo toocreate um pipeline usando Olá [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Olá exemplos mostram como toocopy tooand de dados do armazenamento de BLOBs do Azure e do repositório Data Lake. No entanto, os dados podem ser copiados _diretamente_ de qualquer um dos Olá fontes tooany de Coletores de saudação com suporte. Para obter mais informações, consulte seção hello "repositórios de dados com suporte e formatos" hello [mover dados usando a atividade de cópia](data-factory-data-movement-activities.md) artigo.  

### <a name="example-copy-data-from-azure-blob-storage-tooazure-data-lake-store"></a>Exemplo: Copiar dados de armazenamento de BLOBs do Azure tooAzure repositório Data Lake
código de exemplo Hello nesta seção mostra:

* Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Um serviço vinculado do tipo [AzureDataLakeStore](#linked-service-properties).
* Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureDataLakeStore](#dataset-properties).
* Um [pipeline](data-factory-create-pipelines.md) com atividade de cópia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [AzureDataLakeStoreSink](#copy-activity-properties).

Olá exemplos mostram como série temporal dados do armazenamento de BLOBs do Azure são copiado tooData Lake repositório a cada hora. 

**Serviço vinculado de armazenamento do Azure**

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

**Serviço vinculado do Azure Data Lake Store**

```JSON
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

> [!NOTE]
> Para obter detalhes de configuração, consulte Olá [vinculado propriedades do serviço](#linked-service-properties) seção.
>

**Conjunto de dados de entrada de Blob do Azure**

Em Olá exemplo a seguir, dados são determinados por um novo blob a cada hora (`"frequency": "Hour", "interval": 1`). Olá pasta caminho e nome de arquivo para blob Olá são avaliados dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada. caminho da pasta Olá usa Olá ano, mês e parte do dia da hora de início da saudação. nome do arquivo Hello usa hora Olá parte da saudação hora de início. Olá `"external": true` configuração informa o serviço de fábrica de dados de saudação tabela Olá toohello externo fábrica de dados e não é produzida por uma atividade na fábrica de dados hello.

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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

**Conjunto de dados de saída do Azure Data Lake Store**

Olá exemplo copia dados tooData Lake repositório a seguir. Novos dados são copiados tooData Lake repositório a cada hora.

```JSON
{
    "name": "AzureDataLakeStoreOutput",
      "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
              "frequency": "Hour",
              "interval": 1
        }
      }
}
```


**Atividade de cópia em um pipeline com uma origem de blob e um coletor Data Lake Store**

Saudação de exemplo a seguir, pipeline Olá contém uma atividade de cópia que está configurada toouse Olá conjuntos de dados de entrada e saídos. atividade de cópia de saudação é toorun agendado a cada hora. Na definição JSON de pipeline hello, Olá `source` tipo está definido muito`BlobSource`e hello `sink` tipo está definido muito`AzureDataLakeStoreSink`.

```json
{  
    "name":"SamplePipeline",
    "properties":
    {  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":
        [  
              {
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureBlobInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureDataLakeStoreOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                      },
                      "sink": {
                        "type": "AzureDataLakeStoreSink"
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

### <a name="example-copy-data-from-azure-data-lake-store-tooan-azure-blob"></a>Exemplo: Copiar dados do repositório Azure Data Lake tooan BLOBs do Azure
código de exemplo Hello nesta seção mostra:

* Um serviço vinculado do tipo [AzureDataLakeStore](#linked-service-properties).
* Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureDataLakeStore](#dataset-properties).
* Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* Um [pipeline](data-factory-create-pipelines.md) com uma atividade de cópia que usa [AzureDataLakeStoreSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

código Olá copia dados de série temporal do repositório Data Lake tooan BLOBs do Azure a cada hora. 

**Serviço vinculado do Azure Data Lake Store**

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>"
        }
    }
}
```

> [!NOTE]
> Para obter detalhes de configuração, consulte Olá [vinculado propriedades do serviço](#linked-service-properties) seção.
>

**Serviço vinculado de armazenamento do Azure**

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
**Conjunto de dados de entrada do Azure Data Lake**

Neste exemplo, definindo `"external"` muito`true` informa o serviço de fábrica de dados de saudação tabela Olá toohello externo fábrica de dados e não é produzida por uma atividade na fábrica de dados hello.

```json
{
    "name": "AzureDataLakeStoreInput",
      "properties":
    {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
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
**Conjunto de dados de saída do blob do Azure**

Em Olá exemplo a seguir, os dados são gravados tooa novo blob a cada hora (`"frequency": "Hour", "interval": 1`). caminho da pasta Olá blob Olá é avaliado dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada. caminho da pasta Olá usa Olá ano, mês, dia e parte de horas da hora de início da saudação.

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Uma atividade de cópia em um pipeline com uma origem do Azure Data Lake Store e um coletor de blob**

Saudação de exemplo a seguir, pipeline Olá contém uma atividade de cópia que está configurada toouse Olá conjuntos de dados de entrada e saídos. atividade de cópia de saudação é toorun agendado a cada hora. Na definição JSON de pipeline hello, Olá `source` tipo está definido muito`AzureDataLakeStoreSource`e hello `sink` tipo está definido muito`BlobSink`.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureDakeLaketoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureDataLakeStoreInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureBlobOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "AzureDataLakeStoreSource",
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

Na definição de atividade de cópia hello, você também pode mapear colunas de toocolumns de conjunto de dados de origem Olá no conjunto de dados de coletor de saudação. Para obter detalhes, confira [Mapear colunas de conjunto de dados no Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Desempenho e ajuste
toolearn sobre fatores de saudação que afetam o desempenho de atividade de cópia e como toooptimize, consulte Olá [atividade de cópia guia de desempenho e ajuste](data-factory-copy-activity-performance.md) artigo.
