---
title: Criar uma pilha MEAN em uma VM do Linux no Azure | Microsoft Docs
description: Saiba como criar uma pilha MongoDB, Expresso, AngularJS e Node.js (MEAN) em uma VM do Linux no Azure.
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
ms.openlocfilehash: 892d3481b4ec70fb8434cb25013c5cfd8ab85051
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-mongodb-express-angularjs-and-nodejs-mean-stack-on-a-linux-vm-in-azure"></a><span data-ttu-id="1fbba-103">Criar uma pilha MongoDB, Expresso, AngularJS e Node.js (MEAN) em uma VM do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="1fbba-103">Create a MongoDB, Express, AngularJS, and Node.js (MEAN) stack on a Linux VM in Azure</span></span>

<span data-ttu-id="1fbba-104">Este tutorial mostra como implementar uma pilha MongoDB, Expresso, AngularJS e Node.js (MEAN) em uma VM do Linux no Azure.</span><span class="sxs-lookup"><span data-stu-id="1fbba-104">This tutorial shows you how to implement a MongoDB, Express, AngularJS, and Node.js (MEAN) stack on a Linux VM in Azure.</span></span> <span data-ttu-id="1fbba-105">A pilha MEAN que será criada permite adição, exclusão e listagem de livros em um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="1fbba-105">The MEAN stack that you create enables adding, deleting, and listing books in a database.</span></span> <span data-ttu-id="1fbba-106">Você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="1fbba-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1fbba-107">Criar uma VM do Linux</span><span class="sxs-lookup"><span data-stu-id="1fbba-107">Create a Linux VM</span></span>
> * <span data-ttu-id="1fbba-108">Instalar o Node. js</span><span class="sxs-lookup"><span data-stu-id="1fbba-108">Install Node.js</span></span>
> * <span data-ttu-id="1fbba-109">Instalar o MongoDB e configurar o servidor</span><span class="sxs-lookup"><span data-stu-id="1fbba-109">Install MongoDB and set up the server</span></span>
> * <span data-ttu-id="1fbba-110">Instalar rotas do Expresso e de configuração para o servidor</span><span class="sxs-lookup"><span data-stu-id="1fbba-110">Install Express and set up routes to the server</span></span>
> * <span data-ttu-id="1fbba-111">Acessar as rotas com AngularJS</span><span class="sxs-lookup"><span data-stu-id="1fbba-111">Access the routes with AngularJS</span></span>
> * <span data-ttu-id="1fbba-112">Executar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="1fbba-112">Run the application</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="1fbba-113">Se você optar por instalar e usar a CLI localmente, este tutorial exigirá que você execute a CLI do Azure versão 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="1fbba-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="1fbba-114">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="1fbba-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="1fbba-115">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="1fbba-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>


## <a name="create-a-linux-vm"></a><span data-ttu-id="1fbba-116">Criar uma VM do Linux</span><span class="sxs-lookup"><span data-stu-id="1fbba-116">Create a Linux VM</span></span>

