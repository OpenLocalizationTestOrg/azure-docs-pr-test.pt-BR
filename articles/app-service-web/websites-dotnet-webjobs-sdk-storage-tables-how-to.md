---
title: aaaHow toouse armazenamento de tabela do Azure com hello SDK do WebJobs
description: Saiba como o armazenamento com hello SDK do WebJobs de tabela toouse do Azure. Criar tabelas, adicionar entidades tootables e ler as tabelas existentes.
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
ms.openlocfilehash: 8e28c69df4a934646add9e50c6de28e76dca1636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-with-hello-webjobs-sdk"></a><span data-ttu-id="765ff-104">Como o armazenamento com hello SDK do WebJobs de tabela toouse do Azure</span><span class="sxs-lookup"><span data-stu-id="765ff-104">How toouse Azure table storage with hello WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="765ff-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="765ff-105">Overview</span></span>
<span data-ttu-id="765ff-106">Este guia fornece exemplos de código do c# que mostra como tooread e gravação de armazenamento do Azure tabelas usando [SDK do WebJobs](websites-dotnet-webjobs-sdk.md) versão 1. x.</span><span class="sxs-lookup"><span data-stu-id="765ff-106">This guide provides C# code samples that show how tooread and write Azure storage tables by using [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="765ff-107">Guia de saudação pressupõe que você sabe [como toocreate um projeto do WebJob no Visual Studio com conexão cadeias de caracteres essa conta de armazenamento de ponto tooyour](websites-dotnet-webjobs-sdk-get-started.md) ou muito[várias contas de armazenamento](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="765ff-107">hello guide assumes you know [how toocreate a WebJob project in Visual Studio with connection strings that point tooyour storage account](websites-dotnet-webjobs-sdk-get-started.md) or too[multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

<span data-ttu-id="765ff-108">Alguns dos trechos de código Olá mostram Olá `Table` atributo usado em funções que são [chamado manualmente](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), ou seja, não usando um dos atributos de gatilho hello.</span><span class="sxs-lookup"><span data-stu-id="765ff-108">Some of hello code snippets show hello `Table` attribute used in functions that are [called manually](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), that is, not by using one of hello trigger attributes.</span></span> 

## <span data-ttu-id="765ff-109"><a id="ingress"></a>Como tabela de tooa de entidades de tooadd</span><span class="sxs-lookup"><span data-stu-id="765ff-109"><a id="ingress"></a> How tooadd entities tooa table</span></span>
<span data-ttu-id="765ff-110">tabela de tooa tooadd entidades, use Olá `Table` atributo com um `ICollector<T>` ou `IAsyncCollector<T>` parâmetro onde `T` Especifica o esquema de saudação de entidades Olá deseja tooadd.</span><span class="sxs-lookup"><span data-stu-id="765ff-110">tooadd entities tooa table, use hello `Table` attribute with an `ICollector<T>` or `IAsyncCollector<T>` parameter where `T` specifies hello schema of hello entities you want tooadd.</span></span> <span data-ttu-id="765ff-111">o construtor de atributo Olá leva um parâmetro de cadeia de caracteres que especifica o nome de saudação da tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="765ff-111">hello attribute constructor takes a string parameter that specifies hello name of hello table.</span></span> 

<span data-ttu-id="765ff-112">Olá exemplo de código a seguir adiciona `Person` tabela tooa de entidades denominada *entrada*.</span><span class="sxs-lookup"><span data-stu-id="765ff-112">hello following code sample adds `Person` entities tooa table named *Ingress*.</span></span>

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

<span data-ttu-id="765ff-113">Olá normalmente tipo usado com `ICollector` deriva `TableEntity` ou implementa `ITableEntity`, mas ele não precisa.</span><span class="sxs-lookup"><span data-stu-id="765ff-113">Typically hello type you use with `ICollector` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="765ff-114">Olá seguinte `Person` classes de trabalho com o código de Olá Olá anterior mostrado `Ingress` método.</span><span class="sxs-lookup"><span data-stu-id="765ff-114">Either of hello following `Person` classes work with hello code shown in hello preceding `Ingress` method.</span></span>

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

