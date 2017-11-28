---
title: Como usar o Armazenamento de Tabelas do Azure por meio do Node.js | Microsoft Docs
description: "Armazene dados estruturados na nuvem usando o Armazenamento de Tabelas do Azure, um repositório de dados NoSQL."
services: storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: fc2e33d2-c5da-4861-8503-53fdc25750de
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: f004408910aecc380e20f7da54dbd155d179aaa5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-table-storage-from-nodejs"></a><span data-ttu-id="4f893-103">Como usar o armazenamento de Tabela do Azure por meio do Node.js</span><span class="sxs-lookup"><span data-stu-id="4f893-103">How to use Azure Table storage from Node.js</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="4f893-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="4f893-104">Overview</span></span>
<span data-ttu-id="4f893-105">Este tópico mostra como executar cenários comuns usando o serviço Tabela do Azure em um aplicativo do Node.js.</span><span class="sxs-lookup"><span data-stu-id="4f893-105">This topic shows how to perform common scenarios using the Azure Table service in a Node.js application.</span></span>

<span data-ttu-id="4f893-106">Os exemplos de código neste tópico pressupõem que você já tenha um aplicativo do Node.js.</span><span class="sxs-lookup"><span data-stu-id="4f893-106">The code examples in this topic assume you already have a Node.js application.</span></span> <span data-ttu-id="4f893-107">Para obter informações sobre como criar um aplicativo do Node.js no Azure, confira um destes tópicos:</span><span class="sxs-lookup"><span data-stu-id="4f893-107">For information about how to create a Node.js application in Azure, see any of these topics:</span></span>

