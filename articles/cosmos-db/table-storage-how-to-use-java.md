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
# <a name="how-toouse-table-storage-from-java"></a>Como toouse o armazenamento de tabela do Java
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Visão geral
Este guia mostrará como tooperform cenários comuns usando Olá serviço de armazenamento de tabela do Azure. exemplos de saudação são escritos em Java e usam Olá [SDK de armazenamento do Azure para Java][Azure Storage SDK for Java]. Olá cenários abordados incluem **criando**, **listando**, e **excluindo** tabelas, bem como **inserindo**,  **consultando**, **modificando**, e **excluindo** entidades em uma tabela. Para obter mais informações sobre tabelas, consulte Olá [próximas etapas](#Next-Steps) seção.

Observação: um SDK está disponível para os desenvolvedores que usam o Armazenamento do Azure em dispositivos Android. Para obter mais informações, consulte Olá [SDK de armazenamento do Azure para Android][Azure Storage SDK for Android].

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a>Criar um aplicativo Java
Neste guia, você usará os recursos de armazenamento que podem ser executados em um aplicativo Java localmente ou no código em execução em uma função web ou de trabalho do Azure.

toodo assim, você precisará tooinstall Olá Java Development Kit (JDK) e criar uma conta de armazenamento do Azure em sua assinatura do Azure. Depois de você ter feito isso, você precisará tooverify seu sistema de desenvolvimento atende aos requisitos mínimos de saudação e dependências que são listadas no hello [SDK de armazenamento do Azure para Java] [ Azure Storage SDK for Java] repositório no GitHub. Se seu sistema atende a esses requisitos, você pode seguir as instruções de saudação para baixar e instalar Olá bibliotecas de armazenamento do Azure para Java em seu sistema desse repositório. Depois de concluir essas tarefas, será possível toocreate um aplicativo Java que usa exemplos Olá neste artigo.

## <a name="configure-your-application-tooaccess-table-storage"></a>Configurar o armazenamento de tabela do aplicativo tooaccess
Adicione Olá importação instruções toohello superior do arquivo de Java Olá onde você deseja que as tabelas de tooaccess toouse Microsoft Azure armazenamento APIs a seguir:

```java
// Include hello following imports toouse table APIs
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.table.*;
import com.microsoft.azure.storage.table.TableQuery.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a>Configurar uma cadeia de conexão de armazenamento do Azure
Um cliente de armazenamento do Azure usa um pontos de extremidade de toostore de cadeia de caracteres de conexão de armazenamento e as credenciais para acessar os serviços de gerenciamento de dados. Quando em execução em um aplicativo cliente, deve fornecer a cadeia de conexão de armazenamento Olá no formato a seguir, usando o nome de saudação da sua conta de armazenamento de saudação e Olá chave de acesso primária para conta de armazenamento Olá listada no hello [portal do Azure](https://portal.azure.com)para Olá *AccountName* e *AccountKey* valores. Este exemplo mostra como você pode declarar uma cadeia de caracteres de conexão do campo estático toohold hello:

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

Em um aplicativo em execução dentro de uma função no Microsoft Azure, essa cadeia de caracteres pode ser armazenada no arquivo de configuração do serviço hello, *ServiceConfiguration*e pode ser acessado com uma chamada toohello  **RoleEnvironment.getConfigurationSettings** método. Aqui está um exemplo de obter a cadeia de caracteres de conexão de saudação de um **configuração** elemento chamado *StorageConnectionString* no arquivo de configuração de serviço hello:

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

Olá exemplos a seguir pressupõem que você usou uma cadeia de conexão de armazenamento esses dois métodos tooget hello.

## <a name="how-to-create-a-table"></a>Como: criar uma tabela
Um objeto **CloudTableClient** permite obter os objetos de referência para tabelas e entidades. Olá código a seguir cria um **CloudTableClient** do objeto e o utiliza toocreate um novo **CloudTable** objeto que representa uma tabela denominada "pessoal". (Observação: existem outras maneiras toocreate **CloudStorageAccount** objetos; para obter mais informações, consulte **CloudStorageAccount** em Olá [referência de SDK de cliente de armazenamento de Azure].)

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

## <a name="how-to-list-hello-tables"></a>Como: listar tabelas Olá
tooget uma lista de tabelas, chamada hello **CloudTableClient.listTables()** método tooretrieve uma lista que pode ser iterada dos nomes de tabela.

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

## <a name="how-to-add-an-entity-tooa-table"></a>Como: adicionar uma tabela de entidade tooa
Entidades são mapeadas tooJava objetos usando uma implementação de classe personalizada **TableEntity**. Para sua conveniência, Olá **TableServiceEntity** classe implementa **TableEntity** e usa reflexão toomap propriedades de métodos toogetter e setter para Olá propriedades. tooadd uma tabela de tooa de entidade, primeiro crie uma classe que define as propriedades de saudação da entidade. Olá código a seguir define uma classe de entidade que usa o nome saudação do cliente como chave de linha de saudação e último nome como chave de partição hello. Juntas, chave de linha e de partição da entidade identificam exclusivamente Olá entidade na tabela de saudação. Entidades com a mesma chave de partição pode ser consultado com mais rapidez do que aquelas com diferentes chaves de partição de saudação.

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

As operações de tabela que envolvem entidades exigem umobjeto **TableOperation** . Este objeto define Olá toobe de operação executada em uma entidade, que pode ser executada com um **CloudTable** objeto. Olá, código a seguir cria uma nova instância da saudação **CustomerEntity** classe com alguns toobe de dados do cliente armazenado. Olá chamadas próximas código **TableOperation.insertOrReplace** toocreate um **TableOperation** tooinsert uma entidade do objeto em uma tabela, e associa Olá novos **CustomerEntity**com ele. Finalmente, o código de saudação chama Olá **executar** método hello **CloudTable** objeto, especificando a tabela de "people" hello e hello novo **TableOperation**, que, em seguida, envia um entidade de solicitação toohello armazenamento serviço tooinsert Olá novo cliente na tabela de "people" hello, ou substituir entidade Olá se ele já existe.

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

## <a name="how-to-insert-a-batch-of-entities"></a>Como: inserir um lote de entidades
Você pode inserir um lote de serviço de tabela de toohello de entidades em uma operação de gravação. Olá código a seguir cria um **TableBatchOperation** do objeto, em seguida, adiciona três tooit de operações de inserção. Cada operação de inserção é adicionada por criar um novo objeto de entidade, definir seus valores e, em seguida, chamar hello **inserir** método hello **TableBatchOperation** objeto de entidade de saudação tooassociate com um novo operação de inserção. Olá, em seguida, chamadas de código **executar** em Olá **CloudTable** objeto, especificando a tabela de "people" hello e hello **TableBatchOperation** objeto, que envia o lote de saudação da tabela serviço de armazenamento de toohello de operações em uma única solicitação.

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

Toonote algumas coisas em operações em lote:

* Você pode realizar backup too100 insert, delete, merge, replace, insert ou merge e, em seguida, inserir ou substituir operações em qualquer combinação em um único lote.
* Uma operação em lote pode ter uma operação de recuperação, se for a única operação Olá em lote de saudação.
* Todas as entidades em uma única operação de lote devem ter Olá mesma chave de partição.
* Uma operação em lote é limitada tooa carga de dados de 4MB.

## <a name="how-to-retrieve-all-entities-in-a-partition"></a>Como recuperar todas as entidades em uma partição
tooquery uma tabela para entidades em uma partição, você pode usar um **TableQuery**. Chamar **TableQuery.from** toocreate uma consulta em uma determinada tabela que retorna um tipo de resultado especificado. Olá código a seguir especifica um filtro para entidades onde 'Smith' é a chave de partição hello. **TableQuery.generateFilterCondition** é um método auxiliar toocreate filtros para consultas. Chamar **onde** em referência Olá retornada por Olá **TableQuery.from** consulta toohello do método tooapply Olá filter. Quando Olá consulta é executada com uma chamada muito**executar** em Olá **CloudTable** do objeto, ele retorna um **iterador** com hello **CustomerEntity**especificado do tipo de resultado. Você pode usar Olá **iterador** retornados em um para cada loop tooconsume Olá obter os resultados. Esse código imprime campos de saudação de cada entidade no console de toohello de resultados de consulta de saudação.

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

## <a name="how-to-retrieve-a-range-of-entities-in-a-partition"></a>Como: recuperar um intervalo de entidades em uma partição
Se você não quiser tooquery todas as entidades de saudação em uma partição, você pode especificar um intervalo usando os operadores de comparação em um filtro. Olá dois filtros tooget todas as entidades na partição "Smith" onde a chave de linha de saudação (nome) começa com uma letra too'E combina o código a seguir ' alfabeto hello. Imprime resultados da consulta hello. Se você usar a tabela de toohello adicionado Olá entidades em lote Olá Inserir seção deste guia, apenas duas entidades são retornadas neste momento (Ben e Denise Smith); Jeff Smith não está incluído.

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

## <a name="how-to-retrieve-a-single-entity"></a>Como: recuperar uma única entidade
Você pode escrever uma consulta tooretrieve uma entidade única e específica. chamadas de código a seguir Olá **TableOperation.retrieve** com partição chave e a linha de parâmetros de chave toospecify Olá cliente "Jeff Smith", em vez de criar um **TableQuery** e usando Olá de toodo filtros mesma coisa. Quando executado, Olá recuperar operação retorna apenas uma entidade, em vez de uma coleção. Olá **getResultAsType** método converte o tipo de toohello de resultado de saudação do destino da atribuição de saudação, um **CustomerEntity** objeto. Se esse tipo não é compatível com tipo hello especificado para a consulta hello, uma exceção será lançada. Um valor nulo será retornado se nenhuma entidade tiver uma correspondência exata de chave de partição e chave de linha. Especificar chaves de partição e de linha em uma consulta é tooretrieve de maneira mais rápida de Olá uma única entidade de serviço de tabela de saudação.

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

## <a name="how-to-modify-an-entity"></a>Como modificar uma entidade
toomodify uma entidade, recuperá-lo do serviço de tabela hello, fazer alterações de objeto de entidade de toohello e salvar as alterações de saudação back toohello serviço de tabela com uma operação de substituição ou mesclagem. Olá código a seguir altera o número de telefone de um cliente existente. Em vez de chamar **TableOperation.insert** como fizemos tooinsert, esse código chama **TableOperation.replace**. Olá **CloudTable.execute** método chama o serviço de tabela hello e entidade Olá é substituída, a menos que outro aplicativo alterado em tempo de saudação desde que este aplicativo recuperá-lo. Quando isso acontece, uma exceção será lançada e entidade Olá deve ser recuperada, modificada e salvas novamente. Esse padrão de repetição de simultaneidade otimista é comum em um sistema de armazenamento distribuído.

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

## <a name="how-to-query-a-subset-of-entity-properties"></a>Como: consultar um subconjunto de propriedades de entidade
Uma tabela de consulta tooa pode recuperar apenas algumas propriedades de uma entidade. Essa técnica, chamada projeção, reduz a largura de banda e pode melhorar o desempenho da consulta, principalmente para grandes entidades. Olá, consulta em Olá código a seguir usa Olá **selecione** método tooreturn somente Olá endereços de email de entidades na tabela de saudação. Olá resultados são projetados para uma coleção de **cadeia de caracteres** com a Ajuda de saudação de um **EntityResolver**, qual Olá a conversão de tipo em entidades Olá retornado do servidor de saudação. Saiba mais sobre projeção em [Microsoft Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection] (Tabelas do Microsoft Azure: Apresentando a projeção de upsert e de consulta). Observe que projeção não é suportada no emulador de armazenamento local hello, para que este código seja executado somente quando usar uma conta no serviço de tabela de saudação.

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

## <a name="how-to-insert-or-replace-an-entity"></a>Como: inserir ou substituir uma entidade
Geralmente, você deseja tooadd uma tabela de entidade tooa sem saber se ele já existe na tabela de saudação. Uma operação de inserção ou substituição permite que você toomake uma única solicitação que irá inserir a entidade Olá se ele não existe ou substituir Olá existente a um caso. Criando exemplos anteriores, hello código a seguir insere ou substitui a entidade Olá para "Walter Harp". Depois de criar uma nova entidade, esse código chama Olá **TableOperation.insertOrReplace** método. Esse código, em seguida, chama **executar** em Olá **CloudTable** de objeto com a inserção de tabela e Olá Olá ou operação de tabela como parâmetros de saudação de substituição. tooupdate apenas parte de uma entidade, Olá **TableOperation.insertOrMerge** método pode ser usado em vez disso. Observe que inserir-ou-substituir não tem suporte no emulador de armazenamento local hello, para que este código seja executado somente quando usar uma conta no serviço de tabela de saudação. Saiba mais sobre inserção ou substituição e inserção ou mesclagem em [Microsoft Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection] (Tabelas do Microsoft Azure: Apresentando a projeção de upsert e de consulta).

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

## <a name="how-to-delete-an-entity"></a>Como excluir uma entidade
Você poderá excluir uma entidade facilmente depois que recuperá-la. Depois que a entidade de saudação é recuperada, chamar **TableOperation.delete** com hello toodelete de entidade. Em seguida, chame **executar** em Olá **CloudTable** objeto. saudação de código a seguir recupera e exclui uma entidade customer.

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

## <a name="how-to-delete-a-table"></a>Como excluir uma tabela
Por fim, hello código a seguir exclui uma tabela de uma conta de armazenamento. Uma tabela que foi excluída será toobe indisponível recriado por um período de tempo após a exclusão de hello, geralmente menos de 40 segundos.

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

## <a name="next-steps"></a>Próximas etapas

* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) é um aplicativo autônomo gratuito da Microsoft que permite que você toowork visualmente com dados de armazenamento do Azure no Linux, Windows e macOS.
* [Microsoft Azure Storage SDK for Java][Azure Storage SDK for Java] (SDK de Armazenamento do Microsoft Azure para Java)
* [referência de SDK de cliente de armazenamento de Azure][referência de SDK de cliente de armazenamento de Azure]
* [Azure Storage REST API Reference][Azure Storage REST API] (Referência de API REST do Armazenamento do Azure)
* [Microsoft Azure Storage Team Blog][Azure Storage Team Blog] (Blog da equipe de Armazenamento do Microsoft Azure)

Para saber mais, visite [Azure para desenvolvedores Java](/java/azure).

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[referência de SDK de cliente de armazenamento de Azure]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Tables: Introducing Upsert and Query Projection]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx
