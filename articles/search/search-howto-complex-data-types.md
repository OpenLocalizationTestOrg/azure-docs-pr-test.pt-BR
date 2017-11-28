---
title: tipos de dados complexos toomodel aaaHow na pesquisa do Azure | Microsoft Docs
description: "As estruturas de dados aninhadas e hierárquicas podem ser modeladas em um índice do Azure Search usando o conjunto de linhas nivelado e o tipo de dados Coleções."
services: search
documentationcenter: 
author: LiamCa
manager: pablocas
editor: 
tags: complex data types; compound data types; aggregate data types
ms.assetid: e4bf86b4-497a-4179-b09f-c1b56c3c0bb2
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: liamca
ms.openlocfilehash: b330c5b322f4f33123a454be11733b977684b9e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomodel-complex-data-types-in-azure-search"></a><span data-ttu-id="dbab0-103">Como os tipos de dados complexos toomodel na pesquisa do Azure</span><span class="sxs-lookup"><span data-stu-id="dbab0-103">How toomodel complex data types in Azure Search</span></span>
<span data-ttu-id="dbab0-104">Conjuntos de dados externos usados toopopulate um índice de pesquisa do Azure, às vezes, incluem subestruturas hierárquicas ou aninhadas que não dividir organizado em um conjunto de linhas da tabela.</span><span class="sxs-lookup"><span data-stu-id="dbab0-104">External datasets used toopopulate an Azure Search index sometimes include hierarchical or nested substructures that do not break down neatly into a tabular rowset.</span></span> <span data-ttu-id="dbab0-105">Os exemplos dessas estruturas podem incluir vários locais e números de telefone para um único cliente, vários tamanhos e cores para um único SKU, vários autores de um único livro e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="dbab0-105">Examples of such structures might include multiple locations and phone numbers for a single customer, multiple colors and sizes for a single SKU, multiple authors of a single book, and so on.</span></span> <span data-ttu-id="dbab0-106">Em termos de modelagem, você pode ver essas estruturas chamado tooas *tipos de dados complexos*, *composta de tipos de dados*, *tipos de dados compostos*, ou *agregação tipos de dados*, tooname alguns.</span><span class="sxs-lookup"><span data-stu-id="dbab0-106">In modeling terms, you might see these structures referred tooas *complex data types*, *compound data types*, *composite data types*, or *aggregate data types*, tooname a few.</span></span>

<span data-ttu-id="dbab0-107">Tipos de dados complexos não são suportados na pesquisa do Azure, mas uma solução alternativa comprovada inclui um processo de duas etapas de estrutura Olá a simplificação e, em seguida, usando um **coleção** estrutura interna do tooreconstitute saudação do tipo de dados.</span><span class="sxs-lookup"><span data-stu-id="dbab0-107">Complex data types are not natively supported in Azure Search, but a proven workaround includes a two-step process of flattening hello structure and then using a **Collection** data type tooreconstitute hello interior structure.</span></span> <span data-ttu-id="dbab0-108">Seguir técnica Olá descrita neste artigo permite toobe conteúdo Olá pesquisada, faceta, filtrados e classificados.</span><span class="sxs-lookup"><span data-stu-id="dbab0-108">Following hello technique described in this article allows hello content toobe searched, faceted, filtered, and sorted.</span></span>

## <a name="example-of-a-complex-data-structure"></a><span data-ttu-id="dbab0-109">Exemplo de uma estrutura de dados complexos</span><span class="sxs-lookup"><span data-stu-id="dbab0-109">Example of a complex data structure</span></span>
<span data-ttu-id="dbab0-110">Normalmente, dados de saudação em questão residem como um conjunto de documentos XML ou JSON, ou como itens em um repositório NoSQL, como o banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="dbab0-110">Typically, hello data in question resides as a set of JSON or XML documents, or as items in a NoSQL store such as Azure Cosmos DB.</span></span> <span data-ttu-id="dbab0-111">Estruturalmente, desafio Olá origina-se de ter vários itens filho que precisam toobe pesquisados e filtrados.</span><span class="sxs-lookup"><span data-stu-id="dbab0-111">Structurally, hello challenge stems from having multiple child items that need toobe searched and filtered.</span></span>  <span data-ttu-id="dbab0-112">Como um ponto de partida para ilustrar a solução alternativa de saudação levar Olá documento JSON que lista um conjunto de contatos como um exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="dbab0-112">As a starting point for illustrating hello workaround, take hello following JSON document that lists a set of contacts as an example:</span></span>

