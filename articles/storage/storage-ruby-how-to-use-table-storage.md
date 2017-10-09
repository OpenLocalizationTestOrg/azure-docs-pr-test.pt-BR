---
title: aaaHow toouse armazenamento de tabela do Azure do Ruby | Microsoft Docs
description: "Armazene dados estruturados em nuvem hello usando o armazenamento de tabela do Azure, um repositório de dados NoSQL."
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
ms.openlocfilehash: 9c77ff9f384a776c9bc075b60b351685c61acc36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-ruby"></a><span data-ttu-id="04a6b-103">Como toouse armazenamento de tabela do Azure do Ruby</span><span class="sxs-lookup"><span data-stu-id="04a6b-103">How toouse Azure Table Storage from Ruby</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="04a6b-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="04a6b-104">Overview</span></span>
<span data-ttu-id="04a6b-105">Este guia mostra como os cenários comuns de tooperform usando Olá serviço tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="04a6b-105">This guide shows you how tooperform common scenarios using hello Azure Table service.</span></span> <span data-ttu-id="04a6b-106">exemplos de saudação são gravados usando Olá Ruby API.</span><span class="sxs-lookup"><span data-stu-id="04a6b-106">hello samples are written using hello Ruby API.</span></span> <span data-ttu-id="04a6b-107">Olá cenários abordados incluem **criação e exclusão de uma tabela, inserir e consultar entidades em uma tabela**.</span><span class="sxs-lookup"><span data-stu-id="04a6b-107">hello scenarios covered include **creating and deleting a table, inserting and querying entities in a table**.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="04a6b-108">Criar um aplicativo Ruby</span><span class="sxs-lookup"><span data-stu-id="04a6b-108">Create a Ruby application</span></span>
<span data-ttu-id="04a6b-109">Para obter instruções como toocreate um aplicativo Ruby, consulte [Ruby no aplicativo Web de trilhos em uma VM do Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="04a6b-109">For instructions how toocreate a Ruby application, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="04a6b-110">Configurar o armazenamento de tooaccess do aplicativo</span><span class="sxs-lookup"><span data-stu-id="04a6b-110">Configure your application tooaccess Storage</span></span>
<span data-ttu-id="04a6b-111">toouse armazenamento do Azure, você precisa toodownload e use Olá Ruby pacote do azure que inclui um conjunto de bibliotecas de conveniência que se comunicam com serviços da REST do armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="04a6b-111">toouse Azure Storage, you need toodownload and use hello Ruby azure package which includes a set of convenience libraries that communicate with hello Storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="04a6b-112">Use o pacote de saudação do RubyGems tooobtain</span><span class="sxs-lookup"><span data-stu-id="04a6b-112">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="04a6b-113">Use uma interface de linha de comando como **PowerShell** (Windows), **Terminal** (Mac) ou **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="04a6b-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="04a6b-114">Tipo **azure de instalação de gem** gem de Olá Olá comando janela tooinstall e dependências.</span><span class="sxs-lookup"><span data-stu-id="04a6b-114">Type **gem install azure** in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="04a6b-115">Importar o pacote de saudação</span><span class="sxs-lookup"><span data-stu-id="04a6b-115">Import hello package</span></span>
<span data-ttu-id="04a6b-116">Use o editor de texto favorito, adicione Olá toohello superior de saudação arquivo Ruby onde você pretende toouse armazenamento a seguir:</span><span class="sxs-lookup"><span data-stu-id="04a6b-116">Use your favorite text editor, add hello following toohello top of hello Ruby file where you intend toouse Storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="04a6b-117">Configurar uma conexão do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="04a6b-117">Set up an Azure Storage connection</span></span>
<span data-ttu-id="04a6b-118">Olá módulo do azure lerá variáveis de ambiente Olá **AZURE\_armazenamento\_conta** e **AZURE\_armazenamento\_acesso\_chave**para obter informações necessárias a conta de armazenamento do Azure tooyour tooconnect.</span><span class="sxs-lookup"><span data-stu-id="04a6b-118">hello azure module will read hello environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** for information required tooconnect tooyour Azure Storage account.</span></span> <span data-ttu-id="04a6b-119">Se essas variáveis de ambiente não forem definidas, você deve especificar informações de conta de saudação antes de usar **Azure::TableService** com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="04a6b-119">If these environment variables are not set, you must specify hello account information before using **Azure::TableService** with hello following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="04a6b-120">tooobtain esses valores de um clássico ou Gerenciador de recursos de armazenamento de conta no hello portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="04a6b-120">tooobtain these values from a classic or Resource Manager storage account in hello Azure portal:</span></span>

1. <span data-ttu-id="04a6b-121">Faça logon no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="04a6b-121">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="04a6b-122">Navegue toohello conta de armazenamento que você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="04a6b-122">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="04a6b-123">Na folha de configurações de saudação em saudação à direita, clique em **chaves de acesso**.</span><span class="sxs-lookup"><span data-stu-id="04a6b-123">In hello Settings blade on hello right, click **Access Keys**.</span></span>
4. <span data-ttu-id="04a6b-124">Olá acesso folha de chaves que aparece, você verá a chave de acesso de saudação 1 e 2 de chave de acesso.</span><span class="sxs-lookup"><span data-stu-id="04a6b-124">In hello Access keys blade that appears, you'll see hello access key 1 and access key 2.</span></span> <span data-ttu-id="04a6b-125">Você pode usar qualquer uma das duas.</span><span class="sxs-lookup"><span data-stu-id="04a6b-125">You can use either of these.</span></span>
5. <span data-ttu-id="04a6b-126">Clique em Olá copiar ícone toocopy Olá chave toohello área de transferência.</span><span class="sxs-lookup"><span data-stu-id="04a6b-126">Click hello copy icon toocopy hello key toohello clipboard.</span></span>

<span data-ttu-id="04a6b-127">tooobtain esses valores de um armazenamento clássico contam no portal do Azure clássico de saudação:</span><span class="sxs-lookup"><span data-stu-id="04a6b-127">tooobtain these values from a classic storage account in hello classic Azure portal:</span></span>

1. <span data-ttu-id="04a6b-128">Faça logon no toohello [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="04a6b-128">Log in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="04a6b-129">Navegue toohello conta de armazenamento que você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="04a6b-129">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="04a6b-130">Clique em **gerenciar chaves de acesso** na parte inferior de Olá Olá do painel de navegação.</span><span class="sxs-lookup"><span data-stu-id="04a6b-130">Click **MANAGE ACCESS KEYS** at hello bottom of hello navigation pane.</span></span>
4. <span data-ttu-id="04a6b-131">Na caixa de diálogo pop-up hello, você verá o nome de conta de armazenamento hello, chave de acesso primária e chave de acesso secundária.</span><span class="sxs-lookup"><span data-stu-id="04a6b-131">In hello pop-up dialog, you'll see hello storage account name, primary access key and secondary access key.</span></span> <span data-ttu-id="04a6b-132">Para a chave de acesso, você pode usar Olá principal ou Olá um secundário.</span><span class="sxs-lookup"><span data-stu-id="04a6b-132">For access key, you can use either hello primary one or hello secondary one.</span></span>
5. <span data-ttu-id="04a6b-133">Clique em Olá copiar ícone toocopy Olá chave toohello área de transferência.</span><span class="sxs-lookup"><span data-stu-id="04a6b-133">Click hello copy icon toocopy hello key toohello clipboard.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="04a6b-134">Criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="04a6b-134">Create a table</span></span>
<span data-ttu-id="04a6b-135">Olá **Azure::TableService** objeto permite que você trabalhe com tabelas e entidades.</span><span class="sxs-lookup"><span data-stu-id="04a6b-135">hello **Azure::TableService** object lets you work with tables and entities.</span></span> <span data-ttu-id="04a6b-136">toocreate uma tabela, use Olá **criar\_table()** método.</span><span class="sxs-lookup"><span data-stu-id="04a6b-136">toocreate a table, use hello **create\_table()** method.</span></span> <span data-ttu-id="04a6b-137">Olá, exemplo a seguir cria uma tabela ou imprime Olá erro, se houver algum.</span><span class="sxs-lookup"><span data-stu-id="04a6b-137">hello following example creates a table or prints hello error if there is any.</span></span>

```ruby
azure_table_service = Azure::TableService.new
begin
    azure_table_service.create_table("testtable")
rescue
    puts $!
end
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="04a6b-138">Adicionar uma tabela de entidade tooa</span><span class="sxs-lookup"><span data-stu-id="04a6b-138">Add an entity tooa table</span></span>
<span data-ttu-id="04a6b-139">tooadd uma entidade, primeiro crie um objeto de hash que define as propriedades de entidade.</span><span class="sxs-lookup"><span data-stu-id="04a6b-139">tooadd an entity, first create a hash object that defines your entity properties.</span></span> <span data-ttu-id="04a6b-140">É importante lembrar que, para cada entidade, você deve especificar um **PartitionKey** e um **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="04a6b-140">Note that for every entity you must specify a **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="04a6b-141">Esses são Olá identificadores exclusivos de suas entidades e os valores que podem ser consultados muito mais rápido do que as outras propriedades.</span><span class="sxs-lookup"><span data-stu-id="04a6b-141">These are hello unique identifiers of your entities, and are values that can be queried much faster than your other properties.</span></span> <span data-ttu-id="04a6b-142">Armazenamento do Azure usa **PartitionKey** tooautomatically distribuir entidades da tabela Olá em vários nós de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="04a6b-142">Azure Storage uses **PartitionKey** tooautomatically distribute hello table's entities over many storage nodes.</span></span> <span data-ttu-id="04a6b-143">Entidades com hello mesmo **PartitionKey** são armazenados em Olá mesmo nó.</span><span class="sxs-lookup"><span data-stu-id="04a6b-143">Entities with hello same **PartitionKey** are stored on hello same node.</span></span> <span data-ttu-id="04a6b-144">Olá **RowKey** é Olá a ID exclusiva da entidade de saudação na partição Olá pertence a.</span><span class="sxs-lookup"><span data-stu-id="04a6b-144">hello **RowKey** is hello unique ID of hello entity within hello partition it belongs to.</span></span>

```ruby
entity = { "content" => "test entity",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.insert_entity("testtable", entity)
```

## <a name="update-an-entity"></a><span data-ttu-id="04a6b-145">Atualizar uma entidade</span><span class="sxs-lookup"><span data-stu-id="04a6b-145">Update an entity</span></span>
<span data-ttu-id="04a6b-146">Há vários métodos e disponível tooupdate uma entidade existente:</span><span class="sxs-lookup"><span data-stu-id="04a6b-146">There are multiple methods available tooupdate an existing entity:</span></span>

* <span data-ttu-id="04a6b-147">**update\_entity():** atualiza uma entidade existente substituindo-a.</span><span class="sxs-lookup"><span data-stu-id="04a6b-147">**update\_entity():** Update an existing entity by replacing it.</span></span>
* <span data-ttu-id="04a6b-148">**mesclagem\_entity():** atualiza uma entidade existente, mesclando novos valores de propriedade para a entidade existente hello.</span><span class="sxs-lookup"><span data-stu-id="04a6b-148">**merge\_entity():** Updates an existing entity by merging new property values into hello existing entity.</span></span>
* <span data-ttu-id="04a6b-149">**insert\_or\_merge\_entity():** atualiza uma entidade existente substituindo-a.</span><span class="sxs-lookup"><span data-stu-id="04a6b-149">**insert\_or\_merge\_entity():** Updates an existing entity by replacing it.</span></span> <span data-ttu-id="04a6b-150">Se não existir nenhuma entidade, uma nova será inserida:</span><span class="sxs-lookup"><span data-stu-id="04a6b-150">If no entity exists, a new one will be inserted:</span></span>
* <span data-ttu-id="04a6b-151">**Inserir\_ou\_substituir\_entity():** atualiza uma entidade existente, mesclando novos valores de propriedade para a entidade existente hello.</span><span class="sxs-lookup"><span data-stu-id="04a6b-151">**insert\_or\_replace\_entity():** Updates an existing entity by merging new property values into hello existing entity.</span></span> <span data-ttu-id="04a6b-152">Se nenhuma entidade existir, uma nova será inserida.</span><span class="sxs-lookup"><span data-stu-id="04a6b-152">If no entity exists, a new one will be inserted.</span></span>

<span data-ttu-id="04a6b-153">Olá exemplo a seguir demonstra a atualização de uma entidade usando **atualizar\_entity()**:</span><span class="sxs-lookup"><span data-stu-id="04a6b-153">hello following example demonstrates updating an entity using **update\_entity()**:</span></span>

```ruby
entity = { "content" => "test entity with updated content",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.update_entity("testtable", entity)
```

<span data-ttu-id="04a6b-154">Com **atualizar\_entity()** e **mesclagem\_entity()**, se a entidade Olá que você está atualizando não existir, haverá falha na operação de atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="04a6b-154">With **update\_entity()** and **merge\_entity()**, if hello entity that you are updating doesn't exist then hello update operation will fail.</span></span> <span data-ttu-id="04a6b-155">Portanto, se você quiser toostore uma entidade, independentemente se ela já existir, você deve usar **inserir\_ou\_substituir\_entity()** ou **inserir\_ou \_mesclagem\_entity()**.</span><span class="sxs-lookup"><span data-stu-id="04a6b-155">Therefore if you wish toostore an entity regardless of whether it already exists, you should instead use **insert\_or\_replace\_entity()** or **insert\_or\_merge\_entity()**.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="04a6b-156">Trabalhar com grupos de entidades</span><span class="sxs-lookup"><span data-stu-id="04a6b-156">Work with groups of entities</span></span>
<span data-ttu-id="04a6b-157">Às vezes, faz sentido toosubmit várias operações juntos em um lote tooensure atômico processamento pelo servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="04a6b-157">Sometimes it makes sense toosubmit multiple operations together in a batch tooensure atomic processing by hello server.</span></span> <span data-ttu-id="04a6b-158">tooaccomplish, criar um **lote** de objeto e, em seguida, usar Olá **executar\_batch()** método **TableService**.</span><span class="sxs-lookup"><span data-stu-id="04a6b-158">tooaccomplish that, you first create a **Batch** object and then use hello **execute\_batch()** method on **TableService**.</span></span> <span data-ttu-id="04a6b-159">Olá exemplo a seguir demonstra enviando duas entidades com RowKey 2 e 3 em um lote.</span><span class="sxs-lookup"><span data-stu-id="04a6b-159">hello following example demonstrates submitting two entities with RowKey 2 and 3 in a batch.</span></span> <span data-ttu-id="04a6b-160">Observe que ele somente funciona para entidades com hello mesmo PartitionKey.</span><span class="sxs-lookup"><span data-stu-id="04a6b-160">Notice that it only works for entities with hello same PartitionKey.</span></span>

```ruby
azure_table_service = Azure::TableService.new
batch = Azure::Storage::Table::Batch.new("testtable",
    "test-partition-key") do
    insert "2", { "content" => "new content 2" }
    insert "3", { "content" => "new content 3" }
end
results = azure_table_service.execute_batch(batch)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="04a6b-161">Consultar uma entidade</span><span class="sxs-lookup"><span data-stu-id="04a6b-161">Query for an entity</span></span>
<span data-ttu-id="04a6b-162">tooquery uma entidade em uma tabela, use Olá **obter\_entity()** método, passando o nome da tabela hello, **PartitionKey** e **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="04a6b-162">tooquery an entity in a table, use hello **get\_entity()** method, by passing hello table name, **PartitionKey** and **RowKey**.</span></span>

```ruby
result = azure_table_service.get_entity("testtable", "test-partition-key",
    "1")
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="04a6b-163">Consultar um conjunto de entidades</span><span class="sxs-lookup"><span data-stu-id="04a6b-163">Query a set of entities</span></span>
<span data-ttu-id="04a6b-164">tooquery um conjunto de entidades em uma tabela, crie um objeto de hash de consulta e use Olá **consulta\_entities()** método.</span><span class="sxs-lookup"><span data-stu-id="04a6b-164">tooquery a set of entities in a table, create a query hash object and use hello **query\_entities()** method.</span></span> <span data-ttu-id="04a6b-165">Olá exemplo a seguir demonstra obtendo todas as entidades de saudação com hello mesmo **PartitionKey**:</span><span class="sxs-lookup"><span data-stu-id="04a6b-165">hello following example demonstrates getting all hello entities with hello same **PartitionKey**:</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'" }
result, token = azure_table_service.query_entities("testtable", query)
```

> [!NOTE]
> <span data-ttu-id="04a6b-166">Se o conjunto de resultados de saudação é muito grande para uma única consulta tooreturn, um token de continuação será retornado que você pode usar as páginas subsequentes tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="04a6b-166">If hello result set is too large for a single query tooreturn, a continuation token will be returned which you can use tooretrieve subsequent pages.</span></span>
>
>

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="04a6b-167">consultar um subconjunto de propriedades da entidade</span><span class="sxs-lookup"><span data-stu-id="04a6b-167">Query a subset of entity properties</span></span>
<span data-ttu-id="04a6b-168">Uma tabela de consulta tooa pode recuperar apenas algumas propriedades de uma entidade.</span><span class="sxs-lookup"><span data-stu-id="04a6b-168">A query tooa table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="04a6b-169">Essa técnica, chamada "projeção", reduz a largura de banda e pode melhorar o desempenho da consulta, principalmente em grandes entidades.</span><span class="sxs-lookup"><span data-stu-id="04a6b-169">This technique, called "projection", reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="04a6b-170">Cláusula select de saudação de uso e os nomes de saudação de passagem de Olá propriedades que você gostaria que toobring sobre toohello cliente.</span><span class="sxs-lookup"><span data-stu-id="04a6b-170">Use hello select clause and pass hello names of hello properties you would like toobring over toohello client.</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'",
    :select => ["content"] }
result, token = azure_table_service.query_entities("testtable", query)
```

## <a name="delete-an-entity"></a><span data-ttu-id="04a6b-171">Excluir uma entidade</span><span class="sxs-lookup"><span data-stu-id="04a6b-171">Delete an entity</span></span>
<span data-ttu-id="04a6b-172">toodelete uma entidade, use Olá **excluir\_entity()** método.</span><span class="sxs-lookup"><span data-stu-id="04a6b-172">toodelete an entity, use hello **delete\_entity()** method.</span></span> <span data-ttu-id="04a6b-173">É necessário toopass no nome de saudação da tabela de saudação que contém a entidade hello, Olá PartitionKey e RowKey da entidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="04a6b-173">You need toopass in hello name of hello table which contains hello entity, hello PartitionKey and RowKey of hello entity.</span></span>

```ruby
azure_table_service.delete_entity("testtable", "test-partition-key", "1")
```

## <a name="delete-a-table"></a><span data-ttu-id="04a6b-174">Excluir uma tabela</span><span class="sxs-lookup"><span data-stu-id="04a6b-174">Delete a table</span></span>
<span data-ttu-id="04a6b-175">toodelete uma tabela, use Olá **excluir\_table()** método e passar no nome de saudação do hello tabela que você deseja toodelete.</span><span class="sxs-lookup"><span data-stu-id="04a6b-175">toodelete a table, use hello **delete\_table()** method and pass in hello name of hello table you want toodelete.</span></span>

```ruby
azure_table_service.delete_table("testtable")
```

## <a name="next-steps"></a><span data-ttu-id="04a6b-176">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="04a6b-176">Next steps</span></span>

* <span data-ttu-id="04a6b-177">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) é um aplicativo autônomo gratuito da Microsoft que permite que você toowork visualmente com dados de armazenamento do Azure no Linux, Windows e macOS.</span><span class="sxs-lookup"><span data-stu-id="04a6b-177">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="04a6b-178">[SDK do Azure para repositório Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) no GitHub</span><span class="sxs-lookup"><span data-stu-id="04a6b-178">[Azure SDK for Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

