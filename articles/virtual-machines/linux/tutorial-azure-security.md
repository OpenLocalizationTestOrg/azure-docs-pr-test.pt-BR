---
title: "aaaAzure máquinas virtuais a Central de segurança e Linux no Azure | Microsoft Docs"
description: "Saiba mais sobre a segurança de sua máquina virtual do Linux do Azure com a Central de Segurança do Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/07/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7aa0de35fb311457e769f152c8575ec43e41c39c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-virtual-machine-security-by-using-azure-security-center"></a><span data-ttu-id="bf367-103">Monitorar a segurança da máquina virtual usando a Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="bf367-103">Monitor virtual machine security by using Azure Security Center</span></span>

<span data-ttu-id="bf367-104">A Central de Segurança do Azure pode ajudá-lo a ganhar visibilidade em suas práticas de segurança de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf367-104">Azure Security Center can help you gain visibility into your Azure resource security practices.</span></span> <span data-ttu-id="bf367-105">A Central de segurança oferece o monitoramento de segurança integrado.</span><span class="sxs-lookup"><span data-stu-id="bf367-105">Security Center offers integrated security monitoring.</span></span> <span data-ttu-id="bf367-106">Ela pode detectar ameaças que não seriam notadas de outra forma.</span><span class="sxs-lookup"><span data-stu-id="bf367-106">It can detect threats that otherwise might go unnoticed.</span></span> <span data-ttu-id="bf367-107">Neste tutorial, você saberá mais sobre a Central de Segurança do Azure e como:</span><span class="sxs-lookup"><span data-stu-id="bf367-107">In this tutorial, you learn about Azure Security Center, and how to:</span></span>
 
> [!div class="checklist"]
> * <span data-ttu-id="bf367-108">Configurar a coleta de dados</span><span class="sxs-lookup"><span data-stu-id="bf367-108">Set up data collection</span></span>
> * <span data-ttu-id="bf367-109">Definir políticas de segurança</span><span class="sxs-lookup"><span data-stu-id="bf367-109">Set up security policies</span></span>
> * <span data-ttu-id="bf367-110">Exibir e corrigir problemas de integridade de configuração</span><span class="sxs-lookup"><span data-stu-id="bf367-110">View and fix configuration health issues</span></span>
> * <span data-ttu-id="bf367-111">Examinar ameaças detectadas</span><span class="sxs-lookup"><span data-stu-id="bf367-111">Review detected threats</span></span>  

## <a name="security-center-overview"></a><span data-ttu-id="bf367-112">Visão geral da Central de Segurança</span><span class="sxs-lookup"><span data-stu-id="bf367-112">Security Center overview</span></span>

<span data-ttu-id="bf367-113">A Central de Segurança do Azure identifica possíveis problemas de configuração da VM (máquina virtual) e ameaças de segurança direcionadas.</span><span class="sxs-lookup"><span data-stu-id="bf367-113">Security Center identifies potential virtual machine (VM) configuration issues and targeted security threats.</span></span> <span data-ttu-id="bf367-114">Elas podem incluir VMs que não tenham grupos de segurança de rede, discos não criptografados e ataques de protocolo RDP de força bruta.</span><span class="sxs-lookup"><span data-stu-id="bf367-114">These might include VMs that are missing network security groups, unencrypted disks, and brute-force Remote Desktop Protocol (RDP) attacks.</span></span> <span data-ttu-id="bf367-115">Olá informações são mostradas no painel de Central de segurança Olá nos gráficos de fácil leitura.</span><span class="sxs-lookup"><span data-stu-id="bf367-115">hello information is shown on hello Security Center dashboard in easy-to-read graphs.</span></span>

<span data-ttu-id="bf367-116">tooaccess Olá painel central de segurança, em Olá portal do Azure, no menu de saudação, selecione **Central de segurança**.</span><span class="sxs-lookup"><span data-stu-id="bf367-116">tooaccess hello Security Center dashboard, in hello Azure portal, on hello menu, select  **Security Center**.</span></span> <span data-ttu-id="bf367-117">No painel de hello, ver Olá integridade da segurança do seu ambiente do Azure, encontrar uma contagem de recomendações atuais e exibir hello o estado atual de alertas de ameaça.</span><span class="sxs-lookup"><span data-stu-id="bf367-117">On hello dashboard, you can see hello security health of your Azure environment, find a count of current recommendations, and view hello current state of threat alerts.</span></span> <span data-ttu-id="bf367-118">Você pode expandir cada gráfico de alto nível toosee mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="bf367-118">You can expand each high-level chart toosee more detail.</span></span>

