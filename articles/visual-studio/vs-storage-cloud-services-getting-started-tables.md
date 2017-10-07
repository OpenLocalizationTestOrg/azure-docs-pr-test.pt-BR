---
title: "aaaGet de Introdução ao armazenamento de tabela e o Visual Studio serviços conectados (serviços de nuvem) | Microsoft Docs"
description: "Como tooget iniciado usando o armazenamento de tabela do Azure em um projeto de serviço de nuvem no Visual Studio depois de conectar-se a conta de armazenamento tooa usando o Visual Studio conectada a serviços"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: a3a11ed8-ba7f-4193-912b-e555f5b72184
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 36da6ed4a12a3595e7234482e3040ecee8c33b8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-table-storage-and-visual-studio-connected-services-cloud-services-projects"></a>Introdução ao armazenamento de tabela do Azure e aos serviços conectados do Visual Studio (projetos de serviços de nuvem)
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a>Visão geral
Este artigo descreve como tooget iniciado usando o armazenamento de tabela do Azure no Visual Studio depois que você criou ou referenciado uma conta de armazenamento do Azure em um projeto de serviços de nuvem usando o Visual Studio de saudação **adicionar serviços conectados** caixa de diálogo . Olá **adicionar serviços conectados** operação instala Olá apropriado NuGet pacotes tooaccess armazenamento do Azure em seu projeto e adiciona a cadeia de caracteres de conexão Olá para hello conta de armazenamento tooyour arquivos de configuração do projeto.

saudação de serviço de armazenamento de tabela do Azure permite que você toostore grandes quantidades de dados estruturados. serviço de saudação é um repositório de dados NoSQL que aceita chamadas autenticadas de dentro e fora hello nuvem do Azure. As tabelas do Azure são ideais para armazenar dados estruturados não relacionais.

tooget iniciado, você primeiro precisa toocreate uma tabela em sua conta de armazenamento. Mostraremos como toocreate um Azure tabela no código e como tabela básica tooperform e operações da entidade, como adicionar, modificar, ler e ler da tabela de entidades. exemplos de saudação são escritos em C\# de código e use Olá [biblioteca de cliente de armazenamento do Microsoft Azure para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).

