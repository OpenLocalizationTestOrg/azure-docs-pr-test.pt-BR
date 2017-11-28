---
title: aaaHow toouse armazenamento de tabela do Azure do Node. js | Microsoft Docs
description: "Armazene dados estruturados em nuvem hello usando o armazenamento de tabela do Azure, um repositório de dados NoSQL."
services: cosmos-db
documentationcenter: nodejs
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: fc2e33d2-c5da-4861-8503-53fdc25750de
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 21022491a9a21a5365628de93582ea3a325ed869
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-nodejs"></a><span data-ttu-id="c848f-103">Como toouse armazenamento de tabela do Azure do Node. js</span><span class="sxs-lookup"><span data-stu-id="c848f-103">How toouse Azure Table storage from Node.js</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="c848f-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="c848f-104">Overview</span></span>
<span data-ttu-id="c848f-105">Este tópico mostra como tooperform cenários comuns usando Olá tabela do Azure do serviço em um aplicativo Node. js.</span><span class="sxs-lookup"><span data-stu-id="c848f-105">This topic shows how tooperform common scenarios using hello Azure Table service in a Node.js application.</span></span>

<span data-ttu-id="c848f-106">exemplos de código Olá neste tópico pressupõem que você já tiver um aplicativo Node. js.</span><span class="sxs-lookup"><span data-stu-id="c848f-106">hello code examples in this topic assume you already have a Node.js application.</span></span> <span data-ttu-id="c848f-107">Para obter informações sobre como toocreate um aplicativo Node.js no Azure, consulte qualquer um dos seguintes tópicos:</span><span class="sxs-lookup"><span data-stu-id="c848f-107">For information about how toocreate a Node.js application in Azure, see any of these topics:</span></span>

