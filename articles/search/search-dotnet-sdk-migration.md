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
# <a name="upgrading-toohello-azure-search-net-sdk-version-3"></a><span data-ttu-id="66718-103">Atualizando toohello SDK .NET da pesquisa do Azure versão 3</span><span class="sxs-lookup"><span data-stu-id="66718-103">Upgrading toohello Azure Search .NET SDK version 3</span></span>
<span data-ttu-id="66718-104">Se você estiver usando a versão preview 2.0 ou anterior de saudação [SDK .NET da pesquisa do Azure](https://aka.ms/search-sdk), este artigo o ajudará a atualizar a versão do aplicativo toouse 3.</span><span class="sxs-lookup"><span data-stu-id="66718-104">If you're using version 2.0-preview or older of hello [Azure Search .NET SDK](https://aka.ms/search-sdk), this article will help you upgrade your application toouse version 3.</span></span>

<span data-ttu-id="66718-105">Para obter uma explicação mais geral de saudação SDK incluindo exemplos, consulte [como toouse Azure pesquisa de um aplicativo .NET](search-howto-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="66718-105">For a more general walkthrough of hello SDK including examples, see [How toouse Azure Search from a .NET Application](search-howto-dotnet-sdk.md).</span></span>

<span data-ttu-id="66718-106">A versão 3 do hello SDK .NET da pesquisa do Azure contém algumas alterações de versões anteriores.</span><span class="sxs-lookup"><span data-stu-id="66718-106">Version 3 of hello Azure Search .NET SDK contains some changes from earlier versions.</span></span> <span data-ttu-id="66718-107">A maioria das alterações é leve e, portanto, a alteração do seu código não deve exigir muito.</span><span class="sxs-lookup"><span data-stu-id="66718-107">These are mostly minor, so changing your code should require only minimal effort.</span></span> <span data-ttu-id="66718-108">Consulte [tooupgrade etapas](#UpgradeSteps) para obter instruções sobre como toochange a código toouse Olá nova versão do SDK.</span><span class="sxs-lookup"><span data-stu-id="66718-108">See [Steps tooupgrade](#UpgradeSteps) for instructions on how toochange your code toouse hello new SDK version.</span></span>

> [!NOTE]
> <span data-ttu-id="66718-109">Se você estiver usando a versão 1.0.2-preview ou anterior, você deve atualizar primeiro o tooversion 1.1 e, em seguida, atualizar tooversion 3.</span><span class="sxs-lookup"><span data-stu-id="66718-109">If you're using version 1.0.2-preview or older, you should upgrade tooversion 1.1 first, and then upgrade tooversion 3.</span></span> <span data-ttu-id="66718-110">Consulte [Apêndice: etapas tooupgrade tooversion 1.1](#UpgradeStepsV1) para obter instruções.</span><span class="sxs-lookup"><span data-stu-id="66718-110">See [Appendix: Steps tooupgrade tooversion 1.1](#UpgradeStepsV1) for instructions.</span></span>
>
> <span data-ttu-id="66718-111">Sua instância de serviço de pesquisa do Azure oferece suporte a várias versões da API REST, incluindo hello mais recente.</span><span class="sxs-lookup"><span data-stu-id="66718-111">Your Azure Search service instance supports several REST API versions, including hello latest one.</span></span> <span data-ttu-id="66718-112">Você pode continuar toouse uma versão quando ela não é mais hello mais recente, mas é recomendável que você migre a sua versão mais recente do código toouse hello.</span><span class="sxs-lookup"><span data-stu-id="66718-112">You can continue toouse a version when it is no longer hello latest one, but we recommend that you migrate your code toouse hello newest version.</span></span> <span data-ttu-id="66718-113">Ao usar o hello API REST, você deve especificar a versão de API de Olá em cada solicitação feita por meio do parâmetro de versão de api de saudação.</span><span class="sxs-lookup"><span data-stu-id="66718-113">When using hello REST API, you must specify hello API version in every request via hello api-version parameter.</span></span> <span data-ttu-id="66718-114">Ao usar o SDK .NET de saudação, versão de saudação do Olá SDK que você está usando determina versão correspondente de saudação do hello API REST.</span><span class="sxs-lookup"><span data-stu-id="66718-114">When using hello .NET SDK, hello version of hello SDK you’re using determines hello corresponding version of hello REST API.</span></span> <span data-ttu-id="66718-115">Se você estiver usando um SDK anterior, você pode continuar toorun que o código sem alterações mesmo se o serviço Olá é atualizado toosupport uma API mais recente versão.</span><span class="sxs-lookup"><span data-stu-id="66718-115">If you are using an older SDK, you can continue toorun that code with no changes even if hello service is upgraded toosupport a newer API version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-3"></a><span data-ttu-id="66718-116">Novidades na versão 3</span><span class="sxs-lookup"><span data-stu-id="66718-116">What's new in version 3</span></span>
<span data-ttu-id="66718-117">Versão 3 da saudação de destinos de SDK .NET da pesquisa do Azure hello mais recente versão disponível do hello API de REST de pesquisa do Azure, especificamente 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="66718-117">Version 3 of hello Azure Search .NET SDK targets hello latest generally available version of hello Azure Search REST API, specifically 2016-09-01.</span></span> <span data-ttu-id="66718-118">Isso torna possível toouse muitos novos recursos de pesquisa do Azure de um aplicativo .NET, incluindo Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="66718-118">This makes it possible toouse many new features of Azure Search from a .NET application, including hello following:</span></span>

* [<span data-ttu-id="66718-119">Analisadores personalizados</span><span class="sxs-lookup"><span data-stu-id="66718-119">Custom analyzers</span></span>](https://aka.ms/customanalyzers)
* <span data-ttu-id="66718-120">Suporte do indexador do [Armazenamento de Blobs do Azure](search-howto-indexing-azure-blob-storage.md) e do [Armazenamento de Tabelas do Azure](search-howto-indexing-azure-tables.md)</span><span class="sxs-lookup"><span data-stu-id="66718-120">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexer support</span></span>
* <span data-ttu-id="66718-121">Personalização do indexador por meio de [mapeamentos de campo](search-indexer-field-mappings.md)</span><span class="sxs-lookup"><span data-stu-id="66718-121">Indexer customization via [field mappings](search-indexer-field-mappings.md)</span></span>
* <span data-ttu-id="66718-122">Suporte a ETags tooenable seguro atualizações simultâneas de índice definições, indexadores e fontes de dados</span><span class="sxs-lookup"><span data-stu-id="66718-122">ETags support tooenable safe concurrent updating of index definitions, indexers, and data sources</span></span>
* <span data-ttu-id="66718-123">Suporte para a criação de definições de campo de índice declarativamente a decoração de sua classe de modelo e usando Olá novo `FieldBuilder` classe.</span><span class="sxs-lookup"><span data-stu-id="66718-123">Support for building index field definitions declaratively by decorating your model class and using hello new `FieldBuilder` class.</span></span>
* <span data-ttu-id="66718-124">Suporte para .NET Core e .NET Portable Profile 111</span><span class="sxs-lookup"><span data-stu-id="66718-124">Support for .NET Core and .NET Portable Profile 111</span></span>

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a><span data-ttu-id="66718-125">Etapas tooupgrade</span><span class="sxs-lookup"><span data-stu-id="66718-125">Steps tooupgrade</span></span>
<span data-ttu-id="66718-126">Primeiro, atualize sua referência de NuGet para `Microsoft.Azure.Search` usando o NuGet Package Manager Console hello ou clicando duas vezes em suas referências do projeto e selecionando "Gerenciar NuGet pacotes …" no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="66718-126">First, update your NuGet reference for `Microsoft.Azure.Search` using either hello NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.</span></span>

<span data-ttu-id="66718-127">Depois que o NuGet baixou Olá novos pacotes e suas dependências, recompile o projeto.</span><span class="sxs-lookup"><span data-stu-id="66718-127">Once NuGet has downloaded hello new packages and their dependencies, rebuild your project.</span></span> <span data-ttu-id="66718-128">Dependendo de como o código está estruturado, ele poderá ser recriado com êxito.</span><span class="sxs-lookup"><span data-stu-id="66718-128">Depending on how your code is structured, it may rebuild successfully.</span></span> <span data-ttu-id="66718-129">Nesse caso, você está pronto toogo!</span><span class="sxs-lookup"><span data-stu-id="66718-129">If so, you're ready toogo!</span></span>

<span data-ttu-id="66718-130">Se a compilação falhar, você verá um erro de compilação como Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="66718-130">If your build fails, you should see a build error like hello following:</span></span>

    Program.cs(31,45,31,86): error CS0266: Cannot implicitly convert type 'Microsoft.Azure.Search.ISearchIndexClient' too'Microsoft.Azure.Search.SearchIndexClient'. An explicit conversion exists (are you missing a cast?)

<span data-ttu-id="66718-131">próxima etapa do Hello é toofix esse erro de compilação.</span><span class="sxs-lookup"><span data-stu-id="66718-131">hello next step is toofix this build error.</span></span> <span data-ttu-id="66718-132">Consulte [alterações significativas na versão 3](#ListOfChanges) para obter detalhes sobre o que causa o erro hello e como toofix-lo.</span><span class="sxs-lookup"><span data-stu-id="66718-132">See [Breaking changes in version 3](#ListOfChanges) for details on what causes hello error and how toofix it.</span></span>

<span data-ttu-id="66718-133">Você pode ver compilação adicional avisos relacionados tooobsolete métodos ou propriedades.</span><span class="sxs-lookup"><span data-stu-id="66718-133">You may see additional build warnings related tooobsolete methods or properties.</span></span> <span data-ttu-id="66718-134">avisos de saudação inclui instruções sobre em quais toouse em vez disso, de saudação recurso preterido.</span><span class="sxs-lookup"><span data-stu-id="66718-134">hello warnings will include instructions on what toouse instead of hello deprecated feature.</span></span> <span data-ttu-id="66718-135">Por exemplo, se seu aplicativo usa Olá `IndexingParameters.Base64EncodeKeys` propriedade, você deve receber um aviso que diz`"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`</span><span class="sxs-lookup"><span data-stu-id="66718-135">For example, if your application uses hello `IndexingParameters.Base64EncodeKeys` property, you should get a warning that says `"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`</span></span>

<span data-ttu-id="66718-136">Depois de solucionar os erros de compilação, você pode fazer alterações tooyour aplicativo tootake aproveitar novas funcionalidades se desejar.</span><span class="sxs-lookup"><span data-stu-id="66718-136">Once you've fixed any build errors, you can make changes tooyour application tootake advantage of new functionality if you wish.</span></span> <span data-ttu-id="66718-137">Novos recursos no SDK do hello são detalhados no [o que há de novo na versão 3](#WhatsNew).</span><span class="sxs-lookup"><span data-stu-id="66718-137">New features in hello SDK are detailed in [What's new in version 3](#WhatsNew).</span></span>

<a name="ListOfChanges"></a>

## <a name="breaking-changes-in-version-3"></a><span data-ttu-id="66718-138">Alterações significativas na versão 3</span><span class="sxs-lookup"><span data-stu-id="66718-138">Breaking changes in version 3</span></span>
<span data-ttu-id="66718-139">Há um pequeno número de alterações significativas na versão 3 que podem exigir código altera além toorebuilding seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="66718-139">There a small number of breaking changes in version 3 that may require code changes in addition toorebuilding your application.</span></span>

### <a name="indexesgetclient-return-type"></a><span data-ttu-id="66718-140">Tipo de retorno de Indexes.GetClient</span><span class="sxs-lookup"><span data-stu-id="66718-140">Indexes.GetClient return type</span></span>
<span data-ttu-id="66718-141">Olá `Indexes.GetClient` método tem um novo tipo de retorno.</span><span class="sxs-lookup"><span data-stu-id="66718-141">hello `Indexes.GetClient` method has a new return type.</span></span> <span data-ttu-id="66718-142">Anteriormente, ele retornou `SearchIndexClient`, mas isso foi alterado muito`ISearchIndexClient` na versão 2.0-visualização e que alteração traz tooversion 3.</span><span class="sxs-lookup"><span data-stu-id="66718-142">Previously, it returned `SearchIndexClient`, but this was changed too`ISearchIndexClient` in version 2.0-preview, and that change carries over tooversion 3.</span></span> <span data-ttu-id="66718-143">Isso é toosupport os clientes que desejem Olá toomock `GetClient` método para testes de unidade, retornando uma implementação fictícia do `ISearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="66718-143">This is toosupport customers that wish toomock hello `GetClient` method for unit tests by returning a mock implementation of `ISearchIndexClient`.</span></span>

#### <a name="example"></a><span data-ttu-id="66718-144">Exemplo</span><span class="sxs-lookup"><span data-stu-id="66718-144">Example</span></span>
<span data-ttu-id="66718-145">Se o seu código tiver esta aparência:</span><span class="sxs-lookup"><span data-stu-id="66718-145">If your code looks like this:</span></span>

```csharp
SearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

<span data-ttu-id="66718-146">Você pode alterá-la toothis toofix qualquer erro de compilação:</span><span class="sxs-lookup"><span data-stu-id="66718-146">You can change it toothis toofix any build errors:</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

### <a name="analyzername-datatype-and-others-are-no-longer-implicitly-convertible-toostrings"></a><span data-ttu-id="66718-147">AnalyzerName, tipo de dados e outros não são implicitamente conversíveis toostrings</span><span class="sxs-lookup"><span data-stu-id="66718-147">AnalyzerName, DataType, and others are no longer implicitly convertible toostrings</span></span>
<span data-ttu-id="66718-148">Há muitos tipos de saudação SDK .NET da pesquisa do Azure que derivam de `ExtensibleEnum`.</span><span class="sxs-lookup"><span data-stu-id="66718-148">There are many types in hello Azure Search .NET SDK that derive from `ExtensibleEnum`.</span></span> <span data-ttu-id="66718-149">Anteriormente esses tipos foram todos implicitamente conversível tootype `string`.</span><span class="sxs-lookup"><span data-stu-id="66718-149">Previously these types were all implicitly convertible tootype `string`.</span></span> <span data-ttu-id="66718-150">No entanto, um bug foi descoberto em Olá `Object.Equals` implementação para essas classes e corrigindo Olá bug necessário desabilitar essa conversão implícita.</span><span class="sxs-lookup"><span data-stu-id="66718-150">However, a bug was discovered in hello `Object.Equals` implementation for these classes, and fixing hello bug required disabling this implicit conversion.</span></span> <span data-ttu-id="66718-151">Conversão explícita muito`string` ainda é permitido.</span><span class="sxs-lookup"><span data-stu-id="66718-151">Explicit conversion too`string` is still allowed.</span></span>

#### <a name="example"></a><span data-ttu-id="66718-152">Exemplo</span><span class="sxs-lookup"><span data-stu-id="66718-152">Example</span></span>
<span data-ttu-id="66718-153">Se o seu código tiver esta aparência:</span><span class="sxs-lookup"><span data-stu-id="66718-153">If your code looks like this:</span></span>

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

<span data-ttu-id="66718-154">Você pode alterá-la toothis toofix qualquer erro de compilação:</span><span class="sxs-lookup"><span data-stu-id="66718-154">You can change it toothis toofix any build errors:</span></span>

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

### <a name="removed-obsolete-members"></a><span data-ttu-id="66718-155">Remover membros obsoletos</span><span class="sxs-lookup"><span data-stu-id="66718-155">Removed obsolete members</span></span>

<span data-ttu-id="66718-156">Você pode ver toomethods relacionados de erros de compilação ou propriedades que foram marcadas como obsoletos no versão 2.0-visualização e subsequentemente removidas na versão 3.</span><span class="sxs-lookup"><span data-stu-id="66718-156">You may see build errors related toomethods or properties that were marked as obsolete in version 2.0-preview and subsequently removed in version 3.</span></span> <span data-ttu-id="66718-157">Se você encontrar esses erros, aqui está como tooresolve-los:</span><span class="sxs-lookup"><span data-stu-id="66718-157">If you encounter such errors, here is how tooresolve them:</span></span>

- <span data-ttu-id="66718-158">Se usava o construtor: `ScoringParameter(string name, string value)`, use este em vez dele: `ScoringParameter(string name, IEnumerable<string> values)`</span><span class="sxs-lookup"><span data-stu-id="66718-158">If you were using this constructor: `ScoringParameter(string name, string value)`, use this one instead: `ScoringParameter(string name, IEnumerable<string> values)`</span></span>
- <span data-ttu-id="66718-159">Se você estivesse usando Olá `ScoringParameter.Value` propriedade, use Olá `ScoringParameter.Values` propriedade ou hello `ToString` método em vez disso.</span><span class="sxs-lookup"><span data-stu-id="66718-159">If you were using hello `ScoringParameter.Value` property, use hello `ScoringParameter.Values` property or hello `ToString` method instead.</span></span>
- <span data-ttu-id="66718-160">Se você estivesse usando Olá `SearchRequestOptions.RequestId` propriedade, use Olá `ClientRequestId` propriedade em vez disso.</span><span class="sxs-lookup"><span data-stu-id="66718-160">If you were using hello `SearchRequestOptions.RequestId` property, use hello `ClientRequestId` property instead.</span></span>

### <a name="removed-preview-features"></a><span data-ttu-id="66718-161">Recursos de visualização removidos</span><span class="sxs-lookup"><span data-stu-id="66718-161">Removed preview features</span></span>

<span data-ttu-id="66718-162">Se você estiver atualizando da versão 2.0 preview tooversion 3, lembre-se de que suporte a indexadores de Blob de análise de CSV e JSON foi removido desde que esses recursos ainda estão na visualização.</span><span class="sxs-lookup"><span data-stu-id="66718-162">If you are upgrading from version 2.0-preview tooversion 3, be aware that JSON and CSV parsing support for Blob Indexers has been removed since these features are still in preview.</span></span> <span data-ttu-id="66718-163">Especificamente, Olá Olá métodos a seguir `IndexingParametersExtensions` classe foram removidos:</span><span class="sxs-lookup"><span data-stu-id="66718-163">Specifically, hello following methods of hello `IndexingParametersExtensions` class have been removed:</span></span>

- `ParseJson`
- `ParseJsonArrays`
- `ParseDelimitedTextFiles`

<span data-ttu-id="66718-164">Se seu aplicativo tem uma dependência de disco rígida sobre esses recursos, não será capaz de tooupgrade tooversion 3 de saudação SDK .NET da pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="66718-164">If your application has a hard dependency on these features, you will not be able tooupgrade tooversion 3 of hello Azure Search .NET SDK.</span></span> <span data-ttu-id="66718-165">Você pode continuar toouse versão 2.0-visualização.</span><span class="sxs-lookup"><span data-stu-id="66718-165">You can continue toouse version 2.0-preview.</span></span> <span data-ttu-id="66718-166">No entanto, lembre-se que **não é recomendável usar SDKs de visualização em aplicativos de produção**.</span><span class="sxs-lookup"><span data-stu-id="66718-166">However, please keep in mind that **we do not recommend using preview SDKs in production applications**.</span></span> <span data-ttu-id="66718-167">Os recursos de visualização destinam-se apenas a fins de avaliação e podem ser alterados.</span><span class="sxs-lookup"><span data-stu-id="66718-167">Preview features are for evaluation only and may change.</span></span>

## <a name="conclusion"></a><span data-ttu-id="66718-168">Conclusão</span><span class="sxs-lookup"><span data-stu-id="66718-168">Conclusion</span></span>
<span data-ttu-id="66718-169">Se você precisar de mais detalhes sobre o uso Olá SDK .NET da pesquisa do Azure, consulte nosso atualizado recentemente [instruções](search-howto-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="66718-169">If you need more details on using hello Azure Search .NET SDK, see our recently updated [How-to](search-howto-dotnet-sdk.md).</span></span>

<span data-ttu-id="66718-170">Apreciamos seus comentários em Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="66718-170">We welcome your feedback on hello SDK.</span></span> <span data-ttu-id="66718-171">Se você encontrar problemas, sinta-se livre tooask nos para obter ajuda sobre Olá [Fórum do MSDN de pesquisa do Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch).</span><span class="sxs-lookup"><span data-stu-id="66718-171">If you encounter problems, feel free tooask us for help on hello [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch).</span></span> <span data-ttu-id="66718-172">Se você encontrar um erro, você pode registrar um problema no hello [repositório GitHub do Azure .NET SDK](https://github.com/Azure/azure-sdk-for-net/issues).</span><span class="sxs-lookup"><span data-stu-id="66718-172">If you find a bug, you can file an issue in hello [Azure .NET SDK GitHub repository](https://github.com/Azure/azure-sdk-for-net/issues).</span></span> <span data-ttu-id="66718-173">Verifique se tooprefix o título do problema com "SDK de pesquisa:".</span><span class="sxs-lookup"><span data-stu-id="66718-173">Make sure tooprefix your issue title with "Search SDK: ".</span></span>

<span data-ttu-id="66718-174">Obrigado por usar a Pesquisa do Azure!</span><span class="sxs-lookup"><span data-stu-id="66718-174">Thank you for using Azure Search!</span></span>

<a name="UpgradeStepsV1"></a>

## <a name="appendix-steps-tooupgrade-tooversion-11"></a><span data-ttu-id="66718-175">Apêndice: Etapas tooupgrade tooversion 1.1</span><span class="sxs-lookup"><span data-stu-id="66718-175">Appendix: Steps tooupgrade tooversion 1.1</span></span>
> [!NOTE]
> <span data-ttu-id="66718-176">Esta seção se aplica apenas toousers de saudação SDK .NET da pesquisa do Azure versão 1.0.2-preview e anteriores.</span><span class="sxs-lookup"><span data-stu-id="66718-176">This section applies only toousers of hello Azure Search .NET SDK version 1.0.2-preview and older.</span></span>
> 
> 

<span data-ttu-id="66718-177">Primeiro, atualize sua referência de NuGet para `Microsoft.Azure.Search` usando o NuGet Package Manager Console hello ou clicando duas vezes em suas referências do projeto e selecionando "Gerenciar NuGet pacotes …" no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="66718-177">First, update your NuGet reference for `Microsoft.Azure.Search` using either hello NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.</span></span>

<span data-ttu-id="66718-178">Depois que o NuGet baixou Olá novos pacotes e suas dependências, recompile o projeto.</span><span class="sxs-lookup"><span data-stu-id="66718-178">Once NuGet has downloaded hello new packages and their dependencies, rebuild your project.</span></span>

<span data-ttu-id="66718-179">Se você anteriormente usando a versão 1.0.0-preview, 1.0.1-preview ou 1.0.2-preview, compilação de saudação deve ter êxito e você está pronto toogo!</span><span class="sxs-lookup"><span data-stu-id="66718-179">If you were previously using version 1.0.0-preview, 1.0.1-preview, or 1.0.2-preview, hello build should succeed and you're ready toogo!</span></span>

<span data-ttu-id="66718-180">Se você estava usando anteriormente 0.13.0-preview versão ou anterior, você verá erros como Olá seguinte compilação:</span><span class="sxs-lookup"><span data-stu-id="66718-180">If you were previously using version 0.13.0-preview or older, you should see build errors like hello following:</span></span>

    Program.cs(137,56,137,62): error CS0117: 'Microsoft.Azure.Search.Models.IndexBatch' does not contain a definition for 'Create'
    Program.cs(137,99,137,105): error CS0117: 'Microsoft.Azure.Search.Models.IndexAction' does not contain a definition for 'Create'
    Program.cs(146,41,146,54): error CS1061: 'Microsoft.Azure.Search.IndexBatchException' does not contain a definition for 'IndexResponse' and no extension method 'IndexResponse' accepting a first argument of type 'Microsoft.Azure.Search.IndexBatchException' could be found (are you missing a using directive or an assembly reference?)
    Program.cs(163,13,163,42): error CS0246: hello type or namespace name 'DocumentSearchResponse' could not be found (are you missing a using directive or an assembly reference?)

<span data-ttu-id="66718-181">Olá próxima etapa é erros de compilação toofix Olá uma.</span><span class="sxs-lookup"><span data-stu-id="66718-181">hello next step is toofix hello build errors one by one.</span></span> <span data-ttu-id="66718-182">A maioria exigirá alterando alguns nomes de classe e método que foram renomeados no hello SDK.</span><span class="sxs-lookup"><span data-stu-id="66718-182">Most will require changing some class and method names that have been renamed in hello SDK.</span></span> <span data-ttu-id="66718-183">[Lista de alterações significativas na versão 1.1](#ListOfChangesV1) contém uma lista dessas alterações de nome.</span><span class="sxs-lookup"><span data-stu-id="66718-183">[List of breaking changes in version 1.1](#ListOfChangesV1) contains a list of these name changes.</span></span>

<span data-ttu-id="66718-184">Se você estiver usando classes personalizadas toomodel seus documentos e as classes têm propriedades de tipos primitivos não anulável (por exemplo, `int` ou `bool` em c#), há uma correção de bug na versão Olá 1.1 do SDK Olá dos quais você deve estar ciente.</span><span class="sxs-lookup"><span data-stu-id="66718-184">If you're using custom classes toomodel your documents, and those classes have properties of non-nullable primitive types (for example, `int` or `bool` in C#), there is a bug fix in hello 1.1 version of hello SDK of which you should be aware.</span></span> <span data-ttu-id="66718-185">Veja [Correções de bug na versão 1.1](#BugFixesV1) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="66718-185">See [Bug fixes in version 1.1](#BugFixesV1) for more details.</span></span>

<span data-ttu-id="66718-186">Finalmente, depois de solucionar os erros de compilação, você pode fazer alterações tooyour aplicativo tootake aproveitar novas funcionalidades se desejar.</span><span class="sxs-lookup"><span data-stu-id="66718-186">Finally, once you've fixed any build errors, you can make changes tooyour application tootake advantage of new functionality if you wish.</span></span>

<a name="ListOfChangesV1"></a>

### <a name="list-of-breaking-changes-in-version-11"></a><span data-ttu-id="66718-187">Lista de alterações significativas na versão 1.1</span><span class="sxs-lookup"><span data-stu-id="66718-187">List of breaking changes in version 1.1</span></span>
<span data-ttu-id="66718-188">Olá lista a seguir é ordenada pela probabilidade de saudação que a alteração de saudação afetará o código do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="66718-188">hello following list is ordered by hello likelihood that hello change will affect your application code.</span></span>

#### <a name="indexbatch-and-indexaction-changes"></a><span data-ttu-id="66718-189">Alterações de IndexBatch e IndexAction</span><span class="sxs-lookup"><span data-stu-id="66718-189">IndexBatch and IndexAction changes</span></span>
<span data-ttu-id="66718-190">`IndexBatch.Create`foi renomeado muito`IndexBatch.New` e não tem mais um `params` argumento.</span><span class="sxs-lookup"><span data-stu-id="66718-190">`IndexBatch.Create` has been renamed too`IndexBatch.New` and no longer has a `params` argument.</span></span> <span data-ttu-id="66718-191">Você pode usar `IndexBatch.New` para lotes que combinam tipos diferentes de ações (mesclagens, exclusões, etc.).</span><span class="sxs-lookup"><span data-stu-id="66718-191">You can use `IndexBatch.New` for batches that mix different types of actions (merges, deletes, etc.).</span></span> <span data-ttu-id="66718-192">Além disso, há novos métodos estáticos para a criação de lotes em que todas as ações de saudação são Olá mesmo: `Delete`, `Merge`, `MergeOrUpload`, e `Upload`.</span><span class="sxs-lookup"><span data-stu-id="66718-192">In addition, there are new static methods for creating batches where all hello actions are hello same: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.</span></span>

<span data-ttu-id="66718-193">`IndexAction` não tem mais construtores públicos e suas propriedades agora são imutáveis.</span><span class="sxs-lookup"><span data-stu-id="66718-193">`IndexAction` no longer has public constructors and its properties are now immutable.</span></span> <span data-ttu-id="66718-194">Você deve usar os novos métodos estáticos de saudação para a criação de ações para finalidades diferentes: `Delete`, `Merge`, `MergeOrUpload`, e `Upload`.</span><span class="sxs-lookup"><span data-stu-id="66718-194">You should use hello new static methods for creating actions for different purposes: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.</span></span> <span data-ttu-id="66718-195">`IndexAction.Create` foi removido.</span><span class="sxs-lookup"><span data-stu-id="66718-195">`IndexAction.Create` has been removed.</span></span> <span data-ttu-id="66718-196">Se você usou a sobrecarga de saudação que usa apenas um documento, verifique se toouse `Upload` em vez disso.</span><span class="sxs-lookup"><span data-stu-id="66718-196">If you used hello overload that takes only a document, make sure toouse `Upload` instead.</span></span>

##### <a name="example"></a><span data-ttu-id="66718-197">Exemplo</span><span class="sxs-lookup"><span data-stu-id="66718-197">Example</span></span>
<span data-ttu-id="66718-198">Se o seu código tiver esta aparência:</span><span class="sxs-lookup"><span data-stu-id="66718-198">If your code looks like this:</span></span>

    var batch = IndexBatch.Create(documents.Select(doc => IndexAction.Create(doc)));
    indexClient.Documents.Index(batch);

<span data-ttu-id="66718-199">Você pode alterá-la toothis toofix qualquer erro de compilação:</span><span class="sxs-lookup"><span data-stu-id="66718-199">You can change it toothis toofix any build errors:</span></span>

    var batch = IndexBatch.New(documents.Select(doc => IndexAction.Upload(doc)));
    indexClient.Documents.Index(batch);

<span data-ttu-id="66718-200">Se desejar, você pode simplificar-toothis:</span><span class="sxs-lookup"><span data-stu-id="66718-200">If you want, you can further simplify it toothis:</span></span>

    var batch = IndexBatch.Upload(documents);
    indexClient.Documents.Index(batch);

#### <a name="indexbatchexception-changes"></a><span data-ttu-id="66718-201">Alterações de IndexBatchException</span><span class="sxs-lookup"><span data-stu-id="66718-201">IndexBatchException changes</span></span>
<span data-ttu-id="66718-202">Olá `IndexBatchException.IndexResponse` propriedade foi renomeada muito`IndexingResults`, e seu tipo é agora `IList<IndexingResult>`.</span><span class="sxs-lookup"><span data-stu-id="66718-202">hello `IndexBatchException.IndexResponse` property has been renamed too`IndexingResults`, and its type is now `IList<IndexingResult>`.</span></span>

##### <a name="example"></a><span data-ttu-id="66718-203">Exemplo</span><span class="sxs-lookup"><span data-stu-id="66718-203">Example</span></span>
<span data-ttu-id="66718-204">Se o seu código tiver esta aparência:</span><span class="sxs-lookup"><span data-stu-id="66718-204">If your code looks like this:</span></span>

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexResponse.Results.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<span data-ttu-id="66718-205">Você pode alterá-la toothis toofix qualquer erro de compilação:</span><span class="sxs-lookup"><span data-stu-id="66718-205">You can change it toothis toofix any build errors:</span></span>

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<a name="OperationMethodChanges"></a>

#### <a name="operation-method-changes"></a><span data-ttu-id="66718-206">Alterações de método de operação</span><span class="sxs-lookup"><span data-stu-id="66718-206">Operation method changes</span></span>
<span data-ttu-id="66718-207">Cada operação no hello SDK .NET da pesquisa do Azure é exposta como um conjunto de sobrecargas do método para chamadores síncronos e assíncronos.</span><span class="sxs-lookup"><span data-stu-id="66718-207">Each operation in hello Azure Search .NET SDK is exposed as a set of method overloads for synchronous and asynchronous callers.</span></span> <span data-ttu-id="66718-208">Olá assinaturas e fatorar essas sobrecargas de método foi alterado na versão 1.1.</span><span class="sxs-lookup"><span data-stu-id="66718-208">hello signatures and factoring of these method overloads has changed in version 1.1.</span></span>

<span data-ttu-id="66718-209">Por exemplo, Olá operação "Obter estatísticas de índice" em versões anteriores do SDK do hello expostos estas assinaturas:</span><span class="sxs-lookup"><span data-stu-id="66718-209">For example, hello "Get Index Statistics" operation in older versions of hello SDK exposed these signatures:</span></span>

<span data-ttu-id="66718-210">Em `IIndexOperations`:</span><span class="sxs-lookup"><span data-stu-id="66718-210">In `IIndexOperations`:</span></span>

    // Asynchronous operation with all parameters
    Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        string indexName,
        CancellationToken cancellationToken);

<span data-ttu-id="66718-211">Em `IndexOperationsExtensions`:</span><span class="sxs-lookup"><span data-stu-id="66718-211">In `IndexOperationsExtensions`:</span></span>

    // Asynchronous operation with only required parameters
    public static Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        this IIndexOperations operations,
        string indexName);

    // Synchronous operation with only required parameters
    public static IndexGetStatisticsResponse GetStatistics(
        this IIndexOperations operations,
        string indexName);

<span data-ttu-id="66718-212">assinaturas de método Olá para Olá a mesma operação na versão 1.1 esta aparência:</span><span class="sxs-lookup"><span data-stu-id="66718-212">hello method signatures for hello same operation in version 1.1 look like this:</span></span>

<span data-ttu-id="66718-213">Em `IIndexesOperations`:</span><span class="sxs-lookup"><span data-stu-id="66718-213">In `IIndexesOperations`:</span></span>

    // Asynchronous operation with lower-level HTTP features exposed
    Task<AzureOperationResponse<IndexGetStatisticsResult>> GetStatisticsWithHttpMessagesAsync(
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        Dictionary<string, List<string>> customHeaders = null,
        CancellationToken cancellationToken = default(CancellationToken));

<span data-ttu-id="66718-214">Em `IndexesOperationsExtensions`:</span><span class="sxs-lookup"><span data-stu-id="66718-214">In `IndexesOperationsExtensions`:</span></span>

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

<span data-ttu-id="66718-215">Olá SDK .NET da pesquisa do Azure a partir da versão 1.1, organiza os métodos de operação diferente:</span><span class="sxs-lookup"><span data-stu-id="66718-215">Starting with version 1.1, hello Azure Search .NET SDK organizes operation methods differently:</span></span>

* <span data-ttu-id="66718-216">Os parâmetros opcionais agora são modelados como padrão em vez de sobrecargas de método adicionais.</span><span class="sxs-lookup"><span data-stu-id="66718-216">Optional parameters are now modeled as default parameters rather than additional method overloads.</span></span> <span data-ttu-id="66718-217">Isso reduz o número de saudação de sobrecargas do método, às vezes drasticamente.</span><span class="sxs-lookup"><span data-stu-id="66718-217">This reduces hello number of method overloads, sometimes dramatically.</span></span>
* <span data-ttu-id="66718-218">métodos de extensão Olá agora ocultam muitos detalhes estranhas saudação do HTTP do chamador hello.</span><span class="sxs-lookup"><span data-stu-id="66718-218">hello extension methods now hide a lot of hello extraneous details of HTTP from hello caller.</span></span> <span data-ttu-id="66718-219">Por exemplo, versões mais antigas do hello SDK retornou um objeto de resposta com um código de status HTTP, que você geralmente não precisam toocheck porque métodos de operação gerar `CloudException` para qualquer código de status que indica um erro.</span><span class="sxs-lookup"><span data-stu-id="66718-219">For example, older versions of hello SDK returned a response object with an HTTP status code, which you often didn't need toocheck because operation methods throw `CloudException` for any status code that indicates an error.</span></span> <span data-ttu-id="66718-220">Olá novos objetos de modelo apenas retorno de métodos de extensão, economiza Olá problemas de ter toounwrap-los em seu código.</span><span class="sxs-lookup"><span data-stu-id="66718-220">hello new extension methods just return model objects, saving you hello trouble of having toounwrap them in your code.</span></span>
* <span data-ttu-id="66718-221">Por outro lado, hello interfaces principais agora expõem os métodos que oferecem mais controle no nível de saudação HTTP se necessário.</span><span class="sxs-lookup"><span data-stu-id="66718-221">Conversely, hello core interfaces now expose methods that give you more control at hello HTTP level if you need it.</span></span> <span data-ttu-id="66718-222">Agora você pode transmitir toobe de cabeçalhos HTTP personalizado incluído em solicitações e Olá novo `AzureOperationResponse<T>` retornar tipo fornece acesso direto toohello `HttpRequestMessage` e `HttpResponseMessage` para operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="66718-222">You can now pass in custom HTTP headers toobe included in requests, and hello new `AzureOperationResponse<T>` return type gives you direct access toohello `HttpRequestMessage` and `HttpResponseMessage` for hello operation.</span></span> <span data-ttu-id="66718-223">`AzureOperationResponse`é definido em Olá `Microsoft.Rest.Azure` namespace e substitui `Hyak.Common.OperationResponse`.</span><span class="sxs-lookup"><span data-stu-id="66718-223">`AzureOperationResponse` is defined in hello `Microsoft.Rest.Azure` namespace and replaces `Hyak.Common.OperationResponse`.</span></span>

#### <a name="scoringparameters-changes"></a><span data-ttu-id="66718-224">Alterações de ScoringParameters</span><span class="sxs-lookup"><span data-stu-id="66718-224">ScoringParameters changes</span></span>
<span data-ttu-id="66718-225">Uma nova classe chamada `ScoringParameter` foi adicionado no hello toomake SDK mais recente perfis de tooscoring mais fácil do tooprovide parâmetros em uma consulta de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="66718-225">A new class named `ScoringParameter` has been added in hello latest SDK toomake it easier tooprovide parameters tooscoring profiles in a search query.</span></span> <span data-ttu-id="66718-226">Olá anteriormente `ScoringProfiles` propriedade Olá `SearchParameters` classe foi digitada como `IList<string>`; Agora, ele é digitado como `IList<ScoringParameter>`.</span><span class="sxs-lookup"><span data-stu-id="66718-226">Previously hello `ScoringProfiles` property of hello `SearchParameters` class was typed as `IList<string>`; Now it is typed as `IList<ScoringParameter>`.</span></span>

##### <a name="example"></a><span data-ttu-id="66718-227">Exemplo</span><span class="sxs-lookup"><span data-stu-id="66718-227">Example</span></span>
<span data-ttu-id="66718-228">Se o seu código tiver esta aparência:</span><span class="sxs-lookup"><span data-stu-id="66718-228">If your code looks like this:</span></span>

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters = new[] { "featuredParam-featured", "mapCenterParam-" + lon + "," + lat };

<span data-ttu-id="66718-229">Você pode alterá-la toothis toofix qualquer erro de compilação:</span><span class="sxs-lookup"><span data-stu-id="66718-229">You can change it toothis toofix any build errors:</span></span> 

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters =
        new[]
        {
            new ScoringParameter("featuredParam", new[] { "featured" }),
            new ScoringParameter("mapCenterParam", GeographyPoint.Create(lat, lon))
        };

#### <a name="model-class-changes"></a><span data-ttu-id="66718-230">Alterações no modelo de classe</span><span class="sxs-lookup"><span data-stu-id="66718-230">Model class changes</span></span>
<span data-ttu-id="66718-231">Devido a alterações de assinatura toohello descritas na [alterações de método da operação](#OperationMethodChanges), muitas classes em Olá `Microsoft.Azure.Search.Models` namespace foram renomeados ou removidos.</span><span class="sxs-lookup"><span data-stu-id="66718-231">Due toohello signature changes described in [Operation method changes](#OperationMethodChanges), many classes in hello `Microsoft.Azure.Search.Models` namespace have been renamed or removed.</span></span> <span data-ttu-id="66718-232">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="66718-232">For example:</span></span>

* <span data-ttu-id="66718-233">`IndexDefinitionResponse` foi substituído por `AzureOperationResponse<Index>`</span><span class="sxs-lookup"><span data-stu-id="66718-233">`IndexDefinitionResponse` has been replaced by `AzureOperationResponse<Index>`</span></span>
* <span data-ttu-id="66718-234">`DocumentSearchResponse`foi renomeado muito`DocumentSearchResult`</span><span class="sxs-lookup"><span data-stu-id="66718-234">`DocumentSearchResponse` has been renamed too`DocumentSearchResult`</span></span>
* <span data-ttu-id="66718-235">`IndexResult`foi renomeado muito`IndexingResult`</span><span class="sxs-lookup"><span data-stu-id="66718-235">`IndexResult` has been renamed too`IndexingResult`</span></span>
* <span data-ttu-id="66718-236">`Documents.Count()`agora retorna um `long` com contagem de documentos de saudação em vez de um`DocumentCountResponse`</span><span class="sxs-lookup"><span data-stu-id="66718-236">`Documents.Count()` now returns a `long` with hello document count instead of a `DocumentCountResponse`</span></span>
* <span data-ttu-id="66718-237">`IndexGetStatisticsResponse`foi renomeado muito`IndexGetStatisticsResult`</span><span class="sxs-lookup"><span data-stu-id="66718-237">`IndexGetStatisticsResponse` has been renamed too`IndexGetStatisticsResult`</span></span>
* <span data-ttu-id="66718-238">`IndexListResponse`foi renomeado muito`IndexListResult`</span><span class="sxs-lookup"><span data-stu-id="66718-238">`IndexListResponse` has been renamed too`IndexListResult`</span></span>

<span data-ttu-id="66718-239">toosummarize, `OperationResponse`-as classes derivadas que existiam apenas toowrap um objeto de modelo foram removidos.</span><span class="sxs-lookup"><span data-stu-id="66718-239">toosummarize, `OperationResponse`-derived classes that existed only toowrap a model object have been removed.</span></span> <span data-ttu-id="66718-240">Olá classes restantes tiveram seu sufixo alterado de `Response` muito`Result`.</span><span class="sxs-lookup"><span data-stu-id="66718-240">hello remaining classes have had their suffix changed from `Response` too`Result`.</span></span>

##### <a name="example"></a><span data-ttu-id="66718-241">Exemplo</span><span class="sxs-lookup"><span data-stu-id="66718-241">Example</span></span>
<span data-ttu-id="66718-242">Se o seu código tiver esta aparência:</span><span class="sxs-lookup"><span data-stu-id="66718-242">If your code looks like this:</span></span>

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

<span data-ttu-id="66718-243">Você pode alterá-la toothis toofix qualquer erro de compilação:</span><span class="sxs-lookup"><span data-stu-id="66718-243">You can change it toothis toofix any build errors:</span></span>

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

##### <a name="response-classes-and-ienumerable"></a><span data-ttu-id="66718-244">Classes de resposta e IEnumerable</span><span class="sxs-lookup"><span data-stu-id="66718-244">Response classes and IEnumerable</span></span>
<span data-ttu-id="66718-245">Outra alteração que pode afetar o código é que as classes de resposta que contêm coleções não implementam mais `IEnumerable<T>`.</span><span class="sxs-lookup"><span data-stu-id="66718-245">An additional change that may affect your code is that response classes that hold collections no longer implement `IEnumerable<T>`.</span></span> <span data-ttu-id="66718-246">Em vez disso, você pode acessar diretamente as propriedade de coleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="66718-246">Instead, you can access hello collection property directly.</span></span> <span data-ttu-id="66718-247">Por exemplo, se o seu código tiver esta aparência:</span><span class="sxs-lookup"><span data-stu-id="66718-247">For example, if your code looks like this:</span></span>

    DocumentSearchResponse<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response)
    {
        Console.WriteLine(result.Document);
    }

<span data-ttu-id="66718-248">Você pode alterá-la toothis toofix qualquer erro de compilação:</span><span class="sxs-lookup"><span data-stu-id="66718-248">You can change it toothis toofix any build errors:</span></span>

    DocumentSearchResult<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response.Results)
    {
        Console.WriteLine(result.Document);
    }

##### <a name="special-case-for-web-applications"></a><span data-ttu-id="66718-249">Caso especial para aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="66718-249">Special case for web applications</span></span>
<span data-ttu-id="66718-250">Se você tiver um aplicativo web que serializa `DocumentSearchResponse` diretamente os resultados da pesquisa de toosend toohello navegador, você precisará toochange seu código ou resultados de saudação não irá serializar corretamente.</span><span class="sxs-lookup"><span data-stu-id="66718-250">If you have a web application that serializes `DocumentSearchResponse` directly toosend search results toohello browser, you will need toochange your code or hello results will not serialize correctly.</span></span> <span data-ttu-id="66718-251">Por exemplo, se o seu código tiver esta aparência:</span><span class="sxs-lookup"><span data-stu-id="66718-251">For example, if your code looks like this:</span></span>

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

<span data-ttu-id="66718-252">Você pode alterá-lo, obtendo Olá `.Results` propriedade de processamento de resultados de pesquisa Olá pesquisa resposta toofix:</span><span class="sxs-lookup"><span data-stu-id="66718-252">You can change it by getting hello `.Results` property of hello search response toofix search result rendering:</span></span>

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

<span data-ttu-id="66718-253">Você terá toolook para esses casos em seu código. **compilador Olá não emitirá um aviso** porque `JsonResult.Data` é do tipo `object`.</span><span class="sxs-lookup"><span data-stu-id="66718-253">You will have toolook for such cases in your code yourself; **hello compiler will not warn you** because `JsonResult.Data` is of type `object`.</span></span>

#### <a name="cloudexception-changes"></a><span data-ttu-id="66718-254">Alterações de CloudException</span><span class="sxs-lookup"><span data-stu-id="66718-254">CloudException changes</span></span>
<span data-ttu-id="66718-255">Olá `CloudException` classe foi movido de saudação `Hyak.Common` toohello namespace `Microsoft.Rest.Azure` namespace.</span><span class="sxs-lookup"><span data-stu-id="66718-255">hello `CloudException` class has moved from hello `Hyak.Common` namespace toohello `Microsoft.Rest.Azure` namespace.</span></span> <span data-ttu-id="66718-256">Além disso, sua `Error` propriedade foi renomeada muito`Body`.</span><span class="sxs-lookup"><span data-stu-id="66718-256">Also, its `Error` property has been renamed too`Body`.</span></span>

#### <a name="searchserviceclient-and-searchindexclient-changes"></a><span data-ttu-id="66718-257">Alterações de SearchServiceClient e SearchIndexClient</span><span class="sxs-lookup"><span data-stu-id="66718-257">SearchServiceClient and SearchIndexClient changes</span></span>
<span data-ttu-id="66718-258">Olá tipo de saudação `Credentials` propriedade foi alterada de `SearchCredentials` tooits classe de base `ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="66718-258">hello type of hello `Credentials` property has changed from `SearchCredentials` tooits base class, `ServiceClientCredentials`.</span></span> <span data-ttu-id="66718-259">Se você precisar Olá tooaccess `SearchCredentials` de um `SearchIndexClient` ou `SearchServiceClient`, use Olá novo `SearchCredentials` propriedade.</span><span class="sxs-lookup"><span data-stu-id="66718-259">If you need tooaccess hello `SearchCredentials` of a `SearchIndexClient` or `SearchServiceClient`, please use hello new `SearchCredentials` property.</span></span>

<span data-ttu-id="66718-260">Em versões mais antigas do hello SDK, `SearchServiceClient` e `SearchIndexClient` tinha construtores que levaram um `HttpClient` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="66718-260">In older versions of hello SDK, `SearchServiceClient` and `SearchIndexClient` had constructors that took an `HttpClient` parameter.</span></span> <span data-ttu-id="66718-261">Eles foram substituídos por construtores que usam um `HttpClientHandler` e uma matriz de objetos `DelegatingHandler`.</span><span class="sxs-lookup"><span data-stu-id="66718-261">These have been replaced with constructors that take an `HttpClientHandler` and an array of `DelegatingHandler` objects.</span></span> <span data-ttu-id="66718-262">Isso torna mais fácil tooinstall manipuladores personalizados toopre processo solicitações HTTP se necessário.</span><span class="sxs-lookup"><span data-stu-id="66718-262">This makes it easier tooinstall custom handlers toopre-process HTTP requests if necessary.</span></span>

<span data-ttu-id="66718-263">Por fim, Olá construtores que levaram um `Uri` e `SearchCredentials` foram alterados.</span><span class="sxs-lookup"><span data-stu-id="66718-263">Finally, hello constructors that took a `Uri` and `SearchCredentials` have changed.</span></span> <span data-ttu-id="66718-264">Por exemplo, se você tiver código parecido com este:</span><span class="sxs-lookup"><span data-stu-id="66718-264">For example, if you have code that looks like this:</span></span>

    var client =
        new SearchServiceClient(
            new SearchCredentials("abc123"),
            new Uri("http://myservice.search.windows.net"));

<span data-ttu-id="66718-265">Você pode alterá-la toothis toofix qualquer erro de compilação:</span><span class="sxs-lookup"><span data-stu-id="66718-265">You can change it toothis toofix any build errors:</span></span>

    var client =
        new SearchServiceClient(
            new Uri("http://myservice.search.windows.net"),
            new SearchCredentials("abc123"));

<span data-ttu-id="66718-266">Também Observe que o tipo de saudação do hello credenciais parâmetro mudou muito`ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="66718-266">Also note that hello type of hello credentials parameter has changed too`ServiceClientCredentials`.</span></span> <span data-ttu-id="66718-267">Isso é improvável que tooaffect seu código desde `SearchCredentials` é derivado de `ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="66718-267">This is unlikely tooaffect your code since `SearchCredentials` is derived from `ServiceClientCredentials`.</span></span>

#### <a name="passing-a-request-id"></a><span data-ttu-id="66718-268">Passando uma ID de solicitação</span><span class="sxs-lookup"><span data-stu-id="66718-268">Passing a request ID</span></span>
<span data-ttu-id="66718-269">Em versões mais antigas do hello SDK, você pode definir uma ID de solicitação em Olá `SearchServiceClient` ou `SearchIndexClient` e deve ser incluído em cada solicitação toohello API REST.</span><span class="sxs-lookup"><span data-stu-id="66718-269">In older versions of hello SDK, you could set a request ID on hello `SearchServiceClient` or `SearchIndexClient` and it would be included in every request toohello REST API.</span></span> <span data-ttu-id="66718-270">Isso é útil para solucionar problemas com o serviço de pesquisa, se você precisar de suporte de toocontact.</span><span class="sxs-lookup"><span data-stu-id="66718-270">This is useful for troubleshooting issues with your search service if you need toocontact support.</span></span> <span data-ttu-id="66718-271">No entanto, é mais útil tooset uma ID de solicitação exclusivo para cada operação em vez de toouse Olá a mesma ID para todas as operações.</span><span class="sxs-lookup"><span data-stu-id="66718-271">However, it is more useful tooset a unique request ID for every operation rather than toouse hello same ID for all operations.</span></span> <span data-ttu-id="66718-272">Por esse motivo, Olá `SetClientRequestId` métodos de `SearchServiceClient` e `SearchIndexClient` foram removidos.</span><span class="sxs-lookup"><span data-stu-id="66718-272">For this reason, hello `SetClientRequestId` methods of `SearchServiceClient` and `SearchIndexClient` have been removed.</span></span> <span data-ttu-id="66718-273">Em vez disso, você pode passar um método de operação de tooeach de ID de solicitação por meio de saudação opcional `SearchRequestOptions` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="66718-273">Instead, you can pass a request ID tooeach operation method via hello optional `SearchRequestOptions` parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="66718-274">Em uma versão futura do hello SDK, vamos adicionar um novo mecanismo para configurar uma ID de solicitação globalmente em cliente hello, objetos que é consistente com a abordagem de saudação usada por outros SDKs do Azure.</span><span class="sxs-lookup"><span data-stu-id="66718-274">In a future release of hello SDK, we will add a new mechanism for setting a request ID globally on hello client objects that is consistent with hello approach used by other Azure SDKs.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="66718-275">Exemplo</span><span class="sxs-lookup"><span data-stu-id="66718-275">Example</span></span>
<span data-ttu-id="66718-276">Se você tiver um código parecido com este:</span><span class="sxs-lookup"><span data-stu-id="66718-276">If you have code that looks like this:</span></span>

    client.SetClientRequestId(Guid.NewGuid());
    ...
    long count = client.Documents.Count();

<span data-ttu-id="66718-277">Você pode alterá-la toothis toofix qualquer erro de compilação:</span><span class="sxs-lookup"><span data-stu-id="66718-277">You can change it toothis toofix any build errors:</span></span>

    long count = client.Documents.Count(new SearchRequestOptions(requestId: Guid.NewGuid()));

#### <a name="interface-name-changes"></a><span data-ttu-id="66718-278">Alterações de nome de interface</span><span class="sxs-lookup"><span data-stu-id="66718-278">Interface name changes</span></span>
<span data-ttu-id="66718-279">nomes de interface do grupo de operação Olá ter todos os toobe alterados consistente com os nomes de propriedade correspondentes:</span><span class="sxs-lookup"><span data-stu-id="66718-279">hello operation group interface names have all changed toobe consistent with their corresponding property names:</span></span>

* <span data-ttu-id="66718-280">Olá tipo de `ISearchServiceClient.Indexes` foi renomeado de `IIndexOperations` muito`IIndexesOperations`.</span><span class="sxs-lookup"><span data-stu-id="66718-280">hello type of `ISearchServiceClient.Indexes` has been renamed from `IIndexOperations` too`IIndexesOperations`.</span></span>
* <span data-ttu-id="66718-281">Olá tipo de `ISearchServiceClient.Indexers` foi renomeado de `IIndexerOperations` muito`IIndexersOperations`.</span><span class="sxs-lookup"><span data-stu-id="66718-281">hello type of `ISearchServiceClient.Indexers` has been renamed from `IIndexerOperations` too`IIndexersOperations`.</span></span>
* <span data-ttu-id="66718-282">Olá tipo de `ISearchServiceClient.DataSources` foi renomeado de `IDataSourceOperations` muito`IDataSourcesOperations`.</span><span class="sxs-lookup"><span data-stu-id="66718-282">hello type of `ISearchServiceClient.DataSources` has been renamed from `IDataSourceOperations` too`IDataSourcesOperations`.</span></span>
* <span data-ttu-id="66718-283">Olá tipo de `ISearchIndexClient.Documents` foi renomeado de `IDocumentOperations` muito`IDocumentsOperations`.</span><span class="sxs-lookup"><span data-stu-id="66718-283">hello type of `ISearchIndexClient.Documents` has been renamed from `IDocumentOperations` too`IDocumentsOperations`.</span></span>

<span data-ttu-id="66718-284">Essa alteração é improvável que tooaffect seu código, a menos que você criou as simulações dessas interfaces para fins de teste.</span><span class="sxs-lookup"><span data-stu-id="66718-284">This change is unlikely tooaffect your code unless you created mocks of these interfaces for test purposes.</span></span>

<a name="BugFixesV1"></a>

### <a name="bug-fixes-in-version-11"></a><span data-ttu-id="66718-285">Correções de bug na versão 1.1</span><span class="sxs-lookup"><span data-stu-id="66718-285">Bug fixes in version 1.1</span></span>
<span data-ttu-id="66718-286">Havia um bug nas versões anteriores do SDK .NET da pesquisa do Azure de saudação tooserialization relacionado de classes de modelo personalizado.</span><span class="sxs-lookup"><span data-stu-id="66718-286">There was a bug in older versions of hello Azure Search .NET SDK relating tooserialization of custom model classes.</span></span> <span data-ttu-id="66718-287">bug Olá pode ocorrer se você tiver criado uma classe de modelo personalizado com uma propriedade de um tipo de valor não nulo.</span><span class="sxs-lookup"><span data-stu-id="66718-287">hello bug could occur if you created a custom model class with a property of a non-nullable value type.</span></span>

#### <a name="steps-tooreproduce"></a><span data-ttu-id="66718-288">Etapas tooreproduce</span><span class="sxs-lookup"><span data-stu-id="66718-288">Steps tooreproduce</span></span>
<span data-ttu-id="66718-289">Crie uma classe de modelo personalizada com uma propriedade de tipo de valor não anulável.</span><span class="sxs-lookup"><span data-stu-id="66718-289">Create a custom model class with a property of non-nullable value type.</span></span> <span data-ttu-id="66718-290">Por exemplo, adicione uma propriedade `UnitCount` pública do tipo `int` em vez de `int?`.</span><span class="sxs-lookup"><span data-stu-id="66718-290">For example, add a public `UnitCount` property of type `int` instead of `int?`.</span></span>

<span data-ttu-id="66718-291">Se você indexar um documento com o valor padrão de saudação do mesmo tipo (por exemplo, 0 para `int`), o campo de saudação será nulo na pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="66718-291">If you index a document with hello default value of that type (for example, 0 for `int`), hello field will be null in Azure Search.</span></span> <span data-ttu-id="66718-292">Se você pesquisar posteriormente para o documento, Olá `Search` chamada lançará `JsonSerializationException` indicando que não é possível converter `null` muito`int`.</span><span class="sxs-lookup"><span data-stu-id="66718-292">If you subsequently search for that document, hello `Search` call will throw `JsonSerializationException` complaining that it can't convert `null` too`int`.</span></span>

<span data-ttu-id="66718-293">Além disso, os filtros podem não funcionar conforme o esperado como nulo foi escrito toohello índice em vez do valor de saudação que se destina.</span><span class="sxs-lookup"><span data-stu-id="66718-293">Also, filters may not work as expected since null was written toohello index instead of hello intended value.</span></span>

#### <a name="fix-details"></a><span data-ttu-id="66718-294">Corrigir detalhes</span><span class="sxs-lookup"><span data-stu-id="66718-294">Fix details</span></span>
<span data-ttu-id="66718-295">Corrigimos o problema na versão 1.1 do hello SDK.</span><span class="sxs-lookup"><span data-stu-id="66718-295">We have fixed this issue in version 1.1 of hello SDK.</span></span> <span data-ttu-id="66718-296">Agora, se você tiver uma classe de modelo como esta:</span><span class="sxs-lookup"><span data-stu-id="66718-296">Now, if you have a model class like this:</span></span>

    public class Model
    {
        public string Key { get; set; }

        public int IntValue { get; set; }
    }

<span data-ttu-id="66718-297">e você definir `IntValue` too0, que valor agora está corretamente serializado como 0 na transmissão de saudação e armazenado como 0 no índice de saudação.</span><span class="sxs-lookup"><span data-stu-id="66718-297">and you set `IntValue` too0, that value is now correctly serialized as 0 on hello wire and stored as 0 in hello index.</span></span> <span data-ttu-id="66718-298">A viagem de ida e volta também funciona conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="66718-298">Round tripping also works as expected.</span></span>

<span data-ttu-id="66718-299">Há um toobe problema potencial atento com essa abordagem: se você usar um tipo de modelo com uma propriedade não anulável, você tem muito**garante** sem documentos no índice contêm um valor nulo para o campo correspondente do hello.</span><span class="sxs-lookup"><span data-stu-id="66718-299">There is one potential issue toobe aware of with this approach: If you use a model type with a non-nullable property, you have too**guarantee** that no documents in your index contain a null value for hello corresponding field.</span></span> <span data-ttu-id="66718-300">Olá SDK, nem Olá API de REST de pesquisa do Azure ajudará você tooenforce isso.</span><span class="sxs-lookup"><span data-stu-id="66718-300">Neither hello SDK nor hello Azure Search REST API will help you tooenforce this.</span></span>

<span data-ttu-id="66718-301">Isso não é apenas uma preocupação hipotética: Imagine um cenário em que você adicionar um novo campo tooan índice existente que é do tipo `Edm.Int32`.</span><span class="sxs-lookup"><span data-stu-id="66718-301">This is not just a hypothetical concern: Imagine a scenario where you add a new field tooan existing index that is of type `Edm.Int32`.</span></span> <span data-ttu-id="66718-302">Depois de atualizar a definição de índice hello, todos os documentos terá um valor nulo para esse novo campo (desde que todos os tipos são anuláveis na pesquisa do Azure).</span><span class="sxs-lookup"><span data-stu-id="66718-302">After updating hello index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="66718-303">Se você usar uma classe de modelo com um não anulável `int` propriedade para esse campo, você receberá um `JsonSerializationException` assim ao tentar tooretrieve documentos:</span><span class="sxs-lookup"><span data-stu-id="66718-303">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying tooretrieve documents:</span></span>

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="66718-304">Por esse motivo, continuamos a recomendar que você use tipos anuláveis nas suas classes de modelo como uma prática recomendada.</span><span class="sxs-lookup"><span data-stu-id="66718-304">For this reason, we still recommend that you use nullable types in your model classes as a best practice.</span></span>

<span data-ttu-id="66718-305">Para obter mais detalhes sobre essa correção de bug e hello, consulte [esse problema no GitHub](https://github.com/Azure/azure-sdk-for-net/issues/1063).</span><span class="sxs-lookup"><span data-stu-id="66718-305">For more details on this bug and hello fix, please see [this issue on GitHub](https://github.com/Azure/azure-sdk-for-net/issues/1063).</span></span>