**Observação:** alguns Olá APIs que executam chamadas tooAzure armazenamento são assíncronas. Confira [Programação assíncrona com Async e Await](http://msdn.microsoft.com/library/hh191443.aspx) para saber mais. código de saudação abaixo supõe que os métodos de programação assíncrona estão sendo usados.

* Consulte [Introdução ao Armazenamento de Tabelas do Azure usando .NET](../storage/storage-dotnet-how-to-use-tables.md) para obter mais informações sobre como manipular tabelas com programação.
* Consulte a [Documentação de armazenamento](https://azure.microsoft.com/documentation/services/storage/) para obter informações gerais sobre o armazenamento do Azure.
* Consulte a [documentação de serviços de nuvem](https://azure.microsoft.com/documentation/services/cloud-services/) para obter informações gerais sobre os serviços de nuvem do Azure.
* Consulte [ASP.NET](http://www.asp.net) para obter mais informações sobre como programar aplicativos ASP.NET.

## <a name="access-tables-in-code"></a>Acessar tabelas em código
tooaccess tabelas em projetos de serviço de nuvem, você precisa de saudação tooinclude seguintes arquivos de origem do itens tooany c# que acessam o armazenamento de tabela do Azure.

1. Certifique-se de declarações de namespace Olá na parte superior de saudação do arquivo hello c# incluem-las **usando** instruções.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. Obtenha um objeto **CloudStorageAccount** que represente as informações da conta de armazenamento. Use Olá código tooget Olá conta de armazenamento conexão cadeia de caracteres e o armazenamento de informações a seguir da configuração de serviço do Azure de saudação.
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage account name>
         _AzureStorageConnectionString"));
   > [!NOTE]
   > Use todos Olá acima código código Olá no hello exemplos a seguir.
   > 
   > 
3. Obter um **CloudTableClient** tooreference Olá tabela objetos na conta de armazenamento de objeto.
   
         // Create hello table client.
         CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. Obter um **CloudTable** fazer referência a entidades e objeto tooreference uma tabela específica.
   
        // Get a reference tooa table named "peopleTable".
        CloudTable peopleTable = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a>Criar uma tabela em código
Olá toocreate tabela do Azure, basta adicionar uma chamada muito**CreateIfNotExistsAsync** toohello depois de obter um **CloudTable** conforme descrito na seção de "Tabelas de acesso no código" de saudação do objeto.

    // Create hello CloudTable if it does not exist.
    await peopleTable.CreateIfNotExistsAsync();

## <a name="add-an-entity-tooa-table"></a>Adicionar uma tabela de entidade tooa
tooadd uma tabela de tooa de entidade, crie uma classe que define as propriedades de saudação da entidade. Olá, código a seguir define uma classe de entidade chamada **CustomerEntity** que usa Olá nome do cliente como chave de linha de saudação e sobrenome Olá como chave de partição hello.

    public class CustomerEntity : TableEntity
    {
        public CustomerEntity(string lastName, string firstName)
        {
            this.PartitionKey = lastName;
            this.RowKey = firstName;
        }

        public CustomerEntity() { }

        public string Email { get; set; }

        public string PhoneNumber { get; set; }
    }

Operações de tabela que envolvem entidades são feitas usando Olá **CloudTable** objeto que você criou anteriormente no "Tabelas de acesso no código". Olá **TableOperation** objeto representa Olá operação toobe feito. Olá mostra exemplo de código a seguir como toocreate uma **CloudTable** objeto e um **CustomerEntity** objeto. operação de saudação tooprepare, uma **TableOperation** é criado entidade do cliente Olá tooinsert na tabela de saudação. Por fim, a operação de saudação é executada chamando **CloudTable.ExecuteAsync**.

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create hello TableOperation that inserts hello customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute hello insert operation.
    await peopleTable.ExecuteAsync(insertOperation);


## <a name="insert-a-batch-of-entities"></a>Inserir um lote de entidades
Você pode inserir várias entidades em uma tabela em uma única operação de gravação. Olá exemplo de código a seguir cria dois objetos de entidade ("Jeff Smith" e "Ben Smith"), adiciona tooa **TableBatchOperation** objeto usando Olá método de inserção e, em seguida, inicia Olá operação chamando  **CloudTable.ExecuteBatchAsync**.

    // Create hello batch operation.
    TableBatchOperation batchOperation = new TableBatchOperation();

    // Create a customer entity and add it toohello table.
    CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
    customer1.Email = "Jeff@contoso.com";
    customer1.PhoneNumber = "425-555-0104";

    // Create another customer entity and add it toohello table.
    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.Email = "Ben@contoso.com";
    customer2.PhoneNumber = "425-555-0102";

    // Add both customer entities toohello batch insert operation.
    batchOperation.Insert(customer1);
    batchOperation.Insert(customer2);

    // Execute hello batch operation.
    await peopleTable.ExecuteBatchAsync(batchOperation);

## <a name="get-all-of-hello-entities-in-a-partition"></a>Obter todas as entidades de saudação em uma partição
tooquery uma tabela para todas as entidades de saudação em uma partição, use um **TableQuery** objeto. Olá, exemplo de código a seguir especifica um filtro para entidades onde 'Smith' é a chave de partição hello. Este exemplo imprime campos de saudação de cada entidade no console de toohello de resultados de consulta de saudação.

    // Construct hello query operation for all customer entities where PartitionKey="Smith".
    TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

    // Print hello fields for each customer.
    TableContinuationToken token = null;
    do
    {
        TableQuerySegment<CustomerEntity> resultSegment = await peopleTable.ExecuteQuerySegmentedAsync(query, token);
        token = resultSegment.ContinuationToken;

        foreach (CustomerEntity entity in resultSegment.Results)
        {
            Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
            entity.Email, entity.PhoneNumber);
        }
    } while (token != null);

    return View();


## <a name="get-a-single-entity"></a>Obter uma única entidade
Você pode escrever uma consulta tooget uma entidade única e específica. código a seguir Olá usa um **TableOperation** toospecify um cliente chamado 'Ben Smith' do objeto. Esse método retorna uma única entidade, em vez de uma coleção e Olá retornou o valor em **TableResult.Result** é um **CustomerEntity** objeto. Especificar chaves de partição e de linha em uma consulta é tooretrieve de maneira mais rápida de saudação uma única entidade de saudação **tabela** serviço.

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print hello phone number of hello result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("hello phone number could not be retrieved.");

## <a name="delete-an-entity"></a>Excluir uma entidade
Você poderá excluir uma entidade facilmente depois de encontrá-la. Hello código a seguir procura uma entidade customer denominada "Ben Smith" e, se encontrá-lo, ele o excluirá.

    // Create a retrieve operation that expects a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello operation.
    TableResult retrievedResult = peopleTable.Execute(retrieveOperation);

    // Assign hello result tooa CustomerEntity object.
    CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

    // Create hello Delete TableOperation and then execute it.
    if (deleteEntity != null)
    {
       TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

       // Execute hello operation.
       await peopleTable.ExecuteAsync(deleteOperation);

       Console.WriteLine("Entity deleted.");
    }

    else
       Console.WriteLine("Couldn't delete hello entity.");

## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