* [<span data-ttu-id="c848f-108">Criar um aplicativo Web do Node.js no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="c848f-108">Create a Node.js web app in Azure App Service</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="c848f-109">Criar e implantar um tooAzure de aplicativo web Node.js usando o WebMatrix</span><span class="sxs-lookup"><span data-stu-id="c848f-109">Build and deploy a Node.js web app tooAzure using WebMatrix</span></span>](../app-service-web/web-sites-nodejs-use-webmatrix.md)
* <span data-ttu-id="c848f-110">[Criar e implantar um aplicativo de Node. js tooan serviço de nuvem do Azure](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (usando o Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="c848f-110">[Build and deploy a Node.js application tooan Azure Cloud Service](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (using Windows PowerShell)</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="configure-your-application-tooaccess-azure-storage"></a><span data-ttu-id="c848f-111">Configurar seu aplicativo tooaccess armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="c848f-111">Configure your application tooaccess Azure Storage</span></span>
<span data-ttu-id="c848f-112">toouse armazenamento do Azure, é necessário hello Azure Storage SDK para Node.js, que inclui um conjunto de bibliotecas de conveniência que se comunicam com serviços da REST do armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="c848f-112">toouse Azure Storage, you need hello Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-node-package-manager-npm-tooinstall-hello-package"></a><span data-ttu-id="c848f-113">Usar o pacote de saudação do Gerenciador de pacote de nó (NPM) tooinstall</span><span class="sxs-lookup"><span data-stu-id="c848f-113">Use Node Package Manager (NPM) tooinstall hello package</span></span>
1. <span data-ttu-id="c848f-114">Use uma interface de linha de comando como **PowerShell** (Windows), **Terminal** (Mac), ou **Bash** (Unix) e navegue toohello pasta em que você criou seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c848f-114">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), and navigate toohello folder where you created your application.</span></span>
2. <span data-ttu-id="c848f-115">Tipo **npm instalar o armazenamento do azure** na janela de comando hello.</span><span class="sxs-lookup"><span data-stu-id="c848f-115">Type **npm install azure-storage** in hello command window.</span></span> <span data-ttu-id="c848f-116">A saída do comando de saudação é semelhante toohello exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="c848f-116">Output from hello command is similar toohello following example.</span></span>

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
3. <span data-ttu-id="c848f-117">Você pode executar manualmente Olá **ls** tooverify de comando que um **nó\_módulos** pasta foi criada.</span><span class="sxs-lookup"><span data-stu-id="c848f-117">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="c848f-118">Dentro dessa pasta, você encontrará Olá **armazenamento do azure** pacote, que contém as bibliotecas de hello, você precisa de armazenamento tooaccess.</span><span class="sxs-lookup"><span data-stu-id="c848f-118">Inside that folder you will find hello **azure-storage** package, which contains hello libraries you need tooaccess storage.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="c848f-119">Importar o pacote de saudação</span><span class="sxs-lookup"><span data-stu-id="c848f-119">Import hello package</span></span>
<span data-ttu-id="c848f-120">Adicionar Olá após o início de toohello de código da saudação **server.js** arquivo em seu aplicativo:</span><span class="sxs-lookup"><span data-stu-id="c848f-120">Add hello following code toohello top of hello **server.js** file in your application:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="c848f-121">Configurar uma conexão do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="c848f-121">Set up an Azure Storage connection</span></span>
<span data-ttu-id="c848f-122">módulo de saudação do azure lerá variáveis de ambiente hello AZURE\_armazenamento\_conta e o AZURE\_armazenamento\_acesso\_chave ou o AZURE\_armazenamento\_conexão \_Cadeia de caracteres de informações necessárias tooconnect tooyour conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="c848f-122">hello azure module will read hello environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="c848f-123">Se essas variáveis de ambiente não forem definidas, você deve especificar as informações de conta de saudação ao chamar **TableService**.</span><span class="sxs-lookup"><span data-stu-id="c848f-123">If these environment variables are not set, you must specify hello account information when calling **TableService**.</span></span>

<span data-ttu-id="c848f-124">Para obter um exemplo de configuração de variáveis de ambiente Olá no hello [portal do Azure](https://portal.azure.com) para um site do Azure, consulte [usando o aplicativo web Node.js hello Azure serviço de tabela](../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="c848f-124">For an example of setting hello environment variables in hello [Azure portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using hello Azure Table Service](../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span></span>

## <a name="create-a-table"></a><span data-ttu-id="c848f-125">Criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="c848f-125">Create a table</span></span>
<span data-ttu-id="c848f-126">Olá código a seguir cria um **TableService** do objeto e o utiliza toocreate uma nova tabela.</span><span class="sxs-lookup"><span data-stu-id="c848f-126">hello following code creates a **TableService** object and uses it toocreate a new table.</span></span> <span data-ttu-id="c848f-127">Adicione a seguinte Olá superior de saudação do **server.js**.</span><span class="sxs-lookup"><span data-stu-id="c848f-127">Add hello following near hello top of **server.js**.</span></span>

```nodejs
var tableSvc = azure.createTableService();
```

<span data-ttu-id="c848f-128">Olá chamada muito**createTableIfNotExists** criará uma nova tabela com o nome especificado da saudação se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="c848f-128">hello call too**createTableIfNotExists** will create a new table with hello specified name if it does not already exist.</span></span> <span data-ttu-id="c848f-129">Olá, exemplo a seguir cria uma nova tabela chamada 'mytable' se ele ainda não existir:</span><span class="sxs-lookup"><span data-stu-id="c848f-129">hello following example creates a new table named 'mytable' if it does not already exist:</span></span>

```nodejs
tableSvc.createTableIfNotExists('mytable', function(error, result, response){
  if(!error){
    // Table exists or created
  }
});
```

<span data-ttu-id="c848f-130">Olá `result.created` será `true` se uma nova tabela é criada, e `false` se Olá tabela já existir.</span><span class="sxs-lookup"><span data-stu-id="c848f-130">hello `result.created` will be `true` if a new table is created, and `false` if hello table already exists.</span></span> <span data-ttu-id="c848f-131">Olá `response` conterá informações sobre a solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="c848f-131">hello `response` will contain information about hello request.</span></span>

### <a name="filters"></a><span data-ttu-id="c848f-132">Filtros</span><span class="sxs-lookup"><span data-stu-id="c848f-132">Filters</span></span>
<span data-ttu-id="c848f-133">Operações de filtragem opcionais podem ser aplicadas toooperations realizada usando **TableService**.</span><span class="sxs-lookup"><span data-stu-id="c848f-133">Optional filtering operations can be applied toooperations performed using **TableService**.</span></span> <span data-ttu-id="c848f-134">As operações de filtragem podem incluir registro em log, repetição automática, etc. Os filtros são objetos que implementam um método com assinatura hello:</span><span class="sxs-lookup"><span data-stu-id="c848f-134">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="c848f-135">Depois de fazer sua pré-processamento nas opções de solicitação hello, método hello precisa toocall "Avançar", passando um retorno de chamada com hello assinatura a seguir:</span><span class="sxs-lookup"><span data-stu-id="c848f-135">After doing its preprocessing on hello request options, hello method needs toocall "next", passing a callback with hello following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="c848f-136">Esse retorno de chamada e após o processamento returnObject hello (resposta de saudação do servidor de toohello de solicitação de saudação), o retorno de chamada hello precisa tooeither invocar lado, se ele existe toocontinue outros filtros de processamento ou simplesmente chamar finalCallback caso contrário Olá de tooend invocação de serviço.</span><span class="sxs-lookup"><span data-stu-id="c848f-136">In this callback, and after processing hello returnObject (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or simply invoke finalCallback otherwise tooend hello service invocation.</span></span>

<span data-ttu-id="c848f-137">Dois filtros que implementam a lógica de repetição são incluídos com hello Azure SDK para Node.js, **ExponentialRetryPolicyFilter** e **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="c848f-137">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="c848f-138">Olá seguir cria um **TableService** objeto que usa Olá **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="c848f-138">hello following creates a **TableService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var tableSvc = azure.createTableService().withFilter(retryOperations);
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="c848f-139">Adicionar uma tabela de entidade tooa</span><span class="sxs-lookup"><span data-stu-id="c848f-139">Add an entity tooa table</span></span>
<span data-ttu-id="c848f-140">tooadd uma entidade, primeiro crie um objeto que define as propriedades de entidade.</span><span class="sxs-lookup"><span data-stu-id="c848f-140">tooadd an entity, first create an object that defines your entity properties.</span></span> <span data-ttu-id="c848f-141">Todas as entidades devem conter um **PartitionKey** e **RowKey**, que são identificadores exclusivos para a entidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="c848f-141">All entities must contain a **PartitionKey** and **RowKey**, which are unique identifiers for hello entity.</span></span>

* <span data-ttu-id="c848f-142">**PartitionKey** -determina partição Olá Olá entidade será armazenada no</span><span class="sxs-lookup"><span data-stu-id="c848f-142">**PartitionKey** - determines hello partition that hello entity is stored in</span></span>
* <span data-ttu-id="c848f-143">**RowKey** - exclusivamente identifica a entidade Olá na partição Olá</span><span class="sxs-lookup"><span data-stu-id="c848f-143">**RowKey** - uniquely identifies hello entity within hello partition</span></span>

<span data-ttu-id="c848f-144">Ambas, **PartitionKey** e **RowKey**, devem ser valores de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="c848f-144">Both **PartitionKey** and **RowKey** must be string values.</span></span> <span data-ttu-id="c848f-145">Para obter mais informações, consulte [Olá Noções básicas sobre modelo de dados do serviço de tabela](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="c848f-145">For more information, see [Understanding hello Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="c848f-146">a seguir Olá é um exemplo de definição de uma entidade.</span><span class="sxs-lookup"><span data-stu-id="c848f-146">hello following is an example of defining an entity.</span></span> <span data-ttu-id="c848f-147">Observe que **dueDate** é definido com um tipo de **Edm.DateTime**.</span><span class="sxs-lookup"><span data-stu-id="c848f-147">Note that **dueDate** is defined as a type of **Edm.DateTime**.</span></span> <span data-ttu-id="c848f-148">Especificar tipo de saudação é opcional, e tipos serão ser inferidos se não for especificados.</span><span class="sxs-lookup"><span data-stu-id="c848f-148">Specifying hello type is optional, and types will be inferred if not specified.</span></span>

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20), '$':'Edm.DateTime'}
};
```

> [!NOTE]
> <span data-ttu-id="c848f-149">Existe também um campo **Carimbo de Data/Hora** para cada registro, que é definido pelo Azure quando uma entidade é inserida ou atualizada.</span><span class="sxs-lookup"><span data-stu-id="c848f-149">There is also a **Timestamp** field for each record, which is set by Azure when an entity is inserted or updated.</span></span>
>
>

<span data-ttu-id="c848f-150">Você também pode usar o hello **entityGenerator** toocreate entidades.</span><span class="sxs-lookup"><span data-stu-id="c848f-150">You can also use hello **entityGenerator** toocreate entities.</span></span> <span data-ttu-id="c848f-151">Olá, exemplo a seguir cria Olá mesma entidade de tarefa usando Olá **entityGenerator**.</span><span class="sxs-lookup"><span data-stu-id="c848f-151">hello following example creates hello same task entity using hello **entityGenerator**.</span></span>

```nodejs
var entGen = azure.TableUtilities.entityGenerator;
var task = {
  PartitionKey: entGen.String('hometasks'),
  RowKey: entGen.String('1'),
  description: entGen.String('take out hello trash'),
  dueDate: entGen.DateTime(new Date(Date.UTC(2015, 6, 20))),
};
```

<span data-ttu-id="c848f-152">tooadd uma tabela de tooyour de entidade, passar toohello de objeto de entidade Olá **insertEntity** método.</span><span class="sxs-lookup"><span data-stu-id="c848f-152">tooadd an entity tooyour table, pass hello entity object toohello **insertEntity** method.</span></span>

```nodejs
tableSvc.insertEntity('mytable',task, function (error, result, response) {
  if(!error){
    // Entity inserted
  }
});
```

<span data-ttu-id="c848f-153">Se Olá operação for bem-sucedida, `result` conterá Olá [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) de saudação inserida no registro e `response` contêm informações sobre a operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="c848f-153">If hello operation is successful, `result` will contain hello [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) of hello inserted record and `response` will contain information about hello operation.</span></span>

<span data-ttu-id="c848f-154">Resposta de exemplo:</span><span class="sxs-lookup"><span data-stu-id="c848f-154">Example response:</span></span>

```nodejs
{ '.metadata': { etag: 'W/"datetime\'2015-02-25T01%3A22%3A22.5Z\'"' } }
```

> [!NOTE]
> <span data-ttu-id="c848f-155">Por padrão, **insertEntity** não retornar a entidade Olá inserido como parte da saudação `response` informações.</span><span class="sxs-lookup"><span data-stu-id="c848f-155">By default, **insertEntity** does not return hello inserted entity as part of hello `response` information.</span></span> <span data-ttu-id="c848f-156">Se você planeja realizar outras operações nesta entidade ou deseja informações de saudação toocache, pode ser útil toohave retornou como parte da saudação `result`.</span><span class="sxs-lookup"><span data-stu-id="c848f-156">If you plan on performing other operations on this entity, or wish toocache hello information, it can be useful toohave it returned as part of hello `result`.</span></span> <span data-ttu-id="c848f-157">Você pode fazer isso habilitando **echoContent** da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="c848f-157">You can do this by enabling **echoContent** as follows:</span></span>
>
> `tableSvc.insertEntity('mytable', task, {echoContent: true}, function (error, result, response) {...}`
>
>

## <a name="update-an-entity"></a><span data-ttu-id="c848f-158">Atualizar uma entidade</span><span class="sxs-lookup"><span data-stu-id="c848f-158">Update an entity</span></span>
<span data-ttu-id="c848f-159">Há vários métodos e disponível tooupdate uma entidade existente:</span><span class="sxs-lookup"><span data-stu-id="c848f-159">There are multiple methods available tooupdate an existing entity:</span></span>

* <span data-ttu-id="c848f-160">**replaceEntity** – atualiza uma entidade existente ao substituí-la</span><span class="sxs-lookup"><span data-stu-id="c848f-160">**replaceEntity** - updates an existing entity by replacing it</span></span>
* <span data-ttu-id="c848f-161">**mergeEntity** -atualiza uma entidade existente, mesclando novos valores de propriedade para a entidade existente Olá</span><span class="sxs-lookup"><span data-stu-id="c848f-161">**mergeEntity** - updates an existing entity by merging new property values into hello existing entity</span></span>
* <span data-ttu-id="c848f-162">**insertOrReplaceEntity** – atualiza uma entidade existente substituindo-a.</span><span class="sxs-lookup"><span data-stu-id="c848f-162">**insertOrReplaceEntity** - updates an existing entity by replacing it.</span></span> <span data-ttu-id="c848f-163">Se não existir nenhuma entidade, uma nova será inserida</span><span class="sxs-lookup"><span data-stu-id="c848f-163">If no entity exists, a new one will be inserted</span></span>
* <span data-ttu-id="c848f-164">**insertOrMergeEntity** -atualiza uma entidade existente, mesclando novos valores de propriedade em Olá existente.</span><span class="sxs-lookup"><span data-stu-id="c848f-164">**insertOrMergeEntity** - updates an existing entity by merging new property values into hello existing.</span></span> <span data-ttu-id="c848f-165">Se não existir nenhuma entidade, uma nova será inserida</span><span class="sxs-lookup"><span data-stu-id="c848f-165">If no entity exists, a new one will be inserted</span></span>

<span data-ttu-id="c848f-166">Olá exemplo a seguir demonstra a atualização de uma entidade usando **replaceEntity**:</span><span class="sxs-lookup"><span data-stu-id="c848f-166">hello following example demonstrates updating an entity using **replaceEntity**:</span></span>

```nodejs
tableSvc.replaceEntity('mytable', updatedTask, function(error, result, response){
  if(!error) {
    // Entity updated
  }
});
```

> [!NOTE]
> <span data-ttu-id="c848f-167">Por padrão, a atualização de uma entidade não verifica toosee se dados hello está sendo atualizados anteriormente tem sido modificados por outro processo.</span><span class="sxs-lookup"><span data-stu-id="c848f-167">By default, updating an entity does not check toosee if hello data being updated has previously been modified by another process.</span></span> <span data-ttu-id="c848f-168">atualizações simultâneas de toosupport:</span><span class="sxs-lookup"><span data-stu-id="c848f-168">toosupport concurrent updates:</span></span>
>
> 1. <span data-ttu-id="c848f-169">Obter Olá ETag do objeto de hello está sendo atualizado.</span><span class="sxs-lookup"><span data-stu-id="c848f-169">Get hello ETag of hello object being updated.</span></span> <span data-ttu-id="c848f-170">Isto é retornado como parte da saudação `response` para qualquer operação de entidade e podem ser recuperados por meio de `response['.metadata'].etag`.</span><span class="sxs-lookup"><span data-stu-id="c848f-170">This is returned as part of hello `response` for any entity-related operation and can be retrieved through `response['.metadata'].etag`.</span></span>
> 2. <span data-ttu-id="c848f-171">Ao executar uma operação de atualização em uma entidade, adicione informações de ETag Olá recuperados anteriormente toohello nova entidade.</span><span class="sxs-lookup"><span data-stu-id="c848f-171">When performing an update operation on an entity, add hello ETag information previously retrieved toohello new entity.</span></span> <span data-ttu-id="c848f-172">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="c848f-172">For example:</span></span>
>
>       <span data-ttu-id="c848f-173">entity2['.metadata'].etag = currentEtag;</span><span class="sxs-lookup"><span data-stu-id="c848f-173">entity2['.metadata'].etag = currentEtag;</span></span>
> 3. <span data-ttu-id="c848f-174">Execute a operação de atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="c848f-174">Perform hello update operation.</span></span> <span data-ttu-id="c848f-175">Se a entidade Olá foi modificada desde que você recuperou o valor de ETag hello, como outra instância do seu aplicativo, um `error` será retornado indicando que a condição de atualização de saudação especificada na solicitação de saudação não foi atendida.</span><span class="sxs-lookup"><span data-stu-id="c848f-175">If hello entity has been modified since you retrieved hello ETag value, such as another instance of your application, an `error` will be returned stating that hello update condition specified in hello request was not satisfied.</span></span>
>
>

<span data-ttu-id="c848f-176">Com **replaceEntity** e **mergeEntity**, se a entidade de saudação que está sendo atualizada não existir, e em seguida, haverá falha na operação de atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="c848f-176">With **replaceEntity** and **mergeEntity**, if hello entity that is being updated doesn't exist, then hello update operation will fail.</span></span> <span data-ttu-id="c848f-177">Portanto, se desejar toostore uma entidade, independentemente se ela já existir, usar **insertOrReplaceEntity** ou **insertOrMergeEntity**.</span><span class="sxs-lookup"><span data-stu-id="c848f-177">Therefore if you wish toostore an entity regardless of whether it already exists, use **insertOrReplaceEntity** or **insertOrMergeEntity**.</span></span>

<span data-ttu-id="c848f-178">Olá `result` para atualização bem sucedida operações conterá Olá **Etag** Olá atualizadas entidade.</span><span class="sxs-lookup"><span data-stu-id="c848f-178">hello `result` for successful update operations will contain hello **Etag** of hello updated entity.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="c848f-179">Trabalhar com grupos de entidades</span><span class="sxs-lookup"><span data-stu-id="c848f-179">Work with groups of entities</span></span>
<span data-ttu-id="c848f-180">Às vezes, faz sentido toosubmit várias operações juntos em um lote tooensure atômico processamento pelo servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="c848f-180">Sometimes it makes sense toosubmit multiple operations together in a batch tooensure atomic processing by hello server.</span></span> <span data-ttu-id="c848f-181">tooaccomplish que use Olá **TableBatch** toocreate um lote de classe e, em seguida, usar o hello **executeBatch** método de **TableService** tooperform Olá de operações em lote.</span><span class="sxs-lookup"><span data-stu-id="c848f-181">tooaccomplish that, use hello **TableBatch** class toocreate a batch, and then use hello **executeBatch** method of **TableService** tooperform hello batched operations.</span></span>

 <span data-ttu-id="c848f-182">saudação de exemplo a seguir demonstra duas entidades em um lote de envio:</span><span class="sxs-lookup"><span data-stu-id="c848f-182">hello following example demonstrates submitting two entities in a batch:</span></span>

```nodejs
var task1 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'Take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20)}
};
var task2 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '2'},
  description: {'_':'Wash hello dishes'},
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

<span data-ttu-id="c848f-183">Para operações de lote bem-sucedido, `result` conterá informações para cada operação em lote hello.</span><span class="sxs-lookup"><span data-stu-id="c848f-183">For successful batch operations, `result` will contain information for each operation in hello batch.</span></span>

### <a name="work-with-batched-operations"></a><span data-ttu-id="c848f-184">Trabalhando com operações em lote</span><span class="sxs-lookup"><span data-stu-id="c848f-184">Work with batched operations</span></span>
<span data-ttu-id="c848f-185">Operações adicionadas tooa lote pode ser inspecionado exibindo Olá `operations` propriedade.</span><span class="sxs-lookup"><span data-stu-id="c848f-185">Operations added tooa batch can be inspected by viewing hello `operations` property.</span></span> <span data-ttu-id="c848f-186">Você também pode usar o hello toowork métodos com as operações a seguir:</span><span class="sxs-lookup"><span data-stu-id="c848f-186">You can also use hello following methods toowork with operations:</span></span>

* <span data-ttu-id="c848f-187">**clear** – limpa todas as operações de um lote.</span><span class="sxs-lookup"><span data-stu-id="c848f-187">**clear** - clears all operations from a batch</span></span>
* <span data-ttu-id="c848f-188">**getOperations** -obtém uma operação de lote Olá</span><span class="sxs-lookup"><span data-stu-id="c848f-188">**getOperations** - gets an operation from hello batch</span></span>
* <span data-ttu-id="c848f-189">**hasOperations** -retorna true se o lote Olá contém operações</span><span class="sxs-lookup"><span data-stu-id="c848f-189">**hasOperations** - returns true if hello batch contains operations</span></span>
* <span data-ttu-id="c848f-190">**removeOperations** – remove uma operação</span><span class="sxs-lookup"><span data-stu-id="c848f-190">**removeOperations** - removes an operation</span></span>
* <span data-ttu-id="c848f-191">**tamanho** -retorna Olá número de operações em lote Olá</span><span class="sxs-lookup"><span data-stu-id="c848f-191">**size** - returns hello number of operations in hello batch</span></span>

## <a name="retrieve-an-entity-by-key"></a><span data-ttu-id="c848f-192">Recuperar uma entidade por chave</span><span class="sxs-lookup"><span data-stu-id="c848f-192">Retrieve an entity by key</span></span>
<span data-ttu-id="c848f-193">tooreturn uma entidade específica com base em Olá **PartitionKey** e **RowKey**, use Olá **retrieveEntity** método.</span><span class="sxs-lookup"><span data-stu-id="c848f-193">tooreturn a specific entity based on hello **PartitionKey** and **RowKey**, use hello **retrieveEntity** method.</span></span>

```nodejs
tableSvc.retrieveEntity('mytable', 'hometasks', '1', function(error, result, response){
  if(!error){
    // result contains hello entity
  }
});
```

<span data-ttu-id="c848f-194">Quando essa operação é concluída, `result` conterá entidade hello.</span><span class="sxs-lookup"><span data-stu-id="c848f-194">Once this operation is complete, `result` will contain hello entity.</span></span>

## <a name="query-a-set-of-entities"></a><span data-ttu-id="c848f-195">Consultar um conjunto de entidades</span><span class="sxs-lookup"><span data-stu-id="c848f-195">Query a set of entities</span></span>
<span data-ttu-id="c848f-196">tooquery uma tabela, use Olá **TableQuery** objeto toobuild uma expressão de consulta usando Olá cláusulas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c848f-196">tooquery a table, use hello **TableQuery** object toobuild up a query expression using hello following clauses:</span></span>

* <span data-ttu-id="c848f-197">**Selecione** -Olá campos toobe retornado da consulta de saudação</span><span class="sxs-lookup"><span data-stu-id="c848f-197">**select** - hello fields toobe returned from hello query</span></span>
* <span data-ttu-id="c848f-198">**onde** - Olá onde cláusula</span><span class="sxs-lookup"><span data-stu-id="c848f-198">**where** - hello where clause</span></span>

  * <span data-ttu-id="c848f-199">**and** – uma condição where `and`</span><span class="sxs-lookup"><span data-stu-id="c848f-199">**and** - an `and` where condition</span></span>
  * <span data-ttu-id="c848f-200">**or** – uma condição where `or`</span><span class="sxs-lookup"><span data-stu-id="c848f-200">**or** - an `or` where condition</span></span>
* <span data-ttu-id="c848f-201">**superior** -Olá o número de itens toofetch</span><span class="sxs-lookup"><span data-stu-id="c848f-201">**top** - hello number of items toofetch</span></span>

<span data-ttu-id="c848f-202">Olá, exemplo a seguir cria uma consulta que retornará Olá primeiros cinco itens com um PartitionKey de 'hometasks'.</span><span class="sxs-lookup"><span data-stu-id="c848f-202">hello following example builds a query that will return hello top five items with a PartitionKey of 'hometasks'.</span></span>

```nodejs
var query = new azure.TableQuery()
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

<span data-ttu-id="c848f-203">Como **select** não é usado, todos os campos serão retornados.</span><span class="sxs-lookup"><span data-stu-id="c848f-203">Since **select** is not used, all fields will be returned.</span></span> <span data-ttu-id="c848f-204">consulta de saudação de tooperform em uma tabela, use **queryEntities**.</span><span class="sxs-lookup"><span data-stu-id="c848f-204">tooperform hello query against a table, use **queryEntities**.</span></span> <span data-ttu-id="c848f-205">Olá, exemplo a seguir usa entidades de tooreturn esta consulta de 'mytable'.</span><span class="sxs-lookup"><span data-stu-id="c848f-205">hello following example uses this query tooreturn entities from 'mytable'.</span></span>

```nodejs
tableSvc.queryEntities('mytable',query, null, function(error, result, response) {
  if(!error) {
    // query was successful
  }
});
```

<span data-ttu-id="c848f-206">Se for bem-sucedido, `result.entries` conterá uma matriz de entidades que correspondem à consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="c848f-206">If successful, `result.entries` will contain an array of entities that match hello query.</span></span> <span data-ttu-id="c848f-207">Se a consulta Olá foi tooreturn não é possível todas as entidades, `result.continuationToken` serão não -*nulo* e pode ser usado como Olá terceiro parâmetro de **queryEntities** tooretrieve mais resultados.</span><span class="sxs-lookup"><span data-stu-id="c848f-207">If hello query was unable tooreturn all entities, `result.continuationToken` will be non-*null* and can be used as hello third parameter of **queryEntities** tooretrieve more results.</span></span> <span data-ttu-id="c848f-208">Para consulta inicial de hello, use *nulo* para o terceiro parâmetro de saudação.</span><span class="sxs-lookup"><span data-stu-id="c848f-208">For hello initial query, use *null* for hello third parameter.</span></span>

### <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="c848f-209">consultar um subconjunto de propriedades da entidade</span><span class="sxs-lookup"><span data-stu-id="c848f-209">Query a subset of entity properties</span></span>
<span data-ttu-id="c848f-210">Uma tabela de consulta tooa pode recuperar apenas alguns campos de uma entidade.</span><span class="sxs-lookup"><span data-stu-id="c848f-210">A query tooa table can retrieve just a few fields from an entity.</span></span>
<span data-ttu-id="c848f-211">Isso reduz a largura de banda e pode melhorar o desempenho da consulta, principalmente em grandes entidades.</span><span class="sxs-lookup"><span data-stu-id="c848f-211">This reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="c848f-212">Saudação de uso **selecione** cláusula e passar nomes de saudação do hello campos toobe retornados.</span><span class="sxs-lookup"><span data-stu-id="c848f-212">Use hello **select** clause and pass hello names of hello fields toobe returned.</span></span> <span data-ttu-id="c848f-213">Por exemplo, hello consulta a seguir retornará apenas Olá **descrição** e **dueDate** campos.</span><span class="sxs-lookup"><span data-stu-id="c848f-213">For example, hello following query will return only hello **description** and **dueDate** fields.</span></span>

```nodejs
var query = new azure.TableQuery()
  .select(['description', 'dueDate'])
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

## <a name="delete-an-entity"></a><span data-ttu-id="c848f-214">Excluir uma entidade</span><span class="sxs-lookup"><span data-stu-id="c848f-214">Delete an entity</span></span>
<span data-ttu-id="c848f-215">Você pode excluir uma entidade usando suas chaves de partição e de linha.</span><span class="sxs-lookup"><span data-stu-id="c848f-215">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="c848f-216">Neste exemplo, Olá **task1** objeto contém Olá **RowKey** e **PartitionKey** valores hello entidade toobe excluído.</span><span class="sxs-lookup"><span data-stu-id="c848f-216">In this example, hello **task1** object contains hello **RowKey** and **PartitionKey** values of hello entity toobe deleted.</span></span> <span data-ttu-id="c848f-217">E o objeto de saudação é passado toohello **deleteEntity** método.</span><span class="sxs-lookup"><span data-stu-id="c848f-217">Then hello object is passed toohello **deleteEntity** method.</span></span>

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
> <span data-ttu-id="c848f-218">Considere usar ETags quando a exclusão de itens, tooensure Olá item não foi modificada por outro processo.</span><span class="sxs-lookup"><span data-stu-id="c848f-218">Consider using ETags when deleting items, tooensure that hello item hasn't been modified by another process.</span></span> <span data-ttu-id="c848f-219">Veja [Atualizar uma entidade](#update-an-entity) para obter informações sobre o uso de ETags.</span><span class="sxs-lookup"><span data-stu-id="c848f-219">See [Update an entity](#update-an-entity) for information on using ETags.</span></span>
>
>

## <a name="delete-a-table"></a><span data-ttu-id="c848f-220">Excluir uma tabela</span><span class="sxs-lookup"><span data-stu-id="c848f-220">Delete a table</span></span>
<span data-ttu-id="c848f-221">saudação de código a seguir exclui uma tabela de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c848f-221">hello following code deletes a table from a storage account.</span></span>

```nodejs
tableSvc.deleteTable('mytable', function(error, response){
    if(!error){
        // Table deleted
    }
});
```

<span data-ttu-id="c848f-222">Se você não tiver certeza se a tabela de saudação existe, use **deleteTableIfExists**.</span><span class="sxs-lookup"><span data-stu-id="c848f-222">If you are uncertain whether hello table exists, use **deleteTableIfExists**.</span></span>

## <a name="use-continuation-tokens"></a><span data-ttu-id="c848f-223">Usar tokens de continuação</span><span class="sxs-lookup"><span data-stu-id="c848f-223">Use continuation tokens</span></span>
<span data-ttu-id="c848f-224">Quando você estiver consultando tabelas com grandes quantidades de resultados, deverá procurar tokens de continuação.</span><span class="sxs-lookup"><span data-stu-id="c848f-224">When you are querying tables for large amounts of results, look for continuation tokens.</span></span> <span data-ttu-id="c848f-225">Pode haver grandes quantidades de dados disponíveis para a consulta que você talvez não percebam se você não criar toorecognize quando um token de continuação estiver presente.</span><span class="sxs-lookup"><span data-stu-id="c848f-225">There may be large amounts of data available for your query that you might not realize if you do not build toorecognize when a continuation token is present.</span></span>

<span data-ttu-id="c848f-226">resultados de saudação do objeto retornado durante consultar conjuntos de entidades um `continuationToken` propriedade quando esse token está presente.</span><span class="sxs-lookup"><span data-stu-id="c848f-226">hello results object returned during querying entities sets a `continuationToken` property when such a token is present.</span></span> <span data-ttu-id="c848f-227">Você pode usar isso ao executar uma toomove toocontinue de consulta em entidades de partição e a tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="c848f-227">You can then use this when performing a query toocontinue toomove across hello partition and table entities.</span></span>

<span data-ttu-id="c848f-228">Ao consultar, um parâmetro de continuationToken pode ser fornecido entre a instância do objeto de consulta hello e função de retorno de chamada hello:</span><span class="sxs-lookup"><span data-stu-id="c848f-228">When querying, a continuationToken parameter may be provided between hello query object instance and hello callback function:</span></span>

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

<span data-ttu-id="c848f-229">Se você inspecionar Olá `continuationToken` objeto, você encontrará propriedades como `nextPartitionKey`, `nextRowKey` e `targetLocation`, que pode ser usado tooiterate por meio de todos os resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="c848f-229">If you inspect hello `continuationToken` object, you will find properties such as `nextPartitionKey`, `nextRowKey` and `targetLocation`, which can be used tooiterate through all hello results.</span></span>

<span data-ttu-id="c848f-230">Também é um exemplo de continuação no repositório de Node.js do armazenamento do Azure Olá no GitHub.</span><span class="sxs-lookup"><span data-stu-id="c848f-230">There is also a continuation sample within hello Azure Storage Node.js repo on GitHub.</span></span> <span data-ttu-id="c848f-231">Procure `examples/samples/continuationsample.js`.</span><span class="sxs-lookup"><span data-stu-id="c848f-231">Look for `examples/samples/continuationsample.js`.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="c848f-232">Trabalhar com assinaturas de acesso compartilhado</span><span class="sxs-lookup"><span data-stu-id="c848f-232">Work with shared access signatures</span></span>
<span data-ttu-id="c848f-233">Assinaturas de acesso compartilhado (SAS) são uma tootables de acesso granular de tooprovide de maneira segura sem fornecer o nome da conta de armazenamento ou chaves.</span><span class="sxs-lookup"><span data-stu-id="c848f-233">Shared access signatures (SAS) are a secure way tooprovide granular access tootables without providing your storage account name or keys.</span></span> <span data-ttu-id="c848f-234">SAS geralmente são usadas tooprovide limitado acessar tooyour os dados, como permitir que um aplicativo móvel tooquery registros.</span><span class="sxs-lookup"><span data-stu-id="c848f-234">SAS are often used tooprovide limited access tooyour data, such as allowing a mobile app tooquery records.</span></span>

<span data-ttu-id="c848f-235">Um aplicativo confiável como um serviço baseado em nuvem gera uma SAS usando Olá **generateSharedAccessSignature** de saudação **TableService**e fornece-tooan aplicativos de confiança parcial ou não confiáveis como um aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="c848f-235">A trusted application such as a cloud-based service generates a SAS using hello **generateSharedAccessSignature** of hello **TableService**, and provides it tooan untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="c848f-236">Olá SAS é gerado usando uma política, que descreve o início de saudação e datas finais durante o qual Olá SAS é válido, bem como Olá detentor SAS do nível toohello concedido acesso.</span><span class="sxs-lookup"><span data-stu-id="c848f-236">hello SAS is generated using a policy, which describes hello start and end dates during which hello SAS is valid, as well as hello access level granted toohello SAS holder.</span></span>

<span data-ttu-id="c848f-237">Olá exemplo a seguir gera uma nova política de acesso compartilhado que permitirá a saudação da tabela SAS detentor tooquery ('r') hello e expira 100 minutos após o tempo de saudação que é criado.</span><span class="sxs-lookup"><span data-stu-id="c848f-237">hello following example generates a new shared access policy that will allow hello SAS holder tooquery ('r') hello table, and expires 100 minutes after hello time it is created.</span></span>

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

<span data-ttu-id="c848f-238">Observe que informações do host Olá devem ser fornecido, além disso, como é necessário quando detentor SAS Olá tentativas de tabela de saudação tooaccess.</span><span class="sxs-lookup"><span data-stu-id="c848f-238">Note that hello host information must be provided also, as it is required when hello SAS holder attempts tooaccess hello table.</span></span>

<span data-ttu-id="c848f-239">Olá aplicativo cliente, em seguida, usa Olá SAS com **TableServiceWithSAS** tooperform operações em relação à tabela hello.</span><span class="sxs-lookup"><span data-stu-id="c848f-239">hello client application then uses hello SAS with **TableServiceWithSAS** tooperform operations against hello table.</span></span> <span data-ttu-id="c848f-240">saudação de exemplo a seguir conecta-se a tabela de toohello e executa uma consulta.</span><span class="sxs-lookup"><span data-stu-id="c848f-240">hello following example connects toohello table and performs a query.</span></span>

```nodejs
var sharedTableService = azure.createTableServiceWithSas(host, tableSAS);
var query = azure.TableQuery()
  .where('PartitionKey eq ?', 'hometasks');

sharedTableService.queryEntities(query, null, function(error, result, response) {
  if(!error) {
    // result contains hello entities
  }
});
```

<span data-ttu-id="c848f-241">Desde que hello SAS foi gerado com acesso somente de consulta, se uma tentativa foi feita tooinsert, atualizar ou excluir entidades, um erro será retornado.</span><span class="sxs-lookup"><span data-stu-id="c848f-241">Since hello SAS was generated with only query access, if an attempt were made tooinsert, update, or delete entities, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="c848f-242">Listas de Controle de Acesso</span><span class="sxs-lookup"><span data-stu-id="c848f-242">Access Control Lists</span></span>
<span data-ttu-id="c848f-243">Você também pode usar uma política de acesso de saudação de tooset de lista de controle de acesso (ACL) para uma SAS.</span><span class="sxs-lookup"><span data-stu-id="c848f-243">You can also use an Access Control List (ACL) tooset hello access policy for a SAS.</span></span> <span data-ttu-id="c848f-244">Isso é útil se você quiser tooallow várias tabelas de saudação tooaccess de clientes, mas fornece as políticas de acesso diferentes para cada cliente.</span><span class="sxs-lookup"><span data-stu-id="c848f-244">This is useful if you wish tooallow multiple clients tooaccess hello table, but provide different access policies for each client.</span></span>

<span data-ttu-id="c848f-245">Uma ACL é implementada através de um conjunto de políticas de acesso, com uma ID associada a cada política.</span><span class="sxs-lookup"><span data-stu-id="c848f-245">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="c848f-246">saudação de exemplo a seguir define duas políticas, uma para 'user1' e outra para o 'Usuário2':</span><span class="sxs-lookup"><span data-stu-id="c848f-246">hello following example defines two policies, one for 'user1' and one for 'user2':</span></span>

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

<span data-ttu-id="c848f-247">Olá obtém de exemplo a seguir Olá ACL atual para Olá **hometasks** da tabela e, em seguida, adiciona novas políticas de saudação usando **setTableAcl**.</span><span class="sxs-lookup"><span data-stu-id="c848f-247">hello following example gets hello current ACL for hello **hometasks** table, and then adds hello new policies using **setTableAcl**.</span></span> <span data-ttu-id="c848f-248">Essa abordagem permite:</span><span class="sxs-lookup"><span data-stu-id="c848f-248">This approach allows:</span></span>

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

<span data-ttu-id="c848f-249">Uma vez Olá que ACL tiver sido definido, você pode criar uma SAS com base na ID de saudação de uma política.</span><span class="sxs-lookup"><span data-stu-id="c848f-249">Once hello ACL has been set, you can then create a SAS based on hello ID for a policy.</span></span> <span data-ttu-id="c848f-250">saudação de exemplo a seguir cria uma nova SAS para 'Usuário2':</span><span class="sxs-lookup"><span data-stu-id="c848f-250">hello following example creates a new SAS for 'user2':</span></span>

```nodejs
tableSAS = tableSvc.generateSharedAccessSignature('hometasks', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="c848f-251">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c848f-251">Next steps</span></span>
<span data-ttu-id="c848f-252">Para obter mais informações, consulte Olá recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="c848f-252">For more information, see hello following resources.</span></span>

* <span data-ttu-id="c848f-253">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) é um aplicativo autônomo gratuito da Microsoft que permite que você toowork visualmente com dados de armazenamento do Azure no Linux, Windows e macOS.</span><span class="sxs-lookup"><span data-stu-id="c848f-253">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="c848f-254">[SDK do Armazenamento do Azure para Node](https://github.com/Azure/azure-storage-node) no GitHub.</span><span class="sxs-lookup"><span data-stu-id="c848f-254">[Azure Storage SDK for Node](https://github.com/Azure/azure-storage-node) repository on GitHub.</span></span>
* [<span data-ttu-id="c848f-255">Centro de Desenvolvedores do Node.js</span><span class="sxs-lookup"><span data-stu-id="c848f-255">Node.js Developer Center</span></span>](/develop/nodejs/)
* [<span data-ttu-id="c848f-256">Criar e implantar um aplicativo de Node. js tooan site do Azure</span><span class="sxs-lookup"><span data-stu-id="c848f-256">Create and deploy a Node.js application tooan Azure website</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)
