---
title: Clonagem de Aplicativo Web usando o PowerShell
description: Saiba como clonar seus Aplicativos Web em novos Aplicativos Web usando o Azure PowerShell.
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: f9a5cfa1-fbb0-41e6-95d1-75d457347a35
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: aelnably
ms.openlocfilehash: d47d5a2f7d2462525bf37718a234e222b4f64e6d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-app-cloning-using-powershell"></a><span data-ttu-id="fd7cd-103">Clonagem de aplicativo do Serviço de Aplicativo do Azure usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fd7cd-103">Azure App Service App Cloning Using PowerShell</span></span>
<span data-ttu-id="fd7cd-104">Com o lançamento do Microsoft Azure PowerShell versão 1.1.0, uma nova opção foi adicionada ao New-AzureRMWebApp para dar ao usuário a capacidade de clonar um aplicativo Web existente como um aplicativo recém-criado em uma região diferente ou na mesma região.</span><span class="sxs-lookup"><span data-stu-id="fd7cd-104">With the release of Microsoft Azure PowerShell version 1.1.0 a new option has been added to New-AzureRMWebApp that would give the user the ability to clone an existing Web App to a newly created app in a different region or in the same region.</span></span> <span data-ttu-id="fd7cd-105">Isso permitirá que os clientes implantem vários aplicativos em diferentes regiões de forma rápida e fácil.</span><span class="sxs-lookup"><span data-stu-id="fd7cd-105">This will enable customers to deploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="fd7cd-106">A clonagem de aplicativo atualmente só tem suporte para planos de serviço de aplicativos de camada Premium.</span><span class="sxs-lookup"><span data-stu-id="fd7cd-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="fd7cd-107">O novo recurso usa as mesmas limitações que o recurso de Backup de aplicativos Web; confira [Fazer backup de um aplicativo Web no Serviço de Aplicativo do Azure](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="fd7cd-107">The new feature uses the same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="fd7cd-108">Para saber mais sobre como usar os cmdlets do Azure PowerShell baseados no Azure Resource Manager para gerenciar Aplicativos Web, confira [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="fd7cd-108">To learn about using Azure Resource Manager based Azure PowerShell cmdlets to manage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span></span>

## <a name="cloning-an-existing-app"></a><span data-ttu-id="fd7cd-109">Clonagem de um aplicativo existente</span><span class="sxs-lookup"><span data-stu-id="fd7cd-109">Cloning an existing App</span></span>
<span data-ttu-id="fd7cd-110">Cenário: um aplicativo Web existente na região Centro-Sul dos EUA, o usuário gostaria de clonar o conteúdo como um novo aplicativo Web na região Centro-Norte dos EUA.</span><span class="sxs-lookup"><span data-stu-id="fd7cd-110">Scenario: An existing web app in South Central US region, the user would like to clone the contents to a new web app in North Central US region.</span></span> <span data-ttu-id="fd7cd-111">Isso pode ser feito usando a versão do cmdlet do PowerShell do Azure Resource Manager para criar um novo aplicativo Web com a opção -SourceWebApp.</span><span class="sxs-lookup"><span data-stu-id="fd7cd-111">This can be accomplished by using the Azure Resource Manager version of the PowerShell cmdlet to create a new web app with the -SourceWebApp option.</span></span>

<span data-ttu-id="fd7cd-112">Se soubermos o nome do grupo de recursos que contém o aplicativo Web de origem, poderemos usar o seguinte comando do PowerShell para obter as informações do aplicativo Web de origem (nesse caso, o nome é source-webapp):</span><span class="sxs-lookup"><span data-stu-id="fd7cd-112">Knowing the resource group name that contains the source web app, we can use the following PowerShell command to get the source web app's information (in this case named source-webapp):</span></span>

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

<span data-ttu-id="fd7cd-113">Para criar um novo plano do Serviço de Aplicativo, podemos usar comando New-AzureRmAppServicePlan como no exemplo a seguir</span><span class="sxs-lookup"><span data-stu-id="fd7cd-113">To create a new App Service Plan, we can use New-AzureRmAppServicePlan command as in the following example</span></span>

    New-AzureRmAppServicePlan -Location "South Central US" -ResourceGroupName DestinationAzureResourceGroup -Name NewAppServicePlan -Tier Premium

<span data-ttu-id="fd7cd-114">Usando o comando New-AzureRmWebApp, podemos criar o novo aplicativo Web na região Centro-Norte dos EUA e vinculá-lo a uma plano do Serviço de Aplicativo de camada Premium existente. Além disso, podemos usar o mesmo grupo de recursos do aplicativo Web de origem ou definir um novo grupo de recursos, como demonstrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="fd7cd-114">Using the New-AzureRmWebApp command, we can create the new web app in the North Central US region, and tie it to an existing premium tier App Service Plan, moreover we can use the same resource group as the source web app, or define a new resource group, the following demonstrates that:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp

<span data-ttu-id="fd7cd-115">Para clonar um aplicativo Web existente, incluindo a todos os respectivos slots de implantação, o usuário precisará usar o parâmetro IncludeSourceWebAppSlots. O comando PowerShell abaixo demonstra o uso desse parâmetro com o comando New-AzureRmWebApp:</span><span class="sxs-lookup"><span data-stu-id="fd7cd-115">To clone an existing web app including all associated deployment slots, the user will need to use the IncludeSourceWebAppSlots parameter, the following PowerShell command demonstrates the use of that parameter with the New-AzureRmWebApp command:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -IncludeSourceWebAppSlots

<span data-ttu-id="fd7cd-116">Para clonar um aplicativo Web existente na mesma região, o usuário precisará criar um novo grupo de recursos e um novo plano do serviço de aplicativo na mesma região e usar o comando do PowerShell a seguir para clonar o aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="fd7cd-116">To clone an existing web app within the same region, the user will need to create a new resource group and a new app service plan in the same region, and then using the following PowerShell command to clone the web app</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName NewAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan NewAppServicePlan -SourceWebApp $srcap

## <a name="cloning-an-existing-app-to-an-app-service-environment"></a><span data-ttu-id="fd7cd-117">Clonagem de um aplicativo existente como um Ambiente do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="fd7cd-117">Cloning an existing App to an App Service Environment</span></span>
<span data-ttu-id="fd7cd-118">Cenário: um aplicativo Web existente na região Centro-Sul dos EUA; o usuário gostaria de clonar o conteúdo como um novo aplicativo Web em um ASE (Ambiente de Serviço de Aplicativo) existente.</span><span class="sxs-lookup"><span data-stu-id="fd7cd-118">Scenario: An existing web app in South Central US region, the user would like to clone the contents to a new web app to an existing App Service Environment (ASE).</span></span>

<span data-ttu-id="fd7cd-119">Se soubermos o nome do grupo de recursos que contém o aplicativo Web de origem, poderemos usar o seguinte comando do PowerShell para obter as informações do aplicativo Web de origem (nesse caso, o nome é source-webapp):</span><span class="sxs-lookup"><span data-stu-id="fd7cd-119">Knowing the resource group name that contains the source web app, we can use the following PowerShell command to get the source web app's information (in this case named source-webapp):</span></span>

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

<span data-ttu-id="fd7cd-120">Se souber o nome do ASE e do grupo de recursos a que o ASE pertence, o usuário poderá usar o comando New-AzureRmWebApp para criar o novo aplicativo Web no ASE existente, como demonstrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="fd7cd-120">Knowing the ASE's name, and the resource group name that the ASE belongs to, the user can use the New-AzureRmWebApp command to create the new web app in the existing ASE, the following demonstrates that:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -ASEName DestinationASE -ASEResourceGroupName DestinationASEResourceGroupName -SourceWebApp $srcapp

<span data-ttu-id="fd7cd-121">O parâmetro Location é necessário devido ao que foi herdado, mas, no caso da criação de um aplicativo em um ASE, ele será ignorado.</span><span class="sxs-lookup"><span data-stu-id="fd7cd-121">The Location parameter is required due to legacy reason, but in the case of creating an app in an ASE it will be ignored.</span></span> 

## <a name="cloning-an-existing-app-slot"></a><span data-ttu-id="fd7cd-122">Clonagem de um slot de aplicativo existente</span><span class="sxs-lookup"><span data-stu-id="fd7cd-122">Cloning an existing App Slot</span></span>
<span data-ttu-id="fd7cd-123">Cenário: o usuário deseja clonar um slot do aplicativo Web existente como a um novo aplicativo Web ou um novo slot de aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="fd7cd-123">Scenario: The user would like to clone an existing Web App Slot to either a new Web App or a new Web App slot.</span></span> <span data-ttu-id="fd7cd-124">O novo aplicativo Web pode estar na mesma região que o slot original do aplicativo Web ou em uma região diferente.</span><span class="sxs-lookup"><span data-stu-id="fd7cd-124">The new Web App can be in the same region as the original Web App slot or in a different region.</span></span>

<span data-ttu-id="fd7cd-125">Se soubermos o nome do grupo de recursos que contém o aplicativo Web de origem, poderemos usar o seguinte comando do PowerShell para obter as informações do slot do aplicativo Web de origem (nesse caso, o nome é source-webappslot) vinculado a source-webapp do aplicativo Web:</span><span class="sxs-lookup"><span data-stu-id="fd7cd-125">Knowing the resource group name that contains the source web app, we can use the following PowerShell command to get the source web app slot's information (in this case named source-webappslot) tied to Web App source-webapp:</span></span>

    $srcappslot = Get-AzureRmWebAppSlot -ResourceGroupName SourceAzureResourceGroup -Name source-webapp -Slot source-webappslot

<span data-ttu-id="fd7cd-126">O exemplo a seguir demonstra como criar um clone do aplicativo Web de origem como um novo aplicativo Web:</span><span class="sxs-lookup"><span data-stu-id="fd7cd-126">The following demonstrates creating a clone of the source web app to a new web app:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcappslot

## <a name="configuring-traffic-manager-while-cloning-a-app"></a><span data-ttu-id="fd7cd-127">Configuração do Gerenciador de Tráfego durante a clonagem de um aplicativo</span><span class="sxs-lookup"><span data-stu-id="fd7cd-127">Configuring Traffic Manager while cloning a App</span></span>
<span data-ttu-id="fd7cd-128">A criação de aplicativos Web de várias regiões e a configuração do Gerenciador de Tráfego do Azure para rotear tráfego a todos esses aplicativos Web é um cenário importante para garantir que os aplicativos dos clientes estejam altamente disponíveis; durante a clonagem de um aplicativo Web existente, você tem a opção de conectar os dois aplicativos Web a um novo perfil do gerenciador de tráfego ou a um existente. Observe que apenas a versão Azure Resource Manager do Gerenciador de Tráfego é permitida.</span><span class="sxs-lookup"><span data-stu-id="fd7cd-128">Creating multi-region web apps and configuring Azure Traffic Manager to route traffic to all these web apps, is a n important scenario to insure that customers' apps are highly available, when cloning an existing web app you have the option to connect both web apps to either a new traffic manager profile or an existing one - note that only Azure Resource Manager version of Traffic Manager is supported.</span></span>

### <a name="creating-a-new-traffic-manager-profile-while-cloning-a-app"></a><span data-ttu-id="fd7cd-129">Criando um novo perfil do Gerenciador de Tráfego durante a clonagem de um aplicativo</span><span class="sxs-lookup"><span data-stu-id="fd7cd-129">Creating a new Traffic Manager profile while cloning a App</span></span>
<span data-ttu-id="fd7cd-130">Cenário: o usuário deseja clonar um aplicativo Web em outra região enquanto configura um perfil do gerenciador de tráfego do Azure Resource Manager que inclui ambos os aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="fd7cd-130">Scenario: The user would like to clone an web app to another region, while configuring an Azure Resource Manager traffic manager profile that include both web apps.</span></span> <span data-ttu-id="fd7cd-131">O exemplo a seguir demonstra como criar um clone do aplicativo Web de origem como um novo aplicativo Web ao configurar um novo perfil do Gerenciador de Tráfego:</span><span class="sxs-lookup"><span data-stu-id="fd7cd-131">The following demonstrates creating a clone of the source web app to a new web app while configuring a new Traffic Manager profile:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileName newTrafficManagerProfile

### <a name="adding-new-cloned-web-app-to-an-existing-traffic-manager-profile"></a><span data-ttu-id="fd7cd-132">Adicionando novos aplicativos Web clonados a um perfil existente do Gerenciador de Tráfego</span><span class="sxs-lookup"><span data-stu-id="fd7cd-132">Adding new cloned Web App to an existing Traffic Manager profile</span></span>
<span data-ttu-id="fd7cd-133">Cenário: o usuário já tem um perfil do gerenciador de tráfego do Azure Resource Manager ao qual ele gostaria de adicionar ambos os aplicativos Web como pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="fd7cd-133">Scenario: The user already have an Azure Resource Manager traffic manager profile that he would like to add both web apps as endpoints.</span></span> <span data-ttu-id="fd7cd-134">Para fazer isso, primeiro precisamos montar a ID de perfil do Gerenciador de Tráfego existente; precisamos da ID de assinatura, do nome do grupo de recursos e do nome de perfil de Gerenciador de Tráfego existente.</span><span class="sxs-lookup"><span data-stu-id="fd7cd-134">To do so, we first need to assemble the existing traffic manager profile id, we will need the subscription id, resource group name and the existing traffic manager profile name.</span></span>

    $TMProfileID = "/subscriptions/<Your subscription ID goes here>/resourceGroups/<Your resource group name goes here>/providers/Microsoft.TrafficManagerProfiles/ExistingTrafficManagerProfileName"

<span data-ttu-id="fd7cd-135">Depois de obter a ID do Gerenciador de Tráfego, o código a seguir demonstra como criar um clone do aplicativo Web de origem como um novo aplicativo Web enquanto eles são adicionados a um perfil existente do Gerenciador de Tráfego:</span><span class="sxs-lookup"><span data-stu-id="fd7cd-135">After having the traffic manger id, the following demonstrates creating a clone of the source web app to a new web app while adding them to an existing Traffic Manager profile:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName <Resource group name> -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileId $TMProfileID

## <a name="current-restrictions"></a><span data-ttu-id="fd7cd-136">Restrições atuais</span><span class="sxs-lookup"><span data-stu-id="fd7cd-136">Current Restrictions</span></span>
<span data-ttu-id="fd7cd-137">Esse recurso está atualmente em visualização. Estamos trabalhando para adicionar novos recursos ao longo do tempo; a lista abaixo tem as restrições conhecidas de clonagem de aplicativo da versão atual:</span><span class="sxs-lookup"><span data-stu-id="fd7cd-137">This feature is currently in preview, we are working to add new capabilities over time, the following list are the known restrictions on the current version of app cloning:</span></span>

* <span data-ttu-id="fd7cd-138">As configurações de escala automática não são clonadas</span><span class="sxs-lookup"><span data-stu-id="fd7cd-138">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="fd7cd-139">As configurações de agendamento de backup não são clonadas.</span><span class="sxs-lookup"><span data-stu-id="fd7cd-139">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="fd7cd-140">As configurações da rede virtual não são clonadas</span><span class="sxs-lookup"><span data-stu-id="fd7cd-140">VNET settings are not cloned</span></span>
* <span data-ttu-id="fd7cd-141">O Application Insights não está automaticamente configurado no aplicativo Web de destino</span><span class="sxs-lookup"><span data-stu-id="fd7cd-141">App Insights are not automatically set up on the destination web app</span></span>
* <span data-ttu-id="fd7cd-142">As configurações de Autenticação Fácil não são clonadas</span><span class="sxs-lookup"><span data-stu-id="fd7cd-142">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="fd7cd-143">A extensão Kudu não é clonada</span><span class="sxs-lookup"><span data-stu-id="fd7cd-143">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="fd7cd-144">As regras de TiP não são clonadas</span><span class="sxs-lookup"><span data-stu-id="fd7cd-144">TiP rules are not cloned</span></span>
* <span data-ttu-id="fd7cd-145">O conteúdo do banco de dados não é clonado</span><span class="sxs-lookup"><span data-stu-id="fd7cd-145">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="fd7cd-146">Referências</span><span class="sxs-lookup"><span data-stu-id="fd7cd-146">References</span></span>
* [<span data-ttu-id="fd7cd-147">Azure Resource Manager based PowerShell commands for Azure Web App</span><span class="sxs-lookup"><span data-stu-id="fd7cd-147">Azure Resource Manager based PowerShell commands for Azure Web App</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
* [<span data-ttu-id="fd7cd-148">Clonagem de Aplicativo Web usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="fd7cd-148">Web App Cloning using Azure Portal</span></span>](app-service-web-app-cloning-portal.md)
* [<span data-ttu-id="fd7cd-149">Fazer backup de um aplicativo Web no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="fd7cd-149">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="fd7cd-150">Suporte do Azure Resource Manager para Visualização do Gerenciador de Tráfego do Azure</span><span class="sxs-lookup"><span data-stu-id="fd7cd-150">Azure Resource Manager support for Azure Traffic Manager Preview</span></span>](../traffic-manager/traffic-manager-powershell-arm.md)
* [<span data-ttu-id="fd7cd-151">Introdução ao ambiente de Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="fd7cd-151">Introduction to App Service Environment</span></span>](app-service-app-service-environment-intro.md)
* [<span data-ttu-id="fd7cd-152">Usando o Azure PowerShell com o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fd7cd-152">Using Azure PowerShell with Azure Resource Manager</span></span>](../powershell-azure-resource-manager.md)

