---
title: "Vários idiomas do Azure Search | Microsoft Docs"
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
ms.openlocfilehash: dbbab31bac66ce73dbf9883992713a2c16581e19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-index-for-documents-in-multiple-languages-in-azure-search"></a><span data-ttu-id="1513a-103">Crie um índice para documentos em vários idiomas na Pesquisa do Azure</span><span class="sxs-lookup"><span data-stu-id="1513a-103">Create an index for documents in multiple languages in Azure Search</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="1513a-104">Portal</span><span class="sxs-lookup"><span data-stu-id="1513a-104">Portal</span></span>](search-language-support.md)
> * [<span data-ttu-id="1513a-105">REST</span><span class="sxs-lookup"><span data-stu-id="1513a-105">REST</span></span>](https://msdn.microsoft.com/library/azure/dn879793.aspx)
> * [<span data-ttu-id="1513a-106">.NET</span><span class="sxs-lookup"><span data-stu-id="1513a-106">.NET</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.search.models.analyzername.aspx)
>
>

<span data-ttu-id="1513a-107">Ampliar o poder dos analisadores de linguagem é tão fácil quanto definir uma propriedade em um campo pesquisável na definição de índice.</span><span class="sxs-lookup"><span data-stu-id="1513a-107">Unleashing the power of language analyzers is as easy as setting one property on a searchable field in the index definition.</span></span> <span data-ttu-id="1513a-108">Agora você pode realizar esta etapa no portal.</span><span class="sxs-lookup"><span data-stu-id="1513a-108">Now you can do this step in the portal.</span></span>

<span data-ttu-id="1513a-109">Veja abaixo as capturas de tela das folhas do Portal do Azure para a Pesquisa do Azure que permitem que os usuários definam um esquema de índice.</span><span class="sxs-lookup"><span data-stu-id="1513a-109">Below are screenshots of the Azure Portal blades for Azure Search that allow users to define an index schema.</span></span> <span data-ttu-id="1513a-110">Nesta folha, os usuários podem criar todos os campos e definir a propriedade do analisador de cada um deles.</span><span class="sxs-lookup"><span data-stu-id="1513a-110">From this blade, users can create all of the fields and set the analyzer property for each of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1513a-111">Você pode definir um analisador de linguagem apenas durante a definição de campo, como ao criar um novo índice do zero ou ao adicionar um novo campo a um índice existente.</span><span class="sxs-lookup"><span data-stu-id="1513a-111">You can only set a language analyzer during field definition, as in when creating a new index from the ground up, or when adding a new field to an existing index.</span></span> <span data-ttu-id="1513a-112">Lembre-se de especificar por completo todos os atributos, incluindo o analisador, ao criar o campo.</span><span class="sxs-lookup"><span data-stu-id="1513a-112">Make sure you fully specify all attributes, including the analyzer, while creating the field.</span></span> <span data-ttu-id="1513a-113">Você não poderá editar os atributos ou alterar o tipo de analisador depois de salvar suas alterações.</span><span class="sxs-lookup"><span data-stu-id="1513a-113">You won't be able to edit the attributes or change the analyzer type once you save your changes.</span></span>
>
>

## <a name="define-a-new-field-definition"></a><span data-ttu-id="1513a-114">Definir uma nova definição de campo</span><span class="sxs-lookup"><span data-stu-id="1513a-114">Define a new field definition</span></span>
1. <span data-ttu-id="1513a-115">Entre no [Portal do Azure](https://portal.azure.com) e abra a folha de serviço do seu serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="1513a-115">Sign in to the [Azure portal](https://portal.azure.com) and open the service blade of your search service.</span></span>
2. <span data-ttu-id="1513a-116">Clique em **Adicionar índice** na barra de comandos localizada na parte superior do painel do serviço para iniciar um novo índice, ou abra um índice existente para definir um analisador nos novos campos que você está adicionando a um índice existente.</span><span class="sxs-lookup"><span data-stu-id="1513a-116">Click **Add index** in the command bar at the top of the service dashboard to start a new index, or open an existing index to set an analyzer on new fields you're adding to an existing index.</span></span>
3. <span data-ttu-id="1513a-117">A folha Campos é exibida, oferecendo opções para definir o esquema do índice, incluindo a guia Analisador, usada para escolher um analisador de linguagem.</span><span class="sxs-lookup"><span data-stu-id="1513a-117">The Fields blade appears, giving you options for defining the schema of the index, including the Analyzer tab used for choosing a language analyzer.</span></span>
4. <span data-ttu-id="1513a-118">Em Campos, inicie uma definição de campo fornecendo um nome, escolhendo o tipo de dados e definindo atributos para marcar o campo como texto completo pesquisável, recuperável nos resultados da pesquisa, usável em estruturas de navegação facetada, classificável e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="1513a-118">In Fields, start a field definition by providing a name, choosing the data type, and setting attributes to mark the field as full text searchable, retrievable in search results, usable in facet navigation structures, sortable, and so forth.</span></span>
5. <span data-ttu-id="1513a-119">Antes de passar para o próximo campo, abra a guia **Analisador** .</span><span class="sxs-lookup"><span data-stu-id="1513a-119">Before moving on to the next field, open the **Analyzer** tab.</span></span>

<span data-ttu-id="1513a-120">![][1]
*Para selecionar um analisador, clique na guia Analisador na folha Campos*</span><span class="sxs-lookup"><span data-stu-id="1513a-120">![][1]
*To select an analyzer, click the Analyzer tab on the Fields blade*</span></span>

## <a name="choose-an-analyzer"></a><span data-ttu-id="1513a-121">Escolha um analisador</span><span class="sxs-lookup"><span data-stu-id="1513a-121">Choose an analyzer</span></span>
1. <span data-ttu-id="1513a-122">Role para encontrar o campo que você está definindo.</span><span class="sxs-lookup"><span data-stu-id="1513a-122">Scroll to find the field you are defining.</span></span>
2. <span data-ttu-id="1513a-123">Se ainda não tiver marcado o campo como pesquisável, clique na caixa de seleção agora para marcá-la como **Pesquisável**.</span><span class="sxs-lookup"><span data-stu-id="1513a-123">If you haven't marked the field as searchable, click the checkbox now to mark it as **Searchable**.</span></span>
3. <span data-ttu-id="1513a-124">Clique na área do Analisador para exibir a lista de analisadores disponíveis.</span><span class="sxs-lookup"><span data-stu-id="1513a-124">Click the Analyzer area to display the list of available analyzers.</span></span>
4. <span data-ttu-id="1513a-125">Escolha o analisador que deseja usar.</span><span class="sxs-lookup"><span data-stu-id="1513a-125">Choose the analyzer you want to use.</span></span>

<span data-ttu-id="1513a-126">![][2]
*Selecione um dos analisadores com suporte para cada campo*</span><span class="sxs-lookup"><span data-stu-id="1513a-126">![][2]
*Select one of the supported analyzers for each field*</span></span>

<span data-ttu-id="1513a-127">Por padrão, todos os campos pesquisáveis usam o [analisador padrão da Lucene](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) que é independente de linguagem.</span><span class="sxs-lookup"><span data-stu-id="1513a-127">By default, all searchable fields use the [Standard Lucene analyzer](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) which is language agnostic.</span></span> <span data-ttu-id="1513a-128">Para exibir a lista completa de analisadores com suporte, veja [Suporte de idioma na Pesquisa do Azure](https://msdn.microsoft.com/library/azure/dn879793.aspx).</span><span class="sxs-lookup"><span data-stu-id="1513a-128">To view the full list of supported analyzers, see [Language Support in Azure Search](https://msdn.microsoft.com/library/azure/dn879793.aspx).</span></span>

<span data-ttu-id="1513a-129">Quando o analisador de linguagem for selecionado para um campo, ele será usado com cada solicitação de indexação e pesquisa para esse campo.</span><span class="sxs-lookup"><span data-stu-id="1513a-129">Once the language analyzer is selected for a field, it will be used with each indexing and search request for that field.</span></span> <span data-ttu-id="1513a-130">Quando uma consulta é executada em vários campos usando analisadores diferentes, a consulta será processada de modo independente pelos analisadores certos para cada campo.</span><span class="sxs-lookup"><span data-stu-id="1513a-130">When a query is issued against multiple fields using different analyzers, the query will be processed independently by the right analyzers for each field.</span></span>

<span data-ttu-id="1513a-131">Muitos aplicativos web e móveis atendem usuários em todo o mundo usando diferentes idiomas.</span><span class="sxs-lookup"><span data-stu-id="1513a-131">Many web and mobile applications serve users around the globe using different languages.</span></span> <span data-ttu-id="1513a-132">É possível definir um índice para um cenário como esse criando um campo para cada idioma com suporte.</span><span class="sxs-lookup"><span data-stu-id="1513a-132">It’s possible to define an index for a scenario like this by creating a field for each language supported.</span></span>

<span data-ttu-id="1513a-133">![][3]
*Definição de índice com um campo de descrição para cada idioma com suporte*</span><span class="sxs-lookup"><span data-stu-id="1513a-133">![][3]
*Index definition with a description field for each language supported*</span></span>

<span data-ttu-id="1513a-134">Se o idioma do agente emissor de uma consulta for conhecido, uma solicitação de pesquisa pode ser definida como escopo para um campo específico usando o parâmetro de consulta **searchFields** .</span><span class="sxs-lookup"><span data-stu-id="1513a-134">If the language of the agent issuing a query is known, a search request can be scoped to a specific field using the **searchFields** query parameter.</span></span> <span data-ttu-id="1513a-135">A seguinte consulta será emitida apenas com a descrição em polonês:</span><span class="sxs-lookup"><span data-stu-id="1513a-135">The following query will be issued only against the description in Polish:</span></span>

`https://[service name].search.windows.net/indexes/[index name]/docs?search=darmowy&searchFields=description_pl&api-version=2016-09-01`

<span data-ttu-id="1513a-136">Você pode consultar o índice do portal, usando o **Search Explorer** para colar uma consulta semelhante à mostrado acima.</span><span class="sxs-lookup"><span data-stu-id="1513a-136">You can query your index from the portal, using **Search explorer** to paste in a query similar to the one shown above.</span></span> <span data-ttu-id="1513a-137">O Search Explorer está disponível na barra de comandos na folha de serviço.</span><span class="sxs-lookup"><span data-stu-id="1513a-137">Search explorer is available from the command bar in the service blade.</span></span> <span data-ttu-id="1513a-138">Confira [Consultar seu Índice de Pesquisa do Azure no portal](search-explorer.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="1513a-138">See [Query your Azure Search index in the portal](search-explorer.md) for details.</span></span>

<span data-ttu-id="1513a-139">Às vezes, o idioma do agente emissor de uma consulta não é conhecido; nesse caso, a consulta pode ser emitida em todos os campos simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="1513a-139">Sometimes the language of the agent issuing a query is not known, in which case the query can be issued against all fields simultaneously.</span></span> <span data-ttu-id="1513a-140">Se necessário, a preferência de resultados em um determinado idioma pode ser definida usando os [perfis de pontuação](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span><span class="sxs-lookup"><span data-stu-id="1513a-140">If needed, preference for results in a certain language can be defined using [scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span></span> <span data-ttu-id="1513a-141">No exemplo abaixo, as correspondências encontradas na descrição em inglês terão uma pontuação superior em relação às correspondências em polonês e francês:</span><span class="sxs-lookup"><span data-stu-id="1513a-141">In the example below, matches found in the description in English will be scored higher relative to matches in Polish and French:</span></span>

    "scoringProfiles": [
      {
        "name": "englishFirst",
        "text": {
          "weights": { "description_en": 2 }
        }
      }
    ]

`https://[service name].search.windows.net/indexes/[index name]/docs?search=Microsoft&scoringProfile=englishFirst&api-version=2016-09-01`

<span data-ttu-id="1513a-142">Se você é um desenvolvedor do .NET, é importante lembrar que você pode configurar os analisadores de linguagem usando o [SDK do .NET da Pesquisa do Azure](http://www.nuget.org/packages/Microsoft.Azure.Search).</span><span class="sxs-lookup"><span data-stu-id="1513a-142">If you're a .NET developer, note that you can configure language analyzers using the [Azure Search .NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Search).</span></span> <span data-ttu-id="1513a-143">A versão mais recente também inclui o suporte para os analisadores de linguagem da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1513a-143">The latest release includes support for the Microsoft language analyzers as well.</span></span>

<!-- Image References -->
[1]: ./media/search-language-support/AnalyzerTab.png
[2]: ./media/search-language-support/SelectAnalyzer.png
[3]: ./media/search-language-support/IndexDefinition.png
