---
title: aaaHow toouse armazenamento de tabela (C++) | Microsoft Docs
description: "Armazene dados estruturados em nuvem hello usando o armazenamento de tabela do Azure, um repositório de dados NoSQL."
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jahogg
editor: tysonn
ms.assetid: f191f308-e4b2-4de9-85cb-551b82b1ea7c
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: mimig
ms.openlocfilehash: 8096fe531427ba4858f7f4cb7f664f941892d1c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-c"></a>Como toouse o armazenamento de tabela do C++
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Visão geral
Este guia mostrará como cenários comuns de tooperform usando Olá serviço de armazenamento de tabela do Azure. exemplos de saudação são escritos em C++ e usam Olá [biblioteca de cliente de armazenamento do Azure para C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md). Olá cenários abordados incluem **criação e exclusão de uma tabela** e **trabalhando com entidades de tabela**.

> [!NOTE]
> Destino dessa guia Olá biblioteca de cliente de armazenamento do Azure para a versão 1.0.0 de C++ e acima. Olá recomendado versão é a biblioteca de cliente de armazenamento 2.2.0, que está disponível por meio de [NuGet](http://www.nuget.org/packages/wastorage) ou [GitHub](https://github.com/Azure/azure-storage-cpp/).
> 
> 

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a>Criar um aplicativo em C++
Neste guia, você usará os recursos de armazenamento que podem ser executados em um aplicativo do C++. toodo assim, você precisará tooinstall hello biblioteca de cliente de armazenamento do Azure para C++ e criar uma conta de armazenamento do Azure em sua assinatura do Azure.  

Olá tooinstall biblioteca de cliente de armazenamento do Azure para C++, você pode usar o hello métodos a seguir:

* **Linux:** siga instruções Olá fornecidas na Olá [biblioteca de cliente de armazenamento do Azure para C++ Leiame](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) página.  
* **Windows:** no Visual Studio, clique em **Ferramentas > Gerenciador de Pacotes do NuGet > Console do Gerenciador de Pacotes**. Digite o seguinte Olá comando em Olá [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) e pressione Enter.  
  
     Install-Package wastorage

## <a name="configure-your-application-tooaccess-table-storage"></a>Configurar seu aplicativo tooaccess armazenamento de tabela
Adicione a seguinte Olá incluem superior de toohello de instruções do arquivo de C++ de saudação onde você deseja que as tabelas de tooaccess APIs de armazenamento do Azure do toouse Olá:  

```cpp
#include <was/storage_account.h>
#include <was/table.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a>Configurar uma cadeia de conexão de armazenamento do Azure
Um cliente de armazenamento do Azure usa um pontos de extremidade de toostore de cadeia de caracteres de conexão de armazenamento e as credenciais para acessar os serviços de gerenciamento de dados. Ao executar um aplicativo cliente, você deve fornecer a cadeia de conexão de armazenamento Olá no hello formato a seguir. Use o nome da sua conta e hello armazenamento acesso chave de armazenamento para conta de armazenamento Olá Olá listados no hello [Portal do Azure](https://portal.azure.com) para Olá *AccountName* e *AccountKey* valores. Para obter informações sobre as contas de armazenamento e as teclas de acesso, veja [Sobre as contas de armazenamento do Azure](../storage/common/storage-create-storage-account.md). Este exemplo mostra como você pode declarar uma cadeia de caracteres de conexão do campo estático toohold hello:  

```cpp
// Define hello connection string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

tootest seu aplicativo no seu computador local com base em Windows, você pode usar o hello Azure [emulador de armazenamento](../storage/common/storage-use-emulator.md) que é instalada com hello [SDK do Azure](https://azure.microsoft.com/downloads/). emulador de armazenamento Olá é um utilitário que simula hello Azure Blob, fila e tabela de serviços disponíveis no computador de desenvolvimento local. Olá exemplo a seguir mostra como você pode declarar um emulador de armazenamento local do campo estático toohold Olá cadeia de caracteres conexão tooyour:  

```cpp
// Define hello connection string with Azure storage emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

toostart Olá emulador de armazenamento do Azure, clique em Olá **iniciar** botão ou pressione tecla do Windows hello. Comece digitando **emulador de armazenamento do Azure**e, em seguida, selecione **emulador de armazenamento do Microsoft Azure** da lista de saudação de aplicativos.  

Olá exemplos a seguir pressupõem que você usou uma cadeia de conexão de armazenamento esses dois métodos tooget hello.  

## <a name="retrieve-your-connection-string"></a>Recuperar sua cadeia de conexão
Você pode usar o hello **cloud_storage_account** classe toorepresent suas informações de conta de armazenamento. tooretrieve informações de cadeia de caracteres de conexão de armazenamento Olá da conta de armazenamento, você pode usar o método de análise de saudação.

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

Em seguida, obtenha uma referência tooa **cloud_table_client** de classe, que permite que você obtenha os objetos de referência para tabelas e entidades armazenados em hello, o serviço de armazenamento de tabela. Olá código a seguir cria um **cloud_table_client** objeto usando o objeto de conta de armazenamento Olá recuperamos acima:  

```cpp
// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();
```

## <a name="create-a-table"></a>Criar uma tabela
Um objeto **cloud_table_client** permite obter os objetos de referência para tabelas e entidades. Olá código a seguir cria um **cloud_table_client** do objeto e o utiliza toocreate uma nova tabela.

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);  

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference tooa table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table if it doesn't exist.
table.create_if_not_exists();  
```

## <a name="add-an-entity-tooa-table"></a>Adicionar uma tabela de entidade tooa
tooadd uma tabela de tooa de entidade, crie um novo **table_entity** do objeto e passá-lo muito**table_operation:: insert_entity**. Olá código a seguir usa nome saudação do cliente como a chave de linha de saudação e último nome como chave de partição hello. Juntas, chave de linha e de partição da entidade identificam exclusivamente Olá entidade na tabela de saudação. Entidades com hello a mesma chave de partição pode ser consultado mais rápido do que aquelas com diferentes chaves de partição, mas usar chaves de partição diversas permite maior escalabilidade de operação em paralelo. Para obter mais informações, veja [Lista de verificação de escalabilidade e desempenho do Armazenamento do Microsoft Azure](../storage/common/storage-performance-checklist.md).

Olá, código a seguir cria uma nova instância da **table_entity** com alguns toobe de dados do cliente armazenado. Olá chamadas próximas código **table_operation:: insert_entity** toocreate um **table_operation** tooinsert uma entidade do objeto em uma tabela, e associa Olá nova entidade de tabela com ele. Por fim, Olá chamadas de código Olá executar o método no hello **cloud_table** objeto. E hello novo **table_operation** envia uma solicitação toohello tabela tooinsert Olá novo cliente entidade de serviço na tabela de "people" hello.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference tooa table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table if it doesn't exist.
table.create_if_not_exists();

// Create a new customer entity.
azure::storage::table_entity customer1(U("Harp"), U("Walter"));

azure::storage::table_entity::properties_type& properties = customer1.properties();
properties.reserve(2);
properties[U("Email")] = azure::storage::entity_property(U("Walter@contoso.com"));

properties[U("Phone")] = azure::storage::entity_property(U("425-555-0101"));

// Create hello table operation that inserts hello customer entity.
azure::storage::table_operation insert_operation = azure::storage::table_operation::insert_entity(customer1);

// Execute hello insert operation.
azure::storage::table_result insert_result = table.execute(insert_operation);
```

## <a name="insert-a-batch-of-entities"></a>Inserir um lote de entidades
Você pode inserir um lote de entidades toohello serviço de tabela em uma operação de gravação. Olá código a seguir cria um **table_batch_operation** de objeto e, em seguida, adiciona três tooit de operações de inserção. Cada operação de inserção é adicionada ao criar um novo objeto de entidade, definir seus valores, e, em seguida, chamar hello Inserir método hello **table_batch_operation** entidade de saudação do objeto tooassociate com uma nova operação de inserção. Em seguida, **cloud_table.execute** é chamado de operação de saudação tooexecute.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define a batch operation.
azure::storage::table_batch_operation batch_operation;

// Create a customer entity and add it toohello table.
azure::storage::table_entity customer1(U("Smith"), U("Jeff"));

azure::storage::table_entity::properties_type& properties1 = customer1.properties();
properties1.reserve(2);
properties1[U("Email")] = azure::storage::entity_property(U("Jeff@contoso.com"));
properties1[U("Phone")] = azure::storage::entity_property(U("425-555-0104"));

// Create another customer entity and add it toohello table.
azure::storage::table_entity customer2(U("Smith"), U("Ben"));

azure::storage::table_entity::properties_type& properties2 = customer2.properties();
properties2.reserve(2);
properties2[U("Email")] = azure::storage::entity_property(U("Ben@contoso.com"));
properties2[U("Phone")] = azure::storage::entity_property(U("425-555-0102"));

// Create a third customer entity tooadd toohello table.
azure::storage::table_entity customer3(U("Smith"), U("Denise"));

azure::storage::table_entity::properties_type& properties3 = customer3.properties();
properties3.reserve(2);
properties3[U("Email")] = azure::storage::entity_property(U("Denise@contoso.com"));
properties3[U("Phone")] = azure::storage::entity_property(U("425-555-0103"));

// Add customer entities toohello batch insert operation.
batch_operation.insert_or_replace_entity(customer1);
batch_operation.insert_or_replace_entity(customer2);
batch_operation.insert_or_replace_entity(customer3);

// Execute hello batch operation.
std::vector<azure::storage::table_result> results = table.execute_batch(batch_operation);
```

Toonote algumas coisas em operações em lote:  

* Você pode executar os too100 insert, delete, merge, substituir, operações de inserção ou mesclagem e inserir ou substituir em qualquer combinação em um único lote.  
* Uma operação em lote pode ter uma operação de recuperação, se for a única operação Olá em lote de saudação.  
* Todas as entidades em uma única operação de lote devem ter Olá mesma chave de partição.  
* Uma operação em lote é limitada tooa carga de dados de 4 MB.  

## <a name="retrieve-all-entities-in-a-partition"></a>Recuperar todas as entidades em uma partição
tooquery uma tabela para todas as entidades em uma partição, use um **table_query** objeto. Olá, exemplo de código a seguir especifica um filtro para entidades onde 'Smith' é a chave de partição hello. Este exemplo imprime campos de saudação de cada entidade no console de toohello de resultados de consulta de saudação.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Construct hello query operation for all customer entities where PartitionKey="Smith".
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::generate_filter_condition(U("PartitionKey"), azure::storage::query_comparison_operator::equal, U("Smith")));

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Print hello fields for each customer.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

consulta neste exemplo Hello traz todas as entidades de saudação que correspondem aos critérios de filtro de saudação. Se você tiver grandes tabelas e precisa de entidades de tabela toodownload Olá geralmente, é recomendável que você armazena seus dados em blobs de armazenamento do Azure em vez disso.

## <a name="retrieve-a-range-of-entities-in-a-partition"></a>Recuperar um intervalo de entidades em uma partição
Se você não quiser tooquery todas as entidades de saudação em uma partição, você pode especificar um intervalo, combinando o filtro de chave de partição Olá com um filtro de linha de chave. Olá exemplo de código a seguir usa duas tooget de filtros todas as entidades na partição 'Smith' onde a chave de linha de saudação (nome) começa com uma letra anteriores E alfabeto hello e imprime os resultados da consulta hello.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table query.
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::combine_filter_conditions(
    azure::storage::table_query::generate_filter_condition(U("PartitionKey"),
    azure::storage::query_comparison_operator::equal, U("Smith")),
    azure::storage::query_logical_operator::op_and,
    azure::storage::table_query::generate_filter_condition(U("RowKey"), azure::storage::query_comparison_operator::less_than, U("E"))));

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Loop through hello results, displaying information about hello entity.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