~~~~~
[
  {
    "id": "1",
    "name": "John Smith",
    "company": "Adventureworks",
    "locations": [
      {
        "id": "1",
        "description": "Adventureworks Headquarters"
      },
      {
        "id": "2",
        "description": "Home Office"
      }
    ]
  }, 
  {
    "id": "2",
    "name": "Jen Campbell",
    "company": "Northwind",
    "locations": [
      {
        "id": "3",
        "description": "Northwind Headquarter"
      },
      {
        "id": "4",
        "description": "Home Office"
      }
    ]
}]
~~~~~

<span data-ttu-id="dbab0-113">Enquanto campos Olá chamado 'id', 'name' e 'empresa' podem facilmente ser mapeados individualmente como campos dentro de um índice de pesquisa do Azure, o campo do hello 'local' contém uma matriz de locais, tendo ambos um conjunto de IDs de local, bem como descrições de local.</span><span class="sxs-lookup"><span data-stu-id="dbab0-113">While hello fields named ‘id’, ‘name’ and ‘company’ can easily be mapped one-to-one as fields within an Azure Search index, hello ‘locations’ field contains an array of locations, having both a set of location IDs as well as location descriptions.</span></span> <span data-ttu-id="dbab0-114">Considerando que a pesquisa do Azure não tem um tipo de dados que oferece suporte a isso, é preciso um toomodel de maneira diferente isso na pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="dbab0-114">Given that Azure Search does not have a data type that supports this, we need a different way toomodel this in Azure Search.</span></span> 

