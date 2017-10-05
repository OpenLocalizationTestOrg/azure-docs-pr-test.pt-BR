---
title: "Introdução ao SDK da CDN do Azure para Node.js | Microsoft Docs"
description: Aprenda a escrever aplicativos do Node.js para gerenciar a CDN do Azure.
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
ms.openlocfilehash: 46ae8cd9775432d126cbde856c1fb06ea319297e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-cdn-development"></a><span data-ttu-id="3ea10-103">Introdução ao desenvolvimento de CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="3ea10-103">Get started with Azure CDN development</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3ea10-104">Node.js</span><span class="sxs-lookup"><span data-stu-id="3ea10-104">Node.js</span></span>](cdn-app-dev-node.md)
> * [<span data-ttu-id="3ea10-105">.NET</span><span class="sxs-lookup"><span data-stu-id="3ea10-105">.NET</span></span>](cdn-app-dev-net.md)
> 
> 

<span data-ttu-id="3ea10-106">Você pode usar o [SDK da CDN do Azure para Node.js](https://www.npmjs.com/package/azure-arm-cdn) para automatizar a criação e o gerenciamento de pontos de extremidade e perfis de CDN.</span><span class="sxs-lookup"><span data-stu-id="3ea10-106">You can use the [Azure CDN SDK for Node.js](https://www.npmjs.com/package/azure-arm-cdn) to automate creation and management of CDN profiles and endpoints.</span></span>  <span data-ttu-id="3ea10-107">Este tutorial o orienta na criação de um aplicativo de console simples do Node.js, que demonstra várias operações disponíveis.</span><span class="sxs-lookup"><span data-stu-id="3ea10-107">This tutorial walks through the creation of a simple Node.js console application that demonstrates several of the available operations.</span></span>  <span data-ttu-id="3ea10-108">Este tutorial não se destina a descrever em detalhes todos os aspectos do SDK da CDN do Azure para Node.js.</span><span class="sxs-lookup"><span data-stu-id="3ea10-108">This tutorial is not intended to describe all aspects of the Azure CDN SDK for Node.js in detail.</span></span>

<span data-ttu-id="3ea10-109">Para concluir este tutorial, você já deve ter o [Node.js](http://www.nodejs.org) **4.x.x** ou posterior instalado e configurado.</span><span class="sxs-lookup"><span data-stu-id="3ea10-109">To complete this tutorial, you should already have [Node.js](http://www.nodejs.org) **4.x.x** or higher installed and configured.</span></span>  <span data-ttu-id="3ea10-110">Você pode usar qualquer editor de texto que desejar para criar o aplicativo do Node.js.</span><span class="sxs-lookup"><span data-stu-id="3ea10-110">You can use any text editor you want to create your Node.js application.</span></span>  <span data-ttu-id="3ea10-111">Para escrever este tutorial, usei o [Visual Studio Code](https://code.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="3ea10-111">To write this tutorial, I used [Visual Studio Code](https://code.visualstudio.com).</span></span>  

> [!TIP]
> <span data-ttu-id="3ea10-112">O [projeto concluído deste tutorial](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) está disponível para download no MSDN.</span><span class="sxs-lookup"><span data-stu-id="3ea10-112">The [completed project from this tutorial](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) is available for download on MSDN.</span></span>
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-npm-dependencies"></a><span data-ttu-id="3ea10-113">Criar o projeto e adicionar dependências de NPM</span><span class="sxs-lookup"><span data-stu-id="3ea10-113">Create your project and add NPM dependencies</span></span>
<span data-ttu-id="3ea10-114">Agora que criamos um grupo de recursos para nossos perfis CDN e demos permissão para o nosso aplicativo Azure AD gerenciar os perfis CDN e os pontos de extremidade neste grupo, podemos começar a criação do nosso aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3ea10-114">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission to manage CDN profiles and endpoints within that group, we can start creating our application.</span></span>

<span data-ttu-id="3ea10-115">Crie uma pasta para armazenar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3ea10-115">Create a folder to store your application.</span></span>  <span data-ttu-id="3ea10-116">Em um console com as ferramentas do Node.js no caminho atual, defina o local atual para essa nova pasta e inicialize o projeto executando:</span><span class="sxs-lookup"><span data-stu-id="3ea10-116">From a console with the Node.js tools in your current path, set your current location to this new folder and initialize your project by executing:</span></span>

    npm init

<span data-ttu-id="3ea10-117">Em seguida, será apresentada uma série de perguntas para inicializar o projeto.</span><span class="sxs-lookup"><span data-stu-id="3ea10-117">You will then be presented a series of questions to initialize your project.</span></span>  <span data-ttu-id="3ea10-118">Para o **ponto de entrada**, este tutorial usa *app.js*.</span><span class="sxs-lookup"><span data-stu-id="3ea10-118">For **entry point**, this tutorial uses *app.js*.</span></span>  <span data-ttu-id="3ea10-119">Você pode ver minhas outras opções no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="3ea10-119">You can see my other choices in the following example.</span></span>

![Saída de NPM init](./media/cdn-app-dev-node/cdn-npm-init.png)

<span data-ttu-id="3ea10-121">Agora, o projeto é inicializado com um arquivo *packages.json* .</span><span class="sxs-lookup"><span data-stu-id="3ea10-121">Our project is now initialized with a *packages.json* file.</span></span>  <span data-ttu-id="3ea10-122">Nosso projeto usará algumas bibliotecas do Azure contidas em pacotes NPM.</span><span class="sxs-lookup"><span data-stu-id="3ea10-122">Our project is going to use some Azure libraries contained in NPM packages.</span></span>  <span data-ttu-id="3ea10-123">Usaremos a Execução do Cliente do Azure para Node.js (ms-rest-azure) e a Biblioteca de Clientes de CDN do Azure para Node.js (azure-arm-cd).</span><span class="sxs-lookup"><span data-stu-id="3ea10-123">We'll use the Azure Client Runtime for Node.js (ms-rest-azure) and the Azure CDN Client Library for Node.js (azure-arm-cd).</span></span>  <span data-ttu-id="3ea10-124">Vamos adicioná-los ao projeto como dependências.</span><span class="sxs-lookup"><span data-stu-id="3ea10-124">Let's add those to the project as dependencies.</span></span>

    npm install --save ms-rest-azure
    npm install --save azure-arm-cdn

<span data-ttu-id="3ea10-125">Depois dos pacotes terminarem de ser instalados, o arquivo *package.json* deverá ser semelhante a este exemplo (os números de versão podem diferir):</span><span class="sxs-lookup"><span data-stu-id="3ea10-125">After the packages are done installing, the *package.json* file should look similar to this example (version numbers may differ):</span></span>

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

<span data-ttu-id="3ea10-126">Finalmente, usando o editor de texto, crie um arquivo de texto em branco e salve-o na raiz da pasta do projeto como *app.js*.</span><span class="sxs-lookup"><span data-stu-id="3ea10-126">Finally, using your text editor, create a blank text file and save it in the root of our project folder as *app.js*.</span></span>  <span data-ttu-id="3ea10-127">Agora estamos prontos para começar a escrever o código.</span><span class="sxs-lookup"><span data-stu-id="3ea10-127">We're now ready to begin writing code.</span></span>

## <a name="requires-constants-authentication-and-structure"></a><span data-ttu-id="3ea10-128">Requisitos, constantes, autenticação e estrutura</span><span class="sxs-lookup"><span data-stu-id="3ea10-128">Requires, constants, authentication, and structure</span></span>
<span data-ttu-id="3ea10-129">Com *app.js* aberto no editor, vamos escrever a estrutura básica do programa.</span><span class="sxs-lookup"><span data-stu-id="3ea10-129">With *app.js* open in our editor, let's get the basic structure of our program written.</span></span>

1. <span data-ttu-id="3ea10-130">Adicione os "requisitos" para os pacotes de NPM na parte superior com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="3ea10-130">Add the "requires" for our NPM packages at the top with the following:</span></span>
   
    ``` javascript
    var msRestAzure = require('ms-rest-azure');
    var cdnManagementClient = require('azure-arm-cdn');
    ```
2. <span data-ttu-id="3ea10-131">Precisamos definir algumas constantes que serão usadas nos nossos métodos.</span><span class="sxs-lookup"><span data-stu-id="3ea10-131">We need to define some constants our methods will use.</span></span>  <span data-ttu-id="3ea10-132">Adicione o seguinte.</span><span class="sxs-lookup"><span data-stu-id="3ea10-132">Add the following.</span></span>  <span data-ttu-id="3ea10-133">Substitua os espaços reservados, inclusive os **&lt;sinais maior e menor que&gt;**, por seus próprios valores, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="3ea10-133">Be sure to replace the placeholders, including the **&lt;angle brackets&gt;**, with your own values as needed.</span></span>
   
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
3. <span data-ttu-id="3ea10-134">Em seguida, instanciaremos o cliente de gerenciamento de CDN e forneceremos as credenciais.</span><span class="sxs-lookup"><span data-stu-id="3ea10-134">Next, we'll instantiate the CDN management client and give it our credentials.</span></span>
   
    ``` javascript
    var credentials = new msRestAzure.ApplicationTokenCredentials(clientId, tenantId, clientSecret);
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    <span data-ttu-id="3ea10-135">Se você estiver usando a autenticação de usuário individual, essas duas linhas terão uma aparência ligeiramente diferente.</span><span class="sxs-lookup"><span data-stu-id="3ea10-135">If you are using individual user authentication, these two lines will look slightly different.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="3ea10-136">Use este exemplo de código somente se optar pela autenticação de usuário individual, em vez de uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="3ea10-136">Only use this code sample if you are choosing to have individual user authentication instead of a service principal.</span></span>  <span data-ttu-id="3ea10-137">Tenha muito cuidado para proteger suas credenciais de usuário individuais e mantê-las secretas.</span><span class="sxs-lookup"><span data-stu-id="3ea10-137">Be careful to guard your individual user credentials and keep them secret.</span></span>
   > 
   > 
   
    ``` javascript
    var credentials = new msRestAzure.UserTokenCredentials(clientId, 
        tenantId, '<username>', '<password>', '<redirect URI>');
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    <span data-ttu-id="3ea10-138">Substitua os itens nos **&lt;sinais maior e menor que&gt;** pelas informações corretas.</span><span class="sxs-lookup"><span data-stu-id="3ea10-138">Be sure to replace the items in **&lt;angle brackets&gt;** with the correct information.</span></span>  <span data-ttu-id="3ea10-139">Para `<redirect URI>`, use o URI de redirecionamento que você inseriu quando registrou o aplicativo no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ea10-139">For `<redirect URI>`, use the redirect URI you entered when you registered the application in Azure AD.</span></span>
4. <span data-ttu-id="3ea10-140">O aplicativo de console do Node.js usará alguns parâmetros da linha de comando.</span><span class="sxs-lookup"><span data-stu-id="3ea10-140">Our Node.js console application is going to take some command-line parameters.</span></span>  <span data-ttu-id="3ea10-141">Validaremos que pelo menos um parâmetro foi passado.</span><span class="sxs-lookup"><span data-stu-id="3ea10-141">Let's validate that at least one parameter was passed.</span></span>
   
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
5. <span data-ttu-id="3ea10-142">Isso nos leva para a parte principal do programa, na qual fazemos a ramificação para outras funções com base nos parâmetros passados.</span><span class="sxs-lookup"><span data-stu-id="3ea10-142">That brings us to the main part of our program, where we branch off to other functions based on what parameters were passed.</span></span>
   
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
6. <span data-ttu-id="3ea10-143">Em vários locais no programa, é necessário verificar se o número correto de parâmetros foi passado e exibir ajuda se eles não estiverem corretos.</span><span class="sxs-lookup"><span data-stu-id="3ea10-143">At several places in our program, we'll need to make sure the right number of parameters were passed in and display some help if they don't look correct.</span></span>  <span data-ttu-id="3ea10-144">Vamos criar funções para fazer isso.</span><span class="sxs-lookup"><span data-stu-id="3ea10-144">Let's create functions to do that.</span></span>
   
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
7. <span data-ttu-id="3ea10-145">Finalmente, as funções que usaremos no cliente de gerenciamento de CDN são assíncronas, assim, precisam de um método de retorno de chamada quando são concluídas.</span><span class="sxs-lookup"><span data-stu-id="3ea10-145">Finally, the functions we'll be using on the CDN management client are asynchronous, so they need a method to call back when they're done.</span></span>  <span data-ttu-id="3ea10-146">Vamos criar um que possa exibir a saída do cliente de gerenciamento de CDN (se houver) e sair do programa normalmente.</span><span class="sxs-lookup"><span data-stu-id="3ea10-146">Let's make one that can display the output from the CDN management client (if any) and exit the program gracefully.</span></span>
   
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

<span data-ttu-id="3ea10-147">Agora que a estrutura básica do programa foi escrita, devemos criar as funções chamadas com base em nossos parâmetros.</span><span class="sxs-lookup"><span data-stu-id="3ea10-147">Now that the basic structure of our program is written, we should create the functions called based on our parameters.</span></span>

## <a name="list-cdn-profiles-and-endpoints"></a><span data-ttu-id="3ea10-148">Relacione os perfis CDN e os pontos de extremidade</span><span class="sxs-lookup"><span data-stu-id="3ea10-148">List CDN profiles and endpoints</span></span>
<span data-ttu-id="3ea10-149">Vamos começar com o código para listar os perfis e os pontos de extremidade existentes.</span><span class="sxs-lookup"><span data-stu-id="3ea10-149">Let's start with code to list our existing profiles and endpoints.</span></span>  <span data-ttu-id="3ea10-150">Os comentários do código fornecem a sintaxe esperada para que saibamos onde fica cada parâmetro.</span><span class="sxs-lookup"><span data-stu-id="3ea10-150">My code comments provide the expected syntax so we know where each parameter goes.</span></span>

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

## <a name="create-cdn-profiles-and-endpoints"></a><span data-ttu-id="3ea10-151">Criar perfis CDN e pontos de extremidade</span><span class="sxs-lookup"><span data-stu-id="3ea10-151">Create CDN profiles and endpoints</span></span>
<span data-ttu-id="3ea10-152">Em seguida, escreveremos as funções para criar perfis e pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="3ea10-152">Next, we'll write the functions to create profiles and endpoints.</span></span>

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

## <a name="purge-an-endpoint"></a><span data-ttu-id="3ea10-153">Limpar um ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="3ea10-153">Purge an endpoint</span></span>
<span data-ttu-id="3ea10-154">Supondo que o ponto de extremidade tenha sido criado, uma tarefa comum que convém executar no programa é limpar o conteúdo no ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="3ea10-154">Assuming the endpoint has been created, one common task that we might want to perform in our program is purging content in our endpoint.</span></span>

```javascript
// purge <profile name> <endpoint name> <path>
function cdnPurge() {
    requireParms(4);
    console.log("Purging endpoint...");
    var purgeContentPaths = [ parms[3] ];
    cdnClient.endpoints.purgeContent(parms[2], parms[1], resourceGroupName, purgeContentPaths, callback);
}
```

## <a name="delete-cdn-profiles-and-endpoints"></a><span data-ttu-id="3ea10-155">Excluir perfis CDN e pontos de extremidade</span><span class="sxs-lookup"><span data-stu-id="3ea10-155">Delete CDN profiles and endpoints</span></span>
<span data-ttu-id="3ea10-156">A última função que incluiremos exclui pontos de extremidade e perfis.</span><span class="sxs-lookup"><span data-stu-id="3ea10-156">The last function we will include deletes endpoints and profiles.</span></span>

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

## <a name="running-the-program"></a><span data-ttu-id="3ea10-157">Executando o programa</span><span class="sxs-lookup"><span data-stu-id="3ea10-157">Running the program</span></span>
<span data-ttu-id="3ea10-158">Agora podemos executar o programa do Node.js usando o depurador que preferirmos ou no console.</span><span class="sxs-lookup"><span data-stu-id="3ea10-158">We can now execute our Node.js program using our favorite debugger or at the console.</span></span>

> [!TIP]
> <span data-ttu-id="3ea10-159">Se você estiver usando o Código do Visual Studio como depurador, precisará configurar o ambiente para passar os parâmetros da linha de comando.</span><span class="sxs-lookup"><span data-stu-id="3ea10-159">If you're using Visual Studio Code as your debugger, you'll need to set up your environment to pass in the command-line parameters.</span></span>  <span data-ttu-id="3ea10-160">O Código do Visual Studio faz isso no arquivo **lanuch.json** .</span><span class="sxs-lookup"><span data-stu-id="3ea10-160">Visual Studio Code does this in the **lanuch.json** file.</span></span>  <span data-ttu-id="3ea10-161">Procure uma propriedade denominada **args** e adicione uma matriz de valores da cadeia de caracteres aos parâmetros, para que seja semelhante a isto: `"args": ["list", "profiles"]`.</span><span class="sxs-lookup"><span data-stu-id="3ea10-161">Look for a property named **args** and add an array of string values for your parameters, so that it looks similar to this:  `"args": ["list", "profiles"]`.</span></span>
> 
> 

<span data-ttu-id="3ea10-162">Vamos começar listando os perfis.</span><span class="sxs-lookup"><span data-stu-id="3ea10-162">Let's start by listing our profiles.</span></span>

![Listar perfis](./media/cdn-app-dev-node/cdn-list-profiles.png)

<span data-ttu-id="3ea10-164">Obtivemos uma matriz vazia.</span><span class="sxs-lookup"><span data-stu-id="3ea10-164">We got back an empty array.</span></span>  <span data-ttu-id="3ea10-165">Como não há perfis no grupo de recursos, isso é esperado.</span><span class="sxs-lookup"><span data-stu-id="3ea10-165">Since we don't have any profiles in our resource group, that's expected.</span></span>  <span data-ttu-id="3ea10-166">Vamos criar um perfil agora.</span><span class="sxs-lookup"><span data-stu-id="3ea10-166">Let's create a profile now.</span></span>

![Criar perfil](./media/cdn-app-dev-node/cdn-create-profile.png)

<span data-ttu-id="3ea10-168">Agora, vamos adicionar um ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="3ea10-168">Now, let's add an endpoint.</span></span>

![Criar ponto de extremidade](./media/cdn-app-dev-node/cdn-create-endpoint.png)

<span data-ttu-id="3ea10-170">Por fim, vamos excluir o perfil.</span><span class="sxs-lookup"><span data-stu-id="3ea10-170">Finally, let's delete our profile.</span></span>

![Excluir perfil](./media/cdn-app-dev-node/cdn-delete-profile.png)

## <a name="next-steps"></a><span data-ttu-id="3ea10-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3ea10-172">Next Steps</span></span>
<span data-ttu-id="3ea10-173">Para ver o projeto concluído desse passo a passo, [baixe o exemplo](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).</span><span class="sxs-lookup"><span data-stu-id="3ea10-173">To see the completed project from this walkthrough, [download the sample](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).</span></span>

<span data-ttu-id="3ea10-174">Para ver a referência do SDK da CDN do Azure para Node.js, exiba a [referência](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).</span><span class="sxs-lookup"><span data-stu-id="3ea10-174">To see the reference for the Azure CDN SDK for Node.js, view the [reference](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).</span></span>

<span data-ttu-id="3ea10-175">Para localizar documentação adicional sobre o SDK do Azure para Node.js, exiba a [referência completa](http://azure.github.io/azure-sdk-for-node/).</span><span class="sxs-lookup"><span data-stu-id="3ea10-175">To find additional documentation on the Azure SDK for Node.js, view the [full reference](http://azure.github.io/azure-sdk-for-node/).</span></span>

<span data-ttu-id="3ea10-176">Gerencie seus recursos CDN com o [PowerShell](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="3ea10-176">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span></span>

