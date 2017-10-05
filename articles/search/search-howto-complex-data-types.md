---
title: Como modelar os tipos de dados complexos no Azure Search | Microsoft Docs
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
ms.openlocfilehash: d576fd7bb267ae7a100589413185b595e3b2be42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-model-complex-data-types-in-azure-search"></a><span data-ttu-id="9a3d2-103">Como modelar os tipos de dados complexos no Azure Search</span><span class="sxs-lookup"><span data-stu-id="9a3d2-103">How to model complex data types in Azure Search</span></span>
<span data-ttu-id="9a3d2-104">Os conjuntos de dados externos usados para preencher um índice do Azure Search, às vezes, incluem subestruturas hierárquicas ou aninhadas que não se dividem de modo organizado em um conjunto de linhas da tabela.</span><span class="sxs-lookup"><span data-stu-id="9a3d2-104">External datasets used to populate an Azure Search index sometimes include hierarchical or nested substructures that do not break down neatly into a tabular rowset.</span></span> <span data-ttu-id="9a3d2-105">Os exemplos dessas estruturas podem incluir vários locais e números de telefone para um único cliente, vários tamanhos e cores para um único SKU, vários autores de um único livro e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="9a3d2-105">Examples of such structures might include multiple locations and phone numbers for a single customer, multiple colors and sizes for a single SKU, multiple authors of a single book, and so on.</span></span> <span data-ttu-id="9a3d2-106">Em termos de modelagem, você pode ver essas estruturas referidas como *tipos de dados complexos*, *tipos de dados compostos*, *tipos de dados combinados* ou *tipos de dados de agregação*, para citar alguns.</span><span class="sxs-lookup"><span data-stu-id="9a3d2-106">In modeling terms, you might see these structures referred to as *complex data types*, *compound data types*, *composite data types*, or *aggregate data types*, to name a few.</span></span>

<span data-ttu-id="9a3d2-107">Os tipos de dados complexos não são suportados nativamente no Azure Search, mas uma solução comprovada inclui um processo de duas etapas de nivelamento da estrutura e uso de um tipo de dados **Coleção** para reconstituir a estrutura interna.</span><span class="sxs-lookup"><span data-stu-id="9a3d2-107">Complex data types are not natively supported in Azure Search, but a proven workaround includes a two-step process of flattening the structure and then using a **Collection** data type to reconstitute the interior structure.</span></span> <span data-ttu-id="9a3d2-108">Seguir a técnica descrita neste artigo permite que o conteúdo seja pesquisado, lapidado, filtrado e classificado.</span><span class="sxs-lookup"><span data-stu-id="9a3d2-108">Following the technique described in this article allows the content to be searched, faceted, filtered, and sorted.</span></span>

## <a name="example-of-a-complex-data-structure"></a><span data-ttu-id="9a3d2-109">Exemplo de uma estrutura de dados complexos</span><span class="sxs-lookup"><span data-stu-id="9a3d2-109">Example of a complex data structure</span></span>
<span data-ttu-id="9a3d2-110">Normalmente, os dados em questão residem como um conjunto de documentos JSON ou XML, ou como itens em um repositório NoSQL, como o Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9a3d2-110">Typically, the data in question resides as a set of JSON or XML documents, or as items in a NoSQL store such as Azure Cosmos DB.</span></span> <span data-ttu-id="9a3d2-111">Estruturalmente, o desafio é ter vários itens-filho que precisam ser pesquisados e filtrados.</span><span class="sxs-lookup"><span data-stu-id="9a3d2-111">Structurally, the challenge stems from having multiple child items that need to be searched and filtered.</span></span>  <span data-ttu-id="9a3d2-112">Como ponto de partida para ilustrar a solução alternativa, veja o seguinte documento JSON que lista um conjunto de contatos como um exemplo:</span><span class="sxs-lookup"><span data-stu-id="9a3d2-112">As a starting point for illustrating the workaround, take the following JSON document that lists a set of contacts as an example:</span></span>

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

