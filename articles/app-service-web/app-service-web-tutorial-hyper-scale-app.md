---
title: aaaBuild um aplicativo de hyper-escala no Azure | Microsoft Docs
description: "Saiba como toouse diferentes serviços do Azure toomaximize Olá desempenho de um aplicativo ASP.NET no Azure."
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
ms.openlocfilehash: 7952647b49a82c286c6a737eb41a7f23a13fd75e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-hyper-scale-web-app-in-azure"></a><span data-ttu-id="32ee9-103">Criar um aplicativo Web de hiperescala no Azure</span><span class="sxs-lookup"><span data-stu-id="32ee9-103">Build a hyper-scale web app in Azure</span></span>

<span data-ttu-id="32ee9-104">Este tutorial mostra como tooscale-out de um aplicativo da web ASP.NET no Azure toomaximize usuário solicita.</span><span class="sxs-lookup"><span data-stu-id="32ee9-104">This tutorial shows you how tooscale out an ASP.NET web app in Azure toomaximize user requests.</span></span>

<span data-ttu-id="32ee9-105">Antes de iniciar este tutorial, certifique-se de que [Olá CLI do Azure está instalado](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) em seu computador.</span><span class="sxs-lookup"><span data-stu-id="32ee9-105">Before starting this tutorial, ensure that [hello Azure CLI is installed](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) on your machine.</span></span> <span data-ttu-id="32ee9-106">Além disso, você precisa [Visual Studio](https://www.visualstudio.com/vs/) em seu aplicativo de amostra do computador local toorun hello.</span><span class="sxs-lookup"><span data-stu-id="32ee9-106">In addition, you need [Visual Studio](https://www.visualstudio.com/vs/) on your local machine toorun hello sample application.</span></span>

## <a name="step-1---get-sample-application"></a><span data-ttu-id="32ee9-107">Etapa 1 – Obter aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="32ee9-107">Step 1 - Get sample application</span></span>
<span data-ttu-id="32ee9-108">Nesta etapa, você configura o local do projeto ASP.NET Olá.</span><span class="sxs-lookup"><span data-stu-id="32ee9-108">In this step, you set up hello local ASP.NET project.</span></span>

### <a name="clone-hello-application-repository"></a><span data-ttu-id="32ee9-109">Repositório de aplicativo de saudação do clone</span><span class="sxs-lookup"><span data-stu-id="32ee9-109">Clone hello application repository</span></span>

<span data-ttu-id="32ee9-110">Terminal de linha de comando Olá aberto de sua escolha e `CD` tooa diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="32ee9-110">Open hello command-line terminal of your choice and `CD` tooa working directory.</span></span> <span data-ttu-id="32ee9-111">Em seguida, seguir Olá execução comandos aplicativo de exemplo hello tooclone.</span><span class="sxs-lookup"><span data-stu-id="32ee9-111">Then, run hello following commands tooclone hello sample application.</span></span> 

```powershell
git clone https://github.com/cephalin/HighScaleApp.git
```

### <a name="run-hello-sample-application-in-visual-studio"></a><span data-ttu-id="32ee9-112">Executar o aplicativo de exemplo hello no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="32ee9-112">Run hello sample application in Visual Studio</span></span>

<span data-ttu-id="32ee9-113">Abra a solução de saudação no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="32ee9-113">Open hello solution in Visual Studio.</span></span>

```powershell
cd HighScaleApp
.\HighScaleApp.sln
```

<span data-ttu-id="32ee9-114">Tipo `F5` toorun aplicativo de hello.</span><span class="sxs-lookup"><span data-stu-id="32ee9-114">Type `F5` toorun hello application.</span></span>

<span data-ttu-id="32ee9-115">Este aplicativo de web do ASP.NET de exemplo vem de modelo de padrão de saudação e persiste o cache de saída de saudação de sessões e usos de usuário.</span><span class="sxs-lookup"><span data-stu-id="32ee9-115">This sample ASP.NET web application comes from hello default template, and persists user sessions and uses hello output cache.</span></span> <span data-ttu-id="32ee9-116">Observe `HighScaleApp\Controllers\HomeController.cs`.</span><span class="sxs-lookup"><span data-stu-id="32ee9-116">Take a look at `HighScaleApp\Controllers\HomeController.cs`.</span></span> <span data-ttu-id="32ee9-117">Olá `Index()` método adiciona uma parte da sessão de toohello de dados.</span><span class="sxs-lookup"><span data-stu-id="32ee9-117">hello `Index()` method adds a piece of data toohello session.</span></span>

```csharp
Session.Add("visited", "true"); 
```

<span data-ttu-id="32ee9-118">E hello `About()` e `Contact()` sua saída de cache de métodos.</span><span class="sxs-lookup"><span data-stu-id="32ee9-118">And hello `About()` and `Contact()` methods cache their output.</span></span>

```csharp
[OutputCache(Duration = 60)]
```

## <a name="step-2---deploy-tooazure"></a><span data-ttu-id="32ee9-119">Etapa 2: implantar tooAzure</span><span class="sxs-lookup"><span data-stu-id="32ee9-119">Step 2 - Deploy tooAzure</span></span>
<span data-ttu-id="32ee9-120">Nesta etapa, você cria um aplicativo web do Azure e implanta seu tooit de aplicativo do ASP.NET de exemplo.</span><span class="sxs-lookup"><span data-stu-id="32ee9-120">In this step, you create an Azure web app and deploy your sample ASP.NET application tooit.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="32ee9-121">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="32ee9-121">Create a resource group</span></span>   
<span data-ttu-id="32ee9-122">Use [criar grupo az](https://docs.microsoft.com/cli/azure/group#create) toocreate um [grupo de recursos](../azure-resource-manager/resource-group-overview.md) na região Europa Ocidental de saudação.</span><span class="sxs-lookup"><span data-stu-id="32ee9-122">Use [az group create](https://docs.microsoft.com/cli/azure/group#create) toocreate a [resource group](../azure-resource-manager/resource-group-overview.md) in hello West Europe region.</span></span> <span data-ttu-id="32ee9-123">Um grupo de recursos é onde você coloca todos os Olá recursos do Azure que você deseja toomanage juntos, como Olá web app e qualquer banco de dados SQL back-end.</span><span class="sxs-lookup"><span data-stu-id="32ee9-123">A resource group is where you put all hello Azure resources that you want toomanage together, such as hello web app and any SQL Database back end.</span></span>

```azurecli
az group create --location "West Europe" --name myResourceGroup
```

<span data-ttu-id="32ee9-124">toosee quais possíveis valores que você podem usar para `---location`, use Olá [locais de lista do serviço de aplicativo az](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) comando.</span><span class="sxs-lookup"><span data-stu-id="32ee9-124">toosee what possible values you can use for `---location`, use hello [az appservice list-locations](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="32ee9-125">Criar um plano de Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="32ee9-125">Create an App Service plan</span></span>
<span data-ttu-id="32ee9-126">Use [criar plano de serviço de aplicativo az](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) toocreate "B1" [plano de serviço de aplicativo](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="32ee9-126">Use [az appservice plan create](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) toocreate a "B1" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

```azurecli
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1
```

<span data-ttu-id="32ee9-127">Um plano de serviço de aplicativo é uma unidade de escala, o que pode incluir qualquer número de aplicativos que você deseja tooscale backup ou out junto over Olá mesmo infraestrutura de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="32ee9-127">An App Service plan is a scale unit, which can include any number of apps that you want tooscale up or out together over hello same App Service infrastructure.</span></span> <span data-ttu-id="32ee9-128">Cada plano também recebe um [tipo de preço](https://azure.microsoft.com/en-us/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="32ee9-128">Each plan is also assigned a [pricing tier](https://azure.microsoft.com/en-us/pricing/details/app-service/).</span></span> <span data-ttu-id="32ee9-129">Tipos mais alto incluem hardware melhor e mais recursos, como mais instâncias de escala horizontal.</span><span class="sxs-lookup"><span data-stu-id="32ee9-129">Higher tiers include better hardware and more features, such as more scale-out instances.</span></span>

<span data-ttu-id="32ee9-130">Para este tutorial, B1 é Olá mínimo de camada que permite que instâncias toothree em expansão.</span><span class="sxs-lookup"><span data-stu-id="32ee9-130">For this tutorial, B1 is hello minimum tier that enables scale out toothree instances.</span></span> <span data-ttu-id="32ee9-131">Você sempre pode mover seu aplicativo para cima ou para baixo Olá preço posteriormente, executando [atualização de plano de serviço de aplicativo az](https://docs.microsoft.com/cli/azure/appservice/plan#update).</span><span class="sxs-lookup"><span data-stu-id="32ee9-131">You can always move your app up or down hello pricing tier later by running [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update).</span></span> 

### <a name="create-a-web-app"></a><span data-ttu-id="32ee9-132">Criar um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="32ee9-132">Create a web app</span></span>
<span data-ttu-id="32ee9-133">Use [web do serviço de aplicativo az criar](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate um aplicativo web com um nome exclusivo no `$appName`.</span><span class="sxs-lookup"><span data-stu-id="32ee9-133">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate a web app with a unique name in `$appName`.</span></span>

```azurecli
$appName = "<replace-with-a-unique-name>"
az appservice web create --name $appName --resource-group myResourceGroup --plan myAppServicePlan
```

### <a name="set-deployment-credentials"></a><span data-ttu-id="32ee9-134">Definir credenciais de implantação</span><span class="sxs-lookup"><span data-stu-id="32ee9-134">Set deployment credentials</span></span>
<span data-ttu-id="32ee9-135">Use [usuário de implantação da web do serviço de aplicativo de az definido](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) tooset credenciais de sua implantação do nível de conta de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="32ee9-135">Use [az appservice web deployment user set](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) tooset your account-level deployment credentials for App Service.</span></span>

```azurecli
az appservice web deployment user set --user-name <letters-numbers> --password <mininum-8-char-captital-lowercase-letters-numbers>
```

### <a name="configure-git-deployment"></a><span data-ttu-id="32ee9-136">Configurar a implantação do Git</span><span class="sxs-lookup"><span data-stu-id="32ee9-136">Configure Git deployment</span></span>
<span data-ttu-id="32ee9-137">Use [controle de origem de web do serviço de aplicativo de az-config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure implantação local do Git.</span><span class="sxs-lookup"><span data-stu-id="32ee9-137">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure local Git deployment.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName --resource-group myResourceGroup
```

<span data-ttu-id="32ee9-138">Esse comando fornece uma saída semelhante à seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="32ee9-138">This command gives you an output that looks like hello following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="32ee9-139">Olá Use retornado URL tooconfigure o Git remoto.</span><span class="sxs-lookup"><span data-stu-id="32ee9-139">Use hello returned URL tooconfigure your Git remote.</span></span> <span data-ttu-id="32ee9-140">Olá comando a seguir usa Olá precede o exemplo de saída.</span><span class="sxs-lookup"><span data-stu-id="32ee9-140">hello following command uses hello preceding output example.</span></span>

```powershell
git remote add azure https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-hello-sample-application"></a><span data-ttu-id="32ee9-141">Implantar o aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="32ee9-141">Deploy hello sample application</span></span>
<span data-ttu-id="32ee9-142">Você está agora pronto toodeploy o aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="32ee9-142">You are now ready toodeploy your sample application.</span></span> <span data-ttu-id="32ee9-143">Execute `git push`.</span><span class="sxs-lookup"><span data-stu-id="32ee9-143">Run `git push`.</span></span>

```powershell
git push azure master
```

<span data-ttu-id="32ee9-144">Quando solicitado para a senha, use senha Olá que você especificou quando executou `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="32ee9-144">When prompted for password, use hello password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-tooazure-web-app"></a><span data-ttu-id="32ee9-145">Procurar o aplicativo web de tooAzure</span><span class="sxs-lookup"><span data-stu-id="32ee9-145">Browse tooAzure web app</span></span>
<span data-ttu-id="32ee9-146">Use [procurar de web do serviço de aplicativo az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee seu aplicativo em execução no Azure, execute este comando.</span><span class="sxs-lookup"><span data-stu-id="32ee9-146">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee your app running live in Azure, run this command.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-3---connect-tooredis"></a><span data-ttu-id="32ee9-147">Etapa 3 - conectar tooRedis</span><span class="sxs-lookup"><span data-stu-id="32ee9-147">Step 3 - Connect tooRedis</span></span>
<span data-ttu-id="32ee9-148">Nesta etapa, você configura o Cache Redis do Azure como um aplicativo de web do Azure tooyour cache externo e colocados.</span><span class="sxs-lookup"><span data-stu-id="32ee9-148">In this step, you set up Azure Redis Cache as an external, colocated cache tooyour Azure web app.</span></span> <span data-ttu-id="32ee9-149">Você pode rapidamente utilizar toocache Redis a saída de página.</span><span class="sxs-lookup"><span data-stu-id="32ee9-149">You can quickly utilize Redis toocache your page output.</span></span> <span data-ttu-id="32ee9-150">Além disso, ao escalar horizontalmente os aplicativos Web posteriormente, o Redis ajuda a persistir as sessões do usuário em várias instâncias de modo confiável.</span><span class="sxs-lookup"><span data-stu-id="32ee9-150">In addition, when you scale out your web apps later, Redis helps you persist user sessions across multiple instances reliably.</span></span>

### <a name="create-an-azure-redis-cache"></a><span data-ttu-id="32ee9-151">Criar um Cache Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="32ee9-151">Create an Azure Redis Cache</span></span>
<span data-ttu-id="32ee9-152">Use [redis az criar](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate um Azure Redis Cache e salvar Olá JSON de saída.</span><span class="sxs-lookup"><span data-stu-id="32ee9-152">Use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate an Azure Redis Cache and save hello JSON output.</span></span> <span data-ttu-id="32ee9-153">Use um nome exclusivo em `$cacheName`.</span><span class="sxs-lookup"><span data-stu-id="32ee9-153">Use a unique name in `$cacheName`.</span></span>

```powershell
$cacheName = "<replace-with-a-unique-cache-name>"
$redis = (az redis create --name $cacheName --resource-group myResourceGroup --location "West Europe" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

### <a name="configure-hello-application-toouse-redis"></a><span data-ttu-id="32ee9-154">Configurar Olá aplicativo toouse Redis</span><span class="sxs-lookup"><span data-stu-id="32ee9-154">Configure hello application toouse Redis</span></span>
<span data-ttu-id="32ee9-155">Formato de cadeia de caracteres de conexão de saudação para seu cache.</span><span class="sxs-lookup"><span data-stu-id="32ee9-155">Format hello connection string for your cache.</span></span>

```powershell
$connstring = "$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False"
$connstring 
```

<span data-ttu-id="32ee9-156">segunda linha de saudação deve fornecer uma saída parecida com esta:</span><span class="sxs-lookup"><span data-stu-id="32ee9-156">hello second line should give you an output that looks like this:</span></span>

```
mycachename.redis.cache.windows.net:6380,password=/rQP/TLz1mrEPpmh9b/gnfns/t9vBRXqXn3i1RwBjGA=,ssl=True,abortConnect=False
```

<span data-ttu-id="32ee9-157">No Visual Studio, crie um arquivo de configuração da web em sua raiz de projeto chamado `redis.config` e colar Olá seguindo o código para ele.</span><span class="sxs-lookup"><span data-stu-id="32ee9-157">In Visual Studio, create a web configuration file in your project root called `redis.config` and paste hello following code into it.</span></span> <span data-ttu-id="32ee9-158">Em `value`, use a cadeia de conexão de saudação do hello saída do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="32ee9-158">In `value`, use hello connection string from hello PowerShell output.</span></span>

```xml
<appSettings>
  <add key="RedisConnection" value="your-azure-redis-cache-connection-string"/>
</appSettings>
```

<span data-ttu-id="32ee9-159">Se você observar Olá `.gitignore` arquivo no seu repositório Git, você verá que esse arquivo é excluído do controle de origem.</span><span class="sxs-lookup"><span data-stu-id="32ee9-159">If you look at hello `.gitignore` file in your Git repository, you'll see that this file is excluded from source control.</span></span> <span data-ttu-id="32ee9-160">Dessa forma, as informações confidenciais são mantidas em segurança.</span><span class="sxs-lookup"><span data-stu-id="32ee9-160">That way your sensitive information is kept safe.</span></span> 

<span data-ttu-id="32ee9-161">Abra `Web.config`.</span><span class="sxs-lookup"><span data-stu-id="32ee9-161">Open `Web.config`.</span></span> <span data-ttu-id="32ee9-162">Saudação de aviso `<appSettings file="redis.config">` elemento, que obtém a configuração de saudação criado no `redis.config`.</span><span class="sxs-lookup"><span data-stu-id="32ee9-162">Notice hello `<appSettings file="redis.config">` element, which gets hello setting you created in `redis.config`.</span></span> 

<span data-ttu-id="32ee9-163">Localizar Olá comentado seção inclui `<sessionState>` e `<caching>`.</span><span class="sxs-lookup"><span data-stu-id="32ee9-163">Find hello commented section that includes `<sessionState>` and `<caching>`.</span></span> <span data-ttu-id="32ee9-164">Remova os comentários dessa seção.</span><span class="sxs-lookup"><span data-stu-id="32ee9-164">Uncomment this section.</span></span>

![](./media/app-service-web-tutorial-hyper-scale-app/redisproviders.png)

<span data-ttu-id="32ee9-165">Esse código procura por cadeia de caracteres de conexão de Redis Olá você definiu no `RedisConnection`.</span><span class="sxs-lookup"><span data-stu-id="32ee9-165">This code looks for hello Redis connection string you defined in `RedisConnection`.</span></span> 

<span data-ttu-id="32ee9-166">Seu aplicativo agora usa Redis toomanage sessões e armazenamento em cache.</span><span class="sxs-lookup"><span data-stu-id="32ee9-166">Your application now uses Redis toomanage sessions and caching.</span></span> <span data-ttu-id="32ee9-167">Tipo `F5` toorun aplicativo de hello.</span><span class="sxs-lookup"><span data-stu-id="32ee9-167">Type `F5` toorun hello application.</span></span> <span data-ttu-id="32ee9-168">Se desejar, você pode baixar dados Olá um Redis gerenciamento cliente toovisualize agora salvo toohello cache.</span><span class="sxs-lookup"><span data-stu-id="32ee9-168">If you like, you can download a Redis management client toovisualize hello data that is now saved toohello cache.</span></span>

### <a name="configure-hello-connection-string-in-azure"></a><span data-ttu-id="32ee9-169">Configurar a cadeia de caracteres de conexão Olá no Azure</span><span class="sxs-lookup"><span data-stu-id="32ee9-169">Configure hello connection string in Azure</span></span>

<span data-ttu-id="32ee9-170">Para toowork seu aplicativo no Azure, você precisa tooconfigure Olá a mesma cadeia de conexão do Redis em seu aplicativo web do Azure.</span><span class="sxs-lookup"><span data-stu-id="32ee9-170">For your application toowork in Azure, you need tooconfigure hello same Redis connection string in your Azure web app.</span></span> <span data-ttu-id="32ee9-171">Como `redis.config` é mantida no controle de origem, não é implantado tooAzure quando você executa a implantação do Git.</span><span class="sxs-lookup"><span data-stu-id="32ee9-171">Since `redis.config` is not maintained in source control, it is not deployed tooAzure when you run Git deployment.</span></span>

<span data-ttu-id="32ee9-172">Use [az serviço de aplicativo web configuração appsettings atualizar](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) cadeia de conexão de saudação tooadd com hello mesmo nome (`RedisConnection`).</span><span class="sxs-lookup"><span data-stu-id="32ee9-172">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd hello connection string with hello same name (`RedisConnection`).</span></span>

<span data-ttu-id="32ee9-173">az appservice web config appsettings update --settings "RedisConnection=$connstring" --name $appName --resource-group myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="32ee9-173">az appservice web config appsettings update --settings "RedisConnection=$connstring" --name $appName --resource-group myResourceGroup</span></span>

<span data-ttu-id="32ee9-174">Lembre-se de que `$connstring` contém a cadeia de caracteres de conexão de saudação formatada.</span><span class="sxs-lookup"><span data-stu-id="32ee9-174">Remember that `$connstring` contains hello formatted connection string.</span></span>

### <a name="redeploy-hello-application-tooazure"></a><span data-ttu-id="32ee9-175">Reimplantar Olá aplicativo tooAzure</span><span class="sxs-lookup"><span data-stu-id="32ee9-175">Redeploy hello application tooAzure</span></span>
<span data-ttu-id="32ee9-176">Use Git comandos toopush tooAzure suas alterações</span><span class="sxs-lookup"><span data-stu-id="32ee9-176">Use Git commands toopush your changes tooAzure</span></span>

```bash
git add .
git commit -m "now use Redis providers"
git push azure master
```

<span data-ttu-id="32ee9-177">Quando solicitado para a senha, use senha Olá que você especificou quando executou `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="32ee9-177">When prompted for password, use hello password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="32ee9-178">Procurar o aplicativo web do Azure de toohello</span><span class="sxs-lookup"><span data-stu-id="32ee9-178">Browse toohello Azure web app</span></span>
<span data-ttu-id="32ee9-179">Use [procurar de web do serviço de aplicativo az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) alterações de saudação toosee ao vivo no Azure.</span><span class="sxs-lookup"><span data-stu-id="32ee9-179">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee hello changes live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-4---scale-toomultiple-instances"></a><span data-ttu-id="32ee9-180">Etapa 4 - instâncias de toomultiple de escala</span><span class="sxs-lookup"><span data-stu-id="32ee9-180">Step 4 - Scale toomultiple instances</span></span>
<span data-ttu-id="32ee9-181">Olá plano de serviço de aplicativo é a unidade de escala de saudação para seus aplicativos web do Azure.</span><span class="sxs-lookup"><span data-stu-id="32ee9-181">hello App Service plan is hello scale unit for your Azure web apps.</span></span> <span data-ttu-id="32ee9-182">tooscale-out do seu aplicativo web, você dimensionar Olá plano de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="32ee9-182">tooscale out your web app, you scale hello App Service plan.</span></span>

<span data-ttu-id="32ee9-183">Use [atualização de plano de serviço de aplicativo az](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale as instâncias de toothree do plano do serviço de aplicativo hello, que é Olá número máximo permitido pelo Olá B1 preço.</span><span class="sxs-lookup"><span data-stu-id="32ee9-183">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale out hello App Service plan toothree instances, which is hello maximum number allowed by hello B1 pricing tier.</span></span> <span data-ttu-id="32ee9-184">Lembre-se de que B1 é hello preço que você escolheu quando criou Olá anteriormente plano de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="32ee9-184">Remember that B1 is hello pricing tier that you chose when you created hello App Service plan earlier.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --number-of-workers 3 
```

## <a name="step-5---scale-geographically"></a><span data-ttu-id="32ee9-185">Etapa 5 – Escalar geograficamente</span><span class="sxs-lookup"><span data-stu-id="32ee9-185">Step 5 - Scale geographically</span></span>
<span data-ttu-id="32ee9-186">Ao dimensionar geograficamente, executar seu aplicativo em várias regiões de saudação nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="32ee9-186">When scaling geographically, you run your app in multiple regions of hello Azure cloud.</span></span> <span data-ttu-id="32ee9-187">Esta instalação fornece balanceamento de carga seu aplicativo ainda mais com base na geografia e reduz o tempo de resposta de saudação colocando os navegadores tooclient mais próximos do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="32ee9-187">This setup load-balances your app further based on geography and lowers hello response time by placing your app closer tooclient browsers.</span></span>

<span data-ttu-id="32ee9-188">Nesta etapa, você dimensionar o ASP.NET web aplicativo tooa segunda região com [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/).</span><span class="sxs-lookup"><span data-stu-id="32ee9-188">In this step, you scale your ASP.NET web app tooa second region with [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/).</span></span> <span data-ttu-id="32ee9-189">No final da saudação da etapa Olá, você terá um aplicativo web em execução na Europa Ocidental (já criado) e um aplicativo web em execução no sudeste da Ásia (ainda não foi criado).</span><span class="sxs-lookup"><span data-stu-id="32ee9-189">At hello end of hello step, you will have a web app running in West Europe (already created) and a web app running in Southeast Asia (not yet created).</span></span> <span data-ttu-id="32ee9-190">Ambos os aplicativos serão atendidos a partir Olá mesmo URL do Gerenciador de tráfego.</span><span class="sxs-lookup"><span data-stu-id="32ee9-190">Both apps will be served from hello same Traffic Manager URL.</span></span>

### <a name="scale-up-hello-europe-app-toostandard-tier"></a><span data-ttu-id="32ee9-191">Dimensionar o hello da camada de tooStandard de aplicativo Europa</span><span class="sxs-lookup"><span data-stu-id="32ee9-191">Scale up hello Europe app tooStandard tier</span></span>
<span data-ttu-id="32ee9-192">No serviço de aplicativo, integração com o Azure Traffic Manager requer saudação padrão de preço.</span><span class="sxs-lookup"><span data-stu-id="32ee9-192">In App Service, integration with Azure Traffic Manager requires hello Standard pricing tier.</span></span> <span data-ttu-id="32ee9-193">Use [atualização de plano de serviço de aplicativo az](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale backup seu tooS1 de plano de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="32ee9-193">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale up your App Service plan tooS1.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --sku S1
```
### <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="32ee9-194">Criar um perfil do Gerenciador de Tráfego</span><span class="sxs-lookup"><span data-stu-id="32ee9-194">Create a Traffic Manager profile</span></span> 
<span data-ttu-id="32ee9-195">Use [criar perfil do Gerenciador de tráfego de rede az](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) toocreate um Gerenciador de tráfego de perfil e adicioná-lo tooyour grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="32ee9-195">Use [az network traffic-manager profile create](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) toocreate a Traffic Manager profile and add it tooyour resource group.</span></span> <span data-ttu-id="32ee9-196">Use um nome DNS exclusivo em $dnsName.</span><span class="sxs-lookup"><span data-stu-id="32ee9-196">Use a unique DNS name in $dnsName.</span></span>

```azurecli
$dnsName = "<replace-with-unique-dns-name>"
az network traffic-manager profile create --name myTrafficManagerProfile --resource-group myResourceGroup --routing-method Performance --unique-dns-name $dnsName
```

> [!NOTE]
> <span data-ttu-id="32ee9-197">`--routing-method Performance`Especifica que este perfil [roteia a extremidade mais próxima do usuário tráfego toohello](../traffic-manager/traffic-manager-routing-methods.md).</span><span class="sxs-lookup"><span data-stu-id="32ee9-197">`--routing-method Performance` specifies that this profile [routes user traffic toohello closest endpoint](../traffic-manager/traffic-manager-routing-methods.md).</span></span>

### <a name="get-hello-resource-id-of-hello-europe-app"></a><span data-ttu-id="32ee9-198">Obter a ID de recursos de saudação do aplicativo do hello Europa</span><span class="sxs-lookup"><span data-stu-id="32ee9-198">Get hello resource ID of hello Europe app</span></span>
<span data-ttu-id="32ee9-199">Use [Mostrar de web do serviço de aplicativo az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget Olá ID de recurso de seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="32ee9-199">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget hello resource ID of your web app.</span></span>

```azurecli
$appId = az appservice web show --name $appName --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-europe-app"></a><span data-ttu-id="32ee9-200">Adicionar um ponto de extremidade do Gerenciador de tráfego para o aplicativo de Europa Olá</span><span class="sxs-lookup"><span data-stu-id="32ee9-200">Add a Traffic Manager endpoint for hello Europe app</span></span>
<span data-ttu-id="32ee9-201">Use [criar ponto de extremidade de Gerenciador de tráfego de rede az](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd tooyour um ponto de extremidade perfil do Gerenciador de tráfego e uso Olá ID de recurso de seu aplicativo web como Olá destino.</span><span class="sxs-lookup"><span data-stu-id="32ee9-201">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd an endpoint tooyour Traffic Manager profile and use hello resource ID of your web app as hello target.</span></span>

```azurecli
az network traffic-manager endpoint create --name myWestEuropeEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appId
```

### <a name="get-hello-traffic-manager-endpoint-url"></a><span data-ttu-id="32ee9-202">Obter URL de ponto de extremidade do Traffic Manager Olá</span><span class="sxs-lookup"><span data-stu-id="32ee9-202">Get hello Traffic Manager endpoint URL</span></span>
<span data-ttu-id="32ee9-203">Perfil do Traffic Manager agora tem um ponto de extremidade de aplicativo da web existente que pontos tooyour.</span><span class="sxs-lookup"><span data-stu-id="32ee9-203">Your Traffic Manager profile now has an endpoint that points tooyour existing web app.</span></span> <span data-ttu-id="32ee9-204">Use [Mostrar de perfil de Gerenciador de tráfego de rede az](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) tooget sua URL.</span><span class="sxs-lookup"><span data-stu-id="32ee9-204">Use [az network traffic-manager profile show](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) tooget its URL.</span></span> 

```azurecli
az network traffic-manager profile show --name myTrafficManagerProfile --resource-group myResourceGroup --query dnsConfig.fqdn --output tsv
```

<span data-ttu-id="32ee9-205">Copie saída de hello no seu navegador.</span><span class="sxs-lookup"><span data-stu-id="32ee9-205">Copy hello output into your browser.</span></span> <span data-ttu-id="32ee9-206">Você deve ver o aplicativo Web novamente.</span><span class="sxs-lookup"><span data-stu-id="32ee9-206">You should see your web app again.</span></span>

### <a name="create-an-azure-redis-cache-in-asia"></a><span data-ttu-id="32ee9-207">Criar um Cache Redis do Azure na Ásia</span><span class="sxs-lookup"><span data-stu-id="32ee9-207">Create an Azure Redis Cache in Asia</span></span>
<span data-ttu-id="32ee9-208">Agora, você pode replicar sua região Sudeste da Ásia de toohello de aplicativo de web do Azure.</span><span class="sxs-lookup"><span data-stu-id="32ee9-208">Now, you replicate your Azure web app toohello Southeast Asia region.</span></span> <span data-ttu-id="32ee9-209">toostart, use [redis az criar](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate um segundo Azure Redis Cache do Sudeste da Ásia.</span><span class="sxs-lookup"><span data-stu-id="32ee9-209">toostart, use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate a second Azure Redis Cache in Southeast Asia.</span></span> <span data-ttu-id="32ee9-210">Esse cache precisa toobe posicionada com seu aplicativo na Ásia.</span><span class="sxs-lookup"><span data-stu-id="32ee9-210">This cache needs toobe colocated with your app in Asia.</span></span>

```powershell
$redis = (az redis create --name $cacheName-asia --resource-group myResourceGroup --location "Southeast Asia" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

<span data-ttu-id="32ee9-211">`--name $cacheName-asia`Fornece Olá nome de saudação do cache de saudação cache Europa Ocidental, Olá `-asia` sufixo.</span><span class="sxs-lookup"><span data-stu-id="32ee9-211">`--name $cacheName-asia` gives hello cache hello name of hello West Europe cache, with hello `-asia` suffix.</span></span>

### <a name="create-an-app-service-plan-in-asia"></a><span data-ttu-id="32ee9-212">Criar um plano do Serviço de Aplicativo na Ásia</span><span class="sxs-lookup"><span data-stu-id="32ee9-212">Create an App Service plan in Asia</span></span>
<span data-ttu-id="32ee9-213">Use [criar plano de serviço de aplicativo az](https://docs.microsoft.com/cli/azure/appservice/plan#create) toocreate um segundo serviço de aplicativo planejar na região do Sudeste Asiático hello, usando Olá S1 mesmo nível como plano de Ocidental hello.</span><span class="sxs-lookup"><span data-stu-id="32ee9-213">Use [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) toocreate a second App Service plan in hello Southeast Asia region, using hello same S1 tier as hello West Europe plan.</span></span>

```azurecli
az appservice plan create --name myAppServicePlanAsia --resource-group myResourceGroup --location "Southeast Asia" --sku S1
```

### <a name="create-a-web-app-in-asia"></a><span data-ttu-id="32ee9-214">Criar um aplicativo Web na Ásia</span><span class="sxs-lookup"><span data-stu-id="32ee9-214">Create a web app in Asia</span></span>
<span data-ttu-id="32ee9-215">Use [web do serviço de aplicativo az criar](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate um segundo aplicativo de web.</span><span class="sxs-lookup"><span data-stu-id="32ee9-215">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate a second web app.</span></span>

```azurecli
az appservice web create --name $appName-asia --resource-group myResourceGroup --plan myAppServicePlanAsia
```

<span data-ttu-id="32ee9-216">`--name $appName-asia`Fornece Olá nome do aplicativo Olá Olá Ocidental aplicativo, com hello `-asia` sufixo.</span><span class="sxs-lookup"><span data-stu-id="32ee9-216">`--name $appName-asia` gives hello app hello name of hello West Europe app, with hello `-asia` suffix.</span></span>

### <a name="configure-hello-connection-string-for-redis"></a><span data-ttu-id="32ee9-217">Configurar a cadeia de caracteres de conexão Olá para Redis</span><span class="sxs-lookup"><span data-stu-id="32ee9-217">Configure hello connection string for Redis</span></span>
<span data-ttu-id="32ee9-218">Use [az serviço de aplicativo web configuração appsettings atualizar](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd toohello web aplicativo Olá conexão string hello cache Sudeste da Ásia.</span><span class="sxs-lookup"><span data-stu-id="32ee9-218">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd toohello web app hello connection string for hello Southeast Asia cache.</span></span>

<span data-ttu-id="32ee9-219">az appservice web config appsettings update --settings "RedisConnection=$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False" --name $appName-asia --resource-group myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="32ee9-219">az appservice web config appsettings update --settings "RedisConnection=$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False" --name $appName-asia --resource-group myResourceGroup</span></span>

### <a name="configure-git-deployment-for-hello-asia-app"></a><span data-ttu-id="32ee9-220">Configure a implantação de Git para o aplicativo do hello Ásia.</span><span class="sxs-lookup"><span data-stu-id="32ee9-220">Configure Git deployment for hello Asia app.</span></span>
<span data-ttu-id="32ee9-221">Use [controle de origem de web do serviço de aplicativo de az-config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure implantação do Git local para o aplicativo web da segunda hello.</span><span class="sxs-lookup"><span data-stu-id="32ee9-221">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure local Git deployment for hello second web app.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="32ee9-222">Esse comando fornece uma saída semelhante à seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="32ee9-222">This command gives you an output that looks like hello following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="32ee9-223">Olá Use retornado tooconfigure URL uma segunda Git remoto para seu repositório local.</span><span class="sxs-lookup"><span data-stu-id="32ee9-223">Use hello returned URL tooconfigure a second Git remote for your local repository.</span></span> <span data-ttu-id="32ee9-224">Olá comando a seguir usa Olá precede o exemplo de saída.</span><span class="sxs-lookup"><span data-stu-id="32ee9-224">hello following command uses hello preceding output example.</span></span>

```bash
git remote add azure-asia https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-your-sample-application"></a><span data-ttu-id="32ee9-225">Implantar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="32ee9-225">Deploy your sample application</span></span>
<span data-ttu-id="32ee9-226">Executar `git push` toodeploy exemplo aplicativo toohello segundo Git remoto.</span><span class="sxs-lookup"><span data-stu-id="32ee9-226">Run `git push` toodeploy your sample application toohello second Git remote.</span></span> 

```bash
git push azure-asia master
```

<span data-ttu-id="32ee9-227">Quando solicitado para a senha, use senha Olá que você especificou quando executou `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="32ee9-227">When prompted for password, use hello password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-toohello-asia-app"></a><span data-ttu-id="32ee9-228">Procurar toohello Ásia aplicativo</span><span class="sxs-lookup"><span data-stu-id="32ee9-228">Browse toohello Asia app</span></span>
<span data-ttu-id="32ee9-229">Use [procurar de web do serviço de aplicativo az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) tooverify que seu aplicativo está em execução ao vivo no Azure.</span><span class="sxs-lookup"><span data-stu-id="32ee9-229">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) tooverify that your app is running live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName-asia --resource-group myResourceGroup
```

### <a name="get-hello-resource-id-of-hello-asia-app"></a><span data-ttu-id="32ee9-230">Obter a ID de recursos de saudação do hello Ásia aplicativo</span><span class="sxs-lookup"><span data-stu-id="32ee9-230">Get hello resource ID of hello Asia app</span></span>
<span data-ttu-id="32ee9-231">Use [Mostrar de web do serviço de aplicativo az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget Olá ID de recurso de seu aplicativo web do Sudeste da Ásia.</span><span class="sxs-lookup"><span data-stu-id="32ee9-231">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget hello resource ID of your web app in Southeast Asia.</span></span>

```azurecli
$appIdAsia = az appservice web show --name $appName-asia --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-asia-app"></a><span data-ttu-id="32ee9-232">Adicionar um ponto de extremidade do Gerenciador de tráfego para o aplicativo de Ásia Olá</span><span class="sxs-lookup"><span data-stu-id="32ee9-232">Add a Traffic Manager endpoint for hello Asia app</span></span>
<span data-ttu-id="32ee9-233">Use [criar ponto de extremidade de Gerenciador de tráfego de rede az](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd um segundo toohello de ponto de extremidade perfil do Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="32ee9-233">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd a second endpoint toohello Traffic Manager profile.</span></span>

```azurecli
az network traffic-manager endpoint create --name myAsiaEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appIdAsia
```

### <a name="add-region-identifier-tooweb-apps"></a><span data-ttu-id="32ee9-234">Adicionar aplicativos de tooweb de identificador de região</span><span class="sxs-lookup"><span data-stu-id="32ee9-234">Add region identifier tooweb apps</span></span>
<span data-ttu-id="32ee9-235">Use [az serviço de aplicativo web configuração appsettings atualizar](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd uma variável de ambiente específicas da região.</span><span class="sxs-lookup"><span data-stu-id="32ee9-235">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd a region-specific environment variable.</span></span>

```azurecli
az appservice web config appsettings update --settings "Region=West Europe" --name $appName --resource-group myResourceGroup
az appservice web config appsettings update --settings "Region=Southeast Asia" --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="32ee9-236">O código do seu aplicativo já usa essa configuração de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="32ee9-236">Your application code already uses this application setting.</span></span> <span data-ttu-id="32ee9-237">Observe `HighScaleApp\Views\Home\Index.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="32ee9-237">Take a look at `HighScaleApp\Views\Home\Index.cshtml`.</span></span>

### <a name="complete"></a><span data-ttu-id="32ee9-238">Concluído!</span><span class="sxs-lookup"><span data-stu-id="32ee9-238">Complete!</span></span>

<span data-ttu-id="32ee9-239">Agora, tente tooaccess Olá URL do seu perfil do Gerenciador de tráfego de navegadores em regiões geográficas diferentes.</span><span class="sxs-lookup"><span data-stu-id="32ee9-239">Now, try tooaccess hello URL of your Traffic Manager profile from browsers in different geographical regions.</span></span> <span data-ttu-id="32ee9-240">Os navegadores cliente da Europa devem mostrar "ASP.NET Europa Ocidental" e o navegador cliente da Ásia deve mostrar "ASP.NET Sudeste Asiático".</span><span class="sxs-lookup"><span data-stu-id="32ee9-240">Client browsers from Europe should show "ASP.NET West Europe", and client browser from Asia should show "ASP.NET Southeast Asia."</span></span>

## <a name="more-resources"></a><span data-ttu-id="32ee9-241">Mais recursos</span><span class="sxs-lookup"><span data-stu-id="32ee9-241">More resources</span></span>
