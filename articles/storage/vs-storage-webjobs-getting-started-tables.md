---
title: "Introdução ao armazenamento do Azure e aos Serviços Conectados do Visual Studio (projetos WebJob)"
description: "Como começar a usar o armazenamento de Tabela do Azure em um projeto WebJobs no Visual Studio após a conexão a uma conta de armazenamento usando os serviços conectados do Visual Studio"
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
ms.openlocfilehash: 79fba102377cdc6b681f6798699767961040a7e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-storage-azure-webjob-projects"></a><span data-ttu-id="0d35e-103">Introdução ao Armazenamento do Azure (Projetos WebJob do Azure)</span><span class="sxs-lookup"><span data-stu-id="0d35e-103">Getting Started with Azure Storage (Azure WebJob Projects)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="0d35e-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="0d35e-104">Overview</span></span>
<span data-ttu-id="0d35e-105">Este guia fornece exemplos de código em C# que mostram como usar o SDK do Azure WebJobs versão 1.x com o serviço de armazenamento de tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="0d35e-105">This article provides C# code samples that show show how to use the Azure WebJobs SDK version 1.x with the Azure table storage service.</span></span> <span data-ttu-id="0d35e-106">Os exemplos de código usam o [SDK WebJobs](../app-service-web/websites-dotnet-webjobs-sdk.md) versão 1.x.</span><span class="sxs-lookup"><span data-stu-id="0d35e-106">The code samples use the [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="0d35e-107">O serviço de armazenamento de Tabela do Azure armazena grandes quantidades de dados estruturados.</span><span class="sxs-lookup"><span data-stu-id="0d35e-107">The Azure Table storage service enables you to store large amounts of structured data.</span></span> <span data-ttu-id="0d35e-108">O serviço é um repositório de dados NoSQL que aceita chamadas autenticadas de dentro e de fora da nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="0d35e-108">The service is a NoSQL datastore that accepts authenticated calls from inside and outside the Azure cloud.</span></span> <span data-ttu-id="0d35e-109">As tabelas do Azure são ideais para armazenar dados estruturados não relacionais.</span><span class="sxs-lookup"><span data-stu-id="0d35e-109">Azure tables are ideal for storing structured, non-relational data.</span></span>  <span data-ttu-id="0d35e-110">Consulte a [Introdução ao Armazenamento de Tabelas do Azure usando o .NET](storage-dotnet-how-to-use-tables.md#create-a-table) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="0d35e-110">See [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md#create-a-table) for more information.</span></span>

<span data-ttu-id="0d35e-111">Alguns dos trechos de código mostram o atributo **Table** usado nas funções que são chamadas manualmente ou seja, que não usam um dos atributos de gatilho.</span><span class="sxs-lookup"><span data-stu-id="0d35e-111">Some of the code snippets show the **Table** attribute used in functions that are called manually, that is, not by using one of the trigger attributes.</span></span>

## <a name="how-to-add-entities-to-a-table"></a><span data-ttu-id="0d35e-112">Como adicionar entidades a uma tabela</span><span class="sxs-lookup"><span data-stu-id="0d35e-112">How to add entities to a table</span></span>
<span data-ttu-id="0d35e-113">Para adicionar entidades a uma tabela, use o atributo **Table** com um parâmetro **ICollector<T>** ou **IAsyncCollector<T>**, em que **T** especifica o esquema das entidades que você deseja adicionar.</span><span class="sxs-lookup"><span data-stu-id="0d35e-113">To add entities to a table, use the **Table** attribute with an **ICollector<T>** or **IAsyncCollector<T>** parameter where **T** specifies the schema of the entities you want to add.</span></span> <span data-ttu-id="0d35e-114">O construtor de atributo tem um parâmetro de cadeia que especifica o nome da tabela.</span><span class="sxs-lookup"><span data-stu-id="0d35e-114">The attribute constructor takes a string parameter that specifies the name of the table.</span></span>

