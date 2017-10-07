---
title: aaaAzure ferramentas de linha de comando de plataforma cruzada com base no Gerenciador de recursos para o aplicativo Web do Azure | Microsoft Docs
description: "Saiba como toouse Olá toomanage de novas ferramentas de linha de comando de plataforma cruzada com base no Azure Resource Manager seus aplicativos da Web do Azure."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: d415b195-4262-416f-b59f-7e1aef200054
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: 5f5e03edcb01154aef3bd220cd27358f69656ef4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-xplat-cli-for-azure-app-service"></a><span data-ttu-id="a8b71-103">Como usar a CLI XPlat com base no Azure Resource Manager para o Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="a8b71-103">Using Azure Resource Manager-Based XPlat CLI for Azure App Service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a8b71-104">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="a8b71-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="a8b71-105">PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="a8b71-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)

<span data-ttu-id="a8b71-106">Com o lançamento de saudação da versão de ferramentas de linha de comando de plataforma cruzada do Microsoft Azure 0.10.5, foram adicionados novos comandos.</span><span class="sxs-lookup"><span data-stu-id="a8b71-106">With hello release of Microsoft Azure Cross-platform Command-Line Tools version 0.10.5, new commands have been added.</span></span> <span data-ttu-id="a8b71-107">Esses comandos oferecem Olá usuário Olá capacidade toouse com base no Gerenciador de recursos do Azure PowerShell comandos toomanage do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a8b71-107">These commands give hello user hello ability toouse Azure Resource Manager-based PowerShell commands toomanage App Service.</span></span>

<span data-ttu-id="a8b71-108">toolearn sobre o gerenciamento de grupos de recursos, consulte [usar toomanage de CLI do Azure hello Azure recursos e grupos de recursos](../azure-resource-manager/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="a8b71-108">toolearn about managing Resource Groups, see [Use hello Azure CLI toomanage Azure resources and resource groups](../azure-resource-manager/xplat-cli-azure-resource-manager.md).</span></span> 

> [!NOTE] 
> <span data-ttu-id="a8b71-109">Além disso, experimente [2.0 do CLI do Azure](https://github.com/Azure/azure-cli), uma CLI de última geração escritos em Python para o modelo de implantação do gerenciamento de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="a8b71-109">Also, try out [Azure CLI 2.0](https://github.com/Azure/azure-cli), a next-generation CLI written in Python for hello resource management deployment model.</span></span>
>
>

## <a name="managing-app-service-plans"></a><span data-ttu-id="a8b71-110">Gerenciando Planos do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="a8b71-110">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="a8b71-111">Criar um Plano do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="a8b71-111">Create an App Service Plan</span></span>
<span data-ttu-id="a8b71-112">toocreate um plano de serviço de aplicativo, use Olá **appserviceplan azure criar** comando.</span><span class="sxs-lookup"><span data-stu-id="a8b71-112">toocreate an app service plan, use hello **azure appserviceplan create** command.</span></span>

<span data-ttu-id="a8b71-113">Seguem as descrições dos parâmetros diferentes hello:</span><span class="sxs-lookup"><span data-stu-id="a8b71-113">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="a8b71-114">**-grupo de recursos**: grupo de recursos que inclui o plano de serviço de aplicativo hello recém-criado.</span><span class="sxs-lookup"><span data-stu-id="a8b71-114">**--resource-group**: resource group that includes hello newly created app service plan.</span></span>
* <span data-ttu-id="a8b71-115">**-nome**: nome do plano de serviço de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="a8b71-115">**--name**: name of hello app service plan.</span></span>
* <span data-ttu-id="a8b71-116">**--location**: a localização do plano do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a8b71-116">**--location**: app service plan location.</span></span>
* <span data-ttu-id="a8b71-117">**– sku**: Olá desejado preços sku (Olá opções são: F1 (Free).</span><span class="sxs-lookup"><span data-stu-id="a8b71-117">**--sku**:  hello desired pricing sku (hello options are: F1 (Free).</span></span> <span data-ttu-id="a8b71-118">D1 (Compartilhado).</span><span class="sxs-lookup"><span data-stu-id="a8b71-118">D1 (Shared).</span></span> <span data-ttu-id="a8b71-119">B1 (Básico Breve), B2 (Básico Médio) e B3 (Básico Prolongado).</span><span class="sxs-lookup"><span data-stu-id="a8b71-119">B1 (Basic Small), B2 (Basic Medium), and B3 (Basic Large).</span></span> <span data-ttu-id="a8b71-120">S1 (Standard Breve), S2 (Standard Médio) e S3 (Standard Prolongado).</span><span class="sxs-lookup"><span data-stu-id="a8b71-120">S1 (Standard Small), S2 (Standard Medium), and S3 (Standard Large).</span></span> <span data-ttu-id="a8b71-121">P1 (Premium Breve), P2 (Premium Médio) e P3 (Premium Prolongado)).</span><span class="sxs-lookup"><span data-stu-id="a8b71-121">P1 (Premium Small), P2 (Premium Medium), and P3 (Premium Large).)</span></span>
* <span data-ttu-id="a8b71-122">**-instâncias**: Olá número de trabalhadores no plano de serviço de aplicativo hello (o valor padrão é 1).</span><span class="sxs-lookup"><span data-stu-id="a8b71-122">**--instances**: hello number of workers in hello app service plan (Default value is 1).</span></span>

<span data-ttu-id="a8b71-123">Exemplo toouse esse cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a8b71-123">Example toouse this cmdlet:</span></span>

    azure appserviceplan create --name ContosoAppServicePlan --location "South Central US" --resource-group ContosoAzureResourceGroup --sku P1 --instances 10

#### <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="a8b71-124">Criar um Plano do Serviço de Aplicativo do Linux</span><span class="sxs-lookup"><span data-stu-id="a8b71-124">Create a Linux App Service Plan</span></span>

<span data-ttu-id="a8b71-125">Usando Olá mesmo **appserviceplan azure criar** comando com hello parâmetro extra **true - islinux**.</span><span class="sxs-lookup"><span data-stu-id="a8b71-125">Using hello same **azure appserviceplan create** command, with hello extra parameter **--islinux true**.</span></span> <span data-ttu-id="a8b71-126">Observe as restrições de saudação e regiões descritos no [Introdução tooApp serviço no Linux](app-service-linux-intro.md)</span><span class="sxs-lookup"><span data-stu-id="a8b71-126">Note hello restrictions and regions outlined in [Introduction tooApp Service on Linux](app-service-linux-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="a8b71-127">Listar os Planos do Serviço de Aplicativo existentes</span><span class="sxs-lookup"><span data-stu-id="a8b71-127">List Existing App Service Plans</span></span>
<span data-ttu-id="a8b71-128">toolist Olá existente aplicativo planos de serviço, use **appserviceplan do azure lista** comando.</span><span class="sxs-lookup"><span data-stu-id="a8b71-128">toolist hello existing app service plans, use **azure appserviceplan list** command.</span></span>

<span data-ttu-id="a8b71-129">toolist todos os planos de serviço de aplicativo em um grupo de recursos específico, use:</span><span class="sxs-lookup"><span data-stu-id="a8b71-129">toolist all app service plans under a specific resource group, use:</span></span>

    azure appserviceplan list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="a8b71-130">tooget um plano de serviço de aplicativo específico, use **appserviceplan azure Mostrar** comando:</span><span class="sxs-lookup"><span data-stu-id="a8b71-130">tooget a specific app service plan, use **azure appserviceplan show** command:</span></span>

    azure appserviceplan show --name ContosoAppServicePlan --resource-group southeastasia

### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="a8b71-131">Configurar um Plano do Serviço de Aplicativo existente</span><span class="sxs-lookup"><span data-stu-id="a8b71-131">Configure an existing App Service Plan</span></span>
<span data-ttu-id="a8b71-132">configurações de saudação toochange para um plano de serviço de aplicativo existente, use Olá **appserviceplan azure config** comando.</span><span class="sxs-lookup"><span data-stu-id="a8b71-132">toochange hello settings for an existing app service plan, use hello **azure appserviceplan config** command.</span></span> <span data-ttu-id="a8b71-133">Você pode alterar Olá sku e o número de trabalhos Olá</span><span class="sxs-lookup"><span data-stu-id="a8b71-133">You can change hello sku, and hello number of workers</span></span> 

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1 --instances 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="a8b71-134">Dimensionando um Plano do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="a8b71-134">Scaling an App Service Plan</span></span>
<span data-ttu-id="a8b71-135">tooscale um aplicativo de serviço de plano existente, use:</span><span class="sxs-lookup"><span data-stu-id="a8b71-135">tooscale an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --instances 9

#### <a name="changing-hello-sku-of-an-app-service-plan"></a><span data-ttu-id="a8b71-136">Alterando Olá SKU de um plano de serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="a8b71-136">Changing hello SKU of an App Service Plan</span></span>
<span data-ttu-id="a8b71-137">sku de saudação toochange de um aplicativo de serviço plano existente, use:</span><span class="sxs-lookup"><span data-stu-id="a8b71-137">toochange hello sku of an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1


### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="a8b71-138">Excluir um Plano do Serviço de Aplicativo existente</span><span class="sxs-lookup"><span data-stu-id="a8b71-138">Delete an existing App Service Plan</span></span>
<span data-ttu-id="a8b71-139">toodelete um plano de serviço de aplicativo existente, todos os atribuídos aplicativos necessidade toobe movido ou excluído primeiro.</span><span class="sxs-lookup"><span data-stu-id="a8b71-139">toodelete an existing app service plan, all assigned apps need toobe moved or deleted first.</span></span> <span data-ttu-id="a8b71-140">Usando o hello **webapp azure excluir** comando você pode excluir o plano de serviço de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="a8b71-140">Then using hello **azure webapp delete** command you can delete hello app service plan.</span></span>

    azure appserviceplan delete --name ContosoAppServicePlan --resource-group southeastasia

## <a name="managing-app-service-apps"></a><span data-ttu-id="a8b71-141">Gerenciando aplicativos do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="a8b71-141">Managing App Service apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="a8b71-142">Criar um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="a8b71-142">Create a web app</span></span>
<span data-ttu-id="a8b71-143">toocreate um aplicativo web, use Olá **webapp azure criar** comando.</span><span class="sxs-lookup"><span data-stu-id="a8b71-143">toocreate a web app, use hello **azure webapp create** command.</span></span>

<span data-ttu-id="a8b71-144">Seguem as descrições dos parâmetros diferentes hello:</span><span class="sxs-lookup"><span data-stu-id="a8b71-144">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="a8b71-145">**-nome**: nome do aplicativo web de saudação.</span><span class="sxs-lookup"><span data-stu-id="a8b71-145">**--name**: name for hello web app.</span></span>
* <span data-ttu-id="a8b71-146">**-plano**: nome do plano de serviço Olá usado toohost Olá web app.</span><span class="sxs-lookup"><span data-stu-id="a8b71-146">**--plan**: name for hello service plan used toohost hello web app.</span></span>
* <span data-ttu-id="a8b71-147">**-grupo de recursos**: grupo de recursos que hospeda o plano de serviço de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="a8b71-147">**--resource-group**: resource group that hosts hello App service plan.</span></span>
* <span data-ttu-id="a8b71-148">**– local**: Olá local do aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="a8b71-148">**--location**: hello web app location.</span></span>

<span data-ttu-id="a8b71-149">Exemplo toouse esse cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a8b71-149">Example toouse this cmdlet:</span></span>

    azure webapp create --name ContosoWebApp --resource-group ContosoAzureResourceGroup --plan ContosoAppServicePlan --location "South Central US"

### <a name="delete-an-existing-app"></a><span data-ttu-id="a8b71-150">Excluir um aplicativo existente</span><span class="sxs-lookup"><span data-stu-id="a8b71-150">Delete an existing app</span></span>
<span data-ttu-id="a8b71-151">toodelete um aplicativo existente, você pode usar o hello **webapp azure excluir** comando.</span><span class="sxs-lookup"><span data-stu-id="a8b71-151">toodelete an existing app, you can use hello **azure webapp delete** command.</span></span> <span data-ttu-id="a8b71-152">Você precisará toospecify nome de saudação do aplicativo hello e o nome do grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="a8b71-152">You need toospecify hello name of hello app and hello resource group name.</span></span>

    azure webapp delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="list-existing-apps"></a><span data-ttu-id="a8b71-153">Listar aplicativos existentes</span><span class="sxs-lookup"><span data-stu-id="a8b71-153">List existing apps</span></span>
<span data-ttu-id="a8b71-154">toolist Olá os aplicativos existentes, use Olá **webapp do azure lista** comando.</span><span class="sxs-lookup"><span data-stu-id="a8b71-154">toolist hello existing apps, use hello **azure webapp list** command.</span></span>

<span data-ttu-id="a8b71-155">toolist todos os aplicativos em um grupo de recursos específico, use:</span><span class="sxs-lookup"><span data-stu-id="a8b71-155">toolist all apps in a specific resource group, use:</span></span>

    azure webapp list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="a8b71-156">tooget um aplicativo específico, use Olá **webapp azure Mostrar** comando.</span><span class="sxs-lookup"><span data-stu-id="a8b71-156">tooget a specific app, use hello **azure webapp show** command.</span></span>

    azure webapp show --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="configure-an-existing-app"></a><span data-ttu-id="a8b71-157">Configurar um aplicativo existente</span><span class="sxs-lookup"><span data-stu-id="a8b71-157">Configure an existing app</span></span>
<span data-ttu-id="a8b71-158">configurações de saudação do toochange e as configurações para um aplicativo existente, use Olá **conjunto de configuração de aplicativo Web do azure** comando.</span><span class="sxs-lookup"><span data-stu-id="a8b71-158">toochange hello settings and configurations for an existing app, use hello **azure webapp config set** command.</span></span>

<span data-ttu-id="a8b71-159">Exemplo (1): alterar a versão do php Olá de um aplicativo</span><span class="sxs-lookup"><span data-stu-id="a8b71-159">Example (1): change hello php version of a app</span></span> 

    azure webapp config set --name ContosoWebApp --resource-group ContosoAzureResourceGroup --phpversion 5.6

<span data-ttu-id="a8b71-160">Exemplo (2): adicionar ou alterar as configurações do aplicativo</span><span class="sxs-lookup"><span data-stu-id="a8b71-160">Example (2): add or change app settings</span></span>

    webapp config appsettings set --name ContosoWebApp --resource-group ContosoAzureResourceGroup appsetting1=appsetting1value,appsetting2=appsetting2value

<span data-ttu-id="a8b71-161">tooknow outras configurações que podem ser alteradas, use Olá **-h do conjunto de configuração de aplicativo Web do azure** comando.</span><span class="sxs-lookup"><span data-stu-id="a8b71-161">tooknow what other configuration can be changed, use hello **azure webapp config set -h** command.</span></span>

### <a name="change-hello-state-of-an-existing-app"></a><span data-ttu-id="a8b71-162">Alterar o estado de saudação de um aplicativo existente</span><span class="sxs-lookup"><span data-stu-id="a8b71-162">Change hello state of an existing app</span></span>
#### <a name="restart-an-app"></a><span data-ttu-id="a8b71-163">Reiniciar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="a8b71-163">Restart an app</span></span>
<span data-ttu-id="a8b71-164">toorestart um aplicativo, você deve especificar Olá nome e grupo de recursos do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="a8b71-164">toorestart an app, you must specify hello name and resource group of hello app.</span></span>

    azure webapp restart --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="stop-an-app"></a><span data-ttu-id="a8b71-165">Interromper um aplicativo</span><span class="sxs-lookup"><span data-stu-id="a8b71-165">Stop an app</span></span>
<span data-ttu-id="a8b71-166">toostop um aplicativo, você deve especificar Olá nome e grupo de recursos do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="a8b71-166">toostop an app, you must specify hello name and resource group of hello app.</span></span>

    azure webapp stop --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="start-an-app"></a><span data-ttu-id="a8b71-167">Iniciar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="a8b71-167">Start an app</span></span>
<span data-ttu-id="a8b71-168">toostart um aplicativo, você deve especificar Olá nome e grupo de recursos do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="a8b71-168">toostart an app, you must specify hello name and resource group of hello app.</span></span>

    azure webapp start --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="manage-publishing-profiles-of-an-app"></a><span data-ttu-id="a8b71-169">Gerenciar perfis de publicação de um aplicativo</span><span class="sxs-lookup"><span data-stu-id="a8b71-169">Manage publishing profiles of an app</span></span>
<span data-ttu-id="a8b71-170">Cada aplicativo tem um perfil de publicação que pode ser usado toopublish seu código.</span><span class="sxs-lookup"><span data-stu-id="a8b71-170">Each app has a publishing profile that can be used toopublish your code.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="a8b71-171">Obter o perfil de publicação</span><span class="sxs-lookup"><span data-stu-id="a8b71-171">Get Publishing Profile</span></span>
<span data-ttu-id="a8b71-172">Olá tooget perfil para um aplicativo, o uso de publicação:</span><span class="sxs-lookup"><span data-stu-id="a8b71-172">tooget hello publishing profile for a app, use:</span></span>

    azure webapp publishingprofile --name ContosoWebApp --resource-group ContosoAzureResourceGroup

<span data-ttu-id="a8b71-173">Este comando exibe o saudação de linha de comando de toohello de nome de usuário e senha de perfil de publicação.</span><span class="sxs-lookup"><span data-stu-id="a8b71-173">This command echoes hello publishing profile username and password toohello command line.</span></span>

### <a name="manage-app-hostnames"></a><span data-ttu-id="a8b71-174">Gerenciar nomes do host de aplicativo</span><span class="sxs-lookup"><span data-stu-id="a8b71-174">Manage app hostnames</span></span>
<span data-ttu-id="a8b71-175">toomanage associações de nome de host para seu aplicativo, use Olá **nomes de host do aplicativo Web do azure config** comando</span><span class="sxs-lookup"><span data-stu-id="a8b71-175">toomanage hostname bindings for your app, use hello **azure webapp config hostnames** command</span></span>  

#### <a name="list-hostname-bindings"></a><span data-ttu-id="a8b71-176">Listar associações de nome de host</span><span class="sxs-lookup"><span data-stu-id="a8b71-176">List hostname bindings</span></span>
<span data-ttu-id="a8b71-177">tooget Olá atual associações de nome de host para um aplicativo usar:</span><span class="sxs-lookup"><span data-stu-id="a8b71-177">tooget hello current hostname bindings for an app, use:</span></span>

    azure webapp config hostnames list --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="add-hostname-bindings"></a><span data-ttu-id="a8b71-178">Adicionar associações de nome de host</span><span class="sxs-lookup"><span data-stu-id="a8b71-178">Add hostname bindings</span></span>
<span data-ttu-id="a8b71-179">aplicativo de tooan de associações de hostname tooadd, use:</span><span class="sxs-lookup"><span data-stu-id="a8b71-179">tooadd hostname bindings tooan app, use:</span></span>

    azure webapp config hostnames add --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

#### <a name="delete-hostname-bindings"></a><span data-ttu-id="a8b71-180">Excluir associações de nome de host</span><span class="sxs-lookup"><span data-stu-id="a8b71-180">Delete hostname bindings</span></span>
<span data-ttu-id="a8b71-181">associações de hostname toodelete, use:</span><span class="sxs-lookup"><span data-stu-id="a8b71-181">toodelete hostname bindings, use:</span></span>

    azure webapp config hostnames delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

## <a name="next-steps"></a><span data-ttu-id="a8b71-182">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a8b71-182">Next Steps</span></span>
* <span data-ttu-id="a8b71-183">toolearn sobre o suporte a CLI do Azure Resource Manager, consulte [usar toomanage de CLI do Azure hello Azure recursos e grupos de recursos.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="a8b71-183">toolearn about Azure Resource Manager CLI support, see [Use hello Azure CLI toomanage Azure resources and resource groups.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)</span></span>
* <span data-ttu-id="a8b71-184">toolearn sobre o gerenciamento de serviço de aplicativo usando o PowerShell, consulte [tooManage Using Azure Resource Manager-Based PowerShell aplicativos Web do Azure.](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="a8b71-184">toolearn about managing App Service using PowerShell, see [Using Azure Resource Manager-Based PowerShell tooManage Azure Web Apps.](app-service-web-app-azure-resource-manager-powershell.md)</span></span>
* <span data-ttu-id="a8b71-185">toolearn sobre o serviço de aplicativo do Azure no Linux, consulte [tooApp Introdução serviço no Linux](app-service-linux-intro.md)</span><span class="sxs-lookup"><span data-stu-id="a8b71-185">toolearn about Azure App Service on Linux, see [Introduction tooApp Service on Linux](app-service-linux-intro.md)</span></span>
