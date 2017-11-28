---
title: Como usar o Armazenamento de Tabelas do Java | Microsoft Docs
description: "Armazene dados estruturados na nuvem usando o Armazenamento de Tabelas do Azure, um repositório de dados NoSQL."
services: storage
documentationcenter: java
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 45145189-e67f-4ca6-b15d-43af7bfd3f97
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: a4d6f144cc6940ffe2b2c6f27553cd7aa3bcb381
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-table-storage-from-java"></a><span data-ttu-id="fa199-103">Como usar o Armazenamento de Tabela do Java</span><span class="sxs-lookup"><span data-stu-id="fa199-103">How to use Table storage from Java</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="fa199-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="fa199-104">Overview</span></span>
<span data-ttu-id="fa199-105">Este guia mostra como executar cenários comuns usando o serviço de Armazenamento de Tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="fa199-105">This guide will show you how to perform common scenarios using the Azure Table storage service.</span></span> <span data-ttu-id="fa199-106">As amostras são escritas em Java e usam o [SDK de Armazenamento do Azure para Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="fa199-106">The samples are written in Java and use the [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="fa199-107">Os cenários abrangidos incluem **criar**, **listar** e **excluir** tabelas, além de **inserir**, **consultar**, **modificar** e **excluir** entidades em uma tabela.</span><span class="sxs-lookup"><span data-stu-id="fa199-107">The scenarios covered include **creating**, **listing**, and **deleting** tables, as well as **inserting**, **querying**, **modifying**, and **deleting** entities in a table.</span></span> <span data-ttu-id="fa199-108">Para obter mais informações sobre tabelas, consulte a seção [Próximas etapas](#Next-Steps) .</span><span class="sxs-lookup"><span data-stu-id="fa199-108">For more information on tables, see the [Next steps](#Next-Steps) section.</span></span>

<span data-ttu-id="fa199-109">Observação: um SDK está disponível para os desenvolvedores que usam o Armazenamento do Azure em dispositivos Android.</span><span class="sxs-lookup"><span data-stu-id="fa199-109">Note: An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="fa199-110">Para obter mais informações, consulte [Azure Storage SDK for Android][Azure Storage SDK for Android] (SDK de Armazenamento do Azure para Android).</span><span class="sxs-lookup"><span data-stu-id="fa199-110">For more information, see the [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="fa199-111">Criar um aplicativo Java</span><span class="sxs-lookup"><span data-stu-id="fa199-111">Create a Java application</span></span>
<span data-ttu-id="fa199-112">Neste guia, você usará os recursos de armazenamento que podem ser executados em um aplicativo Java localmente ou no código em execução em uma função web ou de trabalho do Azure.</span><span class="sxs-lookup"><span data-stu-id="fa199-112">In this guide, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="fa199-113">Para isso, você precisará instalar o JDK (Java Development Kit) e criar uma conta de armazenamento do Azure na sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="fa199-113">To do so, you will need to install the Java Development Kit (JDK) and create an Azure storage account in your Azure subscription.</span></span> <span data-ttu-id="fa199-114">Depois disso, você precisará verificar se o sistema de desenvolvimento atende aos requisitos mínimos e às dependências listadas no repositório [Microsoft Azure Storage SDK for Java][Azure Storage SDK for Java] (SDK de Armazenamento do Microsoft Azure para Java) no GitHub.</span><span class="sxs-lookup"><span data-stu-id="fa199-114">Once you have done so, you will need to verify that your development system meets the minimum requirements and dependencies which are listed in the [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="fa199-115">Se o seu sistema atender a esses requisitos, você poderá seguir as instruções para baixar e instalar as Bibliotecas de Armazenamento do Azure para Java em seu sistema por meio desse repositório.</span><span class="sxs-lookup"><span data-stu-id="fa199-115">If your system meets those requirements, you can follow the instructions for downloading and installing the Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="fa199-116">Depois de concluir essas tarefas, você poderá criar um aplicativo Java que usa os exemplos neste artigo.</span><span class="sxs-lookup"><span data-stu-id="fa199-116">Once you have completed those tasks, you will be able to create a Java application which uses the examples in this article.</span></span>

## <a name="configure-your-application-to-access-table-storage"></a><span data-ttu-id="fa199-117">Configurar seu aplicativo para acessar o armazenamento de tabelas</span><span class="sxs-lookup"><span data-stu-id="fa199-117">Configure your application to access table storage</span></span>
<span data-ttu-id="fa199-118">Adicione as seguintes instruções de importação na parte superior do arquivo Java em que deseja usar as APIs de armazenamento do Microsoft Azure para acessar tabelas:</span><span class="sxs-lookup"><span data-stu-id="fa199-118">Add the following import statements to the top of the Java file where you want to use Microsoft Azure storage APIs to access tables:</span></span>

```java
// Include the following imports to use table APIs
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.table.*;
import com.microsoft.azure.storage.table.TableQuery.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="fa199-119">Configurar uma cadeia de conexão de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="fa199-119">Set up an Azure storage connection string</span></span>
<span data-ttu-id="fa199-120">Um cliente de armazenamento do Azure usa uma cadeia de conexão para armazenar pontos de extremidade e credenciais para acessar serviços de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="fa199-120">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="fa199-121">Ao executar um aplicativo cliente, é necessário fornecer a cadeia de conexão de armazenamento no formato a seguir, usando o nome de sua conta de armazenamento e a tecla de Acesso primário da conta de armazenamento listada no [portal do Azure](https://portal.azure.com) para os valores *AccountName* e *AccountKey*.</span><span class="sxs-lookup"><span data-stu-id="fa199-121">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the Primary access key for the storage account listed in the [Azure portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="fa199-122">Este exemplo mostra como você pode declarar um campo estático para armazenar a cadeia de conexão:</span><span class="sxs-lookup"><span data-stu-id="fa199-122">This example shows how you can declare a static field to hold the connection string:</span></span>

```java
// Define the connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="fa199-123">Em um aplicativo que esteja sendo executado em uma função no Microsoft Azure, essa cadeia pode ser armazenada no arquivo de configuração do serviço, *ServiceConfiguration.cscfg*, podendo ser acessada com uma chamada para o método **RoleEnvironment.getConfigurationSettings** .</span><span class="sxs-lookup"><span data-stu-id="fa199-123">In an application running within a role in Microsoft Azure, this string can be stored in the service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call to the **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="fa199-124">Segue um exemplo de como obter a cadeia de conexão de um elemento **Setting** denominado *StorageConnectionString* no arquivo de configuração de serviço:</span><span class="sxs-lookup"><span data-stu-id="fa199-124">Here's an example of getting the connection string from a **Setting** element named *StorageConnectionString* in the service configuration file:</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="fa199-125">Os exemplos abaixo pressupõem que você usou um desses dois métodos para obter a cadeia de conexão do armazenamento.</span><span class="sxs-lookup"><span data-stu-id="fa199-125">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>

## <a name="how-to-create-a-table"></a><span data-ttu-id="fa199-126">Como: criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="fa199-126">How to: Create a table</span></span>
<span data-ttu-id="fa199-127">Um objeto **CloudTableClient** permite obter os objetos de referência para tabelas e entidades.</span><span class="sxs-lookup"><span data-stu-id="fa199-127">A **CloudTableClient** object lets you get reference objects for tables and entities.</span></span> <span data-ttu-id="fa199-128">O código a seguir cria um objeto **CloudTableClient** e o usa para criar um novo objeto **CloudTable**, o qual representa uma tabela nomeada "pessoas".</span><span class="sxs-lookup"><span data-stu-id="fa199-128">The following code creates a **CloudTableClient** object and uses it to create a new **CloudTable** object which represents a table named "people".</span></span> <span data-ttu-id="fa199-129">(Observação: existem outras maneiras de criar objetos **CloudStorageAccount**. Para saber mais, veja **CloudStorageAccount** na [Referência de SDK do cliente de armazenamento do Azure]).</span><span class="sxs-lookup"><span data-stu-id="fa199-129">(Note: There are additional ways to create **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in the [Azure Storage Client SDK Reference].)</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create the table if it doesn't exist.
    String tableName = "people";
    CloudTable cloudTable = tableClient.getTableReference(tableName);
    cloudTable.createIfNotExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-the-tables"></a><span data-ttu-id="fa199-130">Como: listar as tabelas</span><span class="sxs-lookup"><span data-stu-id="fa199-130">How to: List the tables</span></span>
<span data-ttu-id="fa199-131">Para obter uma lista de tabelas, chame o método **CloudTableClient.listTables()** para recuperar uma lista iterável de nomes de tabela.</span><span class="sxs-lookup"><span data-stu-id="fa199-131">To get a list of tables, call the **CloudTableClient.listTables()** method to retrieve an iterable list of table names.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Loop through the collection of table names.
    for (String table : tableClient.listTables())
    {
        // Output each table name.
        System.out.println(table);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-an-entity-to-a-table"></a><span data-ttu-id="fa199-132">Como: adicionar uma entidade a uma tabela</span><span class="sxs-lookup"><span data-stu-id="fa199-132">How to: Add an entity to a table</span></span>
<span data-ttu-id="fa199-133">As entidades mapeiam para os objetos do Java que usam uma classe personalizada, implementando **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="fa199-133">Entities map to Java objects using a custom class implementing **TableEntity**.</span></span> <span data-ttu-id="fa199-134">Para sua conveniência, a classe **TableServiceEntity** implementa **TableEntity** e usa reflexão para mapear as propriedades para os métodos getter e setter nomeados para as propriedades.</span><span class="sxs-lookup"><span data-stu-id="fa199-134">For convenience, the **TableServiceEntity** class implements **TableEntity** and uses reflection to map properties to getter and setter methods named for the properties.</span></span> <span data-ttu-id="fa199-135">Para adicionar uma entidade a uma tabela, primeiro crie uma classe que defina as propriedades da sua entidade.</span><span class="sxs-lookup"><span data-stu-id="fa199-135">To add an entity to a table, first create a class that defines the properties of your entity.</span></span> <span data-ttu-id="fa199-136">O código a seguir define uma classe de entidade que usa o nome do cliente como a chave de linha e o sobrenome como a chave de partição.</span><span class="sxs-lookup"><span data-stu-id="fa199-136">The following code defines an entity class which uses the customer's first name as the row key, and last name as the partition key.</span></span> <span data-ttu-id="fa199-137">Juntas, uma chave de partição e uma chave de linha identificam exclusivamente a entidade na tabela.</span><span class="sxs-lookup"><span data-stu-id="fa199-137">Together, an entity's partition and row key uniquely identify the entity in the table.</span></span> <span data-ttu-id="fa199-138">As entidades com a mesma chave de partição podem ser consultadas mais rápido do que aquelas com chaves de partição diferentes.</span><span class="sxs-lookup"><span data-stu-id="fa199-138">Entities with the same partition key can be queried faster than those with different partition keys.</span></span>

```java
public class CustomerEntity extends TableServiceEntity {
    public CustomerEntity(String lastName, String firstName) {
        this.partitionKey = lastName;
        this.rowKey = firstName;
    }

    public CustomerEntity() { }

    String email;
    String phoneNumber;

    public String getEmail() {
        return this.email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public String getPhoneNumber() {
        return this.phoneNumber;
    }

    public void setPhoneNumber(String phoneNumber) {
        this.phoneNumber = phoneNumber;
    }
}
```

<span data-ttu-id="fa199-139">As operações de tabela que envolvem entidades exigem umobjeto **TableOperation** .</span><span class="sxs-lookup"><span data-stu-id="fa199-139">Table operations involving entities require a **TableOperation** object.</span></span> <span data-ttu-id="fa199-140">Este objeto define a operação a ser realizada em uma entidade, que pode ser executada com um objeto **CloudTable** .</span><span class="sxs-lookup"><span data-stu-id="fa199-140">This object defines the operation to be performed on an entity, which can be executed with a **CloudTable** object.</span></span> <span data-ttu-id="fa199-141">O código a seguir cria uma nova instância da classe **CustomerEntity** com alguns dados do cliente que serão armazenados.</span><span class="sxs-lookup"><span data-stu-id="fa199-141">The following code creates a new instance of the **CustomerEntity** class with some customer data to be stored.</span></span> <span data-ttu-id="fa199-142">O próximo código chama **TableOperation.insertOrReplace** para criar um objeto **TableOperation** para inserir uma entidade em uma tabela e associa a nova **CustomerEntity** a ele.</span><span class="sxs-lookup"><span data-stu-id="fa199-142">The code next calls **TableOperation.insertOrReplace** to create a **TableOperation** object to insert an entity into a table, and associates the new **CustomerEntity** with it.</span></span> <span data-ttu-id="fa199-143">Por fim, o código chama o método **execute** no objeto **CloudTable**, especificando a tabela “pessoas" e a nova **TableOperation**, que envia uma solicitação para o serviço de armazenamento para inserir a nova entidade de cliente na tabela “pessoas” ou substituir a entidade se ela já existir.</span><span class="sxs-lookup"><span data-stu-id="fa199-143">Finally, the code calls the **execute** method on the **CloudTable** object, specifying the "people" table and the new **TableOperation**, which then sends a request to the storage service to insert the new customer entity into the "people" table, or replace the entity if it already exists.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.setEmail("Walter@contoso.com");
    customer1.setPhoneNumber("425-555-0101");

    // Create an operation to add the new customer to the people table.
    TableOperation insertCustomer1 = TableOperation.insertOrReplace(customer1);

    // Submit the operation to the table service.
    cloudTable.execute(insertCustomer1);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-a-batch-of-entities"></a><span data-ttu-id="fa199-144">Como: inserir um lote de entidades</span><span class="sxs-lookup"><span data-stu-id="fa199-144">How to: Insert a batch of entities</span></span>
<span data-ttu-id="fa199-145">Você pode inserir um lote de entidades ao serviço Tabela em uma operação de gravação.</span><span class="sxs-lookup"><span data-stu-id="fa199-145">You can insert a batch of entities to the table service in one write operation.</span></span> <span data-ttu-id="fa199-146">O código a seguir cria um objeto **TableBatchOperation** e adiciona três operações de inserção a ele.</span><span class="sxs-lookup"><span data-stu-id="fa199-146">The following code creates a **TableBatchOperation** object, then adds three insert operations to it.</span></span> <span data-ttu-id="fa199-147">Cada operação de inserção é adicionada criando um novo objeto de entidade, definindo seus valores e, em seguida, chamando o método **insert** no objeto **TableBatchOperation** para associar a entidade a uma nova operação de inserção.</span><span class="sxs-lookup"><span data-stu-id="fa199-147">Each insert operation is added by creating a new entity object, setting its values, and then calling the **insert** method on the **TableBatchOperation** object to associate the entity with a new insert operation.</span></span> <span data-ttu-id="fa199-148">Em seguida, o código chama **execute** no objeto **CloudTable**, especificando a tabela “pessoas" e o objeto **TableBatchOperation**, que envia o lote de operações da tabela para o serviço de armazenamento em uma única solicitação.</span><span class="sxs-lookup"><span data-stu-id="fa199-148">Then the code calls **execute** on the **CloudTable** object, specifying the "people" table and the **TableBatchOperation** object, which sends the batch of table operations to the storage service in a single request.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Define a batch operation.
    TableBatchOperation batchOperation = new TableBatchOperation();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a customer entity to add to the table.
    CustomerEntity customer = new CustomerEntity("Smith", "Jeff");
    customer.setEmail("Jeff@contoso.com");
    customer.setPhoneNumber("425-555-0104");
    batchOperation.insertOrReplace(customer);

    // Create another customer entity to add to the table.
    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.setEmail("Ben@contoso.com");
    customer2.setPhoneNumber("425-555-0102");
    batchOperation.insertOrReplace(customer2);

    // Create a third customer entity to add to the table.
    CustomerEntity customer3 = new CustomerEntity("Smith", "Denise");
    customer3.setEmail("Denise@contoso.com");
    customer3.setPhoneNumber("425-555-0103");
    batchOperation.insertOrReplace(customer3);

    // Execute the batch of operations on the "people" table.
    cloudTable.execute(batchOperation);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="fa199-149">Algumas outras observações sobre as operações em lote:</span><span class="sxs-lookup"><span data-stu-id="fa199-149">Some things to note on batch operations:</span></span>

* <span data-ttu-id="fa199-150">Você pode executar até 100 operações de inserção, exclusão, mesclagem, substituição, inserção ou mesclagem e inserção ou substituição em qualquer combinação em um único lote.</span><span class="sxs-lookup"><span data-stu-id="fa199-150">You can perform up to 100 insert, delete, merge, replace, insert or merge, and insert or replace operations in any combination in a single batch.</span></span>
* <span data-ttu-id="fa199-151">Uma operação em lote pode ter uma operação de recuperação se ela for a única operação no lote.</span><span class="sxs-lookup"><span data-stu-id="fa199-151">A batch operation can have a retrieve operation, if it is the only operation in the batch.</span></span>
* <span data-ttu-id="fa199-152">Todas as entidades em uma única operação em lote devem ter a mesma chave de partição.</span><span class="sxs-lookup"><span data-stu-id="fa199-152">All entities in a single batch operation must have the same partition key.</span></span>
* <span data-ttu-id="fa199-153">Uma operação em lote está limitada a uma carga de dados de 4 MB.</span><span class="sxs-lookup"><span data-stu-id="fa199-153">A batch operation is limited to a 4MB data payload.</span></span>

## <a name="how-to-retrieve-all-entities-in-a-partition"></a><span data-ttu-id="fa199-154">Como recuperar todas as entidades em uma partição</span><span class="sxs-lookup"><span data-stu-id="fa199-154">How to: Retrieve all entities in a partition</span></span>
<span data-ttu-id="fa199-155">Para consultar uma tabela de todas as entidades em uma partição, use **TableQuery**.</span><span class="sxs-lookup"><span data-stu-id="fa199-155">To query a table for entities in a partition, you can use a **TableQuery**.</span></span> <span data-ttu-id="fa199-156">Chame **TableQuery.from** para criar uma consulta em uma determinada tabela que retorna um tipo de resultado especificado.</span><span class="sxs-lookup"><span data-stu-id="fa199-156">Call **TableQuery.from** to create a query on a particular table that returns a specified result type.</span></span> <span data-ttu-id="fa199-157">O código a seguir especifica um filtro para entidades onde 'Smith' é a chave da partição.</span><span class="sxs-lookup"><span data-stu-id="fa199-157">The following code specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="fa199-158">**TableQuery.generateFilterCondition** é um método auxiliar para criar filtros para consultas.</span><span class="sxs-lookup"><span data-stu-id="fa199-158">**TableQuery.generateFilterCondition** is a helper method to create filters for queries.</span></span> <span data-ttu-id="fa199-159">Chame **where** na referência retornada pelo método **TableQuery.from** para aplicar o filtro à consulta.</span><span class="sxs-lookup"><span data-stu-id="fa199-159">Call **where** on the reference returned by the **TableQuery.from** method to apply the filter to the query.</span></span> <span data-ttu-id="fa199-160">Quando a chamada é executada com uma chamada para **execute** no objeto **CloudTable**, ela retorna um **Iterator** com o tipo de resultado **CustomerEntity** especificado.</span><span class="sxs-lookup"><span data-stu-id="fa199-160">When the query is executed with a call to **execute** on the **CloudTable** object, it returns an **Iterator** with the **CustomerEntity** result type specified.</span></span> <span data-ttu-id="fa199-161">Com isso, você pode usar o **Iterator** retornado em cada loop para consumir os resultados.</span><span class="sxs-lookup"><span data-stu-id="fa199-161">You can then use the **Iterator** returned in a for each loop to consume the results.</span></span> <span data-ttu-id="fa199-162">Esse código imprime os campos de cada entidade nos resultados da consulta no console.</span><span class="sxs-lookup"><span data-stu-id="fa199-162">This code prints the fields of each entity in the query results to the console.</span></span>

```java
try
{
    // Define constants for filters.
    final String PARTITION_KEY = "PartitionKey";
    final String ROW_KEY = "RowKey";
    final String TIMESTAMP = "Timestamp";

    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where the partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Specify a partition query, using "Smith" as the partition key filter.
    TableQuery<CustomerEntity> partitionQuery =
        TableQuery.from(CustomerEntity.class)
        .where(partitionFilter);

    // Loop through the results, displaying information about the entity.
    for (CustomerEntity entity : cloudTable.execute(partitionQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="fa199-163">Como: recuperar um intervalo de entidades em uma partição</span><span class="sxs-lookup"><span data-stu-id="fa199-163">How to: Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="fa199-164">Se não desejar consultar todas as entidades em uma partição, você poderá especificar um intervalo, usando as operações de comparação em um filtro.</span><span class="sxs-lookup"><span data-stu-id="fa199-164">If you don't want to query all the entities in a partition, you can specify a range by using comparison operators in a filter.</span></span> <span data-ttu-id="fa199-165">O código a seguir combina dois filtros para obter todas as entidades na partição "Smith", onde a chave de linha (nome) começa com uma letra até a letra 'E' do alfabeto.</span><span class="sxs-lookup"><span data-stu-id="fa199-165">The following code combines two filters to get all entities in partition "Smith" where the row key (first name) starts with a letter up to 'E' in the alphabet.</span></span> <span data-ttu-id="fa199-166">Em seguida, eleimprime os resultados da consulta.</span><span class="sxs-lookup"><span data-stu-id="fa199-166">Then it prints the query results.</span></span> <span data-ttu-id="fa199-167">Se você usar as entidades adicionadas à tabela na seção de inserção do lote deste guia, apenas duas entidades serão retornadas desta vez (Ben e Denise Smith); Jeff Smith não será incluído.</span><span class="sxs-lookup"><span data-stu-id="fa199-167">If you use the entities added to the table in the batch insert section of this guide, only two entities are returned this time (Ben and Denise Smith); Jeff Smith is not included.</span></span>

```java
try
{
    // Define constants for filters.
    final String PARTITION_KEY = "PartitionKey";
    final String ROW_KEY = "RowKey";
    final String TIMESTAMP = "Timestamp";

    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where the partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Create a filter condition where the row key is less than the letter "E".
    String rowFilter = TableQuery.generateFilterCondition(
        ROW_KEY,
        QueryComparisons.LESS_THAN,
        "E");

    // Combine the two conditions into a filter expression.
    String combinedFilter = TableQuery.combineFilters(partitionFilter,
        Operators.AND, rowFilter);

    // Specify a range query, using "Smith" as the partition key,
    // with the row key being up to the letter "E".
    TableQuery<CustomerEntity> rangeQuery =
        TableQuery.from(CustomerEntity.class)
        .where(combinedFilter);

    // Loop through the results, displaying information about the entity
    for (CustomerEntity entity : cloudTable.execute(rangeQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-single-entity"></a><span data-ttu-id="fa199-168">Como: recuperar uma única entidade</span><span class="sxs-lookup"><span data-stu-id="fa199-168">How to: Retrieve a single entity</span></span>
<span data-ttu-id="fa199-169">Você pode escrever uma consulta para recuperar uma entidade única e específica.</span><span class="sxs-lookup"><span data-stu-id="fa199-169">You can write a query to retrieve a single, specific entity.</span></span> <span data-ttu-id="fa199-170">O código a seguir chama **TableOperation.retrieve** com uma chave de partição e parâmetros da chave de linha para especificar o cliente "Jeff Smith", em vez de criar uma **TableQuery** e usar filtros para executar a mesma tarefa.</span><span class="sxs-lookup"><span data-stu-id="fa199-170">The following code calls **TableOperation.retrieve** with partition key and row key parameters to specify the customer "Jeff Smith", instead of creating a **TableQuery** and using filters to do the same thing.</span></span> <span data-ttu-id="fa199-171">Quando executada, a operação de recuperação retorna apenas uma entidade, em vez de uma coleção.</span><span class="sxs-lookup"><span data-stu-id="fa199-171">When executed, the retrieve operation returns just one entity, rather than a collection.</span></span> <span data-ttu-id="fa199-172">O método **getResultAsType** converte o resultado para o tipo de destino da atribuição, um objeto **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="fa199-172">The **getResultAsType** method casts the result to the type of the assignment target, a **CustomerEntity** object.</span></span> <span data-ttu-id="fa199-173">Se esse tipo não for compatível com o tipo especificado na consulta, uma exceção será lançada.</span><span class="sxs-lookup"><span data-stu-id="fa199-173">If this type is not compatible with the type specified for the query, an exception will be thrown.</span></span> <span data-ttu-id="fa199-174">Um valor nulo será retornado se nenhuma entidade tiver uma correspondência exata de chave de partição e chave de linha.</span><span class="sxs-lookup"><span data-stu-id="fa199-174">A null value is returned if no entity has an exact partition and row key match.</span></span> <span data-ttu-id="fa199-175">Especificar chaves de partição e de linha em uma consulta é a maneira mais rápida de recuperar uma única entidade de serviço Table.</span><span class="sxs-lookup"><span data-stu-id="fa199-175">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the Table service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve the entity with partition key of "Smith" and row key of "Jeff"
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit the operation to the table service and get the specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Output the entity.
    if (specificEntity != null)
    {
        System.out.println(specificEntity.getPartitionKey() +
            " " + specificEntity.getRowKey() +
            "\t" + specificEntity.getEmail() +
            "\t" + specificEntity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-modify-an-entity"></a><span data-ttu-id="fa199-176">Como modificar uma entidade</span><span class="sxs-lookup"><span data-stu-id="fa199-176">How to: Modify an entity</span></span>
<span data-ttu-id="fa199-177">Para modificar uma entidade, recupere-a do serviço Tabela, altere o objeto de entidade e, em seguida, salve as alterações novamente no serviço Tabela com uma operação de substituição ou mesclagem.</span><span class="sxs-lookup"><span data-stu-id="fa199-177">To modify an entity, retrieve it from the table service, make changes to the entity object, and save the changes back to the table service with a replace or merge operation.</span></span> <span data-ttu-id="fa199-178">O código a seguir altera o número de telefone de um cliente existente.</span><span class="sxs-lookup"><span data-stu-id="fa199-178">The following code changes an existing customer's phone number.</span></span> <span data-ttu-id="fa199-179">Em vez de chamar **TableOperation.insert**como fizemos para inserir, esse código chama **TableOperation.replace**.</span><span class="sxs-lookup"><span data-stu-id="fa199-179">Instead of calling **TableOperation.insert** like we did to insert, this code calls **TableOperation.replace**.</span></span> <span data-ttu-id="fa199-180">O método **CloudTableClient.execute** chamará o serviço Tabela e a entidade será atualizada, a menos que outro aplicativo a tenha alterado desde o momento em que ela foi recuperada por esse aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fa199-180">The **CloudTable.execute** method calls the table service, and the entity is replaced, unless another application changed it in the time since this application retrieved it.</span></span> <span data-ttu-id="fa199-181">Quando isso acontece, uma exceção é lançada e a entidade deve ser recuperada, modificada e salva novamente.</span><span class="sxs-lookup"><span data-stu-id="fa199-181">When that happens, an exception is thrown, and the entity must be retrieved, modified, and saved again.</span></span> <span data-ttu-id="fa199-182">Esse padrão de repetição de simultaneidade otimista é comum em um sistema de armazenamento distribuído.</span><span class="sxs-lookup"><span data-stu-id="fa199-182">This optimistic concurrency retry pattern is common in a distributed storage system.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve the entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit the operation to the table service and get the specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Specify a new phone number.
    specificEntity.setPhoneNumber("425-555-0105");

    // Create an operation to replace the entity.
    TableOperation replaceEntity = TableOperation.replace(specificEntity);

    // Submit the operation to the table service.
    cloudTable.execute(replaceEntity);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-query-a-subset-of-entity-properties"></a><span data-ttu-id="fa199-183">Como: consultar um subconjunto de propriedades de entidade</span><span class="sxs-lookup"><span data-stu-id="fa199-183">How to: Query a subset of entity properties</span></span>
<span data-ttu-id="fa199-184">Uma consulta a uma tabela pode recuperar apenas algumas propriedades de uma entidade.</span><span class="sxs-lookup"><span data-stu-id="fa199-184">A query to a table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="fa199-185">Essa técnica, chamada projeção, reduz a largura de banda e pode melhorar o desempenho da consulta, principalmente para grandes entidades.</span><span class="sxs-lookup"><span data-stu-id="fa199-185">This technique, called projection, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="fa199-186">A consulta no código a seguir usa o método **select** para retornar apenas os endereços de e-mail das entidades na tabela.</span><span class="sxs-lookup"><span data-stu-id="fa199-186">The query in the following code uses the **select** method to return only the email addresses of entities in the table.</span></span> <span data-ttu-id="fa199-187">Os resultados são projetados em um coleção de **String** com a ajuda de um **EntityResolver**, que faz a conversão de tipo nas entidades retornadas do servidor.</span><span class="sxs-lookup"><span data-stu-id="fa199-187">The results are projected into a collection of **String** with the help of an **EntityResolver**, which does the type conversion on the entities returned from the server.</span></span> <span data-ttu-id="fa199-188">Saiba mais sobre projeção em [Microsoft Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection] (Tabelas do Microsoft Azure: Apresentando a projeção de upsert e de consulta).</span><span class="sxs-lookup"><span data-stu-id="fa199-188">You can learn more about projection in [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span></span> <span data-ttu-id="fa199-189">Observe que a projeção não é compatível com o emulador de armazenamento local, portanto, esse código é executado somente ao usar uma conta no serviço tabela.</span><span class="sxs-lookup"><span data-stu-id="fa199-189">Note that projection is not supported on the local storage emulator, so this code runs only when using an account on the table service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Define a projection query that retrieves only the Email property
    TableQuery<CustomerEntity> projectionQuery =
        TableQuery.from(CustomerEntity.class)
        .select(new String[] {"Email"});

    // Define a Entity resolver to project the entity to the Email value.
    EntityResolver<String> emailResolver = new EntityResolver<String>() {
        @Override
        public String resolve(String PartitionKey, String RowKey, Date timeStamp, HashMap<String, EntityProperty> properties, String etag) {
            return properties.get("Email").getValueAsString();
        }
    };

    // Loop through the results, displaying the Email values.
    for (String projectedString :
        cloudTable.execute(projectionQuery, emailResolver)) {
            System.out.println(projectedString);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-or-replace-an-entity"></a><span data-ttu-id="fa199-190">Como: inserir ou substituir uma entidade</span><span class="sxs-lookup"><span data-stu-id="fa199-190">How to: Insert or Replace an entity</span></span>
<span data-ttu-id="fa199-191">Em geral, você deseja adicionar uma entidade a uma tabela sem saber se ela já existe na tabela.</span><span class="sxs-lookup"><span data-stu-id="fa199-191">Often you want to add an entity to a table without knowing if it already exists in the table.</span></span> <span data-ttu-id="fa199-192">Uma operação de inserção ou substituição permite que você faça uma única solicitação para inserir a entidade, se ela não existir, ou para substituir a entidade existente, se ela existir.</span><span class="sxs-lookup"><span data-stu-id="fa199-192">An insert-or-replace operation allows you to make a single request which will insert the entity if it does not exist or replace the existing one if it does.</span></span> <span data-ttu-id="fa199-193">Com base nos exemplos anteriores, o código a seguir insere ou substitui a entidade para "Walter Harp".</span><span class="sxs-lookup"><span data-stu-id="fa199-193">Building on prior examples, the following code inserts or replaces the entity for "Walter Harp".</span></span> <span data-ttu-id="fa199-194">Depois de criar uma nova entidade, esse código chamará o método **TableOperation.insertOrReplace** .</span><span class="sxs-lookup"><span data-stu-id="fa199-194">After creating a new entity, this code calls the **TableOperation.insertOrReplace** method.</span></span> <span data-ttu-id="fa199-195">Em seguida, esse código chamará **execute** no objeto **CloudTable** com a tabela e a operação de inserção ou substituição de tabela como os parâmetros.</span><span class="sxs-lookup"><span data-stu-id="fa199-195">This code then calls **execute** on the **CloudTable** object with the table and the insert or replace table operation as the parameters.</span></span> <span data-ttu-id="fa199-196">Para atualizar somente parte de uma entidade, o método **TableOperation.insertOrMerge** pode ser usado em vez disso.</span><span class="sxs-lookup"><span data-stu-id="fa199-196">To update only part of an entity, the **TableOperation.insertOrMerge** method can be used instead.</span></span> <span data-ttu-id="fa199-197">Observe que inserir ou substituir não tem suporte com o emulador de armazenamento local, portanto, esse código é executado somente ao usar uma conta no serviço tabela.</span><span class="sxs-lookup"><span data-stu-id="fa199-197">Note that insert-or-replace is not supported on the local storage emulator, so this code runs only when using an account on the table service.</span></span> <span data-ttu-id="fa199-198">Saiba mais sobre inserção ou substituição e inserção ou mesclagem em [Microsoft Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection] (Tabelas do Microsoft Azure: Apresentando a projeção de upsert e de consulta).</span><span class="sxs-lookup"><span data-stu-id="fa199-198">You can learn more about insert-or-replace and insert-or-merge in this [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer5 = new CustomerEntity("Harp", "Walter");
    customer5.setEmail("Walter@contoso.com");
    customer5.setPhoneNumber("425-555-0106");

    // Create an operation to add the new customer to the people table.
    TableOperation insertCustomer5 = TableOperation.insertOrReplace(customer5);

    // Submit the operation to the table service.
    cloudTable.execute(insertCustomer5);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-an-entity"></a><span data-ttu-id="fa199-199">Como excluir uma entidade</span><span class="sxs-lookup"><span data-stu-id="fa199-199">How to: Delete an entity</span></span>
<span data-ttu-id="fa199-200">Você poderá excluir uma entidade facilmente depois que recuperá-la.</span><span class="sxs-lookup"><span data-stu-id="fa199-200">You can easily delete an entity after you have retrieved it.</span></span> <span data-ttu-id="fa199-201">Depois que a entidade for recuperada, chame **TableOperation.delete** com a entidade a excluir.</span><span class="sxs-lookup"><span data-stu-id="fa199-201">Once the entity is retrieved, call **TableOperation.delete** with the entity to delete.</span></span> <span data-ttu-id="fa199-202">Em seguida, chame **execute** no objeto **CloudTable**.</span><span class="sxs-lookup"><span data-stu-id="fa199-202">Then call **execute** on the **CloudTable** object.</span></span> <span data-ttu-id="fa199-203">O código a seguir recupera e exclui uma entidade de cliente.</span><span class="sxs-lookup"><span data-stu-id="fa199-203">The following code retrieves and deletes a customer entity.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create an operation to retrieve the entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff = TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Retrieve the entity with partition key of "Smith" and row key of "Jeff".
    CustomerEntity entitySmithJeff =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Create an operation to delete the entity.
    TableOperation deleteSmithJeff = TableOperation.delete(entitySmithJeff);

    // Submit the delete operation to the table service.
    cloudTable.execute(deleteSmithJeff);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-table"></a><span data-ttu-id="fa199-204">Como excluir uma tabela</span><span class="sxs-lookup"><span data-stu-id="fa199-204">How to: Delete a table</span></span>
<span data-ttu-id="fa199-205">Finalmente, o código a seguir excluirá uma tabela de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="fa199-205">Finally, the following code deletes a table from a storage account.</span></span> <span data-ttu-id="fa199-206">Uma tabela que tenha sido excluída não estará disponível para ser recriada por um período de tempo após a exclusão, geralmente menos de 40 segundos.</span><span class="sxs-lookup"><span data-stu-id="fa199-206">A table which has been deleted will be unavailable to be recreated for a period of time following the deletion, usually less than forty seconds.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Delete the table and all its data if it exists.
    CloudTable cloudTable = tableClient.getTableReference("people");
    cloudTable.deleteIfExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```
[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="next-steps"></a><span data-ttu-id="fa199-207">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fa199-207">Next steps</span></span>

* <span data-ttu-id="fa199-208">[O Gerenciador de Armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) é um aplicativo autônomo e gratuito da Microsoft que possibilita o trabalho visual com os dados do Armazenamento do Azure no Windows, MacOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="fa199-208">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="fa199-209">[Microsoft Azure Storage SDK for Java][Azure Storage SDK for Java] (SDK de Armazenamento do Microsoft Azure para Java)</span><span class="sxs-lookup"><span data-stu-id="fa199-209">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="fa199-210">[Referência de SDK do cliente de armazenamento do Azure][Referência de SDK do cliente de armazenamento do Azure]</span><span class="sxs-lookup"><span data-stu-id="fa199-210">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="fa199-211">[Azure Storage REST API Reference][Azure Storage REST API] (Referência de API REST do Armazenamento do Azure)</span><span class="sxs-lookup"><span data-stu-id="fa199-211">[Azure Storage REST API][Azure Storage REST API]</span></span>
* <span data-ttu-id="fa199-212">[Microsoft Azure Storage Team Blog][Azure Storage Team Blog] (Blog da equipe de Armazenamento do Microsoft Azure)</span><span class="sxs-lookup"><span data-stu-id="fa199-212">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

<span data-ttu-id="fa199-213">Para obter mais informações, consulte também o [Centro de desenvolvedores do Java](/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="fa199-213">For more information, see also the [Java Developer Center](/develop/java/).</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
<span data-ttu-id="fa199-214">[Referência de SDK do cliente de armazenamento do Azure]: http://dl.windowsazure.com/storage/javadoc/</span><span class="sxs-lookup"><span data-stu-id="fa199-214">[Azure Storage Client SDK Reference]: http://dl.windowsazure.com/storage/javadoc/</span></span>
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Tables: Introducing Upsert and Query Projection]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx
