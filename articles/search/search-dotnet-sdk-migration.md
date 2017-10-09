---
title: "aaaUpgrading toohello SDK .NET da pesquisa do Azure versão 1.1 | Microsoft Docs"
description: "Atualizando toohello SDK .NET da pesquisa do Azure versão 1.1"
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 66f89958-a320-4a24-87f9-69315848909f
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/11/2017
ms.author: brjohnst
ms.openlocfilehash: 291ae5731546e47b3c22c721d3552a79bdea80c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrading-toohello-azure-search-net-sdk-version-3"></a>Atualizando toohello SDK .NET da pesquisa do Azure versão 3
Se você estiver usando a versão preview 2.0 ou anterior de saudação [SDK .NET da pesquisa do Azure](https://aka.ms/search-sdk), este artigo o ajudará a atualizar a versão do aplicativo toouse 3.

Para obter uma explicação mais geral de saudação SDK incluindo exemplos, consulte [como toouse Azure pesquisa de um aplicativo .NET](search-howto-dotnet-sdk.md).

A versão 3 do hello SDK .NET da pesquisa do Azure contém algumas alterações de versões anteriores. A maioria das alterações é leve e, portanto, a alteração do seu código não deve exigir muito. Consulte [tooupgrade etapas](#UpgradeSteps) para obter instruções sobre como toochange a código toouse Olá nova versão do SDK.

> [!NOTE]
> Se você estiver usando a versão 1.0.2-preview ou anterior, você deve atualizar primeiro o tooversion 1.1 e, em seguida, atualizar tooversion 3. Consulte [Apêndice: etapas tooupgrade tooversion 1.1](#UpgradeStepsV1) para obter instruções.
>
> Sua instância de serviço de pesquisa do Azure oferece suporte a várias versões da API REST, incluindo hello mais recente. Você pode continuar toouse uma versão quando ela não é mais hello mais recente, mas é recomendável que você migre a sua versão mais recente do código toouse hello. Ao usar o hello API REST, você deve especificar a versão de API de Olá em cada solicitação feita por meio do parâmetro de versão de api de saudação. Ao usar o SDK .NET de saudação, versão de saudação do Olá SDK que você está usando determina versão correspondente de saudação do hello API REST. Se você estiver usando um SDK anterior, você pode continuar toorun que o código sem alterações mesmo se o serviço Olá é atualizado toosupport uma API mais recente versão.

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-3"></a>Novidades na versão 3
Versão 3 da saudação de destinos de SDK .NET da pesquisa do Azure hello mais recente versão disponível do hello API de REST de pesquisa do Azure, especificamente 2016-09-01. Isso torna possível toouse muitos novos recursos de pesquisa do Azure de um aplicativo .NET, incluindo Olá seguinte:

* [Analisadores personalizados](https://aka.ms/customanalyzers)
* Suporte do indexador do [Armazenamento de Blobs do Azure](search-howto-indexing-azure-blob-storage.md) e do [Armazenamento de Tabelas do Azure](search-howto-indexing-azure-tables.md)
* Personalização do indexador por meio de [mapeamentos de campo](search-indexer-field-mappings.md)
* Suporte a ETags tooenable seguro atualizações simultâneas de índice definições, indexadores e fontes de dados
* Suporte para a criação de definições de campo de índice declarativamente a decoração de sua classe de modelo e usando Olá novo `FieldBuilder` classe.
* Suporte para .NET Core e .NET Portable Profile 111

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a>Etapas tooupgrade
Primeiro, atualize sua referência de NuGet para `Microsoft.Azure.Search` usando o NuGet Package Manager Console hello ou clicando duas vezes em suas referências do projeto e selecionando "Gerenciar NuGet pacotes …" no Visual Studio.

Depois que o NuGet baixou Olá novos pacotes e suas dependências, recompile o projeto. Dependendo de como o código está estruturado, ele poderá ser recriado com êxito. Nesse caso, você está pronto toogo!

Se a compilação falhar, você verá um erro de compilação como Olá a seguir:

    Program.cs(31,45,31,86): error CS0266: Cannot implicitly convert type 'Microsoft.Azure.Search.ISearchIndexClient' too'Microsoft.Azure.Search.SearchIndexClient'. An explicit conversion exists (are you missing a cast?)

próxima etapa do Hello é toofix esse erro de compilação. Consulte [alterações significativas na versão 3](#ListOfChanges) para obter detalhes sobre o que causa o erro hello e como toofix-lo.

Você pode ver compilação adicional avisos relacionados tooobsolete métodos ou propriedades. avisos de saudação inclui instruções sobre em quais toouse em vez disso, de saudação recurso preterido. Por exemplo, se seu aplicativo usa Olá `IndexingParameters.Base64EncodeKeys` propriedade, você deve receber um aviso que diz`"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`

Depois de solucionar os erros de compilação, você pode fazer alterações tooyour aplicativo tootake aproveitar novas funcionalidades se desejar. Novos recursos no SDK do hello são detalhados no [o que há de novo na versão 3](#WhatsNew).

<a name="ListOfChanges"></a>

## <a name="breaking-changes-in-version-3"></a>Alterações significativas na versão 3
Há um pequeno número de alterações significativas na versão 3 que podem exigir código altera além toorebuilding seu aplicativo.

### <a name="indexesgetclient-return-type"></a>Tipo de retorno de Indexes.GetClient
Olá `Indexes.GetClient` método tem um novo tipo de retorno. Anteriormente, ele retornou `SearchIndexClient`, mas isso foi alterado muito`ISearchIndexClient` na versão 2.0-visualização e que alteração traz tooversion 3. Isso é toosupport os clientes que desejem Olá toomock `GetClient` método para testes de unidade, retornando uma implementação fictícia do `ISearchIndexClient`.

#### <a name="example"></a>Exemplo
Se o seu código tiver esta aparência:

```csharp
SearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

Você pode alterá-la toothis toofix qualquer erro de compilação:

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

### <a name="analyzername-datatype-and-others-are-no-longer-implicitly-convertible-toostrings"></a>AnalyzerName, tipo de dados e outros não são implicitamente conversíveis toostrings
Há muitos tipos de saudação SDK .NET da pesquisa do Azure que derivam de `ExtensibleEnum`. Anteriormente esses tipos foram todos implicitamente conversível tootype `string`. No entanto, um bug foi descoberto em Olá `Object.Equals` implementação para essas classes e corrigindo Olá bug necessário desabilitar essa conversão implícita. Conversão explícita muito`string` ainda é permitido.

#### <a name="example"></a>Exemplo
Se o seu código tiver esta aparência:

```csharp
var customTokenizerName = TokenizerName.Create("my_tokenizer"); 
var customTokenFilterName = TokenFilterName.Create("my_tokenfilter"); 
var customCharFilterName = CharFilterName.Create("my_charfilter"); 
 
var index = new Index();
index.Analyzers = new Analyzer[] 
{ 
    new CustomAnalyzer( 
        "my_analyzer",  
        customTokenizerName,  
        new[] { customTokenFilterName },  
        new[] { customCharFilterName }), 
}; 
```

Você pode alterá-la toothis toofix qualquer erro de compilação:

```csharp
const string CustomTokenizerName = "my_tokenizer"; 
const string CustomTokenFilterName = "my_tokenfilter"; 
const string CustomCharFilterName = "my_charfilter"; 
 
var index = new Index();
index.Analyzers = new Analyzer[] 
{ 
    new CustomAnalyzer( 
        "my_analyzer",  
        CustomTokenizerName,  
        new TokenFilterName[] { CustomTokenFilterName },  
        new CharFilterName[] { CustomCharFilterName })
}; 
```

### <a name="removed-obsolete-members"></a>Remover membros obsoletos

Você pode ver toomethods relacionados de erros de compilação ou propriedades que foram marcadas como obsoletos no versão 2.0-visualização e subsequentemente removidas na versão 3. Se você encontrar esses erros, aqui está como tooresolve-los:

- Se usava o construtor: `ScoringParameter(string name, string value)`, use este em vez dele: `ScoringParameter(string name, IEnumerable<string> values)`
- Se você estivesse usando Olá `ScoringParameter.Value` propriedade, use Olá `ScoringParameter.Values` propriedade ou hello `ToString` método em vez disso.
- Se você estivesse usando Olá `SearchRequestOptions.RequestId` propriedade, use Olá `ClientRequestId` propriedade em vez disso.

### <a name="removed-preview-features"></a>Recursos de visualização removidos

Se você estiver atualizando da versão 2.0 preview tooversion 3, lembre-se de que suporte a indexadores de Blob de análise de CSV e JSON foi removido desde que esses recursos ainda estão na visualização. Especificamente, Olá Olá métodos a seguir `IndexingParametersExtensions` classe foram removidos:

- `ParseJson`
- `ParseJsonArrays`
- `ParseDelimitedTextFiles`

Se seu aplicativo tem uma dependência de disco rígida sobre esses recursos, não será capaz de tooupgrade tooversion 3 de saudação SDK .NET da pesquisa do Azure. Você pode continuar toouse versão 2.0-visualização. No entanto, lembre-se que **não é recomendável usar SDKs de visualização em aplicativos de produção**. Os recursos de visualização destinam-se apenas a fins de avaliação e podem ser alterados.

## <a name="conclusion"></a>Conclusão
Se você precisar de mais detalhes sobre o uso Olá SDK .NET da pesquisa do Azure, consulte nosso atualizado recentemente [instruções](search-howto-dotnet-sdk.md).

Apreciamos seus comentários em Olá SDK. Se você encontrar problemas, sinta-se livre tooask nos para obter ajuda sobre Olá [Fórum do MSDN de pesquisa do Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch). Se você encontrar um erro, você pode registrar um problema no hello [repositório GitHub do Azure .NET SDK](https://github.com/Azure/azure-sdk-for-net/issues). Verifique se tooprefix o título do problema com "SDK de pesquisa:".

Obrigado por usar a Pesquisa do Azure!

<a name="UpgradeStepsV1"></a>

## <a name="appendix-steps-tooupgrade-tooversion-11"></a>Apêndice: Etapas tooupgrade tooversion 1.1
> [!NOTE]
> Esta seção se aplica apenas toousers de saudação SDK .NET da pesquisa do Azure versão 1.0.2-preview e anteriores.
> 
> 

Primeiro, atualize sua referência de NuGet para `Microsoft.Azure.Search` usando o NuGet Package Manager Console hello ou clicando duas vezes em suas referências do projeto e selecionando "Gerenciar NuGet pacotes …" no Visual Studio.

Depois que o NuGet baixou Olá novos pacotes e suas dependências, recompile o projeto.

Se você anteriormente usando a versão 1.0.0-preview, 1.0.1-preview ou 1.0.2-preview, compilação de saudação deve ter êxito e você está pronto toogo!

Se você estava usando anteriormente 0.13.0-preview versão ou anterior, você verá erros como Olá seguinte compilação:

    Program.cs(137,56,137,62): error CS0117: 'Microsoft.Azure.Search.Models.IndexBatch' does not contain a definition for 'Create'
    Program.cs(137,99,137,105): error CS0117: 'Microsoft.Azure.Search.Models.IndexAction' does not contain a definition for 'Create'
    Program.cs(146,41,146,54): error CS1061: 'Microsoft.Azure.Search.IndexBatchException' does not contain a definition for 'IndexResponse' and no extension method 'IndexResponse' accepting a first argument of type 'Microsoft.Azure.Search.IndexBatchException' could be found (are you missing a using directive or an assembly reference?)
    Program.cs(163,13,163,42): error CS0246: hello type or namespace name 'DocumentSearchResponse' could not be found (are you missing a using directive or an assembly reference?)

Olá próxima etapa é erros de compilação toofix Olá uma. A maioria exigirá alterando alguns nomes de classe e método que foram renomeados no hello SDK. [Lista de alterações significativas na versão 1.1](#ListOfChangesV1) contém uma lista dessas alterações de nome.

Se você estiver usando classes personalizadas toomodel seus documentos e as classes têm propriedades de tipos primitivos não anulável (por exemplo, `int` ou `bool` em c#), há uma correção de bug na versão Olá 1.1 do SDK Olá dos quais você deve estar ciente. Veja [Correções de bug na versão 1.1](#BugFixesV1) para obter mais detalhes.

Finalmente, depois de solucionar os erros de compilação, você pode fazer alterações tooyour aplicativo tootake aproveitar novas funcionalidades se desejar.

<a name="ListOfChangesV1"></a>

### <a name="list-of-breaking-changes-in-version-11"></a>Lista de alterações significativas na versão 1.1
Olá lista a seguir é ordenada pela probabilidade de saudação que a alteração de saudação afetará o código do aplicativo.

#### <a name="indexbatch-and-indexaction-changes"></a>Alterações de IndexBatch e IndexAction
`IndexBatch.Create`foi renomeado muito`IndexBatch.New` e não tem mais um `params` argumento. Você pode usar `IndexBatch.New` para lotes que combinam tipos diferentes de ações (mesclagens, exclusões, etc.). Além disso, há novos métodos estáticos para a criação de lotes em que todas as ações de saudação são Olá mesmo: `Delete`, `Merge`, `MergeOrUpload`, e `Upload`.

`IndexAction` não tem mais construtores públicos e suas propriedades agora são imutáveis. Você deve usar os novos métodos estáticos de saudação para a criação de ações para finalidades diferentes: `Delete`, `Merge`, `MergeOrUpload`, e `Upload`. `IndexAction.Create` foi removido. Se você usou a sobrecarga de saudação que usa apenas um documento, verifique se toouse `Upload` em vez disso.

##### <a name="example"></a>Exemplo
Se o seu código tiver esta aparência:

    var batch = IndexBatch.Create(documents.Select(doc => IndexAction.Create(doc)));
    indexClient.Documents.Index(batch);

Você pode alterá-la toothis toofix qualquer erro de compilação:

    var batch = IndexBatch.New(documents.Select(doc => IndexAction.Upload(doc)));
    indexClient.Documents.Index(batch);

Se desejar, você pode simplificar-toothis:

    var batch = IndexBatch.Upload(documents);
    indexClient.Documents.Index(batch);

#### <a name="indexbatchexception-changes"></a>Alterações de IndexBatchException
Olá `IndexBatchException.IndexResponse` propriedade foi renomeada muito`IndexingResults`, e seu tipo é agora `IList<IndexingResult>`.

##### <a name="example"></a>Exemplo
Se o seu código tiver esta aparência:

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexResponse.Results.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

Você pode alterá-la toothis toofix qualquer erro de compilação:

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<a name="OperationMethodChanges"></a>

#### <a name="operation-method-changes"></a>Alterações de método de operação
Cada operação no hello SDK .NET da pesquisa do Azure é exposta como um conjunto de sobrecargas do método para chamadores síncronos e assíncronos. Olá assinaturas e fatorar essas sobrecargas de método foi alterado na versão 1.1.

Por exemplo, Olá operação "Obter estatísticas de índice" em versões anteriores do SDK do hello expostos estas assinaturas:

Em `IIndexOperations`:

    // Asynchronous operation with all parameters
    Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        string indexName,
        CancellationToken cancellationToken);

Em `IndexOperationsExtensions`:

    // Asynchronous operation with only required parameters
    public static Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        this IIndexOperations operations,
        string indexName);

    // Synchronous operation with only required parameters
    public static IndexGetStatisticsResponse GetStatistics(
        this IIndexOperations operations,
        string indexName);

assinaturas de método Olá para Olá a mesma operação na versão 1.1 esta aparência:

Em `IIndexesOperations`:

    // Asynchronous operation with lower-level HTTP features exposed
    Task<AzureOperationResponse<IndexGetStatisticsResult>> GetStatisticsWithHttpMessagesAsync(
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        Dictionary<string, List<string>> customHeaders = null,
        CancellationToken cancellationToken = default(CancellationToken));

Em `IndexesOperationsExtensions`:

    // Simplified asynchronous operation
    public static Task<IndexGetStatisticsResult> GetStatisticsAsync(
        this IIndexesOperations operations,
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        CancellationToken cancellationToken = default(CancellationToken));

    // Simplified synchronous operation
    public static IndexGetStatisticsResult GetStatistics(
        this IIndexesOperations operations,
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions));

Olá SDK .NET da pesquisa do Azure a partir da versão 1.1, organiza os métodos de operação diferente:

* Os parâmetros opcionais agora são modelados como padrão em vez de sobrecargas de método adicionais. Isso reduz o número de saudação de sobrecargas do método, às vezes drasticamente.
* métodos de extensão Olá agora ocultam muitos detalhes estranhas saudação do HTTP do chamador hello. Por exemplo, versões mais antigas do hello SDK retornou um objeto de resposta com um código de status HTTP, que você geralmente não precisam toocheck porque métodos de operação gerar `CloudException` para qualquer código de status que indica um erro. Olá novos objetos de modelo apenas retorno de métodos de extensão, economiza Olá problemas de ter toounwrap-los em seu código.
* Por outro lado, hello interfaces principais agora expõem os métodos que oferecem mais controle no nível de saudação HTTP se necessário. Agora você pode transmitir toobe de cabeçalhos HTTP personalizado incluído em solicitações e Olá novo `AzureOperationResponse<T>` retornar tipo fornece acesso direto toohello `HttpRequestMessage` e `HttpResponseMessage` para operação de saudação. `AzureOperationResponse`é definido em Olá `Microsoft.Rest.Azure` namespace e substitui `Hyak.Common.OperationResponse`.

#### <a name="scoringparameters-changes"></a>Alterações de ScoringParameters
Uma nova classe chamada `ScoringParameter` foi adicionado no hello toomake SDK mais recente perfis de tooscoring mais fácil do tooprovide parâmetros em uma consulta de pesquisa. Olá anteriormente `ScoringProfiles` propriedade Olá `SearchParameters` classe foi digitada como `IList<string>`; Agora, ele é digitado como `IList<ScoringParameter>`.

##### <a name="example"></a>Exemplo
Se o seu código tiver esta aparência:

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters = new[] { "featuredParam-featured", "mapCenterParam-" + lon + "," + lat };

Você pode alterá-la toothis toofix qualquer erro de compilação: 

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters =
        new[]
        {
            new ScoringParameter("featuredParam", new[] { "featured" }),
            new ScoringParameter("mapCenterParam", GeographyPoint.Create(lat, lon))
        };

#### <a name="model-class-changes"></a>Alterações no modelo de classe
Devido a alterações de assinatura toohello descritas na [alterações de método da operação](#OperationMethodChanges), muitas classes em Olá `Microsoft.Azure.Search.Models` namespace foram renomeados ou removidos. Por exemplo:

* `IndexDefinitionResponse` foi substituído por `AzureOperationResponse<Index>`
* `DocumentSearchResponse`foi renomeado muito`DocumentSearchResult`
* `IndexResult`foi renomeado muito`IndexingResult`
* `Documents.Count()`agora retorna um `long` com contagem de documentos de saudação em vez de um`DocumentCountResponse`
* `IndexGetStatisticsResponse`foi renomeado muito`IndexGetStatisticsResult`
* `IndexListResponse`foi renomeado muito`IndexListResult`

toosummarize, `OperationResponse`-as classes derivadas que existiam apenas toowrap um objeto de modelo foram removidos. Olá classes restantes tiveram seu sufixo alterado de `Response` muito`Result`.

##### <a name="example"></a>Exemplo
Se o seu código tiver esta aparência:

    IndexerGetStatusResponse statusResponse = null;

    try
    {
        statusResponse = _searchClient.Indexers.GetStatus(indexer.Name);
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error polling for indexer status: {0}", ex.Message);
        return;
    }

    IndexerExecutionResult lastResult = statusResponse.ExecutionInfo.LastResult;

Você pode alterá-la toothis toofix qualquer erro de compilação:

    IndexerExecutionInfo status = null;

    try
    {
        status = _searchClient.Indexers.GetStatus(indexer.Name);
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error polling for indexer status: {0}", ex.Message);
        return;
    }

    IndexerExecutionResult lastResult = status.LastResult;

##### <a name="response-classes-and-ienumerable"></a>Classes de resposta e IEnumerable
Outra alteração que pode afetar o código é que as classes de resposta que contêm coleções não implementam mais `IEnumerable<T>`. Em vez disso, você pode acessar diretamente as propriedade de coleção de saudação. Por exemplo, se o seu código tiver esta aparência:

    DocumentSearchResponse<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response)
    {
        Console.WriteLine(result.Document);
    }

Você pode alterá-la toothis toofix qualquer erro de compilação:

    DocumentSearchResult<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response.Results)
    {
        Console.WriteLine(result.Document);
    }

##### <a name="special-case-for-web-applications"></a>Caso especial para aplicativos Web
Se você tiver um aplicativo web que serializa `DocumentSearchResponse` diretamente os resultados da pesquisa de toosend toohello navegador, você precisará toochange seu código ou resultados de saudação não irá serializar corretamente. Por exemplo, se o seu código tiver esta aparência:

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want toosearch everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q)
        };
    }

Você pode alterá-lo, obtendo Olá `.Results` propriedade de processamento de resultados de pesquisa Olá pesquisa resposta toofix:

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want toosearch everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q).Results
        };
    }

Você terá toolook para esses casos em seu código. **compilador Olá não emitirá um aviso** porque `JsonResult.Data` é do tipo `object`.

#### <a name="cloudexception-changes"></a>Alterações de CloudException
Olá `CloudException` classe foi movido de saudação `Hyak.Common` toohello namespace `Microsoft.Rest.Azure` namespace. Além disso, sua `Error` propriedade foi renomeada muito`Body`.

#### <a name="searchserviceclient-and-searchindexclient-changes"></a>Alterações de SearchServiceClient e SearchIndexClient
Olá tipo de saudação `Credentials` propriedade foi alterada de `SearchCredentials` tooits classe de base `ServiceClientCredentials`. Se você precisar Olá tooaccess `SearchCredentials` de um `SearchIndexClient` ou `SearchServiceClient`, use Olá novo `SearchCredentials` propriedade.

Em versões mais antigas do hello SDK, `SearchServiceClient` e `SearchIndexClient` tinha construtores que levaram um `HttpClient` parâmetro. Eles foram substituídos por construtores que usam um `HttpClientHandler` e uma matriz de objetos `DelegatingHandler`. Isso torna mais fácil tooinstall manipuladores personalizados toopre processo solicitações HTTP se necessário.

Por fim, Olá construtores que levaram um `Uri` e `SearchCredentials` foram alterados. Por exemplo, se você tiver código parecido com este:

    var client =
        new SearchServiceClient(
            new SearchCredentials("abc123"),
            new Uri("http://myservice.search.windows.net"));

Você pode alterá-la toothis toofix qualquer erro de compilação:

    var client =
        new SearchServiceClient(
            new Uri("http://myservice.search.windows.net"),
            new SearchCredentials("abc123"));

Também Observe que o tipo de saudação do hello credenciais parâmetro mudou muito`ServiceClientCredentials`. Isso é improvável que tooaffect seu código desde `SearchCredentials` é derivado de `ServiceClientCredentials`.

#### <a name="passing-a-request-id"></a>Passando uma ID de solicitação
Em versões mais antigas do hello SDK, você pode definir uma ID de solicitação em Olá `SearchServiceClient` ou `SearchIndexClient` e deve ser incluído em cada solicitação toohello API REST. Isso é útil para solucionar problemas com o serviço de pesquisa, se você precisar de suporte de toocontact. No entanto, é mais útil tooset uma ID de solicitação exclusivo para cada operação em vez de toouse Olá a mesma ID para todas as operações. Por esse motivo, Olá `SetClientRequestId` métodos de `SearchServiceClient` e `SearchIndexClient` foram removidos. Em vez disso, você pode passar um método de operação de tooeach de ID de solicitação por meio de saudação opcional `SearchRequestOptions` parâmetro.

> [!NOTE]
> Em uma versão futura do hello SDK, vamos adicionar um novo mecanismo para configurar uma ID de solicitação globalmente em cliente hello, objetos que é consistente com a abordagem de saudação usada por outros SDKs do Azure.
> 
> 

#### <a name="example"></a>Exemplo
Se você tiver um código parecido com este:

    client.SetClientRequestId(Guid.NewGuid());
    ...
    long count = client.Documents.Count();

Você pode alterá-la toothis toofix qualquer erro de compilação:

    long count = client.Documents.Count(new SearchRequestOptions(requestId: Guid.NewGuid()));

#### <a name="interface-name-changes"></a>Alterações de nome de interface
nomes de interface do grupo de operação Olá ter todos os toobe alterados consistente com os nomes de propriedade correspondentes:

* Olá tipo de `ISearchServiceClient.Indexes` foi renomeado de `IIndexOperations` muito`IIndexesOperations`.
* Olá tipo de `ISearchServiceClient.Indexers` foi renomeado de `IIndexerOperations` muito`IIndexersOperations`.
* Olá tipo de `ISearchServiceClient.DataSources` foi renomeado de `IDataSourceOperations` muito`IDataSourcesOperations`.
* Olá tipo de `ISearchIndexClient.Documents` foi renomeado de `IDocumentOperations` muito`IDocumentsOperations`.

Essa alteração é improvável que tooaffect seu código, a menos que você criou as simulações dessas interfaces para fins de teste.

<a name="BugFixesV1"></a>

### <a name="bug-fixes-in-version-11"></a>Correções de bug na versão 1.1
Havia um bug nas versões anteriores do SDK .NET da pesquisa do Azure de saudação tooserialization relacionado de classes de modelo personalizado. bug Olá pode ocorrer se você tiver criado uma classe de modelo personalizado com uma propriedade de um tipo de valor não nulo.

#### <a name="steps-tooreproduce"></a>Etapas tooreproduce
Crie uma classe de modelo personalizada com uma propriedade de tipo de valor não anulável. Por exemplo, adicione uma propriedade `UnitCount` pública do tipo `int` em vez de `int?`.

Se você indexar um documento com o valor padrão de saudação do mesmo tipo (por exemplo, 0 para `int`), o campo de saudação será nulo na pesquisa do Azure. Se você pesquisar posteriormente para o documento, Olá `Search` chamada lançará `JsonSerializationException` indicando que não é possível converter `null` muito`int`.

Além disso, os filtros podem não funcionar conforme o esperado como nulo foi escrito toohello índice em vez do valor de saudação que se destina.

#### <a name="fix-details"></a>Corrigir detalhes
Corrigimos o problema na versão 1.1 do hello SDK. Agora, se você tiver uma classe de modelo como esta:

    public class Model
    {
        public string Key { get; set; }

        public int IntValue { get; set; }
    }

e você definir `IntValue` too0, que valor agora está corretamente serializado como 0 na transmissão de saudação e armazenado como 0 no índice de saudação. A viagem de ida e volta também funciona conforme o esperado.

Há um toobe problema potencial atento com essa abordagem: se você usar um tipo de modelo com uma propriedade não anulável, você tem muito**garante** sem documentos no índice contêm um valor nulo para o campo correspondente do hello. Olá SDK, nem Olá API de REST de pesquisa do Azure ajudará você tooenforce isso.

Isso não é apenas uma preocupação hipotética: Imagine um cenário em que você adicionar um novo campo tooan índice existente que é do tipo `Edm.Int32`. Depois de atualizar a definição de índice hello, todos os documentos terá um valor nulo para esse novo campo (desde que todos os tipos são anuláveis na pesquisa do Azure). Se você usar uma classe de modelo com um não anulável `int` propriedade para esse campo, você receberá um `JsonSerializationException` assim ao tentar tooretrieve documentos:

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

Por esse motivo, continuamos a recomendar que você use tipos anuláveis nas suas classes de modelo como uma prática recomendada.

Para obter mais detalhes sobre essa correção de bug e hello, consulte [esse problema no GitHub](https://github.com/Azure/azure-sdk-for-net/issues/1063).