<span data-ttu-id="1fbba-117">Criar um grupo de recursos com o comando [az group create](https://docs.microsoft.com/cli/azure/group#create) e criar uma VM do Linux com o comando [az vm create](https://docs.microsoft.com/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="1fbba-117">Create a resource group with the [az group create](https://docs.microsoft.com/cli/azure/group#create) command and create a Linux VM with the [az vm create](https://docs.microsoft.com/cli/azure/vm#create) command.</span></span> <span data-ttu-id="1fbba-118">Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="1fbba-118">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="1fbba-119">O exemplo a seguir usa a CLI do Azure para criar um grupo de recursos chamado *myResourceGroupMEAN* no local *eastus*.</span><span class="sxs-lookup"><span data-stu-id="1fbba-119">The following example uses the Azure CLI to create a resource group named *myResourceGroupMEAN* in the *eastus* location.</span></span> <span data-ttu-id="1fbba-120">Uma VM é criada com o nome *myVM* com chaves SSH, caso elas ainda não existam em um local de chave padrão.</span><span class="sxs-lookup"><span data-stu-id="1fbba-120">A VM is created named *myVM* with SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="1fbba-121">Para usar um conjunto específico de chaves, use a opção --ssh-key-value.</span><span class="sxs-lookup"><span data-stu-id="1fbba-121">To use a specific set of keys, use the --ssh-key-value option.</span></span>

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

<span data-ttu-id="1fbba-122">Quando a VM tiver sido criada, a CLI do Azure mostrará informações semelhantes ao exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="1fbba-122">When the VM has been created, the Azure CLI shows information similar to the following example:</span></span> 

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
<span data-ttu-id="1fbba-123">Anote `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="1fbba-123">Take note of the `publicIpAddress`.</span></span> <span data-ttu-id="1fbba-124">Esse endereço é usado para acessar a VM.</span><span class="sxs-lookup"><span data-stu-id="1fbba-124">This address is used to access the VM.</span></span>

<span data-ttu-id="1fbba-125">Use o comando a seguir para criar uma sessão SSH com a VM.</span><span class="sxs-lookup"><span data-stu-id="1fbba-125">Use the following command to create an SSH session with the VM.</span></span> <span data-ttu-id="1fbba-126">Certifique-se de usar o endereço IP público correto.</span><span class="sxs-lookup"><span data-stu-id="1fbba-126">Make sure to use the correct public IP address.</span></span> <span data-ttu-id="1fbba-127">Em nosso exemplo acima, o endereço IP era 13.72.77.9.</span><span class="sxs-lookup"><span data-stu-id="1fbba-127">In our example above our IP address was 13.72.77.9.</span></span>

```bash
ssh azureuser@13.72.77.9
```

## <a name="install-nodejs"></a><span data-ttu-id="1fbba-128">Instalar o Node. js</span><span class="sxs-lookup"><span data-stu-id="1fbba-128">Install Node.js</span></span>

<span data-ttu-id="1fbba-129">O [Node.js](https://nodejs.org/en/) é um tempo de execução de JavaScript baseado no mecanismo de JavaScript V8 do Chrome.</span><span class="sxs-lookup"><span data-stu-id="1fbba-129">[Node.js](https://nodejs.org/en/) is a JavaScript runtime built on Chrome's V8 JavaScript engine.</span></span> <span data-ttu-id="1fbba-130">O Node.js é usado neste tutorial para configurar as rotas do Expresso e os controladores AngularJS.</span><span class="sxs-lookup"><span data-stu-id="1fbba-130">Node.js is used in this tutorial to set up the Express routes and AngularJS controllers.</span></span>

<span data-ttu-id="1fbba-131">Na VM, usando o shell bash que você abriu com SSH, instale o Node.js.</span><span class="sxs-lookup"><span data-stu-id="1fbba-131">On the VM, using the bash shell that you opened with SSH, install Node.js.</span></span>

```bash
sudo apt-get install -y nodejs
```

## <a name="install-mongodb-and-set-up-the-server"></a><span data-ttu-id="1fbba-132">Instalar o MongoDB e configurar o servidor</span><span class="sxs-lookup"><span data-stu-id="1fbba-132">Install MongoDB and set up the server</span></span>
<span data-ttu-id="1fbba-133">O [MongoDB](http://www.mongodb.com) armazena dados em documentos flexíveis, como JSON.</span><span class="sxs-lookup"><span data-stu-id="1fbba-133">[MongoDB](http://www.mongodb.com) stores data in flexible, JSON-like documents.</span></span> <span data-ttu-id="1fbba-134">Os campos em um banco de dados podem variar de um documento para outro e a estrutura de dados pode ser alterada ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="1fbba-134">Fields in a database can vary from document to document and data structure can be changed over time.</span></span> <span data-ttu-id="1fbba-135">Em nosso aplicativo de exemplo, estamos adicionando registros de livros no MongoDB que contêm o nome do livro, o número ISBN, o autor e o número de páginas.</span><span class="sxs-lookup"><span data-stu-id="1fbba-135">For our example application, we are adding book records to MongoDB that contain book name, isbn number, author, and number of pages.</span></span> 

1. <span data-ttu-id="1fbba-136">Na VM, usando o shell bash que você abriu com SSH, defina a chave do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="1fbba-136">On the VM, using the bash shell that you opened with SSH, set the MongoDB key.</span></span>

    ```bash
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
    echo "deb [ arch=amd64 ] http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
    ```

2. <span data-ttu-id="1fbba-137">Atualize o gerenciador de pacotes com a chave.</span><span class="sxs-lookup"><span data-stu-id="1fbba-137">Update the package manager with the key.</span></span>
  
    ```bash
    sudo apt-get update
    ```

3. <span data-ttu-id="1fbba-138">Instale o MongoDB.</span><span class="sxs-lookup"><span data-stu-id="1fbba-138">Install MongoDB.</span></span>

    ```bash
    sudo apt-get install -y mongodb
    ```

4. <span data-ttu-id="1fbba-139">Inicie o servidor.</span><span class="sxs-lookup"><span data-stu-id="1fbba-139">Start the server.</span></span>

    ```bash
    sudo service mongodb start
    ```

5. <span data-ttu-id="1fbba-140">Também precisamos instalar o pacote [body-parser](https://www.npmjs.com/package/body-parser-json) para nos ajudar a processar o JSON passado nas solicitações ao servidor.</span><span class="sxs-lookup"><span data-stu-id="1fbba-140">We also need to install the [body-parser](https://www.npmjs.com/package/body-parser-json) package to help us process the JSON passed in requests to the server.</span></span>

    <span data-ttu-id="1fbba-141">Instale o gerenciador de pacotes npm.</span><span class="sxs-lookup"><span data-stu-id="1fbba-141">Install the npm package manager.</span></span>

    ```bash
    sudo apt-get install npm
    ```

    <span data-ttu-id="1fbba-142">Instale o pacote body-parser.</span><span class="sxs-lookup"><span data-stu-id="1fbba-142">Install the body parser package.</span></span>
    
    ```bash
    sudo npm install body-parser
    ```

6. <span data-ttu-id="1fbba-143">Crie uma pasta chamada *Livros* e adicione nela um arquivo chamado *server.js*, que contém a configuração do servidor Web.</span><span class="sxs-lookup"><span data-stu-id="1fbba-143">Create a folder named *Books* and add a file to it named *server.js* that contains the configuration for the web server.</span></span>

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

## <a name="install-express-and-set-up-routes-to-the-server"></a><span data-ttu-id="1fbba-144">Instalar rotas do Expresso e de configuração para o servidor</span><span class="sxs-lookup"><span data-stu-id="1fbba-144">Install Express and set up routes to the server</span></span>

<span data-ttu-id="1fbba-145">O [Expresso](https://expressjs.com) é uma estrutura de aplicativo Web mínima e flexível de Node.js que fornece recursos para aplicativos Web e móveis.</span><span class="sxs-lookup"><span data-stu-id="1fbba-145">[Express](https://expressjs.com) is a minimal and flexible Node.js web application framework that provides features for web and mobile applications.</span></span> <span data-ttu-id="1fbba-146">O Expresso é usado neste tutorial para passar informações de livro para e do nosso banco de dados do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="1fbba-146">Express is used in this tutorial to pass book information to and from our MongoDB database.</span></span> <span data-ttu-id="1fbba-147">[Mongoose](http://mongoosejs.com) fornece uma solução simples, com base em esquema para modelar seus dados de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1fbba-147">[Mongoose](http://mongoosejs.com) provides a straight-forward, schema-based solution to model your application data.</span></span> <span data-ttu-id="1fbba-148">O Mongoose é usado neste tutorial para fornecer um esquema de livro para o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="1fbba-148">Mongoose is used in this tutorial to provide a book schema for the database.</span></span>

1. <span data-ttu-id="1fbba-149">Instale o Expresso e o Mongoose.</span><span class="sxs-lookup"><span data-stu-id="1fbba-149">Install Express and Mongoose.</span></span>

    ```bash
    sudo npm install express mongoose
    ```

2. <span data-ttu-id="1fbba-150">Na pasta *Livros*, crie uma pasta chamada *aplicativos* e adicione um arquivo chamado *routes.js* com as rotas expressas definidas.</span><span class="sxs-lookup"><span data-stu-id="1fbba-150">In the *Books* folder, create a folder named *apps* and add a file named *routes.js* with the express routes defined.</span></span>

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
            message: "Successfully deleted the book",
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

3. <span data-ttu-id="1fbba-151">Na pasta *aplicativos*, crie uma pasta chamada *modelos* e adicione um arquivo chamado *book.js* com a configuração de modelo de livro definida.</span><span class="sxs-lookup"><span data-stu-id="1fbba-151">In the *apps* folder, create a folder named *models* and add a file named *book.js* with the book model configuration defined.</span></span>  

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

## <a name="access-the-routes-with-angularjs"></a><span data-ttu-id="1fbba-152">Acessar as rotas com AngularJS</span><span class="sxs-lookup"><span data-stu-id="1fbba-152">Access the routes with AngularJS</span></span>

<span data-ttu-id="1fbba-153">O [AngularJS](https://angularjs.org) fornece uma estrutura da Web para criar exibições dinâmicas em seus aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="1fbba-153">[AngularJS](https://angularjs.org) provides a web framework for creating dynamic views in your web applications.</span></span> <span data-ttu-id="1fbba-154">Neste tutorial, usamos o AngularJS para conectar a nossa página da Web com o Expresso e realizar ações em nosso banco de dados de livro.</span><span class="sxs-lookup"><span data-stu-id="1fbba-154">In this tutorial, we use AngularJS to connect our web page with Express and perform actions on our book database.</span></span>

1. <span data-ttu-id="1fbba-155">Altere o diretório de backup para *Livros* (`cd ../..`) e, em seguida, crie uma pasta chamada *pública* e adicione um arquivo chamado *script.js* com a configuração do controlador definida.</span><span class="sxs-lookup"><span data-stu-id="1fbba-155">Change the directory back up to *Books* (`cd ../..`), and then create a folder named *public* and add a file named *script.js* with the controller configuration defined.</span></span>

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
    
2. <span data-ttu-id="1fbba-156">Na pasta *pública*, crie um arquivo chamado *index.html* com a página da Web definida.</span><span class="sxs-lookup"><span data-stu-id="1fbba-156">In the *public* folder, create a file named *index.html* with the web page defined.</span></span>

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

##  <a name="run-the-application"></a><span data-ttu-id="1fbba-157">Executar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="1fbba-157">Run the application</span></span>

1. <span data-ttu-id="1fbba-158">Altere o diretório de backup para *Livros* (`cd ..`) e inicie o servidor executando este comando:</span><span class="sxs-lookup"><span data-stu-id="1fbba-158">Change the directory back up to *Books* (`cd ..`) and start the server by running this command:</span></span>

    ```bash
    nodejs server.js
    ```

2. <span data-ttu-id="1fbba-159">Abra um navegador da Web no endereço que você registrou para a VM.</span><span class="sxs-lookup"><span data-stu-id="1fbba-159">Open a web browser to the address that you recorded for the VM.</span></span> <span data-ttu-id="1fbba-160">Por exemplo, *http://13.72.77.9:3300*.</span><span class="sxs-lookup"><span data-stu-id="1fbba-160">For example, *http://13.72.77.9:3300*.</span></span> <span data-ttu-id="1fbba-161">Você verá algo semelhante à página a seguir:</span><span class="sxs-lookup"><span data-stu-id="1fbba-161">You should see something like the following page:</span></span>

    ![Registro de livro](media/tutorial-mean/meanstack-init.png)

3. <span data-ttu-id="1fbba-163">Insira dados nas caixas de texto e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1fbba-163">Enter data into the textboxes and click **Add**.</span></span> <span data-ttu-id="1fbba-164">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="1fbba-164">For example:</span></span>

    ![Adicionar registro de livro](media/tutorial-mean/meanstack-add.png)

4. <span data-ttu-id="1fbba-166">Depois de atualizar a página, você verá algo parecido com esta página:</span><span class="sxs-lookup"><span data-stu-id="1fbba-166">After refreshing the page, you should see something like this page:</span></span>

    ![Listar registros de livro](media/tutorial-mean/meanstack-list.png)

5. <span data-ttu-id="1fbba-168">Você pode clicar em **Excluir** e remover o registro de livro do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="1fbba-168">You could click **Delete** and remove the book record from the database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1fbba-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1fbba-169">Next steps</span></span>

<span data-ttu-id="1fbba-170">Neste tutorial, você criou um aplicativo Web que controla registros de livros usando uma pilha MEAN em uma VM do Linux.</span><span class="sxs-lookup"><span data-stu-id="1fbba-170">In this tutorial, you created a web application that keeps track of book records using a MEAN stack on a Linux VM.</span></span> <span data-ttu-id="1fbba-171">Você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="1fbba-171">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1fbba-172">Criar uma VM do Linux</span><span class="sxs-lookup"><span data-stu-id="1fbba-172">Create a Linux VM</span></span>
> * <span data-ttu-id="1fbba-173">Instalar o Node. js</span><span class="sxs-lookup"><span data-stu-id="1fbba-173">Install Node.js</span></span>
> * <span data-ttu-id="1fbba-174">Instalar o MongoDB e configurar o servidor</span><span class="sxs-lookup"><span data-stu-id="1fbba-174">Install MongoDB and set up the server</span></span>
> * <span data-ttu-id="1fbba-175">Instalar rotas do Expresso e de configuração para o servidor</span><span class="sxs-lookup"><span data-stu-id="1fbba-175">Install Express and set up routes to the server</span></span>
> * <span data-ttu-id="1fbba-176">Acessar as rotas com AngularJS</span><span class="sxs-lookup"><span data-stu-id="1fbba-176">Access the routes with AngularJS</span></span>
> * <span data-ttu-id="1fbba-177">Executar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="1fbba-177">Run the application</span></span>

<span data-ttu-id="1fbba-178">Vá para o próximo tutorial para saber como proteger servidores Web com certificados SSL.</span><span class="sxs-lookup"><span data-stu-id="1fbba-178">Advance to the next tutorial to learn how to secure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1fbba-179">Proteger servidor Web com SSL</span><span class="sxs-lookup"><span data-stu-id="1fbba-179">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)
