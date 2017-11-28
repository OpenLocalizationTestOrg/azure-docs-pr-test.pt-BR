---
title: aaaIndexing armazenamento de BLOBs do Azure com a pesquisa do Azure
description: "Saiba como o texto de extração e o armazenamento de BLOBs do Azure de tooindex de documentos com pesquisa do Azure"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 2a5968f4-6768-4e16-84d0-8b995592f36a
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/22/2017
ms.author: eugenesh
ms.openlocfilehash: 1bdd34e66a4a9192ed88cacbc7b8456d0dcdfeb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-documents-in-azure-blob-storage-with-azure-search"></a>Indexação de documentos no Armazenamento de Blobs do Azure com o Azure Search
Este artigo mostra como toouse documentos de tooindex de pesquisa do Azure (como PDFs, documentos do Microsoft Office e vários outros formatos comuns) armazenados no armazenamento de BLOBs do Azure. Primeiro, ele explica conceitos básicos de saudação de configurar um indexador de blob. Em seguida, ele oferece uma exploração mais profunda de comportamentos e cenários são provavelmente tooencounter.

## <a name="supported-document-formats"></a>Formatos de documento com suporte
indexador de blob Olá pode extrair texto de saudação formatos de documentos a seguir:

* PDF
* Formatos do Microsoft Office: DOCX/DOC, XLSX/XLS, PPT/PPTX, MSG (emails do Outlook)  
* HTML
* XML
* ZIP
* EML
* RTF
* Arquivos de texto sem formatação (consulte também [Como indexar texto sem formatação](#IndexingPlainText))
* JSON (consulte [Como indexar blobs JSON](search-howto-index-json-blobs.md))
* CSV (consulte a versão prévia do recurso [Indexando blobs CSV](search-howto-index-csv-blobs.md))

> [!IMPORTANT]
> No momento, o suporte para matrizes em CSV e JSON está na versão prévia. Esses formatos são disponíveis somente com a versão **2016-09-01-Preview** de saudação 2. x-visualização API REST ou versão do SDK .NET de saudação. Lembre-se de que as APIs de visualização servem para teste e avaliação, e não devem ser usadas em ambientes de produção.
>
>

## <a name="setting-up-blob-indexing"></a>Configuração da indexação de blob
Você pode configurar um indexador do Armazenamento de Blobs do Azure usando:

* [Portal do Azure](https://ms.portal.azure.com)
* [API REST](https://docs.microsoft.com/rest/api/searchservice/Indexer-operations) do Azure Search
* [SDK do .NET](https://aka.ms/search-sdk) do Azure Search

> [!NOTE]
> Alguns recursos (por exemplo, mapeamentos de campo) ainda não estão disponíveis no portal de saudação e tem toobe usada programaticamente.
>
>

Aqui, podemos demonstram hello usando Olá API REST.

### <a name="step-1-create-a-data-source"></a>Etapa 1: Criar uma fonte de dados
Uma fonte de dados especifica quais dados tooindex, as credenciais necessárias tooaccess Olá dados e políticas tooefficiently identificam alterações nos dados da saudação (linhas novo, modificados ou excluídos). Uma fonte de dados pode ser usada por vários indexadores em Olá mesmo serviço de pesquisa.

Para a indexação de blob, a fonte de dados de Olá deve ter Olá propriedades necessárias a seguir:

* **nome** é o nome exclusivo de Olá Olá da fonte de dados no seu serviço de pesquisa.
* **type** deve ser `azureblob`.
* **credenciais** fornece a cadeia de conexão de conta de armazenamento hello como Olá `credentials.connectionString` parâmetro. Consulte [como credenciais toospecify](#Credentials) abaixo para obter detalhes.
* **container** especifica um contêiner em sua conta de armazenamento. Por padrão, todos os blobs no contêiner de saudação são recuperáveis. Se você desejar somente tooindex blobs em um diretório virtual específico, você pode especificar o diretório usando Olá opcional **consulta** parâmetro.

toocreate uma fonte de dados:

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-container", "query" : "<optional-virtual-directory-name>" }
    }   

Para obter mais informações sobre Olá criar fonte de dados API, consulte [criar fonte de dados](https://docs.microsoft.com/rest/api/searchservice/create-data-source).

<a name="Credentials"></a>
#### <a name="how-toospecify-credentials"></a>Como as credenciais de toospecify ####

Você pode fornecer credenciais de saudação do contêiner de blob Olá em uma das seguintes maneiras:

- **Cadeia de conexão da conta de armazenamento de acesso total**: `DefaultEndpointsProtocol=https;AccountName=<your storage account>;AccountKey=<your account key>`. Você pode obter cadeia de caracteres de conexão de saudação do hello portal do Azure navegando toohello folha de conta de armazenamento > Configurações > chaves (para contas de armazenamento do clássico) ou configurações > chaves (para contas de armazenamento do Azure Resource Manager) de acesso.
- **Assinatura de acesso compartilhado de conta de armazenamento** cadeia de caracteres de conexão (SAS): `BlobEndpoint=https://<your account>.blob.core.windows.net/;SharedAccessSignature=?sv=2016-05-31&sig=<hello signature>&spr=https&se=<hello validity end time>&srt=co&ss=b&sp=rl` Olá SAS deve ter Olá lista e permissões de leitura nos contêineres e objetos (blobs nesse caso).
-  **Assinatura de acesso compartilhado do contêiner**: `ContainerSharedAccessUri=https://<your storage account>.blob.core.windows.net/<container name>?sv=2016-05-31&sr=c&sig=<hello signature>&se=<hello validity end time>&sp=rl` Olá SAS deve ter Olá lista e permissões de leitura no contêiner de saudação.

Para saber mais sobre assinaturas de acesso compartilhado de armazenamento, veja [Uso de Assinaturas de Acesso Compartilhado](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

> [!NOTE]
> Se você usar credenciais SAS, você precisará credenciais de fonte de dados tooupdate Olá periodicamente com assinaturas renovado tooprevent da expiração. Se credenciais SAS expirarem, indexador Olá falhará com uma mensagem de erro semelhante muito`Credentials provided in hello connection string are invalid or have expired.`.  

### <a name="step-2-create-an-index"></a>Etapa 2: Criar um índice
índice de saudação especifica campos Olá em um documento, atributos, e outras construções de experiência de pesquisa que forma hello.

Aqui está como toocreate um índice com uma pesquisa `content` campo de texto de saudação toostore extraído de blobs:   

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
          "name" : "my-target-index",
          "fields": [
            { "name": "id", "type": "Edm.String", "key": true, "searchable": false },
            { "name": "content", "type": "Edm.String", "searchable": true, "filterable": false, "sortable": false, "facetable": false }
          ]
    }

Para obter mais informações sobre a criação de índices, consulte [Criar Índice](https://docs.microsoft.com/rest/api/searchservice/create-index)

### <a name="step-3-create-an-indexer"></a>Etapa 3: Criar um indexador
Um indexador se conecta a uma fonte de dados com um índice de pesquisa de destino e fornece uma atualização de dados agendada tooautomate hello.

Após Olá índice e fonte de dados foram criados, você estará pronto toocreate indexador de saudação:

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "blob-indexer",
      "dataSourceName" : "blob-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" }
    }

Esse indexador será executado a cada duas horas (intervalo de agendamento está definido muito "PT2H"). toorun um indexador a cada 30 minutos, defina o intervalo de saudação muito "PT30M". Olá menor intervalo de com suporte é 5 minutos. Olá agenda é opcional - se ele for omitido, um indexador é executado apenas uma vez quando ela é criada. No entanto, você pode executar um indexador sob demanda a qualquer momento.   

Para obter mais detalhes sobre Olá criar indexador API, check-out [criar indexador](https://docs.microsoft.com/rest/api/searchservice/create-indexer).

## <a name="how-azure-search-indexes-blobs"></a>Como o Azure Search indexa os blobs

Dependendo da saudação [configuração indexador](#PartsOfBlobToIndex), indexador de blob Olá pode indexar somente metadados de armazenamento (útil quando apenas cuidado sobre Olá metadados e não precisar tooindex Olá conteúdo de blobs), metadados de conteúdo e armazenamento, ou ambos metadados e o conteúdo textual. Por padrão, o indexador Olá extrai metadados e o conteúdo.

> [!NOTE]
> Por padrão, os blobs com conteúdo estruturado, como JSON, CSV e indexados como uma única parte de texto. Blobs CSV e JSON tooindex de maneira estruturada, consulte [indexação JSON blobs](search-howto-index-json-blobs.md) e [indexação CSV blobs](search-howto-index-csv-blobs.md) recursos de visualização.
>
> Um documento composto ou incorporado (como um arquivo ZIP ou um documento do Word com email do Outlook incorporado contendo anexos) também é indexado como um único documento.

* conteúdo textual de saudação do documento hello é extraído em um campo de cadeia de caracteres chamado `content`.

> [!NOTE]
> A pesquisa do Azure limita a quantidade de texto extrai dependendo Olá preço: 32.000 caracteres gratuitamente camada, 64.000 Basic e 4 milhões para as camadas Standard, Standard S2 e S3 padrão. Um aviso é incluído na resposta de status do indexador Olá para documentos truncados.  

* Propriedades de metadados especificado pelo usuário presentes no blob hello, se houver, serão extraídas textualmente.
* Propriedades de metadados de blob padrão são extraídas em Olá campos a seguir:

  * **metadados\_armazenamento\_nome** (EDM) - nome do arquivo de saudação do blob hello. Por exemplo, se você tiver um blob /my-container/my-folder/subfolder/resume.pdf, Olá valor desse campo é `resume.pdf`.
  * **metadados\_armazenamento\_caminho** (EDM) - Olá completo URI do blob hello, incluindo a conta de armazenamento hello. Por exemplo, `https://myaccount.blob.core.windows.net/my-container/my-folder/subfolder/resume.pdf`
  * **metadados\_armazenamento\_conteúdo\_tipo** (EDM) - tipo de conteúdo, conforme especificado pelo código Olá usado blob de saudação tooupload. Por exemplo: `application/octet-stream`.
  * **metadados\_armazenamento\_último\_modificado** (Edm.DateTimeOffset) - última modificação de carimbo de hora para blobs de saudação. Pesquisa do Azure usa blobs de tooidentify alterado esse carimbo de hora, tooavoid Reindexar tudo após a saudação inicial indexação.
  * **metadata\_storage\_size** (Edm.Int64): tamanho do blob em bytes.
  * **metadados\_armazenamento\_conteúdo\_md5** (EDM) - hash MD5 do conteúdo do blob hello, se disponível.
* Formato de documento de tooeach específico de propriedades de metadados são extraídos em campos de saudação listados [aqui](#ContentSpecificMetadata).

Você não precisa toodefine campos para todos Olá acima propriedades em seu índice de pesquisa - capture apenas propriedades Olá que precisar para seu aplicativo.

> [!NOTE]
> Frequentemente, nomes de campo de saudação em seu índice existente serão diferentes dos nomes de campo Olá gerados durante a extração de documento. Você pode usar **mapeamentos de campo** nomes de propriedade hello toomap fornecidos por nomes de campo de toohello de pesquisa do Azure no seu índice de pesquisa. Você verá um exemplo de uso de mapeamento de campo abaixo.
>
>

<a name="DocumentKeys"></a>
### <a name="defining-document-keys-and-field-mappings"></a>Definir chaves de documento e mapeamentos de campo
Na pesquisa do Azure, a chave de documento hello identifica exclusivamente um documento. Cada índice de pesquisa deve ter exatamente um campo de chave do tipo Edm.String. o campo de chave Olá é necessário para cada documento que está sendo adicionado toohello índice (ele é realmente Olá único campo obrigatório).  

Você deve considerar atentamente qual campo extraído deve ser mapeado toohello campo de chave para o índice. candidatos a saudação são:

* **metadados\_armazenamento\_nome** - isso pode ser um candidato conveniente, mas observe que os nomes de saudação 1) não podem ser exclusivos, porque talvez haja blobs com o mesmo nome em pastas diferentes de saudação e 2) Olá nome pode conter caracteres que são inválidos em chaves de documento, como traços. Você pode lidar com caracteres inválidos usando Olá `base64Encode` [função de mapeamento de campo](search-indexer-field-mappings.md#base64EncodeFunction) - se você fizer isso, lembre-se de chaves de documento tooencode ao transmiti-los na API chama como pesquisa. (Por exemplo, no .NET você pode usar o hello [UrlTokenEncode método](https://msdn.microsoft.com/library/system.web.httpserverutility.urltokenencode.aspx) para essa finalidade).
* **metadados\_armazenamento\_caminho** - usar o caminho completo da saudação garante a exclusividade, mas definitivamente contém um caminho de saudação `/` caracteres [inválida em uma chave de documento](https://docs.microsoft.com/rest/api/searchservice/naming-rules).  Como acima, você tem opção de saudação de codificação chaves hello usando Olá `base64Encode` [função](search-indexer-field-mappings.md#base64EncodeFunction).
* Se nenhuma das opções de saudação acima funcionar, você pode adicionar um blobs de toohello de propriedade de metadados personalizados. Essa opção, no entanto, exigem sua tooadd de processo de carregamento de blob que blobs de tooall de propriedade de metadados. Como chave de saudação é uma propriedade obrigatória, todos os blobs que não têm essa propriedade falhará toobe indexado.

> [!IMPORTANT]
> Se não houver nenhum mapeamento explícito para o campo de chave Olá no índice hello, pesquisa do Azure usa automaticamente `metadata_storage_path` como Olá principal e de base 64 codifica os valores de chave (Olá segunda opção acima).
>
>

Neste exemplo, vamos escolher Olá `metadata_storage_name` campo como chave de documento hello. Vamos supor também o índice tem um campo de chave denominado `key` e um campo `fileSize` para armazenar o tamanho do documento hello. as coisas toowire conforme desejado, especifique Olá mapeamentos de campo ao criar ou atualizar o indexador a seguir:

    "fieldMappings" : [
      { "sourceFieldName" : "metadata_storage_name", "targetFieldName" : "key", "mappingFunction" : { "name" : "base64Encode" } },
      { "sourceFieldName" : "metadata_storage_size", "targetFieldName" : "fileSize" }
    ]

toobring este todos junto, aqui está como você pode adicionar mapeamentos de campo e habilitar codificação de base 64 de chaves para um indexador existente:

    PUT https://[service name].search.windows.net/indexers/blob-indexer?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "dataSourceName" : " blob-datasource ",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" },
      "fieldMappings" : [
        { "sourceFieldName" : "metadata_storage_name", "targetFieldName" : "key", "mappingFunction" : { "name" : "base64Encode" } },
        { "sourceFieldName" : "metadata_storage_size", "targetFieldName" : "fileSize" }
      ]
    }

> [!NOTE]
> toolearn mais informações sobre mapeamentos de campo, consulte [neste artigo](search-indexer-field-mappings.md).
>
>

<a name="WhichBlobsAreIndexed"></a>
## <a name="controlling-which-blobs-are-indexed"></a>Controlando quais blobs serão indexados
É possível controlar quais blobs são indexados e quais são ignorados.

### <a name="index-only-hello-blobs-with-specific-file-extensions"></a>Indexe somente os blobs Olá com extensões de arquivo específico
Você pode indexar somente os blobs Olá com extensões de nome de arquivo hello especificar usando Olá `indexedFileNameExtensions` parâmetro de configuração do indexador. valor de saudação é uma cadeia de caracteres que contém uma lista separada por vírgulas de extensões de arquivo (com um ponto à esquerda). Por exemplo, tooindex somente hello. PDF e. Blobs DOCX, faça o seguinte:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "indexedFileNameExtensions" : ".pdf,.docx" } }
    }

### <a name="exclude-blobs-with-specific-file-extensions"></a>Excluir blobs com extensões de arquivo específicas
Você pode excluir blobs com extensões de nome de arquivo específico de indexação usando Olá `excludedFileNameExtensions` parâmetro de configuração. valor de saudação é uma cadeia de caracteres que contém uma lista separada por vírgulas de extensões de arquivo (com um ponto à esquerda). Por exemplo, tooindex todos os blobs exceto aqueles com hello. PNG e. Extensões JPEG, faça o seguinte:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "excludedFileNameExtensions" : ".png,.jpeg" } }
    }

Se os parâmetros `indexedFileNameExtensions` e `excludedFileNameExtensions` estiverem presentes, o Azure Search primeiro examinará `indexedFileNameExtensions`, em seguida, `excludedFileNameExtensions`. Isso significa que se hello a mesma extensão de arquivo estiver presente em ambas as listas, ele será excluído da indexação.

### <a name="dealing-with-unsupported-content-types"></a>Lidando com tipos de conteúdo sem suporte

Por padrão, o indexador de blob Olá para assim que ele encontra um blob com um tipo de conteúdo sem suporte (por exemplo, uma imagem). Naturalmente, você pode usar Olá `excludedFileNameExtensions` parâmetro tooskip certos tipos de conteúdo. No entanto, talvez seja necessário tooindex blobs sem saber com antecedência todos Olá possíveis tipos de conteúdo. toocontinue indexação quando um tipo de conteúdo sem suporte é encontrado, defina Olá `failOnUnsupportedContentType` parâmetro de configuração muito`false`:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "failOnUnsupportedContentType" : false } }
    }

