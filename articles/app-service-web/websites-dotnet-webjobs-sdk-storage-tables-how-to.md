---
title: Como usar o armazenamento de tabela do Azure com o SDK de Trabalhos Web
description: Saiba como usar o armazenamento de tabela do Azure com o SDK de Trabalhos Web. Crie tabelas, adicione entidades a tabelas e leia tabelas existentes.
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 451432cc-c780-4310-85d3-84f44fe48afe
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 13cfc788c14d714df7022ce003d34691cf73d121
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-azure-table-storage-with-the-webjobs-sdk"></a><span data-ttu-id="f131a-104">Como usar o armazenamento de tabela do Azure com o SDK de Trabalhos Web</span><span class="sxs-lookup"><span data-stu-id="f131a-104">How to use Azure table storage with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="f131a-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="f131a-105">Overview</span></span>
<span data-ttu-id="f131a-106">Este guia fornece exemplos de código em C# que mostram como ler e gravar tabelas de armazenamento do Azure usando o [SDK de Trabalhos Web](websites-dotnet-webjobs-sdk.md) versão 1.x.</span><span class="sxs-lookup"><span data-stu-id="f131a-106">This guide provides C# code samples that show how to read and write Azure storage tables by using [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="f131a-107">Este guia pressupõe que você sabe [como criar um projeto WebJob no Visual Studio com cadeias de conexão que apontam para sua conta de armazenamento](websites-dotnet-webjobs-sdk-get-started.md) ou para [várias contas de armazenamento](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="f131a-107">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md) or to [multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

<span data-ttu-id="f131a-108">Alguns dos trechos de código mostram o atributo `Table` usado nas funções que são [chamadas manualmente](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), ou seja, que não usam um dos atributos de acionamento.</span><span class="sxs-lookup"><span data-stu-id="f131a-108">Some of the code snippets show the `Table` attribute used in functions that are [called manually](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), that is, not by using one of the trigger attributes.</span></span> 

## <span data-ttu-id="f131a-109"><a id="ingress"></a> Como adicionar entidades a uma tabela</span><span class="sxs-lookup"><span data-stu-id="f131a-109"><a id="ingress"></a> How to add entities to a table</span></span>
<span data-ttu-id="f131a-110">Para adicionar entidades em uma tabela, use o atributo `Table` com um parâmetro `ICollector<T>` ou `IAsyncCollector<T>`, no qual `T` especifica o esquema das entidades que você deseja adicionar.</span><span class="sxs-lookup"><span data-stu-id="f131a-110">To add entities to a table, use the `Table` attribute with an `ICollector<T>` or `IAsyncCollector<T>` parameter where `T` specifies the schema of the entities you want to add.</span></span> <span data-ttu-id="f131a-111">O construtor de atributo tem um parâmetro de cadeia que especifica o nome da tabela.</span><span class="sxs-lookup"><span data-stu-id="f131a-111">The attribute constructor takes a string parameter that specifies the name of the table.</span></span> 

<span data-ttu-id="f131a-112">O exemplo de código a seguir adiciona entidades `Person` em uma tabela nomeada *entrada*.</span><span class="sxs-lookup"><span data-stu-id="f131a-112">The following code sample adds `Person` entities to a table named *Ingress*.</span></span>

        [NoAutomaticTrigger]
        public static void IngressDemo(
            [Table("Ingress")] ICollector<Person> tableBinding)
        {
            for (int i = 0; i < 100000; i++)
            {
                tableBinding.Add(
                    new Person() { 
                        PartitionKey = "Test", 
                        RowKey = i.ToString(), 
                        Name = "Name" }
                    );
            }
        }

<span data-ttu-id="f131a-113">Geralmente, o tipo que você usa com `ICollector` deriva de `TableEntity` ou implementa `ITableEntity`,  mas ele não precisa fazer isso.</span><span class="sxs-lookup"><span data-stu-id="f131a-113">Typically the type you use with `ICollector` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="f131a-114">Qualquer uma das seguintes classes `Person` funciona com o código mostrado no método `Ingress` anterior.</span><span class="sxs-lookup"><span data-stu-id="f131a-114">Either of the following `Person` classes work with the code shown in the preceding `Ingress` method.</span></span>

        public class Person : TableEntity
        {
            public string Name { get; set; }
        }

        public class Person
        {
            public string PartitionKey { get; set; }
            public string RowKey { get; set; }
            public string Name { get; set; }
        }

<span data-ttu-id="f131a-115">Para trabalhar diretamente com a API de armazenamento do Azure, você pode adicionar um parâmetro `CloudStorageAccount` à assinatura do método.</span><span class="sxs-lookup"><span data-stu-id="f131a-115">If you want to work directly with the Azure storage API, you can add a `CloudStorageAccount` parameter to the method signature.</span></span>

