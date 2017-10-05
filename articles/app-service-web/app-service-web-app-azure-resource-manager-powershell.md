---
title: Comandos do PowerShell baseados no Azure Resource Manager para aplicativos Web do Azure | Microsoft Docs
description: Saiba como usar os novos comandos do PowerShell baseados no Azure Resource Manager para gerenciar seus aplicativos Web do Azure.
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
ms.openlocfilehash: 8d574f051a327ba0409e6f25a5886af673d3d5e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-resource-manager-based-powershell-to-manage-azure-web-apps"></a><span data-ttu-id="d38b2-103">Usando o PowerShell baseado no Azure Resource Manager para gerenciar aplicativos Web do Azure</span><span class="sxs-lookup"><span data-stu-id="d38b2-103">Using Azure Resource Manager-Based PowerShell to Manage Azure Web Apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d38b2-104">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="d38b2-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="d38b2-105">PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="d38b2-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
> 
> 

<span data-ttu-id="d38b2-106">Com o Microsoft Azure PowerShell versão 1.0.0 foram adicionados novos comandos que concedem ao usuário a capacidade de usar comandos do PowerShell baseados no Azure Resource Manager para gerenciar aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="d38b2-106">With Microsoft Azure PowerShell version 1.0.0 new commands have been added, that give the user the ability to use Azure Resource Manager-based PowerShell commands to manage Web Apps.</span></span>

<span data-ttu-id="d38b2-107">Para saber mais sobre como gerenciar grupos de recursos, consulte [Usando o Azure PowerShell com o Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="d38b2-107">To learn about managing Resource Groups, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span> 

<span data-ttu-id="d38b2-108">Para saber mais sobre a lista completa de parâmetros e opções para os cmdlets do PowerShell, veja a [Referência de cmdlet completa dos cmdlets do PowerShell baseados no Azure Resource Manager de aplicativo Web](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="d38b2-108">To learn about the full list of parameters and options for the PowerShell cmdlets, see the [full Cmdlet Reference of Web App Azure Resource Manager-based PowerShell Cmdlets](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>

## <a name="managing-app-service-plans"></a><span data-ttu-id="d38b2-109">Gerenciando Planos do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="d38b2-109">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="d38b2-110">Criar um Plano do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="d38b2-110">Create an App Service Plan</span></span>
<span data-ttu-id="d38b2-111">Para criar um plano do serviço de aplicativo, use o cmdlet **AzureRmAppServicePlan novo** .</span><span class="sxs-lookup"><span data-stu-id="d38b2-111">To create an app service plan, use the **New-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="d38b2-112">A seguir estão as descrições dos diferentes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="d38b2-112">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="d38b2-113">**Name**: o nome do Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d38b2-113">**Name**: name of the app service plan.</span></span>
* <span data-ttu-id="d38b2-114">**Local**: a localização do plano do serviço.</span><span class="sxs-lookup"><span data-stu-id="d38b2-114">**Location**: service plan location.</span></span>
* <span data-ttu-id="d38b2-115">**ResourceGroupName**: grupo de recursos que inclui o Plano do Serviço de Aplicativo recém-criado.</span><span class="sxs-lookup"><span data-stu-id="d38b2-115">**ResourceGroupName**: resource group that includes the newly created app service plan.</span></span>
* <span data-ttu-id="d38b2-116">**Camada**: o tipo de preço desejado (o padrão é Gratuito, outras opções são Compartilhado, Básico, Standard e Premium).</span><span class="sxs-lookup"><span data-stu-id="d38b2-116">**Tier**:  the desired pricing tier (Default is Free, other options are Shared, Basic, Standard, and Premium.)</span></span>
* <span data-ttu-id="d38b2-117">**WorkerSize**: o tamanho de trabalhadores (o padrão é pequeno se o parâmetro de tipo foi especificado como Básico, Standard ou Premium.</span><span class="sxs-lookup"><span data-stu-id="d38b2-117">**WorkerSize**: the size of workers (Default is small if the Tier parameter was specified as Basic, Standard, or Premium.</span></span> <span data-ttu-id="d38b2-118">Outras opções são Médio e Grande.)</span><span class="sxs-lookup"><span data-stu-id="d38b2-118">Other options are Medium, and Large.)</span></span>
* <span data-ttu-id="d38b2-119">**NumberofWorkers**: o número de funções de trabalho no Plano do Serviço de Aplicativo ( o valor padrão é 1).</span><span class="sxs-lookup"><span data-stu-id="d38b2-119">**NumberofWorkers**: the number of workers in the app service plan (Default value is 1).</span></span> 

<span data-ttu-id="d38b2-120">Exemplo para usar este cmdlet:</span><span class="sxs-lookup"><span data-stu-id="d38b2-120">Example to use this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -Tier Premium -WorkerSize Large -NumberofWorkers 10

### <a name="create-an-app-service-plan-in-an-app-service-environment"></a><span data-ttu-id="d38b2-121">Criar um Plano do Serviço de Aplicativo em um Ambiente de Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="d38b2-121">Create an App Service Plan in an App Service Environment</span></span>
<span data-ttu-id="d38b2-122">Para criar um plano do serviço de aplicativo em um ASE (ambiente do serviço de aplicativo), use o mesmo comando **New-AzureRmAppServicePlan** com parâmetros extra para especificar o nome do ASE e o nome do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d38b2-122">To create an app service plan in an app service environment, use the same command **New-AzureRmAppServicePlan** command with extra parameters to specify the ASE's name and ASE's resource group name.</span></span>

<span data-ttu-id="d38b2-123">Exemplo para usar este cmdlet:</span><span class="sxs-lookup"><span data-stu-id="d38b2-123">Example to use this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -AseName constosoASE -AseResourceGroupName contosoASERG -Tier Premium -WorkerSize Large -NumberofWorkers 10

<span data-ttu-id="d38b2-124">Para saber mais sobre o ambiente do serviço de aplicativo, consulte [Introdução ao Ambiente do Serviço de Aplicativo](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="d38b2-124">To learn more about app service environment, check [Introduction to App Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="d38b2-125">Listar os Planos do Serviço de Aplicativo existentes</span><span class="sxs-lookup"><span data-stu-id="d38b2-125">List Existing App Service Plans</span></span>
<span data-ttu-id="d38b2-126">Para listar os planos do serviço de aplicativo existentes, use o cmdlet **Get-AzureRmAppServicePlan** .</span><span class="sxs-lookup"><span data-stu-id="d38b2-126">To list the existing app service plans, use **Get-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="d38b2-127">Para listar todos os planos do serviço de aplicativo na sua assinatura, use:</span><span class="sxs-lookup"><span data-stu-id="d38b2-127">To list all app service plans under your subscription, use:</span></span> 

    Get-AzureRmAppServicePlan

<span data-ttu-id="d38b2-128">Para listar todos os Planos de Serviço de Aplicativo em um grupo de recursos específico, use:</span><span class="sxs-lookup"><span data-stu-id="d38b2-128">To list all app service plans under a specific resource group, use:</span></span>

    Get-AzureRmAppServicePlan -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="d38b2-129">Para obter um Plano do Serviço de Aplicativo, use:</span><span class="sxs-lookup"><span data-stu-id="d38b2-129">To get a specific app service plan, use:</span></span>

    Get-AzureRmAppServicePlan -Name ContosoAppServicePlan


### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="d38b2-130">Configurar um Plano do Serviço de Aplicativo existente</span><span class="sxs-lookup"><span data-stu-id="d38b2-130">Configure an existing App Service Plan</span></span>
<span data-ttu-id="d38b2-131">Para alterar as configurações para um plano do serviço de aplicativo existente, use o cmdlet **Set-AzureRmAppServicePlan** .</span><span class="sxs-lookup"><span data-stu-id="d38b2-131">To change the settings for an existing app service plan, use the **Set-AzureRmAppServicePlan** cmdlet.</span></span> <span data-ttu-id="d38b2-132">Você pode alterar o tipo, o tamanho das funções de trabalho e o número de funções de trabalho</span><span class="sxs-lookup"><span data-stu-id="d38b2-132">You can change the tier, worker size, and the number of workers</span></span> 

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard -WorkerSize Medium -NumberofWorkers 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="d38b2-133">Dimensionando um Plano do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="d38b2-133">Scaling an App Service Plan</span></span>
<span data-ttu-id="d38b2-134">Para ajustar a escala de um Plano do Serviço de Aplicativo existente, use:</span><span class="sxs-lookup"><span data-stu-id="d38b2-134">To scale an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -NumberofWorkers 9

#### <a name="changing-the-worker-size-of-an-app-service-plan"></a><span data-ttu-id="d38b2-135">Alterando o tamanho do trabalho de um Plano do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="d38b2-135">Changing the worker size of an App Service Plan</span></span>
<span data-ttu-id="d38b2-136">Para alterar o tamanho das funções de trabalho em um Plano do Serviço de Aplicativo existente, use:</span><span class="sxs-lookup"><span data-stu-id="d38b2-136">To change the size of workers in an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -WorkerSize Medium

#### <a name="changing-the-tier-of-an-app-service-plan"></a><span data-ttu-id="d38b2-137">Alterando o tipo de um Plano do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="d38b2-137">Changing the Tier of an App Service Plan</span></span>
<span data-ttu-id="d38b2-138">Para alterar o tipo de um Plano do Serviço de Aplicativo existente, use:</span><span class="sxs-lookup"><span data-stu-id="d38b2-138">To change the tier of an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard

### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="d38b2-139">Excluir um Plano do Serviço de Aplicativo existente</span><span class="sxs-lookup"><span data-stu-id="d38b2-139">Delete an existing App Service Plan</span></span>
<span data-ttu-id="d38b2-140">Para excluir um plano do serviço de aplicativo existente, todos os aplicativos Web atribuídos precisam ser movidos ou excluídos primeiro.</span><span class="sxs-lookup"><span data-stu-id="d38b2-140">To delete an existing app service plan, all assigned web apps need to be moved or deleted first.</span></span> <span data-ttu-id="d38b2-141">Em seguida, usando o cmdlet **Remove-AzureRmAppServicePlan**, você pode excluir o plano do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d38b2-141">Then using the **Remove-AzureRmAppServicePlan** cmdlet you can delete the app service plan.</span></span>

    Remove-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup

## <a name="managing-app-service-web-apps"></a><span data-ttu-id="d38b2-142">Gerenciando Aplicativos Web do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="d38b2-142">Managing App Service Web Apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="d38b2-143">Criar um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="d38b2-143">Create a Web App</span></span>
<span data-ttu-id="d38b2-144">Para criar um aplicativo Web, use o cmdlet **New-AzureRmWebApp** .</span><span class="sxs-lookup"><span data-stu-id="d38b2-144">To create a web app, use the **New-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="d38b2-145">A seguir estão as descrições dos diferentes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="d38b2-145">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="d38b2-146">**Name**: o nome do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="d38b2-146">**Name**: name for the web app.</span></span>
* <span data-ttu-id="d38b2-147">**AppServicePlan**: o nome do plano de serviço usado para hospedar o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="d38b2-147">**AppServicePlan**: name for the service plan used to host the web app.</span></span>
* <span data-ttu-id="d38b2-148">**ResourceGroupName**: o grupo de recursos que hospeda o plano do serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d38b2-148">**ResourceGroupName**: resource group that hosts the App service plan.</span></span>
* <span data-ttu-id="d38b2-149">**Location**: a localização do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="d38b2-149">**Location**: the web app location.</span></span>

<span data-ttu-id="d38b2-150">Exemplo para usar este cmdlet:</span><span class="sxs-lookup"><span data-stu-id="d38b2-150">Example to use this cmdlet:</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"

### <a name="create-a-web-app-in-an-app-service-environment"></a><span data-ttu-id="d38b2-151">Criar um aplicativo Web em um Ambiente de Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="d38b2-151">Create a Web App in an App Service Environment</span></span>
<span data-ttu-id="d38b2-152">Para criar um aplicativo Web em um Ambiente do Serviço de Aplicativo (ASE).</span><span class="sxs-lookup"><span data-stu-id="d38b2-152">To create a web app in an App Service Environment (ASE).</span></span> <span data-ttu-id="d38b2-153">Use o mesmo comando **New-AzureRmWebApp** com parâmetros extras para especificar o nome do ASE e o nome do grupo de recursos ao qual o ASE pertence.</span><span class="sxs-lookup"><span data-stu-id="d38b2-153">Use the same **New-AzureRmWebApp** command with extra parameters to specify the ASE name and the resource group name that the ASE belongs to.</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"  -ASEName ContosoASEName -ASEResourceGroupName ContosoASEResourceGroupName

<span data-ttu-id="d38b2-154">Para saber mais sobre o ambiente do serviço de aplicativo, consulte [Introdução ao Ambiente do Serviço de Aplicativo](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="d38b2-154">To learn more about app service environment, check [Introduction to App Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="delete-an-existing-web-app"></a><span data-ttu-id="d38b2-155">Excluir um aplicativo Web existente</span><span class="sxs-lookup"><span data-stu-id="d38b2-155">Delete an existing Web App</span></span>
<span data-ttu-id="d38b2-156">Para excluir um aplicativo Web existente, você pode usar o cmdlet **Remove-AzureRmWebApp** , você precisa especificar o nome do aplicativo Web e o nome do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d38b2-156">To delete an existing web app you can use the **Remove-AzureRmWebApp** cmdlet, you need to specify the name of the web app and the resource group name.</span></span>

    Remove-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup


### <a name="list-existing-web-apps"></a><span data-ttu-id="d38b2-157">Listar os aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="d38b2-157">List existing Web Apps</span></span>
<span data-ttu-id="d38b2-158">Para listar os aplicativos Web existentes, use o cmdlet **Get-AzureRmWebApp** .</span><span class="sxs-lookup"><span data-stu-id="d38b2-158">To list the existing web apps, use the **Get-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="d38b2-159">Para listar todos os aplicativos Web em sua assinatura, use:</span><span class="sxs-lookup"><span data-stu-id="d38b2-159">To list all web apps under your subscription, use:</span></span>

    Get-AzureRmWebApp

<span data-ttu-id="d38b2-160">Para listar todos os aplicativos Web em um grupo de recursos específico, use:</span><span class="sxs-lookup"><span data-stu-id="d38b2-160">To list all web apps under a specific resource group, use:</span></span>

    Get-AzureRmWebApp -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="d38b2-161">Para obter um aplicativo Web específico, use:</span><span class="sxs-lookup"><span data-stu-id="d38b2-161">To get a specific web app, use:</span></span>

    Get-AzureRmWebApp -Name ContosoWebApp

### <a name="configure-an-existing-web-app"></a><span data-ttu-id="d38b2-162">Configurar um aplicativo Web existente</span><span class="sxs-lookup"><span data-stu-id="d38b2-162">Configure an existing Web App</span></span>
<span data-ttu-id="d38b2-163">Para alterar as definições e configurações para um aplicativo Web existente, use o cmdlet **Set-AzureRmWebApp** .</span><span class="sxs-lookup"><span data-stu-id="d38b2-163">To change the settings and configurations for an existing web app, use the **Set-AzureRmWebApp** cmdlet.</span></span> <span data-ttu-id="d38b2-164">Para obter uma lista completa de parâmetros, consulte o [link de referência de Cmdlet](https://msdn.microsoft.com/library/mt652487.aspx)</span><span class="sxs-lookup"><span data-stu-id="d38b2-164">For a full list of parameters, check the [Cmdlet reference link](https://msdn.microsoft.com/library/mt652487.aspx)</span></span>

<span data-ttu-id="d38b2-165">Exemplo (1): use este cmdlet para alterar cadeias de conexão</span><span class="sxs-lookup"><span data-stu-id="d38b2-165">Example (1): use this cmdlet to change connection strings</span></span>

    $connectionstrings = @{ ContosoConn1 = @{ Type = “MySql”; Value = “MySqlConn”}; ContosoConn2 = @{ Type = “SQLAzure”; Value = “SQLAzureConn”} }
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -ConnectionStrings $connectionstrings

<span data-ttu-id="d38b2-166">Exemplo (2): adicionar ou alterar as configurações do aplicativo</span><span class="sxs-lookup"><span data-stu-id="d38b2-166">Example (2): add or change app settings</span></span>

    $appsettings = @{appsetting1 = "appsetting1value"; appsetting2 = "appsetting2value"}
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -AppSettings $appsettings


<span data-ttu-id="d38b2-167">Exemplo (3): defina o aplicativo Web para executar no modo de 64 bits</span><span class="sxs-lookup"><span data-stu-id="d38b2-167">Example (3):  set the web app to run in 64-bit mode</span></span>

    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -Use32BitWorkerProcess $False

### <a name="change-the-state-of-an-existing-web-app"></a><span data-ttu-id="d38b2-168">Alterar o estado de um aplicativo Web existente</span><span class="sxs-lookup"><span data-stu-id="d38b2-168">Change the state of an existing Web App</span></span>
#### <a name="restart-a-web-app"></a><span data-ttu-id="d38b2-169">Reiniciar um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="d38b2-169">Restart a web app</span></span>
<span data-ttu-id="d38b2-170">Para reiniciar um aplicativo Web, você deve especificar o nome e grupo de recursos do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="d38b2-170">To restart a web app, you must specify the name and resource group of the web app.</span></span>

    Restart-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="stop-a-web-app"></a><span data-ttu-id="d38b2-171">Parar um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="d38b2-171">Stop a web app</span></span>
<span data-ttu-id="d38b2-172">Para parar um aplicativo Web, você deve especificar o nome e grupo de recursos do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="d38b2-172">To stop a web app, you must specify the name and resource group of the web app.</span></span>

    Stop-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="start-a-web-app"></a><span data-ttu-id="d38b2-173">Iniciar um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="d38b2-173">Start a web app</span></span>
<span data-ttu-id="d38b2-174">Para iniciar um aplicativo Web, você deve especificar o nome e grupo de recursos do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="d38b2-174">To start a web app, you must specify the name and resource group of the web app.</span></span>

    Start-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-publishing-profiles"></a><span data-ttu-id="d38b2-175">Gerenciar perfis de publicação de aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="d38b2-175">Manage Web App Publishing profiles</span></span>
<span data-ttu-id="d38b2-176">Cada aplicativo Web tem um perfil de publicação que pode ser usado para publicar seus aplicativos, várias operações podem ser executadas em perfis de publicação.</span><span class="sxs-lookup"><span data-stu-id="d38b2-176">Each web app has a publishing profile that can be used to publish your apps, several operations can be executed on publishing profiles.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="d38b2-177">Obter o perfil de publicação</span><span class="sxs-lookup"><span data-stu-id="d38b2-177">Get Publishing Profile</span></span>
<span data-ttu-id="d38b2-178">Para obter o perfil de publicação para um aplicativo Web, use:</span><span class="sxs-lookup"><span data-stu-id="d38b2-178">To get the publishing profile for a web app, use:</span></span>

    Get-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -OutputFile .\publishingprofile.txt

<span data-ttu-id="d38b2-179">Esse comando retorna o perfil de publicação para a linha de comando, bem como gerará a saída do perfil de publicação em um arquivo de texto.</span><span class="sxs-lookup"><span data-stu-id="d38b2-179">This command echoes the publishing profile to the command line as well output the publishing profile to a text file.</span></span>

#### <a name="reset-publishing-profile"></a><span data-ttu-id="d38b2-180">Redefinir o perfil de publicação</span><span class="sxs-lookup"><span data-stu-id="d38b2-180">Reset Publishing Profile</span></span>
<span data-ttu-id="d38b2-181">Para redefinir a senha de publicação do FTP e a implantação da Web de um aplicativo Web, use:</span><span class="sxs-lookup"><span data-stu-id="d38b2-181">To reset both the publishing password for FTP and web deploy for a web app, use:</span></span>

    Reset-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-certificates"></a><span data-ttu-id="d38b2-182">Gerenciar certificados de aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="d38b2-182">Manage Web App Certificates</span></span>
<span data-ttu-id="d38b2-183">Para saber mais sobre como gerenciar certificados de aplicativo Web, consulte [Associação de certificados SSL usando o PowerShell](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="d38b2-183">To learn about how to manage web app certificates, see [SSL Certificates binding using PowerShell](app-service-web-app-powershell-ssl-binding.md)</span></span>

### <a name="next-steps"></a><span data-ttu-id="d38b2-184">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d38b2-184">Next Steps</span></span>
* <span data-ttu-id="d38b2-185">Para saber sobre o suporte do Azure Resource Manager ao PowerShell, consulte [Usando o Azure PowerShell com o Azure Resource Manager.](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="d38b2-185">To learn about Azure Resource Manager PowerShell support, see [Using Azure PowerShell with Azure Resource Manager.](../powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="d38b2-186">Para saber mais sobre os Ambientes do Serviço de Aplicativo, consulte [Introdução ao Ambiente do Serviço de Aplicativo.](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="d38b2-186">To learn about App Service Environments, see [Introduction to App Service Environment.](app-service-app-service-environment-intro.md)</span></span>
* <span data-ttu-id="d38b2-187">Para saber mais sobre como gerenciar certificados SSL do Serviço de Aplicativo usando o PowerShell, consulte [Associação de certificados SSL usando o PowerShell.](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="d38b2-187">To learn about managing App Service SSL certificates using PowerShell, see [SSL Certificates binding using PowerShell.](app-service-web-app-powershell-ssl-binding.md)</span></span>
* <span data-ttu-id="d38b2-188">Para saber mais sobre a lista completa de cmdlets PowerShell baseados no Azure Resource Manager para aplicativos Web do Azure, consulte [Referência de Cmdlets do Azure dos Cmdlets do PowerShell do Azure Resource Manager de Aplicativos Web.](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="d38b2-188">To learn about the full list of Azure Resource Manager-based PowerShell cmdlets for Azure Web Apps, see [Azure Cmdlet Reference of Web Apps Azure Resource Manager PowerShell Cmdlets.](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>
* * <span data-ttu-id="d38b2-189">Para saber mais sobre o gerenciamento do Serviço de Aplicativo usando a CLI, veja [Using Azure Resource Manager-Based XPlat CLI para aplicativo Web do Azure (Usando a CLI XPlat baseada no Azure Resource Manager para o Aplicativo Web do Azure).](app-service-web-app-azure-resource-manager-xplat-cli.md)</span><span class="sxs-lookup"><span data-stu-id="d38b2-189">To learn about managing App Service using CLI, see [Using Azure Resource Manager-Based XPlat CLI for Azure Web App.](app-service-web-app-azure-resource-manager-xplat-cli.md)</span></span>

