---
title: aaaGet iniciado com hello Azure CDN SDK para Node.js | Microsoft Docs
description: Saiba como toowrite Node. js aplicativos toomanage CDN do Azure.
services: cdn
documentationcenter: nodejs
author: zhangmanling
manager: erikre
editor: 
ms.assetid: c4bb6a61-de3d-4f0c-9dca-202554c43dfa
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 6c805e5fb8e0b471e8b248cb2f4b29efd6c85940
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cdn-development"></a>Introdução ao desenvolvimento de CDN do Azure
> [!div class="op_single_selector"]
> * [Node.js](cdn-app-dev-node.md)
> * [.NET](cdn-app-dev-net.md)
> 
> 

Você pode usar o hello [Azure CDN SDK para Node.js](https://www.npmjs.com/package/azure-arm-cdn) tooautomate criação e gerenciamento de perfis CDN e os pontos de extremidade.  Este tutorial orienta a criação de um aplicativo de console simples Node. js que demonstra várias operações disponíveis Olá Olá.  Este tutorial destina-se não se destina toodescribe todos os aspectos de saudação do SDK do Azure CDN Node. js em detalhes.

toocomplete neste tutorial, você já deve ter [Node.js](http://www.nodejs.org) **4** ou superior instalado e configurado.  Você pode usar qualquer editor de texto que você deseja toocreate seu aplicativo Node. js.  toowrite neste tutorial, usei [código do Visual Studio](https://code.visualstudio.com).  

> [!TIP]
> Olá [projeto concluído deste tutorial](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) está disponível para download no MSDN.
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-npm-dependencies"></a>Criar o projeto e adicionar dependências de NPM
Agora que podemos criar um grupo de recursos para os perfis CDN e considerando nossa perfis de CDN do Azure AD aplicativos permissão toomanage e pontos de extremidade dentro desse grupo, podemos começar criando o nosso aplicativo.

Crie uma pasta toostore seu aplicativo.  Em um console com as ferramentas de Node. js Olá no caminho atual, definir a nova pasta de toothis seu local atual e inicializar o projeto por meio da execução:

    npm init

Em seguida, será apresentada uma série de perguntas tooinitialize seu projeto.  Para o **ponto de entrada**, este tutorial usa *app.js*.  Você pode ver meu outras opções Olá exemplo a seguir.

![Saída de NPM init](./media/cdn-app-dev-node/cdn-npm-init.png)

Agora, o projeto é inicializado com um arquivo *packages.json* .  Nosso projeto vai toouse algumas bibliotecas do Azure contidas em pacotes do NPM.  Vamos usar Olá tempo de execução do cliente do Azure para Node.js (ms-rest-azure) e hello biblioteca de cliente do Azure CDN para Node.js (azure-arm cd).  Vamos adicionar esses projeto toohello como dependências.

    npm install --save ms-rest-azure
    npm install --save azure-arm-cdn

Depois de terminar de pacotes de saudação instalando, hello *Package. JSON* arquivo deve parecer semelhante toothis exemplo (versão números podem ser diferentes):

``` json
{
  "name": "cdn_node",
  "version": "1.0.0",
  "description": "Azure CDN Node.js tutorial project",
  "main": "app.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "Cam Soper",
  "license": "MIT",
  "dependencies": {
    "azure-arm-cdn": "^0.2.1",
    "ms-rest-azure": "^1.14.4"
  }
}
```

Finalmente, usando seu editor de texto, crie um arquivo de texto em branco e salvá-lo na raiz de saudação da nossa pasta de projeto como *app.js*.  Agora estamos pronto toobegin escrever código.

## <a name="requires-constants-authentication-and-structure"></a>Requisitos, constantes, autenticação e estrutura
Com *app.js* abra no nosso editor, vamos estrutura básica de saudação de nosso programa gravado.

1. Adicione hello "requer" para nossos pacotes NPM na parte superior da saudação com os seguintes hello:
   
    ``` javascript
    var msRestAzure = require('ms-rest-azure');
    var cdnManagementClient = require('azure-arm-cdn');
    ```
2. Precisamos toodefine algumas constantes que nossos métodos usará.  Adicione o seguinte de saudação.  Ser tooreplace se espaços reservados hello, incluindo Olá  **&lt;colchetes angulares&gt;**, com seus próprios valores conforme necessário.
   
    ``` javascript
    //Tenant app constants
    const clientId = "<YOUR CLIENT ID>";
    const clientSecret = "<YOUR CLIENT AUTHENTICATION KEY>"; //Only for service principals
    const tenantId = "<YOUR TENANT ID>";
   
    //Application constants
    const subscriptionId = "<YOUR SUBSCRIPTION ID>";
    const resourceGroupName = "CdnConsoleTutorial";
    const resourceLocation = "<YOUR PREFERRED AZURE LOCATION, SUCH AS Central US>";
    ```
3. Em seguida, vamos criar uma instância de cliente de gerenciamento de CDN hello e dê a ele credenciais.
   
    ``` javascript
    var credentials = new msRestAzure.ApplicationTokenCredentials(clientId, tenantId, clientSecret);
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    Se você estiver usando a autenticação de usuário individual, essas duas linhas terão uma aparência ligeiramente diferente.
   
   > [!IMPORTANT]
   > Somente use esse exemplo de código se você está escolhendo toohave autenticação de usuário individual em vez de uma entidade de serviço.  Ser tooguard cuidado suas credenciais de usuário individual e mantê-los segredo.
   > 
   > 
   
    ``` javascript
    var credentials = new msRestAzure.UserTokenCredentials(clientId, 
        tenantId, '<username>', '<password>', '<redirect URI>');
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    Ter tooreplace-se de que os itens de saudação no  **&lt;colchetes angulares&gt;**  com hello informações corretas.  Para `<redirect URI>`, use o redirecionamento de saudação URI que você inseriu quando registrou o aplicativo hello no AD do Azure.
4. Nosso aplicativo de console Node. js será tootake alguns parâmetros de linha de comando.  Validaremos que pelo menos um parâmetro foi passado.
   
   ```javascript
   //Collect command-line parameters
   var parms = process.argv.slice(2);
   
   //Do we have parameters?
   if(parms == null || parms.length == 0)
   {
       console.log("Not enough parameters!");
       console.log("Valid commands are list, delete, create, and purge.");
       process.exit(1);
   }
   ```
5. Chegamos toohello principal parte de nosso programa, onde podemos ramificam tooother funções com base em quais parâmetros foram passados.
   
    ```javascript
    switch(parms[0].toLowerCase())
    {
        case "list":
            cdnList();
            break;
   
        case "create":
            cdnCreate();
            break;
   
        case "delete":
            cdnDelete();
            break;
   
        case "purge":
            cdnPurge();
            break;
   
        default:
            console.log("Valid commands are list, delete, create, and purge.");
            process.exit(1);
    }
    ```
6. Em vários locais em nosso programa, vamos precisar toomake-se de que o número correto de saudação de parâmetros foram passado e exibe ajuda se eles não tiverem corretos.  Vamos criar funções toodo que.
   
   ```javascript
   function requireParms(parmCount) {
       if(parms.length < parmCount) {
           usageHelp(parms[0].toLowerCase());
           process.exit(1);
       }
   }
   
   function usageHelp(cmd) {
       console.log("Usage for " + cmd + ":");
       switch(cmd)
       {
           case "list":
               console.log("list profiles");
               console.log("list endpoints <profile name>");
               break;
   
           case "create":
               console.log("create profile <profile name>");
               console.log("create endpoint <profile name> <endpoint name> <origin hostname>");
               break;
   
           case "delete":
               console.log("delete profile <profile name>");
               console.log("delete endpoint <profile name> <endpoint name>");
               break;
   
           case "purge":
               console.log("purge <profile name> <endpoint name> <path>");
               break;
   
           default:
               console.log("Invalid command.");
       }
   }
   ```
7. Por fim, funções hello que será usado no cliente de gerenciamento de CDN Olá são assíncronas, assim, precisam de um método toocall quando ele terminar.  Vamos fazer um que pode exibir a saída de saudação do cliente de gerenciamento de CDN hello (se houver) e sair de saudação normalmente.
   
    ```javascript
    function callback(err, result, request, response) {
        if (err) {
            console.log(err);
            process.exit(1);
        } else {
            console.log((result == null) ? "Done!" : result);
            process.exit(0);
        }
    }
    ```

Agora que a estrutura básica de saudação do programa é gravada, podemos deve criar funções de saudação chamadas com base em nossos parâmetros.

## <a name="list-cdn-profiles-and-endpoints"></a>Relacione os perfis CDN e os pontos de extremidade
Vamos começar com toolist código nossos perfis existentes e os pontos de extremidade.  Comentários de código fornecem uma sintaxe Olá esperado para sabermos onde vai cada parâmetro.

```javascript
// list profiles
// list endpoints <profile name>
function cdnList(){
    requireParms(2);
    switch(parms[1].toLowerCase())
    {
        case "profiles":
            console.log("Listing profiles...");
            cdnClient.profiles.listByResourceGroup(resourceGroupName, callback);
            break;

        case "endpoints":
            requireParms(3);
            console.log("Listing endpoints...");
            cdnClient.endpoints.listByProfile(parms[2], resourceGroupName, callback);
            break;

        default:
            console.log("Invalid parameter.");
            process.exit(1);
    }
}
```

## <a name="create-cdn-profiles-and-endpoints"></a>Criar perfis CDN e pontos de extremidade
Em seguida, vamos gravar perfis de toocreate funções hello e de pontos de extremidade.

```javascript
function cdnCreate() {
    requireParms(2);
    switch(parms[1].toLowerCase())
    {
        case "profile":
            cdnCreateProfile();
            break;

        case "endpoint":
            cdnCreateEndpoint();
            break;

        default:
            console.log("Invalid parameter.");
            process.exit(1);
    }
}

// create profile <profile name>
function cdnCreateProfile() {
    requireParms(3);
    console.log("Creating profile...");
    var standardCreateParameters = {
        location: resourceLocation,
        sku: {
            name: 'Standard_Verizon'
        }
    };

    cdnClient.profiles.create(parms[2], standardCreateParameters, resourceGroupName, callback);
}

// create endpoint <profile name> <endpoint name> <origin hostname>        
function cdnCreateEndpoint() {
    requireParms(5);
    console.log("Creating endpoint...");
    var endpointProperties = {
        location: resourceLocation,
        origins: [{
            name: parms[4],
            hostName: parms[4]
        }]
    };

    cdnClient.endpoints.create(parms[3], endpointProperties, parms[2], resourceGroupName, callback);
}
```

## <a name="purge-an-endpoint"></a>Limpar um ponto de extremidade
Supondo que o ponto de extremidade de saudação foi criado, uma tarefa comum que que talvez desejemos tooperform em nosso programa está limpando conteúdo no ponto de extremidade.

```javascript
// purge <profile name> <endpoint name> <path>
function cdnPurge() {
    requireParms(4);
    console.log("Purging endpoint...");
    var purgeContentPaths = [ parms[3] ];
    cdnClient.endpoints.purgeContent(parms[2], parms[1], resourceGroupName, purgeContentPaths, callback);
}
```

## <a name="delete-cdn-profiles-and-endpoints"></a>Excluir perfis CDN e pontos de extremidade
função last Hello, que incluiremos exclui perfis e pontos de extremidade.

```javascript
function cdnDelete() {
    requireParms(2);
    switch(parms[1].toLowerCase())
    {
        // delete profile <profile name>
        case "profile":
            requireParms(3);
            console.log("Deleting profile...");
            cdnClient.profiles.deleteIfExists(parms[2], resourceGroupName, callback);
            break;

        // delete endpoint <profile name> <endpoint name>
        case "endpoint":
            requireParms(4);
            console.log("Deleting endpoint...");
            cdnClient.endpoints.deleteIfExists(parms[3], parms[2], resourceGroupName, callback);
            break;

        default:
            console.log("Invalid parameter.");
            process.exit(1);
    }
}
```

## <a name="running-hello-program"></a>Programa de saudação em execução
Agora podemos executar nosso programa Node. js usando nosso depurador favorito ou no console de saudação.

> [!TIP]
> Se você estiver usando o código do Visual Studio como o depurador, você precisará tooset backup toopass seu ambiente nos parâmetros de linha de comando hello.  Código do Visual Studio faz isso de saudação **lanuch.json** arquivo.  Procure uma propriedade chamada **args** e adicione uma matriz de valores de cadeia de caracteres para seus parâmetros, para que ele se parece semelhante toothis: `"args": ["list", "profiles"]`.
> 
> 

Vamos começar listando os perfis.

![Listar perfis](./media/cdn-app-dev-node/cdn-list-profiles.png)

Obtivemos uma matriz vazia.  Como não há perfis no grupo de recursos, isso é esperado.  Vamos criar um perfil agora.

![Criar perfil](./media/cdn-app-dev-node/cdn-create-profile.png)

Agora, vamos adicionar um ponto de extremidade.

![Criar ponto de extremidade](./media/cdn-app-dev-node/cdn-create-endpoint.png)

Por fim, vamos excluir o perfil.

![Excluir perfil](./media/cdn-app-dev-node/cdn-delete-profile.png)

## <a name="next-steps"></a>Próximas etapas
projeto de saudação concluída toosee deste passo a passo, [baixar exemplo hello](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).

referência de saudação toosee para hello Azure CDN SDK para Node.js, Olá de exibição [referência](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).

toofind obter documentação adicional sobre hello Azure SDK para Node.js, Olá exibição [completo referência](http://azure.github.io/azure-sdk-for-node/).

Gerencie seus recursos CDN com o [PowerShell](cdn-manage-powershell.md).