### <a name="ignoring-parsing-errors"></a>Ignorando erros de análise

Lógica de extração de documento de pesquisa do Azure não é perfeita e, às vezes, haverá falha tooparse documentos de um tipo de conteúdo com suporte, como. DOCX ou. PDF. Se você não quiser Olá toointerrupt indexação em tais casos, defina Olá `maxFailedItems` e `maxFailedItemsPerBatch` valores razoável de toosome de parâmetros de configuração. Por exemplo:

    {
      ... other parts of indexer definition
      "parameters" : { "maxFailedItems" : 10, "maxFailedItemsPerBatch" : 10 }
    }

<a name="PartsOfBlobToIndex"></a>
## <a name="controlling-which-parts-of-hello-blob-are-indexed"></a>Controlando quais partes do blob Olá são indexados

Você pode controlar quais partes dos blobs Olá são indexadas usando Olá `dataToExtract` parâmetro de configuração. Pode levar Olá valores a seguir:

* `storageMetadata`-Especifica que somente Olá [propriedades de blob padrão e os metadados especificados pelo usuário](../storage/blobs/storage-properties-metadata.md) são indexados.
* `allMetadata`-Especifica que os metadados de armazenamento e hello [metadados específicos do tipo de conteúdo](#ContentSpecificMetadata) extraído do blob Olá conteúdo são indexados.
* `contentAndMetadata`-Especifica que todos os metadados e o conteúdo textual extraído do blob Olá são indexados. Este é o valor padrão de saudação.

Por exemplo, tooindex apenas os metadados de armazenamento hello, use:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "dataToExtract" : "storageMetadata" } }
    }

