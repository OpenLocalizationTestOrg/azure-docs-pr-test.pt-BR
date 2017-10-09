---
title: "aaaCORS suporte no serviço de aplicativo | Microsoft Docs"
description: "Saiba como toouse CORS dão suporte ao serviço de aplicativo do Azure do Azure."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 4f980a97-b9f5-4d1d-87ab-82b60bb96e1c
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/27/2016
ms.author: alkarche
ms.openlocfilehash: c229378b75840bc0f7b2eefc3df3031233f9b494
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-api-app-from-javascript-using-cors"></a><span data-ttu-id="8714e-103">Consumir um aplicativo de API do JavaScript usando CORS</span><span class="sxs-lookup"><span data-stu-id="8714e-103">Consume an API app from JavaScript using CORS</span></span>
<span data-ttu-id="8714e-104">Serviço de aplicativo oferece suporte interno para [compartilhamento de recursos entre origens (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), que permite que o JavaScript clientes entre toomake domínios chama tooAPIs que são hospedados em aplicativos de API.</span><span class="sxs-lookup"><span data-stu-id="8714e-104">App Service offers built-in support for [Cross Origin Resource Sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), which enables JavaScript clients toomake cross-domain calls tooAPIs that are hosted in API apps.</span></span> <span data-ttu-id="8714e-105">Serviço de aplicativo permite configurar CORS acesso tooyour API sem gravar qualquer código em sua API.</span><span class="sxs-lookup"><span data-stu-id="8714e-105">App Service lets you configure CORS access tooyour API without writing any code in your API.</span></span>

<span data-ttu-id="8714e-106">Este artigo contém duas seções:</span><span class="sxs-lookup"><span data-stu-id="8714e-106">This article contains two sections:</span></span>

* <span data-ttu-id="8714e-107">Olá [como tooconfigure CORS](#corsconfig) seção explica como geral tooconfigure CORS para qualquer aplicativo de API, aplicativo web ou aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="8714e-107">hello [How tooconfigure CORS](#corsconfig) section explains in general how tooconfigure CORS for any API app, web app, or mobile app.</span></span> <span data-ttu-id="8714e-108">Ele se aplica igualmente tooall estruturas que são suportadas pelo serviço de aplicativo, incluindo .NET, Node.js e Java.</span><span class="sxs-lookup"><span data-stu-id="8714e-108">It applies equally tooall frameworks that are supported by App Service, including .NET, Node.js, and Java.</span></span> 
* <span data-ttu-id="8714e-109">Começando com hello [continuar tutoriais de Introdução .NET de saudação](#tutorialstart) seção, artigo Olá é um tutorial que demonstra o suporte de CORS com base em que você fez [Olá primeiro aplicativos de API tutorial de Introdução ](app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8714e-109">Starting with hello [Continuing hello .NET getting-started tutorials](#tutorialstart) section, hello article is a tutorial that demonstrates CORS support by building on what you did in [hello first API Apps getting started tutorial](app-service-api-dotnet-get-started.md).</span></span> 

## <span data-ttu-id="8714e-110"><a id="corsconfig"></a>Como tooconfigure CORS no serviço de aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="8714e-110"><a id="corsconfig"></a> How tooconfigure CORS in Azure App Service</span></span>
<span data-ttu-id="8714e-111">Você pode configurar CORS no hello portal do Azure ou usando [do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) ferramentas.</span><span class="sxs-lookup"><span data-stu-id="8714e-111">You can configure CORS in hello Azure portal or by using [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) tools.</span></span>

#### <a name="configure-cors-in-hello-azure-portal"></a><span data-ttu-id="8714e-112">Configurar CORS Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8714e-112">Configure CORS in hello Azure portal</span></span>
1. <span data-ttu-id="8714e-113">Em um navegador, vá toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8714e-113">In a browser go toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="8714e-114">Clique em **serviços de aplicativos**e, em seguida, clique em nome de saudação do seu aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="8714e-114">Click **App Services**, and then click hello name of your API app.</span></span>
   
    ![Selecione o aplicativo de API no portal](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. <span data-ttu-id="8714e-116">Em Olá **configurações** folha que abre toohello direito da saudação **aplicativo de API** folha, localizar Olá **API** seção e, em seguida, clique em **CORS**.</span><span class="sxs-lookup"><span data-stu-id="8714e-116">In hello **Settings** blade that opens toohello right of hello **API app** blade, find hello **API** section, and then click **CORS**.</span></span>
   
   ![Selecione CORS na folha configurações](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. <span data-ttu-id="8714e-118">Na caixa de texto de saudação digite Olá URL ou URLs que você deseja tooallow toocome de chamadas de JavaScript do.</span><span class="sxs-lookup"><span data-stu-id="8714e-118">In hello text box enter hello URL or URLs that you want tooallow JavaScript calls toocome from.</span></span>

    <span data-ttu-id="8714e-119">Por exemplo, se você implantou seu aplicativo web do JavaScript aplicativo tooa denominado todolistangular, digite "https://todolistangular.azurewebsites.net".</span><span class="sxs-lookup"><span data-stu-id="8714e-119">For example, if you deployed your JavaScript application tooa web app named todolistangular, enter "https://todolistangular.azurewebsites.net".</span></span> <span data-ttu-id="8714e-120">Como alternativa, você pode inserir um toospecify de asterisco (*) que todos os domínios de origem são aceitos.</span><span class="sxs-lookup"><span data-stu-id="8714e-120">As an alternative, you can enter an asterisk (*) toospecify that all origin domains are accepted.</span></span>


1. <span data-ttu-id="8714e-121">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="8714e-121">Click **Save**.</span></span>
   
   ![Clique em Salvar](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   <span data-ttu-id="8714e-123">Depois de clicar em **salvar**, aplicativo hello API aceitará JavaScript chamadas de saudação especificado URLs.</span><span class="sxs-lookup"><span data-stu-id="8714e-123">After you click **Save**, hello API app will accept JavaScript calls from hello specified URLs.</span></span>

#### <a name="configure-cors-by-using-azure-resource-manager-tools"></a><span data-ttu-id="8714e-124">Configurar CORS usando as ferramentas do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8714e-124">Configure CORS by using Azure Resource Manager tools</span></span>
<span data-ttu-id="8714e-125">Você também pode configurar o CORS para um aplicativo de API usando [modelos do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) em ferramentas de linha de comando como [Azure PowerShell](/powershell/azureps-cmdlets-docs) e hello [CLI do Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="8714e-125">You can also configure CORS for an API app by using [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) in command line tools such as [Azure PowerShell](/powershell/azureps-cmdlets-docs) and hello [Azure CLI](../cli-install-nodejs.md).</span></span> 

<span data-ttu-id="8714e-126">Para obter um exemplo de um modelo do Azure Resource Manager que define a propriedade CORS hello, abra Olá [arquivo azuredeploy.json no repositório de saudação aplicativo neste tutorial de exemplo](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="8714e-126">For an example of an Azure Resource Manager template that sets hello CORS property, open hello [azuredeploy.json file in hello repository for this tutorial's sample application](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json).</span></span> <span data-ttu-id="8714e-127">Localize a seção de saudação do modelo de saudação que se parece com hello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="8714e-127">Find hello section of hello template that looks like hello following example:</span></span>

        "cors": {
            "allowedOrigins": [
                "todolistangular.azurewebsites.net"
            ]
        }

## <span data-ttu-id="8714e-128"><a id="tutorialstart"></a>Continuando o tutorial de Introdução .NET de saudação</span><span class="sxs-lookup"><span data-stu-id="8714e-128"><a id="tutorialstart"></a> Continuing hello .NET getting-started tutorial</span></span>
<span data-ttu-id="8714e-129">Se você estiver seguindo Olá Node. js Java Introdução série ou para aplicativos de API, você ter concluído Olá obtendo série iniciada.</span><span class="sxs-lookup"><span data-stu-id="8714e-129">If you are following hello Node.js or Java getting-started series for API apps, you have completed hello getting started series.</span></span> <span data-ttu-id="8714e-130">Ignorar toohello [próximas etapas](#next-steps) seção toofind sugestões para aprender mais sobre aplicativos de API.</span><span class="sxs-lookup"><span data-stu-id="8714e-130">Skip toohello [Next steps](#next-steps) section toofind suggestions for further learning about API Apps.</span></span>

<span data-ttu-id="8714e-131">Olá restante deste artigo é uma continuação de saudação série de guia de Introdução .NET e presume que você concluiu com êxito [tutorial primeiro Olá](app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8714e-131">hello remainder of this article is a continuation of hello .NET getting-started series and assumes that you successfully completed [hello first tutorial](app-service-api-dotnet-get-started.md).</span></span>

## <a name="deploy-hello-todolistangular-project-tooa-new-web-app"></a><span data-ttu-id="8714e-132">Implantar Olá ToDoListAngular projeto tooa novo aplicativo web</span><span class="sxs-lookup"><span data-stu-id="8714e-132">Deploy hello ToDoListAngular project tooa new web app</span></span>
<span data-ttu-id="8714e-133">Em [tutorial primeiro Olá](app-service-api-dotnet-get-started.md), você criou um aplicativo de camada intermediária API e um aplicativo de API de camada de dados.</span><span class="sxs-lookup"><span data-stu-id="8714e-133">In [hello first tutorial](app-service-api-dotnet-get-started.md), you created a middle tier API app and a data tier API app.</span></span> <span data-ttu-id="8714e-134">Neste tutorial você criar um aplicativo web do aplicativo de página única (SPA) esse aplicativo de camada intermediária API Olá chamadas.</span><span class="sxs-lookup"><span data-stu-id="8714e-134">In this tutorial you create a single-page application (SPA) web app that calls hello middle tier API app.</span></span> <span data-ttu-id="8714e-135">Para Olá SPA toowork tiver tooenable CORS na camada intermediária de saudação do aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="8714e-135">For hello SPA toowork you have tooenable CORS on hello middle tier API app.</span></span> 

<span data-ttu-id="8714e-136">Em Olá [aplicativo de amostra ToDoList](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), projeto de ToDoListAngular Olá é um cliente AngularJS simples que chama o projeto de API da Web de ToDoListAPI de camada intermediária hello.</span><span class="sxs-lookup"><span data-stu-id="8714e-136">In hello [ToDoList sample application](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), hello ToDoListAngular project is a simple AngularJS client that calls hello middle tier ToDoListAPI Web API project.</span></span> <span data-ttu-id="8714e-137">Olá código JavaScript em Olá *app/scripts/todoListSvc.js* arquivo chama a API de saudação usando Olá HTTP AngularJS provedor.</span><span class="sxs-lookup"><span data-stu-id="8714e-137">hello JavaScript code in hello *app/scripts/todoListSvc.js* file calls hello API by using hello AngularJS HTTP provider.</span></span> 

        angular.module('todoApp')
        .factory('todoListSvc', ['$http', function ($http) {

            $http.defaults.useXDomain = true;
            delete $http.defaults.headers.common['X-Requested-With']; 

            return {
                getItems : function(){
                    return $http.get(apiEndpoint + '/api/TodoList');
                },

                /* Get by ID, Put, and Delete methods not shown */

                postItem : function(item){
                    return $http.post(apiEndpoint + '/api/TodoList', item);
                }
            };
        }]);

### <a name="create-a-new-web-app-for-hello-todolistangular-project"></a><span data-ttu-id="8714e-138">Criar um novo aplicativo web para o projeto de ToDoListAngular Olá</span><span class="sxs-lookup"><span data-stu-id="8714e-138">Create a new web app for hello ToDoListAngular project</span></span>
<span data-ttu-id="8714e-139">Olá procedimento toocreate um novo aplicativo web do serviço de aplicativo e implantar um projeto tooit é semelhante toowhat você viu para [criando e implantando um aplicativo de API no primeiro tutorial Olá nesta série](app-service-api-dotnet-get-started.md#createapiapp).</span><span class="sxs-lookup"><span data-stu-id="8714e-139">hello procedure toocreate a new App Service web app and deploy a project tooit is similar toowhat you saw for [creating and deploying an API app in hello first tutorial in this series](app-service-api-dotnet-get-started.md#createapiapp).</span></span> <span data-ttu-id="8714e-140">Olá somente a diferença é que tipo de aplicativo hello é **aplicativo Web** em vez de **API App**.</span><span class="sxs-lookup"><span data-stu-id="8714e-140">hello only difference is that hello app type is **Web App** instead of **API App**.</span></span>  <span data-ttu-id="8714e-141">Para capturas de tela de caixas de diálogo hello, consulte</span><span class="sxs-lookup"><span data-stu-id="8714e-141">For screen shots of hello dialogs, see</span></span> 

1. <span data-ttu-id="8714e-142">Em **Solution Explorer**, clique com botão direito Olá ToDoListAngular e, em seguida, clique em **publicar**.</span><span class="sxs-lookup"><span data-stu-id="8714e-142">In **Solution Explorer**, right-click hello ToDoListAngular project, and then click **Publish**.</span></span>
2. <span data-ttu-id="8714e-143">Em Olá **perfil** guia da saudação **Publicar Web** assistente, clique em **serviço de aplicativo do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="8714e-143">In hello **Profile** tab of hello **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="8714e-144">Em Olá **do serviço de aplicativo** caixa de diálogo, clique em **novo**.</span><span class="sxs-lookup"><span data-stu-id="8714e-144">In hello **App Service** dialog box, click **New**.</span></span>
4. <span data-ttu-id="8714e-145">Em Olá **hospedagem** guia da saudação **criar serviço de aplicativo** caixa de diálogo, digite um **nome do aplicativo Web** que é exclusivo no hello *azurewebsites.net* domínio.</span><span class="sxs-lookup"><span data-stu-id="8714e-145">In hello **Hosting** tab of hello **Create App Service** dialog box, enter a **Web App Name** that is unique in hello *azurewebsites.net* domain.</span></span> 
5. <span data-ttu-id="8714e-146">Escolha hello Azure **assinatura** toowork com desejado.</span><span class="sxs-lookup"><span data-stu-id="8714e-146">Choose hello Azure **Subscription** you want toowork with.</span></span>
6. <span data-ttu-id="8714e-147">Em Olá **grupo de recursos** lista suspensa, escolha Olá mesmo grupo de recursos que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8714e-147">In hello **Resource Group** drop-down list, choose hello same resource group you created earlier.</span></span>
7. <span data-ttu-id="8714e-148">Em Olá **plano do serviço de aplicativo** lista suspensa, escolha Olá mesmo plano que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8714e-148">In hello **App Service Plan** drop-down list, choose hello same plan you created earlier.</span></span> 
8. <span data-ttu-id="8714e-149">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="8714e-149">Click **Create**.</span></span>
   
    <span data-ttu-id="8714e-150">Visual Studio cria um aplicativo da web de saudação, cria um perfil de publicação para ele e exibe o saudação **Conexão** etapa Olá **Publicar Web** assistente.</span><span class="sxs-lookup"><span data-stu-id="8714e-150">Visual Studio creates hello web app, creates a publish profile for it, and displays hello **Connection** step of hello **Publish Web** wizard.</span></span>
   
    <span data-ttu-id="8714e-151">Não clique **Publicar** ainda.</span><span class="sxs-lookup"><span data-stu-id="8714e-151">Don't click **Publish** yet.</span></span> <span data-ttu-id="8714e-152">Olá seção a seguir, você configura Olá novo aplicativo web e aplicativo toocall Olá API de camada intermediária que está em execução no serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8714e-152">In hello following section, you configure hello new web app toocall hello middle tier API app that is running in App Service.</span></span> 

### <a name="set-hello-middle-tier-url-in-web-app-settings"></a><span data-ttu-id="8714e-153">Definir a URL de camada intermediária de saudação em configurações do aplicativo web</span><span class="sxs-lookup"><span data-stu-id="8714e-153">Set hello middle tier URL in web app settings</span></span>
1. <span data-ttu-id="8714e-154">Vá toohello [portal do Azure](https://portal.azure.com/)e, em seguida, navegue toohello **aplicativo Web** folha para o aplicativo web de saudação que você criou o projeto do toohost Olá TodoListAngular (front-end).</span><span class="sxs-lookup"><span data-stu-id="8714e-154">Go toohello [Azure portal](https://portal.azure.com/), and then navigate toohello **Web App** blade for hello web app that you created toohost hello TodoListAngular (front end) project.</span></span>
2. <span data-ttu-id="8714e-155">Clique em **Configurações > Configurações do Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="8714e-155">Click **Settings > Application Settings**.</span></span>
3. <span data-ttu-id="8714e-156">Em Olá **configurações do aplicativo** seção, adicione o seguinte Olá chave e valor:</span><span class="sxs-lookup"><span data-stu-id="8714e-156">In hello **App settings** section, add hello following key and value:</span></span>
   
   | <span data-ttu-id="8714e-157">Chave</span><span class="sxs-lookup"><span data-stu-id="8714e-157">Key</span></span> | <span data-ttu-id="8714e-158">Valor</span><span class="sxs-lookup"><span data-stu-id="8714e-158">Value</span></span> | <span data-ttu-id="8714e-159">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8714e-159">Example</span></span> |
   | --- | --- | --- |
   | <span data-ttu-id="8714e-160">toDoListAPIURL</span><span class="sxs-lookup"><span data-stu-id="8714e-160">toDoListAPIURL</span></span> |<span data-ttu-id="8714e-161">https://{nome de aplicativo de API de tipo médio}.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="8714e-161">https://{your middle tier API app name}.azurewebsites.net</span></span> |<span data-ttu-id="8714e-162">https://todolistapi0121.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="8714e-162">https://todolistapi0121.azurewebsites.net</span></span> |
4. <span data-ttu-id="8714e-163">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="8714e-163">Click **Save**.</span></span>
   
    <span data-ttu-id="8714e-164">Quando o código de saudação é executado no Azure, esse valor substitui Olá localhost URL que está em Olá *Web. config* arquivo.</span><span class="sxs-lookup"><span data-stu-id="8714e-164">When hello code runs in Azure, this value overrides hello localhost URL that is in hello *Web.config* file.</span></span> 
   
    <span data-ttu-id="8714e-165">Olá código obtém o valor da configuração hello está em *cshtml*:</span><span class="sxs-lookup"><span data-stu-id="8714e-165">hello code that gets hello setting value is in *index.cshtml*:</span></span>
   
        <script type="text/javascript">
            var apiEndpoint = "@System.Configuration.ConfigurationManager.AppSettings["toDoListAPIURL"]";
        </script>
        <script src="app/scripts/todoListSvc.js"></script>
   
    <span data-ttu-id="8714e-166">Olá código *todoListSvc.js* usa a configuração de saudação:</span><span class="sxs-lookup"><span data-stu-id="8714e-166">hello code in *todoListSvc.js* uses hello setting:</span></span>
   
        return {
            getItems : function(){
                return $http.get(apiEndpoint + '/api/TodoList');
            },
            getItem : function(id){
                return $http.get(apiEndpoint + '/api/TodoList/' + id);
            },
            postItem : function(item){
                return $http.post(apiEndpoint + '/api/TodoList', item);
            },
            putItem : function(item){
                return $http.put(apiEndpoint + '/api/TodoList/', item);
            },
            deleteItem : function(id){
                return $http({
                    method: 'DELETE',
                    url: apiEndpoint + '/api/TodoList/' + id
                });
            }
        };

### <a name="deploy-hello-todolistangular-web-project-toohello-new-web-app"></a><span data-ttu-id="8714e-167">Implantar Olá ToDoListAngular web projeto toohello novo aplicativo web</span><span class="sxs-lookup"><span data-stu-id="8714e-167">Deploy hello ToDoListAngular web project toohello new web app</span></span>
* <span data-ttu-id="8714e-168">No Visual Studio, no hello **Conexão** etapa Olá **Publicar Web** assistente, clique em **publicar**.</span><span class="sxs-lookup"><span data-stu-id="8714e-168">In Visual Studio, in hello **Connection** step of hello **Publish Web** wizard, click **Publish**.</span></span>
  
   <span data-ttu-id="8714e-169">Visual Studio implanta Olá ToDoListAngular projeto toohello novo aplicativo web e abre uma URL de toohello do navegador do aplicativo web de saudação.</span><span class="sxs-lookup"><span data-stu-id="8714e-169">Visual Studio deploys hello ToDoListAngular project toohello new web app and opens a browser toohello URL of hello web app.</span></span> 

### <a name="test-hello-application-without-cors-enabled"></a><span data-ttu-id="8714e-170">Testar o aplicativo hello sem CORS habilitado</span><span class="sxs-lookup"><span data-stu-id="8714e-170">Test hello application without CORS enabled</span></span>
1. <span data-ttu-id="8714e-171">Em seu navegador, ferramentas de desenvolvedor, abra a janela de Console de saudação.</span><span class="sxs-lookup"><span data-stu-id="8714e-171">In your browser Developer Tools, open hello Console window.</span></span>
2. <span data-ttu-id="8714e-172">Na janela de navegador Olá que exibe o saudação AngularJS UI, clique em Olá **tooDo lista** link.</span><span class="sxs-lookup"><span data-stu-id="8714e-172">In hello browser window that displays hello AngularJS UI, click hello **tooDo List** link.</span></span>
   
    <span data-ttu-id="8714e-173">Olá código JavaScript tenta toocall Olá intermediária da camada de aplicativo de API, mas chamada hello falha porque front-end hello está sendo executado em um domínio diferente Olá volta final.</span><span class="sxs-lookup"><span data-stu-id="8714e-173">hello JavaScript code tries toocall hello middle tier API app, but hello call fails because hello front end is running in a different domain than hello back end.</span></span> <span data-ttu-id="8714e-174">janela de Console de ferramentas de desenvolvedor do navegador Olá mostra uma mensagem de erro entre origens.</span><span class="sxs-lookup"><span data-stu-id="8714e-174">hello browser's Developer Tools Console window shows a cross-origin error message.</span></span>
   
    ![Mensagem de erro entre origens](./media/app-service-api-cors-consume-javascript/consoleaccessdenied.png)

## <a name="configure-cors-for-hello-middle-tier-api-app"></a><span data-ttu-id="8714e-176">Configurar CORS para a camada intermediária de saudação do aplicativo de API</span><span class="sxs-lookup"><span data-stu-id="8714e-176">Configure CORS for hello middle tier API app</span></span>
<span data-ttu-id="8714e-177">Nesta seção, você configurar Olá CORS no Azure para a camada intermediária de saudação do aplicativo de API ToDoListAPI.</span><span class="sxs-lookup"><span data-stu-id="8714e-177">In this section, you configure hello CORS setting in Azure for hello middle tier ToDoListAPI API app.</span></span> <span data-ttu-id="8714e-178">Essa configuração permitirá Olá camada intermediária aplicativo tooreceive JavaScript chamadas de API do aplicativo web hello que você criou para o projeto de ToDoListAngular hello.</span><span class="sxs-lookup"><span data-stu-id="8714e-178">This setting will allow hello middle tier API app tooreceive JavaScript calls from hello web app that you created for hello ToDoListAngular project.</span></span>

1. <span data-ttu-id="8714e-179">Em um navegador, vá toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8714e-179">In a browser, go toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="8714e-180">Clique em **serviços de aplicativos**e, em seguida, clique em aplicativo hello API ToDoListAPI (camada intermediária).</span><span class="sxs-lookup"><span data-stu-id="8714e-180">Click **App Services**, and then click hello ToDoListAPI (middle tier) API app.</span></span>
   
    ![Selecione o aplicativo de API no portal](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. <span data-ttu-id="8714e-182">Em Olá **configurações** folha que abre toohello direito da saudação **aplicativo de API** folha, localizar Olá **API** seção e, em seguida, clique em **CORS**.</span><span class="sxs-lookup"><span data-stu-id="8714e-182">In hello **Settings** blade that opens toohello right of hello **API app** blade, find hello **API** section, and then click **CORS**.</span></span>
   
   ![Selecione CORS no portal](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. <span data-ttu-id="8714e-184">Na caixa de texto de saudação, insira a URL de saudação do aplicativo de web hello ToDoListAngular (front-end).</span><span class="sxs-lookup"><span data-stu-id="8714e-184">In hello text box, enter hello URL for hello ToDoListAngular (front end) web app.</span></span> <span data-ttu-id="8714e-185">Por exemplo, se você implantou o aplicativo hello ToDoListAngular projeto tooa web chamado todolistangular0121, permitir chamadas no URL Olá `https://todolistangular0121.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="8714e-185">For example, if you deployed hello ToDoListAngular project tooa web app named todolistangular0121, allow calls from hello URL `https://todolistangular0121.azurewebsites.net`.</span></span>
   
   <span data-ttu-id="8714e-186">Como alternativa, você pode inserir um toospecify de asterisco (*) que todos os domínios de origem são aceitos.</span><span class="sxs-lookup"><span data-stu-id="8714e-186">As an alternative, you can enter an asterisk (*) toospecify that all origin domains are accepted.</span></span>
5. <span data-ttu-id="8714e-187">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="8714e-187">Click **Save**.</span></span>
   
   ![Clique em Salvar](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   <span data-ttu-id="8714e-189">Depois de clicar em **salvar**, aplicativo hello API aceitará JavaScript chamadas de saudação especificou a URL.</span><span class="sxs-lookup"><span data-stu-id="8714e-189">After you click **Save**, hello API app will accept JavaScript calls from hello specified URL.</span></span> <span data-ttu-id="8714e-190">Na captura de tela, aplicativo de API ToDoListAPI0223 Olá aceitará chamadas de cliente JavaScript do aplicativo de web ToDoListAngular hello.</span><span class="sxs-lookup"><span data-stu-id="8714e-190">In this screen shot, hello ToDoListAPI0223 API app will accept JavaScript client calls from hello ToDoListAngular web app.</span></span>

### <a name="test-hello-application-with-cors-enabled"></a><span data-ttu-id="8714e-191">Testar o aplicativo hello com CORS habilitado</span><span class="sxs-lookup"><span data-stu-id="8714e-191">Test hello application with CORS enabled</span></span>
* <span data-ttu-id="8714e-192">Abra um navegador toohello HTTPS URL do aplicativo web de saudação.</span><span class="sxs-lookup"><span data-stu-id="8714e-192">Open a browser toohello HTTPS URL of hello web app.</span></span> 
  
    <span data-ttu-id="8714e-193">Este aplicativo de saudação do tempo permite exibir, adicionar, editar e excluir itens de tarefas pendentes.</span><span class="sxs-lookup"><span data-stu-id="8714e-193">This time hello application lets you view, add, edit, and delete to-do items.</span></span> 
  
    ![página de lista de tooDo do aplicativo de exemplo](./media/app-service-api-cors-consume-javascript/corssuccess.png)

## <a name="app-service-cors-versus-web-api-cors"></a><span data-ttu-id="8714e-195">CORS do Serviço de Aplicativo versus CORS da API Web</span><span class="sxs-lookup"><span data-stu-id="8714e-195">App Service CORS versus Web API CORS</span></span>
<span data-ttu-id="8714e-196">Em um projeto de API da Web, você pode instalar Olá [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) toospecify de pacote do NuGet no código que domínios sua API aceitará o JavaScript chama de.</span><span class="sxs-lookup"><span data-stu-id="8714e-196">In a Web API project, you can install hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet package toospecify in code which domains your API will accept JavaScript calls from.</span></span>

<span data-ttu-id="8714e-197">O suporte a CORS da API Web é mais flexível do que o suporte a CORS do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8714e-197">Web API CORS support is more flexible than App Service CORS support.</span></span> <span data-ttu-id="8714e-198">Por exemplo, você pode especificar no código diferentes origens aceitas para diferentes métodos de ação, enquanto para o CORS do Serviço de Aplicativo, você especifica um conjunto de origens aceitas para todos os métodos do aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="8714e-198">For example, in code you can specify different accepted origins for different action methods, while for App Service CORS you specify one set of accepted origins for all of an API app's methods.</span></span>

> [!NOTE]
> <span data-ttu-id="8714e-199">Não tente toouse CORS da API da Web e CORS de serviço de aplicativo em um aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="8714e-199">Don't try toouse both Web API CORS and App Service CORS in one API app.</span></span> <span data-ttu-id="8714e-200">O CORS do Serviço de Aplicativo terá a precedência e o CORS da API Web não funcionará.</span><span class="sxs-lookup"><span data-stu-id="8714e-200">App Service CORS will take precedence and Web API CORS will have no effect.</span></span> <span data-ttu-id="8714e-201">Por exemplo, se você habilitar um domínio de origem no serviço de aplicativo e habilitar todos os domínios de origem em seu código de API da Web, seu aplicativo de API do Azure só aceitará chamadas de domínio Olá especificado no Azure.</span><span class="sxs-lookup"><span data-stu-id="8714e-201">For example, if you enable one origin domain in App Service, and enable all origin domains in your Web API code, your Azure API app will only accept calls from hello domain you specified in Azure.</span></span>
> 
> 

### <a name="how-tooenable-cors-in-web-api-code"></a><span data-ttu-id="8714e-202">Como tooenable CORS no código da API da Web</span><span class="sxs-lookup"><span data-stu-id="8714e-202">How tooenable CORS in Web API code</span></span>
<span data-ttu-id="8714e-203">Olá etapas a seguir resumem processo Olá para habilitar o suporte de CORS da API da Web.</span><span class="sxs-lookup"><span data-stu-id="8714e-203">hello following steps summarize hello process for enabling Web API CORS support.</span></span> <span data-ttu-id="8714e-204">Para saber mais, confira [Permitindo solicitações entre origens na API Web ASP.NET 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).</span><span class="sxs-lookup"><span data-stu-id="8714e-204">For more information, see [Enabling Cross-Origin Requests in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).</span></span>

1. <span data-ttu-id="8714e-205">Em um projeto de API da Web, instale o hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="8714e-205">In a Web API project, install hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet package.</span></span>
2. <span data-ttu-id="8714e-206">Incluir um `config.EnableCors()` linha de código em Olá **registrar** método hello **WebApiConfig** classe, como no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="8714e-206">Include a `config.EnableCors()` line of code in hello **Register** method of hello **WebApiConfig** class, as in hello following example.</span></span> 
   
        public static class WebApiConfig
        {
            public static void Register(HttpConfiguration config)
            {
                // Web API configuration and services
   
                // hello following line enables you toocontrol CORS by using Web API code
                config.EnableCors();
   
                // Web API routes
                config.MapHttpAttributeRoutes();
   
                config.Routes.MapHttpRoute(
                    name: "DefaultApi",
                    routeTemplate: "api/{controller}/{id}",
                    defaults: new { id = RouteParameter.Optional }
                );
            }
        }
3. <span data-ttu-id="8714e-207">No controlador de API da Web, adicione um `using` instrução Olá `System.Web.Http.Cors` namespace e adicione Olá `EnableCors` métodos de ação toohello controlador tooindividual ou classe de atributo.</span><span class="sxs-lookup"><span data-stu-id="8714e-207">In your Web API controller, add a `using` statement for hello `System.Web.Http.Cors` namespace, and add hello `EnableCors` attribute toohello controller class or tooindividual action methods.</span></span> <span data-ttu-id="8714e-208">Olá exemplo a seguir, o suporte de CORS aplica-se controlador todo toohello.</span><span class="sxs-lookup"><span data-stu-id="8714e-208">In hello following example, CORS support applies toohello entire controller.</span></span>
   
        namespace ToDoListAPI.Controllers 
        {
            [HttpOperationExceptionFilterAttribute]
            [EnableCors(origins:"https://todolistangular0121.azurewebsites.net", headers:"accept,content-type,origin,x-my-header", methods: "get,post")]
            public class ToDoListController : ApiController

## <a name="using-azure-api-management-with-api-apps"></a><span data-ttu-id="8714e-209">Uso do Gerenciamento de API com Aplicativos de API</span><span class="sxs-lookup"><span data-stu-id="8714e-209">Using Azure API Management with API Apps</span></span>
<span data-ttu-id="8714e-210">Se você usar o gerenciamento de API do Azure com um aplicativo de API, configure CORS no gerenciamento de API em vez de no aplicativo de API de saudação.</span><span class="sxs-lookup"><span data-stu-id="8714e-210">If you use Azure API Management with an API app, configure CORS in API Management instead of in hello API app.</span></span> <span data-ttu-id="8714e-211">Para obter mais informações, consulte Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="8714e-211">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="8714e-212">Visão geral do Gerenciamento de API do Azure (vídeo: CORS começa em 12:10)</span><span class="sxs-lookup"><span data-stu-id="8714e-212">Azure API Management Overview (video: CORS starts at 12:10)</span></span>](https://azure.microsoft.com/documentation/videos/azure-api-management-overview/)
* [<span data-ttu-id="8714e-213">Políticas entre domínios de Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="8714e-213">API Management cross domain policies</span></span>](https://msdn.microsoft.com/library/azure/dn894084.aspx#CORS)

## <a name="troubleshooting"></a><span data-ttu-id="8714e-214">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="8714e-214">Troubleshooting</span></span>
<span data-ttu-id="8714e-215">Caso você encontre um problema ao percorrer este tutorial, aqui estão algumas ideias para solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="8714e-215">In case you run into a problem while going through this tutorial, here are some troubleshooting ideas.</span></span>

* <span data-ttu-id="8714e-216">Certifique-se de que você está usando a versão mais recente de saudação do hello [SDK do Azure para .NET para Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="8714e-216">Make sure that you're using hello latest version of hello [Azure SDK for .NET for Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).</span></span>
* <span data-ttu-id="8714e-217">Certifique-se de que você inseriu `https` Olá configuração CORS e certifique-se de que você está usando `https` toorun Olá web front-end aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8714e-217">Make sure that you entered `https` in hello CORS setting, and make sure that you're using `https` toorun hello front-end web app.</span></span>
* <span data-ttu-id="8714e-218">Certifique-se de que você inseriu uma configuração de CORS saudação no aplicativo de API de camada intermediária hello, não no aplicativo da web front-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="8714e-218">Make sure that you entered hello CORS setting in hello middle tier API app, not in hello front-end web app.</span></span>
* <span data-ttu-id="8714e-219">Se você estiver configurando CORS no código do aplicativo e serviço de aplicativo do Azure, observe que configuração de CORS de serviço de aplicativo hello substituirá o que você está fazendo no código do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8714e-219">If you're configuring CORS in both application code and Azure App Service, note that hello App Service CORS setting will override whatever you're doing in application code.</span></span> 

<span data-ttu-id="8714e-220">toolearn mais sobre os recursos do Visual Studio que simplificam a solução de problemas, consulte [aplicativos de solução de problemas do serviço de aplicativo do Azure no Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="8714e-220">toolearn more about Visual Studio features that simplify troubleshooting, see [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8714e-221">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8714e-221">Next steps</span></span>
<span data-ttu-id="8714e-222">Neste artigo, você viu como tooenable CORS de serviço de aplicativo compatível para que o código JavaScript cliente possa chamar uma API em um domínio diferente.</span><span class="sxs-lookup"><span data-stu-id="8714e-222">In this article, you saw how tooenable App Service CORS support so that client JavaScript code can call an API in a different domain.</span></span> <span data-ttu-id="8714e-223">toolearn mais sobre aplicativos de API, ler Olá [tooauthentication de Introdução no serviço de aplicativo](../app-service/app-service-authentication-overview.md), e em seguida, acesse toohello [autenticação de usuário para aplicativos de API](app-service-api-dotnet-user-principal-auth.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="8714e-223">toolearn more about API apps, read hello [introduction tooauthentication in App Service](../app-service/app-service-authentication-overview.md), and then go toohello [user authentication for API apps](app-service-api-dotnet-user-principal-auth.md) tutorial.</span></span>