<span data-ttu-id="9a3d2-113">Embora os campos denominados 'id', 'name' e 'empresa' possam ser mapeados facilmente um a um como campos em um índice do Azure Search, o campo 'locais' contém uma matriz de locais, com um conjunto de IDs de local, bem como descrições do local.</span><span class="sxs-lookup"><span data-stu-id="9a3d2-113">While the fields named ‘id’, ‘name’ and ‘company’ can easily be mapped one-to-one as fields within an Azure Search index, the ‘locations’ field contains an array of locations, having both a set of location IDs as well as location descriptions.</span></span> <span data-ttu-id="9a3d2-114">Considerando que o Azure Search não tem um tipo de dados que oferece suporte, precisamos de uma maneira diferente de modelar isso no Azure Search.</span><span class="sxs-lookup"><span data-stu-id="9a3d2-114">Given that Azure Search does not have a data type that supports this, we need a different way to model this in Azure Search.</span></span> 

> [!NOTE]
> <span data-ttu-id="9a3d2-115">Essa técnica também é descrita por Kirk Evans em uma postagem de blog [Indexando o DocumentDB com o Azure Search](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), que mostra uma técnica denominada "nivelar os dados", por meio da qual você teria os campos chamados `locationsID` e `locationsDescription` que são [coleções](https://msdn.microsoft.com/library/azure/dn798938.aspx) (ou uma matriz de cadeias de caracteres).</span><span class="sxs-lookup"><span data-stu-id="9a3d2-115">This technique is also described by Kirk Evans in a blog post [Indexing DocumentDB with Azure Search](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), which shows a technique called "flattening the data", whereby you would have a field called `locationsID` and `locationsDescription` that are both [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span></span>   
> 
> 

## <a name="part-1-flatten-the-array-into-individual-fields"></a><span data-ttu-id="9a3d2-116">Parte 1: Nivelar a matriz em campos individuais</span><span class="sxs-lookup"><span data-stu-id="9a3d2-116">Part 1: Flatten the array into individual fields</span></span>
<span data-ttu-id="9a3d2-117">Para criar um índice do Azure Search que aceita esse conjunto de dados, crie campos individuais para a subestrutura aninhada: `locationsID` e `locationsDescription` com um tipo de dados de [coleções](https://msdn.microsoft.com/library/azure/dn798938.aspx) (ou uma matriz de cadeias de caracteres).</span><span class="sxs-lookup"><span data-stu-id="9a3d2-117">To create an Azure Search index that accommodates this dataset, create individual fields for the nested substructure: `locationsID` and `locationsDescription` with a data type of [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span></span> <span data-ttu-id="9a3d2-118">Nesses campos, você deve indexar os valores '1' e '2' no campo `locationsID` para John Smith e os valores '3' e '4' no campo `locationsID` para Jen Campbell.</span><span class="sxs-lookup"><span data-stu-id="9a3d2-118">In these fields you would index the values ‘1’ and ‘2’ into the `locationsID` field for John Smith and the values ‘3’ & ‘4’ into the `locationsID` field for Jen Campbell.</span></span>  

<span data-ttu-id="9a3d2-119">Os dados no Azure Search ficariam assim:</span><span class="sxs-lookup"><span data-stu-id="9a3d2-119">Your data within Azure Search would look like this:</span></span> 

![dados de exemplo, 2 linhas](./media/search-howto-complex-data-types/sample-data.png)

## <a name="part-2-add-a-collection-field-in-the-index-definition"></a><span data-ttu-id="9a3d2-121">Parte 2: Adicionar um campo de coleção na definição do índice</span><span class="sxs-lookup"><span data-stu-id="9a3d2-121">Part 2: Add a collection field in the index definition</span></span>
<span data-ttu-id="9a3d2-122">No esquema do índice, as definições do campo podem ser semelhantes a este exemplo.</span><span class="sxs-lookup"><span data-stu-id="9a3d2-122">In the index schema, the field definitions might look similar to this example.</span></span>

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

## <a name="validate-search-behaviors-and-optionally-extend-the-index"></a><span data-ttu-id="9a3d2-123">Validar os comportamentos da pesquisa e, opcionalmente, estender o índice</span><span class="sxs-lookup"><span data-stu-id="9a3d2-123">Validate search behaviors and optionally extend the index</span></span>
<span data-ttu-id="9a3d2-124">Supondo que você criou o índice e carregou os dados, agora você pode testar a solução para verificar a execução da consulta de pesquisa no conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="9a3d2-124">Assuming you created the index and loaded the data, you can now test the solution to verify search query execution against the dataset.</span></span> <span data-ttu-id="9a3d2-125">Cada campo da **coleção** deve ser **pesquisável**, **filtrável** e **lapidável**.</span><span class="sxs-lookup"><span data-stu-id="9a3d2-125">Each **collection** field should be **searchable**, **filterable** and **facetable**.</span></span> <span data-ttu-id="9a3d2-126">Você deve ser capaz de executar consultas como:</span><span class="sxs-lookup"><span data-stu-id="9a3d2-126">You should be able to run queries like:</span></span>

* <span data-ttu-id="9a3d2-127">Localize todas as pessoas que trabalham na 'Matriz Adventureworks'.</span><span class="sxs-lookup"><span data-stu-id="9a3d2-127">Find all people who work at the ‘Adventureworks Headquarters’.</span></span>
* <span data-ttu-id="9a3d2-128">Obtenha uma contagem do número de pessoas que trabalham em um ‘Escritório Central’.</span><span class="sxs-lookup"><span data-stu-id="9a3d2-128">Get a count of the number of people who work in a ‘Home Office’.</span></span>  
* <span data-ttu-id="9a3d2-129">Das pessoas que trabalham em um ‘Escritório Central', mostre em quais outros escritórios elas trabalham, junto com uma contagem de pessoas em cada local.</span><span class="sxs-lookup"><span data-stu-id="9a3d2-129">Of the people who work at a ‘Home Office’, show what other offices they work along with a count of the people in each location.</span></span>  

<span data-ttu-id="9a3d2-130">Onde essa técnica falha é quando você precisa fazer uma pesquisa que combina a identificação do local, bem como a descrição do local.</span><span class="sxs-lookup"><span data-stu-id="9a3d2-130">Where this technique falls apart is when you need to do a search that combines both the location id as well as the location description.</span></span> <span data-ttu-id="9a3d2-131">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9a3d2-131">For example:</span></span>

* <span data-ttu-id="9a3d2-132">Localize todas as pessoas onde elas têm um Escritório Central E uma Identificação de local 4.</span><span class="sxs-lookup"><span data-stu-id="9a3d2-132">Find all people where they have a Home Office AND has a location ID of 4.</span></span>  

<span data-ttu-id="9a3d2-133">Se você se lembra, o conteúdo original era assim:</span><span class="sxs-lookup"><span data-stu-id="9a3d2-133">If you recall the original content looked like this:</span></span>

~~~~
   {
        id: '4',
        description: 'Home Office'
   }
~~~~

<span data-ttu-id="9a3d2-134">No entanto, agora que dividimos os dados em campos separados, não temos nenhuma maneira de saber se o Escritório Central para Jen Campbell relaciona-se a `locationsID 3` ou `locationsID 4`.</span><span class="sxs-lookup"><span data-stu-id="9a3d2-134">However, now that we have separated the data into separate fields, we have no way of knowing if the Home Office for Jen Campbell relates to `locationsID 3` or `locationsID 4`.</span></span>  

<span data-ttu-id="9a3d2-135">Para lidar com isso, defina outro campo no índice que combina todos os dados em uma única coleção.</span><span class="sxs-lookup"><span data-stu-id="9a3d2-135">To handle this case, define another field in the index that combines all of the data into a single collection.</span></span>  <span data-ttu-id="9a3d2-136">Para nosso exemplo, chamaremos esse campo de `locationsCombined` e iremos separar o conteúdo com `||`, embora seja possível escolher qualquer separador que você acha que seria um conjunto exclusivo de caracteres para seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="9a3d2-136">For our example, we will call this field `locationsCombined` and we will separate the content with a `||` although you can choose any separator that you think would be a unique set of characters for your content.</span></span> <span data-ttu-id="9a3d2-137">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9a3d2-137">For example:</span></span> 

![dados de exemplo, 2 linhas com separador](./media/search-howto-complex-data-types/sample-data-2.png)

<span data-ttu-id="9a3d2-139">Usando esse campo `locationsCombined` , agora podemos aceitar ainda mais consultas, como:</span><span class="sxs-lookup"><span data-stu-id="9a3d2-139">Using this `locationsCombined` field, we can now accommodate even more queries, such as:</span></span>

* <span data-ttu-id="9a3d2-140">Mostre uma contagem de pessoas que trabalham em um 'Escritório Central' com uma Id de local '4'.</span><span class="sxs-lookup"><span data-stu-id="9a3d2-140">Show a count of people who work at a ‘Home Office’ with location Id of ‘4’.</span></span>  
* <span data-ttu-id="9a3d2-141">Procure as pessoas que trabalham em um ‘Escritório Central' com uma Id de local '4'.</span><span class="sxs-lookup"><span data-stu-id="9a3d2-141">Search for people who work at a ‘Home Office’ with location Id ‘4’.</span></span> 

## <a name="limitations"></a><span data-ttu-id="9a3d2-142">Limitações</span><span class="sxs-lookup"><span data-stu-id="9a3d2-142">Limitations</span></span>
<span data-ttu-id="9a3d2-143">Essa técnica é útil para vários cenários, mas ela não é aplicável em todos os casos.</span><span class="sxs-lookup"><span data-stu-id="9a3d2-143">This technique is useful for a number of scenarios, but it is not applicable in every case.</span></span>  <span data-ttu-id="9a3d2-144">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9a3d2-144">For example:</span></span>

1. <span data-ttu-id="9a3d2-145">Se você não tem um conjunto estático de campos em seu tipo de dados complexos e não foi possível mapear todos os tipos possíveis para um único campo.</span><span class="sxs-lookup"><span data-stu-id="9a3d2-145">If you do not have a static set of fields in your complex data type and there was no way to map all the possible types to a single field.</span></span> 
2. <span data-ttu-id="9a3d2-146">Atualizar os objetos aninhados requer um trabalho extra para determinar exatamente o que precisa ser atualizado no índice do Azure Search</span><span class="sxs-lookup"><span data-stu-id="9a3d2-146">Updating the nested objects requires some extra work to determine exactly what needs to be updated in the Azure Search index</span></span>

## <a name="sample-code"></a><span data-ttu-id="9a3d2-147">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="9a3d2-147">Sample code</span></span>
<span data-ttu-id="9a3d2-148">Você pode ver um exemplo sobre como indexar um conjunto de dados JSON complexo no Azure Search e executar várias consultas nesse conjunto de dados no [repositório GitHub](https://github.com/liamca/AzureSearchComplexTypes).</span><span class="sxs-lookup"><span data-stu-id="9a3d2-148">You can see an example on how to index a complex JSON data set into Azure Search and perform a number of queries over this dataset at this [GitHub repo](https://github.com/liamca/AzureSearchComplexTypes).</span></span>

## <a name="next-step"></a><span data-ttu-id="9a3d2-149">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="9a3d2-149">Next step</span></span>
<span data-ttu-id="9a3d2-150">[Escolha o suporte nativo para os tipos de dados complexos](https://feedback.azure.com/forums/263029-azure-search) na página UserVoice do Azure Search e forneça qualquer entrada adicional que você gostaria de considerar em relação à implementação do recurso.</span><span class="sxs-lookup"><span data-stu-id="9a3d2-150">[Vote for native support for complex data types](https://feedback.azure.com/forums/263029-azure-search) on the Azure Search UserVoice page and provide any additional input that you’d like us to consider regarding feature implementation.</span></span> <span data-ttu-id="9a3d2-151">Você também pode me contatar diretamente no Twitter em @liamca.</span><span class="sxs-lookup"><span data-stu-id="9a3d2-151">You can also reach out to me directly on Twitter at @liamca.</span></span>

