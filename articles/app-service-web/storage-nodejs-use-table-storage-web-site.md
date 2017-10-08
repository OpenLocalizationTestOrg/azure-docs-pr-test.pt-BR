---
title: "aplicativo de web aaaNode.js usando Olá serviço tabela do Azure"
description: "Este tutorial ensina como toouse hello Azure Table serviço toostore dados de um aplicativo Node. js que está hospedado em aplicativos de Web do serviço de aplicativo do Azure."
tags: azure-portal
services: app-service\web, storage
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 029e6f46-f586-4309-adbf-71c7b8d537d4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: f6e08335b4c7f62f7b3994287edd586860cb7135
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-app-using-hello-azure-table-service"></a><span data-ttu-id="5fe8d-103">Aplicativo de web Node. js usando Olá serviço tabela do Azure</span><span class="sxs-lookup"><span data-stu-id="5fe8d-103">Node.js web app using hello Azure Table Service</span></span>
## <a name="overview"></a><span data-ttu-id="5fe8d-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="5fe8d-104">Overview</span></span>
<span data-ttu-id="5fe8d-105">Este tutorial mostra como o serviço de tabela toouse fornecida pelo toostore e acessar dados de gerenciamento de dados do Azure uma [nó] aplicativo hospedado no [do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-105">This tutorial shows you how toouse Table service provided by Azure Data Management toostore and access data from a [node] application hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="5fe8d-106">Este tutorial pressupõe que você tenha alguma experiência anterior usando nó e [Git].</span><span class="sxs-lookup"><span data-stu-id="5fe8d-106">This tutorial assumes that you have some prior experience using node and [Git].</span></span>

<span data-ttu-id="5fe8d-107">Você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="5fe8d-107">You will learn:</span></span>

* <span data-ttu-id="5fe8d-108">Como toouse npm (Gerenciador de pacotes de nó) tooinstall Olá módulos de nó</span><span class="sxs-lookup"><span data-stu-id="5fe8d-108">How toouse npm (node package manager) tooinstall hello node modules</span></span>
* <span data-ttu-id="5fe8d-109">Como toowork com hello serviço tabela do Azure</span><span class="sxs-lookup"><span data-stu-id="5fe8d-109">How toowork with hello Azure Table service</span></span>
* <span data-ttu-id="5fe8d-110">Como toouse Olá toocreate CLI do Azure com um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-110">How toouse hello Azure CLI toocreate a web app.</span></span>

<span data-ttu-id="5fe8d-111">Seguindo este tutorial, você criará um aplicativo simples de “lista de tarefas” baseado na web, que permite criar, recuperar e concluir tarefas.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-111">By following this tutorial, you will build a simple web-based "to-do list" application that allows creating, retrieving and completing tasks.</span></span> <span data-ttu-id="5fe8d-112">tarefas de saudação são armazenadas em Olá serviço tabela.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-112">hello tasks are stored in hello Table service.</span></span>

<span data-ttu-id="5fe8d-113">Aqui está o aplicativo hello concluída:</span><span class="sxs-lookup"><span data-stu-id="5fe8d-113">Here is hello completed application:</span></span>

![Uma página da Web que exibe uma lista de tarefas vazia][node-table-finished]

> [!NOTE]
> <span data-ttu-id="5fe8d-115">Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-115">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="5fe8d-116">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-116">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="5fe8d-117">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5fe8d-117">Prerequisites</span></span>
<span data-ttu-id="5fe8d-118">Antes de seguir as instruções neste artigo hello, certifique-se de que você tenha a seguinte Olá instalado:</span><span class="sxs-lookup"><span data-stu-id="5fe8d-118">Before following hello instructions in this article, ensure that you have hello following installed:</span></span>

* <span data-ttu-id="5fe8d-119">[nó] versão 0.10.24 ou superior</span><span class="sxs-lookup"><span data-stu-id="5fe8d-119">[node] version 0.10.24 or higher</span></span>
* <span data-ttu-id="5fe8d-120">[Git]</span><span class="sxs-lookup"><span data-stu-id="5fe8d-120">[Git]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="create-a-storage-account"></a><span data-ttu-id="5fe8d-121">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="5fe8d-121">Create a storage account</span></span>
<span data-ttu-id="5fe8d-122">Crie uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-122">Create an Azure storage account.</span></span> <span data-ttu-id="5fe8d-123">aplicativo Hello usará esse itens de tarefas pendentes conta toostore hello.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-123">hello app will use this account toostore hello to-do items.</span></span>

1. <span data-ttu-id="5fe8d-124">Faça logon no hello [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5fe8d-124">Log into hello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="5fe8d-125">Clique em Olá **novo** ícone na parte inferior de saudação à esquerda do portal hello, em seguida, clique em **dados + armazenamento** > **armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-125">Click hello **New** icon on hello bottom left of hello portal, then click **Data + Storage** > **Storage**.</span></span> <span data-ttu-id="5fe8d-126">Dê um nome exclusivo de conta de armazenamento hello e criar um novo [grupo de recursos](../azure-resource-manager/resource-group-overview.md) para ele.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-126">Give hello storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Botão Novo](./media/storage-nodejs-use-table-storage-web-site/configure-storage.png)
   
    <span data-ttu-id="5fe8d-128">Quando tiver sido criada a conta de armazenamento hello, Olá **notificações** botão pisca uma verde **êxito** e folha da conta de armazenamento hello está aberta tooshow que ele pertence toohello novo recurso de grupo criado.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-128">When hello storage account has been created, hello **Notifications** button will flash a green **SUCCESS** and hello storage account's blade is open tooshow that it belongs toohello new resource group you created.</span></span>
3. <span data-ttu-id="5fe8d-129">Na folha da conta de armazenamento hello, clique em **configurações** > **chaves**.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-129">In hello storage account's blade, click **Settings** > **Keys**.</span></span> <span data-ttu-id="5fe8d-130">Copie a área de transferência de toohello chave de acesso primária hello.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-130">Copy hello primary access key toohello clipboard.</span></span>
   
    ![Chave de acesso][portal-storage-access-keys]

## <a name="install-modules-and-generate-scaffolding"></a><span data-ttu-id="5fe8d-132">Instalar módulos e gerar scaffolding</span><span class="sxs-lookup"><span data-stu-id="5fe8d-132">Install modules and generate scaffolding</span></span>
<span data-ttu-id="5fe8d-133">Nesta seção, você cria um novo aplicativo de nó e usar pacotes de módulo tooadd npm.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-133">In this section you will create a new Node application and use npm tooadd module packages.</span></span> <span data-ttu-id="5fe8d-134">Para este aplicativo, você usará Olá [Express] e [Azure] módulos.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-134">For this application you will use hello [Express] and [Azure] modules.</span></span> <span data-ttu-id="5fe8d-135">módulo do Hello Express fornece uma estrutura de Model View Controller para o nó, durante a saudação módulos do Azure fornece o serviço de tabela de toohello de conectividade.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-135">hello Express module provides a Model View Controller framework for node, while hello Azure modules provides connectivity toohello Table service.</span></span>

### <a name="install-express-and-generate-scaffolding"></a><span data-ttu-id="5fe8d-136">Instalar o express e gerar scaffolding</span><span class="sxs-lookup"><span data-stu-id="5fe8d-136">Install express and generate scaffolding</span></span>
1. <span data-ttu-id="5fe8d-137">Na linha de comando hello, criar um novo diretório chamado **tasklist** e comutador toothat directory.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-137">From hello command line, create a new directory named **tasklist** and switch toothat directory.</span></span>  
2. <span data-ttu-id="5fe8d-138">Digite hello seguindo o módulo do comando tooinstall Olá Express.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-138">Enter hello following command tooinstall hello Express module.</span></span>
   
        npm install express-generator@4.2.0 -g
   
    <span data-ttu-id="5fe8d-139">Dependendo do sistema operacional de saudação, talvez seja necessário tooput 'sudo' antes do comando hello:</span><span class="sxs-lookup"><span data-stu-id="5fe8d-139">Depending on hello operating system, you may need tooput 'sudo' before hello command:</span></span>
   
        sudo npm install express-generator@4.2.0 -g
   
    <span data-ttu-id="5fe8d-140">saída de Hello aparece semelhante toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="5fe8d-140">hello output appears similar toohello following example:</span></span>
   
        express-generator@4.2.0 /usr/local/lib/node_modules/express-generator
        ├── mkdirp@0.3.5
        └── commander@1.3.2 (keypress@0.1.0)
   
   > [!NOTE]
   > <span data-ttu-id="5fe8d-141">Olá '-g' parâmetro instala o módulo de saudação globalmente.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-141">hello '-g' parameter installs hello module globally.</span></span> <span data-ttu-id="5fe8d-142">Dessa forma, podemos usar **express** toogenerate scaffolding de aplicativo da web sem ter que tootype nas informações de caminho adicionais.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-142">That way, we can use **express** toogenerate web app scaffolding without having tootype in additional path information.</span></span>
   > 
   > 
3. <span data-ttu-id="5fe8d-143">scaffolding de saudação do toocreate para o aplicativo hello, digite Olá **express** comando:</span><span class="sxs-lookup"><span data-stu-id="5fe8d-143">toocreate hello scaffolding for hello application, enter hello **express** command:</span></span>
   
        express
   
    <span data-ttu-id="5fe8d-144">saída de Hello deste comando será semelhante toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="5fe8d-144">hello output of this command appears similar toohello following example:</span></span>
   
           create : .
           create : ./package.json
           create : ./app.js
           create : ./public
           create : ./public/images
           create : ./routes
           create : ./routes/index.js
           create : ./routes/users.js
           create : ./public/stylesheets
           create : ./public/stylesheets/style.css
           create : ./views
           create : ./views/index.jade
           create : ./views/layout.jade
           create : ./views/error.jade
           create : ./public/javascripts
           create : ./bin
           create : ./bin/www
   
           install dependencies:
             $ cd . && npm install
   
           run hello app:
             $ DEBUG=my-application ./bin/www
   
    <span data-ttu-id="5fe8d-145">Agora você tem vários novos diretórios e arquivos no hello **tasklist** directory.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-145">You now have several new directories and files in hello **tasklist** directory.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="5fe8d-146">Instalar módulos adicionais</span><span class="sxs-lookup"><span data-stu-id="5fe8d-146">Install additional modules</span></span>
<span data-ttu-id="5fe8d-147">Uma saudação arquivos **express** cria é **Package. JSON**.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-147">One of hello files that **express** creates is **package.json**.</span></span> <span data-ttu-id="5fe8d-148">Esse arquivo contém uma lista das dependências do módulo.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-148">This file contains a list of module dependencies.</span></span> <span data-ttu-id="5fe8d-149">Posteriormente, quando você implanta Olá aplicativo tooApp aplicativos Web do serviço, esse arquivo determina quais módulos toobe instalado no Azure.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-149">Later, when you deploy hello application tooApp Service Web Apps, this file determines which modules need toobe installed on Azure.</span></span>

<span data-ttu-id="5fe8d-150">Em Olá de linha de comando, digite Olá seguintes módulos de saudação do comando tooinstall descritos em hello **Package. JSON** arquivo.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-150">From hello command-line, enter hello following command tooinstall hello modules described in hello **package.json** file.</span></span> <span data-ttu-id="5fe8d-151">Talvez seja necessário toouse 'sudo'.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-151">You may need toouse 'sudo'.</span></span>

    npm install

<span data-ttu-id="5fe8d-152">saída de Hello deste comando será semelhante toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="5fe8d-152">hello output of this command appears similar toohello following example:</span></span>

    debug@0.7.4 node_modules\debug

    cookie-parser@1.0.1 node_modules\cookie-parser
    ├── cookie-signature@1.0.3
    └── cookie@0.1.0

    [...]


<span data-ttu-id="5fe8d-153">Em seguida, digite Olá Olá de tooinstall de comando a seguir [azure], [uuid nó], [nconf] e [async] módulos:</span><span class="sxs-lookup"><span data-stu-id="5fe8d-153">Next, enter hello following command tooinstall hello [azure], [node-uuid], [nconf] and [async] modules:</span></span>

    npm install azure-storage node-uuid async nconf --save

<span data-ttu-id="5fe8d-154">Olá **– salvar** sinalizador adiciona entradas para esses módulos toohello **Package. JSON** arquivo.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-154">hello **--save** flag adds entries for these modules toohello **package.json** file.</span></span>

<span data-ttu-id="5fe8d-155">saída de Hello deste comando será semelhante toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="5fe8d-155">hello output of this command appears similar toohello following example:</span></span>

    async@0.9.0 node_modules\async

    node-uuid@1.4.1 node_modules\node-uuid

    nconf@0.6.9 node_modules\nconf
    ├── ini@1.2.1
    ├── async@0.2.9
    └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.10)

    [...]


## <a name="create-hello-application"></a><span data-ttu-id="5fe8d-156">Criar um aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="5fe8d-156">Create hello application</span></span>
<span data-ttu-id="5fe8d-157">Agora, estamos aplicativo hello de toobuild pronto.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-157">Now we're ready toobuild hello application.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="5fe8d-158">Criar um modelo</span><span class="sxs-lookup"><span data-stu-id="5fe8d-158">Create a model</span></span>
<span data-ttu-id="5fe8d-159">Um *modelo* é um objeto que representa dados de saudação em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-159">A *model* is an object that represents hello data in your application.</span></span> <span data-ttu-id="5fe8d-160">Para o aplicativo hello, modelo somente Olá é um objeto de tarefa que representa um item na lista de tarefas pendentes de saudação.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-160">For hello application, hello only model is a task object, which represents an item in hello to-do list.</span></span> <span data-ttu-id="5fe8d-161">Tarefas terá Olá campos a seguir:</span><span class="sxs-lookup"><span data-stu-id="5fe8d-161">Tasks will have hello following fields:</span></span>

* <span data-ttu-id="5fe8d-162">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="5fe8d-162">PartitionKey</span></span>
* <span data-ttu-id="5fe8d-163">RowKey</span><span class="sxs-lookup"><span data-stu-id="5fe8d-163">RowKey</span></span>
* <span data-ttu-id="5fe8d-164">nome (cadeia de caracteres)</span><span class="sxs-lookup"><span data-stu-id="5fe8d-164">name (string)</span></span>
* <span data-ttu-id="5fe8d-165">categoria (cadeia de caracteres)</span><span class="sxs-lookup"><span data-stu-id="5fe8d-165">category (string)</span></span>
* <span data-ttu-id="5fe8d-166">concluído (booleano)</span><span class="sxs-lookup"><span data-stu-id="5fe8d-166">completed (Boolean)</span></span>

<span data-ttu-id="5fe8d-167">**PartitionKey** e **RowKey** são usados por Olá serviço tabela como chaves de tabela.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-167">**PartitionKey** and **RowKey** are used by hello Table Service as table keys.</span></span> <span data-ttu-id="5fe8d-168">Para obter mais informações, consulte [modelo de dados de serviço tabela Noções básicas sobre Olá](https://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="5fe8d-168">For more information, see [Understanding hello Table Service data model](https://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

1. <span data-ttu-id="5fe8d-169">Em Olá **tasklist** diretório, crie um novo diretório chamado **modelos**.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-169">In hello **tasklist** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="5fe8d-170">Em Olá **modelos** diretório, crie um novo arquivo chamado **task.js**.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-170">In hello **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="5fe8d-171">Esse arquivo irá conter modelo Olá Olá tarefas criados pelo seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-171">This file will contain hello model for hello tasks created by your application.</span></span>
3. <span data-ttu-id="5fe8d-172">Início de saudação do hello **task.js** de arquivo, adicione Olá bibliotecas tooreference necessárias de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="5fe8d-172">At hello beginning of hello **task.js** file, add hello following code tooreference required libraries:</span></span>
   
        var azure = require('azure-storage');
          var uuid = require('node-uuid');
        var entityGen = azure.TableUtilities.entityGenerator;
4. <span data-ttu-id="5fe8d-173">Adicione seguinte Olá código toodefine e exportar o objeto de tarefa hello.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-173">Add hello following code toodefine and export hello Task object.</span></span> <span data-ttu-id="5fe8d-174">Esse objeto é responsável por conectar-se a tabela de toohello.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-174">This object is responsible for connecting toohello table.</span></span>
   
          module.exports = Task;
   
        function Task(storageClient, tableName, partitionKey) {
          this.storageClient = storageClient;
          this.tableName = tableName;
          this.partitionKey = partitionKey;
          this.storageClient.createTableIfNotExists(tableName, function tableCreated(error) {
            if(error) {
              throw error;
            }
          });
        };
5. <span data-ttu-id="5fe8d-175">Adicione Olá métodos adicionais de toodefine de código a seguir em objeto de tarefa hello, que permitem que as interações com os dados armazenados na tabela de saudação:</span><span class="sxs-lookup"><span data-stu-id="5fe8d-175">Add hello following code toodefine additional methods on hello Task object, which allow interactions with data stored in hello table:</span></span>
   
        Task.prototype = {
          find: function(query, callback) {
            self = this;
            self.storageClient.queryEntities(this.tableName, query, null, function entitiesQueried(error, result) {
              if(error) {
                callback(error);
              } else {
                callback(null, result.entries);
              }
            });
          },
   
          addItem: function(item, callback) {
            self = this;
            // use entityGenerator tooset types
            // NOTE: RowKey must be a string type, even though
            // it contains a GUID in this example.
            var itemDescriptor = {
              PartitionKey: entityGen.String(self.partitionKey),
              RowKey: entityGen.String(uuid()),
              name: entityGen.String(item.name),
              category: entityGen.String(item.category),
              completed: entityGen.Boolean(false)
            };
            self.storageClient.insertEntity(self.tableName, itemDescriptor, function entityInserted(error) {
              if(error){  
                callback(error);
              }
              callback(null);
            });
          },
   
          updateItem: function(rKey, callback) {
            self = this;
            self.storageClient.retrieveEntity(self.tableName, self.partitionKey, rKey, function entityQueried(error, entity) {
              if(error) {
                callback(error);
              }
              entity.completed._ = true;
              self.storageClient.updateEntity(self.tableName, entity, function entityUpdated(error) {
                if(error) {
                  callback(error);
                }
                callback(null);
              });
            });
          }
        }
6. <span data-ttu-id="5fe8d-176">Salve e feche o hello **task.js** arquivo.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-176">Save and close hello **task.js** file.</span></span>

### <a name="create-a-controller"></a><span data-ttu-id="5fe8d-177">Criar um controlador</span><span class="sxs-lookup"><span data-stu-id="5fe8d-177">Create a controller</span></span>
<span data-ttu-id="5fe8d-178">Um *controlador* lida com solicitações HTTP e processa a resposta Olá HTML.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-178">A *controller* handles HTTP requests and renders hello HTML response.</span></span>

1. <span data-ttu-id="5fe8d-179">Em Olá **tasklist/rotas** diretório, crie um novo arquivo chamado **tasklist.js** e abri-lo em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-179">In hello **tasklist/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="5fe8d-180">Adicionar Olá código a seguir muito**tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-180">Add hello following code too**tasklist.js**.</span></span> <span data-ttu-id="5fe8d-181">Isso carrega hello azure e async módulos, que são usados por **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-181">This loads hello azure and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="5fe8d-182">Isso também define Olá **TaskList** função, que é passada a uma instância do hello **tarefa** objeto definimos anteriormente:</span><span class="sxs-lookup"><span data-stu-id="5fe8d-182">This also defines hello **TaskList** function, which is passed an instance of hello **Task** object we defined earlier:</span></span>
   
        var azure = require('azure-storage');
        var async = require('async');
   
        module.exports = TaskList;
3. <span data-ttu-id="5fe8d-183">Defina um objeto **TaskList** .</span><span class="sxs-lookup"><span data-stu-id="5fe8d-183">Define a **TaskList** object.</span></span>
   
        function TaskList(task) {
          this.task = task;
        }
4. <span data-ttu-id="5fe8d-184">Adicionar Olá métodos a seguir muito**TaskList**:</span><span class="sxs-lookup"><span data-stu-id="5fe8d-184">Add hello following methods too**TaskList**:</span></span>
   
        TaskList.prototype = {
          showTasks: function(req, res) {
            self = this;
            var query = new azure.TableQuery()
              .where('completed eq ?', false);
            self.task.find(query, function itemsFound(error, items) {
              res.render('index',{title: 'My ToDo List ', tasks: items});
            });
          },
   
          addTask: function(req,res) {
            var self = this;
            var item = req.body.item;
            self.task.addItem(item, function itemAdded(error) {
              if(error) {
                throw error;
              }
              res.redirect('/');
            });
          },
   
          completeTask: function(req,res) {
            var self = this;
            var completedTasks = Object.keys(req.body);
            async.forEach(completedTasks, function taskIterator(completedTask, callback) {
              self.task.updateItem(completedTask, function itemsUpdated(error) {
                if(error){
                  callback(error);
                } else {
                  callback(null);
                }
              });
            }, function goHome(error){
              if(error) {
                throw error;
              } else {
               res.redirect('/');
              }
            });
          }
        }

### <a name="modify-appjs"></a><span data-ttu-id="5fe8d-185">Modificar app.js</span><span class="sxs-lookup"><span data-stu-id="5fe8d-185">Modify app.js</span></span>
1. <span data-ttu-id="5fe8d-186">De saudação **tasklist** Olá diretório, abra **app.js** arquivo.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-186">From hello **tasklist** directory, open hello **app.js** file.</span></span> <span data-ttu-id="5fe8d-187">Este arquivo foi criado anteriormente executando Olá **express** comando.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-187">This file was created earlier by running hello **express** command.</span></span>
2. <span data-ttu-id="5fe8d-188">Início de saudação do arquivo hello, adicione Olá tooload hello azure módulo, nome de tabela do conjunto hello, chave de partição e conjunto de credenciais de armazenamento de saudação usadas por este exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="5fe8d-188">At hello beginning of hello file, add hello following tooload hello azure module, set hello table name, partition key, and set hello storage credentials used by this example:</span></span>
   
        var azure = require('azure-storage');
        var nconf = require('nconf');
        nconf.env()
             .file({ file: 'config.json', search: true });
        var tableName = nconf.get("TABLE_NAME");
        var partitionKey = nconf.get("PARTITION_KEY");
        var accountName = nconf.get("STORAGE_NAME");
        var accountKey = nconf.get("STORAGE_KEY");
   
   > [!NOTE]
   > <span data-ttu-id="5fe8d-189">nconf carregará os valores de configuração de saudação de variáveis de ambiente ou hello **config. JSON** arquivo, que vamos criar mais tarde.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-189">nconf will load hello configuration values from either environment variables or hello **config.json** file, which we will create later.</span></span>
   > 
   > 
3. <span data-ttu-id="5fe8d-190">No arquivo de app.js hello, role para baixo toowhere você ver Olá linha a seguir:</span><span class="sxs-lookup"><span data-stu-id="5fe8d-190">In hello app.js file, scroll down toowhere you see hello following line:</span></span>
   
        app.use('/', routes);
        app.use('/users', users);
   
    <span data-ttu-id="5fe8d-191">Substitua Olá acima linhas com o código de saudação mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-191">Replace hello above lines with hello code shown below.</span></span> <span data-ttu-id="5fe8d-192">Inicializar uma instância de <strong>tarefa</strong> com uma conta de armazenamento de tooyour de conexão.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-192">This will initialize an instance of <strong>Task</strong> with a connection tooyour storage account.</span></span> <span data-ttu-id="5fe8d-193">Isso é passado toohello <strong>TaskList</strong>, que irá usá-la toocommunicate com hello serviço tabela:</span><span class="sxs-lookup"><span data-stu-id="5fe8d-193">This is passed toohello <strong>TaskList</strong>, which will use it toocommunicate with hello Table service:</span></span>
   
        var TaskList = require('./routes/tasklist');
        var Task = require('./models/task');
        var task = new Task(azure.createTableService(accountName, accountKey), tableName, partitionKey);
        var taskList = new TaskList(task);
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
4. <span data-ttu-id="5fe8d-194">Salvar Olá **app.js** arquivo.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-194">Save hello **app.js** file.</span></span>

### <a name="modify-hello-index-view"></a><span data-ttu-id="5fe8d-195">Modificar a exibição do índice Olá</span><span class="sxs-lookup"><span data-stu-id="5fe8d-195">Modify hello index view</span></span>
1. <span data-ttu-id="5fe8d-196">Olá abrir **tasklist/views/index.jade** em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-196">Open hello **tasklist/views/index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="5fe8d-197">Substitua todo o conteúdo do arquivo de Olá Olá Olá código a seguir.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-197">Replace hello entire contents of hello file with hello following code.</span></span> <span data-ttu-id="5fe8d-198">Isso define o modo de exibição das tarefas existentes, bem como um formulário para adicionar novas tarefas e marcar as tarefas existentes como concluídas.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-198">This defines a view that displays existing tasks and includes a form for adding new tasks and marking existing ones as completed.</span></span>
   
        extends layout
   
        block content
          h1= title
          br
   
          form(action="/completetask", method="post")
            table.table.table-striped.table-bordered
              tr
                td Name
                td Category
                td Date
                td Complete
              if (typeof tasks === "undefined")
                tr
                  td
              else
                each task in tasks
                  tr
                    td #{task.name._}
                    td #{task.category._}
                    - var day   = task.Timestamp._.getDate();
                    - var month = task.Timestamp._.getMonth() + 1;
                    - var year  = task.Timestamp._.getFullYear();
                    td #{month + "/" + day + "/" + year}
                    td
                      input(type="checkbox", name="#{task.RowKey._}", value="#{!task.completed._}", checked=task.completed._)
            button.btn(type="submit") Update tasks
          hr
          form.well(action="/addtask", method="post")
            label Item Name:
            input(name="item[name]", type="textbox")
            label Item Category:
            input(name="item[category]", type="textbox")
            br
            button.btn(type="submit") Add item
3. <span data-ttu-id="5fe8d-199">Salve e feche o arquivo **index.jade** .</span><span class="sxs-lookup"><span data-stu-id="5fe8d-199">Save and close **index.jade** file.</span></span>

### <a name="modify-hello-global-layout"></a><span data-ttu-id="5fe8d-200">Modificar o layout global Olá</span><span class="sxs-lookup"><span data-stu-id="5fe8d-200">Modify hello global layout</span></span>
<span data-ttu-id="5fe8d-201">Olá **layout.jade** arquivo hello **exibições** diretório é um modelo global para outros **.jade** arquivos.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-201">hello **layout.jade** file in hello **views** directory is a global template for other **.jade** files.</span></span> <span data-ttu-id="5fe8d-202">Nesta etapa você modificá-la toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), que é um kit de ferramentas que torna mais fácil toodesign um aplicativo de web buscam adequado.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-202">In this step you will modify it toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy toodesign a nice looking web app.</span></span>

<span data-ttu-id="5fe8d-203">Baixe e extraia os arquivos de saudação para [Twitter Bootstrap](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="5fe8d-203">Download and extract hello files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="5fe8d-204">Saudação de cópia **bootstrap.min.css** arquivo hello Bootstrap **css** pasta em Olá **público/folhas de estilo** diretório de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-204">Copy hello **bootstrap.min.css** file from hello Bootstrap **css** folder into hello **public/stylesheets** directory of your application.</span></span>

<span data-ttu-id="5fe8d-205">De saudação **exibições** pastas **layout.jade** e substitua todo o conteúdo Olá seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="5fe8d-205">From hello **views** folder, open **layout.jade** and replace hello entire contents with hello following:</span></span>

    doctype html
    html
      head
        title= title
        link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')
        link(rel='stylesheet', href='/stylesheets/style.css')
      body.app
        nav.navbar.navbar-default
          div.navbar-header
          a.navbar-brand(href='/') My Tasks
        block content

### <a name="create-a-config-file"></a><span data-ttu-id="5fe8d-206">Criar um arquivo de configuração</span><span class="sxs-lookup"><span data-stu-id="5fe8d-206">Create a config file</span></span>
<span data-ttu-id="5fe8d-207">toorun aplicativo hello localmente, colocaremos credenciais de armazenamento do Azure em um arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-207">toorun hello app locally, we'll put Azure Storage credentials into a config file.</span></span> <span data-ttu-id="5fe8d-208">Crie um arquivo chamado **config. JSON* * com hello JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="5fe8d-208">Create a file named **config.json* *with hello following JSON:</span></span>

    {
        "STORAGE_NAME": "<storage account name>",
        "STORAGE_KEY": "<storage access key>",
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

<span data-ttu-id="5fe8d-209">Substituir **nome da conta de armazenamento** com nome de saudação do armazenamento Olá conta criada anteriormente e substitua **chave de acesso de armazenamento** com a chave de acesso primária Olá para sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-209">Replace **storage account name** with hello name of hello storage account you created earlier, and replace **storage access key** with hello primary access key for your storage account.</span></span> <span data-ttu-id="5fe8d-210">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="5fe8d-210">For example:</span></span>

    {
        "STORAGE_NAME": "nodejsappstorage",
        "STORAGE_KEY": "KG0oDd..."
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

<span data-ttu-id="5fe8d-211">Salve esse arquivo *um nível de diretório superior* que Olá **tasklist** diretório, como este:</span><span class="sxs-lookup"><span data-stu-id="5fe8d-211">Save this file *one directory level higher* than hello **tasklist** directory, like this:</span></span>

    parent/
      |-- config.json
      |-- tasklist/

<span data-ttu-id="5fe8d-212">razão de saudação para fazer isso é tooavoid Verificando arquivo de configuração de saudação no controle de origem, onde ele pode se tornar público.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-212">hello reason for doing this is tooavoid checking hello config file into source control, where it might become public.</span></span> <span data-ttu-id="5fe8d-213">Quando for implantada Olá aplicativo tooAzure, usaremos as variáveis de ambiente em vez de um arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-213">When we deploy hello app tooAzure, we will use environment variables instead of a config file.</span></span>

## <a name="run-hello-application-locally"></a><span data-ttu-id="5fe8d-214">Executar o aplicativo hello localmente</span><span class="sxs-lookup"><span data-stu-id="5fe8d-214">Run hello application locally</span></span>
<span data-ttu-id="5fe8d-215">aplicativo de hello tootest em seu computador local, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5fe8d-215">tootest hello application on your local machine, perform hello following steps:</span></span>

1. <span data-ttu-id="5fe8d-216">Saudação de linha de comando, alterar diretórios toohello **tasklist** directory.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-216">From hello command-line, change directories toohello **tasklist** directory.</span></span>
2. <span data-ttu-id="5fe8d-217">Use Olá toolaunch Olá aplicativo de comandos do local a seguir:</span><span class="sxs-lookup"><span data-stu-id="5fe8d-217">Use hello following command toolaunch hello application locally:</span></span>
   
        npm start
3. <span data-ttu-id="5fe8d-218">Abra um navegador da web e navegue toohttp://127.0.0.1:3000.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-218">Open a web browser and navigate toohttp://127.0.0.1:3000.</span></span>
   
    <span data-ttu-id="5fe8d-219">Um toohello semelhante de página da web exemplo a seguir é exibida.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-219">A web page similar toohello following example appears.</span></span>
   
    ![Uma página da Web que exibe uma lista de tarefas vazia][node-table-finished]
4. <span data-ttu-id="5fe8d-221">toocreate um novo item de tarefas, insira um nome e uma categoria e clique em **Adicionar Item**.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-221">toocreate a new to-do item, enter a name and category and click **Add Item**.</span></span> 
5. <span data-ttu-id="5fe8d-222">toomark uma tarefa como concluída, verifique **concluir** e clique em **tarefas de atualização**.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-222">toomark a task as complete, check **Complete** and click **Update Tasks**.</span></span>
   
    ![Uma imagem de saudação novo item na lista de saudação de tarefas][node-table-list-items]

<span data-ttu-id="5fe8d-224">Mesmo que o aplicativo hello estiver sendo executado localmente, ele está armazenando dados de saudação em Olá serviço tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-224">Even though hello application is running locally, it is storing hello data in hello Azure Table service.</span></span>

## <a name="deploy-your-application-tooazure"></a><span data-ttu-id="5fe8d-225">Implantar seu aplicativo tooAzure</span><span class="sxs-lookup"><span data-stu-id="5fe8d-225">Deploy your application tooAzure</span></span>
<span data-ttu-id="5fe8d-226">Olá etapas nesta seção usam ferramentas de linha de comando do Azure de saudação toocreate um novo aplicativo web no serviço de aplicativo e, em seguida, usam o Git toodeploy seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-226">hello steps in this section use hello Azure command-line tools toocreate a new web app in App Service, and then use Git toodeploy your application.</span></span> <span data-ttu-id="5fe8d-227">tooperform essas etapas, você deve ter uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-227">tooperform these steps you must have an Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="5fe8d-228">Essas etapas também podem ser executadas usando Olá [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5fe8d-228">These steps can also be performed by using hello [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="5fe8d-229">Confira [Criar e implantar um aplicativo Web do Node.js no Serviço de Aplicativo do Azure].</span><span class="sxs-lookup"><span data-stu-id="5fe8d-229">See [Build and deploy a Node.js web app in Azure App Service].</span></span>
> 
> <span data-ttu-id="5fe8d-230">Se esse for o aplicativo web primeiro Olá que você criou, você deve usar hello Azure Portal toodeploy este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-230">If this is hello first web app you have created, you must use hello Azure Portal toodeploy this application.</span></span>
> 
> 

<span data-ttu-id="5fe8d-231">tooget iniciado, instalar Olá [CLI do Azure] inserindo Olá comando a seguir na linha de comando hello:</span><span class="sxs-lookup"><span data-stu-id="5fe8d-231">tooget started, install hello [Azure CLI] by entering hello following command from hello command line:</span></span>

    npm install azure-cli -g

### <a name="import-publishing-settings"></a><span data-ttu-id="5fe8d-232">Importar configurações de publicação</span><span class="sxs-lookup"><span data-stu-id="5fe8d-232">Import publishing settings</span></span>
<span data-ttu-id="5fe8d-233">Nesta etapa, você baixará um arquivo que contém informações sobre sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-233">In this step, you will download a file containing information about your subscription.</span></span>

1. <span data-ttu-id="5fe8d-234">Digite hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="5fe8d-234">Enter hello following command:</span></span>
   
        azure login
   
    <span data-ttu-id="5fe8d-235">Esse comando inicia um navegador e navega toohello página de download.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-235">This command launches a browser and navigates toohello download page.</span></span> <span data-ttu-id="5fe8d-236">Se solicitado, faça logon com conta Olá associada à sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-236">If prompted, log in with hello account associated with your Azure subscription.</span></span>
   
    <!-- ![hello download page][download-publishing-settings] -->
   
    <span data-ttu-id="5fe8d-237">download do arquivo Hello começa automaticamente. Se não estiver, você pode clicar Olá link no início de Olá Olá toomanually download saudação do arquivo de página.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-237">hello file download begins automatically; if it does not, you can click hello link at hello beginning of hello page toomanually download hello file.</span></span> <span data-ttu-id="5fe8d-238">Salve o caminho de arquivo de saudação de observação e de saudação.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-238">Save hello file and note hello file path.</span></span>
2. <span data-ttu-id="5fe8d-239">Digite hello configurações do comando tooimport Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="5fe8d-239">Enter hello following command tooimport hello settings:</span></span>
   
        azure account import <path-to-file>
   
    <span data-ttu-id="5fe8d-240">Especifica nome de arquivo e caminho de Olá do Olá publicando o arquivo de configurações que você baixou na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-240">Specify hello path and file name of hello publishing settings file you downloaded in hello previous step.</span></span>
3. <span data-ttu-id="5fe8d-241">Depois que as configurações de saudação são importadas, excluir Olá publicar o arquivo de configurações.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-241">After hello settings are imported, delete hello publish settings file.</span></span> <span data-ttu-id="5fe8d-242">Ele não é mais necessário e contém informações confidenciais sobre sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-242">It is no longer needed, and contains sensitive information regarding your Azure subscription.</span></span>

### <a name="create-an-app-service-web-app"></a><span data-ttu-id="5fe8d-243">Criar um aplicativo Web do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="5fe8d-243">Create an App Service web app</span></span>
1. <span data-ttu-id="5fe8d-244">Saudação de linha de comando, alterar diretórios toohello **tasklist** directory.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-244">From hello command-line, change directories toohello **tasklist** directory.</span></span>
2. <span data-ttu-id="5fe8d-245">Use Olá comando toocreate um novo aplicativo web a seguir.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-245">Use hello following command toocreate a new web app.</span></span>
   
        azure site create --git
   
    <span data-ttu-id="5fe8d-246">Você será solicitado para o local e o nome do aplicativo web hello.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-246">You will be prompted for hello web app name and location.</span></span> <span data-ttu-id="5fe8d-247">Forneça um nome exclusivo e selecione Olá mesmo local geográfico da sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-247">Provide a unique name and select hello same geographical location as your Azure Storage account.</span></span>
   
    <span data-ttu-id="5fe8d-248">Olá `--git` parâmetro cria um repositório Git no Azure para este aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-248">hello `--git` parameter creates a Git repository on Azure for this web app.</span></span> <span data-ttu-id="5fe8d-249">Inicializa um repositório Git no diretório atual Olá também se nenhum existir e adiciona um [Git remoto] denominado 'do azure', que é usado toopublish Olá aplicativo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-249">It also initializes a Git repository in hello current directory if none exists, and adds a [Git remote] named 'azure', which is used toopublish hello application tooAzure.</span></span> <span data-ttu-id="5fe8d-250">Por fim, ele cria um **Web. config** arquivo, que contém as configurações usadas por aplicativos de nó toohost do Azure.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-250">Finally, it creates a **web.config** file, which contains settings used by Azure toohost node applications.</span></span> <span data-ttu-id="5fe8d-251">Se você omitir Olá `--git` parâmetro mas Olá diretório contém um repositório Git, comando Olá ainda criará remoto Olá 'do azure'.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-251">If you omit hello `--git` parameter but hello directory contains a Git repository, hello command will still create hello 'azure' remote.</span></span>
   
    <span data-ttu-id="5fe8d-252">Quando esse comando for concluído, você verá a seguinte de toohello semelhante de saída.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-252">Once this command has completed, you will see output similar toohello following.</span></span> <span data-ttu-id="5fe8d-253">Observe que Olá linha a partir **site criado em** contém Olá URL do aplicativo web de saudação.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-253">Note that hello line beginning with **Website created at** contains hello URL for hello web app.</span></span>
   
        info:   Executing command site create
        help:   Need a site name
        Name: TableTasklist
        info:   Using location southcentraluswebspace
        info:   Executing `git init`
        info:   Creating default .gitignore file
        info:   Creating a new web site
        info:   Created web site at  tabletasklist.azurewebsites.net
        info:   Initializing repository
        info:   Repository initialized
        info:   Executing `git remote add azure https://username@tabletasklist.azurewebsites.net/TableTasklist.git`
        info:   site create command OK
   
   > [!NOTE]
   > <span data-ttu-id="5fe8d-254">Se isso for Olá primeiro aplicativo do serviço de aplicativo web para sua assinatura, você será toouse instruções hello Azure Portal toocreate Olá web app.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-254">If this is hello first App Service web app for your subscription, you will be instructed toouse hello Azure Portal toocreate hello web app.</span></span> <span data-ttu-id="5fe8d-255">Para obter mais informações, consulte [Criar e implantar um aplicativo Web do Node.js no Serviço de Aplicativo do Azure].</span><span class="sxs-lookup"><span data-stu-id="5fe8d-255">For more information, see [Build and deploy a Node.js web app in Azure App Service].</span></span>
   > 
   > 

### <a name="set-environment-variables"></a><span data-ttu-id="5fe8d-256">Configurar variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="5fe8d-256">Set environment variables</span></span>
<span data-ttu-id="5fe8d-257">Nesta etapa, você irá adicionar a configuração de aplicativo web do tooyour de variáveis de ambiente no Azure.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-257">In this step, you will add environment variables tooyour web app configuration on Azure.</span></span>
<span data-ttu-id="5fe8d-258">Na linha de comando hello, digite seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="5fe8d-258">From hello command line, enter hello following:</span></span>

    azure site appsetting add
        STORAGE_NAME=<storage account name>;STORAGE_KEY=<storage access key>;PARTITION_KEY=mytasks;TABLE_NAME=tasks


<span data-ttu-id="5fe8d-259">Substituir  **<storage account name>**  com nome de saudação do armazenamento Olá conta criada anteriormente e substitua  **<storage access key>**  com a chave de acesso primária Olá para sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-259">Replace **<storage account name>** with hello name of hello storage account you created earlier, and replace **<storage access key>** with hello primary access key for your storage account.</span></span> <span data-ttu-id="5fe8d-260">(Use Olá mesmos valores como arquivo de config. JSON Olá que você criou anteriormente).</span><span class="sxs-lookup"><span data-stu-id="5fe8d-260">(Use hello same values as hello config.json file that you created earlier.)</span></span>

<span data-ttu-id="5fe8d-261">Como alternativa, você pode definir variáveis de ambiente no hello [Portal do Azure](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="5fe8d-261">Alternatively, you can set environment variables in hello [Azure Portal](https://portal.azure.com/):</span></span>

1. <span data-ttu-id="5fe8d-262">Abra a folha de seu aplicativo da web hello clicando **procurar** > **aplicativos Web** > nome do aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-262">Open hello web app's blade by clicking **Browse** > **Web Apps** > your web app name.</span></span>
2. <span data-ttu-id="5fe8d-263">Na folha do seu aplicativo Web, clique em **Todas as configurações** > **Configurações do Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-263">In your web app's blade, click **All Settings** > **Application Settings**.</span></span>
   
     <!-- ![Top Menu](./media/storage-nodejs-use-table-storage-web-site/PollsCommonWebSiteTopMenu.png) -->
3. <span data-ttu-id="5fe8d-264">Role para baixo toohello **configurações do aplicativo** seção e adicionar pares de chave/valor hello.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-264">Scroll down toohello **App settings** section and add hello key/value pairs.</span></span>
   
     ![Configurações do aplicativo](./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png)
4. <span data-ttu-id="5fe8d-266">Clique em **SALVAR**.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-266">Click **SAVE**.</span></span>

### <a name="publish-hello-application"></a><span data-ttu-id="5fe8d-267">Publicar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="5fe8d-267">Publish hello application</span></span>
<span data-ttu-id="5fe8d-268">toopublish Olá aplicativo, Olá tooGit de arquivos de código de confirmação e, em seguida, enviar por push tooazure/mestre.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-268">toopublish hello app, commit hello code files tooGit and then push tooazure/master.</span></span>

1. <span data-ttu-id="5fe8d-269">Configure suas credenciais de implantação.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-269">Set your deployment credentials.</span></span>
   
        azure site deployment user set <name> <password>
2. <span data-ttu-id="5fe8d-270">Adicione e confirme os arquivos do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-270">Add and commit your application files.</span></span>
   
        git add .
        git commit -m "adding files"
3. <span data-ttu-id="5fe8d-271">Enviar por push Olá confirmação toohello aplicativo do serviço de aplicativo web:</span><span class="sxs-lookup"><span data-stu-id="5fe8d-271">Push hello commit toohello App Service web app:</span></span>
   
        git push azure master
   
    <span data-ttu-id="5fe8d-272">Use **mestre** como branch de destino hello.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-272">Use **master** as hello target branch.</span></span> <span data-ttu-id="5fe8d-273">No final de saudação da implantação Olá, você verá um toohello semelhante instrução exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="5fe8d-273">At hello end of hello deployment, you see a statement similar toohello following example:</span></span>
   
        toohttps://username@tabletasklist.azurewebsites.net/TableTasklist.git
          * [new branch]      master -> master
4. <span data-ttu-id="5fe8d-274">Após a conclusão da operação de envio hello, procurar toohello URL do aplicativo web retornado anteriormente pelo Olá `azure create site` comando tooview seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5fe8d-274">Once hello push operation has completed, browse toohello web app URL returned previously by hello `azure create site` command tooview your application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5fe8d-275">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5fe8d-275">Next steps</span></span>
<span data-ttu-id="5fe8d-276">Olá etapas neste artigo descrevem usando informações de toostore Olá serviço tabela, você também pode usar [MongoDB](https://mlab.com/azure/).</span><span class="sxs-lookup"><span data-stu-id="5fe8d-276">While hello steps in this article describe using hello Table Service toostore information, you can also use [MongoDB](https://mlab.com/azure/).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5fe8d-277">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="5fe8d-277">Additional resources</span></span>
<span data-ttu-id="5fe8d-278">[CLI do Azure]</span><span class="sxs-lookup"><span data-stu-id="5fe8d-278">[Azure CLI]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="5fe8d-279">O que mudou</span><span class="sxs-lookup"><span data-stu-id="5fe8d-279">What's changed</span></span>
* <span data-ttu-id="5fe8d-280">Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="5fe8d-280">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- URLs -->

[Criar e implantar um aplicativo Web do Node.js no Serviço de Aplicativo do Azure]: app-service-web-get-started-nodejs.md
[Azure Developer Center]: /develop/nodejs/

[nó]: http://nodejs.org
[Git]: http://git-scm.com
[Express]: http://expressjs.com
[for free]: http://windowsazure.com
[Git remoto]: http://git-scm.com/docs/git-remote

[CLI do Azure]:../cli-install-nodejs.md

[azure]: https://github.com/Azure/azure-sdk-for-node
[uuid nó]: https://www.npmjs.com/package/node-uuid
[nconf]: https://www.npmjs.com/package/nconf
[async]: https://www.npmjs.com/package/async

[Azure Portal]: https://portal.azure.com

[Create and deploy a Node.js application tooan Azure Web Site]: app-service-web-get-started-nodejs.md

<!-- Image References -->

[node-table-finished]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_empty.png
[node-table-list-items]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_list.png
[download-publishing-settings]: ./media/storage-nodejs-use-table-storage-web-site/azure-account-download-cli.png
[portal-storage-access-keys]: ./media/storage-nodejs-use-table-storage-web-site/manage-access-keys.png
[app-settings]: ./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png
