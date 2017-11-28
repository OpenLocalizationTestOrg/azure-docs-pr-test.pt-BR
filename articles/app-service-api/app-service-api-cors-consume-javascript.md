---
title: "Suporte a CORS no Serviço de Aplicativo | Microsoft Docs"
description: "Saiba como usar o suporte a CORS no Serviço de Aplicativo do Azure."
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
ms.openlocfilehash: f8373cf5b2e06e6c71bce51cd9e9d5123eea7cfd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="consume-an-api-app-from-javascript-using-cors"></a><span data-ttu-id="027c6-103">Consumir um aplicativo de API do JavaScript usando CORS</span><span class="sxs-lookup"><span data-stu-id="027c6-103">Consume an API app from JavaScript using CORS</span></span>
<span data-ttu-id="027c6-104">O Serviço de Aplicativo oferece suporte interno para [CORS (Compartilhamento de Recursos Entre Origens)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), que habilita os clientes JavaScript a fazer chamadas entre domínios para APIs que estão hospedadas em aplicativos de API.</span><span class="sxs-lookup"><span data-stu-id="027c6-104">App Service offers built-in support for [Cross Origin Resource Sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), which enables JavaScript clients to make cross-domain calls to APIs that are hosted in API apps.</span></span> <span data-ttu-id="027c6-105">O Serviço de Aplicativo permite configurar o acesso ao CORS para a API sem escrever código na API.</span><span class="sxs-lookup"><span data-stu-id="027c6-105">App Service lets you configure CORS access to your API without writing any code in your API.</span></span>

<span data-ttu-id="027c6-106">Este artigo contém duas seções:</span><span class="sxs-lookup"><span data-stu-id="027c6-106">This article contains two sections:</span></span>

* <span data-ttu-id="027c6-107">A seção [Como configurar o CORS](#corsconfig) explica de forma geral como configurar o CORS para qualquer aplicativo de API, aplicativo Web ou aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="027c6-107">The [How to configure CORS](#corsconfig) section explains in general how to configure CORS for any API app, web app, or mobile app.</span></span> <span data-ttu-id="027c6-108">Ela se aplica igualmente a todas as estruturas às quais o Serviço de Aplicativo dá suporte, incluindo .NET, Node.js e Java.</span><span class="sxs-lookup"><span data-stu-id="027c6-108">It applies equally to all frameworks that are supported by App Service, including .NET, Node.js, and Java.</span></span> 
* <span data-ttu-id="027c6-109">Começando pela seção [Continuação dos tutoriais de Introdução ao .NET](#tutorialstart), o artigo é um tutorial que demonstra o suporte a CORS com base no que você fez no [primeiro tutorial de Introdução a aplicativos de API](app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="027c6-109">Starting with the [Continuing the .NET getting-started tutorials](#tutorialstart) section, the article is a tutorial that demonstrates CORS support by building on what you did in [the first API Apps getting started tutorial](app-service-api-dotnet-get-started.md).</span></span> 

## <span data-ttu-id="027c6-110"><a id="corsconfig"></a> Como configurar CORS no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="027c6-110"><a id="corsconfig"></a> How to configure CORS in Azure App Service</span></span>
<span data-ttu-id="027c6-111">Você pode configurar o CORS no portal do Azure ou usando as ferramentas do [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="027c6-111">You can configure CORS in the Azure portal or by using [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) tools.</span></span>

#### <a name="configure-cors-in-the-azure-portal"></a><span data-ttu-id="027c6-112">Configurar CORS no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="027c6-112">Configure CORS in the Azure portal</span></span>
1. <span data-ttu-id="027c6-113">Em um navegador, acesse o [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="027c6-113">In a browser go to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="027c6-114">Clique em **Serviços de Aplicativos**e clique no nome do aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="027c6-114">Click **App Services**, and then click the name of your API app.</span></span>
   
    ![Selecione o aplicativo de API no portal](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. <span data-ttu-id="027c6-116">Na folha **Configurações** que abre à direita da folha **Aplicativo de API**, encontre a seção **API** e clique em **CORS**.</span><span class="sxs-lookup"><span data-stu-id="027c6-116">In the **Settings** blade that opens to the right of the **API app** blade, find the **API** section, and then click **CORS**.</span></span>
   
   ![Selecione CORS na folha configurações](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. <span data-ttu-id="027c6-118">Na caixa de texto, insira a URL ou as URLs das quais você deseja permitir chamadas JavaScript.</span><span class="sxs-lookup"><span data-stu-id="027c6-118">In the text box enter the URL or URLs that you want to allow JavaScript calls to come from.</span></span>

    <span data-ttu-id="027c6-119">Por exemplo, se você implantou o aplicativo JavaScript para um aplicativo Web chamado todolistangular, digite "https://todolistangular.azurewebsites.net".</span><span class="sxs-lookup"><span data-stu-id="027c6-119">For example, if you deployed your JavaScript application to a web app named todolistangular, enter "https://todolistangular.azurewebsites.net".</span></span> <span data-ttu-id="027c6-120">Como alternativa, você pode inserir um asterisco (*) para especificar que todos os domínios de origem são aceitos.</span><span class="sxs-lookup"><span data-stu-id="027c6-120">As an alternative, you can enter an asterisk (*) to specify that all origin domains are accepted.</span></span>


1. <span data-ttu-id="027c6-121">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="027c6-121">Click **Save**.</span></span>
   
   ![Clique em Salvar](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   <span data-ttu-id="027c6-123">Depois que você clicar em **Salvar**, o aplicativo de API aceitará chamadas JavaScript das URLs especificadas.</span><span class="sxs-lookup"><span data-stu-id="027c6-123">After you click **Save**, the API app will accept JavaScript calls from the specified URLs.</span></span>

#### <a name="configure-cors-by-using-azure-resource-manager-tools"></a><span data-ttu-id="027c6-124">Configurar CORS usando as ferramentas do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="027c6-124">Configure CORS by using Azure Resource Manager tools</span></span>
<span data-ttu-id="027c6-125">Você também pode configurar o CORS para um aplicativo de API usando os [modelos do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) em ferramentas de linha de comando, como o [Azure PowerShell](/powershell/azureps-cmdlets-docs) e a [CLI do Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="027c6-125">You can also configure CORS for an API app by using [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) in command line tools such as [Azure PowerShell](/powershell/azureps-cmdlets-docs) and the [Azure CLI](../cli-install-nodejs.md).</span></span> 

<span data-ttu-id="027c6-126">Para ver um exemplo de um modelo do Azure Resource Manager que define a propriedade do CORS, abra o [arquivo azuredeploy.json no repositório do aplicativo de exemplo deste tutorial](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="027c6-126">For an example of an Azure Resource Manager template that sets the CORS property, open the [azuredeploy.json file in the repository for this tutorial's sample application](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json).</span></span> <span data-ttu-id="027c6-127">Localize a seção do modelo que se parece com o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="027c6-127">Find the section of the template that looks like the following example:</span></span>

        "cors": {
            "allowedOrigins": [
                "todolistangular.azurewebsites.net"
            ]
        }

## <span data-ttu-id="027c6-128"><a id="tutorialstart"></a> Continuação do tutorial de introdução do .NET</span><span class="sxs-lookup"><span data-stu-id="027c6-128"><a id="tutorialstart"></a> Continuing the .NET getting-started tutorial</span></span>
<span data-ttu-id="027c6-129">Se está seguindo a série de introdução do Node.js ou do Java para aplicativos de API, você concluiu a série de introdução.</span><span class="sxs-lookup"><span data-stu-id="027c6-129">If you are following the Node.js or Java getting-started series for API apps, you have completed the getting started series.</span></span> <span data-ttu-id="027c6-130">Vá para a seção [Próximas etapas](#next-steps) para obter sugestões e saber mais sobre aplicativos de API.</span><span class="sxs-lookup"><span data-stu-id="027c6-130">Skip to the [Next steps](#next-steps) section to find suggestions for further learning about API Apps.</span></span>

<span data-ttu-id="027c6-131">O restante deste artigo é uma continuação da série de introdução do .NET e pressupõe que você tenha concluído com êxito [o primeiro tutorial](app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="027c6-131">The remainder of this article is a continuation of the .NET getting-started series and assumes that you successfully completed [the first tutorial](app-service-api-dotnet-get-started.md).</span></span>

## <a name="deploy-the-todolistangular-project-to-a-new-web-app"></a><span data-ttu-id="027c6-132">Implantar o projeto ToDoListAngular para um novo aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="027c6-132">Deploy the ToDoListAngular project to a new web app</span></span>
<span data-ttu-id="027c6-133">No [primeiro tutorial](app-service-api-dotnet-get-started.md), você criou um aplicativo de API de camada intermediária e um aplicativo de API da camada de dados.</span><span class="sxs-lookup"><span data-stu-id="027c6-133">In [the first tutorial](app-service-api-dotnet-get-started.md), you created a middle tier API app and a data tier API app.</span></span> <span data-ttu-id="027c6-134">Neste tutorial, você criará um aplicativo Web SPA (aplicativo de página única) que chama o aplicativo de API de camada intermediária.</span><span class="sxs-lookup"><span data-stu-id="027c6-134">In this tutorial you create a single-page application (SPA) web app that calls the middle tier API app.</span></span> <span data-ttu-id="027c6-135">Para que o SPA funcione, você terá que habilitar CORS no aplicativo de API de camada intermediária.</span><span class="sxs-lookup"><span data-stu-id="027c6-135">For the SPA to work you have to enable CORS on the middle tier API app.</span></span> 

<span data-ttu-id="027c6-136">No [aplicativo de exemplo ToDoList](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), o projeto ToDoListAngular é um cliente do AngularJS simples que chama o projeto de API Web ToDoListAPI de camada intermediária.</span><span class="sxs-lookup"><span data-stu-id="027c6-136">In the [ToDoList sample application](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), the ToDoListAngular project is a simple AngularJS client that calls the middle tier ToDoListAPI Web API project.</span></span> <span data-ttu-id="027c6-137">O código JavaScript no arquivo *app/scripts/todoListSvc.js* chama a API usando o provedor HTTP do AngularJS.</span><span class="sxs-lookup"><span data-stu-id="027c6-137">The JavaScript code in the *app/scripts/todoListSvc.js* file calls the API by using the AngularJS HTTP provider.</span></span> 

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

### <a name="create-a-new-web-app-for-the-todolistangular-project"></a><span data-ttu-id="027c6-138">Criar um novo aplicativo Web para o projeto ToDoListAngular</span><span class="sxs-lookup"><span data-stu-id="027c6-138">Create a new web app for the ToDoListAngular project</span></span>
<span data-ttu-id="027c6-139">O procedimento para criar um novo aplicativo Web do Serviço de Aplicativo e implantar um projeto nele é semelhante ao que você viu em [criar e implantar um aplicativo de API no primeiro tutorial nesta série](app-service-api-dotnet-get-started.md#createapiapp).</span><span class="sxs-lookup"><span data-stu-id="027c6-139">The procedure to create a new App Service web app and deploy a project to it is similar to what you saw for [creating and deploying an API app in the first tutorial in this series](app-service-api-dotnet-get-started.md#createapiapp).</span></span> <span data-ttu-id="027c6-140">A única diferença é que o tipo de aplicativo é **aplicativo Web** em vez de **aplicativo de API**.</span><span class="sxs-lookup"><span data-stu-id="027c6-140">The only difference is that the app type is **Web App** instead of **API App**.</span></span>  <span data-ttu-id="027c6-141">Para obter capturas de tela das caixas de diálogo, confira</span><span class="sxs-lookup"><span data-stu-id="027c6-141">For screen shots of the dialogs, see</span></span> 

1. <span data-ttu-id="027c6-142">No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto ToDoListAngular e em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="027c6-142">In **Solution Explorer**, right-click the ToDoListAngular project, and then click **Publish**.</span></span>
2. <span data-ttu-id="027c6-143">Na etapa **Perfil** do assistente **Publicar na Web**, clique em **Serviço de Aplicativo do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="027c6-143">In the **Profile** tab of the **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="027c6-144">Na caixa de diálogo **Serviço de Aplicativo**, clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="027c6-144">In the **App Service** dialog box, click **New**.</span></span>
4. <span data-ttu-id="027c6-145">Na guia **Hospedagem** da caixa de diálogo **Criar Serviço de Aplicativo**, insira um **Nome de Aplicativo Web** que seja exclusivo no domínio *azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="027c6-145">In the **Hosting** tab of the **Create App Service** dialog box, enter a **Web App Name** that is unique in the *azurewebsites.net* domain.</span></span> 
5. <span data-ttu-id="027c6-146">Escolha a **Assinatura** do Azure com a qual você deseja trabalhar.</span><span class="sxs-lookup"><span data-stu-id="027c6-146">Choose the Azure **Subscription** you want to work with.</span></span>
6. <span data-ttu-id="027c6-147">Na lista suspensa **Grupo de Recursos** , escolha o mesmo grupo de recursos que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="027c6-147">In the **Resource Group** drop-down list, choose the same resource group you created earlier.</span></span>
7. <span data-ttu-id="027c6-148">Na lista suspensa **Plano do Serviço de Aplicativo** , escolha o mesmo plano criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="027c6-148">In the **App Service Plan** drop-down list, choose the same plan you created earlier.</span></span> 
8. <span data-ttu-id="027c6-149">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="027c6-149">Click **Create**.</span></span>
   
    <span data-ttu-id="027c6-150">O Visual Studio cria o aplicativo Web, cria um perfil de publicação para ele e exibe a etapa **Conexão** do assistente **Publicar na Web**.</span><span class="sxs-lookup"><span data-stu-id="027c6-150">Visual Studio creates the web app, creates a publish profile for it, and displays the **Connection** step of the **Publish Web** wizard.</span></span>
   
    <span data-ttu-id="027c6-151">Não clique **Publicar** ainda.</span><span class="sxs-lookup"><span data-stu-id="027c6-151">Don't click **Publish** yet.</span></span> <span data-ttu-id="027c6-152">Na seção seguinte, você configurará o novo aplicativo Web para chamar o aplicativo de API de camada intermediária que está em execução no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="027c6-152">In the following section, you configure the new web app to call the middle tier API app that is running in App Service.</span></span> 

### <a name="set-the-middle-tier-url-in-web-app-settings"></a><span data-ttu-id="027c6-153">Definir a URL de camada intermediária nas configurações do aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="027c6-153">Set the middle tier URL in web app settings</span></span>
1. <span data-ttu-id="027c6-154">Vá para o [portal do Azure](https://portal.azure.com/)e navegue até a folha **Aplicativo Web** do aplicativo Web que você criou para hospedar o projeto TodoListAngular (front-end).</span><span class="sxs-lookup"><span data-stu-id="027c6-154">Go to the [Azure portal](https://portal.azure.com/), and then navigate to the **Web App** blade for the web app that you created to host the TodoListAngular (front end) project.</span></span>
2. <span data-ttu-id="027c6-155">Clique em **Configurações > Configurações do Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="027c6-155">Click **Settings > Application Settings**.</span></span>
3. <span data-ttu-id="027c6-156">Na seção **Configurações do aplicativo** , adicione a chave e o valor a seguir:</span><span class="sxs-lookup"><span data-stu-id="027c6-156">In the **App settings** section, add the following key and value:</span></span>
   
   | <span data-ttu-id="027c6-157">Chave</span><span class="sxs-lookup"><span data-stu-id="027c6-157">Key</span></span> | <span data-ttu-id="027c6-158">Valor</span><span class="sxs-lookup"><span data-stu-id="027c6-158">Value</span></span> | <span data-ttu-id="027c6-159">Exemplo</span><span class="sxs-lookup"><span data-stu-id="027c6-159">Example</span></span> |
   | --- | --- | --- |
   | <span data-ttu-id="027c6-160">toDoListAPIURL</span><span class="sxs-lookup"><span data-stu-id="027c6-160">toDoListAPIURL</span></span> |<span data-ttu-id="027c6-161">https://{nome de aplicativo de API de tipo médio}.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="027c6-161">https://{your middle tier API app name}.azurewebsites.net</span></span> |<span data-ttu-id="027c6-162">https://todolistapi0121.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="027c6-162">https://todolistapi0121.azurewebsites.net</span></span> |
4. <span data-ttu-id="027c6-163">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="027c6-163">Click **Save**.</span></span>
   
    <span data-ttu-id="027c6-164">Quando o código for executado no Azure, esse valor substituirá a URL de localhost no arquivo *Web.config* .</span><span class="sxs-lookup"><span data-stu-id="027c6-164">When the code runs in Azure, this value overrides the localhost URL that is in the *Web.config* file.</span></span> 
   
    <span data-ttu-id="027c6-165">O código que obtém o valor de configuração está em *index.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="027c6-165">The code that gets the setting value is in *index.cshtml*:</span></span>
   
        <script type="text/javascript">
            var apiEndpoint = "@System.Configuration.ConfigurationManager.AppSettings["toDoListAPIURL"]";
        </script>
        <script src="app/scripts/todoListSvc.js"></script>
   
    <span data-ttu-id="027c6-166">O código em *todoListSvc.js* usa a configuração:</span><span class="sxs-lookup"><span data-stu-id="027c6-166">The code in *todoListSvc.js* uses the setting:</span></span>
   
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

### <a name="deploy-the-todolistangular-web-project-to-the-new-web-app"></a><span data-ttu-id="027c6-167">Implantar o projeto da Web ToDoListAngular no novo aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="027c6-167">Deploy the ToDoListAngular web project to the new web app</span></span>
* <span data-ttu-id="027c6-168">No Visual Studio, na etapa **Conexão** do assistente **Publicar na Web**, clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="027c6-168">In Visual Studio, in the **Connection** step of the **Publish Web** wizard, click **Publish**.</span></span>
  
   <span data-ttu-id="027c6-169">O Visual Studio implanta o projeto ToDoListAngular no novo aplicativo Web e abre um navegador para a URL do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="027c6-169">Visual Studio deploys the ToDoListAngular project to the new web app and opens a browser to the URL of the web app.</span></span> 

### <a name="test-the-application-without-cors-enabled"></a><span data-ttu-id="027c6-170">Testar o aplicativo sem CORS habilitado</span><span class="sxs-lookup"><span data-stu-id="027c6-170">Test the application without CORS enabled</span></span>
1. <span data-ttu-id="027c6-171">Nas Ferramentas de Desenvolvedor do navegador, abra a janela Console.</span><span class="sxs-lookup"><span data-stu-id="027c6-171">In your browser Developer Tools, open the Console window.</span></span>
2. <span data-ttu-id="027c6-172">Na janela do navegador que exibe a interface do usuário AngularJS, clique no link **Lista de Tarefas Pendentes** .</span><span class="sxs-lookup"><span data-stu-id="027c6-172">In the browser window that displays the AngularJS UI, click the **To Do List** link.</span></span>
   
    <span data-ttu-id="027c6-173">O código JavaScript tenta chamar o aplicativo de API de camada intermediária, mas a chamada falhará porque o front-end está em execução em um domínio diferente do back-end.</span><span class="sxs-lookup"><span data-stu-id="027c6-173">The JavaScript code tries to call the middle tier API app, but the call fails because the front end is running in a different domain than the back end.</span></span> <span data-ttu-id="027c6-174">A janela Console de Ferramentas de Desenvolvedor do navegador mostra uma mensagem de erro entre origens.</span><span class="sxs-lookup"><span data-stu-id="027c6-174">The browser's Developer Tools Console window shows a cross-origin error message.</span></span>
   
    ![Mensagem de erro entre origens](./media/app-service-api-cors-consume-javascript/consoleaccessdenied.png)

## <a name="configure-cors-for-the-middle-tier-api-app"></a><span data-ttu-id="027c6-176">Configure o CORS para o aplicativo de API de camada intermediária</span><span class="sxs-lookup"><span data-stu-id="027c6-176">Configure CORS for the middle tier API app</span></span>
<span data-ttu-id="027c6-177">Nesta seção, você define a configuração de CORS no Azure para o aplicativo de API ToDoListAPI de camada intermediária.</span><span class="sxs-lookup"><span data-stu-id="027c6-177">In this section, you configure the CORS setting in Azure for the middle tier ToDoListAPI API app.</span></span> <span data-ttu-id="027c6-178">Essa configuração permitirá que o aplicativo de API de camada intermediária receba chamadas JavaScript do aplicativo Web que você criou para o projeto ToDoListAngular.</span><span class="sxs-lookup"><span data-stu-id="027c6-178">This setting will allow the middle tier API app to receive JavaScript calls from the web app that you created for the ToDoListAngular project.</span></span>

1. <span data-ttu-id="027c6-179">Em um navegador, acesse o [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="027c6-179">In a browser, go to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="027c6-180">Clique em **Serviços de Aplicativos**e clique no aplicativo de API ToDoListAPI (camada intermediária).</span><span class="sxs-lookup"><span data-stu-id="027c6-180">Click **App Services**, and then click the ToDoListAPI (middle tier) API app.</span></span>
   
    ![Selecione o aplicativo de API no portal](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. <span data-ttu-id="027c6-182">Na folha **Configurações** que abre à direita da folha **Aplicativo de API**, encontre a seção **API** e clique em **CORS**.</span><span class="sxs-lookup"><span data-stu-id="027c6-182">In the **Settings** blade that opens to the right of the **API app** blade, find the **API** section, and then click **CORS**.</span></span>
   
   ![Selecione CORS no portal](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. <span data-ttu-id="027c6-184">Na caixa de texto, insira a URL do aplicativo Web ToDoListAngular (front-end).</span><span class="sxs-lookup"><span data-stu-id="027c6-184">In the text box, enter the URL for the ToDoListAngular (front end) web app.</span></span> <span data-ttu-id="027c6-185">Por exemplo, se você tiver implantado o projeto ToDoListAngular para um aplicativo Web chamado todolistangular0121, permitirá chamadas da URL `https://todolistangular0121.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="027c6-185">For example, if you deployed the ToDoListAngular project to a web app named todolistangular0121, allow calls from the URL `https://todolistangular0121.azurewebsites.net`.</span></span>
   
   <span data-ttu-id="027c6-186">Como alternativa, você pode inserir um asterisco (*) para especificar que todos os domínios de origem são aceitos.</span><span class="sxs-lookup"><span data-stu-id="027c6-186">As an alternative, you can enter an asterisk (*) to specify that all origin domains are accepted.</span></span>
5. <span data-ttu-id="027c6-187">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="027c6-187">Click **Save**.</span></span>
   
   ![Clique em Salvar](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   <span data-ttu-id="027c6-189">Depois que você clicar em **Salvar**, o aplicativo de API aceitará chamadas JavaScript da URL especificada.</span><span class="sxs-lookup"><span data-stu-id="027c6-189">After you click **Save**, the API app will accept JavaScript calls from the specified URL.</span></span> <span data-ttu-id="027c6-190">Nessa captura de tela, o aplicativo de API ToDoListAPI0223 aceitará chamadas de cliente JavaScript do aplicativo Web ToDoListAngular.</span><span class="sxs-lookup"><span data-stu-id="027c6-190">In this screen shot, the ToDoListAPI0223 API app will accept JavaScript client calls from the ToDoListAngular web app.</span></span>

### <a name="test-the-application-with-cors-enabled"></a><span data-ttu-id="027c6-191">Testar o aplicativo com CORS habilitado</span><span class="sxs-lookup"><span data-stu-id="027c6-191">Test the application with CORS enabled</span></span>
* <span data-ttu-id="027c6-192">Abra um navegador para a URL HTTPS do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="027c6-192">Open a browser to the HTTPS URL of the web app.</span></span> 
  
    <span data-ttu-id="027c6-193">Desta vez, o aplicativo lhe permite exibir, adicionar, editar e excluir itens pendentes.</span><span class="sxs-lookup"><span data-stu-id="027c6-193">This time the application lets you view, add, edit, and delete to-do items.</span></span> 
  
    ![A página Lista de Tarefas Pendentes do aplicativo de exemplo](./media/app-service-api-cors-consume-javascript/corssuccess.png)

## <a name="app-service-cors-versus-web-api-cors"></a><span data-ttu-id="027c6-195">CORS do Serviço de Aplicativo versus CORS da API Web</span><span class="sxs-lookup"><span data-stu-id="027c6-195">App Service CORS versus Web API CORS</span></span>
<span data-ttu-id="027c6-196">Em um projeto de API Web, você pode instalar o pacote NuGet [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) para especificar no código de quais domínios a API aceitará chamadas JavaScript.</span><span class="sxs-lookup"><span data-stu-id="027c6-196">In a Web API project, you can install the [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet package to specify in code which domains your API will accept JavaScript calls from.</span></span>

<span data-ttu-id="027c6-197">O suporte a CORS da API Web é mais flexível do que o suporte a CORS do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="027c6-197">Web API CORS support is more flexible than App Service CORS support.</span></span> <span data-ttu-id="027c6-198">Por exemplo, você pode especificar no código diferentes origens aceitas para diferentes métodos de ação, enquanto para o CORS do Serviço de Aplicativo, você especifica um conjunto de origens aceitas para todos os métodos do aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="027c6-198">For example, in code you can specify different accepted origins for different action methods, while for App Service CORS you specify one set of accepted origins for all of an API app's methods.</span></span>

> [!NOTE]
> <span data-ttu-id="027c6-199">Não tente usar o CORS da API Web e o CORS do Serviço de Aplicativo em um aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="027c6-199">Don't try to use both Web API CORS and App Service CORS in one API app.</span></span> <span data-ttu-id="027c6-200">O CORS do Serviço de Aplicativo terá a precedência e o CORS da API Web não funcionará.</span><span class="sxs-lookup"><span data-stu-id="027c6-200">App Service CORS will take precedence and Web API CORS will have no effect.</span></span> <span data-ttu-id="027c6-201">Por exemplo, se você habilitar um domínio de origem no Serviço de Aplicativo e habilitar todos os domínios de origem no código de API Web, o aplicativo de API do Azure aceitará somente chamadas de domínio especificadas no Azure.</span><span class="sxs-lookup"><span data-stu-id="027c6-201">For example, if you enable one origin domain in App Service, and enable all origin domains in your Web API code, your Azure API app will only accept calls from the domain you specified in Azure.</span></span>
> 
> 

### <a name="how-to-enable-cors-in-web-api-code"></a><span data-ttu-id="027c6-202">Como habilitar o CORS no código da API Web</span><span class="sxs-lookup"><span data-stu-id="027c6-202">How to enable CORS in Web API code</span></span>
<span data-ttu-id="027c6-203">As etapas a seguir resumem o processo para habilitar o suporte ao CORS da API Web.</span><span class="sxs-lookup"><span data-stu-id="027c6-203">The following steps summarize the process for enabling Web API CORS support.</span></span> <span data-ttu-id="027c6-204">Para saber mais, confira [Permitindo solicitações entre origens na API Web ASP.NET 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).</span><span class="sxs-lookup"><span data-stu-id="027c6-204">For more information, see [Enabling Cross-Origin Requests in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).</span></span>

1. <span data-ttu-id="027c6-205">Em um projeto de API Web, instale o pacote NuGet [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) .</span><span class="sxs-lookup"><span data-stu-id="027c6-205">In a Web API project, install the [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet package.</span></span>
2. <span data-ttu-id="027c6-206">Inclua uma linha de código `config.EnableCors()` no método **Register** da classe **WebApiConfig**, como no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="027c6-206">Include a `config.EnableCors()` line of code in the **Register** method of the **WebApiConfig** class, as in the following example.</span></span> 
   
        public static class WebApiConfig
        {
            public static void Register(HttpConfiguration config)
            {
                // Web API configuration and services
   
                // The following line enables you to control CORS by using Web API code
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
3. <span data-ttu-id="027c6-207">No controlador de API Web, adicione uma instrução `using` ao namespace `System.Web.Http.Cors` e adicione o atributo `EnableCors` à classe de controlador ou a métodos de ação individuais.</span><span class="sxs-lookup"><span data-stu-id="027c6-207">In your Web API controller, add a `using` statement for the `System.Web.Http.Cors` namespace, and add the `EnableCors` attribute to the controller class or to individual action methods.</span></span> <span data-ttu-id="027c6-208">No exemplo a seguir, o suporte a CORS aplica-se ao controlador inteiro.</span><span class="sxs-lookup"><span data-stu-id="027c6-208">In the following example, CORS support applies to the entire controller.</span></span>
   
        namespace ToDoListAPI.Controllers 
        {
            [HttpOperationExceptionFilterAttribute]
            [EnableCors(origins:"https://todolistangular0121.azurewebsites.net", headers:"accept,content-type,origin,x-my-header", methods: "get,post")]
            public class ToDoListController : ApiController

## <a name="using-azure-api-management-with-api-apps"></a><span data-ttu-id="027c6-209">Uso do Gerenciamento de API com Aplicativos de API</span><span class="sxs-lookup"><span data-stu-id="027c6-209">Using Azure API Management with API Apps</span></span>
<span data-ttu-id="027c6-210">Se você usar o Gerenciamento de API do Azure com um aplicativo de API, configure CORS no Gerenciamento de API em vez de no aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="027c6-210">If you use Azure API Management with an API app, configure CORS in API Management instead of in the API app.</span></span> <span data-ttu-id="027c6-211">Para saber mais, consulte os recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="027c6-211">For more information, see the following resources:</span></span>

* [<span data-ttu-id="027c6-212">Visão geral do Gerenciamento de API do Azure (vídeo: CORS começa em 12:10)</span><span class="sxs-lookup"><span data-stu-id="027c6-212">Azure API Management Overview (video: CORS starts at 12:10)</span></span>](https://azure.microsoft.com/documentation/videos/azure-api-management-overview/)
* [<span data-ttu-id="027c6-213">Políticas entre domínios de Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="027c6-213">API Management cross domain policies</span></span>](https://msdn.microsoft.com/library/azure/dn894084.aspx#CORS)

## <a name="troubleshooting"></a><span data-ttu-id="027c6-214">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="027c6-214">Troubleshooting</span></span>
<span data-ttu-id="027c6-215">Caso você encontre um problema ao percorrer este tutorial, aqui estão algumas ideias para solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="027c6-215">In case you run into a problem while going through this tutorial, here are some troubleshooting ideas.</span></span>

* <span data-ttu-id="027c6-216">Verifique se você está usando a última versão do [SDK do Azure para .NET para Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="027c6-216">Make sure that you're using the latest version of the [Azure SDK for .NET for Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).</span></span>
* <span data-ttu-id="027c6-217">Verifique se você inseriu `https` na configuração de CORS e se está usando `https` para executar o aplicativo Web de front-end.</span><span class="sxs-lookup"><span data-stu-id="027c6-217">Make sure that you entered `https` in the CORS setting, and make sure that you're using `https` to run the front-end web app.</span></span>
* <span data-ttu-id="027c6-218">Verifique se você inseriu a configuração CORS no aplicativo de API de camada intermediária e não no aplicativo Web de front-end.</span><span class="sxs-lookup"><span data-stu-id="027c6-218">Make sure that you entered the CORS setting in the middle tier API app, not in the front-end web app.</span></span>
* <span data-ttu-id="027c6-219">Se você estiver configurando o CORS no código do aplicativo e no Serviço de Aplicativo do Azure, observe que a configuração do CORS do Serviço de Aplicativo substituirá tudo o que você estiver fazendo no código do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="027c6-219">If you're configuring CORS in both application code and Azure App Service, note that the App Service CORS setting will override whatever you're doing in application code.</span></span> 

<span data-ttu-id="027c6-220">Para saber mais sobre os recursos do Visual Studio que simplificam a solução de problemas, confira [Solução de problemas em aplicativos do Serviço de Aplicativo do Azure no Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="027c6-220">To learn more about Visual Studio features that simplify troubleshooting, see [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="027c6-221">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="027c6-221">Next steps</span></span>
<span data-ttu-id="027c6-222">Neste artigo, você viu como habilitar o suporte a CORS do Serviço de Aplicativo para que o código JavaScript de cliente possa chamar uma API em um domínio diferente.</span><span class="sxs-lookup"><span data-stu-id="027c6-222">In this article, you saw how to enable App Service CORS support so that client JavaScript code can call an API in a different domain.</span></span> <span data-ttu-id="027c6-223">Para saber mais sobre aplicativos de API, leia a [Introdução à autenticação no Serviço de Aplicativo](../app-service/app-service-authentication-overview.md) e vá para o tutorial [Autenticação de usuário para aplicativos de API](app-service-api-dotnet-user-principal-auth.md).</span><span class="sxs-lookup"><span data-stu-id="027c6-223">To learn more about API apps, read the [introduction to authentication in App Service](../app-service/app-service-authentication-overview.md), and then go to the [user authentication for API apps](app-service-api-dotnet-user-principal-auth.md) tutorial.</span></span>

