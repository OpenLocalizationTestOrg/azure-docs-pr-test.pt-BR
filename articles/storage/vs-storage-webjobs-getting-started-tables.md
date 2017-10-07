---
title: "aaaGetting iniciado com o armazenamento do Azure e os serviços do Visual Studio conectado (WebJob projetos)"
description: "Como tooget iniciado usando o armazenamento de tabela do Azure em um projeto do Azure WebJobs no Visual Studio depois de conectar-se a conta de armazenamento tooa usando o Visual Studio conectada a serviços"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 061a6c46-0592-4e5d-aced-ab7498481cde
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 448dee3369207062ee85c6636c84bcb4e26a2085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-storage-azure-webjob-projects"></a><span data-ttu-id="d217b-103">Introdução ao Armazenamento do Azure (Projetos WebJob do Azure)</span><span class="sxs-lookup"><span data-stu-id="d217b-103">Getting Started with Azure Storage (Azure WebJob Projects)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="d217b-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d217b-104">Overview</span></span>
<span data-ttu-id="d217b-105">Este artigo fornece c# exemplos de código que mostram mostram como toouse Olá versão do SDK do Azure WebJobs 1. x com hello serviço de armazenamento de tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="d217b-105">This article provides C# code samples that show show how toouse hello Azure WebJobs SDK version 1.x with hello Azure table storage service.</span></span> <span data-ttu-id="d217b-106">exemplos de código Olá usam Olá [SDK do WebJobs](../app-service-web/websites-dotnet-webjobs-sdk.md) versão 1. x.</span><span class="sxs-lookup"><span data-stu-id="d217b-106">hello code samples use hello [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="d217b-107">saudação de serviço de armazenamento de tabela do Azure permite que você toostore grandes quantidades de dados estruturados.</span><span class="sxs-lookup"><span data-stu-id="d217b-107">hello Azure Table storage service enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="d217b-108">serviço de saudação é um repositório de dados NoSQL que aceita chamadas autenticadas de dentro e fora hello nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="d217b-108">hello service is a NoSQL datastore that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="d217b-109">As tabelas do Azure são ideais para armazenar dados estruturados não relacionais.</span><span class="sxs-lookup"><span data-stu-id="d217b-109">Azure tables are ideal for storing structured, non-relational data.</span></span>  <span data-ttu-id="d217b-110">Consulte a [Introdução ao Armazenamento de Tabelas do Azure usando o .NET](storage-dotnet-how-to-use-tables.md#create-a-table) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="d217b-110">See [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md#create-a-table) for more information.</span></span>

<span data-ttu-id="d217b-111">Alguns dos trechos de código Olá mostram Olá **tabela** usado nas funções que são chamadas manualmente, ou seja, não usando um dos atributos de gatilho de saudação do atributo.</span><span class="sxs-lookup"><span data-stu-id="d217b-111">Some of hello code snippets show hello **Table** attribute used in functions that are called manually, that is, not by using one of hello trigger attributes.</span></span>

## <a name="how-tooadd-entities-tooa-table"></a><span data-ttu-id="d217b-112">Como tabela de tooa de entidades de tooadd</span><span class="sxs-lookup"><span data-stu-id="d217b-112">How tooadd entities tooa table</span></span>
<span data-ttu-id="d217b-113">tabela de tooa tooadd entidades, use Olá **tabela** atributo com um **ICollector<T>**  ou **IAsyncCollector<T>**  parâmetro onde **T** Especifica o esquema de saudação de entidades Olá deseja tooadd.</span><span class="sxs-lookup"><span data-stu-id="d217b-113">tooadd entities tooa table, use hello **Table** attribute with an **ICollector<T>** or **IAsyncCollector<T>** parameter where **T** specifies hello schema of hello entities you want tooadd.</span></span> <span data-ttu-id="d217b-114">o construtor de atributo Olá leva um parâmetro de cadeia de caracteres que especifica o nome de saudação da tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="d217b-114">hello attribute constructor takes a string parameter that specifies hello name of hello table.</span></span>

