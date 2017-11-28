---
title: "Atualizando para o SDK do .NET do Azure Search versão 1.1 | Microsoft Docs"
description: "Atualizando para o SDK do .NET da Pesquisa do Azure versão 1.1"
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
ms.openlocfilehash: 9782454e3bfc697b63cde8aa28a14be0c393c36b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="upgrading-to-the-azure-search-net-sdk-version-3"></a><span data-ttu-id="b084d-103">Atualizando para o SDK do .NET do Azure Search versão 3</span><span class="sxs-lookup"><span data-stu-id="b084d-103">Upgrading to the Azure Search .NET SDK version 3</span></span>
<span data-ttu-id="b084d-104">Se você estiver usando a visualização da versão 2.0 ou mais antiga do [SDK .NET do Azure Search](https://aka.ms/search-sdk), este artigo ajudará você a atualizar seu aplicativo para usar a versão 3, mais recente.</span><span class="sxs-lookup"><span data-stu-id="b084d-104">If you're using version 2.0-preview or older of the [Azure Search .NET SDK](https://aka.ms/search-sdk), this article will help you upgrade your application to use version 3.</span></span>

<span data-ttu-id="b084d-105">Para obter uma explicação mais geral do SDK, incluindo exemplos, confira [Como usar a Pesquisa do Azure de um aplicativo .NET](search-howto-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="b084d-105">For a more general walkthrough of the SDK including examples, see [How to use Azure Search from a .NET Application](search-howto-dotnet-sdk.md).</span></span>

<span data-ttu-id="b084d-106">A versão 3 do SDK do .NET do Azure Search contém algumas alterações de versões anteriores.</span><span class="sxs-lookup"><span data-stu-id="b084d-106">Version 3 of the Azure Search .NET SDK contains some changes from earlier versions.</span></span> <span data-ttu-id="b084d-107">A maioria das alterações é leve e, portanto, a alteração do seu código não deve exigir muito.</span><span class="sxs-lookup"><span data-stu-id="b084d-107">These are mostly minor, so changing your code should require only minimal effort.</span></span> <span data-ttu-id="b084d-108">Confira [Etapas da atualização](#UpgradeSteps) para obter instruções sobre como alterar o seu código para usar a nova versão do SDK.</span><span class="sxs-lookup"><span data-stu-id="b084d-108">See [Steps to upgrade](#UpgradeSteps) for instructions on how to change your code to use the new SDK version.</span></span>

> [!NOTE]
> <span data-ttu-id="b084d-109">Se você estiver usando a visualização da versão 1.0.2 ou mais antiga, será necessário primeiro atualizar para a versão 1.1 e, em seguida, atualizar para a versão 3.</span><span class="sxs-lookup"><span data-stu-id="b084d-109">If you're using version 1.0.2-preview or older, you should upgrade to version 1.1 first, and then upgrade to version 3.</span></span> <span data-ttu-id="b084d-110">Veja [Apêndice: Etapas para atualizar para a versão 1.1](#UpgradeStepsV1) para obter instruções.</span><span class="sxs-lookup"><span data-stu-id="b084d-110">See [Appendix: Steps to upgrade to version 1.1](#UpgradeStepsV1) for instructions.</span></span>
>
> <span data-ttu-id="b084d-111">Sua instância de serviço do Azure Search dá suporte a várias versões da API REST, incluindo a última.</span><span class="sxs-lookup"><span data-stu-id="b084d-111">Your Azure Search service instance supports several REST API versions, including the latest one.</span></span> <span data-ttu-id="b084d-112">Você pode continuar usando uma versão quando ela não for mais a última, mas aconselhamos a migrar seu código para usar a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="b084d-112">You can continue to use a version when it is no longer the latest one, but we recommend that you migrate your code to use the newest version.</span></span> <span data-ttu-id="b084d-113">Ao usar a API REST, você deve especificar a versão da API em cada solicitação por meio do parâmetro api-version.</span><span class="sxs-lookup"><span data-stu-id="b084d-113">When using the REST API, you must specify the API version in every request via the api-version parameter.</span></span> <span data-ttu-id="b084d-114">Ao usar o SDK do .NET, a versão do SDK que você está usando determina a versão correspondente da API REST.</span><span class="sxs-lookup"><span data-stu-id="b084d-114">When using the .NET SDK, the version of the SDK you’re using determines the corresponding version of the REST API.</span></span> <span data-ttu-id="b084d-115">Se estiver usando um SDK mais antigo, você poderá continuar executando esse código sem alterações, mesmo se o serviço for atualizado para dar suporte a uma versão de API mais recente.</span><span class="sxs-lookup"><span data-stu-id="b084d-115">If you are using an older SDK, you can continue to run that code with no changes even if the service is upgraded to support a newer API version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-3"></a><span data-ttu-id="b084d-116">Novidades na versão 3</span><span class="sxs-lookup"><span data-stu-id="b084d-116">What's new in version 3</span></span>
<span data-ttu-id="b084d-117">A versão 3 do SDK do .NET do Azure Search destina-se à versão mais recente disponível da API REST do Azure Search, especificamente a 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="b084d-117">Version 3 of the Azure Search .NET SDK targets the latest generally available version of the Azure Search REST API, specifically 2016-09-01.</span></span> <span data-ttu-id="b084d-118">Isso possibilita o uso de vários recursos novos do Azure Search por meio de um aplicativo .NET, incluindo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="b084d-118">This makes it possible to use many new features of Azure Search from a .NET application, including the following:</span></span>

* [<span data-ttu-id="b084d-119">Analisadores personalizados</span><span class="sxs-lookup"><span data-stu-id="b084d-119">Custom analyzers</span></span>](https://aka.ms/customanalyzers)
* <span data-ttu-id="b084d-120">Suporte do indexador do [Armazenamento de Blobs do Azure](search-howto-indexing-azure-blob-storage.md) e do [Armazenamento de Tabelas do Azure](search-howto-indexing-azure-tables.md)</span><span class="sxs-lookup"><span data-stu-id="b084d-120">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexer support</span></span>
* <span data-ttu-id="b084d-121">Personalização do indexador por meio de [mapeamentos de campo](search-indexer-field-mappings.md)</span><span class="sxs-lookup"><span data-stu-id="b084d-121">Indexer customization via [field mappings](search-indexer-field-mappings.md)</span></span>
* <span data-ttu-id="b084d-122">O ETags dá suporte à habilitação da atualização simultânea segura de definições de índice, indexadores e fontes de dados</span><span class="sxs-lookup"><span data-stu-id="b084d-122">ETags support to enable safe concurrent updating of index definitions, indexers, and data sources</span></span>
* <span data-ttu-id="b084d-123">Suporte para a criação de definições de campo de índice declarativamente decorando a classe de modelo e usando a nova classe `FieldBuilder`.</span><span class="sxs-lookup"><span data-stu-id="b084d-123">Support for building index field definitions declaratively by decorating your model class and using the new `FieldBuilder` class.</span></span>
* <span data-ttu-id="b084d-124">Suporte para .NET Core e .NET Portable Profile 111</span><span class="sxs-lookup"><span data-stu-id="b084d-124">Support for .NET Core and .NET Portable Profile 111</span></span>

<a name="UpgradeSteps"></a>

## <a name="steps-to-upgrade"></a><span data-ttu-id="b084d-125">Etapas da atualização</span><span class="sxs-lookup"><span data-stu-id="b084d-125">Steps to upgrade</span></span>
<span data-ttu-id="b084d-126">Primeiro, atualize sua referência NuGet para `Microsoft.Azure.Search` usando o Console do Gerenciador de Pacotes NuGet ou clicando com o botão direito do mouse nas referências do projeto e selecionando “Gerenciar pacotes NuGet...” no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b084d-126">First, update your NuGet reference for `Microsoft.Azure.Search` using either the NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.</span></span>

<span data-ttu-id="b084d-127">Depois que o NuGet tiver baixado os novos pacotes e suas dependências, recompile o projeto.</span><span class="sxs-lookup"><span data-stu-id="b084d-127">Once NuGet has downloaded the new packages and their dependencies, rebuild your project.</span></span> <span data-ttu-id="b084d-128">Dependendo de como o código está estruturado, ele poderá ser recriado com êxito.</span><span class="sxs-lookup"><span data-stu-id="b084d-128">Depending on how your code is structured, it may rebuild successfully.</span></span> <span data-ttu-id="b084d-129">Nesse caso, você está pronto para começar!</span><span class="sxs-lookup"><span data-stu-id="b084d-129">If so, you're ready to go!</span></span>

<span data-ttu-id="b084d-130">Se o build falhar, você verá um erro de build semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="b084d-130">If your build fails, you should see a build error like the following:</span></span>

    Program.cs(31,45,31,86): error CS0266: Cannot implicitly convert type 'Microsoft.Azure.Search.ISearchIndexClient' to 'Microsoft.Azure.Search.SearchIndexClient'. An explicit conversion exists (are you missing a cast?)

<span data-ttu-id="b084d-131">A próxima etapa é corrigir esse erro de build.</span><span class="sxs-lookup"><span data-stu-id="b084d-131">The next step is to fix this build error.</span></span> <span data-ttu-id="b084d-132">Veja [Alterações significativas na versão 3](#ListOfChanges) para ver mais detalhes sobre a causa do erro e como corrigi-lo.</span><span class="sxs-lookup"><span data-stu-id="b084d-132">See [Breaking changes in version 3](#ListOfChanges) for details on what causes the error and how to fix it.</span></span>

<span data-ttu-id="b084d-133">Você pode ver avisos de build adicionais relacionados a propriedades ou métodos obsoletos.</span><span class="sxs-lookup"><span data-stu-id="b084d-133">You may see additional build warnings related to obsolete methods or properties.</span></span> <span data-ttu-id="b084d-134">Os avisos incluirão instruções sobre o que deve ser usado no lugar do recurso preterido.</span><span class="sxs-lookup"><span data-stu-id="b084d-134">The warnings will include instructions on what to use instead of the deprecated feature.</span></span> <span data-ttu-id="b084d-135">Por exemplo, se seu aplicativo usar a propriedade `IndexingParameters.Base64EncodeKeys`, você deverá obter um aviso que diz `"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`</span><span class="sxs-lookup"><span data-stu-id="b084d-135">For example, if your application uses the `IndexingParameters.Base64EncodeKeys` property, you should get a warning that says `"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`</span></span>

<span data-ttu-id="b084d-136">Depois de corrigir os erros de build, será possível fazer alterações em seu aplicativo para tirar proveito da nova funcionalidade, se desejar.</span><span class="sxs-lookup"><span data-stu-id="b084d-136">Once you've fixed any build errors, you can make changes to your application to take advantage of new functionality if you wish.</span></span> <span data-ttu-id="b084d-137">Novos recursos no SDK são detalhados em [Novidades na versão 3](#WhatsNew).</span><span class="sxs-lookup"><span data-stu-id="b084d-137">New features in the SDK are detailed in [What's new in version 3](#WhatsNew).</span></span>

<a name="ListOfChanges"></a>

## <a name="breaking-changes-in-version-3"></a><span data-ttu-id="b084d-138">Alterações significativas na versão 3</span><span class="sxs-lookup"><span data-stu-id="b084d-138">Breaking changes in version 3</span></span>
<span data-ttu-id="b084d-139">Há algumas alterações significativas na versão 3 que podem exigir alterações de código, além da recompilação do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b084d-139">There a small number of breaking changes in version 3 that may require code changes in addition to rebuilding your application.</span></span>

### <a name="indexesgetclient-return-type"></a><span data-ttu-id="b084d-140">Tipo de retorno de Indexes.GetClient</span><span class="sxs-lookup"><span data-stu-id="b084d-140">Indexes.GetClient return type</span></span>
<span data-ttu-id="b084d-141">O método `Indexes.GetClient` contém um novo tipo de retorno.</span><span class="sxs-lookup"><span data-stu-id="b084d-141">The `Indexes.GetClient` method has a new return type.</span></span> <span data-ttu-id="b084d-142">Anteriormente, ele retornava `SearchIndexClient`, mas isso foi alterado para `ISearchIndexClient` na visualização da versão 2.0 e essa alteração foi trazida para a versão 3.</span><span class="sxs-lookup"><span data-stu-id="b084d-142">Previously, it returned `SearchIndexClient`, but this was changed to `ISearchIndexClient` in version 2.0-preview, and that change carries over to version 3.</span></span> <span data-ttu-id="b084d-143">Essa mudança ocorreu para dar suporte a clientes que querem simular o método `GetClient` para testes de unidade retornando uma implementação fictícia do `ISearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="b084d-143">This is to support customers that wish to mock the `GetClient` method for unit tests by returning a mock implementation of `ISearchIndexClient`.</span></span>

#### <a name="example"></a><span data-ttu-id="b084d-144">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b084d-144">Example</span></span>
<span data-ttu-id="b084d-145">Se o seu código tiver esta aparência:</span><span class="sxs-lookup"><span data-stu-id="b084d-145">If your code looks like this:</span></span>

```csharp
SearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

<span data-ttu-id="b084d-146">Você poderá alterá-lo para corrigir os erros de compilação:</span><span class="sxs-lookup"><span data-stu-id="b084d-146">You can change it to this to fix any build errors:</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

### <a name="analyzername-datatype-and-others-are-no-longer-implicitly-convertible-to-strings"></a><span data-ttu-id="b084d-147">AnalyzerName, DataType e outros não são implicitamente conversíveis para cadeias de caracteres</span><span class="sxs-lookup"><span data-stu-id="b084d-147">AnalyzerName, DataType, and others are no longer implicitly convertible to strings</span></span>
<span data-ttu-id="b084d-148">Há muitos tipos no SDK do .NET do Azure Search que derivam de `ExtensibleEnum`.</span><span class="sxs-lookup"><span data-stu-id="b084d-148">There are many types in the Azure Search .NET SDK that derive from `ExtensibleEnum`.</span></span> <span data-ttu-id="b084d-149">Antes, todos esses tipos eram implicitamente conversíveis para o tipo `string`.</span><span class="sxs-lookup"><span data-stu-id="b084d-149">Previously these types were all implicitly convertible to type `string`.</span></span> <span data-ttu-id="b084d-150">No entanto, um bug foi descoberto na implementação `Object.Equals` para essas classes e foi necessário desabilitar essa conversão implícita para corrigi-lo.</span><span class="sxs-lookup"><span data-stu-id="b084d-150">However, a bug was discovered in the `Object.Equals` implementation for these classes, and fixing the bug required disabling this implicit conversion.</span></span> <span data-ttu-id="b084d-151">A conversão explícita para `string` ainda é permitida.</span><span class="sxs-lookup"><span data-stu-id="b084d-151">Explicit conversion to `string` is still allowed.</span></span>

#### <a name="example"></a><span data-ttu-id="b084d-152">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b084d-152">Example</span></span>
<span data-ttu-id="b084d-153">Se o seu código tiver esta aparência:</span><span class="sxs-lookup"><span data-stu-id="b084d-153">If your code looks like this:</span></span>

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

<span data-ttu-id="b084d-154">Você poderá alterá-lo para corrigir os erros de compilação:</span><span class="sxs-lookup"><span data-stu-id="b084d-154">You can change it to this to fix any build errors:</span></span>

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

### <a name="removed-obsolete-members"></a><span data-ttu-id="b084d-155">Remover membros obsoletos</span><span class="sxs-lookup"><span data-stu-id="b084d-155">Removed obsolete members</span></span>

<span data-ttu-id="b084d-156">Você pode ver erros de build relacionados a métodos ou propriedades que foram marcados como obsoletos na visualização da versão 2.0 e subsequentemente removidos na versão 3.</span><span class="sxs-lookup"><span data-stu-id="b084d-156">You may see build errors related to methods or properties that were marked as obsolete in version 2.0-preview and subsequently removed in version 3.</span></span> <span data-ttu-id="b084d-157">Se você encontrar esses erros, veja aqui como resolvê-los:</span><span class="sxs-lookup"><span data-stu-id="b084d-157">If you encounter such errors, here is how to resolve them:</span></span>

- <span data-ttu-id="b084d-158">Se usava o construtor: `ScoringParameter(string name, string value)`, use este em vez dele: `ScoringParameter(string name, IEnumerable<string> values)`</span><span class="sxs-lookup"><span data-stu-id="b084d-158">If you were using this constructor: `ScoringParameter(string name, string value)`, use this one instead: `ScoringParameter(string name, IEnumerable<string> values)`</span></span>
- <span data-ttu-id="b084d-159">Se você estiver usando a propriedade `ScoringParameter.Value`, use a propriedade `ScoringParameter.Values` ou o método `ToString` em vez dela.</span><span class="sxs-lookup"><span data-stu-id="b084d-159">If you were using the `ScoringParameter.Value` property, use the `ScoringParameter.Values` property or the `ToString` method instead.</span></span>
- <span data-ttu-id="b084d-160">Se você estiver usando a propriedade `SearchRequestOptions.RequestId`, use a propriedade `ClientRequestId` em vez dela.</span><span class="sxs-lookup"><span data-stu-id="b084d-160">If you were using the `SearchRequestOptions.RequestId` property, use the `ClientRequestId` property instead.</span></span>

### <a name="removed-preview-features"></a><span data-ttu-id="b084d-161">Recursos de visualização removidos</span><span class="sxs-lookup"><span data-stu-id="b084d-161">Removed preview features</span></span>

<span data-ttu-id="b084d-162">Se você estiver atualizando da visualização da versão 2.0 para a versão 3, lembre-se de que o suporte a análise JSON e CSV para a indexadores de Blobs foi removido, visto que esses recursos ainda estão em visualização.</span><span class="sxs-lookup"><span data-stu-id="b084d-162">If you are upgrading from version 2.0-preview to version 3, be aware that JSON and CSV parsing support for Blob Indexers has been removed since these features are still in preview.</span></span> <span data-ttu-id="b084d-163">Especificamente, os seguintes métodos da classe `IndexingParametersExtensions` foram removidos:</span><span class="sxs-lookup"><span data-stu-id="b084d-163">Specifically, the following methods of the `IndexingParametersExtensions` class have been removed:</span></span>

- `ParseJson`
- `ParseJsonArrays`
- `ParseDelimitedTextFiles`

<span data-ttu-id="b084d-164">Se seu aplicativo tiver uma dependência rígida desses recursos, você não poderá atualizar para a versão 3 do SDK do .NET do Azure Search.</span><span class="sxs-lookup"><span data-stu-id="b084d-164">If your application has a hard dependency on these features, you will not be able to upgrade to version 3 of the Azure Search .NET SDK.</span></span> <span data-ttu-id="b084d-165">Você pode continuar a usar a visualização da versão 2.0.</span><span class="sxs-lookup"><span data-stu-id="b084d-165">You can continue to use version 2.0-preview.</span></span> <span data-ttu-id="b084d-166">No entanto, lembre-se que **não é recomendável usar SDKs de visualização em aplicativos de produção**.</span><span class="sxs-lookup"><span data-stu-id="b084d-166">However, please keep in mind that **we do not recommend using preview SDKs in production applications**.</span></span> <span data-ttu-id="b084d-167">Os recursos de visualização destinam-se apenas a fins de avaliação e podem ser alterados.</span><span class="sxs-lookup"><span data-stu-id="b084d-167">Preview features are for evaluation only and may change.</span></span>

## <a name="conclusion"></a><span data-ttu-id="b084d-168">Conclusão</span><span class="sxs-lookup"><span data-stu-id="b084d-168">Conclusion</span></span>
<span data-ttu-id="b084d-169">Se precisar de mais detalhes sobre como usar o SDK do .NET da Pesquisa do Azure, confira nosso [Tutorial](search-howto-dotnet-sdk.md)recém-atualizado.</span><span class="sxs-lookup"><span data-stu-id="b084d-169">If you need more details on using the Azure Search .NET SDK, see our recently updated [How-to](search-howto-dotnet-sdk.md).</span></span>

<span data-ttu-id="b084d-170">Apreciamos os seus comentários sobre o SDK.</span><span class="sxs-lookup"><span data-stu-id="b084d-170">We welcome your feedback on the SDK.</span></span> <span data-ttu-id="b084d-171">Se tiver problemas, fique à vontade para solicitar ajuda no [Fórum do MSDN sobre a Pesquisa do Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch).</span><span class="sxs-lookup"><span data-stu-id="b084d-171">If you encounter problems, feel free to ask us for help on the [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch).</span></span> <span data-ttu-id="b084d-172">Se encontrar um bug, você poderá apresentar um problema no [repositório GitHub sobre o SDK do .NET do Azure](https://github.com/Azure/azure-sdk-for-net/issues).</span><span class="sxs-lookup"><span data-stu-id="b084d-172">If you find a bug, you can file an issue in the [Azure .NET SDK GitHub repository](https://github.com/Azure/azure-sdk-for-net/issues).</span></span> <span data-ttu-id="b084d-173">Não deixe de colocar o prefixo "SDK da Pesquisa:" no título do problema.</span><span class="sxs-lookup"><span data-stu-id="b084d-173">Make sure to prefix your issue title with "Search SDK: ".</span></span>

<span data-ttu-id="b084d-174">Obrigado por usar a Pesquisa do Azure!</span><span class="sxs-lookup"><span data-stu-id="b084d-174">Thank you for using Azure Search!</span></span>

<a name="UpgradeStepsV1"></a>

## <a name="appendix-steps-to-upgrade-to-version-11"></a><span data-ttu-id="b084d-175">Apêndice: Etapas para atualizar para a versão 1.1</span><span class="sxs-lookup"><span data-stu-id="b084d-175">Appendix: Steps to upgrade to version 1.1</span></span>
> [!NOTE]
> <span data-ttu-id="b084d-176">Esta seção se aplica somente aos usuários do SDK do .NET do Azure Search visualização da versão 1.0.2 e anteriores.</span><span class="sxs-lookup"><span data-stu-id="b084d-176">This section applies only to users of the Azure Search .NET SDK version 1.0.2-preview and older.</span></span>
> 
> 

<span data-ttu-id="b084d-177">Primeiro, atualize sua referência NuGet para `Microsoft.Azure.Search` usando o Console do Gerenciador de Pacotes NuGet ou clicando com o botão direito do mouse nas referências do projeto e selecionando “Gerenciar pacotes NuGet...” no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b084d-177">First, update your NuGet reference for `Microsoft.Azure.Search` using either the NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.</span></span>

<span data-ttu-id="b084d-178">Depois que o NuGet tiver baixado os novos pacotes e suas dependências, recompile o projeto.</span><span class="sxs-lookup"><span data-stu-id="b084d-178">Once NuGet has downloaded the new packages and their dependencies, rebuild your project.</span></span>

<span data-ttu-id="b084d-179">Se você estava usando a versão 1.0.0-preview, 1.0.1-preview ou 1.0.2-preview anteriormente, o build deve ter êxito e você estará pronto para começar!</span><span class="sxs-lookup"><span data-stu-id="b084d-179">If you were previously using version 1.0.0-preview, 1.0.1-preview, or 1.0.2-preview, the build should succeed and you're ready to go!</span></span>

<span data-ttu-id="b084d-180">Se estava usando a versão 0.13.0-preview ou mais antiga anteriormente, você deve ver erros de build como o seguinte:</span><span class="sxs-lookup"><span data-stu-id="b084d-180">If you were previously using version 0.13.0-preview or older, you should see build errors like the following:</span></span>

    Program.cs(137,56,137,62): error CS0117: 'Microsoft.Azure.Search.Models.IndexBatch' does not contain a definition for 'Create'
    Program.cs(137,99,137,105): error CS0117: 'Microsoft.Azure.Search.Models.IndexAction' does not contain a definition for 'Create'
    Program.cs(146,41,146,54): error CS1061: 'Microsoft.Azure.Search.IndexBatchException' does not contain a definition for 'IndexResponse' and no extension method 'IndexResponse' accepting a first argument of type 'Microsoft.Azure.Search.IndexBatchException' could be found (are you missing a using directive or an assembly reference?)
    Program.cs(163,13,163,42): error CS0246: The type or namespace name 'DocumentSearchResponse' could not be found (are you missing a using directive or an assembly reference?)

<span data-ttu-id="b084d-181">A próxima etapa é corrigir os erros de compilação individualmente.</span><span class="sxs-lookup"><span data-stu-id="b084d-181">The next step is to fix the build errors one by one.</span></span> <span data-ttu-id="b084d-182">A maioria exigirá a alteração de alguns nomes de classe e de método que foram renomeados no SDK.</span><span class="sxs-lookup"><span data-stu-id="b084d-182">Most will require changing some class and method names that have been renamed in the SDK.</span></span> <span data-ttu-id="b084d-183">[Lista de alterações significativas na versão 1.1](#ListOfChangesV1) contém uma lista dessas alterações de nome.</span><span class="sxs-lookup"><span data-stu-id="b084d-183">[List of breaking changes in version 1.1](#ListOfChangesV1) contains a list of these name changes.</span></span>

<span data-ttu-id="b084d-184">Se estiver usando classes personalizadas para modelar seus documentos e essas classes tiverem propriedades de tipos primitivos que não permitem valor nulo (por exemplo, `int` ou `bool` em C#), haverá uma correção de bug na versão 1.1 do SDK que você deverá reconhecer.</span><span class="sxs-lookup"><span data-stu-id="b084d-184">If you're using custom classes to model your documents, and those classes have properties of non-nullable primitive types (for example, `int` or `bool` in C#), there is a bug fix in the 1.1 version of the SDK of which you should be aware.</span></span> <span data-ttu-id="b084d-185">Veja [Correções de bug na versão 1.1](#BugFixesV1) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="b084d-185">See [Bug fixes in version 1.1](#BugFixesV1) for more details.</span></span>

<span data-ttu-id="b084d-186">Finalmente, depois de solucionar possíveis erros de compilação, você pode fazer alterações no seu aplicativo para tirar proveito da nova funcionalidade, se desejar.</span><span class="sxs-lookup"><span data-stu-id="b084d-186">Finally, once you've fixed any build errors, you can make changes to your application to take advantage of new functionality if you wish.</span></span>

<a name="ListOfChangesV1"></a>

### <a name="list-of-breaking-changes-in-version-11"></a><span data-ttu-id="b084d-187">Lista de alterações significativas na versão 1.1</span><span class="sxs-lookup"><span data-stu-id="b084d-187">List of breaking changes in version 1.1</span></span>
<span data-ttu-id="b084d-188">A lista a seguir é ordenada pela probabilidade de a alteração afetar o seu código de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b084d-188">The following list is ordered by the likelihood that the change will affect your application code.</span></span>

#### <a name="indexbatch-and-indexaction-changes"></a><span data-ttu-id="b084d-189">Alterações de IndexBatch e IndexAction</span><span class="sxs-lookup"><span data-stu-id="b084d-189">IndexBatch and IndexAction changes</span></span>
<span data-ttu-id="b084d-190">`IndexBatch.Create` foi renomeado para `IndexBatch.New` e não tem mais um argumento `params`.</span><span class="sxs-lookup"><span data-stu-id="b084d-190">`IndexBatch.Create` has been renamed to `IndexBatch.New` and no longer has a `params` argument.</span></span> <span data-ttu-id="b084d-191">Você pode usar `IndexBatch.New` para lotes que combinam tipos diferentes de ações (mesclagens, exclusões, etc.).</span><span class="sxs-lookup"><span data-stu-id="b084d-191">You can use `IndexBatch.New` for batches that mix different types of actions (merges, deletes, etc.).</span></span> <span data-ttu-id="b084d-192">Além disso, há novos métodos estáticos para a criação de lotes em que todas as ações são iguais: `Delete`, `Merge`, `MergeOrUpload` e `Upload`.</span><span class="sxs-lookup"><span data-stu-id="b084d-192">In addition, there are new static methods for creating batches where all the actions are the same: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.</span></span>

<span data-ttu-id="b084d-193">`IndexAction` não tem mais construtores públicos e suas propriedades agora são imutáveis.</span><span class="sxs-lookup"><span data-stu-id="b084d-193">`IndexAction` no longer has public constructors and its properties are now immutable.</span></span> <span data-ttu-id="b084d-194">Você deve usar os novos métodos estáticos para criar ações para finalidades diferentes: `Delete`, `Merge`, `MergeOrUpload` e `Upload`.</span><span class="sxs-lookup"><span data-stu-id="b084d-194">You should use the new static methods for creating actions for different purposes: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.</span></span> <span data-ttu-id="b084d-195">`IndexAction.Create` foi removido.</span><span class="sxs-lookup"><span data-stu-id="b084d-195">`IndexAction.Create` has been removed.</span></span> <span data-ttu-id="b084d-196">Se você usou a sobrecarga que utiliza apenas um documento, não deixe de usar `Upload` em seu lugar.</span><span class="sxs-lookup"><span data-stu-id="b084d-196">If you used the overload that takes only a document, make sure to use `Upload` instead.</span></span>

##### <a name="example"></a><span data-ttu-id="b084d-197">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b084d-197">Example</span></span>
<span data-ttu-id="b084d-198">Se o seu código tiver esta aparência:</span><span class="sxs-lookup"><span data-stu-id="b084d-198">If your code looks like this:</span></span>

    var batch = IndexBatch.Create(documents.Select(doc => IndexAction.Create(doc)));
    indexClient.Documents.Index(batch);

<span data-ttu-id="b084d-199">Você poderá alterá-lo para corrigir os erros de compilação:</span><span class="sxs-lookup"><span data-stu-id="b084d-199">You can change it to this to fix any build errors:</span></span>

    var batch = IndexBatch.New(documents.Select(doc => IndexAction.Upload(doc)));
    indexClient.Documents.Index(batch);

<span data-ttu-id="b084d-200">Se desejar, você pode simplificar ainda mais:</span><span class="sxs-lookup"><span data-stu-id="b084d-200">If you want, you can further simplify it to this:</span></span>

    var batch = IndexBatch.Upload(documents);
    indexClient.Documents.Index(batch);

#### <a name="indexbatchexception-changes"></a><span data-ttu-id="b084d-201">Alterações de IndexBatchException</span><span class="sxs-lookup"><span data-stu-id="b084d-201">IndexBatchException changes</span></span>
<span data-ttu-id="b084d-202">A propriedade `IndexBatchException.IndexResponse` foi renomeada para `IndexingResults` e seu tipo agora é `IList<IndexingResult>`.</span><span class="sxs-lookup"><span data-stu-id="b084d-202">The `IndexBatchException.IndexResponse` property has been renamed to `IndexingResults`, and its type is now `IList<IndexingResult>`.</span></span>

##### <a name="example"></a><span data-ttu-id="b084d-203">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b084d-203">Example</span></span>
<span data-ttu-id="b084d-204">Se o seu código tiver esta aparência:</span><span class="sxs-lookup"><span data-stu-id="b084d-204">If your code looks like this:</span></span>

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed to index some of the documents: {0}",
            String.Join(", ", e.IndexResponse.Results.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<span data-ttu-id="b084d-205">Você poderá alterá-lo para corrigir os erros de compilação:</span><span class="sxs-lookup"><span data-stu-id="b084d-205">You can change it to this to fix any build errors:</span></span>

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed to index some of the documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<a name="OperationMethodChanges"></a>

#### <a name="operation-method-changes"></a><span data-ttu-id="b084d-206">Alterações de método de operação</span><span class="sxs-lookup"><span data-stu-id="b084d-206">Operation method changes</span></span>
<span data-ttu-id="b084d-207">Cada operação no SDK .NET da Pesquisa do Azure é exposta como um conjunto de sobrecargas de método para chamadores síncronos e assíncronos.</span><span class="sxs-lookup"><span data-stu-id="b084d-207">Each operation in the Azure Search .NET SDK is exposed as a set of method overloads for synchronous and asynchronous callers.</span></span> <span data-ttu-id="b084d-208">As assinaturas e a fatoração dessas sobrecargas de método mudaram na versão 1.1.</span><span class="sxs-lookup"><span data-stu-id="b084d-208">The signatures and factoring of these method overloads has changed in version 1.1.</span></span>

<span data-ttu-id="b084d-209">Por exemplo, a operação "Obter Estatísticas de Índice" em versões mais antigas do SDK expunham estas assinaturas:</span><span class="sxs-lookup"><span data-stu-id="b084d-209">For example, the "Get Index Statistics" operation in older versions of the SDK exposed these signatures:</span></span>

<span data-ttu-id="b084d-210">Em `IIndexOperations`:</span><span class="sxs-lookup"><span data-stu-id="b084d-210">In `IIndexOperations`:</span></span>

    // Asynchronous operation with all parameters
    Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        string indexName,
        CancellationToken cancellationToken);

<span data-ttu-id="b084d-211">Em `IndexOperationsExtensions`:</span><span class="sxs-lookup"><span data-stu-id="b084d-211">In `IndexOperationsExtensions`:</span></span>

    // Asynchronous operation with only required parameters
    public static Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        this IIndexOperations operations,
        string indexName);

    // Synchronous operation with only required parameters
    public static IndexGetStatisticsResponse GetStatistics(
        this IIndexOperations operations,
        string indexName);

<span data-ttu-id="b084d-212">As assinaturas de método para a mesma operação na versão 1.1 têm esta aparência:</span><span class="sxs-lookup"><span data-stu-id="b084d-212">The method signatures for the same operation in version 1.1 look like this:</span></span>

<span data-ttu-id="b084d-213">Em `IIndexesOperations`:</span><span class="sxs-lookup"><span data-stu-id="b084d-213">In `IIndexesOperations`:</span></span>

    // Asynchronous operation with lower-level HTTP features exposed
    Task<AzureOperationResponse<IndexGetStatisticsResult>> GetStatisticsWithHttpMessagesAsync(
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        Dictionary<string, List<string>> customHeaders = null,
        CancellationToken cancellationToken = default(CancellationToken));

<span data-ttu-id="b084d-214">Em `IndexesOperationsExtensions`:</span><span class="sxs-lookup"><span data-stu-id="b084d-214">In `IndexesOperationsExtensions`:</span></span>

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

<span data-ttu-id="b084d-215">O SDK do .NET da Pesquisa do Azure, a partir da versão 1.1, organiza os métodos de operação de maneira diferente:</span><span class="sxs-lookup"><span data-stu-id="b084d-215">Starting with version 1.1, the Azure Search .NET SDK organizes operation methods differently:</span></span>

* <span data-ttu-id="b084d-216">Os parâmetros opcionais agora são modelados como padrão em vez de sobrecargas de método adicionais.</span><span class="sxs-lookup"><span data-stu-id="b084d-216">Optional parameters are now modeled as default parameters rather than additional method overloads.</span></span> <span data-ttu-id="b084d-217">Isso reduz o número de sobrecargas de método, às vezes drasticamente.</span><span class="sxs-lookup"><span data-stu-id="b084d-217">This reduces the number of method overloads, sometimes dramatically.</span></span>
* <span data-ttu-id="b084d-218">Os métodos de extensão agora ocultam muitos dos detalhes não essenciais de HTTP do chamador.</span><span class="sxs-lookup"><span data-stu-id="b084d-218">The extension methods now hide a lot of the extraneous details of HTTP from the caller.</span></span> <span data-ttu-id="b084d-219">Por exemplo, as versões mais antigas do SDK retornavam um objeto de resposta com um código de status HTTP, que normalmente não é verificado, porque os métodos de operação geram `CloudException` para qualquer código de status que indique um erro.</span><span class="sxs-lookup"><span data-stu-id="b084d-219">For example, older versions of the SDK returned a response object with an HTTP status code, which you often didn't need to check because operation methods throw `CloudException` for any status code that indicates an error.</span></span> <span data-ttu-id="b084d-220">Os novos métodos de extensão retornam apenas objetos de modelo, evitando que você tenha de desencapsulá-los em seu código.</span><span class="sxs-lookup"><span data-stu-id="b084d-220">The new extension methods just return model objects, saving you the trouble of having to unwrap them in your code.</span></span>
* <span data-ttu-id="b084d-221">Por outro lado, as principais interfaces agora expõem métodos que oferecem mais controle no nível de HTTP, se necessário.</span><span class="sxs-lookup"><span data-stu-id="b084d-221">Conversely, the core interfaces now expose methods that give you more control at the HTTP level if you need it.</span></span> <span data-ttu-id="b084d-222">Agora, você pode passar a inclusão de cabeçalhos HTTP personalizados em solicitações e o novo tipo de retorno `AzureOperationResponse<T>` lhe dá acesso direto a `HttpRequestMessage` e a `HttpResponseMessage` para a operação.</span><span class="sxs-lookup"><span data-stu-id="b084d-222">You can now pass in custom HTTP headers to be included in requests, and the new `AzureOperationResponse<T>` return type gives you direct access to the `HttpRequestMessage` and `HttpResponseMessage` for the operation.</span></span> <span data-ttu-id="b084d-223">`AzureOperationResponse` é definido no namespace `Microsoft.Rest.Azure` e substitui `Hyak.Common.OperationResponse`.</span><span class="sxs-lookup"><span data-stu-id="b084d-223">`AzureOperationResponse` is defined in the `Microsoft.Rest.Azure` namespace and replaces `Hyak.Common.OperationResponse`.</span></span>

#### <a name="scoringparameters-changes"></a><span data-ttu-id="b084d-224">Alterações de ScoringParameters</span><span class="sxs-lookup"><span data-stu-id="b084d-224">ScoringParameters changes</span></span>
<span data-ttu-id="b084d-225">Uma nova classe chamada `ScoringParameter` foi adicionada no SDK mais recente para facilitar o fornecimento de parâmetros para perfis de pontuação em uma consulta de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="b084d-225">A new class named `ScoringParameter` has been added in the latest SDK to make it easier to provide parameters to scoring profiles in a search query.</span></span> <span data-ttu-id="b084d-226">Anteriormente, a propriedade `ScoringProfiles` da classe `SearchParameters` foi tipada como `IList<string>`; agora ela é tipada como `IList<ScoringParameter>`.</span><span class="sxs-lookup"><span data-stu-id="b084d-226">Previously the `ScoringProfiles` property of the `SearchParameters` class was typed as `IList<string>`; Now it is typed as `IList<ScoringParameter>`.</span></span>

##### <a name="example"></a><span data-ttu-id="b084d-227">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b084d-227">Example</span></span>
<span data-ttu-id="b084d-228">Se o seu código tiver esta aparência:</span><span class="sxs-lookup"><span data-stu-id="b084d-228">If your code looks like this:</span></span>

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters = new[] { "featuredParam-featured", "mapCenterParam-" + lon + "," + lat };

<span data-ttu-id="b084d-229">Você poderá alterá-lo para corrigir os erros de compilação:</span><span class="sxs-lookup"><span data-stu-id="b084d-229">You can change it to this to fix any build errors:</span></span> 

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters =
        new[]
        {
            new ScoringParameter("featuredParam", new[] { "featured" }),
            new ScoringParameter("mapCenterParam", GeographyPoint.Create(lat, lon))
        };

#### <a name="model-class-changes"></a><span data-ttu-id="b084d-230">Alterações no modelo de classe</span><span class="sxs-lookup"><span data-stu-id="b084d-230">Model class changes</span></span>
<span data-ttu-id="b084d-231">Devido às alterações de assinatura descritas em [Alterações de método de operação](#OperationMethodChanges), várias classes no namespace `Microsoft.Azure.Search.Models` foram renomeadas ou removidas.</span><span class="sxs-lookup"><span data-stu-id="b084d-231">Due to the signature changes described in [Operation method changes](#OperationMethodChanges), many classes in the `Microsoft.Azure.Search.Models` namespace have been renamed or removed.</span></span> <span data-ttu-id="b084d-232">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b084d-232">For example:</span></span>

* <span data-ttu-id="b084d-233">`IndexDefinitionResponse` foi substituído por `AzureOperationResponse<Index>`</span><span class="sxs-lookup"><span data-stu-id="b084d-233">`IndexDefinitionResponse` has been replaced by `AzureOperationResponse<Index>`</span></span>
* <span data-ttu-id="b084d-234">`DocumentSearchResponse` foi renomeado para `DocumentSearchResult`</span><span class="sxs-lookup"><span data-stu-id="b084d-234">`DocumentSearchResponse` has been renamed to `DocumentSearchResult`</span></span>
* <span data-ttu-id="b084d-235">`IndexResult` foi renomeado para `IndexingResult`</span><span class="sxs-lookup"><span data-stu-id="b084d-235">`IndexResult` has been renamed to `IndexingResult`</span></span>
* <span data-ttu-id="b084d-236">`Documents.Count()` agora retorna `long` com a contagem de documentos em vez de `DocumentCountResponse`</span><span class="sxs-lookup"><span data-stu-id="b084d-236">`Documents.Count()` now returns a `long` with the document count instead of a `DocumentCountResponse`</span></span>
* <span data-ttu-id="b084d-237">`IndexGetStatisticsResponse` foi renomeado para `IndexGetStatisticsResult`</span><span class="sxs-lookup"><span data-stu-id="b084d-237">`IndexGetStatisticsResponse` has been renamed to `IndexGetStatisticsResult`</span></span>
* <span data-ttu-id="b084d-238">`IndexListResponse` foi renomeado para `IndexListResult`</span><span class="sxs-lookup"><span data-stu-id="b084d-238">`IndexListResponse` has been renamed to `IndexListResult`</span></span>

<span data-ttu-id="b084d-239">Para resumir, as classes derivadas de `OperationResponse`que existiam somente para encapsular um objeto de modelo foram removidas.</span><span class="sxs-lookup"><span data-stu-id="b084d-239">To summarize, `OperationResponse`-derived classes that existed only to wrap a model object have been removed.</span></span> <span data-ttu-id="b084d-240">As classes restantes tiveram seus sufixos alterados de `Response` para `Result`.</span><span class="sxs-lookup"><span data-stu-id="b084d-240">The remaining classes have had their suffix changed from `Response` to `Result`.</span></span>

##### <a name="example"></a><span data-ttu-id="b084d-241">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b084d-241">Example</span></span>
<span data-ttu-id="b084d-242">Se o seu código tiver esta aparência:</span><span class="sxs-lookup"><span data-stu-id="b084d-242">If your code looks like this:</span></span>

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

<span data-ttu-id="b084d-243">Você poderá alterá-lo para corrigir os erros de compilação:</span><span class="sxs-lookup"><span data-stu-id="b084d-243">You can change it to this to fix any build errors:</span></span>

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

##### <a name="response-classes-and-ienumerable"></a><span data-ttu-id="b084d-244">Classes de resposta e IEnumerable</span><span class="sxs-lookup"><span data-stu-id="b084d-244">Response classes and IEnumerable</span></span>
<span data-ttu-id="b084d-245">Outra alteração que pode afetar o código é que as classes de resposta que contêm coleções não implementam mais `IEnumerable<T>`.</span><span class="sxs-lookup"><span data-stu-id="b084d-245">An additional change that may affect your code is that response classes that hold collections no longer implement `IEnumerable<T>`.</span></span> <span data-ttu-id="b084d-246">Em vez disso, você pode acessar diretamente a propriedade de coleção.</span><span class="sxs-lookup"><span data-stu-id="b084d-246">Instead, you can access the collection property directly.</span></span> <span data-ttu-id="b084d-247">Por exemplo, se o seu código tiver esta aparência:</span><span class="sxs-lookup"><span data-stu-id="b084d-247">For example, if your code looks like this:</span></span>

    DocumentSearchResponse<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response)
    {
        Console.WriteLine(result.Document);
    }

<span data-ttu-id="b084d-248">Você poderá alterá-lo para corrigir os erros de compilação:</span><span class="sxs-lookup"><span data-stu-id="b084d-248">You can change it to this to fix any build errors:</span></span>

    DocumentSearchResult<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response.Results)
    {
        Console.WriteLine(result.Document);
    }

##### <a name="special-case-for-web-applications"></a><span data-ttu-id="b084d-249">Caso especial para aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="b084d-249">Special case for web applications</span></span>
<span data-ttu-id="b084d-250">Se você tiver um aplicativo Web que serializa `DocumentSearchResponse` diretamente para enviar os resultados da pesquisa ao navegador, precisará alterar o código ou os resultados não serão serializados corretamente.</span><span class="sxs-lookup"><span data-stu-id="b084d-250">If you have a web application that serializes `DocumentSearchResponse` directly to send search results to the browser, you will need to change your code or the results will not serialize correctly.</span></span> <span data-ttu-id="b084d-251">Por exemplo, se o seu código tiver esta aparência:</span><span class="sxs-lookup"><span data-stu-id="b084d-251">For example, if your code looks like this:</span></span>

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want to search everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q)
        };
    }

<span data-ttu-id="b084d-252">Você pode alterá-lo obtendo a propriedade `.Results` da resposta da pesquisa para corrigir a renderização dos resultados de pesquisa:</span><span class="sxs-lookup"><span data-stu-id="b084d-252">You can change it by getting the `.Results` property of the search response to fix search result rendering:</span></span>

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want to search everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q).Results
        };
    }