![Painel da Central de Segurança](./media/tutorial-azure-security/asc-dash.png)

<span data-ttu-id="bf367-120">Central de segurança vai além das recomendações de tooprovide de descoberta de dados para problemas detectados.</span><span class="sxs-lookup"><span data-stu-id="bf367-120">Security Center goes beyond data discovery tooprovide recommendations for issues that it detects.</span></span> <span data-ttu-id="bf367-121">Por exemplo, se uma VM foi implantada sem um grupo de segurança de rede, a Central de segurança exibe uma recomendação com etapas de solução que você pode tomar.</span><span class="sxs-lookup"><span data-stu-id="bf367-121">For example, if a VM was deployed without an attached network security group, Security Center displays a recommendation, with remediation steps you can take.</span></span> <span data-ttu-id="bf367-122">Você pode obter retificação automatizada sem sair do contexto de saudação da Central de segurança.</span><span class="sxs-lookup"><span data-stu-id="bf367-122">You get automated remediation without leaving hello context of Security Center.</span></span>  

![Recomendações](./media/tutorial-azure-security/recommendations.png)

## <a name="set-up-data-collection"></a><span data-ttu-id="bf367-124">Configurar a coleta de dados</span><span class="sxs-lookup"><span data-stu-id="bf367-124">Set up data collection</span></span>

<span data-ttu-id="bf367-125">Antes de poder obter visibilidade em configurações de segurança VM, você precisa tooset a coleta de dados da Central de segurança.</span><span class="sxs-lookup"><span data-stu-id="bf367-125">Before you can get visibility into VM security configurations, you need tooset up Security Center data collection.</span></span> <span data-ttu-id="bf367-126">Isso envolve ativar a coleta de dados e criar um toohold coletado dados da conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf367-126">This involves turning on data collection and creating an Azure storage account toohold collected data.</span></span> 

1. <span data-ttu-id="bf367-127">No painel de Central de segurança hello, clique em **política de segurança**e, em seguida, selecione sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="bf367-127">On hello Security Center dashboard, click **Security policy**, and then select your subscription.</span></span> 
2. <span data-ttu-id="bf367-128">Em **Coleta de dados**, selecione **Ativada**.</span><span class="sxs-lookup"><span data-stu-id="bf367-128">For **Data collection**, select **On**.</span></span>
3. <span data-ttu-id="bf367-129">toocreate uma conta de armazenamento, selecione **escolha uma conta de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="bf367-129">toocreate a storage account, select **Choose a storage account**.</span></span> <span data-ttu-id="bf367-130">Depois, selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="bf367-130">Then, select **OK**.</span></span>
4. <span data-ttu-id="bf367-131">Em Olá **política de segurança** folha, selecione **salvar**.</span><span class="sxs-lookup"><span data-stu-id="bf367-131">On hello **Security Policy** blade, select **Save**.</span></span> 

<span data-ttu-id="bf367-132">Agente de coleta de dados Olá Central de segurança é instalado em todas as VMs e começa a coleta de dados.</span><span class="sxs-lookup"><span data-stu-id="bf367-132">hello Security Center data collection agent is then installed on all VMs, and data collection begins.</span></span> 

## <a name="set-up-a-security-policy"></a><span data-ttu-id="bf367-133">Configurar uma política de segurança</span><span class="sxs-lookup"><span data-stu-id="bf367-133">Set up a security policy</span></span>

<span data-ttu-id="bf367-134">Políticas de segurança são itens de saudação toodefine usado para o qual a Central de segurança coleta dados e faz recomendações.</span><span class="sxs-lookup"><span data-stu-id="bf367-134">Security policies are used toodefine hello items for which Security Center collects data and makes recommendations.</span></span> <span data-ttu-id="bf367-135">Você pode aplicar conjuntos de toodifferent de políticas de segurança diferentes de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf367-135">You can apply different security policies toodifferent sets of Azure resources.</span></span> <span data-ttu-id="bf367-136">Embora, por padrão, os recursos do Azure são avaliados em relação a todos os itens de política, você pode desativar itens individuais de política para todos os recursos do Azure ou para um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="bf367-136">Although by default Azure resources are evaluated against all policy items, you can turn off individual policy items for all Azure resources or for a resource group.</span></span> <span data-ttu-id="bf367-137">Para obter informações detalhadas sobre as políticas de segurança da Central de Segurança, consulte [Definir políticas de segurança na Central de Segurança do Azure](../../security-center/security-center-policies.md).</span><span class="sxs-lookup"><span data-stu-id="bf367-137">For in-depth information about Security Center security policies, see [Set security policies in Azure Security Center](../../security-center/security-center-policies.md).</span></span> 