## <a name="retrieve-a-single-entity"></a>Recuperar uma única entidade
Você pode escrever uma consulta tooretrieve uma entidade única e específica. código a seguir Olá usa **table_operation:: retrieve_entity** toospecify Prezado cliente 'Jeff Smith'. Esse método retorna uma única entidade, em vez de uma coleção e hello valor retornado está na **table_result**. Especificar chaves de partição e de linha em uma consulta é tooretrieve de maneira mais rápida de Olá uma única entidade de serviço de tabela de saudação.  

```cpp
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Output hello entity.
azure::storage::table_entity entity = retrieve_result.entity();
const azure::storage::table_entity::properties_type& properties = entity.properties();

std::wcout << U("PartitionKey: ") << entity.partition_key() << U(", RowKey: ") << entity.row_key()
    << U(", Property1: ") << properties.at(U("Email")).string_value()
    << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
```

## <a name="replace-an-entity"></a>Substituir uma entidade
tooreplace uma entidade, recuperá-lo do serviço de tabela hello, modificar o objeto de entidade hello e, em seguida, salvar as alterações de saudação fazer toohello serviço de tabela. Olá código a seguir altera telefone e endereço de um cliente existente de email. Em vez de chamar **table_operation::insert_entity**y, esse código usa **table_operation::replace_entity**. Isso faz com que Olá entidade toobe totalmente substituído no servidor de saudação, a menos que a entidade Olá no servidor de saudação foi alterado desde que foi recuperada, caso em que haverá falha na operação de saudação. Essa falha é tooprevent seu aplicativo substitua inadvertidamente uma alteração feita entre Olá recuperação e atualizar por outro componente do seu aplicativo. Hello manipulação adequada dessa falha é tooretrieve Olá entidade novamente, faça as alterações (se ainda é válida) e, em seguida, executar outro **table_operation:: replace_entity** operação. Olá próxima seção lhe mostrará como toooverride esse comportamento.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Replace an entity.
azure::storage::table_entity entity_to_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_replace = entity_to_replace.properties();
properties_to_replace.reserve(2);

