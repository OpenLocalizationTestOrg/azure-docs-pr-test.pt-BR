---
title: aaaWeb aplicativo clonagem usando o PowerShell
description: Saiba como tooclone seus aplicativos Web de toonew de aplicativos Web usando o PowerShell.
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
ms.openlocfilehash: b8882370d6db6939f8e4473ccc1414091bdcb8f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-app-cloning-using-powershell"></a><span data-ttu-id="e5af1-103">Clonagem de aplicativo do Serviço de Aplicativo do Azure usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e5af1-103">Azure App Service App Cloning Using PowerShell</span></span>
<span data-ttu-id="e5af1-104">Com a versão de saudação do Microsoft Azure PowerShell versão 1.1.0 uma nova opção foi adicionada AzureRMWebApp tooNew que daria Olá usuário Olá capacidade tooclone um aplicativo existente do aplicativo Web tooa recentemente criado em uma região diferente ou em Olá mesma região.</span><span class="sxs-lookup"><span data-stu-id="e5af1-104">With hello release of Microsoft Azure PowerShell version 1.1.0 a new option has been added tooNew-AzureRMWebApp that would give hello user hello ability tooclone an existing Web App tooa newly created app in a different region or in hello same region.</span></span> <span data-ttu-id="e5af1-105">Isso permitirá que os clientes toodeploy um número de aplicativos em regiões diferentes rapidamente e facilmente.</span><span class="sxs-lookup"><span data-stu-id="e5af1-105">This will enable customers toodeploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="e5af1-106">A clonagem de aplicativo atualmente só tem suporte para planos de serviço de aplicativos de camada Premium.</span><span class="sxs-lookup"><span data-stu-id="e5af1-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="e5af1-107">novos usos de recurso Olá Olá mesmo limitações de recurso de Backup de aplicativos da Web, consulte [backup de um aplicativo web no serviço de aplicativo do Azure](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="e5af1-107">hello new feature uses hello same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="e5af1-108">toolearn sobre como usar o Gerenciador de recursos do Azure com base em toomanage de cmdlets do PowerShell do Azure sua seleção de aplicativos Web [Gerenciador de recursos do Azure com base em comandos do PowerShell para o aplicativo Web do Azure](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="e5af1-108">toolearn about using Azure Resource Manager based Azure PowerShell cmdlets toomanage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span></span>

## <a name="cloning-an-existing-app"></a><span data-ttu-id="e5af1-109">Clonagem de um aplicativo existente</span><span class="sxs-lookup"><span data-stu-id="e5af1-109">Cloning an existing App</span></span>
<span data-ttu-id="e5af1-110">Cenário: Um aplicativo web existente na região Centro Sul dos EUA, usuário Olá gostariam tooclone Olá conteúdo tooa novo aplicativo web na região Norte Central dos EUA.</span><span class="sxs-lookup"><span data-stu-id="e5af1-110">Scenario: An existing web app in South Central US region, hello user would like tooclone hello contents tooa new web app in North Central US region.</span></span> <span data-ttu-id="e5af1-111">Isso pode ser feito com a versão de Gerenciador de recursos do Azure de saudação do hello PowerShell cmdlet toocreate um novo aplicativo web com a opção de SourceWebApp - Olá.</span><span class="sxs-lookup"><span data-stu-id="e5af1-111">This can be accomplished by using hello Azure Resource Manager version of hello PowerShell cmdlet toocreate a new web app with hello -SourceWebApp option.</span></span>

<span data-ttu-id="e5af1-112">Conhecer os recursos de saudação nome do grupo que contém o aplicativo de web de origem hello, podemos usar Olá informações PowerShell comando tooget Olá fonte do aplicativo web (nesse caso chamadas webapp fonte) a seguir:</span><span class="sxs-lookup"><span data-stu-id="e5af1-112">Knowing hello resource group name that contains hello source web app, we can use hello following PowerShell command tooget hello source web app's information (in this case named source-webapp):</span></span>

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

<span data-ttu-id="e5af1-113">toocreate um novo plano de serviço de aplicativo, podemos usar o comando New-AzureRmAppServicePlan como no exemplo a seguir de saudação</span><span class="sxs-lookup"><span data-stu-id="e5af1-113">toocreate a new App Service Plan, we can use New-AzureRmAppServicePlan command as in hello following example</span></span>

    New-AzureRmAppServicePlan -Location "South Central US" -ResourceGroupName DestinationAzureResourceGroup -Name NewAppServicePlan -Tier Premium

<span data-ttu-id="e5af1-114">Usando o comando Olá AzureRmWebApp novo, podemos criar novo aplicativo web e Olá na região do hello Centro Norte dos EUA e anexá-la de camada premium existente tooan plano do serviço de aplicativo, além disso, podemos usar Olá mesmo recurso de grupo como o aplicativo de web de origem hello ou definir um novo grupo de recursos , a seguir Olá demonstra que:</span><span class="sxs-lookup"><span data-stu-id="e5af1-114">Using hello New-AzureRmWebApp command, we can create hello new web app in hello North Central US region, and tie it tooan existing premium tier App Service Plan, moreover we can use hello same resource group as hello source web app, or define a new resource group, hello following demonstrates that:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp

<span data-ttu-id="e5af1-115">tooclone um aplicativo web existente, incluindo todos os slots de implantação associado, o usuário Olá precisará toouse Olá parâmetro IncludeSourceWebAppSlots, Olá comando PowerShell a seguir demonstra o uso de saudação desse parâmetro com hello AzureRmWebApp novo comando:</span><span class="sxs-lookup"><span data-stu-id="e5af1-115">tooclone an existing web app including all associated deployment slots, hello user will need toouse hello IncludeSourceWebAppSlots parameter, hello following PowerShell command demonstrates hello use of that parameter with hello New-AzureRmWebApp command:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -IncludeSourceWebAppSlots

<span data-ttu-id="e5af1-116">tooclone um aplicativo web existente no hello mesma região, Olá usuário deverá toocreate plano de um novo grupo de recursos e um novo serviço de aplicativo no Olá Olá a mesma região e, em seguida, usando seguinte aplicativo web do PowerShell comando tooclone Olá</span><span class="sxs-lookup"><span data-stu-id="e5af1-116">tooclone an existing web app within hello same region, hello user will need toocreate a new resource group and a new app service plan in hello same region, and then using hello following PowerShell command tooclone hello web app</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName NewAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan NewAppServicePlan -SourceWebApp $srcap

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a><span data-ttu-id="e5af1-117">Clonagem de um tooan de aplicativo ambiente de serviço de aplicativo existente</span><span class="sxs-lookup"><span data-stu-id="e5af1-117">Cloning an existing App tooan App Service Environment</span></span>
<span data-ttu-id="e5af1-118">Cenário: Um aplicativo web existente na região Centro Sul dos EUA, Olá usuário quer tooclone Olá conteúdo tooa nova web aplicativo tooan existente do ambiente de serviço de aplicativo (ASE).</span><span class="sxs-lookup"><span data-stu-id="e5af1-118">Scenario: An existing web app in South Central US region, hello user would like tooclone hello contents tooa new web app tooan existing App Service Environment (ASE).</span></span>

<span data-ttu-id="e5af1-119">Conhecer os recursos de saudação nome do grupo que contém o aplicativo de web de origem hello, podemos usar Olá informações PowerShell comando tooget Olá fonte do aplicativo web (nesse caso chamadas webapp fonte) a seguir:</span><span class="sxs-lookup"><span data-stu-id="e5af1-119">Knowing hello resource group name that contains hello source web app, we can use hello following PowerShell command tooget hello source web app's information (in this case named source-webapp):</span></span>

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

<span data-ttu-id="e5af1-120">Saber o nome e nome do grupo de recursos de Olá Olá ASE pertence a saudação do ASE, usuário Olá pode usar o comando Olá novo AzureRmWebApp toocreate Olá novo aplicativo web de saudação existente ASE, Olá a seguir demonstra que:</span><span class="sxs-lookup"><span data-stu-id="e5af1-120">Knowing hello ASE's name, and hello resource group name that hello ASE belongs to, hello user can use hello New-AzureRmWebApp command toocreate hello new web app in hello existing ASE, hello following demonstrates that:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -ASEName DestinationASE -ASEResourceGroupName DestinationASEResourceGroupName -SourceWebApp $srcapp

<span data-ttu-id="e5af1-121">parâmetro de local de saudação é necessário devido a motivo toolegacy, mas no caso de saudação de criação de um aplicativo em uma ASE será ignorado.</span><span class="sxs-lookup"><span data-stu-id="e5af1-121">hello Location parameter is required due toolegacy reason, but in hello case of creating an app in an ASE it will be ignored.</span></span> 

## <a name="cloning-an-existing-app-slot"></a><span data-ttu-id="e5af1-122">Clonagem de um slot de aplicativo existente</span><span class="sxs-lookup"><span data-stu-id="e5af1-122">Cloning an existing App Slot</span></span>
<span data-ttu-id="e5af1-123">Cenário: usuário Olá deseja tooclone um tooeither de Slot do aplicativo Web um novo aplicativo Web existente ou um novo slot do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="e5af1-123">Scenario: hello user would like tooclone an existing Web App Slot tooeither a new Web App or a new Web App slot.</span></span> <span data-ttu-id="e5af1-124">Olá novo aplicativo Web pode estar em Olá mesma região, como o slot de aplicativo Web original hello, ou em uma região diferente.</span><span class="sxs-lookup"><span data-stu-id="e5af1-124">hello new Web App can be in hello same region as hello original Web App slot or in a different region.</span></span>

<span data-ttu-id="e5af1-125">Conhecer os recursos de saudação nome do grupo que contém o aplicativo de web de origem hello, podemos usar Olá informações do slot do aplicativo web fonte tooget hello (nesse caso denominadas fonte webappslot) vinculado tooWeb aplicativo origem-webapp de comando do PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="e5af1-125">Knowing hello resource group name that contains hello source web app, we can use hello following PowerShell command tooget hello source web app slot's information (in this case named source-webappslot) tied tooWeb App source-webapp:</span></span>

    $srcappslot = Get-AzureRmWebAppSlot -ResourceGroupName SourceAzureResourceGroup -Name source-webapp -Slot source-webappslot

<span data-ttu-id="e5af1-126">a seguir Olá demonstra como criar um clone de Olá web aplicativo tooa novo aplicativo web de origem:</span><span class="sxs-lookup"><span data-stu-id="e5af1-126">hello following demonstrates creating a clone of hello source web app tooa new web app:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcappslot

## <a name="configuring-traffic-manager-while-cloning-a-app"></a><span data-ttu-id="e5af1-127">Configuração do Gerenciador de Tráfego durante a clonagem de um aplicativo</span><span class="sxs-lookup"><span data-stu-id="e5af1-127">Configuring Traffic Manager while cloning a App</span></span>
<span data-ttu-id="e5af1-128">Criar aplicativos web de várias regiões e configurar o Azure Traffic Manager tooroute tráfego tooall esses aplicativos web, é um tooinsure n cenário importante que aplicativos clientes são altamente disponíveis, quando um aplicativo web existente, você tem a clonagem Olá opção tooconnect ambas as web aplicativos tooeither um perfil do Gerenciador de tráfego novo ou existente - Observe essa versão do Azure Resource Manager somente há suporte ao Gerenciador de tráfego.</span><span class="sxs-lookup"><span data-stu-id="e5af1-128">Creating multi-region web apps and configuring Azure Traffic Manager tooroute traffic tooall these web apps, is a n important scenario tooinsure that customers' apps are highly available, when cloning an existing web app you have hello option tooconnect both web apps tooeither a new traffic manager profile or an existing one - note that only Azure Resource Manager version of Traffic Manager is supported.</span></span>

### <a name="creating-a-new-traffic-manager-profile-while-cloning-a-app"></a><span data-ttu-id="e5af1-129">Criando um novo perfil do Gerenciador de Tráfego durante a clonagem de um aplicativo</span><span class="sxs-lookup"><span data-stu-id="e5af1-129">Creating a new Traffic Manager profile while cloning a App</span></span>
<span data-ttu-id="e5af1-130">Cenário: usuário Olá que tooclone uma região de tooanother do aplicativo web, ao configurar um perfil do Gerenciador de tráfego do Azure Resource Manager que incluem os dois aplicativos da web.</span><span class="sxs-lookup"><span data-stu-id="e5af1-130">Scenario: hello user would like tooclone an web app tooanother region, while configuring an Azure Resource Manager traffic manager profile that include both web apps.</span></span> <span data-ttu-id="e5af1-131">a seguir Olá demonstra como criar um clone de Olá web aplicativo tooa novo aplicativo web de origem ao configurar um novo perfil do Gerenciador de tráfego:</span><span class="sxs-lookup"><span data-stu-id="e5af1-131">hello following demonstrates creating a clone of hello source web app tooa new web app while configuring a new Traffic Manager profile:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileName newTrafficManagerProfile

### <a name="adding-new-cloned-web-app-tooan-existing-traffic-manager-profile"></a><span data-ttu-id="e5af1-132">Adicionando novo clonado aplicativo Web tooan existente perfil do Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="e5af1-132">Adding new cloned Web App tooan existing Traffic Manager profile</span></span>
<span data-ttu-id="e5af1-133">Cenário: usuário Olá já tiver um perfil do Gerenciador de tráfego do Azure Resource Manager que ele quer tooadd web apps como pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="e5af1-133">Scenario: hello user already have an Azure Resource Manager traffic manager profile that he would like tooadd both web apps as endpoints.</span></span> <span data-ttu-id="e5af1-134">toodo assim, é preciso primeiro tooassemble Olá id de perfil de Gerenciador de tráfego existente, precisaremos id da assinatura Olá, nome do grupo de recursos e Olá traffic manager nome do perfil existente.</span><span class="sxs-lookup"><span data-stu-id="e5af1-134">toodo so, we first need tooassemble hello existing traffic manager profile id, we will need hello subscription id, resource group name and hello existing traffic manager profile name.</span></span>

    $TMProfileID = "/subscriptions/<Your subscription ID goes here>/resourceGroups/<Your resource group name goes here>/providers/Microsoft.TrafficManagerProfiles/ExistingTrafficManagerProfileName"

<span data-ttu-id="e5af1-135">Depois de ter o id do Gerenciador de tráfego hello, seguinte Olá demonstra como criar um clone de Olá web aplicativo tooa novo aplicativo web de origem ao adicioná-los tooan perfil existente do Gerenciador de tráfego:</span><span class="sxs-lookup"><span data-stu-id="e5af1-135">After having hello traffic manger id, hello following demonstrates creating a clone of hello source web app tooa new web app while adding them tooan existing Traffic Manager profile:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName <Resource group name> -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileId $TMProfileID

## <a name="current-restrictions"></a><span data-ttu-id="e5af1-136">Restrições atuais</span><span class="sxs-lookup"><span data-stu-id="e5af1-136">Current Restrictions</span></span>
<span data-ttu-id="e5af1-137">Este recurso está atualmente em visualização, estamos trabalhando tooadd novos recursos ao longo do tempo, Olá lista a seguir são Olá restrições conhecidas na versão atual de saudação de clonagem do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="e5af1-137">This feature is currently in preview, we are working tooadd new capabilities over time, hello following list are hello known restrictions on hello current version of app cloning:</span></span>

* <span data-ttu-id="e5af1-138">As configurações de escala automática não são clonadas</span><span class="sxs-lookup"><span data-stu-id="e5af1-138">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="e5af1-139">As configurações de agendamento de backup não são clonadas.</span><span class="sxs-lookup"><span data-stu-id="e5af1-139">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="e5af1-140">As configurações da rede virtual não são clonadas</span><span class="sxs-lookup"><span data-stu-id="e5af1-140">VNET settings are not cloned</span></span>
* <span data-ttu-id="e5af1-141">Ideias de aplicativo não são automaticamente definidas no aplicativo de web de destino Olá</span><span class="sxs-lookup"><span data-stu-id="e5af1-141">App Insights are not automatically set up on hello destination web app</span></span>
* <span data-ttu-id="e5af1-142">As configurações de Autenticação Fácil não são clonadas</span><span class="sxs-lookup"><span data-stu-id="e5af1-142">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="e5af1-143">A extensão Kudu não é clonada</span><span class="sxs-lookup"><span data-stu-id="e5af1-143">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="e5af1-144">As regras de TiP não são clonadas</span><span class="sxs-lookup"><span data-stu-id="e5af1-144">TiP rules are not cloned</span></span>
* <span data-ttu-id="e5af1-145">O conteúdo do banco de dados não é clonado</span><span class="sxs-lookup"><span data-stu-id="e5af1-145">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="e5af1-146">Referências</span><span class="sxs-lookup"><span data-stu-id="e5af1-146">References</span></span>
* [<span data-ttu-id="e5af1-147">Azure Resource Manager based PowerShell commands for Azure Web App</span><span class="sxs-lookup"><span data-stu-id="e5af1-147">Azure Resource Manager based PowerShell commands for Azure Web App</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
* [<span data-ttu-id="e5af1-148">Clonagem de Aplicativo Web usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e5af1-148">Web App Cloning using Azure Portal</span></span>](app-service-web-app-cloning-portal.md)
* [<span data-ttu-id="e5af1-149">Fazer backup de um aplicativo Web no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="e5af1-149">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="e5af1-150">Suporte do Azure Resource Manager para Visualização do Gerenciador de Tráfego do Azure</span><span class="sxs-lookup"><span data-stu-id="e5af1-150">Azure Resource Manager support for Azure Traffic Manager Preview</span></span>](../traffic-manager/traffic-manager-powershell-arm.md)
* [<span data-ttu-id="e5af1-151">Introdução tooApp ambiente de serviço</span><span class="sxs-lookup"><span data-stu-id="e5af1-151">Introduction tooApp Service Environment</span></span>](app-service-app-service-environment-intro.md)
* [<span data-ttu-id="e5af1-152">Usando o Azure PowerShell com o Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="e5af1-152">Using Azure PowerShell with Azure Resource Manager</span></span>](../powershell-azure-resource-manager.md)