<span data-ttu-id="765ff-115">Se você desejar toowork diretamente com hello API de armazenamento do Azure, você pode adicionar um `CloudStorageAccount` a assinatura do método toohello parâmetro.</span><span class="sxs-lookup"><span data-stu-id="765ff-115">If you want toowork directly with hello Azure storage API, you can add a `CloudStorageAccount` parameter toohello method signature.</span></span>

## <span data-ttu-id="765ff-116"><a id="monitor"></a> Monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="765ff-116"><a id="monitor"></a> Real-time monitoring</span></span>
<span data-ttu-id="765ff-117">Como as funções de entrada de dados geralmente processam grandes volumes de dados, Olá painel do SDK do WebJobs fornece dados de monitoramento em tempo real.</span><span class="sxs-lookup"><span data-stu-id="765ff-117">Because data ingress functions often process large volumes of data, hello WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="765ff-118">Olá **invocação Log** seção informa se a função hello ainda em execução.</span><span class="sxs-lookup"><span data-stu-id="765ff-118">hello **Invocation Log** section tells you if hello function is still running.</span></span>

![Função de entrada em execução](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressrunning.png)

<span data-ttu-id="765ff-120">Olá **detalhes de invocação** página relatórios Olá andamento da função (número de entidades gravados) enquanto está em execução e fornece uma oportunidade tooabort-lo.</span><span class="sxs-lookup"><span data-stu-id="765ff-120">hello **Invocation Details** page reports hello function's progress (number of entities written) while it's running and gives you an opportunity tooabort it.</span></span> 

![Função de entrada em execução](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressprogress.png)

<span data-ttu-id="765ff-122">Quando função hello termina, hello **detalhes de invocação** página relata o número de saudação de linhas gravadas.</span><span class="sxs-lookup"><span data-stu-id="765ff-122">When hello function finishes, hello **Invocation Details** page reports hello number of rows written.</span></span>

![Função de entrada concluída](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingresssuccess.png)

## <span data-ttu-id="765ff-124"><a id="multiple"></a>Como tooread várias entidades de uma tabela</span><span class="sxs-lookup"><span data-stu-id="765ff-124"><a id="multiple"></a> How tooread multiple entities from a table</span></span>
<span data-ttu-id="765ff-125">tooread uma tabela, use Olá `Table` atributo com um `IQueryable<T>` parâmetro onde digitar `T` deriva `TableEntity` ou implementa `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="765ff-125">tooread a table, use hello `Table` attribute with an `IQueryable<T>` parameter where type `T` derives from `TableEntity` or implements `ITableEntity`.</span></span>

<span data-ttu-id="765ff-126">Olá exemplo de código a seguir lê e registra em log todas as linhas de saudação `Ingress` tabela:</span><span class="sxs-lookup"><span data-stu-id="765ff-126">hello following code sample reads and logs all rows from hello `Ingress` table:</span></span>

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

### <span data-ttu-id="765ff-127"><a id="readone"></a>Como tooread uma única entidade de uma tabela</span><span class="sxs-lookup"><span data-stu-id="765ff-127"><a id="readone"></a> How tooread a single entity from a table</span></span>
<span data-ttu-id="765ff-128">Há um `Table` construtor de atributos com dois parâmetros adicionais que permitem que você especifique a chave de partição hello e chave de linha quando desejar toobind tooa tabela única entidade.</span><span class="sxs-lookup"><span data-stu-id="765ff-128">There is a `Table` attribute constructor with two additional parameters that let you specify hello partition key and row key when you want toobind tooa single table entity.</span></span>

<span data-ttu-id="765ff-129">Olá, exemplo de código a seguir lê uma linha de tabela para um `Person` entidade com base em partição chave e a linha de valores de chave recebidos em uma mensagem da fila:</span><span class="sxs-lookup"><span data-stu-id="765ff-129">hello following code sample reads a table row for a `Person` entity based on partition key and row key values received in a queue message:</span></span>  

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


<span data-ttu-id="765ff-130">Olá `Person` classe neste exemplo não tem tooimplement `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="765ff-130">hello `Person` class in this example does not have tooimplement `ITableEntity`.</span></span>