### <a name="using-blob-metadata-toocontrol-how-blobs-are-indexed"></a>Usando toocontrol de metadados de blob como blobs são indexados

parâmetros de configuração de saudação descritos acima se aplicam a tooall blobs. Às vezes, convém toocontrol como *blobs individuais* são indexados. Você pode fazer isso adicionando o seguinte Olá valores e propriedades de metadados de blob:

| Nome da propriedade | Valor da propriedade | Explicação |
| --- | --- | --- |
| AzureSearch_Skip |"true" |Instrui o blob de Olá Olá blob indexador toocompletely ignorar. Não há nenhuma tentativa de extração de metadados nem de conteúdo. Isso é útil quando um blob específico falha repetidamente e interrompe o processo de indexação hello. |
| AzureSearch_SkipContent |"true" |Isso é equivalente a `"dataToExtract" : "allMetadata"` configuração descrito [acima](#PartsOfBlobToIndex) blob específico tooa no escopo. |

## <a name="incremental-indexing-and-deletion-detection"></a>Indexação incremental e detecção de exclusão 
Quando você configura um toorun do indexador de blob em um agendamento, ele indexará novamente apenas Olá alterada blobs, conforme determinado pelo blob de saudação `LastModified` timestamp.

> [!NOTE]
> Você não tem uma política de detecção de alteração toospecify – indexação incremental é habilitado automaticamente para você.

documentos de exclusão toosupport, use uma abordagem de "exclusão reversível". Se você excluir blobs de saudação imediatamente, documentos correspondentes não serão removidos do índice de pesquisa de saudação. Em vez disso, use Olá etapas a seguir:  

1. Adicionar tooAzure da tooindicate um blob metadados personalizados propriedade toohello pesquisa que é logicamente excluído
2. Configurar uma política de detecção de exclusão reversível na fonte de dados de saudação
3. Depois que o indexador Olá processou blob hello (conforme mostrado pelo status do indexador Olá API), você pode excluir fisicamente blob Olá

Por exemplo, Olá política a seguir considera uma toobe blob excluído se ele tem uma propriedade de metadados `IsDeleted` com valor de saudação `true`:

    PUT https://[service name].search.windows.net/datasources/blob-datasource?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "<your storage connection string>" },
        "container" : { "name" : "my-container", "query" : "my-folder" },
        "dataDeletionDetectionPolicy" : {
            "@odata.type" :"#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",     
            "softDeleteColumnName" : "IsDeleted",
            "softDeleteMarkerValue" : "true"
        }
    }   

