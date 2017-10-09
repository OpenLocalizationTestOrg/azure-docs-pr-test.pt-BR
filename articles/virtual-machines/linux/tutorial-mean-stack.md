---
title: "aaaCreate uma média de pilha em uma VM do Linux no Azure | Microsoft Docs"
description: "Saiba como o Node. js (média), Express, AngularJS e toocreate um MongoDB pilha em uma VM do Linux no Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/08/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 82a8e34e60d2bb6e6670ee007faa1113ea78b716
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-mongodb-express-angularjs-and-nodejs-mean-stack-on-a-linux-vm-in-azure"></a><span data-ttu-id="43b5a-103">Criar uma pilha MongoDB, Expresso, AngularJS e Node.js (MEAN) em uma VM do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="43b5a-103">Create a MongoDB, Express, AngularJS, and Node.js (MEAN) stack on a Linux VM in Azure</span></span>

<span data-ttu-id="43b5a-104">Este tutorial mostra como o Node. js (média), Express, AngularJS e tooimplement um MongoDB pilha em uma VM do Linux no Azure.</span><span class="sxs-lookup"><span data-stu-id="43b5a-104">This tutorial shows you how tooimplement a MongoDB, Express, AngularJS, and Node.js (MEAN) stack on a Linux VM in Azure.</span></span> <span data-ttu-id="43b5a-105">pilha de média de saudação que você cria permite adicionar, excluir e listar manuais em um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="43b5a-105">hello MEAN stack that you create enables adding, deleting, and listing books in a database.</span></span> <span data-ttu-id="43b5a-106">Você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="43b5a-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="43b5a-107">Criar uma VM do Linux</span><span class="sxs-lookup"><span data-stu-id="43b5a-107">Create a Linux VM</span></span>
> * <span data-ttu-id="43b5a-108">Instalar o Node. js</span><span class="sxs-lookup"><span data-stu-id="43b5a-108">Install Node.js</span></span>
> * <span data-ttu-id="43b5a-109">Instalar o MongoDB e configurar o servidor de saudação</span><span class="sxs-lookup"><span data-stu-id="43b5a-109">Install MongoDB and set up hello server</span></span>
> * <span data-ttu-id="43b5a-110">Express de instalar e configurar o servidor de toohello de rotas</span><span class="sxs-lookup"><span data-stu-id="43b5a-110">Install Express and set up routes toohello server</span></span>
> * <span data-ttu-id="43b5a-111">Rotas de saudação do acesso com AngularJS</span><span class="sxs-lookup"><span data-stu-id="43b5a-111">Access hello routes with AngularJS</span></span>
> * <span data-ttu-id="43b5a-112">Executar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="43b5a-112">Run hello application</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="43b5a-113">Se você escolher tooinstall e usa o hello CLI localmente, este tutorial requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="43b5a-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="43b5a-114">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="43b5a-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="43b5a-115">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="43b5a-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>


## <a name="create-a-linux-vm"></a><span data-ttu-id="43b5a-116">Criar uma VM do Linux</span><span class="sxs-lookup"><span data-stu-id="43b5a-116">Create a Linux VM</span></span>

