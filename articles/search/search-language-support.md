---
title: "aaaAzure vários idiomas de pesquisa | Microsoft Docs"
description: "A Pesquisa do Azure dá suporte a 56 idiomas, aproveitando os analisadores de linguagem da Lucene e a tecnologia Processamento de Linguagem Natural da Microsoft."
services: search
documentationcenter: 
author: yahnoosh
manager: pablocas
editor: 
ms.assetid: 55a00b44-804d-41bb-9c96-e6ea498616f5
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/23/2017
ms.author: jlembicz
ms.openlocfilehash: 9a2e567a82ee563521c12ea320f6c484a8e73f04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-index-for-documents-in-multiple-languages-in-azure-search"></a><span data-ttu-id="0d1cb-103">Crie um índice para documentos em vários idiomas na Pesquisa do Azure</span><span class="sxs-lookup"><span data-stu-id="0d1cb-103">Create an index for documents in multiple languages in Azure Search</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="0d1cb-104">Portal</span><span class="sxs-lookup"><span data-stu-id="0d1cb-104">Portal</span></span>](search-language-support.md)
> * [<span data-ttu-id="0d1cb-105">REST</span><span class="sxs-lookup"><span data-stu-id="0d1cb-105">REST</span></span>](https://msdn.microsoft.com/library/azure/dn879793.aspx)
> * [<span data-ttu-id="0d1cb-106">.NET</span><span class="sxs-lookup"><span data-stu-id="0d1cb-106">.NET</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.search.models.analyzername.aspx)
>
>

<span data-ttu-id="0d1cb-107">Unleashing power Olá de analisadores de idioma é tão fácil quanto uma propriedade de configuração em um campo de pesquisa na definição de índice de saudação.</span><span class="sxs-lookup"><span data-stu-id="0d1cb-107">Unleashing hello power of language analyzers is as easy as setting one property on a searchable field in hello index definition.</span></span> <span data-ttu-id="0d1cb-108">Agora você pode executar esta etapa no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="0d1cb-108">Now you can do this step in hello portal.</span></span>

<span data-ttu-id="0d1cb-109">Abaixo estão capturas de tela de saudação folhas de Portal do Azure para pesquisa do Azure que permitem que os usuários toodefine um esquema de índice.</span><span class="sxs-lookup"><span data-stu-id="0d1cb-109">Below are screenshots of hello Azure Portal blades for Azure Search that allow users toodefine an index schema.</span></span> <span data-ttu-id="0d1cb-110">Desta folha, os usuários podem criar todos os campos de saudação e defina a propriedade de analisador de saudação para cada um deles.</span><span class="sxs-lookup"><span data-stu-id="0d1cb-110">From this blade, users can create all of hello fields and set hello analyzer property for each of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0d1cb-111">Somente você pode definir um analisador de idioma durante a definição de campo, como em quando criar um novo índice de saudação de plano de fundo para cima ou ao adicionar um novo índice de campo tooan existente.</span><span class="sxs-lookup"><span data-stu-id="0d1cb-111">You can only set a language analyzer during field definition, as in when creating a new index from hello ground up, or when adding a new field tooan existing index.</span></span> <span data-ttu-id="0d1cb-112">Verifique se que você especificar completamente todos os atributos, incluindo analyzer hello, ao criar o campo de saudação.</span><span class="sxs-lookup"><span data-stu-id="0d1cb-112">Make sure you fully specify all attributes, including hello analyzer, while creating hello field.</span></span> <span data-ttu-id="0d1cb-113">Você não ser capaz de tooedit atributos hello ou altere o tipo de analisador de hello quando você salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="0d1cb-113">You won't be able tooedit hello attributes or change hello analyzer type once you save your changes.</span></span>
>
>

## <a name="define-a-new-field-definition"></a><span data-ttu-id="0d1cb-114">Definir uma nova definição de campo</span><span class="sxs-lookup"><span data-stu-id="0d1cb-114">Define a new field definition</span></span>
1. <span data-ttu-id="0d1cb-115">Entrar toohello [portal do Azure](https://portal.azure.com) e abra Olá blade de serviço do seu serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="0d1cb-115">Sign in toohello [Azure portal](https://portal.azure.com) and open hello service blade of your search service.</span></span>
2. <span data-ttu-id="0d1cb-116">Clique em **Adicionar índice** no comando Olá barra na parte superior de saudação do hello serviço painel toostart um novo índice, ou abra um tooset de índice existente em novos campos que você está adicionando um analisador de índice existente tooan.</span><span class="sxs-lookup"><span data-stu-id="0d1cb-116">Click **Add index** in hello command bar at hello top of hello service dashboard toostart a new index, or open an existing index tooset an analyzer on new fields you're adding tooan existing index.</span></span>
3. <span data-ttu-id="0d1cb-117">folha de campos de saudação for exibida, fornecendo opções para definir o esquema de saudação do índice hello, incluindo Olá analisador guia usado para escolher um analisador de linguagem.</span><span class="sxs-lookup"><span data-stu-id="0d1cb-117">hello Fields blade appears, giving you options for defining hello schema of hello index, including hello Analyzer tab used for choosing a language analyzer.</span></span>
4. <span data-ttu-id="0d1cb-118">Nos campos, inicie uma definição de campo fornecendo um nome, escolhendo o tipo de dados de saudação e a configuração atributos toomark Olá campo como texto completo pesquisável, recuperáveis nos resultados da pesquisa, pode ser usados em estruturas de navegação de faceta, classificável e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="0d1cb-118">In Fields, start a field definition by providing a name, choosing hello data type, and setting attributes toomark hello field as full text searchable, retrievable in search results, usable in facet navigation structures, sortable, and so forth.</span></span>
5. <span data-ttu-id="0d1cb-119">Antes de avançarmos toohello próximo campo, abra Olá **analisador** guia.</span><span class="sxs-lookup"><span data-stu-id="0d1cb-119">Before moving on toohello next field, open hello **Analyzer** tab.</span></span>

<span data-ttu-id="0d1cb-120">![][1]
*tooselect um analisador, clique em Guia do analisador Olá na folha de campos de saudação*</span><span class="sxs-lookup"><span data-stu-id="0d1cb-120">![][1]
*tooselect an analyzer, click hello Analyzer tab on hello Fields blade*</span></span>

## <a name="choose-an-analyzer"></a><span data-ttu-id="0d1cb-121">Escolha um analisador</span><span class="sxs-lookup"><span data-stu-id="0d1cb-121">Choose an analyzer</span></span>
1. <span data-ttu-id="0d1cb-122">Role o campo de saudação toofind que você está definindo.</span><span class="sxs-lookup"><span data-stu-id="0d1cb-122">Scroll toofind hello field you are defining.</span></span>
2. <span data-ttu-id="0d1cb-123">Se você ainda não marcado como campo hello como pesquisa, clique em Olá caixa de seleção agora toomark como **pesquisável**.</span><span class="sxs-lookup"><span data-stu-id="0d1cb-123">If you haven't marked hello field as searchable, click hello checkbox now toomark it as **Searchable**.</span></span>
3. <span data-ttu-id="0d1cb-124">Clique em Olá analisador área toodisplay Olá lista de analisadores disponíveis.</span><span class="sxs-lookup"><span data-stu-id="0d1cb-124">Click hello Analyzer area toodisplay hello list of available analyzers.</span></span>
4. <span data-ttu-id="0d1cb-125">Escolha o analisador Olá toouse desejado.</span><span class="sxs-lookup"><span data-stu-id="0d1cb-125">Choose hello analyzer you want toouse.</span></span>

<span data-ttu-id="0d1cb-126">![][2]
*Selecione um dos analisadores de saudação com suporte para cada campo*</span><span class="sxs-lookup"><span data-stu-id="0d1cb-126">![][2]
*Select one of hello supported analyzers for each field*</span></span>

<span data-ttu-id="0d1cb-127">Por padrão, todos os campos pesquisáveis usam Olá [analisador padrão Lucene](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) que é independente do idioma.</span><span class="sxs-lookup"><span data-stu-id="0d1cb-127">By default, all searchable fields use hello [Standard Lucene analyzer](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) which is language agnostic.</span></span> <span data-ttu-id="0d1cb-128">lista completa de saudação de tooview de analisadores de suporte, consulte [suporte de idioma na pesquisa do Azure](https://msdn.microsoft.com/library/azure/dn879793.aspx).</span><span class="sxs-lookup"><span data-stu-id="0d1cb-128">tooview hello full list of supported analyzers, see [Language Support in Azure Search](https://msdn.microsoft.com/library/azure/dn879793.aspx).</span></span>

<span data-ttu-id="0d1cb-129">Analisador de linguagem Olá selecionada para um campo, ele será usado com cada solicitação de indexação e pesquisa para esse campo.</span><span class="sxs-lookup"><span data-stu-id="0d1cb-129">Once hello language analyzer is selected for a field, it will be used with each indexing and search request for that field.</span></span> <span data-ttu-id="0d1cb-130">Quando uma consulta é feita em vários campos usando analisadores de diferentes, consulta hello será processada independentemente por analisadores de saudação à direita de cada campo.</span><span class="sxs-lookup"><span data-stu-id="0d1cb-130">When a query is issued against multiple fields using different analyzers, hello query will be processed independently by hello right analyzers for each field.</span></span>

<span data-ttu-id="0d1cb-131">Muitos aplicativos web e móveis servem os usuários em todo o mundo hello usando diferentes idiomas.</span><span class="sxs-lookup"><span data-stu-id="0d1cb-131">Many web and mobile applications serve users around hello globe using different languages.</span></span> <span data-ttu-id="0d1cb-132">É possível toodefine um índice para um cenário de como isso criando um campo para cada idioma com suporte.</span><span class="sxs-lookup"><span data-stu-id="0d1cb-132">It’s possible toodefine an index for a scenario like this by creating a field for each language supported.</span></span>

<span data-ttu-id="0d1cb-133">![][3]
*Definição de índice com um campo de descrição para cada idioma com suporte*</span><span class="sxs-lookup"><span data-stu-id="0d1cb-133">![][3]
*Index definition with a description field for each language supported*</span></span>

<span data-ttu-id="0d1cb-134">Se o idioma de saudação do agente Olá emitindo uma consulta for conhecido, uma solicitação de pesquisa pode ser campo específico do escopo tooa usando Olá **searchFields** parâmetro de consulta.</span><span class="sxs-lookup"><span data-stu-id="0d1cb-134">If hello language of hello agent issuing a query is known, a search request can be scoped tooa specific field using hello **searchFields** query parameter.</span></span> <span data-ttu-id="0d1cb-135">Olá consulta a seguir será emitida somente em relação a descrição de saudação em polonês:</span><span class="sxs-lookup"><span data-stu-id="0d1cb-135">hello following query will be issued only against hello description in Polish:</span></span>

`https://[service name].search.windows.net/indexes/[index name]/docs?search=darmowy&searchFields=description_pl&api-version=2016-09-01`

<span data-ttu-id="0d1cb-136">Você pode consultar o índice do portal de saudação usando **pesquisar no Explorador de** toopaste em uma toohello semelhante de consulta mostrada acima.</span><span class="sxs-lookup"><span data-stu-id="0d1cb-136">You can query your index from hello portal, using **Search explorer** toopaste in a query similar toohello one shown above.</span></span> <span data-ttu-id="0d1cb-137">Gerenciador de pesquisa está disponível na barra de comandos de saudação na folha de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="0d1cb-137">Search explorer is available from hello command bar in hello service blade.</span></span> <span data-ttu-id="0d1cb-138">Consulte [consultar seu índice de pesquisa do Azure no portal de saudação](search-explorer.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="0d1cb-138">See [Query your Azure Search index in hello portal](search-explorer.md) for details.</span></span>

<span data-ttu-id="0d1cb-139">Às vezes, hello idioma do agente Olá emitindo uma consulta não for conhecida, no qual caso Olá consulta pode ser emitida em relação a todos os campos simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="0d1cb-139">Sometimes hello language of hello agent issuing a query is not known, in which case hello query can be issued against all fields simultaneously.</span></span> <span data-ttu-id="0d1cb-140">Se necessário, a preferência de resultados em um determinado idioma pode ser definida usando os [perfis de pontuação](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span><span class="sxs-lookup"><span data-stu-id="0d1cb-140">If needed, preference for results in a certain language can be defined using [scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span></span> <span data-ttu-id="0d1cb-141">O exemplo hello abaixo, correspondências encontradas na descrição de saudação em inglês serão totalizadas toomatches relativo mais alto em polonês e francês:</span><span class="sxs-lookup"><span data-stu-id="0d1cb-141">In hello example below, matches found in hello description in English will be scored higher relative toomatches in Polish and French:</span></span>

    "scoringProfiles": [
      {
        "name": "englishFirst",
        "text": {
          "weights": { "description_en": 2 }
        }
      }
    ]

`https://[service name].search.windows.net/indexes/[index name]/docs?search=Microsoft&scoringProfile=englishFirst&api-version=2016-09-01`

<span data-ttu-id="0d1cb-142">Se você for um desenvolvedor do .NET, observe que você pode configurar os analisadores de idioma usando Olá [SDK .NET da pesquisa do Azure](http://www.nuget.org/packages/Microsoft.Azure.Search).</span><span class="sxs-lookup"><span data-stu-id="0d1cb-142">If you're a .NET developer, note that you can configure language analyzers using hello [Azure Search .NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Search).</span></span> <span data-ttu-id="0d1cb-143">versão mais recente de saudação inclui suporte para analisadores de idioma de Microsoft hello também.</span><span class="sxs-lookup"><span data-stu-id="0d1cb-143">hello latest release includes support for hello Microsoft language analyzers as well.</span></span>

<!-- Image References -->
[1]: ./media/search-language-support/AnalyzerTab.png
[2]: ./media/search-language-support/SelectAnalyzer.png
[3]: ./media/search-language-support/IndexDefinition.png