* [<span data-ttu-id="4f893-108">Criar um aplicativo Web do Node.js no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="4f893-108">Create a Node.js web app in Azure App Service</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="4f893-109">Criar e implantar um aplicativo Web Node.js no Azure usando o WebMatrix</span><span class="sxs-lookup"><span data-stu-id="4f893-109">Build and deploy a Node.js web app to Azure using WebMatrix</span></span>](../app-service-web/web-sites-nodejs-use-webmatrix.md)
* <span data-ttu-id="4f893-110">[Criar e implantar um aplicativo Node.js para um serviço de nuvem do AzureServiço de nuvem do Node.js](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (usando o Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="4f893-110">[Build and deploy a Node.js application to an Azure Cloud Service](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (using Windows PowerShell)</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="configure-your-application-to-access-azure-storage"></a><span data-ttu-id="4f893-111">Configurar seu aplicativo para acessar o Armazenamento de Blob</span><span class="sxs-lookup"><span data-stu-id="4f893-111">Configure your application to access Azure Storage</span></span>
<span data-ttu-id="4f893-112">Para usar o Armazenamento do Azure, você precisa do SDK do Armazenamento do Azure para Node.js, que inclui um conjunto de bibliotecas de conveniência que se comunicam com os serviços REST do armazenamento.</span><span class="sxs-lookup"><span data-stu-id="4f893-112">To use Azure Storage, you need the Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-node-package-manager-npm-to-install-the-package"></a><span data-ttu-id="4f893-113">Usar o NPM (Gerenciador de Pacotes de Nós) para obter o pacote</span><span class="sxs-lookup"><span data-stu-id="4f893-113">Use Node Package Manager (NPM) to install the package</span></span>
1. <span data-ttu-id="4f893-114">Use uma interface de linha de comando, como **PowerShell** (Windows), **Terminal** (Mac) ou **Bash** (Unix), e navegue até a pasta em que você criou o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4f893-114">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), and navigate to the folder where you created your application.</span></span>
2. <span data-ttu-id="4f893-115">Digite **npm install azure-storage** na janela de comando.</span><span class="sxs-lookup"><span data-stu-id="4f893-115">Type **npm install azure-storage** in the command window.</span></span> <span data-ttu-id="4f893-116">A saída do comando é semelhante ao exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="4f893-116">Output from the command is similar to the following example.</span></span>

       azure-storage@0.5.0 node_modules\azure-storage
       +-- extend@1.2.1
       +-- xmlbuilder@0.4.3
       +-- mime@1.2.11
       +-- node-uuid@1.4.3
       +-- validator@3.22.2
       +-- underscore@1.4.4
       +-- readable-stream@1.0.33 (string_decoder@0.10.31, isarray@0.0.1, inherits@2.0.1, core-util-is@1.0.1)
       +-- xml2js@0.2.7 (sax@0.5.2)
       +-- request@2.57.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, bl@0.9.4, combined-stream@1.0.5, qs@3.1.0, mime-types@2.0.14, form-data@0.2.0, http-signature@0.11.0, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
3. <span data-ttu-id="4f893-117">Você pode executar manualmente o comando **ls** para verificar se uma pasta **node\_modules** foi criada.</span><span class="sxs-lookup"><span data-stu-id="4f893-117">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="4f893-118">Dentro dessa pasta, você encontrará o pacote **azure-storage** que contém as bibliotecas necessárias para acessar o armazenamento.</span><span class="sxs-lookup"><span data-stu-id="4f893-118">Inside that folder you will find the **azure-storage** package, which contains the libraries you need to access storage.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="4f893-119">Importar o pacote</span><span class="sxs-lookup"><span data-stu-id="4f893-119">Import the package</span></span>
<span data-ttu-id="4f893-120">Adicione o código a seguir à parte superior do arquivo **server.js** em seu aplicativo:</span><span class="sxs-lookup"><span data-stu-id="4f893-120">Add the following code to the top of the **server.js** file in your application:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="4f893-121">Configurar uma conexão do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="4f893-121">Set up an Azure Storage connection</span></span>
<span data-ttu-id="4f893-122">O módulo do Azure lerá as variáveis de ambiente AZURE\_STORAGE\_ACCOUNT e AZURE\_STORAGE\_ACCESS\_KEY ou AZURE\_STORAGE\_CONNECTION\_STRING para obter as informações necessárias para se conectar à sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="4f893-122">The azure module will read the environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="4f893-123">Se essas variáveis de ambiente não estiverem definidas, você deverá especificar as informações da conta ao chamar **TableService**.</span><span class="sxs-lookup"><span data-stu-id="4f893-123">If these environment variables are not set, you must specify the account information when calling **TableService**.</span></span>

<span data-ttu-id="4f893-124">Para obter um exemplo de como definir as variáveis de ambiente no [portal do Azure](https://portal.azure.com) para um Site do Azure, consulte [Aplicativo Web Node.js com o Serviço Tabela do Azure](../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="4f893-124">For an example of setting the environment variables in the [Azure portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using the Azure Table Service](../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span></span>

## <a name="create-a-table"></a><span data-ttu-id="4f893-125">Criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="4f893-125">Create a table</span></span>
<span data-ttu-id="4f893-126">O código a seguir cria um objeto **TableService** e utiliza-o para criar uma nova tabela.</span><span class="sxs-lookup"><span data-stu-id="4f893-126">The following code creates a **TableService** object and uses it to create a new table.</span></span> <span data-ttu-id="4f893-127">Adicione o seguinte próximo à parte superior do **server.js**.</span><span class="sxs-lookup"><span data-stu-id="4f893-127">Add the following near the top of **server.js**.</span></span>

```nodejs
var tableSvc = azure.createTableService();
```

<span data-ttu-id="4f893-128">A chamada para **createTableIfNotExists** criará uma nova tabela com o nome especificado, se ela ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="4f893-128">The call to **createTableIfNotExists** will create a new table with the specified name if it does not already exist.</span></span> <span data-ttu-id="4f893-129">O exemplo a seguir criará uma nova tabela denominada 'mytable' se ele ainda não existir:</span><span class="sxs-lookup"><span data-stu-id="4f893-129">The following example creates a new table named 'mytable' if it does not already exist:</span></span>

```nodejs
tableSvc.createTableIfNotExists('mytable', function(error, result, response){
  if(!error){
    // Table exists or created
  }
});
```

<span data-ttu-id="4f893-130">O `result.created` será `true` se uma nova tabela for criada e `false` se a tabela já existir.</span><span class="sxs-lookup"><span data-stu-id="4f893-130">The `result.created` will be `true` if a new table is created, and `false` if the table already exists.</span></span> <span data-ttu-id="4f893-131">O `response` conterá informações sobre a solicitação.</span><span class="sxs-lookup"><span data-stu-id="4f893-131">The `response` will contain information about the request.</span></span>

### <a name="filters"></a><span data-ttu-id="4f893-132">Filtros</span><span class="sxs-lookup"><span data-stu-id="4f893-132">Filters</span></span>
<span data-ttu-id="4f893-133">É possível aplicar operações de filtragem opcionais às operações executadas usando **TableService**.</span><span class="sxs-lookup"><span data-stu-id="4f893-133">Optional filtering operations can be applied to operations performed using **TableService**.</span></span> <span data-ttu-id="4f893-134">As operações de filtragem podem incluir registro em log, repetição automática, etc. Os filtros são objetos que implementam um método com a assinatura:</span><span class="sxs-lookup"><span data-stu-id="4f893-134">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="4f893-135">Depois de fazer seu pré-processamento nas opções de solicitação, o método precisará chamar "next", transmitindo um retorno de chamada com a seguinte assinatura:</span><span class="sxs-lookup"><span data-stu-id="4f893-135">After doing its preprocessing on the request options, the method needs to call "next", passing a callback with the following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="4f893-136">Nesse retorno de chamada, e depois de processar o returnObject (a resposta da solicitação ao servidor), o retorno de chamada precisará invocar “next”, se ele existir, para continuar processando outros filtros ou simplesmente invocar finalCallback para terminar a invocação de serviço.</span><span class="sxs-lookup"><span data-stu-id="4f893-136">In this callback, and after processing the returnObject (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or simply invoke finalCallback otherwise to end the service invocation.</span></span>

<span data-ttu-id="4f893-137">Dois filtros que implementam a lógica de repetição estão incluídos no SDK do Azure para Node.js, **ExponentialRetryPolicyFilter** e **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="4f893-137">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="4f893-138">O seguinte código cria um objeto **TableService** que usa o **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="4f893-138">The following creates a **TableService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var tableSvc = azure.createTableService().withFilter(retryOperations);
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="4f893-139">Adicionar uma entidade a uma tabela</span><span class="sxs-lookup"><span data-stu-id="4f893-139">Add an entity to a table</span></span>
<span data-ttu-id="4f893-140">Para adicionar uma entidade, primeiro crie um objeto que defina as propriedades da entidade.</span><span class="sxs-lookup"><span data-stu-id="4f893-140">To add an entity, first create an object that defines your entity properties.</span></span> <span data-ttu-id="4f893-141">Todas as entidades devem conter uma **PartitionKey** e **RowKey**, que são identificadores exclusivos da entidade.</span><span class="sxs-lookup"><span data-stu-id="4f893-141">All entities must contain a **PartitionKey** and **RowKey**, which are unique identifiers for the entity.</span></span>

* <span data-ttu-id="4f893-142">**PartitionKey** – determina a partição em que a entidade está armazenada</span><span class="sxs-lookup"><span data-stu-id="4f893-142">**PartitionKey** - determines the partition that the entity is stored in</span></span>
* <span data-ttu-id="4f893-143">**RowKey** – identifica exclusivamente a entidade dentro da partição</span><span class="sxs-lookup"><span data-stu-id="4f893-143">**RowKey** - uniquely identifies the entity within the partition</span></span>

<span data-ttu-id="4f893-144">Ambas, **PartitionKey** e **RowKey**, devem ser valores de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="4f893-144">Both **PartitionKey** and **RowKey** must be string values.</span></span> <span data-ttu-id="4f893-145">Para obter informações, consulte [Noções básicas sobre o modelo de dados do serviço Tabela](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="4f893-145">For more information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="4f893-146">A seguir, um exemplo de definição de uma entidade.</span><span class="sxs-lookup"><span data-stu-id="4f893-146">The following is an example of defining an entity.</span></span> <span data-ttu-id="4f893-147">Observe que **dueDate** é definido com um tipo de **Edm.DateTime**.</span><span class="sxs-lookup"><span data-stu-id="4f893-147">Note that **dueDate** is defined as a type of **Edm.DateTime**.</span></span> <span data-ttu-id="4f893-148">A especificação do tipo é opcional, e os tipos serão inferidos se não especificados.</span><span class="sxs-lookup"><span data-stu-id="4f893-148">Specifying the type is optional, and types will be inferred if not specified.</span></span>

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'take out the trash'},
  dueDate: {'_':new Date(2015, 6, 20), '$':'Edm.DateTime'}
};
```

> [!NOTE]
> <span data-ttu-id="4f893-149">Existe também um campo **Carimbo de Data/Hora** para cada registro, que é definido pelo Azure quando uma entidade é inserida ou atualizada.</span><span class="sxs-lookup"><span data-stu-id="4f893-149">There is also a **Timestamp** field for each record, which is set by Azure when an entity is inserted or updated.</span></span>
>
>

<span data-ttu-id="4f893-150">Você também pode usar o **entityGenerator** para criar entidades.</span><span class="sxs-lookup"><span data-stu-id="4f893-150">You can also use the **entityGenerator** to create entities.</span></span> <span data-ttu-id="4f893-151">O exemplo a seguir cria a mesma entidade tarefa usando o **entityGenerator**.</span><span class="sxs-lookup"><span data-stu-id="4f893-151">The following example creates the same task entity using the **entityGenerator**.</span></span>

```nodejs
var entGen = azure.TableUtilities.entityGenerator;
var task = {
  PartitionKey: entGen.String('hometasks'),
  RowKey: entGen.String('1'),
  description: entGen.String('take out the trash'),
  dueDate: entGen.DateTime(new Date(Date.UTC(2015, 6, 20))),
};
```

<span data-ttu-id="4f893-152">Para adicionar uma entidade à sua tabela, passe o objeto de entidade para o método **insertEntity** .</span><span class="sxs-lookup"><span data-stu-id="4f893-152">To add an entity to your table, pass the entity object to the **insertEntity** method.</span></span>

```nodejs
tableSvc.insertEntity('mytable',task, function (error, result, response) {
  if(!error){
    // Entity inserted
  }
});
```

<span data-ttu-id="4f893-153">Se a operação for bem-sucedida, `result` conterá a [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) do registro inserido e `response` conterá informações sobre a operação.</span><span class="sxs-lookup"><span data-stu-id="4f893-153">If the operation is successful, `result` will contain the [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) of the inserted record and `response` will contain information about the operation.</span></span>

<span data-ttu-id="4f893-154">Resposta de exemplo:</span><span class="sxs-lookup"><span data-stu-id="4f893-154">Example response:</span></span>

```nodejs
{ '.metadata': { etag: 'W/"datetime\'2015-02-25T01%3A22%3A22.5Z\'"' } }
```

> [!NOTE]
> <span data-ttu-id="4f893-155">Por padrão, **insertEntity** não retorna a entidade inserida como parte da informação de `response`.</span><span class="sxs-lookup"><span data-stu-id="4f893-155">By default, **insertEntity** does not return the inserted entity as part of the `response` information.</span></span> <span data-ttu-id="4f893-156">Se você planeja executar outras operações nessa entidade ou se desejar armazenar as informações em cache, pode ser útil retorná-las como parte de `result`.</span><span class="sxs-lookup"><span data-stu-id="4f893-156">If you plan on performing other operations on this entity, or wish to cache the information, it can be useful to have it returned as part of the `result`.</span></span> <span data-ttu-id="4f893-157">Você pode fazer isso habilitando **echoContent** da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="4f893-157">You can do this by enabling **echoContent** as follows:</span></span>
>
> `tableSvc.insertEntity('mytable', task, {echoContent: true}, function (error, result, response) {...}`
>
>

## <a name="update-an-entity"></a><span data-ttu-id="4f893-158">Atualizar uma entidade</span><span class="sxs-lookup"><span data-stu-id="4f893-158">Update an entity</span></span>
<span data-ttu-id="4f893-159">Há vários métodos disponíveis para atualizar uma entidade existente:</span><span class="sxs-lookup"><span data-stu-id="4f893-159">There are multiple methods available to update an existing entity:</span></span>

* <span data-ttu-id="4f893-160">**replaceEntity** – atualiza uma entidade existente ao substituí-la</span><span class="sxs-lookup"><span data-stu-id="4f893-160">**replaceEntity** - updates an existing entity by replacing it</span></span>
* <span data-ttu-id="4f893-161">**mergeEntity** – atualiza uma entidade existente mesclando novos valores de propriedade à entidade existente</span><span class="sxs-lookup"><span data-stu-id="4f893-161">**mergeEntity** - updates an existing entity by merging new property values into the existing entity</span></span>
* <span data-ttu-id="4f893-162">**insertOrReplaceEntity** – atualiza uma entidade existente substituindo-a.</span><span class="sxs-lookup"><span data-stu-id="4f893-162">**insertOrReplaceEntity** - updates an existing entity by replacing it.</span></span> <span data-ttu-id="4f893-163">Se não existir nenhuma entidade, uma nova será inserida</span><span class="sxs-lookup"><span data-stu-id="4f893-163">If no entity exists, a new one will be inserted</span></span>
* <span data-ttu-id="4f893-164">**insertOrMergeEntity** – atualiza uma entidade existente mesclando novos valores de propriedade à existente.</span><span class="sxs-lookup"><span data-stu-id="4f893-164">**insertOrMergeEntity** - updates an existing entity by merging new property values into the existing.</span></span> <span data-ttu-id="4f893-165">Se não existir nenhuma entidade, uma nova será inserida</span><span class="sxs-lookup"><span data-stu-id="4f893-165">If no entity exists, a new one will be inserted</span></span>

<span data-ttu-id="4f893-166">O exemplo a seguir demonstra a atualização de uma entidade usando **replaceEntity**:</span><span class="sxs-lookup"><span data-stu-id="4f893-166">The following example demonstrates updating an entity using **replaceEntity**:</span></span>

```nodejs
tableSvc.replaceEntity('mytable', updatedTask, function(error, result, response){
  if(!error) {
    // Entity updated
  }
});
```

> [!NOTE]
> <span data-ttu-id="4f893-167">Por padrão, a atualização de uma entidade não verifica se os dados que estão sendo atualizados foram modificados anteriormente por outro processo.</span><span class="sxs-lookup"><span data-stu-id="4f893-167">By default, updating an entity does not check to see if the data being updated has previously been modified by another process.</span></span> <span data-ttu-id="4f893-168">Para suporte a atualizações simultâneas:</span><span class="sxs-lookup"><span data-stu-id="4f893-168">To support concurrent updates:</span></span>
>
> 1. <span data-ttu-id="4f893-169">Obtenha a ETag do objeto que está sendo atualizado.</span><span class="sxs-lookup"><span data-stu-id="4f893-169">Get the ETag of the object being updated.</span></span> <span data-ttu-id="4f893-170">Isso é retornado como parte de `response` para qualquer operação relacionada à entidade e pode ser recuperado por meio de `response['.metadata'].etag`.</span><span class="sxs-lookup"><span data-stu-id="4f893-170">This is returned as part of the `response` for any entity-related operation and can be retrieved through `response['.metadata'].etag`.</span></span>
> 2. <span data-ttu-id="4f893-171">Ao realizar uma operação de atualização em uma entidade, adicione as informações de ETag obtidas anteriormente para a nova entidade.</span><span class="sxs-lookup"><span data-stu-id="4f893-171">When performing an update operation on an entity, add the ETag information previously retrieved to the new entity.</span></span> <span data-ttu-id="4f893-172">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="4f893-172">For example:</span></span>
>
>       <span data-ttu-id="4f893-173">entity2['.metadata'].etag = currentEtag;</span><span class="sxs-lookup"><span data-stu-id="4f893-173">entity2['.metadata'].etag = currentEtag;</span></span>
> 3. <span data-ttu-id="4f893-174">Realize a operação de atualização.</span><span class="sxs-lookup"><span data-stu-id="4f893-174">Perform the update operation.</span></span> <span data-ttu-id="4f893-175">Se a entidade foi modificada desde a recuperação do valor de ETag, como outra instância do seu aplicativo, um `error` será retornado informando que a condição da atualização especificada na solicitação não foi atendida.</span><span class="sxs-lookup"><span data-stu-id="4f893-175">If the entity has been modified since you retrieved the ETag value, such as another instance of your application, an `error` will be returned stating that the update condition specified in the request was not satisfied.</span></span>
>
>

<span data-ttu-id="4f893-176">Com **replaceEntity** e **mergeEntity**, se a entidade que estiver sendo atualizada não existir, a operação de atualização falhará.</span><span class="sxs-lookup"><span data-stu-id="4f893-176">With **replaceEntity** and **mergeEntity**, if the entity that is being updated doesn't exist, then the update operation will fail.</span></span> <span data-ttu-id="4f893-177">Portanto, se desejar armazenar uma entidade independentemente de sua existência, use **insertOrReplaceEntity** ou **insertOrMergeEntity**.</span><span class="sxs-lookup"><span data-stu-id="4f893-177">Therefore if you wish to store an entity regardless of whether it already exists, use **insertOrReplaceEntity** or **insertOrMergeEntity**.</span></span>

<span data-ttu-id="4f893-178">O `result` para operações de atualização de sucesso conterá **Etag** da entidade atualizada.</span><span class="sxs-lookup"><span data-stu-id="4f893-178">The `result` for successful update operations will contain the **Etag** of the updated entity.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="4f893-179">Trabalhar com grupos de entidades</span><span class="sxs-lookup"><span data-stu-id="4f893-179">Work with groups of entities</span></span>
<span data-ttu-id="4f893-180">Às vezes, convém enviar várias operações juntas em um lote para garantir o processamento atômico pelo servidor.</span><span class="sxs-lookup"><span data-stu-id="4f893-180">Sometimes it makes sense to submit multiple operations together in a batch to ensure atomic processing by the server.</span></span> <span data-ttu-id="4f893-181">Para fazer isso, use a classe **TableBatch** para criar um lote; em seguida, use o método **executeBatch** de **TableService** para executar as operações em lote.</span><span class="sxs-lookup"><span data-stu-id="4f893-181">To accomplish that, use the **TableBatch** class to create a batch, and then use the **executeBatch** method of **TableService** to perform the batched operations.</span></span>

 <span data-ttu-id="4f893-182">O exemplo a seguir demonstra o envio de duas entidades em um lote:</span><span class="sxs-lookup"><span data-stu-id="4f893-182">The following example demonstrates submitting two entities in a batch:</span></span>

```nodejs
var task1 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'Take out the trash'},
  dueDate: {'_':new Date(2015, 6, 20)}
};
var task2 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '2'},
  description: {'_':'Wash the dishes'},
  dueDate: {'_':new Date(2015, 6, 20)}
};

var batch = new azure.TableBatch();

batch.insertEntity(task1, {echoContent: true});
batch.insertEntity(task2, {echoContent: true});

tableSvc.executeBatch('mytable', batch, function (error, result, response) {
  if(!error) {
    // Batch completed
  }
});
```

<span data-ttu-id="4f893-183">Para operações em lote bem-sucedidas, `result` conterá informações para cada operação no lote.</span><span class="sxs-lookup"><span data-stu-id="4f893-183">For successful batch operations, `result` will contain information for each operation in the batch.</span></span>

### <a name="work-with-batched-operations"></a><span data-ttu-id="4f893-184">Trabalhando com operações em lote</span><span class="sxs-lookup"><span data-stu-id="4f893-184">Work with batched operations</span></span>
<span data-ttu-id="4f893-185">Operações adicionadas ao lote podem ser inspecionadas ao exibir a propriedade `operations` .</span><span class="sxs-lookup"><span data-stu-id="4f893-185">Operations added to a batch can be inspected by viewing the `operations` property.</span></span> <span data-ttu-id="4f893-186">Você também pode usar os seguintes métodos para trabalhar com as operações:</span><span class="sxs-lookup"><span data-stu-id="4f893-186">You can also use the following methods to work with operations:</span></span>

* <span data-ttu-id="4f893-187">**clear** – limpa todas as operações de um lote.</span><span class="sxs-lookup"><span data-stu-id="4f893-187">**clear** - clears all operations from a batch</span></span>
* <span data-ttu-id="4f893-188">**getOperations** – obtém uma operação do lote</span><span class="sxs-lookup"><span data-stu-id="4f893-188">**getOperations** - gets an operation from the batch</span></span>
* <span data-ttu-id="4f893-189">**hasOperations** – retorna true se o lote contiver operações</span><span class="sxs-lookup"><span data-stu-id="4f893-189">**hasOperations** - returns true if the batch contains operations</span></span>
* <span data-ttu-id="4f893-190">**removeOperations** – remove uma operação</span><span class="sxs-lookup"><span data-stu-id="4f893-190">**removeOperations** - removes an operation</span></span>
* <span data-ttu-id="4f893-191">**size** – retorna o número de operações no lote</span><span class="sxs-lookup"><span data-stu-id="4f893-191">**size** - returns the number of operations in the batch</span></span>

## <a name="retrieve-an-entity-by-key"></a><span data-ttu-id="4f893-192">Recuperar uma entidade por chave</span><span class="sxs-lookup"><span data-stu-id="4f893-192">Retrieve an entity by key</span></span>
<span data-ttu-id="4f893-193">Para retornar uma entidade específica com base em **PartitionKey** e **RowKey**, use o método **retrieveEntity**.</span><span class="sxs-lookup"><span data-stu-id="4f893-193">To return a specific entity based on the **PartitionKey** and **RowKey**, use the **retrieveEntity** method.</span></span>

```nodejs
tableSvc.retrieveEntity('mytable', 'hometasks', '1', function(error, result, response){
  if(!error){
    // result contains the entity
  }
});
```

<span data-ttu-id="4f893-194">Quando essa operação for concluída, `result` conterá a entidade.</span><span class="sxs-lookup"><span data-stu-id="4f893-194">Once this operation is complete, `result` will contain the entity.</span></span>

## <a name="query-a-set-of-entities"></a><span data-ttu-id="4f893-195">Consultar um conjunto de entidades</span><span class="sxs-lookup"><span data-stu-id="4f893-195">Query a set of entities</span></span>
<span data-ttu-id="4f893-196">Para consultar uma tabela, utilize o objeto **TableQuery** para compilar uma expressão de consulta utilizando as seguintes cláusulas:</span><span class="sxs-lookup"><span data-stu-id="4f893-196">To query a table, use the **TableQuery** object to build up a query expression using the following clauses:</span></span>

* <span data-ttu-id="4f893-197">**select** – os campos a serem retornados da consulta</span><span class="sxs-lookup"><span data-stu-id="4f893-197">**select** - the fields to be returned from the query</span></span>
* <span data-ttu-id="4f893-198">**where** – a cláusula “where”</span><span class="sxs-lookup"><span data-stu-id="4f893-198">**where** - the where clause</span></span>

  * <span data-ttu-id="4f893-199">**and** – uma condição where `and`</span><span class="sxs-lookup"><span data-stu-id="4f893-199">**and** - an `and` where condition</span></span>
  * <span data-ttu-id="4f893-200">**or** – uma condição where `or`</span><span class="sxs-lookup"><span data-stu-id="4f893-200">**or** - an `or` where condition</span></span>
* <span data-ttu-id="4f893-201">**top** – o número de itens a serem buscados</span><span class="sxs-lookup"><span data-stu-id="4f893-201">**top** - the number of items to fetch</span></span>

<span data-ttu-id="4f893-202">O exemplo a seguir compila uma consulta que retornará os cinco principais itens com uma PartitionKey de “hometasks”.</span><span class="sxs-lookup"><span data-stu-id="4f893-202">The following example builds a query that will return the top five items with a PartitionKey of 'hometasks'.</span></span>

```nodejs
var query = new azure.TableQuery()
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

<span data-ttu-id="4f893-203">Como **select** não é usado, todos os campos serão retornados.</span><span class="sxs-lookup"><span data-stu-id="4f893-203">Since **select** is not used, all fields will be returned.</span></span> <span data-ttu-id="4f893-204">Para realizar a consulta em uma tabela, use **queryEntities**.</span><span class="sxs-lookup"><span data-stu-id="4f893-204">To perform the query against a table, use **queryEntities**.</span></span> <span data-ttu-id="4f893-205">O exemplo a seguir usa essa consulta para retornar entidades de 'mytable'.</span><span class="sxs-lookup"><span data-stu-id="4f893-205">The following example uses this query to return entities from 'mytable'.</span></span>

```nodejs
tableSvc.queryEntities('mytable',query, null, function(error, result, response) {
  if(!error) {
    // query was successful
  }
});
```

<span data-ttu-id="4f893-206">Se for bem-sucedido, `result.entries` conterá uma matriz de entidades que correspondem à consulta.</span><span class="sxs-lookup"><span data-stu-id="4f893-206">If successful, `result.entries` will contain an array of entities that match the query.</span></span> <span data-ttu-id="4f893-207">Se a consulta não tiver sido capaz de retornar todas as entidades, `result.continuationToken` não será*null* e poderá ser usado como terceiro parâmetro de **queryEntities** para recuperar mais resultados.</span><span class="sxs-lookup"><span data-stu-id="4f893-207">If the query was unable to return all entities, `result.continuationToken` will be non-*null* and can be used as the third parameter of **queryEntities** to retrieve more results.</span></span> <span data-ttu-id="4f893-208">Para a consulta inicial, use *null* como o terceiro parâmetro.</span><span class="sxs-lookup"><span data-stu-id="4f893-208">For the initial query, use *null* for the third parameter.</span></span>

### <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="4f893-209">consultar um subconjunto de propriedades da entidade</span><span class="sxs-lookup"><span data-stu-id="4f893-209">Query a subset of entity properties</span></span>
<span data-ttu-id="4f893-210">Uma consulta a uma tabela pode recuperar apenas alguns campos de uma entidade.</span><span class="sxs-lookup"><span data-stu-id="4f893-210">A query to a table can retrieve just a few fields from an entity.</span></span>
<span data-ttu-id="4f893-211">Isso reduz a largura de banda e pode melhorar o desempenho da consulta, principalmente em grandes entidades.</span><span class="sxs-lookup"><span data-stu-id="4f893-211">This reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="4f893-212">Use a cláusula **select** e transmita os nomes dos campos a serem retornados.</span><span class="sxs-lookup"><span data-stu-id="4f893-212">Use the **select** clause and pass the names of the fields to be returned.</span></span> <span data-ttu-id="4f893-213">Por exemplo, a consulta a seguir retornará apenas os campos **description** e **dueDate**.</span><span class="sxs-lookup"><span data-stu-id="4f893-213">For example, the following query will return only the **description** and **dueDate** fields.</span></span>

```nodejs
var query = new azure.TableQuery()
  .select(['description', 'dueDate'])
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

## <a name="delete-an-entity"></a><span data-ttu-id="4f893-214">Excluir uma entidade</span><span class="sxs-lookup"><span data-stu-id="4f893-214">Delete an entity</span></span>
<span data-ttu-id="4f893-215">Você pode excluir uma entidade usando suas chaves de partição e de linha.</span><span class="sxs-lookup"><span data-stu-id="4f893-215">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="4f893-216">Neste exemplo, o objeto **task1** contém os valores **RowKey** e **PartitionKey** da entidade a ser excluída.</span><span class="sxs-lookup"><span data-stu-id="4f893-216">In this example, the **task1** object contains the **RowKey** and **PartitionKey** values of the entity to be deleted.</span></span> <span data-ttu-id="4f893-217">Depois o objeto é passado para o método **deleteEntity** .</span><span class="sxs-lookup"><span data-stu-id="4f893-217">Then the object is passed to the **deleteEntity** method.</span></span>

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'}
};

tableSvc.deleteEntity('mytable', task, function(error, response){
  if(!error) {
    // Entity deleted
  }
});
```

> [!NOTE]
> <span data-ttu-id="4f893-218">Considere o uso de ETags ao excluir itens, para garantir que o item não seja modificado por outro processo.</span><span class="sxs-lookup"><span data-stu-id="4f893-218">Consider using ETags when deleting items, to ensure that the item hasn't been modified by another process.</span></span> <span data-ttu-id="4f893-219">Veja [Atualizar uma entidade](#update-an-entity) para obter informações sobre o uso de ETags.</span><span class="sxs-lookup"><span data-stu-id="4f893-219">See [Update an entity](#update-an-entity) for information on using ETags.</span></span>
>
>

## <a name="delete-a-table"></a><span data-ttu-id="4f893-220">Excluir uma tabela</span><span class="sxs-lookup"><span data-stu-id="4f893-220">Delete a table</span></span>
<span data-ttu-id="4f893-221">O código a seguir exclui uma tabela de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="4f893-221">The following code deletes a table from a storage account.</span></span>

```nodejs
tableSvc.deleteTable('mytable', function(error, response){
    if(!error){
        // Table deleted
    }
});
```

<span data-ttu-id="4f893-222">Se você não tiver certeza de que a tabela existe, use **deleteTableIfExists**.</span><span class="sxs-lookup"><span data-stu-id="4f893-222">If you are uncertain whether the table exists, use **deleteTableIfExists**.</span></span>

## <a name="use-continuation-tokens"></a><span data-ttu-id="4f893-223">Usar tokens de continuação</span><span class="sxs-lookup"><span data-stu-id="4f893-223">Use continuation tokens</span></span>
<span data-ttu-id="4f893-224">Quando você estiver consultando tabelas com grandes quantidades de resultados, deverá procurar tokens de continuação.</span><span class="sxs-lookup"><span data-stu-id="4f893-224">When you are querying tables for large amounts of results, look for continuation tokens.</span></span> <span data-ttu-id="4f893-225">Pode haver grandes quantidades de dados disponíveis para a sua consulta dos quais talvez você não saiba, se não criá-la de modo a reconhecer quando um token de continuação está presente.</span><span class="sxs-lookup"><span data-stu-id="4f893-225">There may be large amounts of data available for your query that you might not realize if you do not build to recognize when a continuation token is present.</span></span>

<span data-ttu-id="4f893-226">O objeto de resultados retornado durante a consulta de entidades define uma propriedade `continuationToken` quando esse token está presente.</span><span class="sxs-lookup"><span data-stu-id="4f893-226">The results object returned during querying entities sets a `continuationToken` property when such a token is present.</span></span> <span data-ttu-id="4f893-227">Você pode usar isso ao realizar uma consulta para continuar a mover-se pela partição e entidades de tabela.</span><span class="sxs-lookup"><span data-stu-id="4f893-227">You can then use this when performing a query to continue to move across the partition and table entities.</span></span>

<span data-ttu-id="4f893-228">Ao consultar, um parâmetro continuationToken pode ser fornecido entre a instância do objeto de consulta e a função de retorno de chamada:</span><span class="sxs-lookup"><span data-stu-id="4f893-228">When querying, a continuationToken parameter may be provided between the query object instance and the callback function:</span></span>

```nodejs
var nextContinuationToken = null;
dc.table.queryEntities(tableName,
    query,
    nextContinuationToken,
    function (error, results) {
        if (error) throw error;

        // iterate through results.entries with results

        if (results.continuationToken) {
            nextContinuationToken = results.continuationToken;
        }

    });
```

<span data-ttu-id="4f893-229">Se inspecionar o objeto `continuationToken`, você encontrará propriedades como `nextPartitionKey`, `nextRowKey` e `targetLocation`, que podem ser usadas para iterar por todos os resultados.</span><span class="sxs-lookup"><span data-stu-id="4f893-229">If you inspect the `continuationToken` object, you will find properties such as `nextPartitionKey`, `nextRowKey` and `targetLocation`, which can be used to iterate through all the results.</span></span>

<span data-ttu-id="4f893-230">Também há um exemplo de continuação dentro do repositório do Node.js do Armazenamento do Azure no GitHub.</span><span class="sxs-lookup"><span data-stu-id="4f893-230">There is also a continuation sample within the Azure Storage Node.js repo on GitHub.</span></span> <span data-ttu-id="4f893-231">Procure `examples/samples/continuationsample.js`.</span><span class="sxs-lookup"><span data-stu-id="4f893-231">Look for `examples/samples/continuationsample.js`.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="4f893-232">Trabalhar com assinaturas de acesso compartilhado</span><span class="sxs-lookup"><span data-stu-id="4f893-232">Work with shared access signatures</span></span>
<span data-ttu-id="4f893-233">SAS (Assinaturas de acesso compartilhado) são uma maneira segura de fornecer acesso granular a tabelas sem fornecer o nome ou as chaves da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="4f893-233">Shared access signatures (SAS) are a secure way to provide granular access to tables without providing your storage account name or keys.</span></span> <span data-ttu-id="4f893-234">As SAS são muitas vezes usadas para fornecer acesso limitado aos seus dados, como permitir que um aplicativo móvel consulte registros.</span><span class="sxs-lookup"><span data-stu-id="4f893-234">SAS are often used to provide limited access to your data, such as allowing a mobile app to query records.</span></span>

<span data-ttu-id="4f893-235">Um aplicativo confiável, como um serviço baseado em nuvem, gera uma SAS usando **generateSharedAccessSignature** de **TableService** e a fornece a um aplicativo não confiável ou semiconfiável, como um aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="4f893-235">A trusted application such as a cloud-based service generates a SAS using the **generateSharedAccessSignature** of the **TableService**, and provides it to an untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="4f893-236">A SAS é gerada utilizando uma política que descreve as datas inicial e final durante as quais a SAS é válida, assim como o nível de acesso concedido ao titular da SAS.</span><span class="sxs-lookup"><span data-stu-id="4f893-236">The SAS is generated using a policy, which describes the start and end dates during which the SAS is valid, as well as the access level granted to the SAS holder.</span></span>

<span data-ttu-id="4f893-237">O exemplo a seguir gera uma nova política de acesso compartilhado que permitirá que o titular da SAS consulte ('r') a tabela, e expira 100 minutos após o momento em que é criado.</span><span class="sxs-lookup"><span data-stu-id="4f893-237">The following example generates a new shared access policy that will allow the SAS holder to query ('r') the table, and expires 100 minutes after the time it is created.</span></span>

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
};