<span data-ttu-id="b084d-253">Você precisará procurar casos como esse no código por conta própria; **o compilador não emitirá um aviso** porque `JsonResult.Data` é do tipo `object`.</span><span class="sxs-lookup"><span data-stu-id="b084d-253">You will have to look for such cases in your code yourself; **The compiler will not warn you** because `JsonResult.Data` is of type `object`.</span></span>

#### <a name="cloudexception-changes"></a><span data-ttu-id="b084d-254">Alterações de CloudException</span><span class="sxs-lookup"><span data-stu-id="b084d-254">CloudException changes</span></span>
<span data-ttu-id="b084d-255">A classe `CloudException` foi movida do namespace `Hyak.Common` para o namespace `Microsoft.Rest.Azure`.</span><span class="sxs-lookup"><span data-stu-id="b084d-255">The `CloudException` class has moved from the `Hyak.Common` namespace to the `Microsoft.Rest.Azure` namespace.</span></span> <span data-ttu-id="b084d-256">Além disso, sua propriedade `Error` foi renomeada para `Body`.</span><span class="sxs-lookup"><span data-stu-id="b084d-256">Also, its `Error` property has been renamed to `Body`.</span></span>

#### <a name="searchserviceclient-and-searchindexclient-changes"></a><span data-ttu-id="b084d-257">Alterações de SearchServiceClient e SearchIndexClient</span><span class="sxs-lookup"><span data-stu-id="b084d-257">SearchServiceClient and SearchIndexClient changes</span></span>
<span data-ttu-id="b084d-258">O tipo da propriedade `Credentials` foi alterada de `SearchCredentials` para sua classe base, `ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="b084d-258">The type of the `Credentials` property has changed from `SearchCredentials` to its base class, `ServiceClientCredentials`.</span></span> <span data-ttu-id="b084d-259">Se você precisa acessar o `SearchCredentials` de um `SearchIndexClient` ou `SearchServiceClient`, use a nova propriedade `SearchCredentials`.</span><span class="sxs-lookup"><span data-stu-id="b084d-259">If you need to access the `SearchCredentials` of a `SearchIndexClient` or `SearchServiceClient`, please use the new `SearchCredentials` property.</span></span>

<span data-ttu-id="b084d-260">Em versões mais antigas do SDK, `SearchServiceClient` e `SearchIndexClient` tinham construtores que usavam o parâmetro `HttpClient`.</span><span class="sxs-lookup"><span data-stu-id="b084d-260">In older versions of the SDK, `SearchServiceClient` and `SearchIndexClient` had constructors that took an `HttpClient` parameter.</span></span> <span data-ttu-id="b084d-261">Eles foram substituídos por construtores que usam um `HttpClientHandler` e uma matriz de objetos `DelegatingHandler`.</span><span class="sxs-lookup"><span data-stu-id="b084d-261">These have been replaced with constructors that take an `HttpClientHandler` and an array of `DelegatingHandler` objects.</span></span> <span data-ttu-id="b084d-262">Isso facilita a instalação de manipuladores personalizados para pré-processar solicitações HTTP, se necessário.</span><span class="sxs-lookup"><span data-stu-id="b084d-262">This makes it easier to install custom handlers to pre-process HTTP requests if necessary.</span></span>

<span data-ttu-id="b084d-263">Por fim, os construtores que usavam `Uri` e `SearchCredentials` foram alterados.</span><span class="sxs-lookup"><span data-stu-id="b084d-263">Finally, the constructors that took a `Uri` and `SearchCredentials` have changed.</span></span> <span data-ttu-id="b084d-264">Por exemplo, se você tiver código parecido com este:</span><span class="sxs-lookup"><span data-stu-id="b084d-264">For example, if you have code that looks like this:</span></span>

    var client =
        new SearchServiceClient(
            new SearchCredentials("abc123"),
            new Uri("http://myservice.search.windows.net"));

<span data-ttu-id="b084d-265">Você poderá alterá-lo para corrigir os erros de compilação:</span><span class="sxs-lookup"><span data-stu-id="b084d-265">You can change it to this to fix any build errors:</span></span>

    var client =
        new SearchServiceClient(
            new Uri("http://myservice.search.windows.net"),
            new SearchCredentials("abc123"));

<span data-ttu-id="b084d-266">Observe também que o tipo do parâmetro de credenciais foi alterado para `ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="b084d-266">Also note that the type of the credentials parameter has changed to `ServiceClientCredentials`.</span></span> <span data-ttu-id="b084d-267">Isso provavelmente não afetará o código, já que `SearchCredentials` é derivado de `ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="b084d-267">This is unlikely to affect your code since `SearchCredentials` is derived from `ServiceClientCredentials`.</span></span>

#### <a name="passing-a-request-id"></a><span data-ttu-id="b084d-268">Passando uma ID de solicitação</span><span class="sxs-lookup"><span data-stu-id="b084d-268">Passing a request ID</span></span>
<span data-ttu-id="b084d-269">Em versões mais antigas do SDK, você podia definir uma ID de solicitação no `SearchServiceClient` ou `SearchIndexClient` e ela seria incluída em cada solicitação para a API REST.</span><span class="sxs-lookup"><span data-stu-id="b084d-269">In older versions of the SDK, you could set a request ID on the `SearchServiceClient` or `SearchIndexClient` and it would be included in every request to the REST API.</span></span> <span data-ttu-id="b084d-270">Isso é útil para solucionar problemas com o serviço de pesquisa, se você precisar entrar em contato com o suporte.</span><span class="sxs-lookup"><span data-stu-id="b084d-270">This is useful for troubleshooting issues with your search service if you need to contact support.</span></span> <span data-ttu-id="b084d-271">No entanto, é mais útil para definir uma ID de solicitação exclusiva para cada operação em vez de usar a mesma ID para todas as operações.</span><span class="sxs-lookup"><span data-stu-id="b084d-271">However, it is more useful to set a unique request ID for every operation rather than to use the same ID for all operations.</span></span> <span data-ttu-id="b084d-272">Por esse motivo, os métodos `SetClientRequestId` de `SearchServiceClient` e `SearchIndexClient` foram removidos.</span><span class="sxs-lookup"><span data-stu-id="b084d-272">For this reason, the `SetClientRequestId` methods of `SearchServiceClient` and `SearchIndexClient` have been removed.</span></span> <span data-ttu-id="b084d-273">Em vez disso, você pode passar uma ID de solicitação para cada método de operação por meio do parâmetro opcional `SearchRequestOptions` .</span><span class="sxs-lookup"><span data-stu-id="b084d-273">Instead, you can pass a request ID to each operation method via the optional `SearchRequestOptions` parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="b084d-274">Em uma futura versão do SDK, vamos adicionar um novo mecanismo para definir uma ID de solicitação globalmente nos objetos clientes que é consistente com a abordagem usada pelos outros SDKs do Azure.</span><span class="sxs-lookup"><span data-stu-id="b084d-274">In a future release of the SDK, we will add a new mechanism for setting a request ID globally on the client objects that is consistent with the approach used by other Azure SDKs.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="b084d-275">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b084d-275">Example</span></span>
<span data-ttu-id="b084d-276">Se você tiver um código parecido com este:</span><span class="sxs-lookup"><span data-stu-id="b084d-276">If you have code that looks like this:</span></span>

    client.SetClientRequestId(Guid.NewGuid());
    ...
    long count = client.Documents.Count();

<span data-ttu-id="b084d-277">Você poderá alterá-lo para corrigir os erros de compilação:</span><span class="sxs-lookup"><span data-stu-id="b084d-277">You can change it to this to fix any build errors:</span></span>

    long count = client.Documents.Count(new SearchRequestOptions(requestId: Guid.NewGuid()));

#### <a name="interface-name-changes"></a><span data-ttu-id="b084d-278">Alterações de nome de interface</span><span class="sxs-lookup"><span data-stu-id="b084d-278">Interface name changes</span></span>
<span data-ttu-id="b084d-279">Os nomes de interface do grupo de operação foram alterados para ficarem consistentes com os nomes de propriedade correspondentes:</span><span class="sxs-lookup"><span data-stu-id="b084d-279">The operation group interface names have all changed to be consistent with their corresponding property names:</span></span>

* <span data-ttu-id="b084d-280">O tipo de `ISearchServiceClient.Indexes` foi renomeado de `IIndexOperations` para `IIndexesOperations`.</span><span class="sxs-lookup"><span data-stu-id="b084d-280">The type of `ISearchServiceClient.Indexes` has been renamed from `IIndexOperations` to `IIndexesOperations`.</span></span>
* <span data-ttu-id="b084d-281">O tipo de `ISearchServiceClient.Indexers` foi renomeado de `IIndexerOperations` para `IIndexersOperations`.</span><span class="sxs-lookup"><span data-stu-id="b084d-281">The type of `ISearchServiceClient.Indexers` has been renamed from `IIndexerOperations` to `IIndexersOperations`.</span></span>
* <span data-ttu-id="b084d-282">O tipo de `ISearchServiceClient.DataSources` foi renomeado de `IDataSourceOperations` para `IDataSourcesOperations`.</span><span class="sxs-lookup"><span data-stu-id="b084d-282">The type of `ISearchServiceClient.DataSources` has been renamed from `IDataSourceOperations` to `IDataSourcesOperations`.</span></span>
* <span data-ttu-id="b084d-283">O tipo de `ISearchIndexClient.Documents` foi renomeado de `IDocumentOperations` para `IDocumentsOperations`.</span><span class="sxs-lookup"><span data-stu-id="b084d-283">The type of `ISearchIndexClient.Documents` has been renamed from `IDocumentOperations` to `IDocumentsOperations`.</span></span>

<span data-ttu-id="b084d-284">Essa alteração provavelmente não afetará o seu código, a menos que você tenha criado simulações dessas interfaces para fins de teste.</span><span class="sxs-lookup"><span data-stu-id="b084d-284">This change is unlikely to affect your code unless you created mocks of these interfaces for test purposes.</span></span>

<a name="BugFixesV1"></a>

### <a name="bug-fixes-in-version-11"></a><span data-ttu-id="b084d-285">Correções de bug na versão 1.1</span><span class="sxs-lookup"><span data-stu-id="b084d-285">Bug fixes in version 1.1</span></span>
<span data-ttu-id="b084d-286">Havia um bug nas versões mais antigas do SDK .NET da Pesquisa do Azure relacionado à serialização de classes de modelo personalizadas.</span><span class="sxs-lookup"><span data-stu-id="b084d-286">There was a bug in older versions of the Azure Search .NET SDK relating to serialization of custom model classes.</span></span> <span data-ttu-id="b084d-287">O bug ocorria ao criar uma classe de modelo personalizada com uma propriedade de um tipo de valor não anulável.</span><span class="sxs-lookup"><span data-stu-id="b084d-287">The bug could occur if you created a custom model class with a property of a non-nullable value type.</span></span>

#### <a name="steps-to-reproduce"></a><span data-ttu-id="b084d-288">Etapas para reproduzir</span><span class="sxs-lookup"><span data-stu-id="b084d-288">Steps to reproduce</span></span>
<span data-ttu-id="b084d-289">Crie uma classe de modelo personalizada com uma propriedade de tipo de valor não anulável.</span><span class="sxs-lookup"><span data-stu-id="b084d-289">Create a custom model class with a property of non-nullable value type.</span></span> <span data-ttu-id="b084d-290">Por exemplo, adicione uma propriedade `UnitCount` pública do tipo `int` em vez de `int?`.</span><span class="sxs-lookup"><span data-stu-id="b084d-290">For example, add a public `UnitCount` property of type `int` instead of `int?`.</span></span>

<span data-ttu-id="b084d-291">Se você indexar um documento com o valor padrão desse tipo (por exemplo, 0 para `int`), o campo será nulo na Pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="b084d-291">If you index a document with the default value of that type (for example, 0 for `int`), the field will be null in Azure Search.</span></span> <span data-ttu-id="b084d-292">Se você pesquisar esse documento em seguida, a chamada `Search` gerará `JsonSerializationException`, com a indicação de que não é possível converter `null` para `int`.</span><span class="sxs-lookup"><span data-stu-id="b084d-292">If you subsequently search for that document, the `Search` call will throw `JsonSerializationException` complaining that it can't convert `null` to `int`.</span></span>

<span data-ttu-id="b084d-293">Além disso, os filtros podem não funcionar conforme o esperado, já que null foi gravado no índice em vez do valor desejado.</span><span class="sxs-lookup"><span data-stu-id="b084d-293">Also, filters may not work as expected since null was written to the index instead of the intended value.</span></span>

#### <a name="fix-details"></a><span data-ttu-id="b084d-294">Corrigir detalhes</span><span class="sxs-lookup"><span data-stu-id="b084d-294">Fix details</span></span>
<span data-ttu-id="b084d-295">Corrigimos o problema na versão 1.1 do SDK.</span><span class="sxs-lookup"><span data-stu-id="b084d-295">We have fixed this issue in version 1.1 of the SDK.</span></span> <span data-ttu-id="b084d-296">Agora, se você tiver uma classe de modelo como esta:</span><span class="sxs-lookup"><span data-stu-id="b084d-296">Now, if you have a model class like this:</span></span>

    public class Model
    {
        public string Key { get; set; }

        public int IntValue { get; set; }
    }

<span data-ttu-id="b084d-297">e definir `IntValue` como 0, o valor agora corretamente serializado como 0 durante a transmissão e armazenado como 0 no índice.</span><span class="sxs-lookup"><span data-stu-id="b084d-297">and you set `IntValue` to 0, that value is now correctly serialized as 0 on the wire and stored as 0 in the index.</span></span> <span data-ttu-id="b084d-298">A viagem de ida e volta também funciona conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="b084d-298">Round tripping also works as expected.</span></span>

<span data-ttu-id="b084d-299">Há um problema potencial que devemos reconhecer nessa abordagem: se você usar um tipo de modelo com uma propriedade que não permite valor nulo, precisará **garantir** que nenhum documento no índice contém um valor nulo para o campo correspondente.</span><span class="sxs-lookup"><span data-stu-id="b084d-299">There is one potential issue to be aware of with this approach: If you use a model type with a non-nullable property, you have to **guarantee** that no documents in your index contain a null value for the corresponding field.</span></span> <span data-ttu-id="b084d-300">O SDK e a API REST da Pesquisa do Azure não podem ajudá-lo a impor isso.</span><span class="sxs-lookup"><span data-stu-id="b084d-300">Neither the SDK nor the Azure Search REST API will help you to enforce this.</span></span>

<span data-ttu-id="b084d-301">Isso não é apenas uma preocupação hipotética: imagine um cenário em que você adiciona um novo campo a um índice existente do tipo `Edm.Int32`.</span><span class="sxs-lookup"><span data-stu-id="b084d-301">This is not just a hypothetical concern: Imagine a scenario where you add a new field to an existing index that is of type `Edm.Int32`.</span></span> <span data-ttu-id="b084d-302">Depois de atualizar a definição de índice, todos os documentos terão um valor nulo para esse novo campo (já que todos os tipos são anuláveis na Pesquisa do Azure).</span><span class="sxs-lookup"><span data-stu-id="b084d-302">After updating the index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="b084d-303">Ao usar uma classe de modelo com uma propriedade não anulável `int` para esse campo, você obterá uma `JsonSerializationException` como esta ao tentar recuperar os documentos:</span><span class="sxs-lookup"><span data-stu-id="b084d-303">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying to retrieve documents:</span></span>

    Error converting value {null} to type 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="b084d-304">Por esse motivo, continuamos a recomendar que você use tipos anuláveis nas suas classes de modelo como uma prática recomendada.</span><span class="sxs-lookup"><span data-stu-id="b084d-304">For this reason, we still recommend that you use nullable types in your model classes as a best practice.</span></span>

<span data-ttu-id="b084d-305">Para obter mais detalhes sobre esse bug e a correção, confira [esse problema no GitHub](https://github.com/Azure/azure-sdk-for-net/issues/1063).</span><span class="sxs-lookup"><span data-stu-id="b084d-305">For more details on this bug and the fix, please see [this issue on GitHub](https://github.com/Azure/azure-sdk-for-net/issues/1063).</span></span>