<span data-ttu-id="0d35e-115">O exemplo de código a seguir adiciona entidades **Person** a uma tabela denominada *Ingress*.</span><span class="sxs-lookup"><span data-stu-id="0d35e-115">The following code sample adds **Person** entities to a table named *Ingress*.</span></span>

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

<span data-ttu-id="0d35e-116">Normalmente, o tipo que você usa com **ICollector** deriva de **TableEntity** ou implementa **ITableEntity**, mas isso não é necessário.</span><span class="sxs-lookup"><span data-stu-id="0d35e-116">Typically the type you use with **ICollector** derives from **TableEntity** or implements **ITableEntity**, but it doesn't have to.</span></span> <span data-ttu-id="0d35e-117">Qualquer uma das seguintes classes **Person** funciona com o código mostrado no método **Ingress** anterior.</span><span class="sxs-lookup"><span data-stu-id="0d35e-117">Either of the following **Person** classes work with the code shown in the preceding **Ingress** method.</span></span>

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

<span data-ttu-id="0d35e-118">Se quiser trabalhar diretamente com a API de armazenamento do Azure, você pode adicionar um parâmetro **CloudStorageAccount** à assinatura do método.</span><span class="sxs-lookup"><span data-stu-id="0d35e-118">If you want to work directly with the Azure storage API, you can add a **CloudStorageAccount** parameter to the method signature.</span></span>

## <a name="real-time-monitoring"></a><span data-ttu-id="0d35e-119">Monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="0d35e-119">Real-time monitoring</span></span>
<span data-ttu-id="0d35e-120">Como as funções de entrada de dados geralmente processam grandes volumes de dados, o painel do SDK de Trabalhos Web fornece dados de monitoramento em tempo real.</span><span class="sxs-lookup"><span data-stu-id="0d35e-120">Because data ingress functions often process large volumes of data, the WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="0d35e-121">A seção **Log de Invocação** informa se a função ainda está em execução.</span><span class="sxs-lookup"><span data-stu-id="0d35e-121">The **Invocation Log** section tells you if the function is still running.</span></span>

![Função de entrada em execução](./media/vs-storage-webjobs-getting-started-tables/ingressrunning.png)

<span data-ttu-id="0d35e-123">A página **Detalhes de Invocação** relata o progresso da função (número de entidades gravadas) enquanto ela está em execução e lhe dá a oportunidade de anulá-la.</span><span class="sxs-lookup"><span data-stu-id="0d35e-123">The **Invocation Details** page reports the function's progress (number of entities written) while it's running and gives you an opportunity to abort it.</span></span>

![Função de entrada em execução](./media/vs-storage-webjobs-getting-started-tables/ingressprogress.png)

<span data-ttu-id="0d35e-125">Quando a função é concluída, a página **Detalhes de Invocação** relata o número de linhas gravadas.</span><span class="sxs-lookup"><span data-stu-id="0d35e-125">When the function finishes, the **Invocation Details** page reports the number of rows written.</span></span>

![Função de entrada concluída](./media/vs-storage-webjobs-getting-started-tables/ingresssuccess.png)

## <a name="how-to-read-multiple-entities-from-a-table"></a><span data-ttu-id="0d35e-127">Como ler várias entidades de uma tabela</span><span class="sxs-lookup"><span data-stu-id="0d35e-127">How to read multiple entities from a table</span></span>
<span data-ttu-id="0d35e-128">Para ler uma tabela, use o atributo **Table** com um parâmetro **IQueryable<T>**, em que o tipo **T** deriva de **TableEntity** ou implementa **ITableEntity**.</span><span class="sxs-lookup"><span data-stu-id="0d35e-128">To read a table, use the **Table** attribute with an **IQueryable<T>** parameter where type **T** derives from **TableEntity** or implements **ITableEntity**.</span></span>

<span data-ttu-id="0d35e-129">O seguinte exemplo de código lê e registra em log todas as linhas da tabela **Ingress** :</span><span class="sxs-lookup"><span data-stu-id="0d35e-129">The following code sample reads and logs all rows from the **Ingress** table:</span></span>

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