<span data-ttu-id="bf367-138">tooset uma política de segurança para todos os recursos do Azure:</span><span class="sxs-lookup"><span data-stu-id="bf367-138">tooset up a security policy for all Azure resources:</span></span>

1. <span data-ttu-id="bf367-139">No painel de Central de segurança hello, selecione **política de segurança**e, em seguida, selecione sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="bf367-139">On hello Security Center dashboard, select **Security policy**, and then select your subscription.</span></span>
2. <span data-ttu-id="bf367-140">Selecione **Política de prevenção**.</span><span class="sxs-lookup"><span data-stu-id="bf367-140">Select **Prevention policy**.</span></span>
3. <span data-ttu-id="bf367-141">Ativar ou desativar recursos do Azure itens de política que você deseja tooapply tooall.</span><span class="sxs-lookup"><span data-stu-id="bf367-141">Turn on or turn off policy items that you want tooapply tooall Azure resources.</span></span>
4. <span data-ttu-id="bf367-142">Quando terminar de selecionar as configurações, selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="bf367-142">When you're finished selecting your settings, select **OK**.</span></span>
5. <span data-ttu-id="bf367-143">Em Olá **política de segurança** folha, selecione **salvar**.</span><span class="sxs-lookup"><span data-stu-id="bf367-143">On hello **Security policy** blade, select **Save**.</span></span> 

<span data-ttu-id="bf367-144">tooset uma política para um grupo de recursos específicos:</span><span class="sxs-lookup"><span data-stu-id="bf367-144">tooset up a policy for a specific resource group:</span></span>

1. <span data-ttu-id="bf367-145">No painel de Central de segurança hello, selecione **política de segurança**e, em seguida, selecione um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="bf367-145">On hello Security Center dashboard, select **Security policy**, and then select a resource group.</span></span>
2. <span data-ttu-id="bf367-146">Selecione **Política de prevenção**.</span><span class="sxs-lookup"><span data-stu-id="bf367-146">Select **Prevention policy**.</span></span>
3. <span data-ttu-id="bf367-147">Ativar ou desativar itens de política que você deseja que o grupo de recursos de toohello tooapply.</span><span class="sxs-lookup"><span data-stu-id="bf367-147">Turn on or turn off policy items that you want tooapply toohello resource group.</span></span>
4. <span data-ttu-id="bf367-148">Em **HERANÇA**, selecione **Exclusivo**.</span><span class="sxs-lookup"><span data-stu-id="bf367-148">Under **INHERITANCE**, select **Unique**.</span></span>
5. <span data-ttu-id="bf367-149">Quando terminar de selecionar as configurações, selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="bf367-149">When you're finished selecting your settings, select **OK**.</span></span>
6. <span data-ttu-id="bf367-150">Em Olá **política de segurança** folha, selecione **salvar**.</span><span class="sxs-lookup"><span data-stu-id="bf367-150">On hello **Security policy** blade, select **Save**.</span></span>  

<span data-ttu-id="bf367-151">Também é possível desativar a coleta de dados para um grupo de recursos específico nesta página.</span><span class="sxs-lookup"><span data-stu-id="bf367-151">You also can turn off data collection for a specific resource group on this page.</span></span>

<span data-ttu-id="bf367-152">Saudação de exemplo a seguir, uma política exclusiva foi criada para um grupo de recursos denominado *myResoureGroup*.</span><span class="sxs-lookup"><span data-stu-id="bf367-152">In hello following example, a unique policy has been created for a resource group named *myResoureGroup*.</span></span> <span data-ttu-id="bf367-153">Nessa política, a criptografia de disco e as recomendações de firewall do aplicativo Web são desabilitadas.</span><span class="sxs-lookup"><span data-stu-id="bf367-153">In this policy, disk encryption and web application firewall recommendations are turned off.</span></span>

![Política exclusiva](./media/tutorial-azure-security/unique-policy.png)

## <a name="view-vm-configuration-health"></a><span data-ttu-id="bf367-155">Exibir a integridade da configuração da VM</span><span class="sxs-lookup"><span data-stu-id="bf367-155">View VM configuration health</span></span>