// Specify a new phone number.
properties_to_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0106"));

// Specify a new email address.
properties_to_replace[U("Email")] = azure::storage::entity_property(U("JeffS@contoso.com"));

// Create an operation tooreplace hello entity.
azure::storage::table_operation replace_operation = azure::storage::table_operation::replace_entity(entity_to_replace);

// Submit hello operation toohello Table service.
azure::storage::table_result replace_result = table.execute(replace_operation);
```

## <a name="insert-or-replace-an-entity"></a>Inserir ou substituir uma entidade
**table_operation:: replace_entity** operações falharão se a entidade de saudação foi alterada desde que foi recuperada do servidor de saudação. Além disso, você deve recuperar a entidade de saudação do servidor de saudação primeiro na ordem de **table_operation:: replace_entity** toobe com êxito. Às vezes, no entanto, você não souber se a entidade Olá existe no servidor de saudação e valores atuais de saudação armazenados nela são irrelevantes — a atualização deve substituir todos eles. tooaccomplish isso, você usaria uma **table_operation:: insert_or_replace_entity** operação. Essa operação insere a entidade de saudação se ele não existe ou substitui-lo em caso afirmativo, independentemente de quando Olá última atualização foi feita. Em Olá exemplo de código a seguir, entidade customer de saudação de Jeff Smith ainda é recuperada, mas, em seguida, ele será salvo toohello back servidor via **table_operation:: insert_or_replace_entity**. Todas as atualizações feitas toohello entidade entre as operações de recuperação e atualização de saudação serão substituídas.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Insert-or-replace an entity.
azure::storage::table_entity entity_to_insert_or_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_insert_or_replace = entity_to_insert_or_replace.properties();

properties_to_insert_or_replace.reserve(2);

// Specify a phone number.
properties_to_insert_or_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0107"));

// Specify an email address.
properties_to_insert_or_replace[U("Email")] = azure::storage::entity_property(U("Jeffsm@contoso.com"));

// Create an operation tooinsert-or-replace hello entity.
azure::storage::table_operation insert_or_replace_operation = azure::storage::table_operation::insert_or_replace_entity(entity_to_insert_or_replace);

// Submit hello operation toohello Table service.
azure::storage::table_result insert_or_replace_result = table.execute(insert_or_replace_operation);
```