### <a name="how-to-read-a-single-entity-from-a-table"></a><span data-ttu-id="0d35e-130">Como ler uma única entidade de uma tabela</span><span class="sxs-lookup"><span data-stu-id="0d35e-130">How to read a single entity from a table</span></span>
<span data-ttu-id="0d35e-131">Há um construtor de atributo **Table** com dois parâmetros adicionais que permite especificar a chave de partição e a chave de linha quando você deseja associar a uma entidade de tabela única.</span><span class="sxs-lookup"><span data-stu-id="0d35e-131">There is a **Table** attribute constructor with two additional parameters that let you specify the partition key and row key when you want to bind to a single table entity.</span></span>

<span data-ttu-id="0d35e-132">O seguinte exemplo de código lê uma linha de tabela para uma entidade **Person** com base nos valores de chave de partição e chave de linha recebidos em uma mensagem de fila:</span><span class="sxs-lookup"><span data-stu-id="0d35e-132">The following code sample reads a table row for a **Person** entity based on partition key and row key values received in a queue message:</span></span>  

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


<span data-ttu-id="0d35e-133">A classe **Person** neste exemplo não precisa implementar **ITableEntity**.</span><span class="sxs-lookup"><span data-stu-id="0d35e-133">The **Person** class in this example does not have to implement **ITableEntity**.</span></span>

## <a name="how-to-use-the-net-storage-api-directly-to-work-with-a-table"></a><span data-ttu-id="0d35e-134">Como usar a API de Armazenamento .NET diretamente para trabalhar com uma tabela</span><span class="sxs-lookup"><span data-stu-id="0d35e-134">How to use the .NET Storage API directly to work with a table</span></span>
<span data-ttu-id="0d35e-135">Você também pode usar o atributo **Table** com um objeto **CloudTable** para ter mais flexibilidade ao trabalhar com uma tabela.</span><span class="sxs-lookup"><span data-stu-id="0d35e-135">You can also use the **Table** attribute with a **CloudTable** object for more flexibility in working with a table.</span></span>

<span data-ttu-id="0d35e-136">O exemplo de código a seguir usa um objeto **CloudTable** para adicionar uma única entidade à tabela *Ingress* .</span><span class="sxs-lookup"><span data-stu-id="0d35e-136">The following code sample uses a **CloudTable** object to add a single entity to the *Ingress* table.</span></span>

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

<span data-ttu-id="0d35e-137">Para saber mais sobre como usar o objeto **CloudTable** , consulte [Como usar o Armazenamento de Tabelas do Azure usando o .NET](storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="0d35e-137">For more information about how to use the **CloudTable** object, see [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md).</span></span>

## <a name="related-topics-covered-by-the-queues-how-to-article"></a><span data-ttu-id="0d35e-138">Tópicos relacionados abordados no artigo de instruções sobre filas</span><span class="sxs-lookup"><span data-stu-id="0d35e-138">Related topics covered by the queues how-to article</span></span>
<span data-ttu-id="0d35e-139">Para obter informações sobre como lidar com o processamento de tabelas acionado por uma mensagem da fila ou para cenários do SDK de WebJobs não específicos do processamento de tabelas, consulte [Introdução ao Armazenamento de Filas do Azure e aos serviços conectados do Visual Studio (Projetos do WebJob)](vs-storage-webjobs-getting-started-queues.md).</span><span class="sxs-lookup"><span data-stu-id="0d35e-139">For information about how to handle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific to table processing, see [Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)](vs-storage-webjobs-getting-started-queues.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d35e-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0d35e-140">Next steps</span></span>
<span data-ttu-id="0d35e-141">Este artigo forneceu exemplos de código que mostram como lidar com cenários comuns para trabalhar com tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="0d35e-141">This article has provided code samples that show how to handle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="0d35e-142">Para obter mais informações sobre como usar o Azure WebJobs e o SDK do WebJobs, consulte [Recursos de documentação do Azure WebJobs](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="0d35e-142">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