> [!NOTE]
> <span data-ttu-id="dbab0-115">Essa técnica também é descrita por Kirk Evans uma postagem de blog [a indexação de documentos com pesquisa do Azure](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), que mostra uma técnica chamada "nivelamento Olá dados", no qual você teria um campo chamado `locationsID` e `locationsDescription` que são ambos [coleções](https://msdn.microsoft.com/library/azure/dn798938.aspx) (ou uma matriz de cadeias de caracteres).</span><span class="sxs-lookup"><span data-stu-id="dbab0-115">This technique is also described by Kirk Evans in a blog post [Indexing DocumentDB with Azure Search](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), which shows a technique called "flattening hello data", whereby you would have a field called `locationsID` and `locationsDescription` that are both [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span></span>   
> 
> 

## <a name="part-1-flatten-hello-array-into-individual-fields"></a><span data-ttu-id="dbab0-116">Parte 1: Mesclar matriz Olá em campos individuais</span><span class="sxs-lookup"><span data-stu-id="dbab0-116">Part 1: Flatten hello array into individual fields</span></span>
<span data-ttu-id="dbab0-117">toocreate um índice de pesquisa do Azure que acomoda a esse conjunto de dados, criar campos individuais para estruturados aninhada Olá: `locationsID` e `locationsDescription` com um tipo de dados de [coleções](https://msdn.microsoft.com/library/azure/dn798938.aspx) (ou uma matriz de cadeias de caracteres).</span><span class="sxs-lookup"><span data-stu-id="dbab0-117">toocreate an Azure Search index that accommodates this dataset, create individual fields for hello nested substructure: `locationsID` and `locationsDescription` with a data type of [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span></span> <span data-ttu-id="dbab0-118">Nesses campos você seria indexar valores hello '1' e '2' hello `locationsID` campo para valores de John Smith e hello '3' & '4' em Olá `locationsID` campo Jen Campbell.</span><span class="sxs-lookup"><span data-stu-id="dbab0-118">In these fields you would index hello values ‘1’ and ‘2’ into hello `locationsID` field for John Smith and hello values ‘3’ & ‘4’ into hello `locationsID` field for Jen Campbell.</span></span>  

<span data-ttu-id="dbab0-119">Os dados no Azure Search ficariam assim:</span><span class="sxs-lookup"><span data-stu-id="dbab0-119">Your data within Azure Search would look like this:</span></span> 

![dados de exemplo, 2 linhas](./media/search-howto-complex-data-types/sample-data.png)

## <a name="part-2-add-a-collection-field-in-hello-index-definition"></a><span data-ttu-id="dbab0-121">Parte 2: Adicionar um campo de conjunto na definição de índice de saudação</span><span class="sxs-lookup"><span data-stu-id="dbab0-121">Part 2: Add a collection field in hello index definition</span></span>
<span data-ttu-id="dbab0-122">No esquema de índice hello, definições de campo Olá podem parecer exemplo toothis semelhante.</span><span class="sxs-lookup"><span data-stu-id="dbab0-122">In hello index schema, hello field definitions might look similar toothis example.</span></span>

~~~~
var index = new Index()
{
    Name = indexName,
    Fields = new[]
    {
        new Field("id", DataType.String) { IsKey = true },
        new Field("name", DataType.String) { IsSearchable = true, IsFilterable = false, IsSortable = false, IsFacetable = false },
        new Field("company", DataType.String) { IsSearchable = true, IsFilterable = false, IsSortable = false, IsFacetable = false },
        new Field("locationsId", DataType.Collection(DataType.String)) { IsSearchable = true, IsFilterable = true, IsFacetable = true },
        new Field("locationsDescription", DataType.Collection(DataType.String)) { IsSearchable = true, IsFilterable = true, IsFacetable = true }
    }
};
~~~~

## <a name="validate-search-behaviors-and-optionally-extend-hello-index"></a><span data-ttu-id="dbab0-123">Validar comportamentos de pesquisa e, opcionalmente, estender índice Olá</span><span class="sxs-lookup"><span data-stu-id="dbab0-123">Validate search behaviors and optionally extend hello index</span></span>
<span data-ttu-id="dbab0-124">Supondo que você índice criado hello e dados carregados de saudação, agora você pode testar execução de consulta de pesquisa Olá solução tooverify no conjunto de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="dbab0-124">Assuming you created hello index and loaded hello data, you can now test hello solution tooverify search query execution against hello dataset.</span></span> <span data-ttu-id="dbab0-125">Cada campo da **coleção** deve ser **pesquisável**, **filtrável** e **lapidável**.</span><span class="sxs-lookup"><span data-stu-id="dbab0-125">Each **collection** field should be **searchable**, **filterable** and **facetable**.</span></span> <span data-ttu-id="dbab0-126">Você deve ser capaz de toorun consultas como:</span><span class="sxs-lookup"><span data-stu-id="dbab0-126">You should be able toorun queries like:</span></span>

* <span data-ttu-id="dbab0-127">Localize todas as pessoas que trabalham na Olá 'Adventureworks Headquarters'.</span><span class="sxs-lookup"><span data-stu-id="dbab0-127">Find all people who work at hello ‘Adventureworks Headquarters’.</span></span>
* <span data-ttu-id="dbab0-128">Obter uma contagem do número de saudação de pessoas que trabalham em um escritório' Início'.</span><span class="sxs-lookup"><span data-stu-id="dbab0-128">Get a count of hello number of people who work in a ‘Home Office’.</span></span>  
* <span data-ttu-id="dbab0-129">Olá que as pessoas que trabalham em um escritório' Início', mostram quais outros escritórios que funcionam junto com uma contagem de pessoas de saudação em cada local.</span><span class="sxs-lookup"><span data-stu-id="dbab0-129">Of hello people who work at a ‘Home Office’, show what other offices they work along with a count of hello people in each location.</span></span>  

<span data-ttu-id="dbab0-130">Onde essa técnica cai distância é quando você precisa toodo uma pesquisa que combina o id de local de saudação, bem como descrição do local de hello.</span><span class="sxs-lookup"><span data-stu-id="dbab0-130">Where this technique falls apart is when you need toodo a search that combines both hello location id as well as hello location description.</span></span> <span data-ttu-id="dbab0-131">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="dbab0-131">For example:</span></span>

* <span data-ttu-id="dbab0-132">Localize todas as pessoas onde elas têm um Escritório Central E uma Identificação de local 4.</span><span class="sxs-lookup"><span data-stu-id="dbab0-132">Find all people where they have a Home Office AND has a location ID of 4.</span></span>  

<span data-ttu-id="dbab0-133">Se você recuperar o conteúdo original hello, semelhante a este:</span><span class="sxs-lookup"><span data-stu-id="dbab0-133">If you recall hello original content looked like this:</span></span>

~~~~
   {
        id: '4',
        description: 'Home Office'
   }
~~~~

<span data-ttu-id="dbab0-134">No entanto, agora que dividimos dados saudação em campos separados, não temos nenhuma maneira de saber se a saudação inicial do Office para Jen Campbell relaciona muito`locationsID 3` ou `locationsID 4`.</span><span class="sxs-lookup"><span data-stu-id="dbab0-134">However, now that we have separated hello data into separate fields, we have no way of knowing if hello Home Office for Jen Campbell relates too`locationsID 3` or `locationsID 4`.</span></span>  

<span data-ttu-id="dbab0-135">toohandle nesse caso, defina outro campo no índice de saudação que combina todos os dados de saudação em uma única coleção.</span><span class="sxs-lookup"><span data-stu-id="dbab0-135">toohandle this case, define another field in hello index that combines all of hello data into a single collection.</span></span>  <span data-ttu-id="dbab0-136">Para nosso exemplo, chamaremos esse campo `locationsCombined` e estamos separará conteúdo Olá com um `||` Embora você possa escolher qualquer separador que você acha que seria um conjunto exclusivo de caracteres para o seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="dbab0-136">For our example, we will call this field `locationsCombined` and we will separate hello content with a `||` although you can choose any separator that you think would be a unique set of characters for your content.</span></span> <span data-ttu-id="dbab0-137">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="dbab0-137">For example:</span></span> 

![dados de exemplo, 2 linhas com separador](./media/search-howto-complex-data-types/sample-data-2.png)

<span data-ttu-id="dbab0-139">Usando esse campo `locationsCombined` , agora podemos aceitar ainda mais consultas, como:</span><span class="sxs-lookup"><span data-stu-id="dbab0-139">Using this `locationsCombined` field, we can now accommodate even more queries, such as:</span></span>

* <span data-ttu-id="dbab0-140">Mostre uma contagem de pessoas que trabalham em um 'Escritório Central' com uma Id de local '4'.</span><span class="sxs-lookup"><span data-stu-id="dbab0-140">Show a count of people who work at a ‘Home Office’ with location Id of ‘4’.</span></span>  
* <span data-ttu-id="dbab0-141">Procure as pessoas que trabalham em um ‘Escritório Central' com uma Id de local '4'.</span><span class="sxs-lookup"><span data-stu-id="dbab0-141">Search for people who work at a ‘Home Office’ with location Id ‘4’.</span></span> 

## <a name="limitations"></a><span data-ttu-id="dbab0-142">Limitações</span><span class="sxs-lookup"><span data-stu-id="dbab0-142">Limitations</span></span>
<span data-ttu-id="dbab0-143">Essa técnica é útil para vários cenários, mas ela não é aplicável em todos os casos.</span><span class="sxs-lookup"><span data-stu-id="dbab0-143">This technique is useful for a number of scenarios, but it is not applicable in every case.</span></span>  <span data-ttu-id="dbab0-144">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="dbab0-144">For example:</span></span>

1. <span data-ttu-id="dbab0-145">Se você não tem um conjunto estático de campos no seu tipo de dados complexos e não havia nenhuma maneira toomap todos os possíveis Olá tipos tooa único campo.</span><span class="sxs-lookup"><span data-stu-id="dbab0-145">If you do not have a static set of fields in your complex data type and there was no way toomap all hello possible types tooa single field.</span></span> 
2. <span data-ttu-id="dbab0-146">Atualizando objetos de saudação aninhado requer toodetermine algum trabalho extra exatamente o que precisa toobe atualizado no índice de pesquisa do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="dbab0-146">Updating hello nested objects requires some extra work toodetermine exactly what needs toobe updated in hello Azure Search index</span></span>

## <a name="sample-code"></a><span data-ttu-id="dbab0-147">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="dbab0-147">Sample code</span></span>
<span data-ttu-id="dbab0-148">Você pode ver um exemplo sobre como tooindex um dados JSON complexos configurado na pesquisa do Azure e executar um número de consultas sobre este conjunto de dados neste [repositório GitHub](https://github.com/liamca/AzureSearchComplexTypes).</span><span class="sxs-lookup"><span data-stu-id="dbab0-148">You can see an example on how tooindex a complex JSON data set into Azure Search and perform a number of queries over this dataset at this [GitHub repo](https://github.com/liamca/AzureSearchComplexTypes).</span></span>

## <a name="next-step"></a><span data-ttu-id="dbab0-149">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="dbab0-149">Next step</span></span>
<span data-ttu-id="dbab0-150">[Voto para o suporte nativo para tipos de dados complexos](https://feedback.azure.com/forums/263029-azure-search) em hello Azure UserVoice de pesquisa de página e fornecer qualquer entrada adicional que você deseja tooconsider sobre implementação de recurso.</span><span class="sxs-lookup"><span data-stu-id="dbab0-150">[Vote for native support for complex data types](https://feedback.azure.com/forums/263029-azure-search) on hello Azure Search UserVoice page and provide any additional input that you’d like us tooconsider regarding feature implementation.</span></span> <span data-ttu-id="dbab0-151">Você também pode alcançar toome diretamente no Twitter em @liamca.</span><span class="sxs-lookup"><span data-stu-id="dbab0-151">You can also reach out toome directly on Twitter at @liamca.</span></span>