## <span data-ttu-id="f131a-116"><a id="monitor"></a> Monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="f131a-116"><a id="monitor"></a> Real-time monitoring</span></span>
<span data-ttu-id="f131a-117">Como as funções de entrada de dados geralmente processam grandes volumes de dados, o painel do SDK de Trabalhos Web fornece dados de monitoramento em tempo real.</span><span class="sxs-lookup"><span data-stu-id="f131a-117">Because data ingress functions often process large volumes of data, the WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="f131a-118">A seção **Log de Invocação** informa se a função ainda está em execução.</span><span class="sxs-lookup"><span data-stu-id="f131a-118">The **Invocation Log** section tells you if the function is still running.</span></span>

![Função de entrada em execução](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressrunning.png)

<span data-ttu-id="f131a-120">A página **Detalhes de Invocação** relata o progresso da função (número de entidades gravadas) enquanto ela está em execução e lhe dá a oportunidade de anulá-la.</span><span class="sxs-lookup"><span data-stu-id="f131a-120">The **Invocation Details** page reports the function's progress (number of entities written) while it's running and gives you an opportunity to abort it.</span></span> 

![Função de entrada em execução](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressprogress.png)

<span data-ttu-id="f131a-122">Quando a função é concluída, a página **Detalhes de Invocação** relata o número de linhas gravadas.</span><span class="sxs-lookup"><span data-stu-id="f131a-122">When the function finishes, the **Invocation Details** page reports the number of rows written.</span></span>

![Função de entrada concluída](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingresssuccess.png)

## <span data-ttu-id="f131a-124"><a id="multiple"></a> Como ler várias entidades de uma tabela</span><span class="sxs-lookup"><span data-stu-id="f131a-124"><a id="multiple"></a> How to read multiple entities from a table</span></span>
<span data-ttu-id="f131a-125">Para ler uma tabela, use o atributo `Table` com um parâmetro `IQueryable<T>`, em que tipo `T` deriva de `TableEntity` ou implementa `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="f131a-125">To read a table, use the `Table` attribute with an `IQueryable<T>` parameter where type `T` derives from `TableEntity` or implements `ITableEntity`.</span></span>

<span data-ttu-id="f131a-126">O seguinte exemplo de código lê e registra em log todas as linhas da tabela `Ingress`:</span><span class="sxs-lookup"><span data-stu-id="f131a-126">The following code sample reads and logs all rows from the `Ingress` table:</span></span>

        public static void ReadTable(
            [Table("Ingress")] IQueryable<Person> tableBinding,
            TextWriter logger)
        {
            var query = from p in tableBinding select p;
            foreach (Person person in query)
            {
                logger.WriteLine("PK:{0}, RK:{1}, Name:{2}", 
                    person.PartitionKey, person.RowKey, person.Name);
            }
        }

### <span data-ttu-id="f131a-127"><a id="readone"></a> Como ler uma única entidade de uma tabela</span><span class="sxs-lookup"><span data-stu-id="f131a-127"><a id="readone"></a> How to read a single entity from a table</span></span>
<span data-ttu-id="f131a-128">Há um construtor de atributo `Table` com dois parâmetros adicionais que permite especificar a chave de partição e a chave de linha quando você deseja associar a uma entidade de tabela única.</span><span class="sxs-lookup"><span data-stu-id="f131a-128">There is a `Table` attribute constructor with two additional parameters that let you specify the partition key and row key when you want to bind to a single table entity.</span></span>

<span data-ttu-id="f131a-129">O seguinte exemplo de código lê uma linha de tabela para uma entidade `Person` com base nos valores de chave de partição e chave de linha recebidos em uma mensagem de fila:</span><span class="sxs-lookup"><span data-stu-id="f131a-129">The following code sample reads a table row for a `Person` entity based on partition key and row key values received in a queue message:</span></span>  

        public static void ReadTableEntity(
            [QueueTrigger("inputqueue")] Person personInQueue,
            [Table("persontable","{PartitionKey}", "{RowKey}")] Person personInTable,
            TextWriter logger)
        {
            if (personInTable == null)
            {
                logger.WriteLine("Person not found: PK:{0}, RK:{1}",
                        personInQueue.PartitionKey, personInQueue.RowKey);
            }
            else
            {
                logger.WriteLine("Person found: PK:{0}, RK:{1}, Name:{2}",
                        personInTable.PartitionKey, personInTable.RowKey, personInTable.Name);
            }
        }


<span data-ttu-id="f131a-130">A classe `Person` nesse exemplo não precisa implementar `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="f131a-130">The `Person` class in this example does not have to implement `ITableEntity`.</span></span>