<span data-ttu-id="43b5a-117">Criar um grupo de recursos com hello [criar grupo az](https://docs.microsoft.com/cli/azure/group#create) de comando e criar uma VM do Linux com hello [criar vm az](https://docs.microsoft.com/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="43b5a-117">Create a resource group with hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command and create a Linux VM with hello [az vm create](https://docs.microsoft.com/cli/azure/vm#create) command.</span></span> <span data-ttu-id="43b5a-118">Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="43b5a-118">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="43b5a-119">Olá, exemplo a seguir usa Olá CLI do Azure toocreate um grupo de recursos denominado *myResourceGroupMEAN* em Olá *eastus* local.</span><span class="sxs-lookup"><span data-stu-id="43b5a-119">hello following example uses hello Azure CLI toocreate a resource group named *myResourceGroupMEAN* in hello *eastus* location.</span></span> <span data-ttu-id="43b5a-120">Uma VM é criada com o nome *myVM* com chaves SSH, caso elas ainda não existam em um local de chave padrão.</span><span class="sxs-lookup"><span data-stu-id="43b5a-120">A VM is created named *myVM* with SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="43b5a-121">toouse um conjunto específico de chaves, use hello – opção ssh-chave-valor.</span><span class="sxs-lookup"><span data-stu-id="43b5a-121">toouse a specific set of keys, use hello --ssh-key-value option.</span></span>

```azurecli-interactive
az group create --name myResourceGroupMEAN --location eastus
az vm create \
    --resource-group myResourceGroupMEAN \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --admin-password 'Azure12345678!' \
    --generate-ssh-keys
az vm open-port --port 3300 --resource-group myResourceGroupMEAN --name myVM
```

<span data-ttu-id="43b5a-122">Quando Olá VM tiver sido criado, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="43b5a-122">When hello VM has been created, hello Azure CLI shows information similar toohello following example:</span></span> 

```azurecli-interactive
{
  "fqdns": "",
  "id": "/subscriptions/{subscription-id}/resourceGroups/myResourceGroupMEAN/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.72.77.9",
  "resourceGroup": "myResourceGroupMEAN"
}
```
<span data-ttu-id="43b5a-123">Anote Olá `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="43b5a-123">Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="43b5a-124">Esse endereço é usado tooaccess Olá VM.</span><span class="sxs-lookup"><span data-stu-id="43b5a-124">This address is used tooaccess hello VM.</span></span>

<span data-ttu-id="43b5a-125">A seguir Olá Use o comando toocreate uma sessão SSH com hello VM.</span><span class="sxs-lookup"><span data-stu-id="43b5a-125">Use hello following command toocreate an SSH session with hello VM.</span></span> <span data-ttu-id="43b5a-126">Certifique-se de toouse Olá endereço IP público correto.</span><span class="sxs-lookup"><span data-stu-id="43b5a-126">Make sure toouse hello correct public IP address.</span></span> <span data-ttu-id="43b5a-127">Em nosso exemplo acima, o endereço IP era 13.72.77.9.</span><span class="sxs-lookup"><span data-stu-id="43b5a-127">In our example above our IP address was 13.72.77.9.</span></span>

```bash
ssh azureuser@13.72.77.9
```

## <a name="install-nodejs"></a><span data-ttu-id="43b5a-128">Instalar o Node. js</span><span class="sxs-lookup"><span data-stu-id="43b5a-128">Install Node.js</span></span>

<span data-ttu-id="43b5a-129">O [Node.js](https://nodejs.org/en/) é um tempo de execução de JavaScript baseado no mecanismo de JavaScript V8 do Chrome.</span><span class="sxs-lookup"><span data-stu-id="43b5a-129">[Node.js](https://nodejs.org/en/) is a JavaScript runtime built on Chrome's V8 JavaScript engine.</span></span> <span data-ttu-id="43b5a-130">Node. js é usado neste tutorial tooset Olá que roteia Express e controladores AngularJS.</span><span class="sxs-lookup"><span data-stu-id="43b5a-130">Node.js is used in this tutorial tooset up hello Express routes and AngularJS controllers.</span></span>

<span data-ttu-id="43b5a-131">Em Olá VM, usando o shell bash Olá que você abriu com SSH, instale o Node. js.</span><span class="sxs-lookup"><span data-stu-id="43b5a-131">On hello VM, using hello bash shell that you opened with SSH, install Node.js.</span></span>

```bash
sudo apt-get install -y nodejs
```

## <a name="install-mongodb-and-set-up-hello-server"></a><span data-ttu-id="43b5a-132">Instalar o MongoDB e configurar o servidor de saudação</span><span class="sxs-lookup"><span data-stu-id="43b5a-132">Install MongoDB and set up hello server</span></span>
<span data-ttu-id="43b5a-133">O [MongoDB](http://www.mongodb.com) armazena dados em documentos flexíveis, como JSON.</span><span class="sxs-lookup"><span data-stu-id="43b5a-133">[MongoDB](http://www.mongodb.com) stores data in flexible, JSON-like documents.</span></span> <span data-ttu-id="43b5a-134">Campos em um banco de dados podem variar de documento toodocument e estrutura de dados pode ser alterada ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="43b5a-134">Fields in a database can vary from document toodocument and data structure can be changed over time.</span></span> <span data-ttu-id="43b5a-135">Em nosso aplicativo de exemplo, estamos adicionando tooMongoDB de registros de catálogo que contêm o nome do catálogo, o número isbn, autor e número de páginas.</span><span class="sxs-lookup"><span data-stu-id="43b5a-135">For our example application, we are adding book records tooMongoDB that contain book name, isbn number, author, and number of pages.</span></span> 

1. <span data-ttu-id="43b5a-136">No hello VM, usando o shell bash Olá que você abriu com SSH, defina a chave do MongoDB de saudação.</span><span class="sxs-lookup"><span data-stu-id="43b5a-136">On hello VM, using hello bash shell that you opened with SSH, set hello MongoDB key.</span></span>

    ```bash
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
    echo "deb [ arch=amd64 ] http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
    ```

2. <span data-ttu-id="43b5a-137">Atualize Gerenciador de pacotes de saudação com chave hello.</span><span class="sxs-lookup"><span data-stu-id="43b5a-137">Update hello package manager with hello key.</span></span>
  
    ```bash
    sudo apt-get update
    ```

3. <span data-ttu-id="43b5a-138">Instale o MongoDB.</span><span class="sxs-lookup"><span data-stu-id="43b5a-138">Install MongoDB.</span></span>

    ```bash
    sudo apt-get install -y mongodb
    ```

4. <span data-ttu-id="43b5a-139">Servidor de saudação inicial.</span><span class="sxs-lookup"><span data-stu-id="43b5a-139">Start hello server.</span></span>

    ```bash
    sudo service mongodb start
    ```

5. <span data-ttu-id="43b5a-140">Também precisamos Olá tooinstall [corpo analisador](https://www.npmjs.com/package/body-parser-json) toohelp de pacote nos processar Olá JSON transmitido no servidor de toohello de solicitações.</span><span class="sxs-lookup"><span data-stu-id="43b5a-140">We also need tooinstall hello [body-parser](https://www.npmjs.com/package/body-parser-json) package toohelp us process hello JSON passed in requests toohello server.</span></span>

    <span data-ttu-id="43b5a-141">Instale o Gerenciador de pacote de npm hello.</span><span class="sxs-lookup"><span data-stu-id="43b5a-141">Install hello npm package manager.</span></span>

    ```bash
    sudo apt-get install npm
    ```

    <span data-ttu-id="43b5a-142">Instale o pacote de analisador de corpo de saudação.</span><span class="sxs-lookup"><span data-stu-id="43b5a-142">Install hello body parser package.</span></span>
    
    ```bash
    sudo npm install body-parser
    ```

6. <span data-ttu-id="43b5a-143">Crie uma pasta chamada *manuais* e adicione um tooit arquivo denominado *server.js* que contém a configuração de saudação para Olá web server.</span><span class="sxs-lookup"><span data-stu-id="43b5a-143">Create a folder named *Books* and add a file tooit named *server.js* that contains hello configuration for hello web server.</span></span>

    ```node.js
    var express = require('express');
    var bodyParser = require('body-parser');
    var app = express();
    app.use(express.static(__dirname + '/public'));
    app.use(bodyParser.json());
    require('./apps/routes')(app);
    app.set('port', 3300);
    app.listen(app.get('port'), function() {
        console.log('Server up: http://localhost:' + app.get('port'));
    });
    ```

## <a name="install-express-and-set-up-routes-toohello-server"></a><span data-ttu-id="43b5a-144">Express de instalar e configurar o servidor de toohello de rotas</span><span class="sxs-lookup"><span data-stu-id="43b5a-144">Install Express and set up routes toohello server</span></span>

<span data-ttu-id="43b5a-145">O [Expresso](https://expressjs.com) é uma estrutura de aplicativo Web mínima e flexível de Node.js que fornece recursos para aplicativos Web e móveis.</span><span class="sxs-lookup"><span data-stu-id="43b5a-145">[Express](https://expressjs.com) is a minimal and flexible Node.js web application framework that provides features for web and mobile applications.</span></span> <span data-ttu-id="43b5a-146">Express é usado em tooand de informações de catálogo este tutorial toopass de nosso banco de dados do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="43b5a-146">Express is used in this tutorial toopass book information tooand from our MongoDB database.</span></span> <span data-ttu-id="43b5a-147">[Mongoose](http://mongoosejs.com) fornece uma solução baseada em esquema direta toomodel os dados do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="43b5a-147">[Mongoose](http://mongoosejs.com) provides a straight-forward, schema-based solution toomodel your application data.</span></span> <span data-ttu-id="43b5a-148">Mongoose é usado neste tutorial tooprovide um esquema de catálogo para o banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="43b5a-148">Mongoose is used in this tutorial tooprovide a book schema for hello database.</span></span>

1. <span data-ttu-id="43b5a-149">Instale o Expresso e o Mongoose.</span><span class="sxs-lookup"><span data-stu-id="43b5a-149">Install Express and Mongoose.</span></span>

    ```bash
    sudo npm install express mongoose
    ```

2. <span data-ttu-id="43b5a-150">Em Olá *manuais* pasta, crie uma pasta chamada *aplicativos* e adicione um arquivo chamado *routes.js* com hello express rotas definidas.</span><span class="sxs-lookup"><span data-stu-id="43b5a-150">In hello *Books* folder, create a folder named *apps* and add a file named *routes.js* with hello express routes defined.</span></span>

    ```node.js
    var Book = require('./models/book');
    module.exports = function(app) {
      app.get('/book', function(req, res) {
        Book.find({}, function(err, result) {
          if ( err ) throw err;
          res.json(result);
        });
      }); 
      app.post('/book', function(req, res) {
        var book = new Book( {
          name:req.body.name,
          isbn:req.body.isbn,
          author:req.body.author,
          pages:req.body.pages
        });
        book.save(function(err, result) {
          if ( err ) throw err;
          res.json( {
            message:"Successfully added book",
            book:result
          });
        });
      });
      app.delete("/book/:isbn", function(req, res) {
        Book.findOneAndRemove(req.query, function(err, result) {
          if ( err ) throw err;
          res.json( {
            message: "Successfully deleted hello book",
            book: result
          });
        });
      });
      var path = require('path');
      app.get('*', function(req, res) {
        res.sendfile(path.join(__dirname + '/public', 'index.html'));
      });
    };
    ```

3. <span data-ttu-id="43b5a-151">Em Olá *aplicativos* pasta, crie uma pasta chamada *modelos* e adicione um arquivo chamado *book.js* com configuração de modelo de catálogo Olá definida.</span><span class="sxs-lookup"><span data-stu-id="43b5a-151">In hello *apps* folder, create a folder named *models* and add a file named *book.js* with hello book model configuration defined.</span></span>  

    ```node.js
    var mongoose = require('mongoose');
    var dbHost = 'mongodb://localhost:27017/test';
    mongoose.connect(dbHost);
    mongoose.connection;
    mongoose.set('debug', true);
    var bookSchema = mongoose.Schema( {
      name: String,
      isbn: {type: String, index: true},
      author: String,
      pages: Number
    });
    var Book = mongoose.model('Book', bookSchema);
    module.exports = mongoose.model('Book', bookSchema); 
    ```

## <a name="access-hello-routes-with-angularjs"></a><span data-ttu-id="43b5a-152">Rotas de saudação do acesso com AngularJS</span><span class="sxs-lookup"><span data-stu-id="43b5a-152">Access hello routes with AngularJS</span></span>

<span data-ttu-id="43b5a-153">O [AngularJS](https://angularjs.org) fornece uma estrutura da Web para criar exibições dinâmicas em seus aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="43b5a-153">[AngularJS](https://angularjs.org) provides a web framework for creating dynamic views in your web applications.</span></span> <span data-ttu-id="43b5a-154">Neste tutorial, usamos AngularJS tooconnect nossa página da web com o Express e executar ações em nosso banco de dados do catálogo.</span><span class="sxs-lookup"><span data-stu-id="43b5a-154">In this tutorial, we use AngularJS tooconnect our web page with Express and perform actions on our book database.</span></span>

1. <span data-ttu-id="43b5a-155">Altere o diretório de saudação backup muito*manuais* (`cd ../..`) e, em seguida, crie uma pasta chamada *pública* e adicione um arquivo chamado *script. js* com controlador Olá configuração definida.</span><span class="sxs-lookup"><span data-stu-id="43b5a-155">Change hello directory back up too*Books* (`cd ../..`), and then create a folder named *public* and add a file named *script.js* with hello controller configuration defined.</span></span>

    ```node.js
    var app = angular.module('myApp', []);
    app.controller('myCtrl', function($scope, $http) {
      $http( {
        method: 'GET',
        url: '/book'
      }).then(function successCallback(response) {
        $scope.books = response.data;
      }, function errorCallback(response) {
        console.log('Error: ' + response);
      });
      $scope.del_book = function(book) {
        $http( {
          method: 'DELETE',
          url: '/book/:isbn',
          params: {'isbn': book.isbn}
        }).then(function successCallback(response) {
          console.log(response);
        }, function errorCallback(response) {
          console.log('Error: ' + response);
        });
      };
      $scope.add_book = function() {
        var body = '{ "name": "' + $scope.Name + 
        '", "isbn": "' + $scope.Isbn +
        '", "author": "' + $scope.Author + 
        '", "pages": "' + $scope.Pages + '" }';
        $http({
          method: 'POST',
          url: '/book',
          data: body
        }).then(function successCallback(response) {
          console.log(response);
        }, function errorCallback(response) {
          console.log('Error: ' + response);
        });
      };
    });
    ```
    
2. <span data-ttu-id="43b5a-156">Em Olá *pública* pasta, crie um arquivo chamado *index* com a página de web hello definido.</span><span class="sxs-lookup"><span data-stu-id="43b5a-156">In hello *public* folder, create a file named *index.html* with hello web page defined.</span></span>

    ```html
    <!doctype html>
    <html ng-app="myApp" ng-controller="myCtrl">
      <head>
        <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.4/angular.min.js"></script>
        <script src="script.js"></script>
      </head>
      <body>
        <div>
          <table>
            <tr>
              <td>Name:</td> 
              <td><input type="text" ng-model="Name"></td>
            </tr>
            <tr>
              <td>Isbn:</td>
              <td><input type="text" ng-model="Isbn"></td>
            </tr>
            <tr>
              <td>Author:</td> 
              <td><input type="text" ng-model="Author"></td>
            </tr>
            <tr>
              <td>Pages:</td>
              <td><input type="number" ng-model="Pages"></td>
            </tr>
          </table>
          <button ng-click="add_book()">Add</button>
        </div>
        <hr>
        <div>
          <table>
            <tr>
              <th>Name</th>
              <th>Isbn</th>
              <th>Author</th>
              <th>Pages</th>
            </tr>
            <tr ng-repeat="book in books">
              <td><input type="button" value="Delete" data-ng-click="del_book(book)"></td>
              <td>{{book.name}}</td>
              <td>{{book.isbn}}</td>
              <td>{{book.author}}</td>
              <td>{{book.pages}}</td>
            </tr>
          </table>
        </div>
      </body>
    </html>
    ```

##  <a name="run-hello-application"></a><span data-ttu-id="43b5a-157">Executar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="43b5a-157">Run hello application</span></span>

1. <span data-ttu-id="43b5a-158">Altere o diretório de saudação backup muito*manuais* (`cd ..`) e inicie o servidor de saudação executando este comando:</span><span class="sxs-lookup"><span data-stu-id="43b5a-158">Change hello directory back up too*Books* (`cd ..`) and start hello server by running this command:</span></span>

    ```bash
    nodejs server.js
    ```

2. <span data-ttu-id="43b5a-159">Abra um endereço de toohello de navegador da web que você registrou para Olá VM.</span><span class="sxs-lookup"><span data-stu-id="43b5a-159">Open a web browser toohello address that you recorded for hello VM.</span></span> <span data-ttu-id="43b5a-160">Por exemplo, *http://13.72.77.9:3300*.</span><span class="sxs-lookup"><span data-stu-id="43b5a-160">For example, *http://13.72.77.9:3300*.</span></span> <span data-ttu-id="43b5a-161">Você verá algo parecido com hello página a seguir:</span><span class="sxs-lookup"><span data-stu-id="43b5a-161">You should see something like hello following page:</span></span>

    ![Registro de livro](media/tutorial-mean/meanstack-init.png)

3. <span data-ttu-id="43b5a-163">Inserir dados nas caixas de texto de saudação e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="43b5a-163">Enter data into hello textboxes and click **Add**.</span></span> <span data-ttu-id="43b5a-164">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="43b5a-164">For example:</span></span>

    ![Adicionar registro de livro](media/tutorial-mean/meanstack-add.png)

4. <span data-ttu-id="43b5a-166">Depois de atualizar a página hello, você verá algo parecido com esta página:</span><span class="sxs-lookup"><span data-stu-id="43b5a-166">After refreshing hello page, you should see something like this page:</span></span>

    ![Listar registros de livro](media/tutorial-mean/meanstack-list.png)

5. <span data-ttu-id="43b5a-168">Você pode clicar em **excluir** e remover o registro de catálogo de saudação do banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="43b5a-168">You could click **Delete** and remove hello book record from hello database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="43b5a-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="43b5a-169">Next steps</span></span>

<span data-ttu-id="43b5a-170">Neste tutorial, você criou um aplicativo Web que controla registros de livros usando uma pilha MEAN em uma VM do Linux.</span><span class="sxs-lookup"><span data-stu-id="43b5a-170">In this tutorial, you created a web application that keeps track of book records using a MEAN stack on a Linux VM.</span></span> <span data-ttu-id="43b5a-171">Você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="43b5a-171">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="43b5a-172">Criar uma VM do Linux</span><span class="sxs-lookup"><span data-stu-id="43b5a-172">Create a Linux VM</span></span>
> * <span data-ttu-id="43b5a-173">Instalar o Node. js</span><span class="sxs-lookup"><span data-stu-id="43b5a-173">Install Node.js</span></span>
> * <span data-ttu-id="43b5a-174">Instalar o MongoDB e configurar o servidor de saudação</span><span class="sxs-lookup"><span data-stu-id="43b5a-174">Install MongoDB and set up hello server</span></span>
> * <span data-ttu-id="43b5a-175">Express de instalar e configurar o servidor de toohello de rotas</span><span class="sxs-lookup"><span data-stu-id="43b5a-175">Install Express and set up routes toohello server</span></span>
> * <span data-ttu-id="43b5a-176">Rotas de saudação do acesso com AngularJS</span><span class="sxs-lookup"><span data-stu-id="43b5a-176">Access hello routes with AngularJS</span></span>
> * <span data-ttu-id="43b5a-177">Executar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="43b5a-177">Run hello application</span></span>

<span data-ttu-id="43b5a-178">Avançar toohello toolearn de tutorial Avançar como servidores de web toosecure com certificados SSL.</span><span class="sxs-lookup"><span data-stu-id="43b5a-178">Advance toohello next tutorial toolearn how toosecure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="43b5a-179">Proteger servidor Web com SSL</span><span class="sxs-lookup"><span data-stu-id="43b5a-179">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)
