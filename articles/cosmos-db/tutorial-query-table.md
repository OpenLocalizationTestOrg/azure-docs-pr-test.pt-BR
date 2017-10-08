---
title: aaaHow tooquery dados da tabela no banco de dados do Azure Cosmos? | Microsoft Docs
description: Saiba tooquery dados da tabela no banco de dados do Azure Cosmos
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
ms.openlocfilehash: 32526c3488c589c5be3a4a2f174aa769570f0c0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-table-data-by-using-hello-table-api-preview"></a><span data-ttu-id="68ba9-104">Cosmos do Azure DB: Como dados de tabela tooquery usando Olá API de tabela (visualização)?</span><span class="sxs-lookup"><span data-stu-id="68ba9-104">Azure Cosmos DB: How tooquery table data by using hello Table API (preview)?</span></span>

<span data-ttu-id="68ba9-105">Olá banco de dados do Azure Cosmos [API tabela](table-introduction.md) (visualização) oferece suporte a OData e [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) consultas em dados de chave/valor (tabela).</span><span class="sxs-lookup"><span data-stu-id="68ba9-105">hello Azure Cosmos DB [Table API](table-introduction.md) (preview) supports OData and [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) queries against key/value (table) data.</span></span>  

<span data-ttu-id="68ba9-106">Este artigo aborda Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="68ba9-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="68ba9-107">Consultando dados com hello API de tabela</span><span class="sxs-lookup"><span data-stu-id="68ba9-107">Querying data with hello Table API</span></span>

<span data-ttu-id="68ba9-108">as consultas neste artigo Hello usam Olá exemplo a seguir `People` tabela:</span><span class="sxs-lookup"><span data-stu-id="68ba9-108">hello queries in this article use hello following sample `People` table:</span></span>

| <span data-ttu-id="68ba9-109">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="68ba9-109">PartitionKey</span></span> | <span data-ttu-id="68ba9-110">RowKey</span><span class="sxs-lookup"><span data-stu-id="68ba9-110">RowKey</span></span> | <span data-ttu-id="68ba9-111">Email</span><span class="sxs-lookup"><span data-stu-id="68ba9-111">Email</span></span> | <span data-ttu-id="68ba9-112">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="68ba9-112">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="68ba9-113">Harp</span><span class="sxs-lookup"><span data-stu-id="68ba9-113">Harp</span></span> | <span data-ttu-id="68ba9-114">Walter</span><span class="sxs-lookup"><span data-stu-id="68ba9-114">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="68ba9-115">425-555-0101</span><span class="sxs-lookup"><span data-stu-id="68ba9-115">425-555-0101</span></span> |
| <span data-ttu-id="68ba9-116">Smith</span><span class="sxs-lookup"><span data-stu-id="68ba9-116">Smith</span></span> | <span data-ttu-id="68ba9-117">Ben</span><span class="sxs-lookup"><span data-stu-id="68ba9-117">Ben</span></span> | Ben@contoso.com| <span data-ttu-id="68ba9-118">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="68ba9-118">425-555-0102</span></span> |
| <span data-ttu-id="68ba9-119">Smith</span><span class="sxs-lookup"><span data-stu-id="68ba9-119">Smith</span></span> | <span data-ttu-id="68ba9-120">Jeff</span><span class="sxs-lookup"><span data-stu-id="68ba9-120">Jeff</span></span> | Jeff@contoso.com| <span data-ttu-id="68ba9-121">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="68ba9-121">425-555-0104</span></span> | 

<span data-ttu-id="68ba9-122">Porque o banco de dados do Azure Cosmos é compatível com hello APIs de armazenamento de tabela do Azure, consulte [consultando tabelas e entidades] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) para obter detalhes sobre como tooquery usando Olá Tabela de API.</span><span class="sxs-lookup"><span data-stu-id="68ba9-122">Because Azure Cosmos DB is compatible with hello Azure Table storage APIs, see [Querying Tables and Entities] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) for details on how tooquery by using hello Table API.</span></span> 

