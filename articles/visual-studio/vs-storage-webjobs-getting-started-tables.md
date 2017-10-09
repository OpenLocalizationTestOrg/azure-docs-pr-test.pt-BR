---
title: "aaaGetting iniciado com o armazenamento do Azure e os serviços do Visual Studio conectado (WebJob projetos)"
description: "Como tooget iniciado usando o armazenamento de tabela do Azure em um projeto do Azure WebJobs no Visual Studio depois de conectar-se a conta de armazenamento tooa usando o Visual Studio conectada a serviços"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 061a6c46-0592-4e5d-aced-ab7498481cde
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 80d9f8d8b493ce612623dfed7e89325fb154a1c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-storage-azure-webjob-projects"></a>Introdução ao Armazenamento do Azure (Projetos WebJob do Azure)
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a>Visão geral
Este artigo fornece c# exemplos de código que mostram mostram como toouse Olá versão do SDK do Azure WebJobs 1. x com hello serviço de armazenamento de tabela do Azure. exemplos de código Olá usam Olá [SDK do WebJobs](../app-service-web/websites-dotnet-webjobs-sdk.md) versão 1. x.

saudação de serviço de armazenamento de tabela do Azure permite que você toostore grandes quantidades de dados estruturados. serviço de saudação é um repositório de dados NoSQL que aceita chamadas autenticadas de dentro e fora hello nuvem do Azure. As tabelas do Azure são ideais para armazenar dados estruturados não relacionais.  Consulte a [Introdução ao Armazenamento de Tabelas do Azure usando o .NET](../cosmos-db/table-storage-how-to-use-dotnet.md#create-a-table) para obter mais informações.

Alguns dos trechos de código Olá mostram Olá **tabela** usado nas funções que são chamadas manualmente, ou seja, não usando um dos atributos de gatilho de saudação do atributo.

## <a name="how-tooadd-entities-tooa-table"></a>Como tabela de tooa de entidades de tooadd
tabela de tooa tooadd entidades, use Olá **tabela** atributo com um **ICollector<T>**  ou **IAsyncCollector<T>**  parâmetro onde **T** Especifica o esquema de saudação de entidades Olá deseja tooadd. o construtor de atributo Olá leva um parâmetro de cadeia de caracteres que especifica o nome de saudação da tabela de saudação.

Olá exemplo de código a seguir adiciona **pessoa** tabela tooa de entidades denominada *entrada*.

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

Olá normalmente tipo usado com **ICollector** deriva **TableEntity** ou implementa **ITableEntity**, mas ele não precisa. Olá seguinte **pessoa** classes de trabalho com o código de Olá Olá anterior mostrado **entrada** método.

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

Se você desejar toowork diretamente com hello API de armazenamento do Azure, você pode adicionar uma **CloudStorageAccount** assinatura de método do parâmetro toohello.

## <a name="real-time-monitoring"></a>Monitoramento em tempo real
Como as funções de entrada de dados geralmente processam grandes volumes de dados, Olá painel do SDK do WebJobs fornece dados de monitoramento em tempo real. Olá **invocação Log** seção informa se a função hello ainda em execução.

![Função de entrada em execução](./media/vs-storage-webjobs-getting-started-tables/ingressrunning.png)

Olá **detalhes de invocação** página relatórios Olá andamento da função (número de entidades gravados) enquanto está em execução e fornece uma oportunidade tooabort-lo.

![Função de entrada em execução](./media/vs-storage-webjobs-getting-started-tables/ingressprogress.png)

Quando função hello termina, hello **detalhes de invocação** página relata o número de saudação de linhas gravadas.

![Função de entrada concluída](./media/vs-storage-webjobs-getting-started-tables/ingresssuccess.png)

## <a name="how-tooread-multiple-entities-from-a-table"></a>Como tooread várias entidades de uma tabela
tooread uma tabela, use Olá **tabela** atributo com um **IQueryable<T>**  parâmetro onde digitar **T** deriva **TableEntity**ou implementa **ITableEntity**.

Olá exemplo de código a seguir lê e registra em log todas as linhas de saudação **entrada** tabela:

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

### <a name="how-tooread-a-single-entity-from-a-table"></a>Como tooread uma única entidade de uma tabela
Há um **tabela** construtor de atributos com dois parâmetros adicionais que permitem que você especifique a chave de partição hello e chave de linha quando desejar toobind tooa tabela única entidade.

Olá, exemplo de código a seguir lê uma linha de tabela para uma **pessoa** entidade com base em partição chave e a linha de valores de chave recebidos em uma mensagem da fila:  

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


Olá **pessoa** classe neste exemplo não tem tooimplement **ITableEntity**.

## <a name="how-toouse-hello-net-storage-api-directly-toowork-with-a-table"></a>Como toouse Olá API de armazenamento .NET diretamente toowork com uma tabela
Você também pode usar o hello **tabela** atributo com um **CloudTable** objeto mais flexibilidade ao trabalhar com uma tabela.

exemplo de código a seguir Olá um **CloudTable** tooadd toohello uma única entidade do objeto *entrada* tabela.

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

Para obter mais informações sobre como Olá toouse **CloudTable** de objeto, consulte [Introdução ao armazenamento de tabela do Azure usando o .NET](../storage/storage-dotnet-how-to-use-tables.md).

## <a name="related-topics-covered-by-hello-queues-how-tooarticle"></a>Tópicos relacionados cobertos por filas de saudação como-tooarticle
Para obter informações sobre como processamento de tabela toohandle disparada por uma mensagem da fila, ou para WebJobs cenários do SDK não específicas tootable processamento, consulte [guia de Introdução ao armazenamento de fila do Azure e o Visual Studio conectada a serviços (WebJob projetos) ](../storage/vs-storage-webjobs-getting-started-queues.md).

## <a name="next-steps"></a>Próximas etapas
Este artigo fornece código exemplos que mostram como os cenários comuns de toohandle para trabalhar com tabelas do Azure. Para obter mais informações sobre como toouse WebJobs do Azure e hello WebJobs SDK, consulte [recursos de documentação do Azure WebJobs](http://go.microsoft.com/fwlink/?linkid=390226).