<span data-ttu-id="d217b-115">Olá exemplo de código a seguir adiciona **pessoa** tabela tooa de entidades denominada *entrada*.</span><span class="sxs-lookup"><span data-stu-id="d217b-115">hello following code sample adds **Person** entities tooa table named *Ingress*.</span></span>

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

<span data-ttu-id="d217b-116">Olá normalmente tipo usado com **ICollector** deriva **TableEntity** ou implementa **ITableEntity**, mas ele não precisa.</span><span class="sxs-lookup"><span data-stu-id="d217b-116">Typically hello type you use with **ICollector** derives from **TableEntity** or implements **ITableEntity**, but it doesn't have to.</span></span> <span data-ttu-id="d217b-117">Olá seguinte **pessoa** classes de trabalho com o código de Olá Olá anterior mostrado **entrada** método.</span><span class="sxs-lookup"><span data-stu-id="d217b-117">Either of hello following **Person** classes work with hello code shown in hello preceding **Ingress** method.</span></span>

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

<span data-ttu-id="d217b-118">Se você desejar toowork diretamente com hello API de armazenamento do Azure, você pode adicionar uma **CloudStorageAccount** assinatura de método do parâmetro toohello.</span><span class="sxs-lookup"><span data-stu-id="d217b-118">If you want toowork directly with hello Azure storage API, you can add a **CloudStorageAccount** parameter toohello method signature.</span></span>

## <a name="real-time-monitoring"></a><span data-ttu-id="d217b-119">Monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="d217b-119">Real-time monitoring</span></span>
<span data-ttu-id="d217b-120">Como as funções de entrada de dados geralmente processam grandes volumes de dados, Olá painel do SDK do WebJobs fornece dados de monitoramento em tempo real.</span><span class="sxs-lookup"><span data-stu-id="d217b-120">Because data ingress functions often process large volumes of data, hello WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="d217b-121">Olá **invocação Log** seção informa se a função hello ainda em execução.</span><span class="sxs-lookup"><span data-stu-id="d217b-121">hello **Invocation Log** section tells you if hello function is still running.</span></span>

![Função de entrada em execução](./media/vs-storage-webjobs-getting-started-tables/ingressrunning.png)

<span data-ttu-id="d217b-123">Olá **detalhes de invocação** página relatórios Olá andamento da função (número de entidades gravados) enquanto está em execução e fornece uma oportunidade tooabort-lo.</span><span class="sxs-lookup"><span data-stu-id="d217b-123">hello **Invocation Details** page reports hello function's progress (number of entities written) while it's running and gives you an opportunity tooabort it.</span></span>

![Função de entrada em execução](./media/vs-storage-webjobs-getting-started-tables/ingressprogress.png)

<span data-ttu-id="d217b-125">Quando função hello termina, hello **detalhes de invocação** página relata o número de saudação de linhas gravadas.</span><span class="sxs-lookup"><span data-stu-id="d217b-125">When hello function finishes, hello **Invocation Details** page reports hello number of rows written.</span></span>

![Função de entrada concluída](./media/vs-storage-webjobs-getting-started-tables/ingresssuccess.png)

## <a name="how-tooread-multiple-entities-from-a-table"></a><span data-ttu-id="d217b-127">Como tooread várias entidades de uma tabela</span><span class="sxs-lookup"><span data-stu-id="d217b-127">How tooread multiple entities from a table</span></span>
<span data-ttu-id="d217b-128">tooread uma tabela, use Olá **tabela** atributo com um **IQueryable<T>**  parâmetro onde digitar **T** deriva **TableEntity**ou implementa **ITableEntity**.</span><span class="sxs-lookup"><span data-stu-id="d217b-128">tooread a table, use hello **Table** attribute with an **IQueryable<T>** parameter where type **T** derives from **TableEntity** or implements **ITableEntity**.</span></span>

<span data-ttu-id="d217b-129">Olá exemplo de código a seguir lê e registra em log todas as linhas de saudação **entrada** tabela:</span><span class="sxs-lookup"><span data-stu-id="d217b-129">hello following code sample reads and logs all rows from hello **Ingress** table:</span></span>

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