## <a name="indexing-large-datasets"></a>Indexando grandes conjuntos de dados

A indexação de blobs pode ser um processo demorado. Em casos em que você tiver milhões de tooindex blobs, você pode acelerar a indexação de particionar seus dados e usando várias indexadores tooprocess Olá de dados em paralelo. Veja como você pode configurar isso:

- Particione seus dados em vários contêineres de blob ou pastas virtuais
- Configure várias fontes de dados do Azure Search, um por contêiner ou pasta. pasta de blob tooa toopoint, use Olá `query` parâmetro:

    ```
    {
        "name" : "blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "<your storage connection string>" },
        "container" : { "name" : "my-container", "query" : "my-folder" }
    }
    ```

- Crie um indexador correspondente para cada fonte de dados. Todos os Olá indexadores podem ponto toohello mesmo índice de pesquisa de destino.  

- Uma unidade de pesquisa em seu serviço pode executar um indexador a qualquer momento. Criar vários indexadores conforme descrito acima será útil somente se eles realmente forem executados em paralelo. toorun vários indexadores em paralelo, dimensionar o serviço de pesquisa com a criação de um número apropriado de partições e réplicas. Por exemplo, se o serviço de pesquisa tiver 6 unidades de pesquisa (por exemplo, réplicas de 2 partições x 3), em seguida, 6 indexadores podem executar simultaneamente, resultando em um aumento de seis vezes produtividade da indexação hello. toolearn mais informações sobre dimensionamento e planejamento de capacidade, consulte [níveis de recursos para cargas de trabalho na pesquisa do Azure de indexação e consulta de escala](search-capacity-planning.md).

