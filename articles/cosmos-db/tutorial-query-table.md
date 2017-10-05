---
title: Como consultar dados de tabela no Azure Cosmos DB? | Microsoft Docs
description: Saiba como consultar dados de tabela no Azure Cosmos DB
services: cosmos-db
documentationcenter: 
author: kanshiG
manager: jhubbard
editor: 
tags: 
ms.assetid: 14bcb94e-583c-46f7-9ea8-db010eb2ab43
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: govindk
ms.openlocfilehash: e59cfa85c6bf584e44bdc6e88cc19d67df390041
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-how-to-query-table-data-by-using-the-table-api-preview"></a><span data-ttu-id="2368c-104">Azure Cosmos DB: Como consultar os dados da tabela utilizando a API de Tabela (versão prévia)?</span><span class="sxs-lookup"><span data-stu-id="2368c-104">Azure Cosmos DB: How to query table data by using the Table API (preview)?</span></span>

<span data-ttu-id="2368c-105">A [API de Tabela](table-introduction.md) (visualização) do Azure Cosmos DB oferece suporte a consultas de OData e [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) em dados de chave/valor (tabela).</span><span class="sxs-lookup"><span data-stu-id="2368c-105">The Azure Cosmos DB [Table API](table-introduction.md) (preview) supports OData and [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) queries against key/value (table) data.</span></span>  

<span data-ttu-id="2368c-106">Este artigo aborda as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="2368c-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="2368c-107">Consultar dados com a API de Tabela</span><span class="sxs-lookup"><span data-stu-id="2368c-107">Querying data with the Table API</span></span>

<span data-ttu-id="2368c-108">As consultas neste artigo usam a seguinte tabela de exemplo `People`:</span><span class="sxs-lookup"><span data-stu-id="2368c-108">The queries in this article use the following sample `People` table:</span></span>

| <span data-ttu-id="2368c-109">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="2368c-109">PartitionKey</span></span> | <span data-ttu-id="2368c-110">RowKey</span><span class="sxs-lookup"><span data-stu-id="2368c-110">RowKey</span></span> | <span data-ttu-id="2368c-111">Email</span><span class="sxs-lookup"><span data-stu-id="2368c-111">Email</span></span> | <span data-ttu-id="2368c-112">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="2368c-112">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2368c-113">Harp</span><span class="sxs-lookup"><span data-stu-id="2368c-113">Harp</span></span> | <span data-ttu-id="2368c-114">Walter</span><span class="sxs-lookup"><span data-stu-id="2368c-114">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="2368c-115">425-555-0101</span><span class="sxs-lookup"><span data-stu-id="2368c-115">425-555-0101</span></span> |
| <span data-ttu-id="2368c-116">Smith</span><span class="sxs-lookup"><span data-stu-id="2368c-116">Smith</span></span> | <span data-ttu-id="2368c-117">Ben</span><span class="sxs-lookup"><span data-stu-id="2368c-117">Ben</span></span> | Ben@contoso.com| <span data-ttu-id="2368c-118">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="2368c-118">425-555-0102</span></span> |
| <span data-ttu-id="2368c-119">Smith</span><span class="sxs-lookup"><span data-stu-id="2368c-119">Smith</span></span> | <span data-ttu-id="2368c-120">Jeff</span><span class="sxs-lookup"><span data-stu-id="2368c-120">Jeff</span></span> | Jeff@contoso.com| <span data-ttu-id="2368c-121">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="2368c-121">425-555-0104</span></span> | 

<span data-ttu-id="2368c-122">Como o Azure Cosmos DB é compatível com as APIs de Armazenamento de Tabelas do Azure, consulte [Consultar tabelas e entidades] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) para obter detalhes sobre como consultar utilizando a API de Tabela.</span><span class="sxs-lookup"><span data-stu-id="2368c-122">Because Azure Cosmos DB is compatible with the Azure Table storage APIs, see [Querying Tables and Entities] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) for details on how to query by using the Table API.</span></span> 