### <a name="how-tooread-a-single-entity-from-a-table"></a><span data-ttu-id="d217b-130">Como tooread uma única entidade de uma tabela</span><span class="sxs-lookup"><span data-stu-id="d217b-130">How tooread a single entity from a table</span></span>
<span data-ttu-id="d217b-131">Há um **tabela** construtor de atributos com dois parâmetros adicionais que permitem que você especifique a chave de partição hello e chave de linha quando desejar toobind tooa tabela única entidade.</span><span class="sxs-lookup"><span data-stu-id="d217b-131">There is a **Table** attribute constructor with two additional parameters that let you specify hello partition key and row key when you want toobind tooa single table entity.</span></span>

<span data-ttu-id="d217b-132">Olá, exemplo de código a seguir lê uma linha de tabela para uma **pessoa** entidade com base em partição chave e a linha de valores de chave recebidos em uma mensagem da fila:</span><span class="sxs-lookup"><span data-stu-id="d217b-132">hello following code sample reads a table row for a **Person** entity based on partition key and row key values received in a queue message:</span></span>  

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


<span data-ttu-id="d217b-133">Olá **pessoa** classe neste exemplo não tem tooimplement **ITableEntity**.</span><span class="sxs-lookup"><span data-stu-id="d217b-133">hello **Person** class in this example does not have tooimplement **ITableEntity**.</span></span>

## <a name="how-toouse-hello-net-storage-api-directly-toowork-with-a-table"></a><span data-ttu-id="d217b-134">Como toouse Olá API de armazenamento .NET diretamente toowork com uma tabela</span><span class="sxs-lookup"><span data-stu-id="d217b-134">How toouse hello .NET Storage API directly toowork with a table</span></span>
<span data-ttu-id="d217b-135">Você também pode usar o hello **tabela** atributo com um **CloudTable** objeto mais flexibilidade ao trabalhar com uma tabela.</span><span class="sxs-lookup"><span data-stu-id="d217b-135">You can also use hello **Table** attribute with a **CloudTable** object for more flexibility in working with a table.</span></span>

<span data-ttu-id="d217b-136">exemplo de código a seguir Olá um **CloudTable** tooadd toohello uma única entidade do objeto *entrada* tabela.</span><span class="sxs-lookup"><span data-stu-id="d217b-136">hello following code sample uses a **CloudTable** object tooadd a single entity toohello *Ingress* table.</span></span>

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

<span data-ttu-id="d217b-137">Para obter mais informações sobre como Olá toouse **CloudTable** de objeto, consulte [Introdução ao armazenamento de tabela do Azure usando o .NET](storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="d217b-137">For more information about how toouse hello **CloudTable** object, see [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md).</span></span>

## <a name="related-topics-covered-by-hello-queues-how-tooarticle"></a><span data-ttu-id="d217b-138">Tópicos relacionados cobertos por filas de saudação como-tooarticle</span><span class="sxs-lookup"><span data-stu-id="d217b-138">Related topics covered by hello queues how-tooarticle</span></span>
<span data-ttu-id="d217b-139">Para obter informações sobre como processamento de tabela toohandle disparada por uma mensagem da fila, ou para WebJobs cenários do SDK não específicas tootable processamento, consulte [guia de Introdução ao armazenamento de fila do Azure e o Visual Studio conectada a serviços (WebJob projetos) ](vs-storage-webjobs-getting-started-queues.md).</span><span class="sxs-lookup"><span data-stu-id="d217b-139">For information about how toohandle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific tootable processing, see [Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)](vs-storage-webjobs-getting-started-queues.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d217b-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d217b-140">Next steps</span></span>
<span data-ttu-id="d217b-141">Este artigo fornece código exemplos que mostram como os cenários comuns de toohandle para trabalhar com tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="d217b-141">This article has provided code samples that show how toohandle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="d217b-142">Para obter mais informações sobre como toouse WebJobs do Azure e hello WebJobs SDK, consulte [recursos de documentação do Azure WebJobs](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="d217b-142">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

