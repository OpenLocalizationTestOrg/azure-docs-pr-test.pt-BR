---
title: Como usar o Armazenamento de Tabelas do Azure por meio do Ruby | Microsoft Docs
description: "Armazene dados estruturados na nuvem usando o Armazenamento de Tabelas do Azure, um repositório de dados NoSQL."
services: storage
documentationcenter: ruby
author: mmacy
manager: timlt
editor: 
ms.assetid: 047cd9ff-17d3-4c15-9284-1b5cc61a3224
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 03f466cb08ed2ccbd2985471d0956af9e66d97f1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-table-storage-from-ruby"></a><span data-ttu-id="e2b81-103">Como usar o Armazenamento de Tabela do Azure por meio do Ruby</span><span class="sxs-lookup"><span data-stu-id="e2b81-103">How to use Azure Table Storage from Ruby</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="e2b81-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="e2b81-104">Overview</span></span>
<span data-ttu-id="e2b81-105">Este guia mostra como executar cenários comuns usando o serviço Tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="e2b81-105">This guide shows you how to perform common scenarios using the Azure Table service.</span></span> <span data-ttu-id="e2b81-106">Os exemplos de código são gravados com a API do Ruby.</span><span class="sxs-lookup"><span data-stu-id="e2b81-106">The samples are written using the Ruby API.</span></span> <span data-ttu-id="e2b81-107">Os cenários abrangidos incluem **criar e excluir uma tabela, inserindo e consultando entidades em uma tabela**.</span><span class="sxs-lookup"><span data-stu-id="e2b81-107">The scenarios covered include **creating and deleting a table, inserting and querying entities in a table**.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="e2b81-108">Criar um aplicativo Ruby</span><span class="sxs-lookup"><span data-stu-id="e2b81-108">Create a Ruby application</span></span>
<span data-ttu-id="e2b81-109">Para obter instruções sobre como criar um aplicativo Ruby, confira [Aplicativo Web Ruby on Rails em uma VM do Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="e2b81-109">For instructions how to create a Ruby application, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="e2b81-110">Configurar seu aplicativo para acessar o Armazenamento</span><span class="sxs-lookup"><span data-stu-id="e2b81-110">Configure your application to access Storage</span></span>
<span data-ttu-id="e2b81-111">Para usar o Armazenamento do Azure, você precisará baixar e usar o pacote do Azure para o Ruby, que inclui um conjunto de bibliotecas de conveniência que se comunicam com os serviços REST do Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e2b81-111">To use Azure Storage, you need to download and use the Ruby azure package which includes a set of convenience libraries that communicate with the Storage REST services.</span></span>

### <a name="use-rubygems-to-obtain-the-package"></a><span data-ttu-id="e2b81-112">Usar RubyGems para obter o pacote</span><span class="sxs-lookup"><span data-stu-id="e2b81-112">Use RubyGems to obtain the package</span></span>
1. <span data-ttu-id="e2b81-113">Use uma interface de linha de comando como **PowerShell** (Windows), **Terminal** (Mac) ou **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="e2b81-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="e2b81-114">Digite **gem install azure** na janela de comandos para instalar a gema e as dependências.</span><span class="sxs-lookup"><span data-stu-id="e2b81-114">Type **gem install azure** in the command window to install the gem and dependencies.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="e2b81-115">Importar o pacote</span><span class="sxs-lookup"><span data-stu-id="e2b81-115">Import the package</span></span>
<span data-ttu-id="e2b81-116">Use seu editor de texto favorito e adicione o seguinte na parte superior do arquivo do Ruby no qual você pretende usar o Armazenamento:</span><span class="sxs-lookup"><span data-stu-id="e2b81-116">Use your favorite text editor, add the following to the top of the Ruby file where you intend to use Storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="e2b81-117">Configurar uma conexão do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="e2b81-117">Set up an Azure Storage connection</span></span>
<span data-ttu-id="e2b81-118">O módulo do Azure lerá as variáveis de ambiente **AZURE\_STORAGE\_ACCOUNT** e **AZURE\_STORAGE\_ACCESS\_KEY** para obter as informações necessárias para se conectar à sua conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e2b81-118">The azure module will read the environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** for information required to connect to your Azure Storage account.</span></span> <span data-ttu-id="e2b81-119">Se essas variáveis de ambiente não estiverem definidas, você deverá especificar as informações da conta antes de usar **Azure::TableService** com o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="e2b81-119">If these environment variables are not set, you must specify the account information before using **Azure::TableService** with the following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="e2b81-120">Para obter esses valores de uma conta de armazenamento clássico ou do Resource Manager no Portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="e2b81-120">To obtain these values from a classic or Resource Manager storage account in the Azure portal:</span></span>

1. <span data-ttu-id="e2b81-121">Faça logon no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e2b81-121">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e2b81-122">Navegue até a conta de armazenamento que você deseja usar.</span><span class="sxs-lookup"><span data-stu-id="e2b81-122">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="e2b81-123">Na folha Configurações no lado direito, clique em **Chaves de Acesso**.</span><span class="sxs-lookup"><span data-stu-id="e2b81-123">In the Settings blade on the right, click **Access Keys**.</span></span>
4. <span data-ttu-id="e2b81-124">Na folha Acessar chaves exibida, você verá as teclas de acesso 1 e 2.</span><span class="sxs-lookup"><span data-stu-id="e2b81-124">In the Access keys blade that appears, you'll see the access key 1 and access key 2.</span></span> <span data-ttu-id="e2b81-125">Você pode usar qualquer uma das duas.</span><span class="sxs-lookup"><span data-stu-id="e2b81-125">You can use either of these.</span></span>
5. <span data-ttu-id="e2b81-126">Clique no ícone de cópia para copiar a chave para a área de transferência.</span><span class="sxs-lookup"><span data-stu-id="e2b81-126">Click the copy icon to copy the key to the clipboard.</span></span>

<span data-ttu-id="e2b81-127">Para obter esses valores de uma conta de armazenamento clássico no Portal Clássico do Azure:</span><span class="sxs-lookup"><span data-stu-id="e2b81-127">To obtain these values from a classic storage account in the classic Azure portal:</span></span>

1. <span data-ttu-id="e2b81-128">Faça logon no [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="e2b81-128">Log in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="e2b81-129">Navegue até a conta de armazenamento que você deseja usar.</span><span class="sxs-lookup"><span data-stu-id="e2b81-129">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="e2b81-130">Clique em **GERENCIAR CHAVES DE ACESSO** na parte inferior do painel de navegação.</span><span class="sxs-lookup"><span data-stu-id="e2b81-130">Click **MANAGE ACCESS KEYS** at the bottom of the navigation pane.</span></span>
4. <span data-ttu-id="e2b81-131">Na caixa de diálogo pop-up, você verá o nome da conta de armazenamento, a tecla de acesso primária e a tecla de acesso secundária.</span><span class="sxs-lookup"><span data-stu-id="e2b81-131">In the pop-up dialog, you'll see the storage account name, primary access key and secondary access key.</span></span> <span data-ttu-id="e2b81-132">Para a chave de acesso, você pode usar tanto a primária quanto a secundária.</span><span class="sxs-lookup"><span data-stu-id="e2b81-132">For access key, you can use either the primary one or the secondary one.</span></span>
5. <span data-ttu-id="e2b81-133">Clique no ícone de cópia para copiar a chave para a área de transferência.</span><span class="sxs-lookup"><span data-stu-id="e2b81-133">Click the copy icon to copy the key to the clipboard.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="e2b81-134">Criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="e2b81-134">Create a table</span></span>
<span data-ttu-id="e2b81-135">O objeto **Azure::TableService** permite trabalhar com tabelas e entidades.</span><span class="sxs-lookup"><span data-stu-id="e2b81-135">The **Azure::TableService** object lets you work with tables and entities.</span></span> <span data-ttu-id="e2b81-136">Para criar uma tabela, use o método **create\_table()**.</span><span class="sxs-lookup"><span data-stu-id="e2b81-136">To create a table, use the **create\_table()** method.</span></span> <span data-ttu-id="e2b81-137">O exemplo a seguir cria uma tabela ou imprime o erro, se houver.</span><span class="sxs-lookup"><span data-stu-id="e2b81-137">The following example creates a table or prints the error if there is any.</span></span>

```ruby
azure_table_service = Azure::TableService.new
begin
    azure_table_service.create_table("testtable")
rescue
    puts $!
end
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="e2b81-138">Adicionar uma entidade a uma tabela</span><span class="sxs-lookup"><span data-stu-id="e2b81-138">Add an entity to a table</span></span>
<span data-ttu-id="e2b81-139">Para adicionar uma entidade, primeiro crie um objeto hash que defina as propriedades da entidade.</span><span class="sxs-lookup"><span data-stu-id="e2b81-139">To add an entity, first create a hash object that defines your entity properties.</span></span> <span data-ttu-id="e2b81-140">É importante lembrar que, para cada entidade, você deve especificar um **PartitionKey** e um **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="e2b81-140">Note that for every entity you must specify a **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="e2b81-141">Estes são os identificadores exclusivos das entidades e são os valores que podem ser consultados muito mais rápido que as outras propriedades.</span><span class="sxs-lookup"><span data-stu-id="e2b81-141">These are the unique identifiers of your entities, and are values that can be queried much faster than your other properties.</span></span> <span data-ttu-id="e2b81-142">O Armazenamento do Azure usa **PartitionKey** para distribuir automaticamente as entidades da tabela entre vários nós de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e2b81-142">Azure Storage uses **PartitionKey** to automatically distribute the table's entities over many storage nodes.</span></span> <span data-ttu-id="e2b81-143">As entidades com o mesmo **PartitionKey** são armazenadas no mesmo nó.</span><span class="sxs-lookup"><span data-stu-id="e2b81-143">Entities with the same **PartitionKey** are stored on the same node.</span></span> <span data-ttu-id="e2b81-144">O **RowKey** é o ID exclusivo da entidade na partição à qual pertence.</span><span class="sxs-lookup"><span data-stu-id="e2b81-144">The **RowKey** is the unique ID of the entity within the partition it belongs to.</span></span>

```ruby
entity = { "content" => "test entity",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.insert_entity("testtable", entity)
```

## <a name="update-an-entity"></a><span data-ttu-id="e2b81-145">Atualizar uma entidade</span><span class="sxs-lookup"><span data-stu-id="e2b81-145">Update an entity</span></span>
<span data-ttu-id="e2b81-146">Há vários métodos disponíveis para atualizar uma entidade existente:</span><span class="sxs-lookup"><span data-stu-id="e2b81-146">There are multiple methods available to update an existing entity:</span></span>

* <span data-ttu-id="e2b81-147">**update\_entity():** atualiza uma entidade existente substituindo-a.</span><span class="sxs-lookup"><span data-stu-id="e2b81-147">**update\_entity():** Update an existing entity by replacing it.</span></span>
* <span data-ttu-id="e2b81-148">**merge\_entity():** atualiza uma entidade existente mesclando novos valores de propriedade à entidade existente.</span><span class="sxs-lookup"><span data-stu-id="e2b81-148">**merge\_entity():** Updates an existing entity by merging new property values into the existing entity.</span></span>
* <span data-ttu-id="e2b81-149">**insert\_or\_merge\_entity():** atualiza uma entidade existente substituindo-a.</span><span class="sxs-lookup"><span data-stu-id="e2b81-149">**insert\_or\_merge\_entity():** Updates an existing entity by replacing it.</span></span> <span data-ttu-id="e2b81-150">Se não existir nenhuma entidade, uma nova será inserida:</span><span class="sxs-lookup"><span data-stu-id="e2b81-150">If no entity exists, a new one will be inserted:</span></span>
* <span data-ttu-id="e2b81-151">**insert\_or\_replace\_entity():** atualiza uma entidade existente mesclando novos valores de propriedade à entidade existente.</span><span class="sxs-lookup"><span data-stu-id="e2b81-151">**insert\_or\_replace\_entity():** Updates an existing entity by merging new property values into the existing entity.</span></span> <span data-ttu-id="e2b81-152">Se nenhuma entidade existir, uma nova será inserida.</span><span class="sxs-lookup"><span data-stu-id="e2b81-152">If no entity exists, a new one will be inserted.</span></span>

<span data-ttu-id="e2b81-153">O exemplo a seguir demonstra a atualização de uma entidade usando **update\_entity()**:</span><span class="sxs-lookup"><span data-stu-id="e2b81-153">The following example demonstrates updating an entity using **update\_entity()**:</span></span>

```ruby
entity = { "content" => "test entity with updated content",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.update_entity("testtable", entity)
```

<span data-ttu-id="e2b81-154">Com **update\_entity()** e **merge\_entity()**, se a entidade que estiver sendo atualizada não existir, a operação de atualização falhará.</span><span class="sxs-lookup"><span data-stu-id="e2b81-154">With **update\_entity()** and **merge\_entity()**, if the entity that you are updating doesn't exist then the update operation will fail.</span></span> <span data-ttu-id="e2b81-155">Portanto, se desejar armazenar uma entidade independentemente de sua existência, você deverá usar **insert\_or\_replace\_entity()** ou **insert\_or\_merge\_entity()**.</span><span class="sxs-lookup"><span data-stu-id="e2b81-155">Therefore if you wish to store an entity regardless of whether it already exists, you should instead use **insert\_or\_replace\_entity()** or **insert\_or\_merge\_entity()**.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="e2b81-156">Trabalhar com grupos de entidades</span><span class="sxs-lookup"><span data-stu-id="e2b81-156">Work with groups of entities</span></span>
<span data-ttu-id="e2b81-157">Às vezes, convém enviar várias operações juntas em um lote para garantir o processamento atômico pelo servidor.</span><span class="sxs-lookup"><span data-stu-id="e2b81-157">Sometimes it makes sense to submit multiple operations together in a batch to ensure atomic processing by the server.</span></span> <span data-ttu-id="e2b81-158">Para fazer isso, você cria primeiro um objeto **Batch** e depois usa o método **execute\_batch()** em **TableService**.</span><span class="sxs-lookup"><span data-stu-id="e2b81-158">To accomplish that, you first create a **Batch** object and then use the **execute\_batch()** method on **TableService**.</span></span> <span data-ttu-id="e2b81-159">O seguinte exemplo demonstra o envio de duas entidades com RowKey 2 e 3 em um lote.</span><span class="sxs-lookup"><span data-stu-id="e2b81-159">The following example demonstrates submitting two entities with RowKey 2 and 3 in a batch.</span></span> <span data-ttu-id="e2b81-160">Observe que isso funciona apenas em entidades com o mesmo PartitionKey.</span><span class="sxs-lookup"><span data-stu-id="e2b81-160">Notice that it only works for entities with the same PartitionKey.</span></span>

```ruby
azure_table_service = Azure::TableService.new
batch = Azure::Storage::Table::Batch.new("testtable",
    "test-partition-key") do
    insert "2", { "content" => "new content 2" }
    insert "3", { "content" => "new content 3" }
end
results = azure_table_service.execute_batch(batch)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="e2b81-161">Consultar uma entidade</span><span class="sxs-lookup"><span data-stu-id="e2b81-161">Query for an entity</span></span>
<span data-ttu-id="e2b81-162">Para consultar uma entidade em uma tabela, use o método **get\_entity()**, transmitindo o nome da tabela, **PartitionKey** e **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="e2b81-162">To query an entity in a table, use the **get\_entity()** method, by passing the table name, **PartitionKey** and **RowKey**.</span></span>

```ruby
result = azure_table_service.get_entity("testtable", "test-partition-key",
    "1")
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="e2b81-163">Consultar um conjunto de entidades</span><span class="sxs-lookup"><span data-stu-id="e2b81-163">Query a set of entities</span></span>
<span data-ttu-id="e2b81-164">Para consultar um conjunto de entidades em uma tabela, crie um objeto de hash de consulta e use o método **query\_entities()**.</span><span class="sxs-lookup"><span data-stu-id="e2b81-164">To query a set of entities in a table, create a query hash object and use the **query\_entities()** method.</span></span> <span data-ttu-id="e2b81-165">O exemplo a seguir demonstra como obter todas as entidades com o mesmo **PartitionKey**:</span><span class="sxs-lookup"><span data-stu-id="e2b81-165">The following example demonstrates getting all the entities with the same **PartitionKey**:</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'" }
result, token = azure_table_service.query_entities("testtable", query)
```

> [!NOTE]
> <span data-ttu-id="e2b81-166">Se o conjunto de resultados for muito grande para ser retornado por uma única consulta, um token de continuação será retornado para que você possa usar para recuperar páginas subsequentes.</span><span class="sxs-lookup"><span data-stu-id="e2b81-166">If the result set is too large for a single query to return, a continuation token will be returned which you can use to retrieve subsequent pages.</span></span>
>
>

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="e2b81-167">consultar um subconjunto de propriedades da entidade</span><span class="sxs-lookup"><span data-stu-id="e2b81-167">Query a subset of entity properties</span></span>
<span data-ttu-id="e2b81-168">Uma consulta a uma tabela pode recuperar apenas algumas propriedades de uma entidade.</span><span class="sxs-lookup"><span data-stu-id="e2b81-168">A query to a table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="e2b81-169">Essa técnica, chamada "projeção", reduz a largura de banda e pode melhorar o desempenho da consulta, principalmente em grandes entidades.</span><span class="sxs-lookup"><span data-stu-id="e2b81-169">This technique, called "projection", reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="e2b81-170">Use a cláusula select e transmita os nomes das propriedades que você gostaria de trazer para o cliente.</span><span class="sxs-lookup"><span data-stu-id="e2b81-170">Use the select clause and pass the names of the properties you would like to bring over to the client.</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'",
    :select => ["content"] }
result, token = azure_table_service.query_entities("testtable", query)
```

## <a name="delete-an-entity"></a><span data-ttu-id="e2b81-171">Excluir uma entidade</span><span class="sxs-lookup"><span data-stu-id="e2b81-171">Delete an entity</span></span>
<span data-ttu-id="e2b81-172">Para excluir uma entidade, use o método **delete\_entity()**.</span><span class="sxs-lookup"><span data-stu-id="e2b81-172">To delete an entity, use the **delete\_entity()** method.</span></span> <span data-ttu-id="e2b81-173">Você precisa transmitir o nome da tabela que contém a entidade, a PartitionKey e a RowKey da entidade.</span><span class="sxs-lookup"><span data-stu-id="e2b81-173">You need to pass in the name of the table which contains the entity, the PartitionKey and RowKey of the entity.</span></span>

```ruby
azure_table_service.delete_entity("testtable", "test-partition-key", "1")
```

## <a name="delete-a-table"></a><span data-ttu-id="e2b81-174">Excluir uma tabela</span><span class="sxs-lookup"><span data-stu-id="e2b81-174">Delete a table</span></span>
<span data-ttu-id="e2b81-175">Para excluir uma tabela, use o método **delete\_table()** e passe o nome da tabela que você quer excluir.</span><span class="sxs-lookup"><span data-stu-id="e2b81-175">To delete a table, use the **delete\_table()** method and pass in the name of the table you want to delete.</span></span>

```ruby
azure_table_service.delete_table("testtable")
```

## <a name="next-steps"></a><span data-ttu-id="e2b81-176">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e2b81-176">Next steps</span></span>

* <span data-ttu-id="e2b81-177">[O Gerenciador de Armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) é um aplicativo autônomo e gratuito da Microsoft que possibilita o trabalho visual com os dados do Armazenamento do Azure no Windows, MacOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="e2b81-177">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="e2b81-178">[SDK do Azure para repositório Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) no GitHub</span><span class="sxs-lookup"><span data-stu-id="e2b81-178">[Azure SDK for Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