## <a name="query-a-subset-of-entity-properties"></a>consultar um subconjunto de propriedades da entidade
Uma tabela de consulta tooa pode recuperar apenas algumas propriedades de uma entidade. Olá, consulta em Olá código a seguir usa Olá **table_query:: set_select_columns** método tooreturn somente Olá endereços de email de entidades na tabela de saudação.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define hello query, and select only hello Email property.
azure::storage::table_query query;
std::vector<utility::string_t> columns;

columns.push_back(U("Email"));
query.set_select_columns(columns);

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Display hello results.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key();

    const azure::storage::table_entity::properties_type& properties = it->properties();
    for (auto prop_it = properties.begin(); prop_it != properties.end(); ++prop_it)
    {
        std::wcout << ", " << prop_it->first << ": " << prop_it->second.str();
    }

    std::wcout << std::endl;
}
```

> [!NOTE]
> Consultar algumas propriedades de uma entidade é uma operação mais eficiente do que recuperar todas as propriedades.
> 
> 

## <a name="delete-an-entity"></a>Excluir uma entidade
Você poderá excluir uma entidade facilmente depois que recuperá-la. Depois que a entidade de saudação é recuperada, chamar **table_operation:: delete_entity** com hello toodelete de entidade. Em seguida, chamar hello **cloud_table.execute** método. Olá código a seguir recupera e exclui uma entidade com uma chave de partição de "Smith" e uma chave de linha de "Jeff".  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation toodelete hello entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit hello delete operation toohello Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);  
```

## <a name="delete-a-table"></a>Excluir uma tabela
Por fim, Olá exemplo de código a seguir exclui uma tabela de uma conta de armazenamento. Uma tabela que tenha sido excluída será toobe indisponível recriado por um período de tempo após a exclusão de saudação.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation toodelete hello entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit hello delete operation toohello Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);
```

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu as Noções básicas de saudação do armazenamento de tabela, siga essas toolearn links mais sobre o armazenamento do Azure:  

* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) é um aplicativo autônomo gratuito da Microsoft que permite que você toowork visualmente com dados de armazenamento do Azure no Linux, Windows e macOS.
* [Como toouse armazenamento de Blob de C++](../storage/blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [Como toouse armazenamento de fila de C++](../storage/queues/storage-c-plus-plus-how-to-use-queues.md)
* [Listar recursos do Armazenamento do Azure no C++](../storage/common/storage-c-plus-plus-enumeration.md)
* [Referência da Biblioteca de Cliente de Armazenamento para C++](http://azure.github.io/azure-storage-cpp)
* [Documentação do Armazenamento do Azure](https://azure.microsoft.com/documentation/services/storage/)
