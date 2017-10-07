---
title: aaaAzure perguntas Frequentes do IoT Suite | Microsoft Docs
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
ms.openlocfilehash: cb39e24af6d1ce2afea554285512d05b2d7c721e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-iot-suite"></a><span data-ttu-id="e5076-103">Perguntas frequentes sobre o IoT Suite</span><span class="sxs-lookup"><span data-stu-id="e5076-103">Frequently asked questions for IoT Suite</span></span>

<span data-ttu-id="e5076-104">Consulte também, Olá fábrica conectado específico [perguntas frequentes sobre](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="e5076-104">See also, hello connected factory specific [FAQ](iot-suite-faq-cf.md).</span></span>

### <a name="where-can-i-find-hello-source-code-for-hello-preconfigured-solutions"></a><span data-ttu-id="e5076-105">Onde posso encontrar o código-fonte Olá para soluções de saudação pré-configurado?</span><span class="sxs-lookup"><span data-stu-id="e5076-105">Where can I find hello source code for hello preconfigured solutions?</span></span>

<span data-ttu-id="e5076-106">código-fonte Olá é armazenado no hello repositórios GitHub a seguir:</span><span class="sxs-lookup"><span data-stu-id="e5076-106">hello source code is stored in hello following GitHub repositories:</span></span>
* <span data-ttu-id="e5076-107">[Solução pré-configurada de monitoramento remoto][lnk-remote-monitoring-github]</span><span class="sxs-lookup"><span data-stu-id="e5076-107">[Remote monitoring preconfigured solution][lnk-remote-monitoring-github]</span></span>
* <span data-ttu-id="e5076-108">[Solução pré-configurada de manutenção preditiva][lnk-predictive-maintenance-github]</span><span class="sxs-lookup"><span data-stu-id="e5076-108">[Predictive maintenance preconfigured solution][lnk-predictive-maintenance-github]</span></span>
* [<span data-ttu-id="e5076-109">Solução pré-configurada de fábrica conectada</span><span class="sxs-lookup"><span data-stu-id="e5076-109">Connected factory preconfigured solution</span></span>](https://github.com/Azure/azure-iot-connected-factory)

### <a name="how-do-i-update-toohello-latest-version-of-hello-remote-monitoring-preconfigured-solution-that-uses-hello-iot-hub-device-management-features"></a><span data-ttu-id="e5076-110">Como atualizar o toohello versão mais recente do remoto solução pré-configurada monitoramento Olá usa Olá recursos de gerenciamento de dispositivo do IoT Hub?</span><span class="sxs-lookup"><span data-stu-id="e5076-110">How do I update toohello latest version of hello remote monitoring preconfigured solution that uses hello IoT Hub device management features?</span></span>

* <span data-ttu-id="e5076-111">Se você implantar uma solução pré-configurada do site de https://www.azureiotsuite.com/ hello, sempre implanta uma nova instância da versão mais recente de saudação de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="e5076-111">If you deploy a preconfigured solution from hello https://www.azureiotsuite.com/ site, it always deploys a new instance of hello latest version of hello solution.</span></span>
* <span data-ttu-id="e5076-112">Se você implantar uma solução pré-configurada usando a linha de comando hello, você pode atualizar uma implantação existente com o novo código.</span><span class="sxs-lookup"><span data-stu-id="e5076-112">If you deploy a preconfigured solution using hello command line, you can update an existing deployment with new code.</span></span> <span data-ttu-id="e5076-113">Consulte [implantação de nuvem] [ lnk-cloud-deployment] em Olá GitHub [repositório][lnk-remote-monitoring-github].</span><span class="sxs-lookup"><span data-stu-id="e5076-113">See [Cloud deployment][lnk-cloud-deployment] in hello GitHub [repository][lnk-remote-monitoring-github].</span></span>

### <a name="how-can-i-add-support-for-a-new-device-method-toohello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="e5076-114">Como adicionar suporte para um novo dispositivo método toohello solução pré-configurada de monitoramento remoto?</span><span class="sxs-lookup"><span data-stu-id="e5076-114">How can I add support for a new device method toohello remote monitoring preconfigured solution?</span></span>

<span data-ttu-id="e5076-115">Consulte a seção Olá [adicionar suporte para um novo simulador de toohello método] [ lnk-add-method] em Olá [personalizar uma solução pré-configurada] [ lnk-customize] artigo.</span><span class="sxs-lookup"><span data-stu-id="e5076-115">See hello section [Add support for a new method toohello simulator][lnk-add-method] in hello [Customize a preconfigured solution][lnk-customize] article.</span></span>

### <a name="hello-simulated-device-is-ignoring-my-desired-property-changes-why"></a><span data-ttu-id="e5076-116">dispositivo simulado Hello está ignorando as alterações de propriedade desejada, por que?</span><span class="sxs-lookup"><span data-stu-id="e5076-116">hello simulated device is ignoring my desired property changes, why?</span></span>
<span data-ttu-id="e5076-117">Em Olá monitoramento remoto pré-configurado solução, Olá simulado dispositivo código só usa Olá **Desired.Config.TemperatureMeanValue** e **Desired.Config.TelemetryInterval** propriedades desejadas Olá tooupdate relatado propriedades.</span><span class="sxs-lookup"><span data-stu-id="e5076-117">In hello remote monitoring preconfigured solution, hello simulated device code only uses hello **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties tooupdate hello reported properties.</span></span> <span data-ttu-id="e5076-118">Todas as outras solicitações de alteração de propriedade desejadas são ignoradas.</span><span class="sxs-lookup"><span data-stu-id="e5076-118">All other desired property change requests are ignored.</span></span>

### <a name="my-device-does-not-appear-in-hello-list-of-devices-in-hello-solution-dashboard-why"></a><span data-ttu-id="e5076-119">Meu dispositivo não aparecer na lista de saudação de dispositivos no painel da solução hello, por que?</span><span class="sxs-lookup"><span data-stu-id="e5076-119">My device does not appear in hello list of devices in hello solution dashboard, why?</span></span>

<span data-ttu-id="e5076-120">lista de saudação de dispositivos no painel de solução de saudação usa uma lista de saudação do tooreturn de consulta de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="e5076-120">hello list of devices in hello solution dashboard uses a query tooreturn hello list of devices.</span></span> <span data-ttu-id="e5076-121">Atualmente, uma consulta não pode retornar mais de 10 mil dispositivos.</span><span class="sxs-lookup"><span data-stu-id="e5076-121">Currently, a query cannot return more than 10K devices.</span></span> <span data-ttu-id="e5076-122">Tente fazer os critérios de pesquisa de saudação da consulta mais restritivo.</span><span class="sxs-lookup"><span data-stu-id="e5076-122">Try making hello search criteria for your query more restrictive.</span></span>

### <a name="whats-hello-difference-between-deleting-a-resource-group-in-hello-azure-portal-and-clicking-delete-on-a-preconfigured-solution-in-azureiotsuitecom"></a><span data-ttu-id="e5076-123">Qual é a diferença de saudação entre a exclusão de um grupo de recursos no hello Azure portal e clicando em Excluir em uma solução pré-configurada em azureiotsuite.com?</span><span class="sxs-lookup"><span data-stu-id="e5076-123">What's hello difference between deleting a resource group in hello Azure portal and clicking delete on a preconfigured solution in azureiotsuite.com?</span></span>

* <span data-ttu-id="e5076-124">Se você excluir a solução Olá pré-configurado no [azureiotsuite.com][lnk-azureiotsuite], exclua todos os recursos de saudação que foram provisionados quando você criou a solução Olá pré-configurado.</span><span class="sxs-lookup"><span data-stu-id="e5076-124">If you delete hello preconfigured solution in [azureiotsuite.com][lnk-azureiotsuite], you delete all hello resources that were provisioned when you created hello preconfigured solution.</span></span> <span data-ttu-id="e5076-125">Se você adicionou o grupo de recursos de toohello recursos adicionais, esses recursos também serão excluídos.</span><span class="sxs-lookup"><span data-stu-id="e5076-125">If you added additional resources toohello resource group, these resources are also deleted.</span></span> 
* <span data-ttu-id="e5076-126">Se você excluir o grupo de recursos Olá Olá [portal do Azure][lnk-azure-portal], você apenas excluir recursos, Olá desse grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e5076-126">If you delete hello resource group in hello [Azure portal][lnk-azure-portal], you only delete hello resources in that resource group.</span></span> <span data-ttu-id="e5076-127">Você também precisa aplicativo de Active Directory do Azure hello toodelete associado com a solução Olá pré-configurado no hello [portal clássico do Azure][lnk-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="e5076-127">You also need toodelete hello Azure Active Directory application associated with hello preconfigured solution in hello [Azure classic portal][lnk-classic-portal].</span></span>

### <a name="how-many-iot-hub-instances-can-i-provision-in-a-subscription"></a><span data-ttu-id="e5076-128">Quantas instâncias do Hub IoT posso provisionar em uma assinatura?</span><span class="sxs-lookup"><span data-stu-id="e5076-128">How many IoT Hub instances can I provision in a subscription?</span></span>

<span data-ttu-id="e5076-129">Por padrão, você pode provisionar [10 Hubs IoT por assinatura][link-azuresublimits].</span><span class="sxs-lookup"><span data-stu-id="e5076-129">By default you can provision [10 IoT hubs per subscription][link-azuresublimits].</span></span> <span data-ttu-id="e5076-130">Você pode criar um [tíquete de suporte do Azure] [ link-azuresupportticket] tooraise esse limite.</span><span class="sxs-lookup"><span data-stu-id="e5076-130">You can create an [Azure support ticket][link-azuresupportticket] tooraise this limit.</span></span> <span data-ttu-id="e5076-131">Como resultado, desde que cada solução pré-configurada de provisiona um novo IoT Hub, você só pode provisionar o too10 pré-configurado soluções em uma determinada assinatura.</span><span class="sxs-lookup"><span data-stu-id="e5076-131">As a result, since every preconfigured solution provisions a new IoT Hub, you can only provision up too10 preconfigured solutions in a given subscription.</span></span> 

### <a name="how-many-azure-cosmos-db-instances-can-i-provision-in-a-subscription"></a><span data-ttu-id="e5076-132">Quantas instâncias do Azure Cosmos DB posso provisionar em uma assinatura?</span><span class="sxs-lookup"><span data-stu-id="e5076-132">How many Azure Cosmos DB instances can I provision in a subscription?</span></span>

<span data-ttu-id="e5076-133">Cinquenta.</span><span class="sxs-lookup"><span data-stu-id="e5076-133">Fifty.</span></span> <span data-ttu-id="e5076-134">Você pode criar um [tíquete de suporte do Azure] [ link-azuresupportticket] tooraise esse limite, mas, por padrão, você só pode provisionar 50 instâncias de banco de dados do Cosmos por assinatura.</span><span class="sxs-lookup"><span data-stu-id="e5076-134">You can create an [Azure support ticket][link-azuresupportticket] tooraise this limit, but by default, you can only provision 50 Cosmos DB instances per subscription.</span></span> 

### <a name="how-many-free-bing-maps-apis-can-i-provision-in-a-subscription"></a><span data-ttu-id="e5076-135">Quantas APIs do Bing Mapas Gratuitas posso provisionar em uma assinatura?</span><span class="sxs-lookup"><span data-stu-id="e5076-135">How many Free Bing Maps APIs can I provision in a subscription?</span></span>

<span data-ttu-id="e5076-136">Duas.</span><span class="sxs-lookup"><span data-stu-id="e5076-136">Two.</span></span> <span data-ttu-id="e5076-137">Você só pode criar dois Bing Mapas de Transações Internas de Nível 1 para planos Enterprise em uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="e5076-137">You can create only two Internal Transactions Level 1 Bing Maps for Enterprise plans in an Azure subscription.</span></span> <span data-ttu-id="e5076-138">solução de monitoramento remoto Olá é configurada por padrão com o plano de saudação interno transações de nível 1.</span><span class="sxs-lookup"><span data-stu-id="e5076-138">hello remote monitoring solution is provisioned by default with hello Internal Transactions Level 1 plan.</span></span> <span data-ttu-id="e5076-139">Como resultado, você só pode provisionar o tootwo soluções em uma assinatura sem modificações de monitoramento remoto.</span><span class="sxs-lookup"><span data-stu-id="e5076-139">As a result, you can only provision up tootwo remote monitoring solutions in a subscription with no modifications.</span></span>

### <a name="i-have-a-remote-monitoring-solution-deployment-with-a-static-map-how-do-i-add-an-interactive-bing-map"></a><span data-ttu-id="e5076-140">Tenho uma implantação de solução de monitoramento remoto com um mapa estático, como posso adicionar um mapa interativo do Bing?</span><span class="sxs-lookup"><span data-stu-id="e5076-140">I have a remote monitoring solution deployment with a static map, how do I add an interactive Bing map?</span></span>

1. <span data-ttu-id="e5076-141">Obtenha a QueryKey da API do Bing Mapas para Empresas no [Portal do Azure][lnk-azure-portal]:</span><span class="sxs-lookup"><span data-stu-id="e5076-141">Get your Bing Maps API for Enterprise QueryKey from [Azure portal][lnk-azure-portal]:</span></span> 
   
   1. <span data-ttu-id="e5076-142">Navegue toohello grupo de recursos onde a API do Bing Maps para a empresa está Olá [portal do Azure][lnk-azure-portal].</span><span class="sxs-lookup"><span data-stu-id="e5076-142">Navigate toohello Resource Group where your Bing Maps API for Enterprise is in hello [Azure portal][lnk-azure-portal].</span></span>
   2. <span data-ttu-id="e5076-143">Clique em **Todas as Configurações** e em **Gerenciamento de Chaves**.</span><span class="sxs-lookup"><span data-stu-id="e5076-143">Click **All Settings**, then **Key Management**.</span></span> 
   3. <span data-ttu-id="e5076-144">Você pode ver duas chaves: **MasterKey** e **QueryKey**.</span><span class="sxs-lookup"><span data-stu-id="e5076-144">You can see two keys: **MasterKey** and **QueryKey**.</span></span> <span data-ttu-id="e5076-145">Copiar valor Olá **QueryKey**.</span><span class="sxs-lookup"><span data-stu-id="e5076-145">Copy hello value for **QueryKey**.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="e5076-146">Você não tem uma conta da API do Bing Maps para Empresa?</span><span class="sxs-lookup"><span data-stu-id="e5076-146">Don't have a Bing Maps API for Enterprise account?</span></span> <span data-ttu-id="e5076-147">Criar um no hello [portal do Azure] [ lnk-azure-portal] clicando + novo, procurando a API do Bing Maps para Enterprise e siga solicita toocreate.</span><span class="sxs-lookup"><span data-stu-id="e5076-147">Create one in hello [Azure portal][lnk-azure-portal] by clicking + New, searching for Bing Maps API for Enterprise and follow prompts toocreate.</span></span>
      > 
      > 
2. <span data-ttu-id="e5076-148">Suspenso código mais recente de saudação do hello [Azure-IoT-monitoramento remoto][lnk-remote-monitoring-github].</span><span class="sxs-lookup"><span data-stu-id="e5076-148">Pull down hello latest code from hello [Azure-IoT-Remote-Monitoring][lnk-remote-monitoring-github].</span></span>
3. <span data-ttu-id="e5076-149">Executar um local ou seguindo as diretrizes de implantação de linha de comando de saudação na pasta de /docs/ Olá no repositório de saudação de implantação de nuvem.</span><span class="sxs-lookup"><span data-stu-id="e5076-149">Run a local or cloud deployment following hello command-line deployment guidance in hello /docs/ folder in hello repository.</span></span> 
4. <span data-ttu-id="e5076-150">Depois que você tiver executado um local ou nuvem de implantação, procure na pasta raiz para hello *. config arquivo criado durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="e5076-150">After you've run a local or cloud deployment, look in your root folder for hello *.user.config file created during deployment.</span></span> <span data-ttu-id="e5076-151">Abra esse arquivo em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="e5076-151">Open this file in a text editor.</span></span> 
5. <span data-ttu-id="e5076-152">Alteração Olá linha tooinclude valor de saudação que você copiou de seu **QueryKey**:</span><span class="sxs-lookup"><span data-stu-id="e5076-152">Change hello following line tooinclude hello value you copied from your **QueryKey**:</span></span> 
   
   `<setting name="MapApiQueryKey" value="" />`

### <a name="can-i-create-a-preconfigured-solution-if-i-have-microsoft-azure-for-dreamspark"></a><span data-ttu-id="e5076-153">Posso criar uma solução pré-configurada se possuo o Microsoft Azure para DreamSpark?</span><span class="sxs-lookup"><span data-stu-id="e5076-153">Can I create a preconfigured solution if I have Microsoft Azure for DreamSpark?</span></span>

<span data-ttu-id="e5076-154">Atualmente, você não pode criar uma solução pré-configurada com uma conta do [Microsoft Azure para DreamSpark][lnk-dreamspark].</span><span class="sxs-lookup"><span data-stu-id="e5076-154">Currently, you cannot create a preconfigured solution with a [Microsoft Azure for DreamSpark][lnk-dreamspark] account.</span></span> <span data-ttu-id="e5076-155">No entanto, você pode criar uma [conta de avaliação gratuita do Azure][lnk-30daytrial] em apenas alguns minutos que permite a você criar uma solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="e5076-155">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span></span>

### <a name="can-i-create-a-preconfigured-solution-if-i-have-cloud-solution-provider-csp-subscription"></a><span data-ttu-id="e5076-156">Poderei criar uma solução pré-configurada se eu tiver uma assinatura do CSP (Provedor de Soluções na Nuvem)?</span><span class="sxs-lookup"><span data-stu-id="e5076-156">Can I create a preconfigured solution if I have Cloud Solution Provider (CSP) subscription?</span></span>

<span data-ttu-id="e5076-157">Atualmente, não é possível criar uma solução pré-configurada com uma assinatura do CSP (Provedor de Soluções na Nuvem).</span><span class="sxs-lookup"><span data-stu-id="e5076-157">Currently, you cannot create a preconfigured solution with a Cloud Solution Provider (CSP) subscription.</span></span> <span data-ttu-id="e5076-158">No entanto, você pode criar uma [conta de avaliação gratuita do Azure][lnk-30daytrial] em apenas alguns minutos que permite a você criar uma solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="e5076-158">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span></span>

### <a name="how-do-i-delete-an-aad-tenant"></a><span data-ttu-id="e5076-159">Como posso excluir um locatário do AAD?</span><span class="sxs-lookup"><span data-stu-id="e5076-159">How do I delete an AAD tenant?</span></span>

<span data-ttu-id="e5076-160">Veja a postagem do blog de Eric Golpe, [Walkthrough of Deleting an Azure AD Tenant][lnk-delete-aad-tennant] (Passo a passo da exclusão de um locatário do Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e5076-160">See Eric Golpe's blog post [Walkthrough of Deleting an Azure AD Tenant][lnk-delete-aad-tennant].</span></span>

### <a name="next-steps"></a><span data-ttu-id="e5076-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e5076-161">Next steps</span></span>

<span data-ttu-id="e5076-162">Você também pode explorar alguns Olá outros recursos e capacidades de soluções do IoT Suite pré-configurado hello:</span><span class="sxs-lookup"><span data-stu-id="e5076-162">You can also explore some of hello other features and capabilities of hello IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="e5076-163">[Visão geral da solução pré-configurada de manutenção preditiva][lnk-predictive-overview]</span><span class="sxs-lookup"><span data-stu-id="e5076-163">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span></span>
* [<span data-ttu-id="e5076-164">Visão geral da solução pré-configurada de fábrica conectada</span><span class="sxs-lookup"><span data-stu-id="e5076-164">Connected factory preconfigured solution overview</span></span>](iot-suite-connected-factory-overview.md)
* <span data-ttu-id="e5076-165">[Segurança de IoT da saudação de plano de fundo para cima][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="e5076-165">[IoT security from hello ground up][lnk-security-groundup]</span></span>

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