<span data-ttu-id="bf367-156">Depois que você tiver ativado a coleta de dados e definir uma política de segurança, a Central de segurança começa tooprovide alertas e recomendações.</span><span class="sxs-lookup"><span data-stu-id="bf367-156">After you've turned on data collection and set a security policy, Security Center begins tooprovide alerts and recommendations.</span></span> <span data-ttu-id="bf367-157">Como as VMs são implantadas, agente de coleta de dados hello está instalado.</span><span class="sxs-lookup"><span data-stu-id="bf367-157">As VMs are deployed, hello data collection agent is installed.</span></span> <span data-ttu-id="bf367-158">Central de segurança é populada com os dados de saudação novas VMs.</span><span class="sxs-lookup"><span data-stu-id="bf367-158">Security Center is then populated with data for hello new VMs.</span></span> <span data-ttu-id="bf367-159">Para obter informações detalhadas sobre a integridade de configuração de VM, consulte [Proteger suas VMs na Central de segurança](../../security-center/security-center-virtual-machine-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="bf367-159">For in-depth information about VM configuration health, see [Protect your VMs in Security Center](../../security-center/security-center-virtual-machine-recommendations.md).</span></span> 

<span data-ttu-id="bf367-160">Como os dados são coletados, integridade de recursos Olá para cada VM e os recursos do Azure relacionados é agregada.</span><span class="sxs-lookup"><span data-stu-id="bf367-160">As data is collected, hello resource health for each VM and related Azure resource is aggregated.</span></span> <span data-ttu-id="bf367-161">Olá informações são mostradas em um gráfico de fácil leitura.</span><span class="sxs-lookup"><span data-stu-id="bf367-161">hello information is shown in an easy-to-read chart.</span></span> 

<span data-ttu-id="bf367-162">integridade de recursos tooview:</span><span class="sxs-lookup"><span data-stu-id="bf367-162">tooview resource health:</span></span>

1.  <span data-ttu-id="bf367-163">No painel de Central de segurança hello, em **integridade da segurança do recurso**, selecione **de computação**.</span><span class="sxs-lookup"><span data-stu-id="bf367-163">On hello Security Center dashboard, under **Resource security health**, select **Compute**.</span></span> 
2.  <span data-ttu-id="bf367-164">Em Olá **de computação** folha, selecione **máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="bf367-164">On hello **Compute** blade, select **Virtual machines**.</span></span> <span data-ttu-id="bf367-165">Essa exibição fornece um resumo do status de configuração de saudação para todas as suas VMs.</span><span class="sxs-lookup"><span data-stu-id="bf367-165">This view provides a summary of hello configuration status for all your VMs.</span></span>

![Computar integridade](./media/tutorial-azure-security/compute-health.png)

<span data-ttu-id="bf367-167">toosee todas as recomendações para uma VM, selecione Olá VM.</span><span class="sxs-lookup"><span data-stu-id="bf367-167">toosee all recommendations for a VM, select hello VM.</span></span> <span data-ttu-id="bf367-168">Recomendações e correção são abordados em mais detalhes na próxima seção, Olá deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="bf367-168">Recommendations and remediation are covered in more detail in hello next section of this tutorial.</span></span>

## <a name="remediate-configuration-issues"></a><span data-ttu-id="bf367-169">Corrigir problemas de configuração</span><span class="sxs-lookup"><span data-stu-id="bf367-169">Remediate configuration issues</span></span>

<span data-ttu-id="bf367-170">Depois que a Central de segurança começa toopopulate com dados de configuração, as recomendações são feitas com base na política de segurança Olá que você configurar.</span><span class="sxs-lookup"><span data-stu-id="bf367-170">After Security Center begins toopopulate with configuration data, recommendations are made based on hello security policy you set up.</span></span> <span data-ttu-id="bf367-171">Por exemplo, se uma máquina virtual foi configurada sem um grupo de segurança de rede associados, uma recomendação é feita toocreate um.</span><span class="sxs-lookup"><span data-stu-id="bf367-171">For instance, if a VM was set up without an associated network security group, a recommendation is made toocreate one.</span></span> 

<span data-ttu-id="bf367-172">toosee uma lista de todas as recomendações:</span><span class="sxs-lookup"><span data-stu-id="bf367-172">toosee a list of all recommendations:</span></span> 