<span data-ttu-id="68ba9-123">Para obter mais informações sobre recursos premium Olá que o banco de dados do Azure Cosmos oferece, consulte [o banco de dados do Azure Cosmos: API de tabela](table-introduction.md) e [desenvolver com hello API de tabela no .NET](tutorial-develop-table-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="68ba9-123">For more information on hello premium capabilities that Azure Cosmos DB offers, see [Azure Cosmos DB: Table API](table-introduction.md) and [Develop with hello Table API in .NET](tutorial-develop-table-dotnet.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="68ba9-124">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="68ba9-124">Prerequisites</span></span>

<span data-ttu-id="68ba9-125">Para toowork essas consultas, você deve ter uma conta de banco de dados do Azure Cosmos e ter dados de entidade no contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="68ba9-125">For these queries toowork, you must have an Azure Cosmos DB account and have entity data in hello container.</span></span> <span data-ttu-id="68ba9-126">Não tenho nenhum deles?</span><span class="sxs-lookup"><span data-stu-id="68ba9-126">Don't have any of those?</span></span> <span data-ttu-id="68ba9-127">Olá completa [início rápido de cinco minutos](https://aka.ms/acdbtnetqs) ou hello [tutorial de desenvolvedor](https://aka.ms/acdbtabletut) toocreate uma conta e preencher o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="68ba9-127">Complete hello [five-minute quickstart](https://aka.ms/acdbtnetqs) or hello [developer tutorial](https://aka.ms/acdbtabletut) toocreate an account and populate your database.</span></span>

## <a name="query-on-partitionkey-and-rowkey"></a><span data-ttu-id="68ba9-128">Consultar em PartitionKey e RowKey</span><span class="sxs-lookup"><span data-stu-id="68ba9-128">Query on PartitionKey and RowKey</span></span>
<span data-ttu-id="68ba9-129">Como as propriedades PartitionKey e RowKey Olá constituem a chave primária da entidade, você pode usar Olá entidade de saudação tooidentify sintaxe especial a seguir:</span><span class="sxs-lookup"><span data-stu-id="68ba9-129">Because hello PartitionKey and RowKey properties form an entity's primary key, you can use hello following special syntax tooidentify hello entity:</span></span> 

<span data-ttu-id="68ba9-130">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="68ba9-130">**Query**</span></span>

```
https://<mytableendpoint>/People(PartitionKey='Harp',RowKey='Walter')  
```
<span data-ttu-id="68ba9-131">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="68ba9-131">**Results**</span></span>

| <span data-ttu-id="68ba9-132">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="68ba9-132">PartitionKey</span></span> | <span data-ttu-id="68ba9-133">RowKey</span><span class="sxs-lookup"><span data-stu-id="68ba9-133">RowKey</span></span> | <span data-ttu-id="68ba9-134">Email</span><span class="sxs-lookup"><span data-stu-id="68ba9-134">Email</span></span> | <span data-ttu-id="68ba9-135">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="68ba9-135">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="68ba9-136">Harp</span><span class="sxs-lookup"><span data-stu-id="68ba9-136">Harp</span></span> | <span data-ttu-id="68ba9-137">Walter</span><span class="sxs-lookup"><span data-stu-id="68ba9-137">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="68ba9-138">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="68ba9-138">425-555-0104</span></span> |

<span data-ttu-id="68ba9-139">Como alternativa, você pode especificar essas propriedades como parte da saudação `$filter` opção, conforme mostrado no hello seção a seguir.</span><span class="sxs-lookup"><span data-stu-id="68ba9-139">Alternatively, you can specify these properties as part of hello `$filter` option, as shown in hello following section.</span></span> <span data-ttu-id="68ba9-140">Observe que os nomes de propriedade de chave hello e valores constantes diferenciam maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="68ba9-140">Note that hello key property names and constant values are case-sensitive.</span></span> <span data-ttu-id="68ba9-141">Olá PartitionKey e RowKey propriedades são do tipo cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="68ba9-141">Both hello PartitionKey and RowKey properties are of type String.</span></span> 

## <a name="query-by-using-an-odata-filter"></a><span data-ttu-id="68ba9-142">Consultar utilizando um filtro OData</span><span class="sxs-lookup"><span data-stu-id="68ba9-142">Query by using an OData filter</span></span>
<span data-ttu-id="68ba9-143">Ao construir uma cadeia de caracteres de filtro, lembre-se destas regras:</span><span class="sxs-lookup"><span data-stu-id="68ba9-143">When you're constructing a filter string, keep these rules in mind:</span></span> 

* <span data-ttu-id="68ba9-144">Use operadores lógicos de saudação definidos pela Olá especificação do protocolo OData toocompare um valor da propriedade tooa.</span><span class="sxs-lookup"><span data-stu-id="68ba9-144">Use hello logical operators defined by hello OData Protocol Specification toocompare a property tooa value.</span></span> <span data-ttu-id="68ba9-145">Observe que você não pode comparar um valor da propriedade tooa dinâmico.</span><span class="sxs-lookup"><span data-stu-id="68ba9-145">Note that you can't compare a property tooa dynamic value.</span></span> <span data-ttu-id="68ba9-146">Um lado da expressão Olá deve ser uma constante.</span><span class="sxs-lookup"><span data-stu-id="68ba9-146">One side of hello expression must be a constant.</span></span> 
* <span data-ttu-id="68ba9-147">nome da propriedade Hello, o operador e o valor constante devem ser separados por espaços codificados de URL.</span><span class="sxs-lookup"><span data-stu-id="68ba9-147">hello property name, operator, and constant value must be separated by URL-encoded spaces.</span></span> <span data-ttu-id="68ba9-148">Um espaço é codificado por URL como `%20`.</span><span class="sxs-lookup"><span data-stu-id="68ba9-148">A space is URL-encoded as `%20`.</span></span> 
* <span data-ttu-id="68ba9-149">Todas as partes da cadeia de caracteres de filtro Olá diferenciam maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="68ba9-149">All parts of hello filter string are case-sensitive.</span></span> 
* <span data-ttu-id="68ba9-150">valor constante Olá deve ser de saudação mesmo tipo que propriedade Olá para que os resultados Olá filtro tooreturn válidos.</span><span class="sxs-lookup"><span data-stu-id="68ba9-150">hello constant value must be of hello same data type as hello property in order for hello filter tooreturn valid results.</span></span> <span data-ttu-id="68ba9-151">Para obter mais informações sobre os tipos de propriedade com suporte, consulte [Olá Noções básicas sobre modelo de dados do serviço de tabela](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model).</span><span class="sxs-lookup"><span data-stu-id="68ba9-151">For more information about supported property types, see [Understanding hello Table Service Data Model](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model).</span></span> 

<span data-ttu-id="68ba9-152">Aqui está uma consulta de exemplo que mostra como toofilter por Olá PartitionKey e propriedades de Email usando um OData `$filter`.</span><span class="sxs-lookup"><span data-stu-id="68ba9-152">Here's an example query that shows how toofilter by hello PartitionKey and Email properties by using an OData `$filter`.</span></span>

<span data-ttu-id="68ba9-153">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="68ba9-153">**Query**</span></span>

```
https://<mytableapi-endpoint>/People()?$filter=PartitionKey%20eq%20'Smith'%20and%20Email%20eq%20'Ben@contoso.com'
```

<span data-ttu-id="68ba9-154">Para obter mais informações sobre como tooconstruct filtrar expressões para vários tipos de dados, consulte [consultar tabelas e entidades](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).</span><span class="sxs-lookup"><span data-stu-id="68ba9-154">For more information on how tooconstruct filter expressions for various data types, see [Querying Tables and Entities](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).</span></span>

<span data-ttu-id="68ba9-155">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="68ba9-155">**Results**</span></span>

| <span data-ttu-id="68ba9-156">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="68ba9-156">PartitionKey</span></span> | <span data-ttu-id="68ba9-157">RowKey</span><span class="sxs-lookup"><span data-stu-id="68ba9-157">RowKey</span></span> | <span data-ttu-id="68ba9-158">Email</span><span class="sxs-lookup"><span data-stu-id="68ba9-158">Email</span></span> | <span data-ttu-id="68ba9-159">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="68ba9-159">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="68ba9-160">Ben</span><span class="sxs-lookup"><span data-stu-id="68ba9-160">Ben</span></span> |<span data-ttu-id="68ba9-161">Smith</span><span class="sxs-lookup"><span data-stu-id="68ba9-161">Smith</span></span> | Ben@contoso.com| <span data-ttu-id="68ba9-162">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="68ba9-162">425-555-0102</span></span> |

## <a name="query-by-using-linq"></a><span data-ttu-id="68ba9-163">Consultar utilizando LINQ</span><span class="sxs-lookup"><span data-stu-id="68ba9-163">Query by using LINQ</span></span> 
<span data-ttu-id="68ba9-164">Você também pode consultar usando LINQ, que converte as expressões de consulta OData de toohello correspondentes.</span><span class="sxs-lookup"><span data-stu-id="68ba9-164">You can also query by using LINQ, which translates toohello corresponding OData query expressions.</span></span> <span data-ttu-id="68ba9-165">Aqui está um exemplo de como toobuild consultas usando Olá .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="68ba9-165">Here's an example of how toobuild queries by using hello .NET SDK:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="68ba9-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="68ba9-166">Next steps</span></span>

<span data-ttu-id="68ba9-167">Neste tutorial, você fez a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="68ba9-167">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="68ba9-168">Aprendeu como tooquery usando Olá API de tabela (visualização)</span><span class="sxs-lookup"><span data-stu-id="68ba9-168">Learned how tooquery by using hello Table API (preview)</span></span> 

<span data-ttu-id="68ba9-169">Você pode continuar toolearn tutorial do próximo toohello como toodistribute seus dados globalmente.</span><span class="sxs-lookup"><span data-stu-id="68ba9-169">You can now proceed toohello next tutorial toolearn how toodistribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="68ba9-170">Distribuir os dados globalmente</span><span class="sxs-lookup"><span data-stu-id="68ba9-170">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)