<span data-ttu-id="2368c-123">Para obter mais informações sobre os recursos premium que o Azure Cosmos DB oferece, consulte [Azure Cosmos DB: API de Tabela](table-introduction.md) e [Desenvolver com a API de Tabela em .NET](tutorial-develop-table-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="2368c-123">For more information on the premium capabilities that Azure Cosmos DB offers, see [Azure Cosmos DB: Table API](table-introduction.md) and [Develop with the Table API in .NET](tutorial-develop-table-dotnet.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="2368c-124">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2368c-124">Prerequisites</span></span>

<span data-ttu-id="2368c-125">Para essas consultas funcionarem, você deve ter uma conta do Azure Cosmos DB e ter dados de entidade no contêiner.</span><span class="sxs-lookup"><span data-stu-id="2368c-125">For these queries to work, you must have an Azure Cosmos DB account and have entity data in the container.</span></span> <span data-ttu-id="2368c-126">Não tenho nenhum deles?</span><span class="sxs-lookup"><span data-stu-id="2368c-126">Don't have any of those?</span></span> <span data-ttu-id="2368c-127">Complete o [Guia de início rápido de cinco minutos](https://aka.ms/acdbtnetqs) ou o [tutorial de desenvolvedor](https://aka.ms/acdbtabletut) para criar uma conta e preencher seu banco de dados.</span><span class="sxs-lookup"><span data-stu-id="2368c-127">Complete the [five-minute quickstart](https://aka.ms/acdbtnetqs) or the [developer tutorial](https://aka.ms/acdbtabletut) to create an account and populate your database.</span></span>

## <a name="query-on-partitionkey-and-rowkey"></a><span data-ttu-id="2368c-128">Consultar em PartitionKey e RowKey</span><span class="sxs-lookup"><span data-stu-id="2368c-128">Query on PartitionKey and RowKey</span></span>
<span data-ttu-id="2368c-129">Como as propriedades PartitionKey e RowKey formam a chave primária de uma entidade, é possível utilizar a seguinte sintaxe especial para identificar a entidade:</span><span class="sxs-lookup"><span data-stu-id="2368c-129">Because the PartitionKey and RowKey properties form an entity's primary key, you can use the following special syntax to identify the entity:</span></span> 

<span data-ttu-id="2368c-130">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="2368c-130">**Query**</span></span>

```
https://<mytableendpoint>/People(PartitionKey='Harp',RowKey='Walter')  
```
<span data-ttu-id="2368c-131">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="2368c-131">**Results**</span></span>

| <span data-ttu-id="2368c-132">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="2368c-132">PartitionKey</span></span> | <span data-ttu-id="2368c-133">RowKey</span><span class="sxs-lookup"><span data-stu-id="2368c-133">RowKey</span></span> | <span data-ttu-id="2368c-134">Email</span><span class="sxs-lookup"><span data-stu-id="2368c-134">Email</span></span> | <span data-ttu-id="2368c-135">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="2368c-135">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2368c-136">Harp</span><span class="sxs-lookup"><span data-stu-id="2368c-136">Harp</span></span> | <span data-ttu-id="2368c-137">Walter</span><span class="sxs-lookup"><span data-stu-id="2368c-137">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="2368c-138">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="2368c-138">425-555-0104</span></span> |

<span data-ttu-id="2368c-139">Como alternativa, você pode especificar essas propriedades como parte da opção `$filter`, conforme mostra a seção a seguir.</span><span class="sxs-lookup"><span data-stu-id="2368c-139">Alternatively, you can specify these properties as part of the `$filter` option, as shown in the following section.</span></span> <span data-ttu-id="2368c-140">Observe que os nomes de propriedade de chave e valores constantes diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="2368c-140">Note that the key property names and constant values are case-sensitive.</span></span> <span data-ttu-id="2368c-141">As propriedades PartitionKey e RowKey são do tipo Cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="2368c-141">Both the PartitionKey and RowKey properties are of type String.</span></span> 

## <a name="query-by-using-an-odata-filter"></a><span data-ttu-id="2368c-142">Consultar utilizando um filtro OData</span><span class="sxs-lookup"><span data-stu-id="2368c-142">Query by using an OData filter</span></span>
<span data-ttu-id="2368c-143">Ao construir uma cadeia de caracteres de filtro, lembre-se destas regras:</span><span class="sxs-lookup"><span data-stu-id="2368c-143">When you're constructing a filter string, keep these rules in mind:</span></span> 

* <span data-ttu-id="2368c-144">Use os operadores lógicos definidos pela Especificação do Protocolo OData para comparar uma propriedade a um valor.</span><span class="sxs-lookup"><span data-stu-id="2368c-144">Use the logical operators defined by the OData Protocol Specification to compare a property to a value.</span></span> <span data-ttu-id="2368c-145">Observe que você não pode comparar uma propriedade com um valor dinâmico.</span><span class="sxs-lookup"><span data-stu-id="2368c-145">Note that you can't compare a property to a dynamic value.</span></span> <span data-ttu-id="2368c-146">Um lado da expressão deve ser uma constante.</span><span class="sxs-lookup"><span data-stu-id="2368c-146">One side of the expression must be a constant.</span></span> 
* <span data-ttu-id="2368c-147">O nome da propriedade, o operador e um valor constante devem ser separados por espaços codificados por URL.</span><span class="sxs-lookup"><span data-stu-id="2368c-147">The property name, operator, and constant value must be separated by URL-encoded spaces.</span></span> <span data-ttu-id="2368c-148">Um espaço é codificado por URL como `%20`.</span><span class="sxs-lookup"><span data-stu-id="2368c-148">A space is URL-encoded as `%20`.</span></span> 
* <span data-ttu-id="2368c-149">Todas as partes da cadeia de caracteres de filtro diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="2368c-149">All parts of the filter string are case-sensitive.</span></span> 
* <span data-ttu-id="2368c-150">O valor da constante deve ser do mesmo tipo de dados como a propriedade para que o filtro retorne resultados válidos.</span><span class="sxs-lookup"><span data-stu-id="2368c-150">The constant value must be of the same data type as the property in order for the filter to return valid results.</span></span> <span data-ttu-id="2368c-151">Para obter informações sobre tipos de propriedades com suporte, consulte [Noções básicas sobre o modelo de dados do serviço Tabela](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model).</span><span class="sxs-lookup"><span data-stu-id="2368c-151">For more information about supported property types, see [Understanding the Table Service Data Model](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model).</span></span> 

<span data-ttu-id="2368c-152">Veja um exemplo de consulta que mostra como filtrar por PartitionKey e as propriedades de Email usando um OData `$filter`.</span><span class="sxs-lookup"><span data-stu-id="2368c-152">Here's an example query that shows how to filter by the PartitionKey and Email properties by using an OData `$filter`.</span></span>

<span data-ttu-id="2368c-153">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="2368c-153">**Query**</span></span>

```
https://<mytableapi-endpoint>/People()?$filter=PartitionKey%20eq%20'Smith'%20and%20Email%20eq%20'Ben@contoso.com'
```

<span data-ttu-id="2368c-154">Para obter mais informações sobre como construir expressões de filtro para vários tipos de dados, consulte [Consultar tabelas e entidades](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).</span><span class="sxs-lookup"><span data-stu-id="2368c-154">For more information on how to construct filter expressions for various data types, see [Querying Tables and Entities](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).</span></span>

<span data-ttu-id="2368c-155">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="2368c-155">**Results**</span></span>

| <span data-ttu-id="2368c-156">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="2368c-156">PartitionKey</span></span> | <span data-ttu-id="2368c-157">RowKey</span><span class="sxs-lookup"><span data-stu-id="2368c-157">RowKey</span></span> | <span data-ttu-id="2368c-158">Email</span><span class="sxs-lookup"><span data-stu-id="2368c-158">Email</span></span> | <span data-ttu-id="2368c-159">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="2368c-159">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2368c-160">Ben</span><span class="sxs-lookup"><span data-stu-id="2368c-160">Ben</span></span> |<span data-ttu-id="2368c-161">Smith</span><span class="sxs-lookup"><span data-stu-id="2368c-161">Smith</span></span> | Ben@contoso.com| <span data-ttu-id="2368c-162">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="2368c-162">425-555-0102</span></span> |

## <a name="query-by-using-linq"></a><span data-ttu-id="2368c-163">Consultar utilizando LINQ</span><span class="sxs-lookup"><span data-stu-id="2368c-163">Query by using LINQ</span></span> 
<span data-ttu-id="2368c-164">Você também pode consultar utilizando o LINQ, o que resulta em expressões de consulta Odata correspondentes.</span><span class="sxs-lookup"><span data-stu-id="2368c-164">You can also query by using LINQ, which translates to the corresponding OData query expressions.</span></span> <span data-ttu-id="2368c-165">Veja um exemplo de como criar consultas usando o SDK do .NET.:</span><span class="sxs-lookup"><span data-stu-id="2368c-165">Here's an example of how to build queries by using the .NET SDK:</span></span>

```csharp
CloudTableClient tableClient = account.CreateCloudTableClient();
CloudTable table = tableClient.GetTableReference("people");

TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>()
    .Where(
        TableQuery.CombineFilters(
            TableQuery.GenerateFilterCondition(PartitionKey, QueryComparisons.Equal, "Smith"),
            TableOperators.And,
            TableQuery.GenerateFilterCondition(Email, QueryComparisons.Equal,"Ben@contoso.com")
    ));

await table.ExecuteQuerySegmentedAsync<CustomerEntity>(query, null);
```

## <a name="next-steps"></a><span data-ttu-id="2368c-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2368c-166">Next steps</span></span>

<span data-ttu-id="2368c-167">Neste tutorial, você fez o seguinte:</span><span class="sxs-lookup"><span data-stu-id="2368c-167">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2368c-168">Aprendeu a consultar utilizando a API de Tabela (versão prévia)</span><span class="sxs-lookup"><span data-stu-id="2368c-168">Learned how to query by using the Table API (preview)</span></span> 

<span data-ttu-id="2368c-169">Agora você pode prosseguir para o próximo tutorial e aprender a distribuir seus dados globalmente.</span><span class="sxs-lookup"><span data-stu-id="2368c-169">You can now proceed to the next tutorial to learn how to distribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2368c-170">Distribuir os dados globalmente</span><span class="sxs-lookup"><span data-stu-id="2368c-170">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)
