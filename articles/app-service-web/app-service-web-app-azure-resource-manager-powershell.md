---
title: aaaAzure PowerShell com base no Gerenciador de recursos de comandos para o aplicativo Web do Azure | Microsoft Docs
description: "Saiba como toouse Olá toomanage novo de comandos PowerShell do Azure Resource Manager com base em seus aplicativos da Web do Azure."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 4231fbba-61e5-4f92-b958-531c066fb87f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: bbb821e89daa315280436e84e11316217bb644d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-powershell-toomanage-azure-web-apps"></a><span data-ttu-id="97fdd-103">Usando aplicativos de Web do Azure PowerShell Azure Resource Manager-Based tooManage</span><span class="sxs-lookup"><span data-stu-id="97fdd-103">Using Azure Resource Manager-Based PowerShell tooManage Azure Web Apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="97fdd-104">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="97fdd-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="97fdd-105">PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="97fdd-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
> 
> 

<span data-ttu-id="97fdd-106">Com o Microsoft Azure PowerShell versão 1.0.0 foram adicionados novos comandos, que fornecem Olá usuário Olá capacidade toouse com base no Gerenciador de recursos do Azure PowerShell comandos toomanage aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="97fdd-106">With Microsoft Azure PowerShell version 1.0.0 new commands have been added, that give hello user hello ability toouse Azure Resource Manager-based PowerShell commands toomanage Web Apps.</span></span>

<span data-ttu-id="97fdd-107">toolearn sobre o gerenciamento de grupos de recursos, consulte [usando o PowerShell do Azure com o Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="97fdd-107">toolearn about managing Resource Groups, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span> 

<span data-ttu-id="97fdd-108">toolearn sobre a lista completa de saudação de parâmetros e as opções de saudação cmdlets do PowerShell, consulte Olá [completo referência do Cmdlet baseado em Web aplicativo do Azure Resource Manager de Cmdlets do PowerShell](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="97fdd-108">toolearn about hello full list of parameters and options for hello PowerShell cmdlets, see hello [full Cmdlet Reference of Web App Azure Resource Manager-based PowerShell Cmdlets](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>

## <a name="managing-app-service-plans"></a><span data-ttu-id="97fdd-109">Gerenciando Planos do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="97fdd-109">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="97fdd-110">Criar um Plano do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="97fdd-110">Create an App Service Plan</span></span>
<span data-ttu-id="97fdd-111">toocreate um plano de serviço de aplicativo, use Olá **AzureRmAppServicePlan novo** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="97fdd-111">toocreate an app service plan, use hello **New-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="97fdd-112">Seguem as descrições dos parâmetros diferentes hello:</span><span class="sxs-lookup"><span data-stu-id="97fdd-112">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="97fdd-113">**Nome**: nome do plano de serviço de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="97fdd-113">**Name**: name of hello app service plan.</span></span>
* <span data-ttu-id="97fdd-114">**Local**: a localização do plano do serviço.</span><span class="sxs-lookup"><span data-stu-id="97fdd-114">**Location**: service plan location.</span></span>
* <span data-ttu-id="97fdd-115">**ResourceGroupName**: grupo de recursos que inclui o plano de serviço de aplicativo hello recém-criado.</span><span class="sxs-lookup"><span data-stu-id="97fdd-115">**ResourceGroupName**: resource group that includes hello newly created app service plan.</span></span>
* <span data-ttu-id="97fdd-116">**Camada**: Olá desejado de preço (o padrão é gratuito, outras opções são compartilhados, Basic, Standard e Premium).</span><span class="sxs-lookup"><span data-stu-id="97fdd-116">**Tier**:  hello desired pricing tier (Default is Free, other options are Shared, Basic, Standard, and Premium.)</span></span>
* <span data-ttu-id="97fdd-117">**WorkerSize**: Olá tamanho de trabalhadores (o padrão é pequeno se o parâmetro de camada de saudação foi especificado como Basic, Standard ou Premium.</span><span class="sxs-lookup"><span data-stu-id="97fdd-117">**WorkerSize**: hello size of workers (Default is small if hello Tier parameter was specified as Basic, Standard, or Premium.</span></span> <span data-ttu-id="97fdd-118">Outras opções são Médio e Grande.)</span><span class="sxs-lookup"><span data-stu-id="97fdd-118">Other options are Medium, and Large.)</span></span>
* <span data-ttu-id="97fdd-119">**NumberofWorkers**: Olá número de trabalhadores no plano de serviço de aplicativo hello (o valor padrão é 1).</span><span class="sxs-lookup"><span data-stu-id="97fdd-119">**NumberofWorkers**: hello number of workers in hello app service plan (Default value is 1).</span></span> 

<span data-ttu-id="97fdd-120">Exemplo toouse esse cmdlet:</span><span class="sxs-lookup"><span data-stu-id="97fdd-120">Example toouse this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -Tier Premium -WorkerSize Large -NumberofWorkers 10

### <a name="create-an-app-service-plan-in-an-app-service-environment"></a><span data-ttu-id="97fdd-121">Criar um Plano do Serviço de Aplicativo em um Ambiente de Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="97fdd-121">Create an App Service Plan in an App Service Environment</span></span>
<span data-ttu-id="97fdd-122">plano de um aplicativo de serviço toocreate em um ambiente de serviço de aplicativo, use Olá mesmo comando **AzureRmAppServicePlan novo** com nome hello toospecify de parâmetros adicionais do ASE e o nome do grupo de recursos do ASE.</span><span class="sxs-lookup"><span data-stu-id="97fdd-122">toocreate an app service plan in an app service environment, use hello same command **New-AzureRmAppServicePlan** command with extra parameters toospecify hello ASE's name and ASE's resource group name.</span></span>

<span data-ttu-id="97fdd-123">Exemplo toouse esse cmdlet:</span><span class="sxs-lookup"><span data-stu-id="97fdd-123">Example toouse this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -AseName constosoASE -AseResourceGroupName contosoASERG -Tier Premium -WorkerSize Large -NumberofWorkers 10

<span data-ttu-id="97fdd-124">mais sobre o ambiente de serviço de aplicativo, seleção de toolearn [Introdução tooApp ambiente de serviço](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="97fdd-124">toolearn more about app service environment, check [Introduction tooApp Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="97fdd-125">Listar os Planos do Serviço de Aplicativo existentes</span><span class="sxs-lookup"><span data-stu-id="97fdd-125">List Existing App Service Plans</span></span>
<span data-ttu-id="97fdd-126">toolist Olá existente aplicativo planos de serviço, use **AzureRmAppServicePlan Get** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="97fdd-126">toolist hello existing app service plans, use **Get-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="97fdd-127">toolist todos os planos de serviço de aplicativo em sua assinatura, use:</span><span class="sxs-lookup"><span data-stu-id="97fdd-127">toolist all app service plans under your subscription, use:</span></span> 

    Get-AzureRmAppServicePlan

<span data-ttu-id="97fdd-128">toolist todos os planos de serviço de aplicativo em um grupo de recursos específico, use:</span><span class="sxs-lookup"><span data-stu-id="97fdd-128">toolist all app service plans under a specific resource group, use:</span></span>

    Get-AzureRmAppServicePlan -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="97fdd-129">tooget um plano de serviço de aplicativo específico, use:</span><span class="sxs-lookup"><span data-stu-id="97fdd-129">tooget a specific app service plan, use:</span></span>

    Get-AzureRmAppServicePlan -Name ContosoAppServicePlan


### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="97fdd-130">Configurar um Plano do Serviço de Aplicativo existente</span><span class="sxs-lookup"><span data-stu-id="97fdd-130">Configure an existing App Service Plan</span></span>
<span data-ttu-id="97fdd-131">configurações de saudação toochange para um plano de serviço de aplicativo existente, use Olá **AzureRmAppServicePlan conjunto** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="97fdd-131">toochange hello settings for an existing app service plan, use hello **Set-AzureRmAppServicePlan** cmdlet.</span></span> <span data-ttu-id="97fdd-132">Você pode alterar a camada Olá, tamanho do trabalho e número de saudação de trabalhos</span><span class="sxs-lookup"><span data-stu-id="97fdd-132">You can change hello tier, worker size, and hello number of workers</span></span> 

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard -WorkerSize Medium -NumberofWorkers 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="97fdd-133">Dimensionando um Plano do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="97fdd-133">Scaling an App Service Plan</span></span>
<span data-ttu-id="97fdd-134">tooscale um aplicativo de serviço de plano existente, use:</span><span class="sxs-lookup"><span data-stu-id="97fdd-134">tooscale an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -NumberofWorkers 9

#### <a name="changing-hello-worker-size-of-an-app-service-plan"></a><span data-ttu-id="97fdd-135">Alterando o tamanho de trabalhador de saudação de um plano de serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="97fdd-135">Changing hello worker size of an App Service Plan</span></span>
<span data-ttu-id="97fdd-136">tamanho de saudação toochange de trabalhadores em um aplicativo de serviço plano existente, use:</span><span class="sxs-lookup"><span data-stu-id="97fdd-136">toochange hello size of workers in an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -WorkerSize Medium

#### <a name="changing-hello-tier-of-an-app-service-plan"></a><span data-ttu-id="97fdd-137">Saudação de alteração da camada de um plano de serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="97fdd-137">Changing hello Tier of an App Service Plan</span></span>
<span data-ttu-id="97fdd-138">camada de saudação toochange de um aplicativo de serviço plano existente, use:</span><span class="sxs-lookup"><span data-stu-id="97fdd-138">toochange hello tier of an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard

### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="97fdd-139">Excluir um Plano do Serviço de Aplicativo existente</span><span class="sxs-lookup"><span data-stu-id="97fdd-139">Delete an existing App Service Plan</span></span>
<span data-ttu-id="97fdd-140">toodelete um plano de serviço de aplicativo existente, todos os atribuídos toobe de necessidade de aplicativos web movido ou excluído primeiro.</span><span class="sxs-lookup"><span data-stu-id="97fdd-140">toodelete an existing app service plan, all assigned web apps need toobe moved or deleted first.</span></span> <span data-ttu-id="97fdd-141">Usando o hello **AzureRmAppServicePlan remover** cmdlet, você pode excluir o plano de serviço de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="97fdd-141">Then using hello **Remove-AzureRmAppServicePlan** cmdlet you can delete hello app service plan.</span></span>

    Remove-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup

## <a name="managing-app-service-web-apps"></a><span data-ttu-id="97fdd-142">Gerenciando Aplicativos Web do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="97fdd-142">Managing App Service Web Apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="97fdd-143">Criar um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="97fdd-143">Create a Web App</span></span>
<span data-ttu-id="97fdd-144">toocreate um aplicativo web, use Olá **AzureRmWebApp novo** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="97fdd-144">toocreate a web app, use hello **New-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="97fdd-145">Seguem as descrições dos parâmetros diferentes hello:</span><span class="sxs-lookup"><span data-stu-id="97fdd-145">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="97fdd-146">**Nome**: nome do aplicativo web de saudação.</span><span class="sxs-lookup"><span data-stu-id="97fdd-146">**Name**: name for hello web app.</span></span>
* <span data-ttu-id="97fdd-147">**AppServicePlan**: nome do plano de serviço Olá usado toohost Olá web app.</span><span class="sxs-lookup"><span data-stu-id="97fdd-147">**AppServicePlan**: name for hello service plan used toohost hello web app.</span></span>
* <span data-ttu-id="97fdd-148">**ResourceGroupName**: grupo de recursos que hospeda o plano de serviço de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="97fdd-148">**ResourceGroupName**: resource group that hosts hello App service plan.</span></span>
* <span data-ttu-id="97fdd-149">**Local**: Olá local do aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="97fdd-149">**Location**: hello web app location.</span></span>

<span data-ttu-id="97fdd-150">Exemplo toouse esse cmdlet:</span><span class="sxs-lookup"><span data-stu-id="97fdd-150">Example toouse this cmdlet:</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"

### <a name="create-a-web-app-in-an-app-service-environment"></a><span data-ttu-id="97fdd-151">Criar um aplicativo Web em um Ambiente de Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="97fdd-151">Create a Web App in an App Service Environment</span></span>
<span data-ttu-id="97fdd-152">toocreate um aplicativo web no ambiente de serviço de um aplicativo (ASE).</span><span class="sxs-lookup"><span data-stu-id="97fdd-152">toocreate a web app in an App Service Environment (ASE).</span></span> <span data-ttu-id="97fdd-153">Use Olá mesmo **AzureRmWebApp novo** com o nome da saudação ASE toospecify parâmetros adicionais e o nome do grupo de recursos de Olá Olá ASE pertence a.</span><span class="sxs-lookup"><span data-stu-id="97fdd-153">Use hello same **New-AzureRmWebApp** command with extra parameters toospecify hello ASE name and hello resource group name that hello ASE belongs to.</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"  -ASEName ContosoASEName -ASEResourceGroupName ContosoASEResourceGroupName

<span data-ttu-id="97fdd-154">mais sobre o ambiente de serviço de aplicativo, seleção de toolearn [Introdução tooApp ambiente de serviço](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="97fdd-154">toolearn more about app service environment, check [Introduction tooApp Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="delete-an-existing-web-app"></a><span data-ttu-id="97fdd-155">Excluir um aplicativo Web existente</span><span class="sxs-lookup"><span data-stu-id="97fdd-155">Delete an existing Web App</span></span>
<span data-ttu-id="97fdd-156">toodelete um aplicativo web existente, você pode usar o hello **AzureRmWebApp remover** cmdlet, você precisa toospecify nome de saudação do aplicativo web de saudação e o nome do grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="97fdd-156">toodelete an existing web app you can use hello **Remove-AzureRmWebApp** cmdlet, you need toospecify hello name of hello web app and hello resource group name.</span></span>

    Remove-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup


### <a name="list-existing-web-apps"></a><span data-ttu-id="97fdd-157">Listar os aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="97fdd-157">List existing Web Apps</span></span>
<span data-ttu-id="97fdd-158">toolist Olá existente os aplicativos web, use Olá **AzureRmWebApp Get** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="97fdd-158">toolist hello existing web apps, use hello **Get-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="97fdd-159">toolist todos os aplicativos web em sua assinatura, use:</span><span class="sxs-lookup"><span data-stu-id="97fdd-159">toolist all web apps under your subscription, use:</span></span>

    Get-AzureRmWebApp

<span data-ttu-id="97fdd-160">toolist todos os aplicativos web em um grupo de recursos específico, use:</span><span class="sxs-lookup"><span data-stu-id="97fdd-160">toolist all web apps under a specific resource group, use:</span></span>

    Get-AzureRmWebApp -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="97fdd-161">tooget um aplicativo web específico, use:</span><span class="sxs-lookup"><span data-stu-id="97fdd-161">tooget a specific web app, use:</span></span>

    Get-AzureRmWebApp -Name ContosoWebApp

### <a name="configure-an-existing-web-app"></a><span data-ttu-id="97fdd-162">Configurar um aplicativo Web existente</span><span class="sxs-lookup"><span data-stu-id="97fdd-162">Configure an existing Web App</span></span>
<span data-ttu-id="97fdd-163">configurações de saudação do toochange e as configurações para um aplicativo web existente, use Olá **AzureRmWebApp conjunto** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="97fdd-163">toochange hello settings and configurations for an existing web app, use hello **Set-AzureRmWebApp** cmdlet.</span></span> <span data-ttu-id="97fdd-164">Para obter uma lista completa de parâmetros, verifique Olá [link de referência de Cmdlet](https://msdn.microsoft.com/library/mt652487.aspx)</span><span class="sxs-lookup"><span data-stu-id="97fdd-164">For a full list of parameters, check hello [Cmdlet reference link](https://msdn.microsoft.com/library/mt652487.aspx)</span></span>

<span data-ttu-id="97fdd-165">Exemplo (1): use essa cadeias de caracteres de conexão do cmdlet toochange</span><span class="sxs-lookup"><span data-stu-id="97fdd-165">Example (1): use this cmdlet toochange connection strings</span></span>

    $connectionstrings = @{ ContosoConn1 = @{ Type = “MySql”; Value = “MySqlConn”}; ContosoConn2 = @{ Type = “SQLAzure”; Value = “SQLAzureConn”} }
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -ConnectionStrings $connectionstrings

<span data-ttu-id="97fdd-166">Exemplo (2): adicionar ou alterar as configurações do aplicativo</span><span class="sxs-lookup"><span data-stu-id="97fdd-166">Example (2): add or change app settings</span></span>

    $appsettings = @{appsetting1 = "appsetting1value"; appsetting2 = "appsetting2value"}
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -AppSettings $appsettings


<span data-ttu-id="97fdd-167">Exemplo (3): definir Olá web aplicativo toorun no modo de 64 bits</span><span class="sxs-lookup"><span data-stu-id="97fdd-167">Example (3):  set hello web app toorun in 64-bit mode</span></span>

    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -Use32BitWorkerProcess $False

### <a name="change-hello-state-of-an-existing-web-app"></a><span data-ttu-id="97fdd-168">Alterar o estado de saudação de um aplicativo Web existente</span><span class="sxs-lookup"><span data-stu-id="97fdd-168">Change hello state of an existing Web App</span></span>
#### <a name="restart-a-web-app"></a><span data-ttu-id="97fdd-169">Reiniciar um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="97fdd-169">Restart a web app</span></span>
<span data-ttu-id="97fdd-170">toorestart um aplicativo web, você deve especificar Olá nome e grupo de recursos do aplicativo web de saudação.</span><span class="sxs-lookup"><span data-stu-id="97fdd-170">toorestart a web app, you must specify hello name and resource group of hello web app.</span></span>

    Restart-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="stop-a-web-app"></a><span data-ttu-id="97fdd-171">Parar um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="97fdd-171">Stop a web app</span></span>
<span data-ttu-id="97fdd-172">toostop um aplicativo web, você deve especificar Olá nome e grupo de recursos do aplicativo web de saudação.</span><span class="sxs-lookup"><span data-stu-id="97fdd-172">toostop a web app, you must specify hello name and resource group of hello web app.</span></span>

    Stop-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="start-a-web-app"></a><span data-ttu-id="97fdd-173">Iniciar um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="97fdd-173">Start a web app</span></span>
<span data-ttu-id="97fdd-174">toostart um aplicativo web, você deve especificar Olá nome e grupo de recursos do aplicativo web de saudação.</span><span class="sxs-lookup"><span data-stu-id="97fdd-174">toostart a web app, you must specify hello name and resource group of hello web app.</span></span>

    Start-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-publishing-profiles"></a><span data-ttu-id="97fdd-175">Gerenciar perfis de publicação de aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="97fdd-175">Manage Web App Publishing profiles</span></span>
<span data-ttu-id="97fdd-176">Cada aplicativo web tem um perfil de publicação que pode ser usado toopublish seus aplicativos, várias operações podem ser executadas em perfis de publicação.</span><span class="sxs-lookup"><span data-stu-id="97fdd-176">Each web app has a publishing profile that can be used toopublish your apps, several operations can be executed on publishing profiles.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="97fdd-177">Obter o perfil de publicação</span><span class="sxs-lookup"><span data-stu-id="97fdd-177">Get Publishing Profile</span></span>
<span data-ttu-id="97fdd-178">Olá tooget perfil para um aplicativo web, o uso de publicação:</span><span class="sxs-lookup"><span data-stu-id="97fdd-178">tooget hello publishing profile for a web app, use:</span></span>

    Get-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -OutputFile .\publishingprofile.txt

<span data-ttu-id="97fdd-179">Este comando exibe Olá publicação de linha de comando de toohello perfil também Olá publicando o arquivo de texto tooa perfil de saída.</span><span class="sxs-lookup"><span data-stu-id="97fdd-179">This command echoes hello publishing profile toohello command line as well output hello publishing profile tooa text file.</span></span>

#### <a name="reset-publishing-profile"></a><span data-ttu-id="97fdd-180">Redefinir o perfil de publicação</span><span class="sxs-lookup"><span data-stu-id="97fdd-180">Reset Publishing Profile</span></span>
<span data-ttu-id="97fdd-181">tooreset ambos Olá a senha de publicação de FTP e implantação da web para um aplicativo web, use:</span><span class="sxs-lookup"><span data-stu-id="97fdd-181">tooreset both hello publishing password for FTP and web deploy for a web app, use:</span></span>

    Reset-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-certificates"></a><span data-ttu-id="97fdd-182">Gerenciar certificados de aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="97fdd-182">Manage Web App Certificates</span></span>
<span data-ttu-id="97fdd-183">toolearn sobre como toomanage web certificados de aplicativo, consulte [associação de certificados SSL usando o PowerShell](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="97fdd-183">toolearn about how toomanage web app certificates, see [SSL Certificates binding using PowerShell](app-service-web-app-powershell-ssl-binding.md)</span></span>

### <a name="next-steps"></a><span data-ttu-id="97fdd-184">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="97fdd-184">Next Steps</span></span>
* <span data-ttu-id="97fdd-185">toolearn sobre o suporte do PowerShell do Gerenciador de recursos do Azure, consulte [usando o PowerShell do Azure com o Gerenciador de recursos do Azure.](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="97fdd-185">toolearn about Azure Resource Manager PowerShell support, see [Using Azure PowerShell with Azure Resource Manager.](../powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="97fdd-186">toolearn sobre ambientes de serviço de aplicativo, consulte [Introdução tooApp ambiente de serviço.](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="97fdd-186">toolearn about App Service Environments, see [Introduction tooApp Service Environment.](app-service-app-service-environment-intro.md)</span></span>
* <span data-ttu-id="97fdd-187">toolearn sobre como gerenciar certificados SSL do serviço de aplicativo usando o PowerShell, consulte [associação de certificados SSL usando o PowerShell.](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="97fdd-187">toolearn about managing App Service SSL certificates using PowerShell, see [SSL Certificates binding using PowerShell.](app-service-web-app-powershell-ssl-binding.md)</span></span>
* <span data-ttu-id="97fdd-188">toolearn sobre a lista completa de saudação de cmdlets do PowerShell com base no Gerenciador de recursos do Azure para aplicativos da Web do Azure, consulte [referência de Cmdlet do Azure Web aplicativos do Azure Resource Manager de Cmdlets do PowerShell.](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="97fdd-188">toolearn about hello full list of Azure Resource Manager-based PowerShell cmdlets for Azure Web Apps, see [Azure Cmdlet Reference of Web Apps Azure Resource Manager PowerShell Cmdlets.](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>
* * <span data-ttu-id="97fdd-189">toolearn sobre o gerenciamento de serviço de aplicativo usando a CLI, consulte [Using Azure Resource Manager-Based XPlat CLI para o aplicativo Web do Azure.](app-service-web-app-azure-resource-manager-xplat-cli.md)</span><span class="sxs-lookup"><span data-stu-id="97fdd-189">toolearn about managing App Service using CLI, see [Using Azure Resource Manager-Based XPlat CLI for Azure Web App.](app-service-web-app-azure-resource-manager-xplat-cli.md)</span></span>

