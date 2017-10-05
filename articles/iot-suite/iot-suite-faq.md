---
title: Perguntas frequentes sobre o Azure IoT Suite | Microsoft Docs
description: Perguntas frequentes sobre o IoT Suite
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: cb537749-a8a1-4e53-b3bf-f1b64a38188a
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: 85867fb8d18377637b3aa848555831a8d9b53512
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="frequently-asked-questions-for-iot-suite"></a><span data-ttu-id="273d8-103">Perguntas frequentes sobre o IoT Suite</span><span class="sxs-lookup"><span data-stu-id="273d8-103">Frequently asked questions for IoT Suite</span></span>

<span data-ttu-id="273d8-104">Consulte também as [Perguntas frequentes](iot-suite-faq-cf.md) específicas sobre a fábrica conectada.</span><span class="sxs-lookup"><span data-stu-id="273d8-104">See also, the connected factory specific [FAQ](iot-suite-faq-cf.md).</span></span>

### <a name="where-can-i-find-the-source-code-for-the-preconfigured-solutions"></a><span data-ttu-id="273d8-105">Onde encontrar o código-fonte para as soluções pré-configuradas?</span><span class="sxs-lookup"><span data-stu-id="273d8-105">Where can I find the source code for the preconfigured solutions?</span></span>

<span data-ttu-id="273d8-106">O código-fonte é armazenado nos seguintes repositórios GitHub:</span><span class="sxs-lookup"><span data-stu-id="273d8-106">The source code is stored in the following GitHub repositories:</span></span>
* <span data-ttu-id="273d8-107">[Solução pré-configurada de monitoramento remoto][lnk-remote-monitoring-github]</span><span class="sxs-lookup"><span data-stu-id="273d8-107">[Remote monitoring preconfigured solution][lnk-remote-monitoring-github]</span></span>
* <span data-ttu-id="273d8-108">[Solução pré-configurada de manutenção preditiva][lnk-predictive-maintenance-github]</span><span class="sxs-lookup"><span data-stu-id="273d8-108">[Predictive maintenance preconfigured solution][lnk-predictive-maintenance-github]</span></span>
* [<span data-ttu-id="273d8-109">Solução pré-configurada de fábrica conectada</span><span class="sxs-lookup"><span data-stu-id="273d8-109">Connected factory preconfigured solution</span></span>](https://github.com/Azure/azure-iot-connected-factory)

### <a name="how-do-i-update-to-the-latest-version-of-the-remote-monitoring-preconfigured-solution-that-uses-the-iot-hub-device-management-features"></a><span data-ttu-id="273d8-110">Como atualizar para a versão mais recente da solução de monitoramento remoto predefinida que usa os recursos de gerenciamento de dispositivo do Hub IoT?</span><span class="sxs-lookup"><span data-stu-id="273d8-110">How do I update to the latest version of the remote monitoring preconfigured solution that uses the IoT Hub device management features?</span></span>

* <span data-ttu-id="273d8-111">Se você implantar uma solução pré-configurada do site https://www.azureiotsuite.com/, ela sempre implantará uma nova instância da versão mais recente da solução.</span><span class="sxs-lookup"><span data-stu-id="273d8-111">If you deploy a preconfigured solution from the https://www.azureiotsuite.com/ site, it always deploys a new instance of the latest version of the solution.</span></span>
* <span data-ttu-id="273d8-112">Se implantar uma solução pré-configurada usando a linha de comando, você poderá atualizar uma implantação existente com o novo código.</span><span class="sxs-lookup"><span data-stu-id="273d8-112">If you deploy a preconfigured solution using the command line, you can update an existing deployment with new code.</span></span> <span data-ttu-id="273d8-113">Confira [Implantação de nuvem][lnk-cloud-deployment] no [repositório][lnk-remote-monitoring-github] GitHub.</span><span class="sxs-lookup"><span data-stu-id="273d8-113">See [Cloud deployment][lnk-cloud-deployment] in the GitHub [repository][lnk-remote-monitoring-github].</span></span>

### <a name="how-can-i-add-support-for-a-new-device-method-to-the-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="273d8-114">Como adicionar suporte a um novo método de dispositivo para a solução pré-configurada de monitoramento remoto?</span><span class="sxs-lookup"><span data-stu-id="273d8-114">How can I add support for a new device method to the remote monitoring preconfigured solution?</span></span>

<span data-ttu-id="273d8-115">Confira a seção [Adicionar suporte a um novo método para o simulador][lnk-add-method] no artigo [Personalizar uma solução pré-configurada][lnk-customize].</span><span class="sxs-lookup"><span data-stu-id="273d8-115">See the section [Add support for a new method to the simulator][lnk-add-method] in the [Customize a preconfigured solution][lnk-customize] article.</span></span>

### <a name="the-simulated-device-is-ignoring-my-desired-property-changes-why"></a><span data-ttu-id="273d8-116">Por que o dispositivo simulado está ignorando as alterações de propriedade desejadas?</span><span class="sxs-lookup"><span data-stu-id="273d8-116">The simulated device is ignoring my desired property changes, why?</span></span>
<span data-ttu-id="273d8-117">Na solução pré-configurada de monitoramento remoto, o código de dispositivo simulado usa apenas as propriedades desejadas **Desired.Config.TemperatureMeanValue** e **Desired.Config.TelemetryInterval** para atualizar as propriedades relatadas.</span><span class="sxs-lookup"><span data-stu-id="273d8-117">In the remote monitoring preconfigured solution, the simulated device code only uses the **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties to update the reported properties.</span></span> <span data-ttu-id="273d8-118">Todas as outras solicitações de alteração de propriedade desejadas são ignoradas.</span><span class="sxs-lookup"><span data-stu-id="273d8-118">All other desired property change requests are ignored.</span></span>

### <a name="my-device-does-not-appear-in-the-list-of-devices-in-the-solution-dashboard-why"></a><span data-ttu-id="273d8-119">Por que o dispositivo não aparece na lista de dispositivos no painel de solução?</span><span class="sxs-lookup"><span data-stu-id="273d8-119">My device does not appear in the list of devices in the solution dashboard, why?</span></span>

<span data-ttu-id="273d8-120">A lista de dispositivos no painel de solução usa uma consulta para retornar a lista de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="273d8-120">The list of devices in the solution dashboard uses a query to return the list of devices.</span></span> <span data-ttu-id="273d8-121">Atualmente, uma consulta não pode retornar mais de 10 mil dispositivos.</span><span class="sxs-lookup"><span data-stu-id="273d8-121">Currently, a query cannot return more than 10K devices.</span></span> <span data-ttu-id="273d8-122">Tente tornar os critérios de pesquisa da consulta mais restritivos.</span><span class="sxs-lookup"><span data-stu-id="273d8-122">Try making the search criteria for your query more restrictive.</span></span>

### <a name="whats-the-difference-between-deleting-a-resource-group-in-the-azure-portal-and-clicking-delete-on-a-preconfigured-solution-in-azureiotsuitecom"></a><span data-ttu-id="273d8-123">Qual é a diferença entre excluir um grupo de recursos no portal do Azure e clicar em excluir em uma solução pré-configurada no site azureiotsuite.com?</span><span class="sxs-lookup"><span data-stu-id="273d8-123">What's the difference between deleting a resource group in the Azure portal and clicking delete on a preconfigured solution in azureiotsuite.com?</span></span>

* <span data-ttu-id="273d8-124">Se você excluir a solução pré-configurada no site [azureiotsuite.com][lnk-azureiotsuite], todos os recursos provisionados na criação da solução pré-configurada serão excluídos.</span><span class="sxs-lookup"><span data-stu-id="273d8-124">If you delete the preconfigured solution in [azureiotsuite.com][lnk-azureiotsuite], you delete all the resources that were provisioned when you created the preconfigured solution.</span></span> <span data-ttu-id="273d8-125">Se você adicionou mais recursos ao grupo de recursos, esses recursos também serão excluídos.</span><span class="sxs-lookup"><span data-stu-id="273d8-125">If you added additional resources to the resource group, these resources are also deleted.</span></span> 
* <span data-ttu-id="273d8-126">Se você excluir o grupo de recursos no [Portal do Azure][lnk-azure-portal], somente os recursos nesse grupo serão excluídos.</span><span class="sxs-lookup"><span data-stu-id="273d8-126">If you delete the resource group in the [Azure portal][lnk-azure-portal], you only delete the resources in that resource group.</span></span> <span data-ttu-id="273d8-127">Você também precisa excluir o aplicativo do Azure Active Directory associado à solução pré-configurada no [Portal Clássico do Azure][lnk-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="273d8-127">You also need to delete the Azure Active Directory application associated with the preconfigured solution in the [Azure classic portal][lnk-classic-portal].</span></span>

### <a name="how-many-iot-hub-instances-can-i-provision-in-a-subscription"></a><span data-ttu-id="273d8-128">Quantas instâncias do Hub IoT posso provisionar em uma assinatura?</span><span class="sxs-lookup"><span data-stu-id="273d8-128">How many IoT Hub instances can I provision in a subscription?</span></span>

<span data-ttu-id="273d8-129">Por padrão, você pode provisionar [10 Hubs IoT por assinatura][link-azuresublimits].</span><span class="sxs-lookup"><span data-stu-id="273d8-129">By default you can provision [10 IoT hubs per subscription][link-azuresublimits].</span></span> <span data-ttu-id="273d8-130">Você pode criar um [tíquete de suporte do Azure][link-azuresupportticket] para aumentar esse limite.</span><span class="sxs-lookup"><span data-stu-id="273d8-130">You can create an [Azure support ticket][link-azuresupportticket] to raise this limit.</span></span> <span data-ttu-id="273d8-131">Como resultado, uma vez que cada solução pré-configurada provisiona um novo Hub IoT, você só poderá provisionar até 10 soluções pré-configuradas em uma determinada assinatura.</span><span class="sxs-lookup"><span data-stu-id="273d8-131">As a result, since every preconfigured solution provisions a new IoT Hub, you can only provision up to 10 preconfigured solutions in a given subscription.</span></span> 

### <a name="how-many-azure-cosmos-db-instances-can-i-provision-in-a-subscription"></a><span data-ttu-id="273d8-132">Quantas instâncias do Azure Cosmos DB posso provisionar em uma assinatura?</span><span class="sxs-lookup"><span data-stu-id="273d8-132">How many Azure Cosmos DB instances can I provision in a subscription?</span></span>

<span data-ttu-id="273d8-133">Cinquenta.</span><span class="sxs-lookup"><span data-stu-id="273d8-133">Fifty.</span></span> <span data-ttu-id="273d8-134">Você pode criar um [tíquete de suporte do Azure][link-azuresupportticket] para aumentar esse limite, mas por padrão, você poderá apenas provisionar 50 instâncias do Cosmos DB por assinatura.</span><span class="sxs-lookup"><span data-stu-id="273d8-134">You can create an [Azure support ticket][link-azuresupportticket] to raise this limit, but by default, you can only provision 50 Cosmos DB instances per subscription.</span></span> 

### <a name="how-many-free-bing-maps-apis-can-i-provision-in-a-subscription"></a><span data-ttu-id="273d8-135">Quantas APIs do Bing Mapas Gratuitas posso provisionar em uma assinatura?</span><span class="sxs-lookup"><span data-stu-id="273d8-135">How many Free Bing Maps APIs can I provision in a subscription?</span></span>

<span data-ttu-id="273d8-136">Duas.</span><span class="sxs-lookup"><span data-stu-id="273d8-136">Two.</span></span> <span data-ttu-id="273d8-137">Você só pode criar dois Bing Mapas de Transações Internas de Nível 1 para planos Enterprise em uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="273d8-137">You can create only two Internal Transactions Level 1 Bing Maps for Enterprise plans in an Azure subscription.</span></span> <span data-ttu-id="273d8-138">A solução de monitoramento remoto é provisionada por padrão com o plano Transações Internas de Nível 1.</span><span class="sxs-lookup"><span data-stu-id="273d8-138">The remote monitoring solution is provisioned by default with the Internal Transactions Level 1 plan.</span></span> <span data-ttu-id="273d8-139">Como resultado, você só poderá provisionar até duas soluções de monitoramento remotas em uma assinatura sem modificações.</span><span class="sxs-lookup"><span data-stu-id="273d8-139">As a result, you can only provision up to two remote monitoring solutions in a subscription with no modifications.</span></span>

### <a name="i-have-a-remote-monitoring-solution-deployment-with-a-static-map-how-do-i-add-an-interactive-bing-map"></a><span data-ttu-id="273d8-140">Tenho uma implantação de solução de monitoramento remoto com um mapa estático, como posso adicionar um mapa interativo do Bing?</span><span class="sxs-lookup"><span data-stu-id="273d8-140">I have a remote monitoring solution deployment with a static map, how do I add an interactive Bing map?</span></span>

1. <span data-ttu-id="273d8-141">Obtenha a QueryKey da API do Bing Mapas para Empresas no [Portal do Azure][lnk-azure-portal]:</span><span class="sxs-lookup"><span data-stu-id="273d8-141">Get your Bing Maps API for Enterprise QueryKey from [Azure portal][lnk-azure-portal]:</span></span> 
   
   1. <span data-ttu-id="273d8-142">Navegue até o Grupo de Recursos onde está a API do Bing Mapas para Empresas no [Portal do Azure][lnk-azure-portal].</span><span class="sxs-lookup"><span data-stu-id="273d8-142">Navigate to the Resource Group where your Bing Maps API for Enterprise is in the [Azure portal][lnk-azure-portal].</span></span>
   2. <span data-ttu-id="273d8-143">Clique em **Todas as Configurações** e em **Gerenciamento de Chaves**.</span><span class="sxs-lookup"><span data-stu-id="273d8-143">Click **All Settings**, then **Key Management**.</span></span> 
   3. <span data-ttu-id="273d8-144">Você pode ver duas chaves: **MasterKey** e **QueryKey**.</span><span class="sxs-lookup"><span data-stu-id="273d8-144">You can see two keys: **MasterKey** and **QueryKey**.</span></span> <span data-ttu-id="273d8-145">Copie o valor de **QueryKey**.</span><span class="sxs-lookup"><span data-stu-id="273d8-145">Copy the value for **QueryKey**.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="273d8-146">Você não tem uma conta da API do Bing Maps para Empresa?</span><span class="sxs-lookup"><span data-stu-id="273d8-146">Don't have a Bing Maps API for Enterprise account?</span></span> <span data-ttu-id="273d8-147">Crie uma no [Portal do Azure][lnk-azure-portal] clicando em + Novo, procurando pela API do Bing Mapas para Empresas e seguindo os prompts de criação.</span><span class="sxs-lookup"><span data-stu-id="273d8-147">Create one in the [Azure portal][lnk-azure-portal] by clicking + New, searching for Bing Maps API for Enterprise and follow prompts to create.</span></span>
      > 
      > 
2. <span data-ttu-id="273d8-148">Obtenha o código mais recente do [Azure-IoT-Remote-Monitoring][lnk-remote-monitoring-github].</span><span class="sxs-lookup"><span data-stu-id="273d8-148">Pull down the latest code from the [Azure-IoT-Remote-Monitoring][lnk-remote-monitoring-github].</span></span>
3. <span data-ttu-id="273d8-149">Execute uma implantação local ou em nuvem seguindo as diretrizes de implantação de linha de comando na pasta /docs/ do repositório.</span><span class="sxs-lookup"><span data-stu-id="273d8-149">Run a local or cloud deployment following the command-line deployment guidance in the /docs/ folder in the repository.</span></span> 
4. <span data-ttu-id="273d8-150">Depois de executar uma implantação local ou em nuvem, procure na pasta raiz pelo arquivo *.user.config criado durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="273d8-150">After you've run a local or cloud deployment, look in your root folder for the *.user.config file created during deployment.</span></span> <span data-ttu-id="273d8-151">Abra esse arquivo em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="273d8-151">Open this file in a text editor.</span></span> 
5. <span data-ttu-id="273d8-152">Altere a linha a seguir para incluir o valor que você copiou de **QueryKey**:</span><span class="sxs-lookup"><span data-stu-id="273d8-152">Change the following line to include the value you copied from your **QueryKey**:</span></span> 
   
   `<setting name="MapApiQueryKey" value="" />`

### <a name="can-i-create-a-preconfigured-solution-if-i-have-microsoft-azure-for-dreamspark"></a><span data-ttu-id="273d8-153">Posso criar uma solução pré-configurada se possuo o Microsoft Azure para DreamSpark?</span><span class="sxs-lookup"><span data-stu-id="273d8-153">Can I create a preconfigured solution if I have Microsoft Azure for DreamSpark?</span></span>

<span data-ttu-id="273d8-154">Atualmente, você não pode criar uma solução pré-configurada com uma conta do [Microsoft Azure para DreamSpark][lnk-dreamspark].</span><span class="sxs-lookup"><span data-stu-id="273d8-154">Currently, you cannot create a preconfigured solution with a [Microsoft Azure for DreamSpark][lnk-dreamspark] account.</span></span> <span data-ttu-id="273d8-155">No entanto, você pode criar uma [conta de avaliação gratuita do Azure][lnk-30daytrial] em apenas alguns minutos que permite a você criar uma solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="273d8-155">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span></span>

### <a name="can-i-create-a-preconfigured-solution-if-i-have-cloud-solution-provider-csp-subscription"></a><span data-ttu-id="273d8-156">Poderei criar uma solução pré-configurada se eu tiver uma assinatura do CSP (Provedor de Soluções na Nuvem)?</span><span class="sxs-lookup"><span data-stu-id="273d8-156">Can I create a preconfigured solution if I have Cloud Solution Provider (CSP) subscription?</span></span>

<span data-ttu-id="273d8-157">Atualmente, não é possível criar uma solução pré-configurada com uma assinatura do CSP (Provedor de Soluções na Nuvem).</span><span class="sxs-lookup"><span data-stu-id="273d8-157">Currently, you cannot create a preconfigured solution with a Cloud Solution Provider (CSP) subscription.</span></span> <span data-ttu-id="273d8-158">No entanto, você pode criar uma [conta de avaliação gratuita do Azure][lnk-30daytrial] em apenas alguns minutos que permite a você criar uma solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="273d8-158">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span></span>

### <a name="how-do-i-delete-an-aad-tenant"></a><span data-ttu-id="273d8-159">Como posso excluir um locatário do AAD?</span><span class="sxs-lookup"><span data-stu-id="273d8-159">How do I delete an AAD tenant?</span></span>

<span data-ttu-id="273d8-160">Veja a postagem do blog de Eric Golpe, [Walkthrough of Deleting an Azure AD Tenant][lnk-delete-aad-tennant] (Passo a passo da exclusão de um locatário do Azure AD).</span><span class="sxs-lookup"><span data-stu-id="273d8-160">See Eric Golpe's blog post [Walkthrough of Deleting an Azure AD Tenant][lnk-delete-aad-tennant].</span></span>

### <a name="next-steps"></a><span data-ttu-id="273d8-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="273d8-161">Next steps</span></span>

<span data-ttu-id="273d8-162">Você também pode explorar alguns dos outros recursos das soluções pré-configuradas do IoT Suite:</span><span class="sxs-lookup"><span data-stu-id="273d8-162">You can also explore some of the other features and capabilities of the IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="273d8-163">[Visão geral da solução pré-configurada de manutenção preditiva][lnk-predictive-overview]</span><span class="sxs-lookup"><span data-stu-id="273d8-163">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span></span>
* [<span data-ttu-id="273d8-164">Visão geral da solução pré-configurada de fábrica conectada</span><span class="sxs-lookup"><span data-stu-id="273d8-164">Connected factory preconfigured solution overview</span></span>](iot-suite-connected-factory-overview.md)
* <span data-ttu-id="273d8-165">[Segurança IoT desde o início][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="273d8-165">[IoT security from the ground up][lnk-security-groundup]</span></span>

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-security-groundup]: securing-iot-ground-up.md

[link-azuresupportticket]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade 
[link-azuresublimits]: https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/#iot-hub-limits
[lnk-azure-portal]: https://portal.azure.com
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring 
[lnk-dreamspark]: https://www.dreamspark.com/Product/Product.aspx?productid=99 
[lnk-30daytrial]: https://azure.microsoft.com/free/
[lnk-delete-aad-tennant]: http://blogs.msdn.com/b/ericgolpe/archive/2015/04/30/walkthrough-of-deleting-an-azure-ad-tenant.aspx
[lnk-cloud-deployment]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
[lnk-add-method]: iot-suite-guidance-on-customizing-preconfigured-solutions.md#add-support-for-a-new-method-to-the-simulator
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-predictive-maintenance-github]: https://github.com/Azure/azure-iot-predictive-maintenance