1. <span data-ttu-id="bf367-173">No painel de Central de segurança hello, selecione **recomendações**.</span><span class="sxs-lookup"><span data-stu-id="bf367-173">On hello Security Center dashboard, select **Recommendations**.</span></span>
2. <span data-ttu-id="bf367-174">Selecione uma recomendação específica.</span><span class="sxs-lookup"><span data-stu-id="bf367-174">Select a specific recommendation.</span></span> <span data-ttu-id="bf367-175">É exibida uma lista de todos os recursos para o qual se aplica a recomendação de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf367-175">A list of all resources for which hello recommendation applies appears.</span></span>
3. <span data-ttu-id="bf367-176">tooapply uma recomendação, selecione um recurso específico.</span><span class="sxs-lookup"><span data-stu-id="bf367-176">tooapply a recommendation, select a specific resource.</span></span> 
4. <span data-ttu-id="bf367-177">Siga as instruções de saudação para etapas de correção.</span><span class="sxs-lookup"><span data-stu-id="bf367-177">Follow hello instructions for remediation steps.</span></span> 

<span data-ttu-id="bf367-178">Em muitos casos, a Central de segurança fornece etapas acionáveis você pode tomar uma recomendação de tooaddress sem sair da Central de segurança.</span><span class="sxs-lookup"><span data-stu-id="bf367-178">In many cases, Security Center provides actionable steps you can take tooaddress a recommendation without leaving Security Center.</span></span> <span data-ttu-id="bf367-179">Saudação de exemplo a seguir, a Central de segurança detecta um grupo de segurança de rede que tenha uma regra de entrada irrestrita.</span><span class="sxs-lookup"><span data-stu-id="bf367-179">In hello following example, Security Center detects a network security group that has an unrestricted inbound rule.</span></span> <span data-ttu-id="bf367-180">Na página de recomendação hello, você pode selecionar Olá **editar regras de entrada** botão.</span><span class="sxs-lookup"><span data-stu-id="bf367-180">On hello recommendation page, you can select hello **Edit inbound rules** button.</span></span> <span data-ttu-id="bf367-181">Saudação da interface do usuário é necessária toomodify Olá regra é exibida.</span><span class="sxs-lookup"><span data-stu-id="bf367-181">hello UI that is needed toomodify hello rule appears.</span></span> 

![Recomendações](./media/tutorial-azure-security/remediation.png)

<span data-ttu-id="bf367-183">À medida que as recomendações são corrigidas, elas são marcadas como resolvidas.</span><span class="sxs-lookup"><span data-stu-id="bf367-183">As recommendations are remediated, they are marked as resolved.</span></span> 

## <a name="view-detected-threats"></a><span data-ttu-id="bf367-184">Exibir as ameaças detectadas</span><span class="sxs-lookup"><span data-stu-id="bf367-184">View detected threats</span></span>

<span data-ttu-id="bf367-185">Além disso, recomendações de configuração de tooresource, Central de segurança exibe os alertas de detecção de ameaças.</span><span class="sxs-lookup"><span data-stu-id="bf367-185">In addition tooresource configuration recommendations, Security Center displays threat detection alerts.</span></span> <span data-ttu-id="bf367-186">o recurso de alertas de segurança Olá agrega os dados coletados de cada VM, logs de sistema de rede do Azure e parceiro conectado soluções toodetect contra ameaças à segurança com base nos recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf367-186">hello security alerts feature aggregates data collected from each VM, Azure networking logs, and connected partner solutions toodetect security threats against Azure resources.</span></span> <span data-ttu-id="bf367-187">Para obter informações detalhadas sobre as funcionalidades de detecção de ameaças da Central de Segurança, consulte [Funcionalidades de detecção da Central de Segurança do Azure](../../security-center/security-center-detection-capabilities.md).</span><span class="sxs-lookup"><span data-stu-id="bf367-187">For in-depth information about Security Center threat detection capabilities, see [Azure Security Center detection capabilities](../../security-center/security-center-detection-capabilities.md).</span></span>

<span data-ttu-id="bf367-188">o recurso de alertas de segurança Olá requer a Central de segurança Olá preços toobe camada aumentado de *livre* muito*padrão*.</span><span class="sxs-lookup"><span data-stu-id="bf367-188">hello security alerts feature requires hello Security Center pricing tier toobe increased from *Free* too*Standard*.</span></span> <span data-ttu-id="bf367-189">30 dias **avaliação gratuita** está disponível quando você move toothis maior preço.</span><span class="sxs-lookup"><span data-stu-id="bf367-189">A 30-day **free trial** is available when you move toothis higher pricing tier.</span></span> 

<span data-ttu-id="bf367-190">camada de preços toochange hello:</span><span class="sxs-lookup"><span data-stu-id="bf367-190">toochange hello pricing tier:</span></span>  

1. <span data-ttu-id="bf367-191">No painel de Central de segurança hello, clique em **política de segurança**e, em seguida, selecione sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="bf367-191">On hello Security Center dashboard, click **Security policy**, and then select your subscription.</span></span>
2. <span data-ttu-id="bf367-192">Selecione **Tipo de preço**.</span><span class="sxs-lookup"><span data-stu-id="bf367-192">Select **Pricing tier**.</span></span>
3. <span data-ttu-id="bf367-193">Selecione nova camada de saudação e, em seguida, selecione **selecione**.</span><span class="sxs-lookup"><span data-stu-id="bf367-193">Select hello new tier, and then select **Select**.</span></span>
4. <span data-ttu-id="bf367-194">Em Olá **política de segurança** folha, selecione **salvar**.</span><span class="sxs-lookup"><span data-stu-id="bf367-194">On hello **Security policy** blade, select **Save**.</span></span> 

<span data-ttu-id="bf367-195">Depois que você alterou Olá preço, o gráfico de alertas de segurança Olá começa toopopulate que ameaças de segurança são detectadas.</span><span class="sxs-lookup"><span data-stu-id="bf367-195">After you've changed hello pricing tier, hello security alerts graph begins toopopulate as security threats are detected.</span></span>

![Alertas de segurança](./media/tutorial-azure-security/security-alerts.png)

<span data-ttu-id="bf367-197">Selecione um alerta tooview informações.</span><span class="sxs-lookup"><span data-stu-id="bf367-197">Select an alert tooview information.</span></span> <span data-ttu-id="bf367-198">Por exemplo, você pode ver uma descrição de ameaça hello, tempo de detecção de saudação, todas as tentativas de ameaça e Olá correção recomendada.</span><span class="sxs-lookup"><span data-stu-id="bf367-198">For example, you can see a description of hello threat, hello detection time, all threat attempts, and hello recommended remediation.</span></span> <span data-ttu-id="bf367-199">Em Olá exemplo a seguir, um ataque de força bruta do RDP foi detectado, com 294 tentativas RDP.</span><span class="sxs-lookup"><span data-stu-id="bf367-199">In hello following example, an RDP brute-force attack was detected, with 294 failed RDP attempts.</span></span> <span data-ttu-id="bf367-200">Uma solução recomendada é fornecida.</span><span class="sxs-lookup"><span data-stu-id="bf367-200">A recommended resolution is provided.</span></span>

![Ataque de RDP](./media/tutorial-azure-security/rdp-attack.png)

## <a name="next-steps"></a><span data-ttu-id="bf367-202">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bf367-202">Next steps</span></span>
<span data-ttu-id="bf367-203">Nesse tutorial, você configurou a Central de Segurança do Azure e, em seguida, analisou VMs na Central de Segurança.</span><span class="sxs-lookup"><span data-stu-id="bf367-203">In this tutorial, you set up Azure Security Center, and then reviewed VMs in Security Center.</span></span> <span data-ttu-id="bf367-204">Você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="bf367-204">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bf367-205">Configurar a coleta de dados</span><span class="sxs-lookup"><span data-stu-id="bf367-205">Set up data collection</span></span>
> * <span data-ttu-id="bf367-206">Definir políticas de segurança</span><span class="sxs-lookup"><span data-stu-id="bf367-206">Set up security policies</span></span>
> * <span data-ttu-id="bf367-207">Exibir e corrigir problemas de integridade de configuração</span><span class="sxs-lookup"><span data-stu-id="bf367-207">View and fix configuration health issues</span></span>
> * <span data-ttu-id="bf367-208">Examinar ameaças detectadas</span><span class="sxs-lookup"><span data-stu-id="bf367-208">Review detected threats</span></span>

<span data-ttu-id="bf367-209">Avança toohello toolearn de tutorial Avançar mais sobre como criar um pipeline de CI/CD com Jenkins, GitHub e o Docker.</span><span class="sxs-lookup"><span data-stu-id="bf367-209">Advance toohello next tutorial toolearn more about creating a CI/CD pipeline with Jenkins, GitHub, and Docker.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bf367-210">Criar uma infra-estrutura de CI/CD com Jenkins, GitHub e Docker</span><span class="sxs-lookup"><span data-stu-id="bf367-210">Create CI/CD infrastructure with Jenkins, GitHub, and Docker</span></span>](tutorial-jenkins-github-docker-cicd.md)

