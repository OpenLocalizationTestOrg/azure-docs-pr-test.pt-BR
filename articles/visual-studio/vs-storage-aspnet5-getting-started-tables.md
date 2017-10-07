---
title: "aaaHow tooget de Introdução ao armazenamento de tabela e o Visual Studio serviços conectados (ASP.NET Core) | Microsoft Docs"
description: "Como tooget iniciada com o armazenamento de tabela do Azure em um projeto do ASP.NET Core no Visual Studio depois de conectar-se a conta de armazenamento tooa usando o Visual Studio conectada a serviços"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: c3c451d1-71ff-4222-a348-c41c98a02b85
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: e3eb3f3e65456108dd3cde7e3e470f98ba456e35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-started-with-azure-table-storage-and-visual-studio-connected-services"></a>Como tooget iniciada com o armazenamento de tabela do Azure e o Visual Studio serviços conectados
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a>Visão geral
Este artigo descreve como obter iniciado usando a tabela do Azure Olá de armazenamento no Visual Studio depois que você criou ou referenciados de uma conta de armazenamento do Azure em um projeto do ASP.NET Core usando Visual Studio **adicionar serviços conectados** caixa de diálogo.

saudação de serviço de armazenamento de tabela do Azure permite que você toostore grandes quantidades de dados estruturados. serviço de saudação é um repositório de dados NoSQL que aceita chamadas autenticadas de dentro e fora hello nuvem do Azure. As tabelas do Azure são ideais para armazenar dados estruturados não relacionais.

Olá **adicionar serviços conectados** operação instala Olá apropriado NuGet pacotes tooaccess armazenamento do Azure em seu projeto e adiciona a cadeia de caracteres de conexão Olá para hello conta de armazenamento tooyour arquivos de configuração do projeto.

Para obter mais informações sobre como usar o Armazenamento de Tabelas do Azure, consulte [Introdução ao armazenamento de Tabelas do Azure usando o .NET](../storage/storage-dotnet-how-to-use-tables.md).

tooget iniciado, você primeiro precisa toocreate uma tabela em sua conta de armazenamento. Mostraremos como toocreate um Azure tabela no código. Também mostraremos como tabela básica tooperform e operações da entidade, como adicionar, modificar, ler e ler da tabela de entidades. exemplos de saudação são escritos em C\# de código e use Olá biblioteca de cliente de armazenamento do Azure para .NET.

**Observação** -algumas Olá APIs que executam chamadas tooAzure armazenamento no núcleo do ASP.NET são assíncronas. Confira [Programação assíncrona com Async e Await](http://msdn.microsoft.com/library/hh191443.aspx) para saber mais. código de saudação abaixo supõe que os métodos de programação assíncrona estão sendo usados.

## <a name="access-tables-in-code"></a>Acessar tabelas em código
tooaccess tabelas em projetos do ASP.NET Core, é necessário tooinclude Olá seguintes arquivos de origem do itens tooany c# que acessam o armazenamento de tabela do Azure.

1. Certifique-se de declarações de namespace Olá na parte superior de saudação do arquivo hello c# incluem-las **usando** instruções.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. Obtenha um objeto **CloudStorageAccount** que represente as informações da conta de armazenamento. Saudação de uso tooget de código a seguir Olá sua cadeia de caracteres de conexão de armazenamento e as informações de conta de armazenamento da configuração de serviço do Azure de saudação.
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
            CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
   
    **Observação** -Use todos Olá acima código código Olá Olá exemplos a seguir.
3. Obter um **CloudTableClient** tooreference Olá tabela objetos na conta de armazenamento de objeto.  
   
        // Create hello table client.
        CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. Obter um **CloudTable** fazer referência a entidades e objeto tooreference uma tabela específica.
   
        // Get a reference tooa table named "peopleTable"
        CloudTable table = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a>Criar uma tabela em código
Olá toocreate tabela do Azure, basta adicionar uma chamada muito**CreateIfNotExistsAsync()**.

    // Create hello CloudTable if it does not exist
    await table.CreateIfNotExistsAsync();

## <a name="add-an-entity-tooa-table"></a>Adicionar uma tabela de entidade tooa
tooadd uma tabela de tooa de entidade que você criar uma classe que define as propriedades de saudação da entidade. Olá, código a seguir define uma classe de entidade chamada **CustomerEntity** que usa Olá nome do cliente como chave de linha de saudação e último nome como chave de partição hello.

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

Operações de tabela que envolvem entidades são feitas usando Olá **CloudTable** objeto que você criou anteriormente no "Tabelas de acesso no código". Olá **TableOperation** objeto representa Olá operação toobe feito. Olá mostra exemplo de código a seguir como toocreate uma **CloudTable** objeto e um **CustomerEntity** objeto. operação de saudação tooprepare, uma **TableOperation** é criado entidade do cliente Olá tooinsert na tabela de saudação. Por fim, a operação de saudação é executada chamando CloudTable.ExecuteAsync.

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create hello TableOperation that inserts hello customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute hello insert operation.
    await peopleTable.ExecuteAsync(insertOperation);

## <a name="insert-a-batch-of-entities"></a>Inserir um lote de entidades
Você pode inserir várias entidades em uma tabela em uma única operação de gravação. Olá exemplo de código a seguir cria dois objetos de entidade ("Jeff Smith" e "Ben Smith"), adiciona tooa **TableBatchOperation** objeto usando Olá **inserir** método e, em seguida, inicia Olá operação por chamando CloudTable.ExecuteBatchAsync.

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
    TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>().Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

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
Você poderá excluir uma entidade facilmente depois de encontrá-la. Olá código a seguir procura uma entidade customer denominada "Ben Smith" e se encontrá-lo, ele o excluirá.

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

