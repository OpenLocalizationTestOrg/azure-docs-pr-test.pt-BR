---
title: aaaIndexing armazenamento de tabela do Azure com a pesquisa do Azure | Microsoft Docs
description: Saiba como tooindex dados armazenados no armazenamento de tabela do Azure com a pesquisa do Azure
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 1cc27411-d0cc-40ed-8aed-c7cb9ab402b9
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/10/2017
ms.author: eugenesh
ms.openlocfilehash: abb01a4d807cede310246b34775d8059fceb4456
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="index-azure-table-storage-with-azure-search"></a>Indexação do Armazenamento de Tabelas do Azure com a Pesquisa do Azure
Este artigo mostra como toouse dados de tooindex de pesquisa do Azure são armazenados no armazenamento de tabela do Azure.

## <a name="set-up-azure-table-storage-indexing"></a>Indexador do Armazenamento de Tabelas do Azure

Você pode configurar um indexador de armazenamento de Tabela do Azure usando estes recursos:

* [Portal do Azure](https://ms.portal.azure.com)
* [API REST](https://docs.microsoft.com/rest/api/searchservice/Indexer-operations) do Azure Search
* [SDK do .NET](https://aka.ms/search-sdk) do Azure Search

Aqui nós demonstram hello usando Olá API REST. 

### <a name="step-1-create-a-datasource"></a>Etapa 1: Criar uma fonte de dados

Uma fonte de dados especifica quais dados tooindex, hello credenciais tooaccess Olá os dados necessários e políticas de saudação que habilitar a pesquisa do Azure tooefficiently identificam alterações nos dados de saudação.

Para a tabela de indexação, Olá datasource deve ter Olá propriedades a seguir:

- **nome** é Olá o nome exclusivo da fonte de dados hello dentro de seu serviço de pesquisa.
- **type** deve ser `azuretable`.
- **credenciais** parâmetro contém a cadeia de conexão da conta de armazenamento hello. Consulte Olá [especificar credenciais](#Credentials) seção para obter detalhes.
- **contêiner** conjuntos Olá nome da tabela e uma consulta opcional.
    - Especificar o nome da tabela hello usando Olá `name` parâmetro.
    - Opcionalmente, especifique uma consulta usando Olá `query` parâmetro. 

> [!IMPORTANT] 
> Sempre que possível, use um filtro em PartitionKey para obter um melhor desempenho. Qualquer outra consulta faz uma verificação de tabela completa, resultando em mau desempenho se usada em grandes tabelas. Consulte Olá [considerações sobre desempenho](#Performance) seção.


toocreate uma fonte de dados:

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "table-datasource",
        "type" : "azuretable",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-table", "query" : "PartitionKey eq '123'" }
    }   

Para obter mais informações sobre Olá criar fonte de dados API, consulte [criar fonte de dados](https://docs.microsoft.com/rest/api/searchservice/create-data-source).

<a name="Credentials"></a>
#### <a name="ways-toospecify-credentials"></a>Credenciais de toospecify maneiras ####

Você pode fornecer credenciais de saudação para a tabela de saudação em uma das seguintes maneiras: 

- **Cadeia de conexão da conta de armazenamento total acesso**: `DefaultEndpointsProtocol=https;AccountName=<your storage account>;AccountKey=<your account key>` você pode obter cadeia de caracteres de conexão de saudação do hello portal do Azure vai toohello **folha da conta de armazenamento** > **configurações**   >  **Chaves** (para contas de armazenamento clássico) ou **configurações** > **chaves de acesso** (para recursos do Azure Contas de armazenamento Manager).
- **Conta de armazenamento compartilhado a cadeia de conexão de assinatura de acesso**: `TableEndpoint=https://<your account>.table.core.windows.net/;SharedAccessSignature=?sv=2016-05-31&sig=<hello signature>&spr=https&se=<hello validity end time>&srt=co&ss=t&sp=rl` assinatura de acesso compartilhado Olá deve ter Olá lista e permissões de leitura nos contêineres (tabelas neste caso) e objetos (linhas de tabela).
-  **Assinatura de acesso compartilhado de tabela**: `ContainerSharedAccessUri=https://<your storage account>.table.core.windows.net/<table name>?tn=<table name>&sv=2016-05-31&sig=<hello signature>&se=<hello validity end time>&sp=r` assinatura de acesso compartilhado Olá deve ter permissões de consulta (leitura) na tabela de saudação.

Para saber mais sobre assinaturas de acesso compartilhado, confira [Uso de assinaturas de acesso compartilhado](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

> [!NOTE]
> Se você usar credenciais de assinatura de acesso compartilhado, você precisará credenciais de fonte de dados tooupdate Olá periodicamente com assinaturas renovado tooprevent da expiração. Se as credenciais de assinatura de acesso compartilhado expirarem, indexador Olá falhará com uma mensagem de erro semelhante muito "as credenciais fornecidas na cadeia de caracteres de conexão de saudação são inválidas ou expiraram."  

### <a name="step-2-create-an-index"></a>Etapa 2: Criar um índice
índice de saudação especifica campos Olá em um documento, os atributos de Olá, e outras construções essa experiência de pesquisa de saudação de forma.

toocreate um índice:

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
          "name" : "my-target-index",
          "fields": [
            { "name": "key", "type": "Edm.String", "key": true, "searchable": false },
            { "name": "SomeColumnInMyTable", "type": "Edm.String", "searchable": true }
          ]
    }

Para obter mais informações sobre a criação de índices, consulte [Criar Índice](https://docs.microsoft.com/rest/api/searchservice/create-index).

### <a name="step-3-create-an-indexer"></a>Etapa 3: Criar um indexador
Um indexador se conecta a uma fonte de dados com um índice de pesquisa de destino e fornece uma atualização de dados agendada tooautomate hello. 

Depois que a fonte de dados e o índice de saudação são criados, você está pronto toocreate indexador de saudação:

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "table-indexer",
      "dataSourceName" : "table-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" }
    }

Esse indexador é executado a cada duas horas. (intervalo de agendamento hello está definido muito "PT2H".) toorun um indexador a cada 30 minutos, defina o intervalo de saudação muito "PT30M". intervalo com suporte mais curto de saudação é de cinco minutos. agendamento de saudação é opcional. Se omitido, um indexador é executado apenas uma vez quando ela é criada. No entanto, você pode executar um indexador sob demanda a qualquer momento.   

Para obter mais informações sobre Olá criar indexador API, consulte [criar indexador](https://docs.microsoft.com/rest/api/searchservice/create-indexer).

## <a name="deal-with-different-field-names"></a>Lidar com nomes de campos diferentes
Às vezes, os nomes de campo de saudação em seu índice existente são diferentes dos nomes de propriedade Olá em sua tabela. Você pode usar nomes de propriedade de saudação do campo mapeamentos toomap de nomes de campos do hello tabela toohello no seu índice de pesquisa. toolearn mais informações sobre mapeamentos de campo, consulte [mapeamentos de campo do indexador de pesquisa do Azure ligar as diferenças de saudação entre os índices de fontes de dados e a pesquisa](search-indexer-field-mappings.md).

## <a name="handle-document-keys"></a>Manipular chaves de documento
Na pesquisa do Azure, a chave de documento hello identifica exclusivamente um documento. Cada índice de pesquisa deve ter exatamente um campo de chave do tipo `Edm.String`. o campo de chave Olá é necessário para cada documento que está sendo adicionado toohello índice. (Na verdade, Olá é necessário apenas para campos.)

Como as linhas de tabela têm uma chave composta, a Pesquisa do Azure gera um campo sintético chamado `Key` que é uma concatenação dos valores de chave de linha e de chave de partição. Por exemplo, se uma linha do PartitionKey é `PK1` e RowKey é `RK1`, em seguida, Olá `Key` valor do campo é `PK1RK1`.

> [!NOTE]
> Olá `Key` valor pode conter caracteres inválidos em chaves de documento, como traços. Você pode lidar com caracteres inválidos usando Olá `base64Encode` [função de mapeamento de campo](search-indexer-field-mappings.md#base64EncodeFunction). Se você fizer isso, lembre-se a codificação de Base64 de URL seguro de uso tooalso quando passar as chaves de documento na API chama como pesquisa.
>
>

## <a name="incremental-indexing-and-deletion-detection"></a>Indexação incremental e detecção de exclusão 
Quando você configura um toorun do indexador de tabela em um agendamento, ele reindexes linhas somente novas ou atualizadas, conforme determinado por uma linha `Timestamp` valor. Você não tem toospecify uma política de detecção de alteração. Indexação incremental é habilitada automaticamente para você.

tooindicate que certos documentos devem ser removidos do índice hello, você pode usar uma estratégia de exclusão reversível. Em vez de excluir uma linha, adicione um tooindicate de propriedade que ela foi excluída e configurar uma política de detecção de exclusão reversível Olá fonte de dados. Por exemplo, Olá política a seguir considera que uma linha é excluída se Olá linha tem uma propriedade `IsDeleted` com valor de saudação `"true"`:

    PUT https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "my-table-datasource",
        "type" : "azuretable",
        "credentials" : { "connectionString" : "<your storage connection string>" },
        "container" : { "name" : "table name", "query" : "<query>" },
        "dataDeletionDetectionPolicy" : { "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy", "softDeleteColumnName" : "IsDeleted", "softDeleteMarkerValue" : "true" }
    }   

<a name="Performance"></a>
## <a name="performance-considerations"></a>Considerações sobre o desempenho

Por padrão, a pesquisa do Azure usa Olá filtro de consulta a seguir: `Timestamp >= HighWaterMarkValue`. Porque as tabelas do Azure não tem um índice secundário em Olá `Timestamp` campo, esse tipo de consulta requer uma verificação completa e, portanto, lento para tabelas grandes.


Aqui estão duas abordagens possíveis para melhorar o desempenho de indexação de tabela. Ambas as abordagens dependem do uso de partições de tabela: 

- Se seus dados podem ser naturalmente particionados em vários intervalos de partição, crie uma fonte de dados e um indexador correspondente para cada intervalo de partição. Cada indexador agora tem tooprocess apenas um intervalo de partição específica, resultando em melhor desempenho de consulta. Se dados Olá que precisa toobe indexada tem um pequeno número de partições fixas, ainda melhores: cada indexador só faz uma verificação de partição. Por exemplo, toocreate uma fonte de dados para o processamento de um intervalo de partição com chaves de `000` muito`100`, use uma consulta como esta: 
    ```
    "container" : { "name" : "my-table", "query" : "PartitionKey ge '000' and PartitionKey lt '100' " }
    ```

- Se seus dados são particionados por hora (por exemplo, se você criar uma nova partição de cada dia ou semana), considere Olá abordagem a seguir: 
    - Use uma consulta de forma Olá: `(PartitionKey ge <TimeStamp>) and (other filters)`. 
    - Monitorar o progresso de indexador usando [obter API de Status do indexador](https://docs.microsoft.com/rest/api/searchservice/get-indexer-status)e atualizar periodicamente Olá `<TimeStamp>` condição de consulta de saudação com base no hello mais recente bem-sucedida watermark de alto valor. 
    - Com essa abordagem, se você precisar tootrigger uma reindexação completa, você precisa consulta de fonte de dados de saudação tooreset no indexador de saudação tooresetting adição. 


## <a name="help-us-make-azure-search-better"></a>Ajude-nos a aprimorar o Azure Search
Se você tiver solicitações de recursos ou ideias para aperfeiçoamentos, envie-os por meio do nosso [site UserVoice](https://feedback.azure.com/forums/263029-azure-search/).