## <span data-ttu-id="765ff-131"><a id="storageapi"></a>Como toouse Olá API de armazenamento .NET diretamente toowork com uma tabela</span><span class="sxs-lookup"><span data-stu-id="765ff-131"><a id="storageapi"></a> How toouse hello .NET Storage API directly toowork with a table</span></span>
<span data-ttu-id="765ff-132">Você também pode usar o hello `Table` atributo com um `CloudTable` objeto mais flexibilidade ao trabalhar com uma tabela.</span><span class="sxs-lookup"><span data-stu-id="765ff-132">You can also use hello `Table` attribute with a `CloudTable` object for more flexibility in working with a table.</span></span>

<span data-ttu-id="765ff-133">exemplo de código a seguir Olá um `CloudTable` tooadd toohello uma única entidade do objeto *entrada* tabela.</span><span class="sxs-lookup"><span data-stu-id="765ff-133">hello following code sample uses a `CloudTable` object tooadd a single entity toohello *Ingress* table.</span></span> 

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

<span data-ttu-id="765ff-134">Para obter mais informações sobre como Olá toouse `CloudTable` de objeto, consulte [como toouse o armazenamento de tabela do .NET](../cosmos-db/table-storage-how-to-use-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="765ff-134">For more information about how toouse hello `CloudTable` object, see [How toouse Table Storage from .NET](../cosmos-db/table-storage-how-to-use-dotnet.md).</span></span> 

## <span data-ttu-id="765ff-135"><a id="queues"></a>Tópicos relacionados cobertos por filas de saudação como-tooarticle</span><span class="sxs-lookup"><span data-stu-id="765ff-135"><a id="queues"></a>Related topics covered by hello queues how-tooarticle</span></span>
<span data-ttu-id="765ff-136">Para obter informações sobre como processamento de tabela toohandle disparada por uma mensagem da fila, ou para WebJobs cenários do SDK não específicas tootable processamento, consulte [como toouse Azure fila de armazenamento com hello SDK do WebJobs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="765ff-136">For information about how toohandle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific tootable processing, see [How toouse Azure queue storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="765ff-137">Os tópicos abordados nesse artigo incluem o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="765ff-137">Topics covered in that article include hello following:</span></span>

* <span data-ttu-id="765ff-138">Funções assíncronas</span><span class="sxs-lookup"><span data-stu-id="765ff-138">Async functions</span></span>
* <span data-ttu-id="765ff-139">Várias instâncias</span><span class="sxs-lookup"><span data-stu-id="765ff-139">Multiple instances</span></span>
* <span data-ttu-id="765ff-140">Desligamento normal</span><span class="sxs-lookup"><span data-stu-id="765ff-140">Graceful shutdown</span></span>
* <span data-ttu-id="765ff-141">Usar atributos de SDK do WebJobs no corpo de saudação de uma função</span><span class="sxs-lookup"><span data-stu-id="765ff-141">Use WebJobs SDK attributes in hello body of a function</span></span>
* <span data-ttu-id="765ff-142">Cadeias de conexão do conjunto Olá SDK no código</span><span class="sxs-lookup"><span data-stu-id="765ff-142">Set hello SDK connection strings in code</span></span>
* <span data-ttu-id="765ff-143">Definir valores para parâmetros do construtor do SDK WebJobs no código</span><span class="sxs-lookup"><span data-stu-id="765ff-143">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="765ff-144">Disparar uma função manualmente</span><span class="sxs-lookup"><span data-stu-id="765ff-144">Trigger a function manually</span></span>
* <span data-ttu-id="765ff-145">Gravar logs</span><span class="sxs-lookup"><span data-stu-id="765ff-145">Write logs</span></span>

## <span data-ttu-id="765ff-146"><a id="nextsteps"></a> Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="765ff-146"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="765ff-147">Este guia fornece código exemplos que mostram como os cenários comuns de toohandle para trabalhar com tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="765ff-147">This guide has provided code samples that show how toohandle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="765ff-148">Para obter mais informações sobre como toouse WebJobs do Azure e hello WebJobs SDK, consulte [recursos recomendada do Azure WebJobs](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="765ff-148">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

