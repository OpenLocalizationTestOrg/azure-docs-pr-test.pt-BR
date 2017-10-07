---
title: aaaService cotas e limites de lote do Azure | Microsoft Docs
description: "Saiba mais sobre cotas do lote do Azure padrão, limites e restrições e como toorequest cota aumenta"
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
ms.openlocfilehash: 6035d1c7618cfe97ebca3780e02a4ee34f54e534
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="batch-service-quotas-and-limits"></a><span data-ttu-id="ee8c4-103">Cotas e limites de serviço do Lote</span><span class="sxs-lookup"><span data-stu-id="ee8c4-103">Batch service quotas and limits</span></span>

<span data-ttu-id="ee8c4-104">Como com outros serviços do Azure, há limites no determinados recursos associados à saudação serviço de lote.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-104">As with other Azure services, there are limits on certain resources associated with hello Batch service.</span></span> <span data-ttu-id="ee8c4-105">Muitos desses limites são cotas padrão aplicadas pelo Azure no nível de conta ou assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-105">Many of these limits are default quotas applied by Azure at hello subscription or account level.</span></span> <span data-ttu-id="ee8c4-106">Este artigo discute esses padrões e como você pode solicitar aumentos de cotas.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-106">This article discusses those defaults, and how you can request quota increases.</span></span>

<span data-ttu-id="ee8c4-107">Lembre-se dessas cotas quando estiver projetando e dimensionando suas cargas de trabalho do Lote.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-107">Keep these quotas in mind as you are designing and scaling up your Batch workloads.</span></span> <span data-ttu-id="ee8c4-108">Por exemplo, se o pool não alcançar o número de destino de Olá de nós de computação que você especificou, você pode atingiu limite de cota de núcleos Olá para a conta de lote ou uma cota de núcleos VM regional para sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-108">For example, if your pool isn't reaching hello target number of compute nodes you've specified, you might have reached hello core quota limit for your Batch account, or a regional VM cores quota for your subscription.</span></span>

<span data-ttu-id="ee8c4-109">Você pode executar várias cargas de trabalho em lotes em uma única conta de lote ou distribuir suas cargas de trabalho entre contas em lotes que estão em Olá mesma assinatura, mas em diferentes regiões do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-109">You can run multiple Batch workloads in a single Batch account, or distribute your workloads among Batch accounts that are in hello same subscription, but in different Azure regions.</span></span>

<span data-ttu-id="ee8c4-110">Se você planejar toorun cargas de trabalho de produção em lote, talvez seja necessário tooincrease uma ou mais das cotas Olá acima padrão hello.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-110">If you plan toorun production workloads in Batch, you may need tooincrease one or more of hello quotas above hello default.</span></span> <span data-ttu-id="ee8c4-111">Se você quiser tooraise uma cota, você pode abrir um online [solicitação de suporte do cliente](#increase-a-quota) sem custo adicional.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-111">If you want tooraise a quota, you can open an online [customer support request](#increase-a-quota) at no charge.</span></span>

> [!NOTE]
> <span data-ttu-id="ee8c4-112">Uma cota é um limite de crédito, não uma garantia de capacidade.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-112">A quota is a credit limit, not a capacity guarantee.</span></span> <span data-ttu-id="ee8c4-113">Se você precisar de capacidade em larga escala, entre em contato com o suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-113">If you have large-scale capacity needs, please contact Azure support.</span></span>
> 
> 

## <a name="resource-quotas"></a><span data-ttu-id="ee8c4-114">Cotas de recursos</span><span class="sxs-lookup"><span data-stu-id="ee8c4-114">Resource quotas</span></span>
[!INCLUDE [azure-batch-limits](../../includes/azure-batch-limits.md)]

## <a name="quotas-in-user-subscription-mode"></a><span data-ttu-id="ee8c4-115">Cotas no modo de assinatura de usuário</span><span class="sxs-lookup"><span data-stu-id="ee8c4-115">Quotas in user subscription mode</span></span>

<span data-ttu-id="ee8c4-116">Para uma conta de lote com o modo de alocação de pool definido muito**assinatura de usuário**, máquinas virtuais e outros recursos, como contas de armazenamento do lote, são criados diretamente em sua assinatura, quando um pool é criado.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-116">For a Batch account with pool allocation mode set too**user subscription**, Batch VMs and other resources, such as storage accounts, are created directly in your subscription when a pool is created.</span></span> <span data-ttu-id="ee8c4-117">cota de núcleos de lote do Azure Olá não se aplica a conta tooan criada nesse modo.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-117">hello Azure Batch cores quota does not apply tooan account created in this mode.</span></span> <span data-ttu-id="ee8c4-118">Em vez disso, são aplicadas as cotas de saudação em sua assinatura de núcleos de computação regional e outros recursos.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-118">Instead, hello quotas in your subscription for regional compute cores and other resources are applied.</span></span> <span data-ttu-id="ee8c4-119">Saiba mais sobre a [assinatura do Azure e limites de serviços, cotas e restrições](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="ee8c4-119">Learn more about these quotas in [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="ee8c4-120">Ao planejar o uso de recursos para uma conta criada no modo de usuário de assinatura, Olá Observação recursos de lote (em núcleos de toocompute adição) a seguir são necessários para cada 40 VMs do Linux, ou 20 VMs do Windows:</span><span class="sxs-lookup"><span data-stu-id="ee8c4-120">When planning resource usage for an account created in user subscription mode, note hello following Batch resources (in addition toocompute cores) are required for every 40 Linux VMs, or 20 Windows VMs:</span></span>

| <span data-ttu-id="ee8c4-121">Recurso</span><span class="sxs-lookup"><span data-stu-id="ee8c4-121">Resource</span></span> | <span data-ttu-id="ee8c4-122">Cota</span><span class="sxs-lookup"><span data-stu-id="ee8c4-122">Quota</span></span> | <span data-ttu-id="ee8c4-123">Provedor</span><span class="sxs-lookup"><span data-stu-id="ee8c4-123">Provider</span></span> |
| --- | ---| --- |
| <span data-ttu-id="ee8c4-124">Uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="ee8c4-124">One storage account</span></span> | <span data-ttu-id="ee8c4-125">Contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="ee8c4-125">Storage Accounts</span></span> | <span data-ttu-id="ee8c4-126">Microsoft.Storage</span><span class="sxs-lookup"><span data-stu-id="ee8c4-126">Microsoft.Storage</span></span> |
| <span data-ttu-id="ee8c4-127">Um endereço IP público</span><span class="sxs-lookup"><span data-stu-id="ee8c4-127">One public IP address</span></span> | <span data-ttu-id="ee8c4-128">Endereços IP públicos</span><span class="sxs-lookup"><span data-stu-id="ee8c4-128">Public IP Addresses</span></span> | <span data-ttu-id="ee8c4-129">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="ee8c4-129">Microsoft.Network</span></span> | 
| <span data-ttu-id="ee8c4-130">Uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="ee8c4-130">One virtual network</span></span> | <span data-ttu-id="ee8c4-131">Redes Virtuais</span><span class="sxs-lookup"><span data-stu-id="ee8c4-131">Virtual Networks</span></span> | <span data-ttu-id="ee8c4-132">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="ee8c4-132">Microsoft.Network</span></span> | 
| <span data-ttu-id="ee8c4-133">Um grupo de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="ee8c4-133">One network security group</span></span> | <span data-ttu-id="ee8c4-134">Grupos de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="ee8c4-134">Network Security Groups</span></span> | <span data-ttu-id="ee8c4-135">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="ee8c4-135">Microsoft.Network</span></span> | 
| <span data-ttu-id="ee8c4-136">Conjunto de escala de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="ee8c4-136">One virtual machine scale set</span></span> | <span data-ttu-id="ee8c4-137">Conjuntos de Escala de Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="ee8c4-137">Virtual Machine Scale Sets</span></span> | <span data-ttu-id="ee8c4-138">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="ee8c4-138">Microsoft.Compute</span></span> | 
| <span data-ttu-id="ee8c4-139">Um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="ee8c4-139">One load balancer</span></span> | <span data-ttu-id="ee8c4-140">Balanceadores de Carga</span><span class="sxs-lookup"><span data-stu-id="ee8c4-140">Load Balancers</span></span> | <span data-ttu-id="ee8c4-141">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="ee8c4-141">Microsoft.Network</span></span> | 

<span data-ttu-id="ee8c4-142">cota de núcleos de saudação em um nível regional ou por família VM deve ser conjunto acordo toohello VM tamanho necessário para o pool de lote ou pools:</span><span class="sxs-lookup"><span data-stu-id="ee8c4-142">hello cores quota at a regional level or per VM family should be set according toohello VM size required for your Batch pool or pools:</span></span>

| <span data-ttu-id="ee8c4-143">Quota</span><span class="sxs-lookup"><span data-stu-id="ee8c4-143">Quota</span></span> | <span data-ttu-id="ee8c4-144">Provedor</span><span class="sxs-lookup"><span data-stu-id="ee8c4-144">Provider</span></span> |
| --- | ---- |
| <span data-ttu-id="ee8c4-145">Total de núcleos regionais</span><span class="sxs-lookup"><span data-stu-id="ee8c4-145">Total Regional Cores</span></span> | <span data-ttu-id="ee8c4-146">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="ee8c4-146">Microsoft.Compute</span></span> |
| <span data-ttu-id="ee8c4-147">…</span><span class="sxs-lookup"><span data-stu-id="ee8c4-147">…</span></span> <span data-ttu-id="ee8c4-148">Núcleos de família</span><span class="sxs-lookup"><span data-stu-id="ee8c4-148">Family Cores</span></span> | <span data-ttu-id="ee8c4-149">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="ee8c4-149">Microsoft.Compute</span></span> |



## <a name="other-limits"></a><span data-ttu-id="ee8c4-150">Outros limites</span><span class="sxs-lookup"><span data-stu-id="ee8c4-150">Other limits</span></span>
| <span data-ttu-id="ee8c4-151">**Recurso**</span><span class="sxs-lookup"><span data-stu-id="ee8c4-151">**Resource**</span></span> | <span data-ttu-id="ee8c4-152">**Limite máximo**</span><span class="sxs-lookup"><span data-stu-id="ee8c4-152">**Maximum Limit**</span></span> |
| --- | --- |
| <span data-ttu-id="ee8c4-153">[Tarefas simultâneas](batch-parallel-node-tasks.md) por nó de computação</span><span class="sxs-lookup"><span data-stu-id="ee8c4-153">[Concurrent tasks](batch-parallel-node-tasks.md) per compute node</span></span> |<span data-ttu-id="ee8c4-154">4 vezes o número de núcleos de nó</span><span class="sxs-lookup"><span data-stu-id="ee8c4-154">4 x number of node cores</span></span> |
| <span data-ttu-id="ee8c4-155">[Aplicativos](batch-application-packages.md) por conta do Lote</span><span class="sxs-lookup"><span data-stu-id="ee8c4-155">[Applications](batch-application-packages.md) per Batch account</span></span> |<span data-ttu-id="ee8c4-156">20</span><span class="sxs-lookup"><span data-stu-id="ee8c4-156">20</span></span> |
| <span data-ttu-id="ee8c4-157">Pacotes de aplicativos por aplicativo</span><span class="sxs-lookup"><span data-stu-id="ee8c4-157">Application packages per application</span></span> |<span data-ttu-id="ee8c4-158">40</span><span class="sxs-lookup"><span data-stu-id="ee8c4-158">40</span></span> |
| <span data-ttu-id="ee8c4-159">Tamanho do pacote de aplicativos (cada)</span><span class="sxs-lookup"><span data-stu-id="ee8c4-159">Application package size (each)</span></span> |<span data-ttu-id="ee8c4-160">Aproximadamente 195 GB<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="ee8c4-160">Approx. 195GB<sup>1</sup></span></span> |
| <span data-ttu-id="ee8c4-161">Tamanho de tarefa inicial máximo</span><span class="sxs-lookup"><span data-stu-id="ee8c4-161">Maximum start task size</span></span> | <span data-ttu-id="ee8c4-162">32768 caracteres<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="ee8c4-162">32768 characters<sup>2</sup></span></span> |

<span data-ttu-id="ee8c4-163"><sup>1</sup> O limite do Armazenamento do Azure para o tamanho máximo do blob de blocos</span><span class="sxs-lookup"><span data-stu-id="ee8c4-163"><sup>1</sup> Azure Storage limit for maximum block blob size</span></span><br /><span data-ttu-id="ee8c4-164">
<sup>2</sup> Inclui arquivos de recurso e variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="ee8c4-164">
<sup>2</sup> Includes resource files and environment variables</span></span>

## <a name="view-batch-quotas"></a><span data-ttu-id="ee8c4-165">Exibir cotas do Lote</span><span class="sxs-lookup"><span data-stu-id="ee8c4-165">View Batch quotas</span></span>
<span data-ttu-id="ee8c4-166">Exibir suas cotas de conta de lote no hello [portal do Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="ee8c4-166">View your Batch account quotas in hello [Azure portal][portal].</span></span>

1. <span data-ttu-id="ee8c4-167">Selecione **contas de lote** no portal de Olá, selecione conta de lote Olá você está interessado.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-167">Select **Batch accounts** in hello portal, then select hello Batch account you're interested in.</span></span>
2. <span data-ttu-id="ee8c4-168">Selecione **propriedades** na folha de menu da conta do lote de saudação.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-168">Select **Properties** on hello Batch account's menu blade.</span></span>
3. <span data-ttu-id="ee8c4-169">folha de propriedades de saudação exibe Olá **cotas** aplicadas toohello conta do lote</span><span class="sxs-lookup"><span data-stu-id="ee8c4-169">hello Properties blade displays hello **quotas** currently applied toohello Batch account</span></span>
   
    ![Cotas para conta do Lote][account_quotas]

<span data-ttu-id="ee8c4-171">Para uma conta de lote criada no modo de usuário de assinatura, Olá de exibição relacionados cotas de assinatura no hello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-171">For a Batch account created in user subscription mode, view hello related subscription quotas in hello Azure Portal.</span></span>

1. <span data-ttu-id="ee8c4-172">Selecione **assinaturas**e selecione a assinatura Olá que você está usando para Olá conta do lote.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-172">Select **Subscriptions**, and select hello subscription you are using for hello Batch account.</span></span>

2. <span data-ttu-id="ee8c4-173">Em Olá **assinatura** folha, selecione **uso + cotas**.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-173">On hello **Subscription** blade, select **Usage + quotas**.</span></span>



## <a name="increase-a-quota"></a><span data-ttu-id="ee8c4-174">Aumentar uma cota</span><span class="sxs-lookup"><span data-stu-id="ee8c4-174">Increase a quota</span></span>
<span data-ttu-id="ee8c4-175">Siga essas toorequest etapas aumentar uma cota para a conta de lote ou sua assinatura usando Olá [portal do Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="ee8c4-175">Follow these steps toorequest a quota increase for your Batch account or your subscription using hello [Azure portal][portal].</span></span> <span data-ttu-id="ee8c4-176">tipo de saudação do aumento da cota depende do modo de alocação de pool de saudação da sua conta do lote.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-176">hello type of quota increase depends on hello pool allocation mode of your Batch account.</span></span>

### <a name="increase-a-batch-cores-quota"></a><span data-ttu-id="ee8c4-177">Aumentar a cota de núcleos de lote</span><span class="sxs-lookup"><span data-stu-id="ee8c4-177">Increase a Batch cores quota</span></span> 

<span data-ttu-id="ee8c4-178">Se sua conta em lotes foi criada no **serviço de lote** modo, siga essas etapas toorequest um aumento de cota de núcleos de lote:</span><span class="sxs-lookup"><span data-stu-id="ee8c4-178">If your Batch account was created in **Batch service** mode, follow these steps toorequest a Batch cores quota increase:</span></span>

1. <span data-ttu-id="ee8c4-179">Selecione Olá **ajuda + suporte** lado a lado em seu painel do portal ou Olá ponto de interrogação (**?**) no canto superior direito de saudação do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-179">Select hello **Help + support** tile on your portal dashboard, or hello question mark (**?**) in hello upper-right corner of hello portal.</span></span>
2. <span data-ttu-id="ee8c4-180">Selecione **Nova solicitação de suporte** > **Fundamentos**.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-180">Select **New support request** > **Basics**.</span></span>
3. <span data-ttu-id="ee8c4-181">Em Olá **Noções básicas sobre** folha:</span><span class="sxs-lookup"><span data-stu-id="ee8c4-181">On hello **Basics** blade:</span></span>
   
    <span data-ttu-id="ee8c4-182">a.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-182">a.</span></span> <span data-ttu-id="ee8c4-183">**Tipo de Problema** > **Cota**</span><span class="sxs-lookup"><span data-stu-id="ee8c4-183">**Issue Type** > **Quota**</span></span>
   
    <span data-ttu-id="ee8c4-184">b.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-184">b.</span></span> <span data-ttu-id="ee8c4-185">Selecione sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-185">Select your subscription.</span></span>
   
    <span data-ttu-id="ee8c4-186">c.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-186">c.</span></span> <span data-ttu-id="ee8c4-187">**Tipo de cota** > **Lote**</span><span class="sxs-lookup"><span data-stu-id="ee8c4-187">**Quota type** > **Batch**</span></span>
   
    <span data-ttu-id="ee8c4-188">d.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-188">d.</span></span> <span data-ttu-id="ee8c4-189">**Plano de suporte** > **Suporte da cota - Incluído**</span><span class="sxs-lookup"><span data-stu-id="ee8c4-189">**Support plan** > **Quota support - Included**</span></span>
   
    <span data-ttu-id="ee8c4-190">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-190">Click **Next**.</span></span>
4. <span data-ttu-id="ee8c4-191">Em Olá **problema** folha:</span><span class="sxs-lookup"><span data-stu-id="ee8c4-191">On hello **Problem** blade:</span></span>
   
    <span data-ttu-id="ee8c4-192">a.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-192">a.</span></span> <span data-ttu-id="ee8c4-193">Selecione um **severidade** tooyour de acordo com [impacto nos negócios][support_sev].</span><span class="sxs-lookup"><span data-stu-id="ee8c4-193">Select a **Severity** according tooyour [business impact][support_sev].</span></span>
   
    <span data-ttu-id="ee8c4-194">b.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-194">b.</span></span> <span data-ttu-id="ee8c4-195">Em **detalhes**, especifique cada cota que você deseja toochange, nome da conta em lotes hello e novo limite de saudação.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-195">In **Details**, specify each quota you want toochange, hello Batch account name, and hello new limit.</span></span>
   
    <span data-ttu-id="ee8c4-196">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-196">Click **Next**.</span></span>
5. <span data-ttu-id="ee8c4-197">Em Olá **informações de contato** folha:</span><span class="sxs-lookup"><span data-stu-id="ee8c4-197">On hello **Contact information** blade:</span></span>
   
    <span data-ttu-id="ee8c4-198">a.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-198">a.</span></span> <span data-ttu-id="ee8c4-199">Selecione um **método de contato preferencial**.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-199">Select a **Preferred contact method**.</span></span>
   
    <span data-ttu-id="ee8c4-200">b.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-200">b.</span></span> <span data-ttu-id="ee8c4-201">Verifique e insira os detalhes de contato Olá necessário.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-201">Verify and enter hello required contact details.</span></span>
   
    <span data-ttu-id="ee8c4-202">Clique em **criar** toosubmit Olá o suporte da solicitação.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-202">Click **Create** toosubmit hello support request.</span></span>

<span data-ttu-id="ee8c4-203">Depois que a solicitação de suporte foi enviada, o suporte do Azure entrará em contato com você.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-203">Once you've submitted your support request, Azure support will contact you.</span></span> <span data-ttu-id="ee8c4-204">Observe que concluir solicitação Olá poderá levar até too2 dias.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-204">Note that completing hello request can take up too2 business days.</span></span>

### <a name="increase-a-subscription-cores-quota"></a><span data-ttu-id="ee8c4-205">Aumentar a cota de núcleos de assinatura</span><span class="sxs-lookup"><span data-stu-id="ee8c4-205">Increase a subscription cores quota</span></span>

<span data-ttu-id="ee8c4-206">Se sua conta do Lote foi criada no modo **assinatura do usuário** e você precisa de núcleos regionais adicionais ou de família VM, solicite um aumento de cota em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="ee8c4-206">If your Batch account was created in **user subscription** mode and you need additional regional or VM family cores, request a quota increase in your subscription.</span></span> <span data-ttu-id="ee8c4-207">Para as etapas, consulte [Solicitações de aumento da cota de núcleo do Gerenciador de recursos](../azure-supportability/resource-manager-core-quotas-request.md).</span><span class="sxs-lookup"><span data-stu-id="ee8c4-207">For steps, see [Resource Manager core quota increase requests](../azure-supportability/resource-manager-core-quotas-request.md).</span></span>



## <a name="related-topics"></a><span data-ttu-id="ee8c4-208">Tópicos relacionados</span><span class="sxs-lookup"><span data-stu-id="ee8c4-208">Related topics</span></span>
* [<span data-ttu-id="ee8c4-209">Criar uma conta de lote do Azure usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ee8c4-209">Create an Azure Batch account using hello Azure portal</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="ee8c4-210">Visão geral dos recursos do Lote do Azure</span><span class="sxs-lookup"><span data-stu-id="ee8c4-210">Azure Batch feature overview</span></span>](batch-api-basics.md)
* [<span data-ttu-id="ee8c4-211">Assinatura do Azure e limite de serviços, cotas e restrições</span><span class="sxs-lookup"><span data-stu-id="ee8c4-211">Azure subscription and service limits, quotas, and constraints</span></span>](../azure-subscription-service-limits.md)

[portal]: https://portal.azure.com
[portal_classic_increase]: https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/
[support_sev]: http://aka.ms/supportseverity

[account_quotas]: ./media/batch-quota-limit/accountquota_portal.PNG
