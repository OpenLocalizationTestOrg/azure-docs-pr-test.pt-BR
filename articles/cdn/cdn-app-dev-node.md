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
# <a name="get-started-with-azure-cdn-development"></a><span data-ttu-id="6074b-103">Introdução ao desenvolvimento de CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="6074b-103">Get started with Azure CDN development</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6074b-104">Node.js</span><span class="sxs-lookup"><span data-stu-id="6074b-104">Node.js</span></span>](cdn-app-dev-node.md)
> * [<span data-ttu-id="6074b-105">.NET</span><span class="sxs-lookup"><span data-stu-id="6074b-105">.NET</span></span>](cdn-app-dev-net.md)
> 
> 

<span data-ttu-id="6074b-106">Você pode usar o hello [Azure CDN SDK para Node.js](https://www.npmjs.com/package/azure-arm-cdn) tooautomate criação e gerenciamento de perfis CDN e os pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="6074b-106">You can use hello [Azure CDN SDK for Node.js](https://www.npmjs.com/package/azure-arm-cdn) tooautomate creation and management of CDN profiles and endpoints.</span></span>  <span data-ttu-id="6074b-107">Este tutorial orienta a criação de um aplicativo de console simples Node. js que demonstra várias operações disponíveis Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="6074b-107">This tutorial walks through hello creation of a simple Node.js console application that demonstrates several of hello available operations.</span></span>  <span data-ttu-id="6074b-108">Este tutorial destina-se não se destina toodescribe todos os aspectos de saudação do SDK do Azure CDN Node. js em detalhes.</span><span class="sxs-lookup"><span data-stu-id="6074b-108">This tutorial is not intended toodescribe all aspects of hello Azure CDN SDK for Node.js in detail.</span></span>

<span data-ttu-id="6074b-109">toocomplete neste tutorial, você já deve ter [Node.js](http://www.nodejs.org) **4** ou superior instalado e configurado.</span><span class="sxs-lookup"><span data-stu-id="6074b-109">toocomplete this tutorial, you should already have [Node.js](http://www.nodejs.org) **4.x.x** or higher installed and configured.</span></span>  <span data-ttu-id="6074b-110">Você pode usar qualquer editor de texto que você deseja toocreate seu aplicativo Node. js.</span><span class="sxs-lookup"><span data-stu-id="6074b-110">You can use any text editor you want toocreate your Node.js application.</span></span>  <span data-ttu-id="6074b-111">toowrite neste tutorial, usei [código do Visual Studio](https://code.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="6074b-111">toowrite this tutorial, I used [Visual Studio Code](https://code.visualstudio.com).</span></span>  

> [!TIP]
> <span data-ttu-id="6074b-112">Olá [projeto concluído deste tutorial](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) está disponível para download no MSDN.</span><span class="sxs-lookup"><span data-stu-id="6074b-112">hello [completed project from this tutorial](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) is available for download on MSDN.</span></span>
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-npm-dependencies"></a><span data-ttu-id="6074b-113">Criar o projeto e adicionar dependências de NPM</span><span class="sxs-lookup"><span data-stu-id="6074b-113">Create your project and add NPM dependencies</span></span>
<span data-ttu-id="6074b-114">Agora que podemos criar um grupo de recursos para os perfis CDN e considerando nossa perfis de CDN do Azure AD aplicativos permissão toomanage e pontos de extremidade dentro desse grupo, podemos começar criando o nosso aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6074b-114">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission toomanage CDN profiles and endpoints within that group, we can start creating our application.</span></span>

<span data-ttu-id="6074b-115">Crie uma pasta toostore seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6074b-115">Create a folder toostore your application.</span></span>  <span data-ttu-id="6074b-116">Em um console com as ferramentas de Node. js Olá no caminho atual, definir a nova pasta de toothis seu local atual e inicializar o projeto por meio da execução:</span><span class="sxs-lookup"><span data-stu-id="6074b-116">From a console with hello Node.js tools in your current path, set your current location toothis new folder and initialize your project by executing:</span></span>

    npm init

<span data-ttu-id="6074b-117">Em seguida, será apresentada uma série de perguntas tooinitialize seu projeto.</span><span class="sxs-lookup"><span data-stu-id="6074b-117">You will then be presented a series of questions tooinitialize your project.</span></span>  <span data-ttu-id="6074b-118">Para o **ponto de entrada**, este tutorial usa *app.js*.</span><span class="sxs-lookup"><span data-stu-id="6074b-118">For **entry point**, this tutorial uses *app.js*.</span></span>  <span data-ttu-id="6074b-119">Você pode ver meu outras opções Olá exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="6074b-119">You can see my other choices in hello following example.</span></span>

![Saída de NPM init](./media/cdn-app-dev-node/cdn-npm-init.png)

<span data-ttu-id="6074b-121">Agora, o projeto é inicializado com um arquivo *packages.json* .</span><span class="sxs-lookup"><span data-stu-id="6074b-121">Our project is now initialized with a *packages.json* file.</span></span>  <span data-ttu-id="6074b-122">Nosso projeto vai toouse algumas bibliotecas do Azure contidas em pacotes do NPM.</span><span class="sxs-lookup"><span data-stu-id="6074b-122">Our project is going toouse some Azure libraries contained in NPM packages.</span></span>  <span data-ttu-id="6074b-123">Vamos usar Olá tempo de execução do cliente do Azure para Node.js (ms-rest-azure) e hello biblioteca de cliente do Azure CDN para Node.js (azure-arm cd).</span><span class="sxs-lookup"><span data-stu-id="6074b-123">We'll use hello Azure Client Runtime for Node.js (ms-rest-azure) and hello Azure CDN Client Library for Node.js (azure-arm-cd).</span></span>  <span data-ttu-id="6074b-124">Vamos adicionar esses projeto toohello como dependências.</span><span class="sxs-lookup"><span data-stu-id="6074b-124">Let's add those toohello project as dependencies.</span></span>

    npm install --save ms-rest-azure
    npm install --save azure-arm-cdn

<span data-ttu-id="6074b-125">Depois de terminar de pacotes de saudação instalando, hello *Package. JSON* arquivo deve parecer semelhante toothis exemplo (versão números podem ser diferentes):</span><span class="sxs-lookup"><span data-stu-id="6074b-125">After hello packages are done installing, hello *package.json* file should look similar toothis example (version numbers may differ):</span></span>

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

<span data-ttu-id="6074b-126">Finalmente, usando seu editor de texto, crie um arquivo de texto em branco e salvá-lo na raiz de saudação da nossa pasta de projeto como *app.js*.</span><span class="sxs-lookup"><span data-stu-id="6074b-126">Finally, using your text editor, create a blank text file and save it in hello root of our project folder as *app.js*.</span></span>  <span data-ttu-id="6074b-127">Agora estamos pronto toobegin escrever código.</span><span class="sxs-lookup"><span data-stu-id="6074b-127">We're now ready toobegin writing code.</span></span>

## <a name="requires-constants-authentication-and-structure"></a><span data-ttu-id="6074b-128">Requisitos, constantes, autenticação e estrutura</span><span class="sxs-lookup"><span data-stu-id="6074b-128">Requires, constants, authentication, and structure</span></span>
<span data-ttu-id="6074b-129">Com *app.js* abra no nosso editor, vamos estrutura básica de saudação de nosso programa gravado.</span><span class="sxs-lookup"><span data-stu-id="6074b-129">With *app.js* open in our editor, let's get hello basic structure of our program written.</span></span>

1. <span data-ttu-id="6074b-130">Adicione hello "requer" para nossos pacotes NPM na parte superior da saudação com os seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="6074b-130">Add hello "requires" for our NPM packages at hello top with hello following:</span></span>
   
    ``` javascript
    var msRestAzure = require('ms-rest-azure');
    var cdnManagementClient = require('azure-arm-cdn');
    ```
2. <span data-ttu-id="6074b-131">Precisamos toodefine algumas constantes que nossos métodos usará.</span><span class="sxs-lookup"><span data-stu-id="6074b-131">We need toodefine some constants our methods will use.</span></span>  <span data-ttu-id="6074b-132">Adicione o seguinte de saudação.</span><span class="sxs-lookup"><span data-stu-id="6074b-132">Add hello following.</span></span>  <span data-ttu-id="6074b-133">Ser tooreplace se espaços reservados hello, incluindo Olá  **&lt;colchetes angulares&gt;**, com seus próprios valores conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="6074b-133">Be sure tooreplace hello placeholders, including hello **&lt;angle brackets&gt;**, with your own values as needed.</span></span>
   
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
3. <span data-ttu-id="6074b-134">Em seguida, vamos criar uma instância de cliente de gerenciamento de CDN hello e dê a ele credenciais.</span><span class="sxs-lookup"><span data-stu-id="6074b-134">Next, we'll instantiate hello CDN management client and give it our credentials.</span></span>
   
    ``` javascript
    var credentials = new msRestAzure.ApplicationTokenCredentials(clientId, tenantId, clientSecret);
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    <span data-ttu-id="6074b-135">Se você estiver usando a autenticação de usuário individual, essas duas linhas terão uma aparência ligeiramente diferente.</span><span class="sxs-lookup"><span data-stu-id="6074b-135">If you are using individual user authentication, these two lines will look slightly different.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="6074b-136">Somente use esse exemplo de código se você está escolhendo toohave autenticação de usuário individual em vez de uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="6074b-136">Only use this code sample if you are choosing toohave individual user authentication instead of a service principal.</span></span>  <span data-ttu-id="6074b-137">Ser tooguard cuidado suas credenciais de usuário individual e mantê-los segredo.</span><span class="sxs-lookup"><span data-stu-id="6074b-137">Be careful tooguard your individual user credentials and keep them secret.</span></span>
   > 
   > 
   
    ``` javascript
    var credentials = new msRestAzure.UserTokenCredentials(clientId, 
        tenantId, '<username>', '<password>', '<redirect URI>');
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    <span data-ttu-id="6074b-138">Ter tooreplace-se de que os itens de saudação no  **&lt;colchetes angulares&gt;**  com hello informações corretas.</span><span class="sxs-lookup"><span data-stu-id="6074b-138">Be sure tooreplace hello items in **&lt;angle brackets&gt;** with hello correct information.</span></span>  <span data-ttu-id="6074b-139">Para `<redirect URI>`, use o redirecionamento de saudação URI que você inseriu quando registrou o aplicativo hello no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="6074b-139">For `<redirect URI>`, use hello redirect URI you entered when you registered hello application in Azure AD.</span></span>
4. <span data-ttu-id="6074b-140">Nosso aplicativo de console Node. js será tootake alguns parâmetros de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="6074b-140">Our Node.js console application is going tootake some command-line parameters.</span></span>  <span data-ttu-id="6074b-141">Validaremos que pelo menos um parâmetro foi passado.</span><span class="sxs-lookup"><span data-stu-id="6074b-141">Let's validate that at least one parameter was passed.</span></span>
   
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
5. <span data-ttu-id="6074b-142">Chegamos toohello principal parte de nosso programa, onde podemos ramificam tooother funções com base em quais parâmetros foram passados.</span><span class="sxs-lookup"><span data-stu-id="6074b-142">That brings us toohello main part of our program, where we branch off tooother functions based on what parameters were passed.</span></span>
   
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
6. <span data-ttu-id="6074b-143">Em vários locais em nosso programa, vamos precisar toomake-se de que o número correto de saudação de parâmetros foram passado e exibe ajuda se eles não tiverem corretos.</span><span class="sxs-lookup"><span data-stu-id="6074b-143">At several places in our program, we'll need toomake sure hello right number of parameters were passed in and display some help if they don't look correct.</span></span>  <span data-ttu-id="6074b-144">Vamos criar funções toodo que.</span><span class="sxs-lookup"><span data-stu-id="6074b-144">Let's create functions toodo that.</span></span>
   
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
7. <span data-ttu-id="6074b-145">Por fim, funções hello que será usado no cliente de gerenciamento de CDN Olá são assíncronas, assim, precisam de um método toocall quando ele terminar.</span><span class="sxs-lookup"><span data-stu-id="6074b-145">Finally, hello functions we'll be using on hello CDN management client are asynchronous, so they need a method toocall back when they're done.</span></span>  <span data-ttu-id="6074b-146">Vamos fazer um que pode exibir a saída de saudação do cliente de gerenciamento de CDN hello (se houver) e sair de saudação normalmente.</span><span class="sxs-lookup"><span data-stu-id="6074b-146">Let's make one that can display hello output from hello CDN management client (if any) and exit hello program gracefully.</span></span>
   
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

<span data-ttu-id="6074b-147">Agora que a estrutura básica de saudação do programa é gravada, podemos deve criar funções de saudação chamadas com base em nossos parâmetros.</span><span class="sxs-lookup"><span data-stu-id="6074b-147">Now that hello basic structure of our program is written, we should create hello functions called based on our parameters.</span></span>

## <a name="list-cdn-profiles-and-endpoints"></a><span data-ttu-id="6074b-148">Relacione os perfis CDN e os pontos de extremidade</span><span class="sxs-lookup"><span data-stu-id="6074b-148">List CDN profiles and endpoints</span></span>
<span data-ttu-id="6074b-149">Vamos começar com toolist código nossos perfis existentes e os pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="6074b-149">Let's start with code toolist our existing profiles and endpoints.</span></span>  <span data-ttu-id="6074b-150">Comentários de código fornecem uma sintaxe Olá esperado para sabermos onde vai cada parâmetro.</span><span class="sxs-lookup"><span data-stu-id="6074b-150">My code comments provide hello expected syntax so we know where each parameter goes.</span></span>

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

## <a name="create-cdn-profiles-and-endpoints"></a><span data-ttu-id="6074b-151">Criar perfis CDN e pontos de extremidade</span><span class="sxs-lookup"><span data-stu-id="6074b-151">Create CDN profiles and endpoints</span></span>
<span data-ttu-id="6074b-152">Em seguida, vamos gravar perfis de toocreate funções hello e de pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="6074b-152">Next, we'll write hello functions toocreate profiles and endpoints.</span></span>

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

## <a name="purge-an-endpoint"></a><span data-ttu-id="6074b-153">Limpar um ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="6074b-153">Purge an endpoint</span></span>
<span data-ttu-id="6074b-154">Supondo que o ponto de extremidade de saudação foi criado, uma tarefa comum que que talvez desejemos tooperform em nosso programa está limpando conteúdo no ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="6074b-154">Assuming hello endpoint has been created, one common task that we might want tooperform in our program is purging content in our endpoint.</span></span>

```javascript
// purge <profile name> <endpoint name> <path>
function cdnPurge() {
    requireParms(4);
    console.log("Purging endpoint...");
    var purgeContentPaths = [ parms[3] ];
    cdnClient.endpoints.purgeContent(parms[2], parms[1], resourceGroupName, purgeContentPaths, callback);
}
```

## <a name="delete-cdn-profiles-and-endpoints"></a><span data-ttu-id="6074b-155">Excluir perfis CDN e pontos de extremidade</span><span class="sxs-lookup"><span data-stu-id="6074b-155">Delete CDN profiles and endpoints</span></span>
<span data-ttu-id="6074b-156">função last Hello, que incluiremos exclui perfis e pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="6074b-156">hello last function we will include deletes endpoints and profiles.</span></span>

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

## <a name="running-hello-program"></a><span data-ttu-id="6074b-157">Programa de saudação em execução</span><span class="sxs-lookup"><span data-stu-id="6074b-157">Running hello program</span></span>
<span data-ttu-id="6074b-158">Agora podemos executar nosso programa Node. js usando nosso depurador favorito ou no console de saudação.</span><span class="sxs-lookup"><span data-stu-id="6074b-158">We can now execute our Node.js program using our favorite debugger or at hello console.</span></span>

> [!TIP]
> <span data-ttu-id="6074b-159">Se você estiver usando o código do Visual Studio como o depurador, você precisará tooset backup toopass seu ambiente nos parâmetros de linha de comando hello.</span><span class="sxs-lookup"><span data-stu-id="6074b-159">If you're using Visual Studio Code as your debugger, you'll need tooset up your environment toopass in hello command-line parameters.</span></span>  <span data-ttu-id="6074b-160">Código do Visual Studio faz isso de saudação **lanuch.json** arquivo.</span><span class="sxs-lookup"><span data-stu-id="6074b-160">Visual Studio Code does this in hello **lanuch.json** file.</span></span>  <span data-ttu-id="6074b-161">Procure uma propriedade chamada **args** e adicione uma matriz de valores de cadeia de caracteres para seus parâmetros, para que ele se parece semelhante toothis: `"args": ["list", "profiles"]`.</span><span class="sxs-lookup"><span data-stu-id="6074b-161">Look for a property named **args** and add an array of string values for your parameters, so that it looks similar toothis:  `"args": ["list", "profiles"]`.</span></span>
> 
> 

<span data-ttu-id="6074b-162">Vamos começar listando os perfis.</span><span class="sxs-lookup"><span data-stu-id="6074b-162">Let's start by listing our profiles.</span></span>

![Listar perfis](./media/cdn-app-dev-node/cdn-list-profiles.png)

<span data-ttu-id="6074b-164">Obtivemos uma matriz vazia.</span><span class="sxs-lookup"><span data-stu-id="6074b-164">We got back an empty array.</span></span>  <span data-ttu-id="6074b-165">Como não há perfis no grupo de recursos, isso é esperado.</span><span class="sxs-lookup"><span data-stu-id="6074b-165">Since we don't have any profiles in our resource group, that's expected.</span></span>  <span data-ttu-id="6074b-166">Vamos criar um perfil agora.</span><span class="sxs-lookup"><span data-stu-id="6074b-166">Let's create a profile now.</span></span>

![Criar perfil](./media/cdn-app-dev-node/cdn-create-profile.png)

<span data-ttu-id="6074b-168">Agora, vamos adicionar um ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="6074b-168">Now, let's add an endpoint.</span></span>

![Criar ponto de extremidade](./media/cdn-app-dev-node/cdn-create-endpoint.png)

<span data-ttu-id="6074b-170">Por fim, vamos excluir o perfil.</span><span class="sxs-lookup"><span data-stu-id="6074b-170">Finally, let's delete our profile.</span></span>

![Excluir perfil](./media/cdn-app-dev-node/cdn-delete-profile.png)

## <a name="next-steps"></a><span data-ttu-id="6074b-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6074b-172">Next Steps</span></span>
<span data-ttu-id="6074b-173">projeto de saudação concluída toosee deste passo a passo, [baixar exemplo hello](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).</span><span class="sxs-lookup"><span data-stu-id="6074b-173">toosee hello completed project from this walkthrough, [download hello sample](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).</span></span>

<span data-ttu-id="6074b-174">referência de saudação toosee para hello Azure CDN SDK para Node.js, Olá de exibição [referência](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).</span><span class="sxs-lookup"><span data-stu-id="6074b-174">toosee hello reference for hello Azure CDN SDK for Node.js, view hello [reference](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).</span></span>

<span data-ttu-id="6074b-175">toofind obter documentação adicional sobre hello Azure SDK para Node.js, Olá exibição [completo referência](http://azure.github.io/azure-sdk-for-node/).</span><span class="sxs-lookup"><span data-stu-id="6074b-175">toofind additional documentation on hello Azure SDK for Node.js, view hello [full reference](http://azure.github.io/azure-sdk-for-node/).</span></span>

<span data-ttu-id="6074b-176">Gerencie seus recursos CDN com o [PowerShell](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="6074b-176">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span></span>

