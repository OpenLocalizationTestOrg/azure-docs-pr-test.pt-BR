---
title: "Cotas do serviço e limites do Lote do Azure | Microsoft Docs"
description: "Saiba mais sobre as restrições, limites e cotas padrão do Lote do Azure e como aumentar a cota da solicitação"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 28998df4-8693-431d-b6ad-974c2f8db5fb
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f3f69ed8d3a985afe07e648e7512a88b25278ced
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="batch-service-quotas-and-limits"></a><span data-ttu-id="d4dab-103">Cotas e limites de serviço do Lote</span><span class="sxs-lookup"><span data-stu-id="d4dab-103">Batch service quotas and limits</span></span>

<span data-ttu-id="d4dab-104">Como com outros serviços do Azure, há limites em determinados recursos associados ao serviço de Lote.</span><span class="sxs-lookup"><span data-stu-id="d4dab-104">As with other Azure services, there are limits on certain resources associated with the Batch service.</span></span> <span data-ttu-id="d4dab-105">Muitos desses limites são cotas padrão aplicadas pelo Azure no nível da assinatura ou da conta.</span><span class="sxs-lookup"><span data-stu-id="d4dab-105">Many of these limits are default quotas applied by Azure at the subscription or account level.</span></span> <span data-ttu-id="d4dab-106">Este artigo discute esses padrões e como você pode solicitar aumentos de cotas.</span><span class="sxs-lookup"><span data-stu-id="d4dab-106">This article discusses those defaults, and how you can request quota increases.</span></span>

<span data-ttu-id="d4dab-107">Lembre-se dessas cotas quando estiver projetando e dimensionando suas cargas de trabalho do Lote.</span><span class="sxs-lookup"><span data-stu-id="d4dab-107">Keep these quotas in mind as you are designing and scaling up your Batch workloads.</span></span> <span data-ttu-id="d4dab-108">Por exemplo, se o pool não alcançar o número de destino de nós de computação que você especificou, você talvez atingiu o limite de cota de núcleos para sua conta de lote ou uma cota de núcleos de VMs regional para sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="d4dab-108">For example, if your pool isn't reaching the target number of compute nodes you've specified, you might have reached the core quota limit for your Batch account, or a regional VM cores quota for your subscription.</span></span>

<span data-ttu-id="d4dab-109">Você pode executar várias cargas de trabalho do Lote em uma única conta do Lote ou distribuir suas cargas de trabalho entre contas do Lote que estão na mesma assinatura mas em diferentes regiões do Azure.</span><span class="sxs-lookup"><span data-stu-id="d4dab-109">You can run multiple Batch workloads in a single Batch account, or distribute your workloads among Batch accounts that are in the same subscription, but in different Azure regions.</span></span>

<span data-ttu-id="d4dab-110">Se você planeja executar cargas de trabalho de produção em Lote, talvez seja necessário aumentar uma ou mais cotas para acima do padrão.</span><span class="sxs-lookup"><span data-stu-id="d4dab-110">If you plan to run production workloads in Batch, you may need to increase one or more of the quotas above the default.</span></span> <span data-ttu-id="d4dab-111">Se desejar aumentar a cota, você poderá abrir uma [solicitação de atendimento ao cliente](#increase-a-quota) online gratuitamente.</span><span class="sxs-lookup"><span data-stu-id="d4dab-111">If you want to raise a quota, you can open an online [customer support request](#increase-a-quota) at no charge.</span></span>

> [!NOTE]
> <span data-ttu-id="d4dab-112">Uma cota é um limite de crédito, não uma garantia de capacidade.</span><span class="sxs-lookup"><span data-stu-id="d4dab-112">A quota is a credit limit, not a capacity guarantee.</span></span> <span data-ttu-id="d4dab-113">Se você precisar de capacidade em larga escala, entre em contato com o suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="d4dab-113">If you have large-scale capacity needs, please contact Azure support.</span></span>
> 
> 

## <a name="resource-quotas"></a><span data-ttu-id="d4dab-114">Cotas de recursos</span><span class="sxs-lookup"><span data-stu-id="d4dab-114">Resource quotas</span></span>
[!INCLUDE [azure-batch-limits](../../includes/azure-batch-limits.md)]

## <a name="quotas-in-user-subscription-mode"></a><span data-ttu-id="d4dab-115">Cotas no modo de assinatura de usuário</span><span class="sxs-lookup"><span data-stu-id="d4dab-115">Quotas in user subscription mode</span></span>

<span data-ttu-id="d4dab-116">Para uma conta de lote com modo de alocação do pool definido como **assinatura de usuário**, lote VMs e outros recursos, como contas de armazenamento, são criados diretamente na sua assinatura quando um pool é criado.</span><span class="sxs-lookup"><span data-stu-id="d4dab-116">For a Batch account with pool allocation mode set to **user subscription**, Batch VMs and other resources, such as storage accounts, are created directly in your subscription when a pool is created.</span></span> <span data-ttu-id="d4dab-117">A cota de núcleos de lote do Azure não se aplica a uma conta criada nesse modo.</span><span class="sxs-lookup"><span data-stu-id="d4dab-117">The Azure Batch cores quota does not apply to an account created in this mode.</span></span> <span data-ttu-id="d4dab-118">Em vez disso, as cotas em sua assinatura para regionais núcleos de computação e outros recursos são aplicados.</span><span class="sxs-lookup"><span data-stu-id="d4dab-118">Instead, the quotas in your subscription for regional compute cores and other resources are applied.</span></span> <span data-ttu-id="d4dab-119">Saiba mais sobre a [assinatura do Azure e limites de serviços, cotas e restrições](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="d4dab-119">Learn more about these quotas in [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="d4dab-120">Ao planejar o uso de recursos para uma conta criada no modo de usuário de assinatura, observe que os seguintes recursos de lote (além de núcleos de computação) são necessários para cada 40 VMs do Linux ou 20 VMs do Windows:</span><span class="sxs-lookup"><span data-stu-id="d4dab-120">When planning resource usage for an account created in user subscription mode, note the following Batch resources (in addition to compute cores) are required for every 40 Linux VMs, or 20 Windows VMs:</span></span>

| <span data-ttu-id="d4dab-121">Recurso</span><span class="sxs-lookup"><span data-stu-id="d4dab-121">Resource</span></span> | <span data-ttu-id="d4dab-122">Cota</span><span class="sxs-lookup"><span data-stu-id="d4dab-122">Quota</span></span> | <span data-ttu-id="d4dab-123">Provedor</span><span class="sxs-lookup"><span data-stu-id="d4dab-123">Provider</span></span> |
| --- | ---| --- |
| <span data-ttu-id="d4dab-124">Uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="d4dab-124">One storage account</span></span> | <span data-ttu-id="d4dab-125">Contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="d4dab-125">Storage Accounts</span></span> | <span data-ttu-id="d4dab-126">Microsoft.Storage</span><span class="sxs-lookup"><span data-stu-id="d4dab-126">Microsoft.Storage</span></span> |
| <span data-ttu-id="d4dab-127">Um endereço IP público</span><span class="sxs-lookup"><span data-stu-id="d4dab-127">One public IP address</span></span> | <span data-ttu-id="d4dab-128">Endereços IP públicos</span><span class="sxs-lookup"><span data-stu-id="d4dab-128">Public IP Addresses</span></span> | <span data-ttu-id="d4dab-129">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="d4dab-129">Microsoft.Network</span></span> | 
| <span data-ttu-id="d4dab-130">Uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="d4dab-130">One virtual network</span></span> | <span data-ttu-id="d4dab-131">Redes Virtuais</span><span class="sxs-lookup"><span data-stu-id="d4dab-131">Virtual Networks</span></span> | <span data-ttu-id="d4dab-132">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="d4dab-132">Microsoft.Network</span></span> | 
| <span data-ttu-id="d4dab-133">Um grupo de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="d4dab-133">One network security group</span></span> | <span data-ttu-id="d4dab-134">Grupos de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="d4dab-134">Network Security Groups</span></span> | <span data-ttu-id="d4dab-135">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="d4dab-135">Microsoft.Network</span></span> | 
| <span data-ttu-id="d4dab-136">Conjunto de escala de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="d4dab-136">One virtual machine scale set</span></span> | <span data-ttu-id="d4dab-137">Conjuntos de Escala de Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="d4dab-137">Virtual Machine Scale Sets</span></span> | <span data-ttu-id="d4dab-138">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="d4dab-138">Microsoft.Compute</span></span> | 
| <span data-ttu-id="d4dab-139">Um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="d4dab-139">One load balancer</span></span> | <span data-ttu-id="d4dab-140">Balanceadores de Carga</span><span class="sxs-lookup"><span data-stu-id="d4dab-140">Load Balancers</span></span> | <span data-ttu-id="d4dab-141">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="d4dab-141">Microsoft.Network</span></span> | 

<span data-ttu-id="d4dab-142">A cota de núcleos em nível regional ou por família VM deve ser definida de acordo com o tamanho da VM necessário para o pool do lote ou pools:</span><span class="sxs-lookup"><span data-stu-id="d4dab-142">The cores quota at a regional level or per VM family should be set according to the VM size required for your Batch pool or pools:</span></span>

| <span data-ttu-id="d4dab-143">Cota</span><span class="sxs-lookup"><span data-stu-id="d4dab-143">Quota</span></span> | <span data-ttu-id="d4dab-144">Provedor</span><span class="sxs-lookup"><span data-stu-id="d4dab-144">Provider</span></span> |
| --- | ---- |
| <span data-ttu-id="d4dab-145">Total de núcleos regionais</span><span class="sxs-lookup"><span data-stu-id="d4dab-145">Total Regional Cores</span></span> | <span data-ttu-id="d4dab-146">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="d4dab-146">Microsoft.Compute</span></span> |
| <span data-ttu-id="d4dab-147">…</span><span class="sxs-lookup"><span data-stu-id="d4dab-147">…</span></span> <span data-ttu-id="d4dab-148">Núcleos de família</span><span class="sxs-lookup"><span data-stu-id="d4dab-148">Family Cores</span></span> | <span data-ttu-id="d4dab-149">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="d4dab-149">Microsoft.Compute</span></span> |



## <a name="other-limits"></a><span data-ttu-id="d4dab-150">Outros limites</span><span class="sxs-lookup"><span data-stu-id="d4dab-150">Other limits</span></span>
| <span data-ttu-id="d4dab-151">**Recurso**</span><span class="sxs-lookup"><span data-stu-id="d4dab-151">**Resource**</span></span> | <span data-ttu-id="d4dab-152">**Limite máximo**</span><span class="sxs-lookup"><span data-stu-id="d4dab-152">**Maximum Limit**</span></span> |
| --- | --- |
| <span data-ttu-id="d4dab-153">[Tarefas simultâneas](batch-parallel-node-tasks.md) por nó de computação</span><span class="sxs-lookup"><span data-stu-id="d4dab-153">[Concurrent tasks](batch-parallel-node-tasks.md) per compute node</span></span> |<span data-ttu-id="d4dab-154">4 vezes o número de núcleos de nó</span><span class="sxs-lookup"><span data-stu-id="d4dab-154">4 x number of node cores</span></span> |
| <span data-ttu-id="d4dab-155">[Aplicativos](batch-application-packages.md) por conta do Lote</span><span class="sxs-lookup"><span data-stu-id="d4dab-155">[Applications](batch-application-packages.md) per Batch account</span></span> |<span data-ttu-id="d4dab-156">20</span><span class="sxs-lookup"><span data-stu-id="d4dab-156">20</span></span> |
| <span data-ttu-id="d4dab-157">Pacotes de aplicativos por aplicativo</span><span class="sxs-lookup"><span data-stu-id="d4dab-157">Application packages per application</span></span> |<span data-ttu-id="d4dab-158">40</span><span class="sxs-lookup"><span data-stu-id="d4dab-158">40</span></span> |
| <span data-ttu-id="d4dab-159">Tamanho do pacote de aplicativos (cada)</span><span class="sxs-lookup"><span data-stu-id="d4dab-159">Application package size (each)</span></span> |<span data-ttu-id="d4dab-160">Aproximadamente 195 GB<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="d4dab-160">Approx. 195GB<sup>1</sup></span></span> |
| <span data-ttu-id="d4dab-161">Tamanho de tarefa inicial máximo</span><span class="sxs-lookup"><span data-stu-id="d4dab-161">Maximum start task size</span></span> | <span data-ttu-id="d4dab-162">32768 caracteres<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="d4dab-162">32768 characters<sup>2</sup></span></span> |

<span data-ttu-id="d4dab-163"><sup>1</sup> O limite do Armazenamento do Azure para o tamanho máximo do blob de blocos</span><span class="sxs-lookup"><span data-stu-id="d4dab-163"><sup>1</sup> Azure Storage limit for maximum block blob size</span></span><br /><span data-ttu-id="d4dab-164">
<sup>2</sup> Inclui arquivos de recurso e variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="d4dab-164">
<sup>2</sup> Includes resource files and environment variables</span></span>

## <a name="view-batch-quotas"></a><span data-ttu-id="d4dab-165">Exibir cotas do Lote</span><span class="sxs-lookup"><span data-stu-id="d4dab-165">View Batch quotas</span></span>
<span data-ttu-id="d4dab-166">Exibir suas cotas de conta do Lote no [portal do Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="d4dab-166">View your Batch account quotas in the [Azure portal][portal].</span></span>

1. <span data-ttu-id="d4dab-167">Selecione **Contas do Lote** no portal e selecione a conta do Lote na qual você está interessado.</span><span class="sxs-lookup"><span data-stu-id="d4dab-167">Select **Batch accounts** in the portal, then select the Batch account you're interested in.</span></span>
2. <span data-ttu-id="d4dab-168">Selecione **Propriedades** na folha de menu da conta de Lote.</span><span class="sxs-lookup"><span data-stu-id="d4dab-168">Select **Properties** on the Batch account's menu blade.</span></span>
3. <span data-ttu-id="d4dab-169">A folha Propriedades exibe as **cotas** atualmente aplicadas à conta do Lote</span><span class="sxs-lookup"><span data-stu-id="d4dab-169">The Properties blade displays the **quotas** currently applied to the Batch account</span></span>
   
    ![Cotas para conta do Lote][account_quotas]

<span data-ttu-id="d4dab-171">Para uma conta de lote criada no modo de usuário de assinatura, exiba as cotas de assinatura relacionadas no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d4dab-171">For a Batch account created in user subscription mode, view the related subscription quotas in the Azure Portal.</span></span>

1. <span data-ttu-id="d4dab-172">Selecione **Assinaturas**e selecione a assinatura que você está usando para a conta do lote.</span><span class="sxs-lookup"><span data-stu-id="d4dab-172">Select **Subscriptions**, and select the subscription you are using for the Batch account.</span></span>

2. <span data-ttu-id="d4dab-173">Na folha **Assinatura**, selecione **Uso + cotas**.</span><span class="sxs-lookup"><span data-stu-id="d4dab-173">On the **Subscription** blade, select **Usage + quotas**.</span></span>



## <a name="increase-a-quota"></a><span data-ttu-id="d4dab-174">Aumentar uma cota</span><span class="sxs-lookup"><span data-stu-id="d4dab-174">Increase a quota</span></span>
<span data-ttu-id="d4dab-175">Siga estas etapas para solicitar uma cota aumentam para sua conta de lote ou sua assinatura usando o [portal do Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="d4dab-175">Follow these steps to request a quota increase for your Batch account or your subscription using the [Azure portal][portal].</span></span> <span data-ttu-id="d4dab-176">O tipo de aumento de cota depende do modo de alocação de pool de sua conta do lote.</span><span class="sxs-lookup"><span data-stu-id="d4dab-176">The type of quota increase depends on the pool allocation mode of your Batch account.</span></span>

### <a name="increase-a-batch-cores-quota"></a><span data-ttu-id="d4dab-177">Aumentar a cota de núcleos de lote</span><span class="sxs-lookup"><span data-stu-id="d4dab-177">Increase a Batch cores quota</span></span> 

<span data-ttu-id="d4dab-178">Se sua conta do lote foi criada em modo de **serviço de lote**, siga estas etapas para solicitar uma cota de núcleos de lote aumentam:</span><span class="sxs-lookup"><span data-stu-id="d4dab-178">If your Batch account was created in **Batch service** mode, follow these steps to request a Batch cores quota increase:</span></span>

1. <span data-ttu-id="d4dab-179">Selecione o bloco **Ajuda + suporte** no painel do portal ou o ponto de interrogação (**?**) no canto superior direito do portal.</span><span class="sxs-lookup"><span data-stu-id="d4dab-179">Select the **Help + support** tile on your portal dashboard, or the question mark (**?**) in the upper-right corner of the portal.</span></span>
2. <span data-ttu-id="d4dab-180">Selecione **Nova solicitação de suporte** > **Fundamentos**.</span><span class="sxs-lookup"><span data-stu-id="d4dab-180">Select **New support request** > **Basics**.</span></span>
3. <span data-ttu-id="d4dab-181">Na folha **Fundamentos** :</span><span class="sxs-lookup"><span data-stu-id="d4dab-181">On the **Basics** blade:</span></span>
   
    <span data-ttu-id="d4dab-182">a.</span><span class="sxs-lookup"><span data-stu-id="d4dab-182">a.</span></span> <span data-ttu-id="d4dab-183">**Tipo de Problema** > **Cota**</span><span class="sxs-lookup"><span data-stu-id="d4dab-183">**Issue Type** > **Quota**</span></span>
   
    <span data-ttu-id="d4dab-184">b.</span><span class="sxs-lookup"><span data-stu-id="d4dab-184">b.</span></span> <span data-ttu-id="d4dab-185">Selecione sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="d4dab-185">Select your subscription.</span></span>
   
    <span data-ttu-id="d4dab-186">c.</span><span class="sxs-lookup"><span data-stu-id="d4dab-186">c.</span></span> <span data-ttu-id="d4dab-187">**Tipo de cota** > **Lote**</span><span class="sxs-lookup"><span data-stu-id="d4dab-187">**Quota type** > **Batch**</span></span>
   
    <span data-ttu-id="d4dab-188">d.</span><span class="sxs-lookup"><span data-stu-id="d4dab-188">d.</span></span> <span data-ttu-id="d4dab-189">**Plano de suporte** > **Suporte da cota - Incluído**</span><span class="sxs-lookup"><span data-stu-id="d4dab-189">**Support plan** > **Quota support - Included**</span></span>
   
    <span data-ttu-id="d4dab-190">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="d4dab-190">Click **Next**.</span></span>
4. <span data-ttu-id="d4dab-191">Na folha **Problema** :</span><span class="sxs-lookup"><span data-stu-id="d4dab-191">On the **Problem** blade:</span></span>
   
    <span data-ttu-id="d4dab-192">a.</span><span class="sxs-lookup"><span data-stu-id="d4dab-192">a.</span></span> <span data-ttu-id="d4dab-193">Selecione uma **Gravidade** de acordo com o [impacto nos negócios][support_sev].</span><span class="sxs-lookup"><span data-stu-id="d4dab-193">Select a **Severity** according to your [business impact][support_sev].</span></span>
   
    <span data-ttu-id="d4dab-194">b.</span><span class="sxs-lookup"><span data-stu-id="d4dab-194">b.</span></span> <span data-ttu-id="d4dab-195">Em **Detalhes**, especifique cada cota que você deseja alterar, o nome da conta do Lote e o novo limite.</span><span class="sxs-lookup"><span data-stu-id="d4dab-195">In **Details**, specify each quota you want to change, the Batch account name, and the new limit.</span></span>
   
    <span data-ttu-id="d4dab-196">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="d4dab-196">Click **Next**.</span></span>
5. <span data-ttu-id="d4dab-197">Na folha **Informações de contato** :</span><span class="sxs-lookup"><span data-stu-id="d4dab-197">On the **Contact information** blade:</span></span>
   
    <span data-ttu-id="d4dab-198">a.</span><span class="sxs-lookup"><span data-stu-id="d4dab-198">a.</span></span> <span data-ttu-id="d4dab-199">Selecione um **método de contato preferencial**.</span><span class="sxs-lookup"><span data-stu-id="d4dab-199">Select a **Preferred contact method**.</span></span>
   
    <span data-ttu-id="d4dab-200">b.</span><span class="sxs-lookup"><span data-stu-id="d4dab-200">b.</span></span> <span data-ttu-id="d4dab-201">Verifique e insira os detalhes de contato necessários.</span><span class="sxs-lookup"><span data-stu-id="d4dab-201">Verify and enter the required contact details.</span></span>
   
    <span data-ttu-id="d4dab-202">Clique em **Criar** para enviar a solicitação de suporte.</span><span class="sxs-lookup"><span data-stu-id="d4dab-202">Click **Create** to submit the support request.</span></span>

<span data-ttu-id="d4dab-203">Depois que a solicitação de suporte foi enviada, o suporte do Azure entrará em contato com você.</span><span class="sxs-lookup"><span data-stu-id="d4dab-203">Once you've submitted your support request, Azure support will contact you.</span></span> <span data-ttu-id="d4dab-204">Observe que a conclusão do pedido pode levar até dois dias úteis.</span><span class="sxs-lookup"><span data-stu-id="d4dab-204">Note that completing the request can take up to 2 business days.</span></span>

### <a name="increase-a-subscription-cores-quota"></a><span data-ttu-id="d4dab-205">Aumentar a cota de núcleos de assinatura</span><span class="sxs-lookup"><span data-stu-id="d4dab-205">Increase a subscription cores quota</span></span>

<span data-ttu-id="d4dab-206">Se sua conta do Lote foi criada no modo **assinatura do usuário** e você precisa de núcleos regionais adicionais ou de família VM, solicite um aumento de cota em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="d4dab-206">If your Batch account was created in **user subscription** mode and you need additional regional or VM family cores, request a quota increase in your subscription.</span></span> <span data-ttu-id="d4dab-207">Para as etapas, consulte [Solicitações de aumento da cota de núcleo do Gerenciador de recursos](../azure-supportability/resource-manager-core-quotas-request.md).</span><span class="sxs-lookup"><span data-stu-id="d4dab-207">For steps, see [Resource Manager core quota increase requests](../azure-supportability/resource-manager-core-quotas-request.md).</span></span>



## <a name="related-topics"></a><span data-ttu-id="d4dab-208">Tópicos relacionados</span><span class="sxs-lookup"><span data-stu-id="d4dab-208">Related topics</span></span>
* [<span data-ttu-id="d4dab-209">Criar uma conta do Lote do Azure usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d4dab-209">Create an Azure Batch account using the Azure portal</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="d4dab-210">Visão geral dos recursos do Lote do Azure</span><span class="sxs-lookup"><span data-stu-id="d4dab-210">Azure Batch feature overview</span></span>](batch-api-basics.md)
* [<span data-ttu-id="d4dab-211">Assinatura do Azure e limite de serviços, cotas e restrições</span><span class="sxs-lookup"><span data-stu-id="d4dab-211">Azure subscription and service limits, quotas, and constraints</span></span>](../azure-subscription-service-limits.md)

[portal]: https://portal.azure.com
[portal_classic_increase]: https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/
[support_sev]: http://aka.ms/supportseverity

[account_quotas]: ./media/batch-quota-limit/accountquota_portal.PNG
