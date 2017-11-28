---
title: aaaHow toouse o armazenamento de tabela do Java | Microsoft Docs
description: "Armazene dados estruturados em nuvem hello usando o armazenamento de tabela do Azure, um repositório de dados NoSQL."
services: cosmos-db
documentationcenter: java
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: 45145189-e67f-4ca6-b15d-43af7bfd3f97
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 20d03e867219cc254da8dad37cf3cf61bca65671
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-java"></a><span data-ttu-id="f4f03-103">Como toouse o armazenamento de tabela do Java</span><span class="sxs-lookup"><span data-stu-id="f4f03-103">How toouse Table storage from Java</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="f4f03-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="f4f03-104">Overview</span></span>
<span data-ttu-id="f4f03-105">Este guia mostrará como tooperform cenários comuns usando Olá serviço de armazenamento de tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="f4f03-105">This guide will show you how tooperform common scenarios using hello Azure Table storage service.</span></span> <span data-ttu-id="f4f03-106">exemplos de saudação são escritos em Java e usam Olá [SDK de armazenamento do Azure para Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="f4f03-106">hello samples are written in Java and use hello [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="f4f03-107">Olá cenários abordados incluem **criando**, **listando**, e **excluindo** tabelas, bem como **inserindo**,  **consultando**, **modificando**, e **excluindo** entidades em uma tabela.</span><span class="sxs-lookup"><span data-stu-id="f4f03-107">hello scenarios covered include **creating**, **listing**, and **deleting** tables, as well as **inserting**, **querying**, **modifying**, and **deleting** entities in a table.</span></span> <span data-ttu-id="f4f03-108">Para obter mais informações sobre tabelas, consulte Olá [próximas etapas](#Next-Steps) seção.</span><span class="sxs-lookup"><span data-stu-id="f4f03-108">For more information on tables, see hello [Next steps](#Next-Steps) section.</span></span>

<span data-ttu-id="f4f03-109">Observação: um SDK está disponível para os desenvolvedores que usam o Armazenamento do Azure em dispositivos Android.</span><span class="sxs-lookup"><span data-stu-id="f4f03-109">Note: An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="f4f03-110">Para obter mais informações, consulte Olá [SDK de armazenamento do Azure para Android][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="f4f03-110">For more information, see hello [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="f4f03-111">Criar um aplicativo Java</span><span class="sxs-lookup"><span data-stu-id="f4f03-111">Create a Java application</span></span>
<span data-ttu-id="f4f03-112">Neste guia, você usará os recursos de armazenamento que podem ser executados em um aplicativo Java localmente ou no código em execução em uma função web ou de trabalho do Azure.</span><span class="sxs-lookup"><span data-stu-id="f4f03-112">In this guide, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="f4f03-113">toodo assim, você precisará tooinstall Olá Java Development Kit (JDK) e criar uma conta de armazenamento do Azure em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="f4f03-113">toodo so, you will need tooinstall hello Java Development Kit (JDK) and create an Azure storage account in your Azure subscription.</span></span> <span data-ttu-id="f4f03-114">Depois de você ter feito isso, você precisará tooverify seu sistema de desenvolvimento atende aos requisitos mínimos de saudação e dependências que são listadas no hello [SDK de armazenamento do Azure para Java] [ Azure Storage SDK for Java] repositório no GitHub.</span><span class="sxs-lookup"><span data-stu-id="f4f03-114">Once you have done so, you will need tooverify that your development system meets hello minimum requirements and dependencies which are listed in hello [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="f4f03-115">Se seu sistema atende a esses requisitos, você pode seguir as instruções de saudação para baixar e instalar Olá bibliotecas de armazenamento do Azure para Java em seu sistema desse repositório.</span><span class="sxs-lookup"><span data-stu-id="f4f03-115">If your system meets those requirements, you can follow hello instructions for downloading and installing hello Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="f4f03-116">Depois de concluir essas tarefas, será possível toocreate um aplicativo Java que usa exemplos Olá neste artigo.</span><span class="sxs-lookup"><span data-stu-id="f4f03-116">Once you have completed those tasks, you will be able toocreate a Java application which uses hello examples in this article.</span></span>

## <a name="configure-your-application-tooaccess-table-storage"></a><span data-ttu-id="f4f03-117">Configurar o armazenamento de tabela do aplicativo tooaccess</span><span class="sxs-lookup"><span data-stu-id="f4f03-117">Configure your application tooaccess table storage</span></span>
<span data-ttu-id="f4f03-118">Adicione Olá importação instruções toohello superior do arquivo de Java Olá onde você deseja que as tabelas de tooaccess toouse Microsoft Azure armazenamento APIs a seguir:</span><span class="sxs-lookup"><span data-stu-id="f4f03-118">Add hello following import statements toohello top of hello Java file where you want toouse Microsoft Azure storage APIs tooaccess tables:</span></span>

```java
// Include hello following imports toouse table APIs
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.table.*;
import com.microsoft.azure.storage.table.TableQuery.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="f4f03-119">Configurar uma cadeia de conexão de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="f4f03-119">Set up an Azure storage connection string</span></span>
<span data-ttu-id="f4f03-120">Um cliente de armazenamento do Azure usa um pontos de extremidade de toostore de cadeia de caracteres de conexão de armazenamento e as credenciais para acessar os serviços de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="f4f03-120">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="f4f03-121">Quando em execução em um aplicativo cliente, deve fornecer a cadeia de conexão de armazenamento Olá no formato a seguir, usando o nome de saudação da sua conta de armazenamento de saudação e Olá chave de acesso primária para conta de armazenamento Olá listada no hello [portal do Azure](https://portal.azure.com)para Olá *AccountName* e *AccountKey* valores.</span><span class="sxs-lookup"><span data-stu-id="f4f03-121">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello Primary access key for hello storage account listed in hello [Azure portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="f4f03-122">Este exemplo mostra como você pode declarar uma cadeia de caracteres de conexão do campo estático toohold hello:</span><span class="sxs-lookup"><span data-stu-id="f4f03-122">This example shows how you can declare a static field toohold hello connection string:</span></span>

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="f4f03-123">Em um aplicativo em execução dentro de uma função no Microsoft Azure, essa cadeia de caracteres pode ser armazenada no arquivo de configuração do serviço hello, *ServiceConfiguration*e pode ser acessado com uma chamada toohello  **RoleEnvironment.getConfigurationSettings** método.</span><span class="sxs-lookup"><span data-stu-id="f4f03-123">In an application running within a role in Microsoft Azure, this string can be stored in hello service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call toohello **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="f4f03-124">Aqui está um exemplo de obter a cadeia de caracteres de conexão de saudação de um **configuração** elemento chamado *StorageConnectionString* no arquivo de configuração de serviço hello:</span><span class="sxs-lookup"><span data-stu-id="f4f03-124">Here's an example of getting hello connection string from a **Setting** element named *StorageConnectionString* in hello service configuration file:</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="f4f03-125">Olá exemplos a seguir pressupõem que você usou uma cadeia de conexão de armazenamento esses dois métodos tooget hello.</span><span class="sxs-lookup"><span data-stu-id="f4f03-125">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="how-to-create-a-table"></a><span data-ttu-id="f4f03-126">Como: criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="f4f03-126">How to: Create a table</span></span>
<span data-ttu-id="f4f03-127">Um objeto **CloudTableClient** permite obter os objetos de referência para tabelas e entidades.</span><span class="sxs-lookup"><span data-stu-id="f4f03-127">A **CloudTableClient** object lets you get reference objects for tables and entities.</span></span> <span data-ttu-id="f4f03-128">Olá código a seguir cria um **CloudTableClient** do objeto e o utiliza toocreate um novo **CloudTable** objeto que representa uma tabela denominada "pessoal".</span><span class="sxs-lookup"><span data-stu-id="f4f03-128">hello following code creates a **CloudTableClient** object and uses it toocreate a new **CloudTable** object which represents a table named "people".</span></span> <span data-ttu-id="f4f03-129">(Observação: existem outras maneiras toocreate **CloudStorageAccount** objetos; para obter mais informações, consulte **CloudStorageAccount** em Olá [referência de SDK de cliente de armazenamento de Azure].)</span><span class="sxs-lookup"><span data-stu-id="f4f03-129">(Note: There are additional ways toocreate **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in hello [Azure Storage Client SDK Reference].)</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create hello table if it doesn't exist.
    String tableName = "people";
    CloudTable cloudTable = tableClient.getTableReference(tableName);
    cloudTable.createIfNotExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-hello-tables"></a><span data-ttu-id="f4f03-130">Como: listar tabelas Olá</span><span class="sxs-lookup"><span data-stu-id="f4f03-130">How to: List hello tables</span></span>
<span data-ttu-id="f4f03-131">tooget uma lista de tabelas, chamada hello **CloudTableClient.listTables()** método tooretrieve uma lista que pode ser iterada dos nomes de tabela.</span><span class="sxs-lookup"><span data-stu-id="f4f03-131">tooget a list of tables, call hello **CloudTableClient.listTables()** method tooretrieve an iterable list of table names.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Loop through hello collection of table names.
    for (String table : tableClient.listTables())
    {
        // Output each table name.
        System.out.println(table);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-an-entity-tooa-table"></a><span data-ttu-id="f4f03-132">Como: adicionar uma tabela de entidade tooa</span><span class="sxs-lookup"><span data-stu-id="f4f03-132">How to: Add an entity tooa table</span></span>
<span data-ttu-id="f4f03-133">Entidades são mapeadas tooJava objetos usando uma implementação de classe personalizada **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="f4f03-133">Entities map tooJava objects using a custom class implementing **TableEntity**.</span></span> <span data-ttu-id="f4f03-134">Para sua conveniência, Olá **TableServiceEntity** classe implementa **TableEntity** e usa reflexão toomap propriedades de métodos toogetter e setter para Olá propriedades.</span><span class="sxs-lookup"><span data-stu-id="f4f03-134">For convenience, hello **TableServiceEntity** class implements **TableEntity** and uses reflection toomap properties toogetter and setter methods named for hello properties.</span></span> <span data-ttu-id="f4f03-135">tooadd uma tabela de tooa de entidade, primeiro crie uma classe que define as propriedades de saudação da entidade.</span><span class="sxs-lookup"><span data-stu-id="f4f03-135">tooadd an entity tooa table, first create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="f4f03-136">Olá código a seguir define uma classe de entidade que usa o nome saudação do cliente como chave de linha de saudação e último nome como chave de partição hello.</span><span class="sxs-lookup"><span data-stu-id="f4f03-136">hello following code defines an entity class which uses hello customer's first name as hello row key, and last name as hello partition key.</span></span> <span data-ttu-id="f4f03-137">Juntas, chave de linha e de partição da entidade identificam exclusivamente Olá entidade na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="f4f03-137">Together, an entity's partition and row key uniquely identify hello entity in hello table.</span></span> <span data-ttu-id="f4f03-138">Entidades com a mesma chave de partição pode ser consultado com mais rapidez do que aquelas com diferentes chaves de partição de saudação.</span><span class="sxs-lookup"><span data-stu-id="f4f03-138">Entities with hello same partition key can be queried faster than those with different partition keys.</span></span>

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

<span data-ttu-id="f4f03-139">As operações de tabela que envolvem entidades exigem umobjeto **TableOperation** .</span><span class="sxs-lookup"><span data-stu-id="f4f03-139">Table operations involving entities require a **TableOperation** object.</span></span> <span data-ttu-id="f4f03-140">Este objeto define Olá toobe de operação executada em uma entidade, que pode ser executada com um **CloudTable** objeto.</span><span class="sxs-lookup"><span data-stu-id="f4f03-140">This object defines hello operation toobe performed on an entity, which can be executed with a **CloudTable** object.</span></span> <span data-ttu-id="f4f03-141">Olá, código a seguir cria uma nova instância da saudação **CustomerEntity** classe com alguns toobe de dados do cliente armazenado.</span><span class="sxs-lookup"><span data-stu-id="f4f03-141">hello following code creates a new instance of hello **CustomerEntity** class with some customer data toobe stored.</span></span> <span data-ttu-id="f4f03-142">Olá chamadas próximas código **TableOperation.insertOrReplace** toocreate um **TableOperation** tooinsert uma entidade do objeto em uma tabela, e associa Olá novos **CustomerEntity**com ele.</span><span class="sxs-lookup"><span data-stu-id="f4f03-142">hello code next calls **TableOperation.insertOrReplace** toocreate a **TableOperation** object tooinsert an entity into a table, and associates hello new **CustomerEntity** with it.</span></span> <span data-ttu-id="f4f03-143">Finalmente, o código de saudação chama Olá **executar** método hello **CloudTable** objeto, especificando a tabela de "people" hello e hello novo **TableOperation**, que, em seguida, envia um entidade de solicitação toohello armazenamento serviço tooinsert Olá novo cliente na tabela de "people" hello, ou substituir entidade Olá se ele já existe.</span><span class="sxs-lookup"><span data-stu-id="f4f03-143">Finally, hello code calls hello **execute** method on hello **CloudTable** object, specifying hello "people" table and hello new **TableOperation**, which then sends a request toohello storage service tooinsert hello new customer entity into hello "people" table, or replace hello entity if it already exists.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.setEmail("Walter@contoso.com");
    customer1.setPhoneNumber("425-555-0101");

    // Create an operation tooadd hello new customer toohello people table.
    TableOperation insertCustomer1 = TableOperation.insertOrReplace(customer1);

    // Submit hello operation toohello table service.
    cloudTable.execute(insertCustomer1);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-a-batch-of-entities"></a><span data-ttu-id="f4f03-144">Como: inserir um lote de entidades</span><span class="sxs-lookup"><span data-stu-id="f4f03-144">How to: Insert a batch of entities</span></span>
<span data-ttu-id="f4f03-145">Você pode inserir um lote de serviço de tabela de toohello de entidades em uma operação de gravação.</span><span class="sxs-lookup"><span data-stu-id="f4f03-145">You can insert a batch of entities toohello table service in one write operation.</span></span> <span data-ttu-id="f4f03-146">Olá código a seguir cria um **TableBatchOperation** do objeto, em seguida, adiciona três tooit de operações de inserção.</span><span class="sxs-lookup"><span data-stu-id="f4f03-146">hello following code creates a **TableBatchOperation** object, then adds three insert operations tooit.</span></span> <span data-ttu-id="f4f03-147">Cada operação de inserção é adicionada por criar um novo objeto de entidade, definir seus valores e, em seguida, chamar hello **inserir** método hello **TableBatchOperation** objeto de entidade de saudação tooassociate com um novo operação de inserção.</span><span class="sxs-lookup"><span data-stu-id="f4f03-147">Each insert operation is added by creating a new entity object, setting its values, and then calling hello **insert** method on hello **TableBatchOperation** object tooassociate hello entity with a new insert operation.</span></span> <span data-ttu-id="f4f03-148">Olá, em seguida, chamadas de código **executar** em Olá **CloudTable** objeto, especificando a tabela de "people" hello e hello **TableBatchOperation** objeto, que envia o lote de saudação da tabela serviço de armazenamento de toohello de operações em uma única solicitação.</span><span class="sxs-lookup"><span data-stu-id="f4f03-148">Then hello code calls **execute** on hello **CloudTable** object, specifying hello "people" table and hello **TableBatchOperation** object, which sends hello batch of table operations toohello storage service in a single request.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Define a batch operation.
    TableBatchOperation batchOperation = new TableBatchOperation();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a customer entity tooadd toohello table.
    CustomerEntity customer = new CustomerEntity("Smith", "Jeff");
    customer.setEmail("Jeff@contoso.com");
    customer.setPhoneNumber("425-555-0104");
    batchOperation.insertOrReplace(customer);

    // Create another customer entity tooadd toohello table.
    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.setEmail("Ben@contoso.com");
    customer2.setPhoneNumber("425-555-0102");
    batchOperation.insertOrReplace(customer2);

    // Create a third customer entity tooadd toohello table.
    CustomerEntity customer3 = new CustomerEntity("Smith", "Denise");
    customer3.setEmail("Denise@contoso.com");
    customer3.setPhoneNumber("425-555-0103");
    batchOperation.insertOrReplace(customer3);

    // Execute hello batch of operations on hello "people" table.
    cloudTable.execute(batchOperation);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="f4f03-149">Toonote algumas coisas em operações em lote:</span><span class="sxs-lookup"><span data-stu-id="f4f03-149">Some things toonote on batch operations:</span></span>

* <span data-ttu-id="f4f03-150">Você pode realizar backup too100 insert, delete, merge, replace, insert ou merge e, em seguida, inserir ou substituir operações em qualquer combinação em um único lote.</span><span class="sxs-lookup"><span data-stu-id="f4f03-150">You can perform up too100 insert, delete, merge, replace, insert or merge, and insert or replace operations in any combination in a single batch.</span></span>
* <span data-ttu-id="f4f03-151">Uma operação em lote pode ter uma operação de recuperação, se for a única operação Olá em lote de saudação.</span><span class="sxs-lookup"><span data-stu-id="f4f03-151">A batch operation can have a retrieve operation, if it is hello only operation in hello batch.</span></span>
* <span data-ttu-id="f4f03-152">Todas as entidades em uma única operação de lote devem ter Olá mesma chave de partição.</span><span class="sxs-lookup"><span data-stu-id="f4f03-152">All entities in a single batch operation must have hello same partition key.</span></span>
* <span data-ttu-id="f4f03-153">Uma operação em lote é limitada tooa carga de dados de 4MB.</span><span class="sxs-lookup"><span data-stu-id="f4f03-153">A batch operation is limited tooa 4MB data payload.</span></span>

## <a name="how-to-retrieve-all-entities-in-a-partition"></a><span data-ttu-id="f4f03-154">Como recuperar todas as entidades em uma partição</span><span class="sxs-lookup"><span data-stu-id="f4f03-154">How to: Retrieve all entities in a partition</span></span>
<span data-ttu-id="f4f03-155">tooquery uma tabela para entidades em uma partição, você pode usar um **TableQuery**.</span><span class="sxs-lookup"><span data-stu-id="f4f03-155">tooquery a table for entities in a partition, you can use a **TableQuery**.</span></span> <span data-ttu-id="f4f03-156">Chamar **TableQuery.from** toocreate uma consulta em uma determinada tabela que retorna um tipo de resultado especificado.</span><span class="sxs-lookup"><span data-stu-id="f4f03-156">Call **TableQuery.from** toocreate a query on a particular table that returns a specified result type.</span></span> <span data-ttu-id="f4f03-157">Olá código a seguir especifica um filtro para entidades onde 'Smith' é a chave de partição hello.</span><span class="sxs-lookup"><span data-stu-id="f4f03-157">hello following code specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="f4f03-158">**TableQuery.generateFilterCondition** é um método auxiliar toocreate filtros para consultas.</span><span class="sxs-lookup"><span data-stu-id="f4f03-158">**TableQuery.generateFilterCondition** is a helper method toocreate filters for queries.</span></span> <span data-ttu-id="f4f03-159">Chamar **onde** em referência Olá retornada por Olá **TableQuery.from** consulta toohello do método tooapply Olá filter.</span><span class="sxs-lookup"><span data-stu-id="f4f03-159">Call **where** on hello reference returned by hello **TableQuery.from** method tooapply hello filter toohello query.</span></span> <span data-ttu-id="f4f03-160">Quando Olá consulta é executada com uma chamada muito**executar** em Olá **CloudTable** do objeto, ele retorna um **iterador** com hello **CustomerEntity**especificado do tipo de resultado.</span><span class="sxs-lookup"><span data-stu-id="f4f03-160">When hello query is executed with a call too**execute** on hello **CloudTable** object, it returns an **Iterator** with hello **CustomerEntity** result type specified.</span></span> <span data-ttu-id="f4f03-161">Você pode usar Olá **iterador** retornados em um para cada loop tooconsume Olá obter os resultados.</span><span class="sxs-lookup"><span data-stu-id="f4f03-161">You can then use hello **Iterator** returned in a for each loop tooconsume hello results.</span></span> <span data-ttu-id="f4f03-162">Esse código imprime campos de saudação de cada entidade no console de toohello de resultados de consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="f4f03-162">This code prints hello fields of each entity in hello query results toohello console.</span></span>

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

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where hello partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Specify a partition query, using "Smith" as hello partition key filter.
    TableQuery<CustomerEntity> partitionQuery =
        TableQuery.from(CustomerEntity.class)
        .where(partitionFilter);

    // Loop through hello results, displaying information about hello entity.
    for (CustomerEntity entity : cloudTable.execute(partitionQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="f4f03-163">Como: recuperar um intervalo de entidades em uma partição</span><span class="sxs-lookup"><span data-stu-id="f4f03-163">How to: Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="f4f03-164">Se você não quiser tooquery todas as entidades de saudação em uma partição, você pode especificar um intervalo usando os operadores de comparação em um filtro.</span><span class="sxs-lookup"><span data-stu-id="f4f03-164">If you don't want tooquery all hello entities in a partition, you can specify a range by using comparison operators in a filter.</span></span> <span data-ttu-id="f4f03-165">Olá dois filtros tooget todas as entidades na partição "Smith" onde a chave de linha de saudação (nome) começa com uma letra too'E combina o código a seguir ' alfabeto hello.</span><span class="sxs-lookup"><span data-stu-id="f4f03-165">hello following code combines two filters tooget all entities in partition "Smith" where hello row key (first name) starts with a letter up too'E' in hello alphabet.</span></span> <span data-ttu-id="f4f03-166">Imprime resultados da consulta hello.</span><span class="sxs-lookup"><span data-stu-id="f4f03-166">Then it prints hello query results.</span></span> <span data-ttu-id="f4f03-167">Se você usar a tabela de toohello adicionado Olá entidades em lote Olá Inserir seção deste guia, apenas duas entidades são retornadas neste momento (Ben e Denise Smith); Jeff Smith não está incluído.</span><span class="sxs-lookup"><span data-stu-id="f4f03-167">If you use hello entities added toohello table in hello batch insert section of this guide, only two entities are returned this time (Ben and Denise Smith); Jeff Smith is not included.</span></span>

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

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where hello partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Create a filter condition where hello row key is less than hello letter "E".
    String rowFilter = TableQuery.generateFilterCondition(
        ROW_KEY,
        QueryComparisons.LESS_THAN,
        "E");

    // Combine hello two conditions into a filter expression.
    String combinedFilter = TableQuery.combineFilters(partitionFilter,
        Operators.AND, rowFilter);

    // Specify a range query, using "Smith" as hello partition key,
    // with hello row key being up toohello letter "E".
    TableQuery<CustomerEntity> rangeQuery =
        TableQuery.from(CustomerEntity.class)
        .where(combinedFilter);

    // Loop through hello results, displaying information about hello entity
    for (CustomerEntity entity : cloudTable.execute(rangeQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-single-entity"></a><span data-ttu-id="f4f03-168">Como: recuperar uma única entidade</span><span class="sxs-lookup"><span data-stu-id="f4f03-168">How to: Retrieve a single entity</span></span>
<span data-ttu-id="f4f03-169">Você pode escrever uma consulta tooretrieve uma entidade única e específica.</span><span class="sxs-lookup"><span data-stu-id="f4f03-169">You can write a query tooretrieve a single, specific entity.</span></span> <span data-ttu-id="f4f03-170">chamadas de código a seguir Olá **TableOperation.retrieve** com partição chave e a linha de parâmetros de chave toospecify Olá cliente "Jeff Smith", em vez de criar um **TableQuery** e usando Olá de toodo filtros mesma coisa.</span><span class="sxs-lookup"><span data-stu-id="f4f03-170">hello following code calls **TableOperation.retrieve** with partition key and row key parameters toospecify hello customer "Jeff Smith", instead of creating a **TableQuery** and using filters toodo hello same thing.</span></span> <span data-ttu-id="f4f03-171">Quando executado, Olá recuperar operação retorna apenas uma entidade, em vez de uma coleção.</span><span class="sxs-lookup"><span data-stu-id="f4f03-171">When executed, hello retrieve operation returns just one entity, rather than a collection.</span></span> <span data-ttu-id="f4f03-172">Olá **getResultAsType** método converte o tipo de toohello de resultado de saudação do destino da atribuição de saudação, um **CustomerEntity** objeto.</span><span class="sxs-lookup"><span data-stu-id="f4f03-172">hello **getResultAsType** method casts hello result toohello type of hello assignment target, a **CustomerEntity** object.</span></span> <span data-ttu-id="f4f03-173">Se esse tipo não é compatível com tipo hello especificado para a consulta hello, uma exceção será lançada.</span><span class="sxs-lookup"><span data-stu-id="f4f03-173">If this type is not compatible with hello type specified for hello query, an exception will be thrown.</span></span> <span data-ttu-id="f4f03-174">Um valor nulo será retornado se nenhuma entidade tiver uma correspondência exata de chave de partição e chave de linha.</span><span class="sxs-lookup"><span data-stu-id="f4f03-174">A null value is returned if no entity has an exact partition and row key match.</span></span> <span data-ttu-id="f4f03-175">Especificar chaves de partição e de linha em uma consulta é tooretrieve de maneira mais rápida de Olá uma única entidade de serviço de tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="f4f03-175">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello Table service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve hello entity with partition key of "Smith" and row key of "Jeff"
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit hello operation toohello table service and get hello specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Output hello entity.
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
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-modify-an-entity"></a><span data-ttu-id="f4f03-176">Como modificar uma entidade</span><span class="sxs-lookup"><span data-stu-id="f4f03-176">How to: Modify an entity</span></span>
<span data-ttu-id="f4f03-177">toomodify uma entidade, recuperá-lo do serviço de tabela hello, fazer alterações de objeto de entidade de toohello e salvar as alterações de saudação back toohello serviço de tabela com uma operação de substituição ou mesclagem.</span><span class="sxs-lookup"><span data-stu-id="f4f03-177">toomodify an entity, retrieve it from hello table service, make changes toohello entity object, and save hello changes back toohello table service with a replace or merge operation.</span></span> <span data-ttu-id="f4f03-178">Olá código a seguir altera o número de telefone de um cliente existente.</span><span class="sxs-lookup"><span data-stu-id="f4f03-178">hello following code changes an existing customer's phone number.</span></span> <span data-ttu-id="f4f03-179">Em vez de chamar **TableOperation.insert** como fizemos tooinsert, esse código chama **TableOperation.replace**.</span><span class="sxs-lookup"><span data-stu-id="f4f03-179">Instead of calling **TableOperation.insert** like we did tooinsert, this code calls **TableOperation.replace**.</span></span> <span data-ttu-id="f4f03-180">Olá **CloudTable.execute** método chama o serviço de tabela hello e entidade Olá é substituída, a menos que outro aplicativo alterado em tempo de saudação desde que este aplicativo recuperá-lo.</span><span class="sxs-lookup"><span data-stu-id="f4f03-180">hello **CloudTable.execute** method calls hello table service, and hello entity is replaced, unless another application changed it in hello time since this application retrieved it.</span></span> <span data-ttu-id="f4f03-181">Quando isso acontece, uma exceção será lançada e entidade Olá deve ser recuperada, modificada e salvas novamente.</span><span class="sxs-lookup"><span data-stu-id="f4f03-181">When that happens, an exception is thrown, and hello entity must be retrieved, modified, and saved again.</span></span> <span data-ttu-id="f4f03-182">Esse padrão de repetição de simultaneidade otimista é comum em um sistema de armazenamento distribuído.</span><span class="sxs-lookup"><span data-stu-id="f4f03-182">This optimistic concurrency retry pattern is common in a distributed storage system.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit hello operation toohello table service and get hello specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Specify a new phone number.
    specificEntity.setPhoneNumber("425-555-0105");

    // Create an operation tooreplace hello entity.
    TableOperation replaceEntity = TableOperation.replace(specificEntity);

    // Submit hello operation toohello table service.
    cloudTable.execute(replaceEntity);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-query-a-subset-of-entity-properties"></a><span data-ttu-id="f4f03-183">Como: consultar um subconjunto de propriedades de entidade</span><span class="sxs-lookup"><span data-stu-id="f4f03-183">How to: Query a subset of entity properties</span></span>
<span data-ttu-id="f4f03-184">Uma tabela de consulta tooa pode recuperar apenas algumas propriedades de uma entidade.</span><span class="sxs-lookup"><span data-stu-id="f4f03-184">A query tooa table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="f4f03-185">Essa técnica, chamada projeção, reduz a largura de banda e pode melhorar o desempenho da consulta, principalmente para grandes entidades.</span><span class="sxs-lookup"><span data-stu-id="f4f03-185">This technique, called projection, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="f4f03-186">Olá, consulta em Olá código a seguir usa Olá **selecione** método tooreturn somente Olá endereços de email de entidades na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="f4f03-186">hello query in hello following code uses hello **select** method tooreturn only hello email addresses of entities in hello table.</span></span> <span data-ttu-id="f4f03-187">Olá resultados são projetados para uma coleção de **cadeia de caracteres** com a Ajuda de saudação de um **EntityResolver**, qual Olá a conversão de tipo em entidades Olá retornado do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="f4f03-187">hello results are projected into a collection of **String** with hello help of an **EntityResolver**, which does hello type conversion on hello entities returned from hello server.</span></span> <span data-ttu-id="f4f03-188">Saiba mais sobre projeção em [Microsoft Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection] (Tabelas do Microsoft Azure: Apresentando a projeção de upsert e de consulta).</span><span class="sxs-lookup"><span data-stu-id="f4f03-188">You can learn more about projection in [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span></span> <span data-ttu-id="f4f03-189">Observe que projeção não é suportada no emulador de armazenamento local hello, para que este código seja executado somente quando usar uma conta no serviço de tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="f4f03-189">Note that projection is not supported on hello local storage emulator, so this code runs only when using an account on hello table service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Define a projection query that retrieves only hello Email property
    TableQuery<CustomerEntity> projectionQuery =
        TableQuery.from(CustomerEntity.class)
        .select(new String[] {"Email"});

    // Define a Entity resolver tooproject hello entity toohello Email value.
    EntityResolver<String> emailResolver = new EntityResolver<String>() {
        @Override
        public String resolve(String PartitionKey, String RowKey, Date timeStamp, HashMap<String, EntityProperty> properties, String etag) {
            return properties.get("Email").getValueAsString();
        }
    };

    // Loop through hello results, displaying hello Email values.
    for (String projectedString :
        cloudTable.execute(projectionQuery, emailResolver)) {
            System.out.println(projectedString);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-or-replace-an-entity"></a><span data-ttu-id="f4f03-190">Como: inserir ou substituir uma entidade</span><span class="sxs-lookup"><span data-stu-id="f4f03-190">How to: Insert or Replace an entity</span></span>
<span data-ttu-id="f4f03-191">Geralmente, você deseja tooadd uma tabela de entidade tooa sem saber se ele já existe na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="f4f03-191">Often you want tooadd an entity tooa table without knowing if it already exists in hello table.</span></span> <span data-ttu-id="f4f03-192">Uma operação de inserção ou substituição permite que você toomake uma única solicitação que irá inserir a entidade Olá se ele não existe ou substituir Olá existente a um caso.</span><span class="sxs-lookup"><span data-stu-id="f4f03-192">An insert-or-replace operation allows you toomake a single request which will insert hello entity if it does not exist or replace hello existing one if it does.</span></span> <span data-ttu-id="f4f03-193">Criando exemplos anteriores, hello código a seguir insere ou substitui a entidade Olá para "Walter Harp".</span><span class="sxs-lookup"><span data-stu-id="f4f03-193">Building on prior examples, hello following code inserts or replaces hello entity for "Walter Harp".</span></span> <span data-ttu-id="f4f03-194">Depois de criar uma nova entidade, esse código chama Olá **TableOperation.insertOrReplace** método.</span><span class="sxs-lookup"><span data-stu-id="f4f03-194">After creating a new entity, this code calls hello **TableOperation.insertOrReplace** method.</span></span> <span data-ttu-id="f4f03-195">Esse código, em seguida, chama **executar** em Olá **CloudTable** de objeto com a inserção de tabela e Olá Olá ou operação de tabela como parâmetros de saudação de substituição.</span><span class="sxs-lookup"><span data-stu-id="f4f03-195">This code then calls **execute** on hello **CloudTable** object with hello table and hello insert or replace table operation as hello parameters.</span></span> <span data-ttu-id="f4f03-196">tooupdate apenas parte de uma entidade, Olá **TableOperation.insertOrMerge** método pode ser usado em vez disso.</span><span class="sxs-lookup"><span data-stu-id="f4f03-196">tooupdate only part of an entity, hello **TableOperation.insertOrMerge** method can be used instead.</span></span> <span data-ttu-id="f4f03-197">Observe que inserir-ou-substituir não tem suporte no emulador de armazenamento local hello, para que este código seja executado somente quando usar uma conta no serviço de tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="f4f03-197">Note that insert-or-replace is not supported on hello local storage emulator, so this code runs only when using an account on hello table service.</span></span> <span data-ttu-id="f4f03-198">Saiba mais sobre inserção ou substituição e inserção ou mesclagem em [Microsoft Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection] (Tabelas do Microsoft Azure: Apresentando a projeção de upsert e de consulta).</span><span class="sxs-lookup"><span data-stu-id="f4f03-198">You can learn more about insert-or-replace and insert-or-merge in this [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer5 = new CustomerEntity("Harp", "Walter");
    customer5.setEmail("Walter@contoso.com");
    customer5.setPhoneNumber("425-555-0106");

    // Create an operation tooadd hello new customer toohello people table.
    TableOperation insertCustomer5 = TableOperation.insertOrReplace(customer5);

    // Submit hello operation toohello table service.
    cloudTable.execute(insertCustomer5);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-an-entity"></a><span data-ttu-id="f4f03-199">Como excluir uma entidade</span><span class="sxs-lookup"><span data-stu-id="f4f03-199">How to: Delete an entity</span></span>
<span data-ttu-id="f4f03-200">Você poderá excluir uma entidade facilmente depois que recuperá-la.</span><span class="sxs-lookup"><span data-stu-id="f4f03-200">You can easily delete an entity after you have retrieved it.</span></span> <span data-ttu-id="f4f03-201">Depois que a entidade de saudação é recuperada, chamar **TableOperation.delete** com hello toodelete de entidade.</span><span class="sxs-lookup"><span data-stu-id="f4f03-201">Once hello entity is retrieved, call **TableOperation.delete** with hello entity toodelete.</span></span> <span data-ttu-id="f4f03-202">Em seguida, chame **executar** em Olá **CloudTable** objeto.</span><span class="sxs-lookup"><span data-stu-id="f4f03-202">Then call **execute** on hello **CloudTable** object.</span></span> <span data-ttu-id="f4f03-203">saudação de código a seguir recupera e exclui uma entidade customer.</span><span class="sxs-lookup"><span data-stu-id="f4f03-203">hello following code retrieves and deletes a customer entity.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff = TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
    CustomerEntity entitySmithJeff =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Create an operation toodelete hello entity.
    TableOperation deleteSmithJeff = TableOperation.delete(entitySmithJeff);

    // Submit hello delete operation toohello table service.
    cloudTable.execute(deleteSmithJeff);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-table"></a><span data-ttu-id="f4f03-204">Como excluir uma tabela</span><span class="sxs-lookup"><span data-stu-id="f4f03-204">How to: Delete a table</span></span>
<span data-ttu-id="f4f03-205">Por fim, hello código a seguir exclui uma tabela de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f4f03-205">Finally, hello following code deletes a table from a storage account.</span></span> <span data-ttu-id="f4f03-206">Uma tabela que foi excluída será toobe indisponível recriado por um período de tempo após a exclusão de hello, geralmente menos de 40 segundos.</span><span class="sxs-lookup"><span data-stu-id="f4f03-206">A table which has been deleted will be unavailable toobe recreated for a period of time following hello deletion, usually less than forty seconds.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Delete hello table and all its data if it exists.
    CloudTable cloudTable = tableClient.getTableReference("people");
    cloudTable.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```
[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="next-steps"></a><span data-ttu-id="f4f03-207">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f4f03-207">Next steps</span></span>

* <span data-ttu-id="f4f03-208">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) é um aplicativo autônomo gratuito da Microsoft que permite que você toowork visualmente com dados de armazenamento do Azure no Linux, Windows e macOS.</span><span class="sxs-lookup"><span data-stu-id="f4f03-208">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="f4f03-209">[Microsoft Azure Storage SDK for Java][Azure Storage SDK for Java] (SDK de Armazenamento do Microsoft Azure para Java)</span><span class="sxs-lookup"><span data-stu-id="f4f03-209">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="f4f03-210">[referência de SDK de cliente de armazenamento de Azure][referência de SDK de cliente de armazenamento de Azure]</span><span class="sxs-lookup"><span data-stu-id="f4f03-210">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="f4f03-211">[Azure Storage REST API Reference][Azure Storage REST API] (Referência de API REST do Armazenamento do Azure)</span><span class="sxs-lookup"><span data-stu-id="f4f03-211">[Azure Storage REST API][Azure Storage REST API]</span></span>
* <span data-ttu-id="f4f03-212">[Microsoft Azure Storage Team Blog][Azure Storage Team Blog] (Blog da equipe de Armazenamento do Microsoft Azure)</span><span class="sxs-lookup"><span data-stu-id="f4f03-212">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

<span data-ttu-id="f4f03-213">Para saber mais, visite [Azure para desenvolvedores Java](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="f4f03-213">For more information, visit [Azure for Java developers](/java/azure).</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[referência de SDK de cliente de armazenamento de Azure]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Tables: Introducing Upsert and Query Projection]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx
