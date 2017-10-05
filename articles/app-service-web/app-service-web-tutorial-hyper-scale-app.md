---
title: Criar um aplicativo de hiperescala no Azure | Microsoft Docs
description: "Aprenda a usar os diferentes serviços do Azure para maximizar o desempenho de um aplicativo ASP.NET no Azure."
services: app-service\web
documentationcenter: dotnet
author: cephalin
manager: erikre
editor: 
ms.assetid: a4d49ac7-0f97-4997-84c5-cdb9c4465757
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 03/23/2017
ms.author: cephalin
ms.openlocfilehash: eac9c5b0d8d0f7802d88e6f4f27d9d23c406e025
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="build-a-hyper-scale-web-app-in-azure"></a><span data-ttu-id="d5e74-103">Criar um aplicativo Web de hiperescala no Azure</span><span class="sxs-lookup"><span data-stu-id="d5e74-103">Build a hyper-scale web app in Azure</span></span>

<span data-ttu-id="d5e74-104">Este tutorial mostra como escalar horizontalmente um aplicativo Web ASP.NET no Azure para maximizar as solicitações do usuário.</span><span class="sxs-lookup"><span data-stu-id="d5e74-104">This tutorial shows you how to scale out an ASP.NET web app in Azure to maximize user requests.</span></span>

<span data-ttu-id="d5e74-105">Antes de começar este tutorial, verifique se [a CLI do Azure está instalada](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) no computador.</span><span class="sxs-lookup"><span data-stu-id="d5e74-105">Before starting this tutorial, ensure that [the Azure CLI is installed](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) on your machine.</span></span> <span data-ttu-id="d5e74-106">Além disso, você precisa do [Visual Studio](https://www.visualstudio.com/vs/) no computador local para executar o aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="d5e74-106">In addition, you need [Visual Studio](https://www.visualstudio.com/vs/) on your local machine to run the sample application.</span></span>

## <a name="step-1---get-sample-application"></a><span data-ttu-id="d5e74-107">Etapa 1 – Obter aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="d5e74-107">Step 1 - Get sample application</span></span>
<span data-ttu-id="d5e74-108">Nesta etapa, você deve configurar o projeto local do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="d5e74-108">In this step, you set up the local ASP.NET project.</span></span>

### <a name="clone-the-application-repository"></a><span data-ttu-id="d5e74-109">Clonar o repositório de aplicativo</span><span class="sxs-lookup"><span data-stu-id="d5e74-109">Clone the application repository</span></span>

<span data-ttu-id="d5e74-110">Abra o terminal de linha de comando de sua escolha e `CD` para um diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d5e74-110">Open the command-line terminal of your choice and `CD` to a working directory.</span></span> <span data-ttu-id="d5e74-111">Execute os comandos a seguir para clonar o aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="d5e74-111">Then, run the following commands to clone the sample application.</span></span> 

```powershell
git clone https://github.com/cephalin/HighScaleApp.git
```

### <a name="run-the-sample-application-in-visual-studio"></a><span data-ttu-id="d5e74-112">Executar o aplicativo de exemplo no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d5e74-112">Run the sample application in Visual Studio</span></span>

<span data-ttu-id="d5e74-113">Abra a solução no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d5e74-113">Open the solution in Visual Studio.</span></span>

```powershell
cd HighScaleApp
.\HighScaleApp.sln
```

<span data-ttu-id="d5e74-114">Digite `F5` para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d5e74-114">Type `F5` to run the application.</span></span>

<span data-ttu-id="d5e74-115">Esse aplicativo Web ASP.NET de exemplo é originado do modelo padrão, além de persistir sessões do usuário e usar o cache de saída.</span><span class="sxs-lookup"><span data-stu-id="d5e74-115">This sample ASP.NET web application comes from the default template, and persists user sessions and uses the output cache.</span></span> <span data-ttu-id="d5e74-116">Observe `HighScaleApp\Controllers\HomeController.cs`.</span><span class="sxs-lookup"><span data-stu-id="d5e74-116">Take a look at `HighScaleApp\Controllers\HomeController.cs`.</span></span> <span data-ttu-id="d5e74-117">O método `Index()` adiciona uma parte dos dados à sessão.</span><span class="sxs-lookup"><span data-stu-id="d5e74-117">The `Index()` method adds a piece of data to the session.</span></span>

```csharp
Session.Add("visited", "true"); 
```

<span data-ttu-id="d5e74-118">E os métodos `About()` e `Contact()` armazenam a saída em cache.</span><span class="sxs-lookup"><span data-stu-id="d5e74-118">And the `About()` and `Contact()` methods cache their output.</span></span>

```csharp
[OutputCache(Duration = 60)]
```

## <a name="step-2---deploy-to-azure"></a><span data-ttu-id="d5e74-119">Etapa 2 – Implantar no Azure</span><span class="sxs-lookup"><span data-stu-id="d5e74-119">Step 2 - Deploy to Azure</span></span>
<span data-ttu-id="d5e74-120">Nesta etapa, você cria um aplicativo Web do Azure e implanta o aplicativo ASP.NET de exemplo nele.</span><span class="sxs-lookup"><span data-stu-id="d5e74-120">In this step, you create an Azure web app and deploy your sample ASP.NET application to it.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="d5e74-121">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="d5e74-121">Create a resource group</span></span>   
<span data-ttu-id="d5e74-122">Use [az group create](https://docs.microsoft.com/cli/azure/group#create) para criar um [grupo de recursos](../azure-resource-manager/resource-group-overview.md) na região Europa Ocidental.</span><span class="sxs-lookup"><span data-stu-id="d5e74-122">Use [az group create](https://docs.microsoft.com/cli/azure/group#create) to create a [resource group](../azure-resource-manager/resource-group-overview.md) in the West Europe region.</span></span> <span data-ttu-id="d5e74-123">Um grupo de recursos é onde você coloca todos os recursos do Azure que quer gerenciar, como o aplicativo Web e qualquer back-end do Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="d5e74-123">A resource group is where you put all the Azure resources that you want to manage together, such as the web app and any SQL Database back end.</span></span>

```azurecli
az group create --location "West Europe" --name myResourceGroup
```

<span data-ttu-id="d5e74-124">Para ver quais são os possíveis valores que podem ser usados para `---location`, use o comando [az appservice list-locations](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations).</span><span class="sxs-lookup"><span data-stu-id="d5e74-124">To see what possible values you can use for `---location`, use the [az appservice list-locations](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="d5e74-125">Criar um plano de Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="d5e74-125">Create an App Service plan</span></span>
<span data-ttu-id="d5e74-126">Use [az appservice plan create](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) para criar um [plano do Serviço de Aplicativo](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) "B1".</span><span class="sxs-lookup"><span data-stu-id="d5e74-126">Use [az appservice plan create](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) to create a "B1" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

```azurecli
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1
```

<span data-ttu-id="d5e74-127">Um plano do Serviço de Aplicativo é uma unidade de escala, que pode incluir qualquer número de aplicativos que você desejar escalar vertical ou horizontalmente juntos na mesma infraestrutura de Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d5e74-127">An App Service plan is a scale unit, which can include any number of apps that you want to scale up or out together over the same App Service infrastructure.</span></span> <span data-ttu-id="d5e74-128">Cada plano também recebe um [tipo de preço](https://azure.microsoft.com/en-us/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="d5e74-128">Each plan is also assigned a [pricing tier](https://azure.microsoft.com/en-us/pricing/details/app-service/).</span></span> <span data-ttu-id="d5e74-129">Tipos mais alto incluem hardware melhor e mais recursos, como mais instâncias de escala horizontal.</span><span class="sxs-lookup"><span data-stu-id="d5e74-129">Higher tiers include better hardware and more features, such as more scale-out instances.</span></span>

<span data-ttu-id="d5e74-130">Neste tutorial, B1 é tipo mínimo, que permite escalar horizontalmente para três instâncias.</span><span class="sxs-lookup"><span data-stu-id="d5e74-130">For this tutorial, B1 is the minimum tier that enables scale out to three instances.</span></span> <span data-ttu-id="d5e74-131">Sempre que quiser, você pode mover seu aplicativo para cima ou para baixo no tipo de preço executando o comando [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update).</span><span class="sxs-lookup"><span data-stu-id="d5e74-131">You can always move your app up or down the pricing tier later by running [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update).</span></span> 

### <a name="create-a-web-app"></a><span data-ttu-id="d5e74-132">Criar um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="d5e74-132">Create a web app</span></span>
<span data-ttu-id="d5e74-133">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) para criar um aplicativo Web com um nome exclusivo em `$appName`.</span><span class="sxs-lookup"><span data-stu-id="d5e74-133">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) to create a web app with a unique name in `$appName`.</span></span>

```azurecli
$appName = "<replace-with-a-unique-name>"
az appservice web create --name $appName --resource-group myResourceGroup --plan myAppServicePlan
```

### <a name="set-deployment-credentials"></a><span data-ttu-id="d5e74-134">Definir credenciais de implantação</span><span class="sxs-lookup"><span data-stu-id="d5e74-134">Set deployment credentials</span></span>
<span data-ttu-id="d5e74-135">Use [az appservice web deployment user set](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) para definir as credenciais no nível de conta para o Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d5e74-135">Use [az appservice web deployment user set](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) to set your account-level deployment credentials for App Service.</span></span>

```azurecli
az appservice web deployment user set --user-name <letters-numbers> --password <mininum-8-char-captital-lowercase-letters-numbers>
```

### <a name="configure-git-deployment"></a><span data-ttu-id="d5e74-136">Configurar a implantação do Git</span><span class="sxs-lookup"><span data-stu-id="d5e74-136">Configure Git deployment</span></span>
<span data-ttu-id="d5e74-137">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) para configurar a implantação do Git local.</span><span class="sxs-lookup"><span data-stu-id="d5e74-137">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) to configure local Git deployment.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName --resource-group myResourceGroup
```

<span data-ttu-id="d5e74-138">Esse comando fornece uma saída semelhante a esta:</span><span class="sxs-lookup"><span data-stu-id="d5e74-138">This command gives you an output that looks like the following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="d5e74-139">Use a URL retornada para configurar o Git remoto.</span><span class="sxs-lookup"><span data-stu-id="d5e74-139">Use the returned URL to configure your Git remote.</span></span> <span data-ttu-id="d5e74-140">O comando a seguir usa o exemplo de saída anterior.</span><span class="sxs-lookup"><span data-stu-id="d5e74-140">The following command uses the preceding output example.</span></span>

```powershell
git remote add azure https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-the-sample-application"></a><span data-ttu-id="d5e74-141">Implantar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="d5e74-141">Deploy the sample application</span></span>
<span data-ttu-id="d5e74-142">Agora, você está pronto para implantar o aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="d5e74-142">You are now ready to deploy your sample application.</span></span> <span data-ttu-id="d5e74-143">Execute `git push`.</span><span class="sxs-lookup"><span data-stu-id="d5e74-143">Run `git push`.</span></span>

```powershell
git push azure master
```

<span data-ttu-id="d5e74-144">Quando a senha for solicitada, use a senha que você especificou quando executou `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="d5e74-144">When prompted for password, use the password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-to-azure-web-app"></a><span data-ttu-id="d5e74-145">Navegar até o aplicativo Web do Azure</span><span class="sxs-lookup"><span data-stu-id="d5e74-145">Browse to Azure web app</span></span>
<span data-ttu-id="d5e74-146">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) para ver seu aplicativo em execução ao vivo no Azure. Execute este comando.</span><span class="sxs-lookup"><span data-stu-id="d5e74-146">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) to see your app running live in Azure, run this command.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-3---connect-to-redis"></a><span data-ttu-id="d5e74-147">Etapa 3 – Conectar-se ao Redis</span><span class="sxs-lookup"><span data-stu-id="d5e74-147">Step 3 - Connect to Redis</span></span>
<span data-ttu-id="d5e74-148">Nesta etapa, você configura o Cache Redis do Azure como um cache externo, colocado no seu aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5e74-148">In this step, you set up Azure Redis Cache as an external, colocated cache to your Azure web app.</span></span> <span data-ttu-id="d5e74-149">É possível utilizar rapidamente o Redis para armazenar em cache a saída da página.</span><span class="sxs-lookup"><span data-stu-id="d5e74-149">You can quickly utilize Redis to cache your page output.</span></span> <span data-ttu-id="d5e74-150">Além disso, ao escalar horizontalmente os aplicativos Web posteriormente, o Redis ajuda a persistir as sessões do usuário em várias instâncias de modo confiável.</span><span class="sxs-lookup"><span data-stu-id="d5e74-150">In addition, when you scale out your web apps later, Redis helps you persist user sessions across multiple instances reliably.</span></span>

### <a name="create-an-azure-redis-cache"></a><span data-ttu-id="d5e74-151">Criar um Cache Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="d5e74-151">Create an Azure Redis Cache</span></span>
<span data-ttu-id="d5e74-152">Use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) para criar um Cache Redis do Azure e salvar a saída JSON.</span><span class="sxs-lookup"><span data-stu-id="d5e74-152">Use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) to create an Azure Redis Cache and save the JSON output.</span></span> <span data-ttu-id="d5e74-153">Use um nome exclusivo em `$cacheName`.</span><span class="sxs-lookup"><span data-stu-id="d5e74-153">Use a unique name in `$cacheName`.</span></span>

```powershell
$cacheName = "<replace-with-a-unique-cache-name>"
$redis = (az redis create --name $cacheName --resource-group myResourceGroup --location "West Europe" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

### <a name="configure-the-application-to-use-redis"></a><span data-ttu-id="d5e74-154">Configurar o aplicativo para usar o Redis</span><span class="sxs-lookup"><span data-stu-id="d5e74-154">Configure the application to use Redis</span></span>
<span data-ttu-id="d5e74-155">Formate a cadeia de conexão para o cache.</span><span class="sxs-lookup"><span data-stu-id="d5e74-155">Format the connection string for your cache.</span></span>

```powershell
$connstring = "$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False"
$connstring 
```

<span data-ttu-id="d5e74-156">A segunda linha deve fornecer uma saída parecida com esta:</span><span class="sxs-lookup"><span data-stu-id="d5e74-156">The second line should give you an output that looks like this:</span></span>

```
mycachename.redis.cache.windows.net:6380,password=/rQP/TLz1mrEPpmh9b/gnfns/t9vBRXqXn3i1RwBjGA=,ssl=True,abortConnect=False
```

<span data-ttu-id="d5e74-157">No Visual Studio, crie um arquivo de configuração da Web na raiz do projeto chamado `redis.config` e cole nele o código a seguir.</span><span class="sxs-lookup"><span data-stu-id="d5e74-157">In Visual Studio, create a web configuration file in your project root called `redis.config` and paste the following code into it.</span></span> <span data-ttu-id="d5e74-158">Em `value`, use a cadeia de conexão da saída do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d5e74-158">In `value`, use the connection string from the PowerShell output.</span></span>

```xml
<appSettings>
  <add key="RedisConnection" value="your-azure-redis-cache-connection-string"/>
</appSettings>
```

<span data-ttu-id="d5e74-159">Examinando o arquivo `.gitignore` no repositório Git, você verá que esse arquivo foi excluído do controle de origem.</span><span class="sxs-lookup"><span data-stu-id="d5e74-159">If you look at the `.gitignore` file in your Git repository, you'll see that this file is excluded from source control.</span></span> <span data-ttu-id="d5e74-160">Dessa forma, as informações confidenciais são mantidas em segurança.</span><span class="sxs-lookup"><span data-stu-id="d5e74-160">That way your sensitive information is kept safe.</span></span> 

<span data-ttu-id="d5e74-161">Abra `Web.config`.</span><span class="sxs-lookup"><span data-stu-id="d5e74-161">Open `Web.config`.</span></span> <span data-ttu-id="d5e74-162">Observe o elemento `<appSettings file="redis.config">`, que obtém a configuração que você criou em `redis.config`.</span><span class="sxs-lookup"><span data-stu-id="d5e74-162">Notice the `<appSettings file="redis.config">` element, which gets the setting you created in `redis.config`.</span></span> 

<span data-ttu-id="d5e74-163">Localize a seção comentada que inclui `<sessionState>` e `<caching>`.</span><span class="sxs-lookup"><span data-stu-id="d5e74-163">Find the commented section that includes `<sessionState>` and `<caching>`.</span></span> <span data-ttu-id="d5e74-164">Remova os comentários dessa seção.</span><span class="sxs-lookup"><span data-stu-id="d5e74-164">Uncomment this section.</span></span>

![](./media/app-service-web-tutorial-hyper-scale-app/redisproviders.png)

<span data-ttu-id="d5e74-165">Esse código procura a cadeia de conexão do Redis que você definiu em `RedisConnection`.</span><span class="sxs-lookup"><span data-stu-id="d5e74-165">This code looks for the Redis connection string you defined in `RedisConnection`.</span></span> 

<span data-ttu-id="d5e74-166">Agora, o aplicativo usa o Redis para gerenciar sessões e o caching.</span><span class="sxs-lookup"><span data-stu-id="d5e74-166">Your application now uses Redis to manage sessions and caching.</span></span> <span data-ttu-id="d5e74-167">Digite `F5` para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d5e74-167">Type `F5` to run the application.</span></span> <span data-ttu-id="d5e74-168">Se desejar, você pode baixar um cliente de gerenciamento do Redis para visualizar os dados que agora são salvos no cache.</span><span class="sxs-lookup"><span data-stu-id="d5e74-168">If you like, you can download a Redis management client to visualize the data that is now saved to the cache.</span></span>

### <a name="configure-the-connection-string-in-azure"></a><span data-ttu-id="d5e74-169">Configurar a cadeia de conexão no Azure</span><span class="sxs-lookup"><span data-stu-id="d5e74-169">Configure the connection string in Azure</span></span>

<span data-ttu-id="d5e74-170">Para que o aplicativo funcione no Azure, você precisa configurar a mesma cadeia de conexão do Redis no aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5e74-170">For your application to work in Azure, you need to configure the same Redis connection string in your Azure web app.</span></span> <span data-ttu-id="d5e74-171">Uma vez que `redis.config` não é mantido no controle de origem, ele não é implantado no Azure quando você executa a implantação do Git.</span><span class="sxs-lookup"><span data-stu-id="d5e74-171">Since `redis.config` is not maintained in source control, it is not deployed to Azure when you run Git deployment.</span></span>

<span data-ttu-id="d5e74-172">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) para adicionar a cadeia de conexão com o mesmo nome (`RedisConnection`).</span><span class="sxs-lookup"><span data-stu-id="d5e74-172">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) to add the connection string with the same name (`RedisConnection`).</span></span>

<span data-ttu-id="d5e74-173">az appservice web config appsettings update --settings "RedisConnection=$connstring" --name $appName --resource-group myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d5e74-173">az appservice web config appsettings update --settings "RedisConnection=$connstring" --name $appName --resource-group myResourceGroup</span></span>

<span data-ttu-id="d5e74-174">Lembre-se de que `$connstring` contém a cadeia de conexão formatada.</span><span class="sxs-lookup"><span data-stu-id="d5e74-174">Remember that `$connstring` contains the formatted connection string.</span></span>

### <a name="redeploy-the-application-to-azure"></a><span data-ttu-id="d5e74-175">Reimplantar o aplicativo no Azure</span><span class="sxs-lookup"><span data-stu-id="d5e74-175">Redeploy the application to Azure</span></span>
<span data-ttu-id="d5e74-176">Use os comandos Git para enviar por push suas alterações ao Azure</span><span class="sxs-lookup"><span data-stu-id="d5e74-176">Use Git commands to push your changes to Azure</span></span>

```bash
git add .
git commit -m "now use Redis providers"
git push azure master
```

<span data-ttu-id="d5e74-177">Quando a senha for solicitada, use a senha que você especificou quando executou `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="d5e74-177">When prompted for password, use the password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-to-the-azure-web-app"></a><span data-ttu-id="d5e74-178">Navegar até o aplicativo Web do Azure</span><span class="sxs-lookup"><span data-stu-id="d5e74-178">Browse to the Azure web app</span></span>
<span data-ttu-id="d5e74-179">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) para ver as alterações em tempo real no Azure.</span><span class="sxs-lookup"><span data-stu-id="d5e74-179">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) to see the changes live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-4---scale-to-multiple-instances"></a><span data-ttu-id="d5e74-180">Etapa 4 – Escalar para várias instâncias</span><span class="sxs-lookup"><span data-stu-id="d5e74-180">Step 4 - Scale to multiple instances</span></span>
<span data-ttu-id="d5e74-181">O plano do Serviço de Aplicativo é a unidade de escala para seus aplicativos Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5e74-181">The App Service plan is the scale unit for your Azure web apps.</span></span> <span data-ttu-id="d5e74-182">Para escalar horizontalmente o aplicativo Web, escale o plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d5e74-182">To scale out your web app, you scale the App Service plan.</span></span>

<span data-ttu-id="d5e74-183">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) para escalar horizontalmente o plano do Serviço de Aplicativo para três instâncias, que é o número máximo permitido pelo tipo de preço B1.</span><span class="sxs-lookup"><span data-stu-id="d5e74-183">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) to scale out the App Service plan to three instances, which is the maximum number allowed by the B1 pricing tier.</span></span> <span data-ttu-id="d5e74-184">Lembre-se de que B1 é o tipo de preço que você escolheu quando criou anteriormente o plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d5e74-184">Remember that B1 is the pricing tier that you chose when you created the App Service plan earlier.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --number-of-workers 3 
```

## <a name="step-5---scale-geographically"></a><span data-ttu-id="d5e74-185">Etapa 5 – Escalar geograficamente</span><span class="sxs-lookup"><span data-stu-id="d5e74-185">Step 5 - Scale geographically</span></span>
<span data-ttu-id="d5e74-186">Ao escalar geograficamente, você executa o aplicativo em várias regiões da nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5e74-186">When scaling geographically, you run your app in multiple regions of the Azure cloud.</span></span> <span data-ttu-id="d5e74-187">Essa configuração balanceia a carga do aplicativo com base na localização geográfica e reduz o tempo de resposta colocando o aplicativo mais próximo dos navegadores cliente.</span><span class="sxs-lookup"><span data-stu-id="d5e74-187">This setup load-balances your app further based on geography and lowers the response time by placing your app closer to client browsers.</span></span>

<span data-ttu-id="d5e74-188">Nessa etapa, você escala o aplicativo Web ASP.NET para uma segunda região com o [Gerenciador de Tráfego do Azure](https://docs.microsoft.com/en-us/azure/traffic-manager/).</span><span class="sxs-lookup"><span data-stu-id="d5e74-188">In this step, you scale your ASP.NET web app to a second region with [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/).</span></span> <span data-ttu-id="d5e74-189">No final da etapa, você terá um aplicativo Web em execução na Europa Ocidental (já criado) e um aplicativo Web em execução no Sudeste Asiático (ainda não criado).</span><span class="sxs-lookup"><span data-stu-id="d5e74-189">At the end of the step, you will have a web app running in West Europe (already created) and a web app running in Southeast Asia (not yet created).</span></span> <span data-ttu-id="d5e74-190">Ambos os aplicativos serão atendidos pela mesma URL do Gerenciador de Tráfego.</span><span class="sxs-lookup"><span data-stu-id="d5e74-190">Both apps will be served from the same Traffic Manager URL.</span></span>

### <a name="scale-up-the-europe-app-to-standard-tier"></a><span data-ttu-id="d5e74-191">Escalar verticalmente o aplicativo na Europa para o tipo Standard</span><span class="sxs-lookup"><span data-stu-id="d5e74-191">Scale up the Europe app to Standard tier</span></span>
<span data-ttu-id="d5e74-192">No Serviço de Aplicativo, a integração ao Gerenciador de Tráfego do Azure exige o tipo de preço Standard.</span><span class="sxs-lookup"><span data-stu-id="d5e74-192">In App Service, integration with Azure Traffic Manager requires the Standard pricing tier.</span></span> <span data-ttu-id="d5e74-193">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) para escalar verticalmente o plano do Serviço de Aplicativo para S1.</span><span class="sxs-lookup"><span data-stu-id="d5e74-193">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) to scale up your App Service plan to S1.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --sku S1
```
### <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="d5e74-194">Criar um perfil do Gerenciador de Tráfego</span><span class="sxs-lookup"><span data-stu-id="d5e74-194">Create a Traffic Manager profile</span></span> 
<span data-ttu-id="d5e74-195">Use [az network traffic-manager profile create](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) para criar um perfil do Gerenciador de Tráfego e adicioná-lo ao grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d5e74-195">Use [az network traffic-manager profile create](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) to create a Traffic Manager profile and add it to your resource group.</span></span> <span data-ttu-id="d5e74-196">Use um nome DNS exclusivo em $dnsName.</span><span class="sxs-lookup"><span data-stu-id="d5e74-196">Use a unique DNS name in $dnsName.</span></span>

```azurecli
$dnsName = "<replace-with-unique-dns-name>"
az network traffic-manager profile create --name myTrafficManagerProfile --resource-group myResourceGroup --routing-method Performance --unique-dns-name $dnsName
```

> [!NOTE]
> <span data-ttu-id="d5e74-197">`--routing-method Performance` especifica que esse perfil [roteia o tráfego do usuário para o ponto de extremidade mais próximo](../traffic-manager/traffic-manager-routing-methods.md).</span><span class="sxs-lookup"><span data-stu-id="d5e74-197">`--routing-method Performance` specifies that this profile [routes user traffic to the closest endpoint](../traffic-manager/traffic-manager-routing-methods.md).</span></span>

### <a name="get-the-resource-id-of-the-europe-app"></a><span data-ttu-id="d5e74-198">Obter a ID de recurso do aplicativo na Europa</span><span class="sxs-lookup"><span data-stu-id="d5e74-198">Get the resource ID of the Europe app</span></span>
<span data-ttu-id="d5e74-199">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) para obter a ID de recurso do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="d5e74-199">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) to get the resource ID of your web app.</span></span>

```azurecli
$appId = az appservice web show --name $appName --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-the-europe-app"></a><span data-ttu-id="d5e74-200">Adicionar um ponto de extremidade do Gerenciador de Tráfego para o aplicativo na Europa</span><span class="sxs-lookup"><span data-stu-id="d5e74-200">Add a Traffic Manager endpoint for the Europe app</span></span>
<span data-ttu-id="d5e74-201">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) para adicionar um ponto de extremidade ao seu perfil do Gerenciador de Tráfego e use a ID de recurso do aplicativo Web como o destino.</span><span class="sxs-lookup"><span data-stu-id="d5e74-201">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) to add an endpoint to your Traffic Manager profile and use the resource ID of your web app as the target.</span></span>

```azurecli
az network traffic-manager endpoint create --name myWestEuropeEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appId
```

### <a name="get-the-traffic-manager-endpoint-url"></a><span data-ttu-id="d5e74-202">Obter a URL do ponto de extremidade do Gerenciador de Tráfego</span><span class="sxs-lookup"><span data-stu-id="d5e74-202">Get the Traffic Manager endpoint URL</span></span>
<span data-ttu-id="d5e74-203">O perfil do Gerenciador de Tráfego agora tem um ponto de extremidade que aponta para seu aplicativo Web existente.</span><span class="sxs-lookup"><span data-stu-id="d5e74-203">Your Traffic Manager profile now has an endpoint that points to your existing web app.</span></span> <span data-ttu-id="d5e74-204">Use [az network traffic-manager profile show](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) para obter sua URL.</span><span class="sxs-lookup"><span data-stu-id="d5e74-204">Use [az network traffic-manager profile show](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) to get its URL.</span></span> 

```azurecli
az network traffic-manager profile show --name myTrafficManagerProfile --resource-group myResourceGroup --query dnsConfig.fqdn --output tsv
```

<span data-ttu-id="d5e74-205">Copie a saída no navegador.</span><span class="sxs-lookup"><span data-stu-id="d5e74-205">Copy the output into your browser.</span></span> <span data-ttu-id="d5e74-206">Você deve ver o aplicativo Web novamente.</span><span class="sxs-lookup"><span data-stu-id="d5e74-206">You should see your web app again.</span></span>

### <a name="create-an-azure-redis-cache-in-asia"></a><span data-ttu-id="d5e74-207">Criar um Cache Redis do Azure na Ásia</span><span class="sxs-lookup"><span data-stu-id="d5e74-207">Create an Azure Redis Cache in Asia</span></span>
<span data-ttu-id="d5e74-208">Agora, você replica seu aplicativo Web na região Sudeste Asiático.</span><span class="sxs-lookup"><span data-stu-id="d5e74-208">Now, you replicate your Azure web app to the Southeast Asia region.</span></span> <span data-ttu-id="d5e74-209">Para começar, use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) para criar um segundo Cache Redis do Azure no Sudeste Asiático.</span><span class="sxs-lookup"><span data-stu-id="d5e74-209">To start, use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) to create a second Azure Redis Cache in Southeast Asia.</span></span> <span data-ttu-id="d5e74-210">Esse cache precisa ser colocado com seu aplicativo na Ásia.</span><span class="sxs-lookup"><span data-stu-id="d5e74-210">This cache needs to be colocated with your app in Asia.</span></span>

```powershell
$redis = (az redis create --name $cacheName-asia --resource-group myResourceGroup --location "Southeast Asia" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

<span data-ttu-id="d5e74-211">`--name $cacheName-asia` dá ao cache o nome do cache da Europa Ocidental, com o sufixo `-asia`.</span><span class="sxs-lookup"><span data-stu-id="d5e74-211">`--name $cacheName-asia` gives the cache the name of the West Europe cache, with the `-asia` suffix.</span></span>

### <a name="create-an-app-service-plan-in-asia"></a><span data-ttu-id="d5e74-212">Criar um plano do Serviço de Aplicativo na Ásia</span><span class="sxs-lookup"><span data-stu-id="d5e74-212">Create an App Service plan in Asia</span></span>
<span data-ttu-id="d5e74-213">Use [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) para criar um segundo plano do Serviço de Aplicativo na região Sudeste Asiático usando o mesmo tipo S1 que o plano da Europa Ocidental.</span><span class="sxs-lookup"><span data-stu-id="d5e74-213">Use [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) to create a second App Service plan in the Southeast Asia region, using the same S1 tier as the West Europe plan.</span></span>

```azurecli
az appservice plan create --name myAppServicePlanAsia --resource-group myResourceGroup --location "Southeast Asia" --sku S1
```

### <a name="create-a-web-app-in-asia"></a><span data-ttu-id="d5e74-214">Criar um aplicativo Web na Ásia</span><span class="sxs-lookup"><span data-stu-id="d5e74-214">Create a web app in Asia</span></span>
<span data-ttu-id="d5e74-215">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) para criar um segundo aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="d5e74-215">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) to create a second web app.</span></span>

```azurecli
az appservice web create --name $appName-asia --resource-group myResourceGroup --plan myAppServicePlanAsia
```

<span data-ttu-id="d5e74-216">`--name $appName-asia` dá ao aplicativo o nome do aplicativo da Europa Ocidental, com o sufixo `-asia`.</span><span class="sxs-lookup"><span data-stu-id="d5e74-216">`--name $appName-asia` gives the app the name of the West Europe app, with the `-asia` suffix.</span></span>

### <a name="configure-the-connection-string-for-redis"></a><span data-ttu-id="d5e74-217">Configurar a cadeia de conexão para Redis</span><span class="sxs-lookup"><span data-stu-id="d5e74-217">Configure the connection string for Redis</span></span>
<span data-ttu-id="d5e74-218">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) para adicionar ao aplicativo Web a cadeia de conexão para o cache do Sudeste Asiático.</span><span class="sxs-lookup"><span data-stu-id="d5e74-218">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) to add to the web app the connection string for the Southeast Asia cache.</span></span>

<span data-ttu-id="d5e74-219">az appservice web config appsettings update --settings "RedisConnection=$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False" --name $appName-asia --resource-group myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d5e74-219">az appservice web config appsettings update --settings "RedisConnection=$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False" --name $appName-asia --resource-group myResourceGroup</span></span>

### <a name="configure-git-deployment-for-the-asia-app"></a><span data-ttu-id="d5e74-220">Configurar a implantação do Git para o aplicativo na Ásia.</span><span class="sxs-lookup"><span data-stu-id="d5e74-220">Configure Git deployment for the Asia app.</span></span>
<span data-ttu-id="d5e74-221">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) a fim de configurar a implantação do Git local para o segundo aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="d5e74-221">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) to configure local Git deployment for the second web app.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="d5e74-222">Esse comando fornece uma saída semelhante a esta:</span><span class="sxs-lookup"><span data-stu-id="d5e74-222">This command gives you an output that looks like the following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="d5e74-223">Use a URL retornada de modo a configurar um segundo Git remoto para o repositório local.</span><span class="sxs-lookup"><span data-stu-id="d5e74-223">Use the returned URL to configure a second Git remote for your local repository.</span></span> <span data-ttu-id="d5e74-224">O comando a seguir usa o exemplo de saída anterior.</span><span class="sxs-lookup"><span data-stu-id="d5e74-224">The following command uses the preceding output example.</span></span>

```bash
git remote add azure-asia https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-your-sample-application"></a><span data-ttu-id="d5e74-225">Implantar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="d5e74-225">Deploy your sample application</span></span>
<span data-ttu-id="d5e74-226">Execute `git push` para implantar o aplicativo de exemplo no segundo Git remoto.</span><span class="sxs-lookup"><span data-stu-id="d5e74-226">Run `git push` to deploy your sample application to the second Git remote.</span></span> 

```bash
git push azure-asia master
```

<span data-ttu-id="d5e74-227">Quando a senha for solicitada, use a senha que você especificou quando executou `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="d5e74-227">When prompted for password, use the password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-to-the-asia-app"></a><span data-ttu-id="d5e74-228">Navegar até o aplicativo na Ásia</span><span class="sxs-lookup"><span data-stu-id="d5e74-228">Browse to the Asia app</span></span>
<span data-ttu-id="d5e74-229">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) para verificar se o aplicativo está em execução em tempo real no Azure.</span><span class="sxs-lookup"><span data-stu-id="d5e74-229">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) to verify that your app is running live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName-asia --resource-group myResourceGroup
```

### <a name="get-the-resource-id-of-the-asia-app"></a><span data-ttu-id="d5e74-230">Obter a ID de recurso do aplicativo na Ásia</span><span class="sxs-lookup"><span data-stu-id="d5e74-230">Get the resource ID of the Asia app</span></span>
<span data-ttu-id="d5e74-231">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) para obter a ID de recurso do aplicativo Web no Sudeste Asiático.</span><span class="sxs-lookup"><span data-stu-id="d5e74-231">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) to get the resource ID of your web app in Southeast Asia.</span></span>

```azurecli
$appIdAsia = az appservice web show --name $appName-asia --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-the-asia-app"></a><span data-ttu-id="d5e74-232">Adicionar um ponto de extremidade do Gerenciador de Tráfego para o aplicativo na Ásia</span><span class="sxs-lookup"><span data-stu-id="d5e74-232">Add a Traffic Manager endpoint for the Asia app</span></span>
<span data-ttu-id="d5e74-233">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) para adicionar um segundo ponto de extremidade ao perfil do Gerenciador de Tráfego.</span><span class="sxs-lookup"><span data-stu-id="d5e74-233">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) to add a second endpoint to the Traffic Manager profile.</span></span>

```azurecli
az network traffic-manager endpoint create --name myAsiaEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appIdAsia
```

### <a name="add-region-identifier-to-web-apps"></a><span data-ttu-id="d5e74-234">Adicionar identificador de região aos aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="d5e74-234">Add region identifier to web apps</span></span>
<span data-ttu-id="d5e74-235">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) para adicionar uma variável de ambiente específica da região.</span><span class="sxs-lookup"><span data-stu-id="d5e74-235">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) to add a region-specific environment variable.</span></span>

```azurecli
az appservice web config appsettings update --settings "Region=West Europe" --name $appName --resource-group myResourceGroup
az appservice web config appsettings update --settings "Region=Southeast Asia" --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="d5e74-236">O código do seu aplicativo já usa essa configuração de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d5e74-236">Your application code already uses this application setting.</span></span> <span data-ttu-id="d5e74-237">Observe `HighScaleApp\Views\Home\Index.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="d5e74-237">Take a look at `HighScaleApp\Views\Home\Index.cshtml`.</span></span>

### <a name="complete"></a><span data-ttu-id="d5e74-238">Concluído!</span><span class="sxs-lookup"><span data-stu-id="d5e74-238">Complete!</span></span>

<span data-ttu-id="d5e74-239">Agora, tente acessar a URL do seu perfil do Gerenciador de Tráfego nos navegadores em diferentes regiões geográficas.</span><span class="sxs-lookup"><span data-stu-id="d5e74-239">Now, try to access the URL of your Traffic Manager profile from browsers in different geographical regions.</span></span> <span data-ttu-id="d5e74-240">Os navegadores cliente da Europa devem mostrar "ASP.NET Europa Ocidental" e o navegador cliente da Ásia deve mostrar "ASP.NET Sudeste Asiático".</span><span class="sxs-lookup"><span data-stu-id="d5e74-240">Client browsers from Europe should show "ASP.NET West Europe", and client browser from Asia should show "ASP.NET Southeast Asia."</span></span>

## <a name="more-resources"></a><span data-ttu-id="d5e74-241">Mais recursos</span><span class="sxs-lookup"><span data-stu-id="d5e74-241">More resources</span></span>