## <a name="indexing-documents-along-with-related-data"></a>Indexação de documentos junto com os dados relacionados

Talvez você queira "montar" muito documentos de várias fontes em seu índice. Por exemplo, talvez você queira toomerge texto de blobs de com outros metadados armazenados no banco de dados do Cosmos. Você pode até usar Olá API de indexação de push junto com vários indexadores muito criar documentos de pesquisa de várias partes. 

Para este toowork, todos os indexadores e outros componentes necessário tooagree na chave de documento hello. Para obter instruções passo a passo detalhadas, consulte este artigo externo: [Combinar documentos com outros dados no Azure Search](http://blog.lytzen.name/2017/01/combine-documents-with-other-data-in.html).

<a name="IndexingPlainText"></a>
## <a name="indexing-plain-text"></a>Indexação de texto sem formatação 

Se todos os seus blobs contenham texto sem formatação no hello a mesma codificação, você pode melhorar significativamente o desempenho de indexação usando **modo de análise de texto**. texto toouse análise modo, Olá conjunto `parsingMode` propriedade de configuração muito`text`:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "parsingMode" : "text" } }
    }

Por padrão, Olá `UTF-8` codificação será assumida. toospecify uma codificação diferente, use Olá `encoding` propriedade de configuração: 

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "parsingMode" : "text", "encoding" : "windows-1252" } }
    }


