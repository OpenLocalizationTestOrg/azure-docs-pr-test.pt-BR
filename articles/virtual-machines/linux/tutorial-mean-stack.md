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
# <a name="create-a-mongodb-express-angularjs-and-nodejs-mean-stack-on-a-linux-vm-in-azure"></a>Criar uma pilha MongoDB, Expresso, AngularJS e Node.js (MEAN) em uma VM do Linux no Azure

Este tutorial mostra como o Node. js (média), Express, AngularJS e tooimplement um MongoDB pilha em uma VM do Linux no Azure. pilha de média de saudação que você cria permite adicionar, excluir e listar manuais em um banco de dados. Você aprenderá como:

> [!div class="checklist"]
> * Criar uma VM do Linux
> * Instalar o Node. js
> * Instalar o MongoDB e configurar o servidor de saudação
> * Express de instalar e configurar o servidor de toohello de rotas
> * Rotas de saudação do acesso com AngularJS
> * Executar o aplicativo hello

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este tutorial requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).


## <a name="create-a-linux-vm"></a>Criar uma VM do Linux

Criar um grupo de recursos com hello [criar grupo az](https://docs.microsoft.com/cli/azure/group#create) de comando e criar uma VM do Linux com hello [criar vm az](https://docs.microsoft.com/cli/azure/vm#create) comando. Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.

Olá, exemplo a seguir usa Olá CLI do Azure toocreate um grupo de recursos denominado *myResourceGroupMEAN* em Olá *eastus* local. Uma VM é criada com o nome *myVM* com chaves SSH, caso elas ainda não existam em um local de chave padrão. toouse um conjunto específico de chaves, use hello – opção ssh-chave-valor.

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

Quando Olá VM tiver sido criado, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir: 

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
Anote Olá `publicIpAddress`. Esse endereço é usado tooaccess Olá VM.

A seguir Olá Use o comando toocreate uma sessão SSH com hello VM. Certifique-se de toouse Olá endereço IP público correto. Em nosso exemplo acima, o endereço IP era 13.72.77.9.

```bash
ssh azureuser@13.72.77.9
```

## <a name="install-nodejs"></a>Instalar o Node. js

O [Node.js](https://nodejs.org/en/) é um tempo de execução de JavaScript baseado no mecanismo de JavaScript V8 do Chrome. Node. js é usado neste tutorial tooset Olá que roteia Express e controladores AngularJS.

Em Olá VM, usando o shell bash Olá que você abriu com SSH, instale o Node. js.

```bash
sudo apt-get install -y nodejs
```

## <a name="install-mongodb-and-set-up-hello-server"></a>Instalar o MongoDB e configurar o servidor de saudação
O [MongoDB](http://www.mongodb.com) armazena dados em documentos flexíveis, como JSON. Campos em um banco de dados podem variar de documento toodocument e estrutura de dados pode ser alterada ao longo do tempo. Em nosso aplicativo de exemplo, estamos adicionando tooMongoDB de registros de catálogo que contêm o nome do catálogo, o número isbn, autor e número de páginas. 

1. No hello VM, usando o shell bash Olá que você abriu com SSH, defina a chave do MongoDB de saudação.

    ```bash
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
    echo "deb [ arch=amd64 ] http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
    ```

2. Atualize Gerenciador de pacotes de saudação com chave hello.
  
    ```bash
    sudo apt-get update
    ```

3. Instale o MongoDB.

    ```bash
    sudo apt-get install -y mongodb
    ```

4. Servidor de saudação inicial.

    ```bash
    sudo service mongodb start
    ```

5. Também precisamos Olá tooinstall [corpo analisador](https://www.npmjs.com/package/body-parser-json) toohelp de pacote nos processar Olá JSON transmitido no servidor de toohello de solicitações.

    Instale o Gerenciador de pacote de npm hello.

    ```bash
    sudo apt-get install npm
    ```

    Instale o pacote de analisador de corpo de saudação.
    
    ```bash
    sudo npm install body-parser
    ```

6. Crie uma pasta chamada *manuais* e adicione um tooit arquivo denominado *server.js* que contém a configuração de saudação para Olá web server.

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

## <a name="install-express-and-set-up-routes-toohello-server"></a>Express de instalar e configurar o servidor de toohello de rotas

O [Expresso](https://expressjs.com) é uma estrutura de aplicativo Web mínima e flexível de Node.js que fornece recursos para aplicativos Web e móveis. Express é usado em tooand de informações de catálogo este tutorial toopass de nosso banco de dados do MongoDB. [Mongoose](http://mongoosejs.com) fornece uma solução baseada em esquema direta toomodel os dados do aplicativo. Mongoose é usado neste tutorial tooprovide um esquema de catálogo para o banco de dados de saudação.

1. Instale o Expresso e o Mongoose.

    ```bash
    sudo npm install express mongoose
    ```

2. Em Olá *manuais* pasta, crie uma pasta chamada *aplicativos* e adicione um arquivo chamado *routes.js* com hello express rotas definidas.

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

3. Em Olá *aplicativos* pasta, crie uma pasta chamada *modelos* e adicione um arquivo chamado *book.js* com configuração de modelo de catálogo Olá definida.  

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

## <a name="access-hello-routes-with-angularjs"></a>Rotas de saudação do acesso com AngularJS

O [AngularJS](https://angularjs.org) fornece uma estrutura da Web para criar exibições dinâmicas em seus aplicativos Web. Neste tutorial, usamos AngularJS tooconnect nossa página da web com o Express e executar ações em nosso banco de dados do catálogo.

1. Altere o diretório de saudação backup muito*manuais* (`cd ../..`) e, em seguida, crie uma pasta chamada *pública* e adicione um arquivo chamado *script. js* com controlador Olá configuração definida.

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
    
2. Em Olá *pública* pasta, crie um arquivo chamado *index* com a página de web hello definido.

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

##  <a name="run-hello-application"></a>Executar o aplicativo hello

1. Altere o diretório de saudação backup muito*manuais* (`cd ..`) e inicie o servidor de saudação executando este comando:

    ```bash
    nodejs server.js
    ```

2. Abra um endereço de toohello de navegador da web que você registrou para Olá VM. Por exemplo, *http://13.72.77.9:3300*. Você verá algo parecido com hello página a seguir:

    ![Registro de livro](media/tutorial-mean/meanstack-init.png)

3. Inserir dados nas caixas de texto de saudação e clique em **adicionar**. Por exemplo:

    ![Adicionar registro de livro](media/tutorial-mean/meanstack-add.png)

4. Depois de atualizar a página hello, você verá algo parecido com esta página:

    ![Listar registros de livro](media/tutorial-mean/meanstack-list.png)

5. Você pode clicar em **excluir** e remover o registro de catálogo de saudação do banco de dados de saudação.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você criou um aplicativo Web que controla registros de livros usando uma pilha MEAN em uma VM do Linux. Você aprendeu como:

> [!div class="checklist"]
> * Criar uma VM do Linux
> * Instalar o Node. js
> * Instalar o MongoDB e configurar o servidor de saudação
> * Express de instalar e configurar o servidor de toohello de rotas
> * Rotas de saudação do acesso com AngularJS
> * Executar o aplicativo hello

Avançar toohello toolearn de tutorial Avançar como servidores de web toosecure com certificados SSL.

> [!div class="nextstepaction"]
> [Proteger servidor Web com SSL](tutorial-secure-web-server.md)