var tableSAS = tableSvc.generateSharedAccessSignature('mytable', sharedAccessPolicy);
var host = tableSvc.host;
```

<span data-ttu-id="4f893-238">Observe que também devem ser fornecidas as informações do host, já que são necessárias quando o titular da SAS tenta acessar a tabela.</span><span class="sxs-lookup"><span data-stu-id="4f893-238">Note that the host information must be provided also, as it is required when the SAS holder attempts to access the table.</span></span>

<span data-ttu-id="4f893-239">O aplicativo cliente usa a SAS com **TableServiceWithSAS** para executar operações na tabela.</span><span class="sxs-lookup"><span data-stu-id="4f893-239">The client application then uses the SAS with **TableServiceWithSAS** to perform operations against the table.</span></span> <span data-ttu-id="4f893-240">O exemplo a seguir conecta à tabela e executa uma consulta.</span><span class="sxs-lookup"><span data-stu-id="4f893-240">The following example connects to the table and performs a query.</span></span>

```nodejs
var sharedTableService = azure.createTableServiceWithSas(host, tableSAS);
var query = azure.TableQuery()
  .where('PartitionKey eq ?', 'hometasks');

sharedTableService.queryEntities(query, null, function(error, result, response) {
  if(!error) {
    // result contains the entities
  }
});
```

<span data-ttu-id="4f893-241">Como a SAS foi gerada só com acesso de consulta, se for feita uma tentativa de inserir, atualizar ou excluir entidades, será retornado um erro.</span><span class="sxs-lookup"><span data-stu-id="4f893-241">Since the SAS was generated with only query access, if an attempt were made to insert, update, or delete entities, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="4f893-242">Listas de Controle de Acesso</span><span class="sxs-lookup"><span data-stu-id="4f893-242">Access Control Lists</span></span>
<span data-ttu-id="4f893-243">Você também pode usar uma ACL (Lista de Controle de Acesso) para definir a política de acesso para uma SAS.</span><span class="sxs-lookup"><span data-stu-id="4f893-243">You can also use an Access Control List (ACL) to set the access policy for a SAS.</span></span> <span data-ttu-id="4f893-244">Isso é útil se você quiser permitir que vários clientes acessem a tabela, mas oferecem diferentes políticas de acesso para cada cliente.</span><span class="sxs-lookup"><span data-stu-id="4f893-244">This is useful if you wish to allow multiple clients to access the table, but provide different access policies for each client.</span></span>

<span data-ttu-id="4f893-245">Uma ACL é implementada através de um conjunto de políticas de acesso, com uma ID associada a cada política.</span><span class="sxs-lookup"><span data-stu-id="4f893-245">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="4f893-246">O seguinte exemplo define duas políticas: uma para “user1” e outra para “user2”:</span><span class="sxs-lookup"><span data-stu-id="4f893-246">The following example defines two policies, one for 'user1' and one for 'user2':</span></span>

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

<span data-ttu-id="4f893-247">O exemplo a seguir obtém a ACL atual para a tabela **hometasks** e adiciona as novas políticas usando **setTableAcl**.</span><span class="sxs-lookup"><span data-stu-id="4f893-247">The following example gets the current ACL for the **hometasks** table, and then adds the new policies using **setTableAcl**.</span></span> <span data-ttu-id="4f893-248">Essa abordagem permite:</span><span class="sxs-lookup"><span data-stu-id="4f893-248">This approach allows:</span></span>

```nodejs
var extend = require('extend');
tableSvc.getTableAcl('hometasks', function(error, result, response) {
if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    tableSvc.setTableAcl('hometasks', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

<span data-ttu-id="4f893-249">Uma vez que a ACL foi definida, você pode criar uma SAS com base na ID de uma política.</span><span class="sxs-lookup"><span data-stu-id="4f893-249">Once the ACL has been set, you can then create a SAS based on the ID for a policy.</span></span> <span data-ttu-id="4f893-250">O exemplo a seguir cria uma nova SAS para 'user2':</span><span class="sxs-lookup"><span data-stu-id="4f893-250">The following example creates a new SAS for 'user2':</span></span>

```nodejs
tableSAS = tableSvc.generateSharedAccessSignature('hometasks', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="4f893-251">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4f893-251">Next steps</span></span>
<span data-ttu-id="4f893-252">Para saber mais, consulte os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="4f893-252">For more information, see the following resources.</span></span>

* <span data-ttu-id="4f893-253">[O Gerenciador de Armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) é um aplicativo autônomo e gratuito da Microsoft que possibilita o trabalho visual com os dados do Armazenamento do Azure no Windows, MacOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="4f893-253">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="4f893-254">[SDK do Armazenamento do Azure para Node](https://github.com/Azure/azure-storage-node) no GitHub.</span><span class="sxs-lookup"><span data-stu-id="4f893-254">[Azure Storage SDK for Node](https://github.com/Azure/azure-storage-node) repository on GitHub.</span></span>
* [<span data-ttu-id="4f893-255">Centro de desenvolvedores do Node. js</span><span class="sxs-lookup"><span data-stu-id="4f893-255">Node.js Developer Center</span></span>](/develop/nodejs/)
* [<span data-ttu-id="4f893-256">Criar e implantar um aplicativo Node.js em um site do Azure</span><span class="sxs-lookup"><span data-stu-id="4f893-256">Create and deploy a Node.js application to an Azure website</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)