---
title: Ferramentas de linha de comando de plataforma cruzada com base no Azure Resource Manager para Aplicativos Web do Azure | Microsoft Docs
description: Saiba como usar as novas Ferramentas de linha de comando de plataforma cruzada com base no Azure Resource Manager para gerenciar Aplicativos Web do Azure.
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
ms.openlocfilehash: 7a03e1417617453c43edcc3787da10d171359757
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-resource-manager-based-xplat-cli-for-azure-app-service"></a><span data-ttu-id="79df8-103">Como usar a CLI XPlat com base no Azure Resource Manager para o Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="79df8-103">Using Azure Resource Manager-Based XPlat CLI for Azure App Service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="79df8-104">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="79df8-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="79df8-105">PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="79df8-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)

<span data-ttu-id="79df8-106">Com o lançamento da versão 0.10.5 das Ferramentas de Linha de Comando de plataforma cruzada do Microsoft Azure, foram adicionados novos comandos.</span><span class="sxs-lookup"><span data-stu-id="79df8-106">With the release of Microsoft Azure Cross-platform Command-Line Tools version 0.10.5, new commands have been added.</span></span> <span data-ttu-id="79df8-107">Esses comandos permitem que o usuário utilize comandos do PowerShell baseados no Azure Resource Manager para gerenciar o Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="79df8-107">These commands give the user the ability to use Azure Resource Manager-based PowerShell commands to manage App Service.</span></span>

<span data-ttu-id="79df8-108">Para saber mais sobre como gerenciar Grupos de Recursos, veja [Usar a CLI do Azure para gerenciar recursos e grupos de recursos do Azure](../azure-resource-manager/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="79df8-108">To learn about managing Resource Groups, see [Use the Azure CLI to manage Azure resources and resource groups](../azure-resource-manager/xplat-cli-azure-resource-manager.md).</span></span> 

> [!NOTE] 
> <span data-ttu-id="79df8-109">Além disso, experimente a [CLI do Azure 2.0](https://github.com/Azure/azure-cli), uma CLI de próxima geração escrita em Python para o modelo de implantação do resource manager.</span><span class="sxs-lookup"><span data-stu-id="79df8-109">Also, try out [Azure CLI 2.0](https://github.com/Azure/azure-cli), a next-generation CLI written in Python for the resource management deployment model.</span></span>
>
>

## <a name="managing-app-service-plans"></a><span data-ttu-id="79df8-110">Gerenciando Planos do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="79df8-110">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="79df8-111">Criar um Plano do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="79df8-111">Create an App Service Plan</span></span>
<span data-ttu-id="79df8-112">Para criar um plano do serviço de aplicativo, use o comando **azure appserviceplan create**.</span><span class="sxs-lookup"><span data-stu-id="79df8-112">To create an app service plan, use the **azure appserviceplan create** command.</span></span>

<span data-ttu-id="79df8-113">A seguir estão as descrições dos diferentes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="79df8-113">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="79df8-114">**--resource-group**: grupo de recursos que inclui o plano do serviço de aplicativo recém-criado.</span><span class="sxs-lookup"><span data-stu-id="79df8-114">**--resource-group**: resource group that includes the newly created app service plan.</span></span>
* <span data-ttu-id="79df8-115">**--name**: o nome do plano do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="79df8-115">**--name**: name of the app service plan.</span></span>
* <span data-ttu-id="79df8-116">**--location**: a localização do plano do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="79df8-116">**--location**: app service plan location.</span></span>
* <span data-ttu-id="79df8-117">**--sku**: o SKU de preços desejado (as opções são: F1 (Gratuito).</span><span class="sxs-lookup"><span data-stu-id="79df8-117">**--sku**:  the desired pricing sku (The options are: F1 (Free).</span></span> <span data-ttu-id="79df8-118">D1 (Compartilhado).</span><span class="sxs-lookup"><span data-stu-id="79df8-118">D1 (Shared).</span></span> <span data-ttu-id="79df8-119">B1 (Básico Breve), B2 (Básico Médio) e B3 (Básico Prolongado).</span><span class="sxs-lookup"><span data-stu-id="79df8-119">B1 (Basic Small), B2 (Basic Medium), and B3 (Basic Large).</span></span> <span data-ttu-id="79df8-120">S1 (Standard Breve), S2 (Standard Médio) e S3 (Standard Prolongado).</span><span class="sxs-lookup"><span data-stu-id="79df8-120">S1 (Standard Small), S2 (Standard Medium), and S3 (Standard Large).</span></span> <span data-ttu-id="79df8-121">P1 (Premium Breve), P2 (Premium Médio) e P3 (Premium Prolongado)).</span><span class="sxs-lookup"><span data-stu-id="79df8-121">P1 (Premium Small), P2 (Premium Medium), and P3 (Premium Large).)</span></span>
* <span data-ttu-id="79df8-122">**--instances**: o número de trabalhos no plano do serviço de aplicativo (o valor padrão é 1).</span><span class="sxs-lookup"><span data-stu-id="79df8-122">**--instances**: the number of workers in the app service plan (Default value is 1).</span></span>

<span data-ttu-id="79df8-123">Exemplo para usar este cmdlet:</span><span class="sxs-lookup"><span data-stu-id="79df8-123">Example to use this cmdlet:</span></span>

    azure appserviceplan create --name ContosoAppServicePlan --location "South Central US" --resource-group ContosoAzureResourceGroup --sku P1 --instances 10

#### <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="79df8-124">Criar um Plano do Serviço de Aplicativo do Linux</span><span class="sxs-lookup"><span data-stu-id="79df8-124">Create a Linux App Service Plan</span></span>

<span data-ttu-id="79df8-125">Usando o mesmo comando **azure appserviceplan create** com o parâmetro extra **--islinux true**.</span><span class="sxs-lookup"><span data-stu-id="79df8-125">Using the same **azure appserviceplan create** command, with the extra parameter **--islinux true**.</span></span> <span data-ttu-id="79df8-126">Observe as restrições e regiões descritas em [Introdução ao Serviço de Aplicativo no Linux](app-service-linux-intro.md)</span><span class="sxs-lookup"><span data-stu-id="79df8-126">Note the restrictions and regions outlined in [Introduction to App Service on Linux](app-service-linux-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="79df8-127">Listar os Planos do Serviço de Aplicativo existentes</span><span class="sxs-lookup"><span data-stu-id="79df8-127">List Existing App Service Plans</span></span>
<span data-ttu-id="79df8-128">Para listar os planos do serviço de aplicativo existentes, use o comando **azure appserviceplan list**.</span><span class="sxs-lookup"><span data-stu-id="79df8-128">To list the existing app service plans, use **azure appserviceplan list** command.</span></span>

<span data-ttu-id="79df8-129">Para listar todos os Planos de Serviço de Aplicativo em um grupo de recursos específico, use:</span><span class="sxs-lookup"><span data-stu-id="79df8-129">To list all app service plans under a specific resource group, use:</span></span>

    azure appserviceplan list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="79df8-130">Para obter um planos do serviço de aplicativo existente, use o comando **azure appserviceplan show**:</span><span class="sxs-lookup"><span data-stu-id="79df8-130">To get a specific app service plan, use **azure appserviceplan show** command:</span></span>

    azure appserviceplan show --name ContosoAppServicePlan --resource-group southeastasia

### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="79df8-131">Configurar um Plano do Serviço de Aplicativo existente</span><span class="sxs-lookup"><span data-stu-id="79df8-131">Configure an existing App Service Plan</span></span>
<span data-ttu-id="79df8-132">Para alterar as configurações para um plano do serviço de aplicativo existente, use o comando **azure appserviceplan config**.</span><span class="sxs-lookup"><span data-stu-id="79df8-132">To change the settings for an existing app service plan, use the **azure appserviceplan config** command.</span></span> <span data-ttu-id="79df8-133">Você pode alterar o sku e o número de trabalhos</span><span class="sxs-lookup"><span data-stu-id="79df8-133">You can change the sku, and the number of workers</span></span> 

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1 --instances 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="79df8-134">Dimensionando um Plano do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="79df8-134">Scaling an App Service Plan</span></span>
<span data-ttu-id="79df8-135">Para ajustar a escala de um Plano do Serviço de Aplicativo existente, use:</span><span class="sxs-lookup"><span data-stu-id="79df8-135">To scale an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --instances 9

#### <a name="changing-the-sku-of-an-app-service-plan"></a><span data-ttu-id="79df8-136">Como alterar o SKU de um Plano do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="79df8-136">Changing the SKU of an App Service Plan</span></span>
<span data-ttu-id="79df8-137">Para alterar o SKU de um Plano do Serviço de Aplicativo existente, use:</span><span class="sxs-lookup"><span data-stu-id="79df8-137">To change the sku of an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1


### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="79df8-138">Excluir um Plano do Serviço de Aplicativo existente</span><span class="sxs-lookup"><span data-stu-id="79df8-138">Delete an existing App Service Plan</span></span>
<span data-ttu-id="79df8-139">Para excluir um plano do serviço de aplicativo existente, todos os aplicativos atribuídos precisam ser movidos ou excluídos primeiro.</span><span class="sxs-lookup"><span data-stu-id="79df8-139">To delete an existing app service plan, all assigned apps need to be moved or deleted first.</span></span> <span data-ttu-id="79df8-140">Em seguida, com o comando **azure webapp delete**, você pode excluir o plano do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="79df8-140">Then using the **azure webapp delete** command you can delete the app service plan.</span></span>

    azure appserviceplan delete --name ContosoAppServicePlan --resource-group southeastasia

## <a name="managing-app-service-apps"></a><span data-ttu-id="79df8-141">Gerenciando aplicativos do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="79df8-141">Managing App Service apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="79df8-142">Criar um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="79df8-142">Create a web app</span></span>
<span data-ttu-id="79df8-143">Para criar um aplicativo Web, use o comando **azure webapp create**.</span><span class="sxs-lookup"><span data-stu-id="79df8-143">To create a web app, use the **azure webapp create** command.</span></span>

<span data-ttu-id="79df8-144">A seguir estão as descrições dos diferentes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="79df8-144">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="79df8-145">**--name**: o nome do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="79df8-145">**--name**: name for the web app.</span></span>
* <span data-ttu-id="79df8-146">**--plan**: o nome do plano do serviço usado para hospedar o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="79df8-146">**--plan**: name for the service plan used to host the web app.</span></span>
* <span data-ttu-id="79df8-147">**--resource-group**: o grupo de recursos que hospeda o plano do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="79df8-147">**--resource-group**: resource group that hosts the App service plan.</span></span>
* <span data-ttu-id="79df8-148">**--location**: a localização do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="79df8-148">**--location**: the web app location.</span></span>

<span data-ttu-id="79df8-149">Exemplo para usar este cmdlet:</span><span class="sxs-lookup"><span data-stu-id="79df8-149">Example to use this cmdlet:</span></span>

    azure webapp create --name ContosoWebApp --resource-group ContosoAzureResourceGroup --plan ContosoAppServicePlan --location "South Central US"

### <a name="delete-an-existing-app"></a><span data-ttu-id="79df8-150">Excluir um aplicativo existente</span><span class="sxs-lookup"><span data-stu-id="79df8-150">Delete an existing app</span></span>
<span data-ttu-id="79df8-151">Para excluir um aplicativo existente, você pode usar o comando **azure webapp delete**.</span><span class="sxs-lookup"><span data-stu-id="79df8-151">To delete an existing app, you can use the **azure webapp delete** command.</span></span> <span data-ttu-id="79df8-152">Você precisa especificar o nome do aplicativo e o nome do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="79df8-152">You need to specify the name of the app and the resource group name.</span></span>

    azure webapp delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="list-existing-apps"></a><span data-ttu-id="79df8-153">Listar aplicativos existentes</span><span class="sxs-lookup"><span data-stu-id="79df8-153">List existing apps</span></span>
<span data-ttu-id="79df8-154">Para listar os aplicativos existentes, use o comando **azure webapp list**.</span><span class="sxs-lookup"><span data-stu-id="79df8-154">To list the existing apps, use the **azure webapp list** command.</span></span>

<span data-ttu-id="79df8-155">Para listar todos os aplicativos em um grupo de recursos específico, use:</span><span class="sxs-lookup"><span data-stu-id="79df8-155">To list all apps in a specific resource group, use:</span></span>

    azure webapp list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="79df8-156">Para obter um aplicativo específico, use o comando **azure webapp show**.</span><span class="sxs-lookup"><span data-stu-id="79df8-156">To get a specific app, use the **azure webapp show** command.</span></span>

    azure webapp show --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="configure-an-existing-app"></a><span data-ttu-id="79df8-157">Configurar um aplicativo existente</span><span class="sxs-lookup"><span data-stu-id="79df8-157">Configure an existing app</span></span>
<span data-ttu-id="79df8-158">Para alterar as definições e configurações de um aplicativo existente, use o comando **azure webapp config set**.</span><span class="sxs-lookup"><span data-stu-id="79df8-158">To change the settings and configurations for an existing app, use the **azure webapp config set** command.</span></span>

<span data-ttu-id="79df8-159">Exemplo (1): alterar a versão php de um aplicativo</span><span class="sxs-lookup"><span data-stu-id="79df8-159">Example (1): change the php version of a app</span></span> 

    azure webapp config set --name ContosoWebApp --resource-group ContosoAzureResourceGroup --phpversion 5.6

<span data-ttu-id="79df8-160">Exemplo (2): adicionar ou alterar as configurações do aplicativo</span><span class="sxs-lookup"><span data-stu-id="79df8-160">Example (2): add or change app settings</span></span>

    webapp config appsettings set --name ContosoWebApp --resource-group ContosoAzureResourceGroup appsetting1=appsetting1value,appsetting2=appsetting2value

<span data-ttu-id="79df8-161">Para saber que outras configurações podem ser alteradas, use o comando **azure webapp config set -h**.</span><span class="sxs-lookup"><span data-stu-id="79df8-161">To know what other configuration can be changed, use the **azure webapp config set -h** command.</span></span>

### <a name="change-the-state-of-an-existing-app"></a><span data-ttu-id="79df8-162">Alterar o estado de um aplicativo existente</span><span class="sxs-lookup"><span data-stu-id="79df8-162">Change the state of an existing app</span></span>
#### <a name="restart-an-app"></a><span data-ttu-id="79df8-163">Reiniciar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="79df8-163">Restart an app</span></span>
<span data-ttu-id="79df8-164">Para reiniciar um aplicativo, você deve especificar o nome e grupo de recursos do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="79df8-164">To restart an app, you must specify the name and resource group of the app.</span></span>

    azure webapp restart --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="stop-an-app"></a><span data-ttu-id="79df8-165">Interromper um aplicativo</span><span class="sxs-lookup"><span data-stu-id="79df8-165">Stop an app</span></span>
<span data-ttu-id="79df8-166">Para interromper um aplicativo, você deve especificar o nome e grupo de recursos do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="79df8-166">To stop an app, you must specify the name and resource group of the app.</span></span>

    azure webapp stop --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="start-an-app"></a><span data-ttu-id="79df8-167">Iniciar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="79df8-167">Start an app</span></span>
<span data-ttu-id="79df8-168">Para iniciar um aplicativo, você deve especificar o nome e grupo de recursos do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="79df8-168">To start an app, you must specify the name and resource group of the app.</span></span>

    azure webapp start --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="manage-publishing-profiles-of-an-app"></a><span data-ttu-id="79df8-169">Gerenciar perfis de publicação de um aplicativo</span><span class="sxs-lookup"><span data-stu-id="79df8-169">Manage publishing profiles of an app</span></span>
<span data-ttu-id="79df8-170">Cada aplicativo tem um perfil de publicação que pode ser usado para publicar seu código.</span><span class="sxs-lookup"><span data-stu-id="79df8-170">Each app has a publishing profile that can be used to publish your code.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="79df8-171">Obter o perfil de publicação</span><span class="sxs-lookup"><span data-stu-id="79df8-171">Get Publishing Profile</span></span>
<span data-ttu-id="79df8-172">Para obter o perfil de publicação para um aplicativo, use:</span><span class="sxs-lookup"><span data-stu-id="79df8-172">To get the publishing profile for a app, use:</span></span>

    azure webapp publishingprofile --name ContosoWebApp --resource-group ContosoAzureResourceGroup

<span data-ttu-id="79df8-173">Esse comando ecoa o nome de perfil de publicação e a senha para a linha de comando.</span><span class="sxs-lookup"><span data-stu-id="79df8-173">This command echoes the publishing profile username and password to the command line.</span></span>

### <a name="manage-app-hostnames"></a><span data-ttu-id="79df8-174">Gerenciar nomes do host de aplicativo</span><span class="sxs-lookup"><span data-stu-id="79df8-174">Manage app hostnames</span></span>
<span data-ttu-id="79df8-175">Para gerenciar associações de nome do host para seu aplicativo, use o comando **azure webapp config hostnames**</span><span class="sxs-lookup"><span data-stu-id="79df8-175">To manage hostname bindings for your app, use the **azure webapp config hostnames** command</span></span>  

#### <a name="list-hostname-bindings"></a><span data-ttu-id="79df8-176">Listar associações de nome de host</span><span class="sxs-lookup"><span data-stu-id="79df8-176">List hostname bindings</span></span>
<span data-ttu-id="79df8-177">Para obter as associações de nome do host atuais de um aplicativo, use:</span><span class="sxs-lookup"><span data-stu-id="79df8-177">To get the current hostname bindings for an app, use:</span></span>

    azure webapp config hostnames list --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="add-hostname-bindings"></a><span data-ttu-id="79df8-178">Adicionar associações de nome de host</span><span class="sxs-lookup"><span data-stu-id="79df8-178">Add hostname bindings</span></span>
<span data-ttu-id="79df8-179">Para adicionar associações de nome do host de um aplicativo, use:</span><span class="sxs-lookup"><span data-stu-id="79df8-179">To add hostname bindings to an app, use:</span></span>

    azure webapp config hostnames add --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

#### <a name="delete-hostname-bindings"></a><span data-ttu-id="79df8-180">Excluir associações de nome de host</span><span class="sxs-lookup"><span data-stu-id="79df8-180">Delete hostname bindings</span></span>
<span data-ttu-id="79df8-181">Para excluir associações de nome de host, use:</span><span class="sxs-lookup"><span data-stu-id="79df8-181">To delete hostname bindings, use:</span></span>

    azure webapp config hostnames delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

## <a name="next-steps"></a><span data-ttu-id="79df8-182">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="79df8-182">Next Steps</span></span>
* <span data-ttu-id="79df8-183">Para saber mais sobre o suporte da CLI do Azure Resource Manager, veja [Usar a CLI do Azure para gerenciar recursos e grupos de recursos do Azure](../azure-resource-manager/xplat-cli-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="79df8-183">To learn about Azure Resource Manager CLI support, see [Use the Azure CLI to manage Azure resources and resource groups.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)</span></span>
* <span data-ttu-id="79df8-184">Para saber mais sobre como gerenciar o Serviço de Aplicativo usando o PowerShell, veja [Como usar o PowerShell baseado no Azure Resource Manager para gerenciar Aplicativos Web do Azure.](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="79df8-184">To learn about managing App Service using PowerShell, see [Using Azure Resource Manager-Based PowerShell to Manage Azure Web Apps.](app-service-web-app-azure-resource-manager-powershell.md)</span></span>
* <span data-ttu-id="79df8-185">Para saber mais sobre o Serviço de Aplicativo do Azure no Linux, veja [Introdução ao Serviço de Aplicativo no Linux.](app-service-linux-intro.md)</span><span class="sxs-lookup"><span data-stu-id="79df8-185">To learn about Azure App Service on Linux, see [Introduction to App Service on Linux](app-service-linux-intro.md)</span></span>
