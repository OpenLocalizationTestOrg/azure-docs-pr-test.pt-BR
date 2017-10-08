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
# <a name="how-toouse-azure-table-storage-with-hello-webjobs-sdk"></a>Como o armazenamento com hello SDK do WebJobs de tabela toouse do Azure
## <a name="overview"></a>Visão geral
Este guia fornece exemplos de código do c# que mostra como tooread e gravação de armazenamento do Azure tabelas usando [SDK do WebJobs](websites-dotnet-webjobs-sdk.md) versão 1. x.

Guia de saudação pressupõe que você sabe [como toocreate um projeto do WebJob no Visual Studio com conexão cadeias de caracteres essa conta de armazenamento de ponto tooyour](websites-dotnet-webjobs-sdk-get-started.md) ou muito[várias contas de armazenamento](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).

Alguns dos trechos de código Olá mostram Olá `Table` atributo usado em funções que são [chamado manualmente](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), ou seja, não usando um dos atributos de gatilho hello. 

## <a id="ingress"></a>Como tabela de tooa de entidades de tooadd
tabela de tooa tooadd entidades, use Olá `Table` atributo com um `ICollector<T>` ou `IAsyncCollector<T>` parâmetro onde `T` Especifica o esquema de saudação de entidades Olá deseja tooadd. o construtor de atributo Olá leva um parâmetro de cadeia de caracteres que especifica o nome de saudação da tabela de saudação. 

Olá exemplo de código a seguir adiciona `Person` tabela tooa de entidades denominada *entrada*.

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

Olá normalmente tipo usado com `ICollector` deriva `TableEntity` ou implementa `ITableEntity`, mas ele não precisa. Olá seguinte `Person` classes de trabalho com o código de Olá Olá anterior mostrado `Ingress` método.

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

Se você desejar toowork diretamente com hello API de armazenamento do Azure, você pode adicionar um `CloudStorageAccount` a assinatura do método toohello parâmetro.

## <a id="monitor"></a> Monitoramento em tempo real
Como as funções de entrada de dados geralmente processam grandes volumes de dados, Olá painel do SDK do WebJobs fornece dados de monitoramento em tempo real. Olá **invocação Log** seção informa se a função hello ainda em execução.

![Função de entrada em execução](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressrunning.png)

Olá **detalhes de invocação** página relatórios Olá andamento da função (número de entidades gravados) enquanto está em execução e fornece uma oportunidade tooabort-lo. 

![Função de entrada em execução](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressprogress.png)

Quando função hello termina, hello **detalhes de invocação** página relata o número de saudação de linhas gravadas.

![Função de entrada concluída](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingresssuccess.png)

## <a id="multiple"></a>Como tooread várias entidades de uma tabela
tooread uma tabela, use Olá `Table` atributo com um `IQueryable<T>` parâmetro onde digitar `T` deriva `TableEntity` ou implementa `ITableEntity`.

Olá exemplo de código a seguir lê e registra em log todas as linhas de saudação `Ingress` tabela:

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

### <a id="readone"></a>Como tooread uma única entidade de uma tabela
Há um `Table` construtor de atributos com dois parâmetros adicionais que permitem que você especifique a chave de partição hello e chave de linha quando desejar toobind tooa tabela única entidade.

Olá, exemplo de código a seguir lê uma linha de tabela para um `Person` entidade com base em partição chave e a linha de valores de chave recebidos em uma mensagem da fila:  

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


Olá `Person` classe neste exemplo não tem tooimplement `ITableEntity`.

## <a id="storageapi"></a>Como toouse Olá API de armazenamento .NET diretamente toowork com uma tabela
Você também pode usar o hello `Table` atributo com um `CloudTable` objeto mais flexibilidade ao trabalhar com uma tabela.

exemplo de código a seguir Olá um `CloudTable` tooadd toohello uma única entidade do objeto *entrada* tabela. 

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

Para obter mais informações sobre como Olá toouse `CloudTable` de objeto, consulte [como toouse o armazenamento de tabela do .NET](../cosmos-db/table-storage-how-to-use-dotnet.md). 

## <a id="queues"></a>Tópicos relacionados cobertos por filas de saudação como-tooarticle
Para obter informações sobre como processamento de tabela toohandle disparada por uma mensagem da fila, ou para WebJobs cenários do SDK não específicas tootable processamento, consulte [como toouse Azure fila de armazenamento com hello SDK do WebJobs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

Os tópicos abordados nesse artigo incluem o seguinte hello:

* Funções assíncronas
* Várias instâncias
* Desligamento normal
* Usar atributos de SDK do WebJobs no corpo de saudação de uma função
* Cadeias de conexão do conjunto Olá SDK no código
* Definir valores para parâmetros do construtor do SDK WebJobs no código
* Disparar uma função manualmente
* Gravar logs

## <a id="nextsteps"></a> Próximas etapas
Este guia fornece código exemplos que mostram como os cenários comuns de toohandle para trabalhar com tabelas do Azure. Para obter mais informações sobre como toouse WebJobs do Azure e hello WebJobs SDK, consulte [recursos recomendada do Azure WebJobs](http://go.microsoft.com/fwlink/?linkid=390226).