## <span data-ttu-id="f131a-131"><a id="storageapi"></a> Como usar a API de Armazenamento .NET diretamente para trabalhar com uma tabela</span><span class="sxs-lookup"><span data-stu-id="f131a-131"><a id="storageapi"></a> How to use the .NET Storage API directly to work with a table</span></span>
<span data-ttu-id="f131a-132">Você também pode usar o atributo `Table` com um objeto `CloudTable` para ter mais flexibilidade ao trabalhar com uma tabela.</span><span class="sxs-lookup"><span data-stu-id="f131a-132">You can also use the `Table` attribute with a `CloudTable` object for more flexibility in working with a table.</span></span>

<span data-ttu-id="f131a-133">A seguinte amostra de código usa um objeto `CloudTable` para adicionar uma única entidade de *entrada* à tabela.</span><span class="sxs-lookup"><span data-stu-id="f131a-133">The following code sample uses a `CloudTable` object to add a single entity to the *Ingress* table.</span></span> 

        public static void UseStorageAPI(
            [Table("Ingress")] CloudTable tableBinding,
            TextWriter logger)
        {
            var person = new Person()
                {
                    PartitionKey = "Test",
                    RowKey = "100",
                    Name = "Name"
                };
            TableOperation insertOperation = TableOperation.Insert(person);
            tableBinding.Execute(insertOperation);
        }

<span data-ttu-id="f131a-134">Para obter mais informações sobre como usar o objeto `CloudTable` , consulte [Como usar o Armazenamento de Tabela do .NET](../cosmos-db/table-storage-how-to-use-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="f131a-134">For more information about how to use the `CloudTable` object, see [How to use Table Storage from .NET](../cosmos-db/table-storage-how-to-use-dotnet.md).</span></span> 

## <span data-ttu-id="f131a-135"><a id="queues"></a>Tópicos relacionados abordados no artigo de instruções sobre filas</span><span class="sxs-lookup"><span data-stu-id="f131a-135"><a id="queues"></a>Related topics covered by the queues how-to article</span></span>
<span data-ttu-id="f131a-136">Para obter informações sobre como lidar com o processamento de tabelas acionado por uma mensagem da fila ou para cenários do SDK de Trabalhos Web não específicos do processamento de tabelas, consulte [Como usar o armazenamento de fila do Azure com o SDK de Trabalhos Web](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="f131a-136">For information about how to handle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific to table processing, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="f131a-137">Os tópicos abordados nesse artigo incluem o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f131a-137">Topics covered in that article include the following:</span></span>

* <span data-ttu-id="f131a-138">Funções assíncronas</span><span class="sxs-lookup"><span data-stu-id="f131a-138">Async functions</span></span>
* <span data-ttu-id="f131a-139">Várias instâncias</span><span class="sxs-lookup"><span data-stu-id="f131a-139">Multiple instances</span></span>
* <span data-ttu-id="f131a-140">Desligamento normal</span><span class="sxs-lookup"><span data-stu-id="f131a-140">Graceful shutdown</span></span>
* <span data-ttu-id="f131a-141">Usar atributos do SDK de Trabalhos Web no corpo de uma função</span><span class="sxs-lookup"><span data-stu-id="f131a-141">Use WebJobs SDK attributes in the body of a function</span></span>
* <span data-ttu-id="f131a-142">Definir as cadeias de conexão do SDK no código</span><span class="sxs-lookup"><span data-stu-id="f131a-142">Set the SDK connection strings in code</span></span>
* <span data-ttu-id="f131a-143">Definir valores para parâmetros do construtor do SDK WebJobs no código</span><span class="sxs-lookup"><span data-stu-id="f131a-143">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="f131a-144">Disparar uma função manualmente</span><span class="sxs-lookup"><span data-stu-id="f131a-144">Trigger a function manually</span></span>
* <span data-ttu-id="f131a-145">Gravar logs</span><span class="sxs-lookup"><span data-stu-id="f131a-145">Write logs</span></span>

## <span data-ttu-id="f131a-146"><a id="nextsteps"></a> Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f131a-146"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="f131a-147">Este guia forneceu exemplos de código que mostram como lidar com cenários comuns para trabalhar com tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="f131a-147">This guide has provided code samples that show how to handle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="f131a-148">Para obter mais informações sobre como usar os Trabalhos Web do Azure e o SDK de Trabalhos Web, consulte [Trabalhos Web do Azure – Recursos recomendados](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="f131a-148">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