<a name="ContentSpecificMetadata"></a>
## <a name="content-type-specific-metadata-properties"></a>Propriedades de metadados específicas ao tipo de conteúdo
Olá tabela a seguir resume o processo executado para cada formato de documento e descreve as propriedades de metadados Olá extraídas pela pesquisa do Azure.

| Formato de documento/tipo de conteúdo | Propriedades de metadados específicas do tipo de conteúdo | Detalhes do processamento |
| --- | --- | --- |
| HTML (`text/html`) |`metadata_content_encoding`<br/>`metadata_content_type`<br/>`metadata_language`<br/>`metadata_description`<br/>`metadata_keywords`<br/>`metadata_title` |Remoção da marcação HTML e extração do texto |
| PDF (`application/pdf`) |`metadata_content_type`<br/>`metadata_language`<br/>`metadata_author`<br/>`metadata_title` |Extração do texto, incluindo documentos incorporados (excluindo imagens) |
| DOCX (application/vnd.openxmlformats-officedocument.wordprocessingml.document) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_character_count`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_page_count`<br/>`metadata_word_count` |Extração de texto, incluindo documentos incorporados |
| DOC (application/msword) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_character_count`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_page_count`<br/>`metadata_word_count` |Extração de texto, incluindo documentos incorporados |
| XLSX (application/vnd.openxmlformats-officedocument.spreadsheetml.sheet) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified` |Extração de texto, incluindo documentos incorporados |
| XLS (application/vnd.ms-excel) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified` |Extração de texto, incluindo documentos incorporados |
| PPTX (application/vnd.openxmlformats-officedocument.presentationml.presentation) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_slide_count`<br/>`metadata_title` |Extração de texto, incluindo documentos incorporados |
| PPT (application/vnd.ms-powerpoint) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_slide_count`<br/>`metadata_title` |Extração de texto, incluindo documentos incorporados |
| MSG (application/vnd.ms-outlook) |`metadata_content_type`<br/>`metadata_message_from`<br/>`metadata_message_to`<br/>`metadata_message_cc`<br/>`metadata_message_bcc`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_subject` |Extração do texto, incluindo anexos |
| ZIP (application/zip) |`metadata_content_type` |Extrair texto de todos os documentos no arquivo hello |
| XML (application/xml) |`metadata_content_type`</br>`metadata_content_encoding`</br> |Remoção da marcação XML e extração do texto |
| JSON (application/json) |`metadata_content_type`</br>`metadata_content_encoding` |Extrair texto<br/>Observação: Se você precisar tooextract documento vários campos de um blob JSON, consulte [indexação JSON blobs](search-howto-index-json-blobs.md) para obter detalhes |
| EML (message/rfc822) |`metadata_content_type`<br/>`metadata_message_from`<br/>`metadata_message_to`<br/>`metadata_message_cc`<br/>`metadata_creation_date`<br/>`metadata_subject` |Extração do texto, incluindo anexos |
| RTF (aplicativo/rtf) |`metadata_content_type`</br>`metadata_author`</br>`metadata_character_count`</br>`metadata_creation_date`</br>`metadata_page_count`</br>`metadata_word_count`</br> | Extrair texto|
| Texto sem formatação (text/plain) |`metadata_content_type`</br>`metadata_content_encoding`</br> | Extrair texto|


## <a name="help-us-make-azure-search-better"></a>Ajude-nos a aprimorar o Azure Search
Caso você tenha solicitações de recursos ou ideias para melhorias, entre em contato conosco pelo [site UserVoice](https://feedback.azure.com/forums/263029-azure-search/).
