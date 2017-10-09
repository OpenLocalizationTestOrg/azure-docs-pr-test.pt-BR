---
title: "aaaAdd runbooks de automação do Azure toorecovery planos no Azure Site Recovery | Microsoft Docs"
description: "Saiba como o Azure Site Recovery pode ajudar você a estender planos de recuperação usando a Automação do Azure. Saiba como toocomplete complexo tarefas durante a recuperação tooAzure."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: ecece14d-5f92-4596-bbaf-5204addb95c2
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/23/2017
ms.author: ruturajd@microsoft.com
ms.openlocfilehash: 90d517200cec5527e98a0d00da466bace587b70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans"></a><span data-ttu-id="9ca46-104">Adicionar planos de toorecovery de runbooks de automação do Azure</span><span class="sxs-lookup"><span data-stu-id="9ca46-104">Add Azure Automation runbooks toorecovery plans</span></span>
<span data-ttu-id="9ca46-105">Neste artigo, descreveremos como o Azure Site Recovery integra toohelp de automação do Azure estender seus planos de recuperação.</span><span class="sxs-lookup"><span data-stu-id="9ca46-105">In this article, we describe how Azure Site Recovery integrates with Azure Automation toohelp you extend your recovery plans.</span></span> <span data-ttu-id="9ca46-106">Os planos de recuperação podem orquestrar a recuperação de VMs que são protegidas com o Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="9ca46-106">Recovery plans can orchestrate recovery of VMs that are protected with Site Recovery.</span></span> <span data-ttu-id="9ca46-107">Planos de recuperação de trabalho para a nuvem secundária de tooa de replicação e de replicação tooAzure.</span><span class="sxs-lookup"><span data-stu-id="9ca46-107">Recovery plans work both for replication tooa secondary cloud, and for replication tooAzure.</span></span> <span data-ttu-id="9ca46-108">Planos de recuperação também ajudam a tornar a recuperação Olá **precisas**, **repeatable**, e **automatizada**.</span><span class="sxs-lookup"><span data-stu-id="9ca46-108">Recovery plans also help make hello recovery **consistently accurate**, **repeatable**, and **automated**.</span></span> <span data-ttu-id="9ca46-109">Se você fizer failover tooAzure suas VMs, integração com a automação do Azure estende os planos de recuperação.</span><span class="sxs-lookup"><span data-stu-id="9ca46-109">If you fail over your VMs tooAzure, integration with Azure Automation extends your recovery plans.</span></span> <span data-ttu-id="9ca46-110">Você pode usá-lo tooexecute runbooks, que oferecem tarefas de automação avançada.</span><span class="sxs-lookup"><span data-stu-id="9ca46-110">You can use it tooexecute runbooks, which offer powerful automation tasks.</span></span>

<span data-ttu-id="9ca46-111">Se você for novo tooAzure automação, você pode [inscrever](https://azure.microsoft.com/services/automation/) e [Baixe scripts de exemplo](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="9ca46-111">If you are new tooAzure Automation, you can [sign up](https://azure.microsoft.com/services/automation/) and [download sample scripts](https://azure.microsoft.com/documentation/scripts/).</span></span> <span data-ttu-id="9ca46-112">Para obter mais informações e toolearn como tooorchestrate recuperação tooAzure usando [planos de recuperação](https://azure.microsoft.com/blog/?p=166264), consulte [do Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="9ca46-112">For more information, and toolearn how tooorchestrate recovery tooAzure by using [recovery plans](https://azure.microsoft.com/blog/?p=166264), see [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).</span></span>

<span data-ttu-id="9ca46-113">Neste artigo, descrevemos como você pode integrar runbooks da Automação do Azure em planos de recuperação.</span><span class="sxs-lookup"><span data-stu-id="9ca46-113">In this article, we describe how you can integrate Azure Automation runbooks into your recovery plans.</span></span> <span data-ttu-id="9ca46-114">Podemos usar exemplos tooautomate tarefas básicas que previamente necessitaram de intervenção manual.</span><span class="sxs-lookup"><span data-stu-id="9ca46-114">We use examples tooautomate basic tasks that previously required manual intervention.</span></span> <span data-ttu-id="9ca46-115">Podemos também descrevem como tooconvert tooa uma recuperação de várias etapas clicar uma ação de recuperação.</span><span class="sxs-lookup"><span data-stu-id="9ca46-115">We also describe how tooconvert a multi-step recovery tooa single-click recovery action.</span></span>

## <a name="customize-hello-recovery-plan"></a><span data-ttu-id="9ca46-116">Personalizar plano de recuperação de saudação</span><span class="sxs-lookup"><span data-stu-id="9ca46-116">Customize hello recovery plan</span></span>
1. <span data-ttu-id="9ca46-117">Vá toohello **recuperação de Site** folha de recursos do plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="9ca46-117">Go toohello **Site Recovery** recovery plan resource blade.</span></span> <span data-ttu-id="9ca46-118">Neste exemplo, o plano de recuperação de saudação possui tooit adicionado VMs dois, para recuperação.</span><span class="sxs-lookup"><span data-stu-id="9ca46-118">For this example, hello recovery plan has two VMs added tooit, for recovery.</span></span> <span data-ttu-id="9ca46-119">toobegin adicionando um runbook, clique em Olá **personalizar** guia.</span><span class="sxs-lookup"><span data-stu-id="9ca46-119">toobegin adding a runbook, click hello **Customize** tab.</span></span>

    ![Botão de personalizar Olá](media/site-recovery-runbook-automation-new/essentials-rp.png)


2. <span data-ttu-id="9ca46-121">Clique com o botão direito do mouse em **Grupo 1: Iniciar** e, em seguida, selecione **Adicionar pós-ação**.</span><span class="sxs-lookup"><span data-stu-id="9ca46-121">Right-click **Group 1: Start**, and then select **Add post action**.</span></span>

    ![Clicar com o botão direito do mouse em Grupo 1: Iniciar e em Adicionar pós-ação](media/site-recovery-runbook-automation-new/customize-rp.png)

3. <span data-ttu-id="9ca46-123">Clique em **Escolher um script**.</span><span class="sxs-lookup"><span data-stu-id="9ca46-123">Click **Choose a script**.</span></span>

4. <span data-ttu-id="9ca46-124">Em Olá **atualizar ação** folha, script de saudação do nome **Hello World**.</span><span class="sxs-lookup"><span data-stu-id="9ca46-124">On hello **Update action** blade, name hello script **Hello World**.</span></span>

    ![folha de ação de atualização de saudação](media/site-recovery-runbook-automation-new/update-rp.png)

5. <span data-ttu-id="9ca46-126">Insira um nome para a conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="9ca46-126">Enter an Automation account name.</span></span>
    >[!NOTE]
    > <span data-ttu-id="9ca46-127">Olá conta de automação pode estar em qualquer região do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ca46-127">hello Automation account can be in any Azure region.</span></span> <span data-ttu-id="9ca46-128">Olá conta de automação deve estar no hello mesma assinatura que o cofre do Azure Site Recovery hello.</span><span class="sxs-lookup"><span data-stu-id="9ca46-128">hello Automation account must be in hello same subscription as hello Azure Site Recovery vault.</span></span>

6. <span data-ttu-id="9ca46-129">Na conta de Automação, selecione um runbook.</span><span class="sxs-lookup"><span data-stu-id="9ca46-129">In your Automation account, select a runbook.</span></span> <span data-ttu-id="9ca46-130">Este runbook é o script hello executado durante a execução de Olá Olá do plano de recuperação, após a recuperação de saudação do primeiro grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ca46-130">This runbook is hello script that runs during hello execution of hello recovery plan, after hello recovery of hello first group.</span></span>

7. <span data-ttu-id="9ca46-131">script de saudação toosave, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="9ca46-131">toosave hello script, click **OK**.</span></span> <span data-ttu-id="9ca46-132">saudação de script é adicionada muito**grupo 1: pós-etapas**.</span><span class="sxs-lookup"><span data-stu-id="9ca46-132">hello script is added too**Group 1: Post-steps**.</span></span>

    ![Grupo 1: Iniciar de pós-ação](media/site-recovery-runbook-automation-new/addedscript-rp.PNG)


## <a name="considerations-for-adding-a-script"></a><span data-ttu-id="9ca46-134">Considerações sobre a adição de um script</span><span class="sxs-lookup"><span data-stu-id="9ca46-134">Considerations for adding a script</span></span>

* <span data-ttu-id="9ca46-135">Para opções muito**excluir uma etapa** ou **Atualizar script hello**, clique com botão direito script hello.</span><span class="sxs-lookup"><span data-stu-id="9ca46-135">For options too**delete a step** or **update hello script**, right-click hello script.</span></span>
* <span data-ttu-id="9ca46-136">Um script pode executar no Azure durante o failover de um tooAzure de máquina local.</span><span class="sxs-lookup"><span data-stu-id="9ca46-136">A script can run on Azure during failover from an on-premises machine tooAzure.</span></span> <span data-ttu-id="9ca46-137">Ele também pode executar no Azure como um script do site primário antes do desligamento, durante o failback da máquina do Azure tooan local.</span><span class="sxs-lookup"><span data-stu-id="9ca46-137">It also can run on Azure as a primary-site script before shutdown, during failback from Azure tooan on-premises machine.</span></span>
* <span data-ttu-id="9ca46-138">Quando um script é executado, ele injeta um contexto do plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="9ca46-138">When a script runs, it injects a recovery plan context.</span></span> <span data-ttu-id="9ca46-139">saudação de exemplo a seguir mostra uma variável de contexto:</span><span class="sxs-lookup"><span data-stu-id="9ca46-139">hello following example shows a context variable:</span></span>

    ```
            {"RecoveryPlanName":"hrweb-recovery",

            "FailoverType":"Test",

            "FailoverDirection":"PrimaryToSecondary",

            "GroupId":"1",

            "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                    { "SubscriptionId":"7a1111111-c1d6-49c5-8c5d-111ce8dd183",

                    "ResourceGroupName":"ContosoRG",

                    "CloudServiceName":"pod02hrweb-Chicago-test",

                    "RoleName":"Fabrikam-Hrweb-frontend-test",

                    "RecoveryPointId":"TimeStamp"}

                    }

            }
    ```

    <span data-ttu-id="9ca46-140">Olá, a tabela a seguir lista o nome de saudação e descrição de cada variável no contexto de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ca46-140">hello following table lists hello name and description of each variable in hello context.</span></span>

    | <span data-ttu-id="9ca46-141">**Nome da variável**</span><span class="sxs-lookup"><span data-stu-id="9ca46-141">**Variable name**</span></span> | <span data-ttu-id="9ca46-142">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="9ca46-142">**Description**</span></span> |
    | --- | --- |
    | <span data-ttu-id="9ca46-143">RecoveryPlanName</span><span class="sxs-lookup"><span data-stu-id="9ca46-143">RecoveryPlanName</span></span> |<span data-ttu-id="9ca46-144">nome de saudação do plano hello está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="9ca46-144">hello name of hello plan being run.</span></span> <span data-ttu-id="9ca46-145">Essa variável ajuda você a executar ações diferentes com base no nome do plano de recuperação de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ca46-145">This variable helps you take different actions based on hello recovery plan name.</span></span> <span data-ttu-id="9ca46-146">Você também pode reutilizar o script hello.</span><span class="sxs-lookup"><span data-stu-id="9ca46-146">You also can reuse hello script.</span></span> |
    | <span data-ttu-id="9ca46-147">FailoverType</span><span class="sxs-lookup"><span data-stu-id="9ca46-147">FailoverType</span></span> |<span data-ttu-id="9ca46-148">Especifica se o failover de saudação é um teste, planejado ou não planejado.</span><span class="sxs-lookup"><span data-stu-id="9ca46-148">Specifies whether hello failover is a test, planned, or unplanned.</span></span> |
    | <span data-ttu-id="9ca46-149">FailoverDirection</span><span class="sxs-lookup"><span data-stu-id="9ca46-149">FailoverDirection</span></span> |<span data-ttu-id="9ca46-150">Especifica se a recuperação é site primário ou secundário do tooa.</span><span class="sxs-lookup"><span data-stu-id="9ca46-150">Specifies whether recovery is tooa primary or secondary site.</span></span> |
    | <span data-ttu-id="9ca46-151">GroupID</span><span class="sxs-lookup"><span data-stu-id="9ca46-151">GroupID</span></span> |<span data-ttu-id="9ca46-152">Identifica o número de grupo de saudação no plano de recuperação de saudação quando plano hello está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="9ca46-152">Identifies hello group number in hello recovery plan when hello plan is running.</span></span> |
    | <span data-ttu-id="9ca46-153">VmMap</span><span class="sxs-lookup"><span data-stu-id="9ca46-153">VmMap</span></span> |<span data-ttu-id="9ca46-154">Uma matriz de todas as máquinas virtuais no grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ca46-154">An array of all VMs in hello group.</span></span> |
    | <span data-ttu-id="9ca46-155">Chave VMMap</span><span class="sxs-lookup"><span data-stu-id="9ca46-155">VMMap key</span></span> |<span data-ttu-id="9ca46-156">Uma chave exclusiva (GUID) para cada VM.</span><span class="sxs-lookup"><span data-stu-id="9ca46-156">A unique key (GUID) for each VM.</span></span> <span data-ttu-id="9ca46-157">Seu Olá igual Olá ID Azure Virtual Machine Manager (VMM) do hello VM, onde aplicável.</span><span class="sxs-lookup"><span data-stu-id="9ca46-157">It's hello same as hello Azure Virtual Machine Manager (VMM) ID of hello VM, where applicable.</span></span> |
    | <span data-ttu-id="9ca46-158">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="9ca46-158">SubscriptionId</span></span> |<span data-ttu-id="9ca46-159">ID de assinatura do Azure Olá Olá a VM no qual foi criado.</span><span class="sxs-lookup"><span data-stu-id="9ca46-159">hello Azure subscription ID in which hello VM was created.</span></span> |
    | <span data-ttu-id="9ca46-160">RoleName</span><span class="sxs-lookup"><span data-stu-id="9ca46-160">RoleName</span></span> |<span data-ttu-id="9ca46-161">nome de saudação do hello VM do Azure que está sendo recuperado.</span><span class="sxs-lookup"><span data-stu-id="9ca46-161">hello name of hello Azure VM that's being recovered.</span></span> |
    | <span data-ttu-id="9ca46-162">CloudServiceName</span><span class="sxs-lookup"><span data-stu-id="9ca46-162">CloudServiceName</span></span> |<span data-ttu-id="9ca46-163">nome do serviço de nuvem do Azure Olá que sob a qual Olá VM foi criada.</span><span class="sxs-lookup"><span data-stu-id="9ca46-163">hello Azure cloud service name under which hello VM was created.</span></span> |
    | <span data-ttu-id="9ca46-164">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="9ca46-164">ResourceGroupName</span></span>|<span data-ttu-id="9ca46-165">nome do grupo de recursos do Azure Olá que sob a qual Olá VM foi criada.</span><span class="sxs-lookup"><span data-stu-id="9ca46-165">hello Azure resource group name under which hello VM was created.</span></span> |
    | <span data-ttu-id="9ca46-166">RecoveryPointId</span><span class="sxs-lookup"><span data-stu-id="9ca46-166">RecoveryPointId</span></span>|<span data-ttu-id="9ca46-167">Olá carimbo de hora de quando Olá VM é recuperado.</span><span class="sxs-lookup"><span data-stu-id="9ca46-167">hello timestamp for when hello VM is recovered.</span></span> |

* <span data-ttu-id="9ca46-168">Certifique-se de que essa conta de automação Olá tem Olá módulos a seguir:</span><span class="sxs-lookup"><span data-stu-id="9ca46-168">Ensure that hello Automation account has hello following modules:</span></span>
    * <span data-ttu-id="9ca46-169">AzureRM.profile</span><span class="sxs-lookup"><span data-stu-id="9ca46-169">AzureRM.profile</span></span>
    * <span data-ttu-id="9ca46-170">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="9ca46-170">AzureRM.Resources</span></span>
    * <span data-ttu-id="9ca46-171">AzureRM.Automation</span><span class="sxs-lookup"><span data-stu-id="9ca46-171">AzureRM.Automation</span></span>
    * <span data-ttu-id="9ca46-172">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="9ca46-172">AzureRM.Network</span></span>
    * <span data-ttu-id="9ca46-173">AzureRM.Compute</span><span class="sxs-lookup"><span data-stu-id="9ca46-173">AzureRM.Compute</span></span>

<span data-ttu-id="9ca46-174">Todos os módulos devem ser de versões compatíveis.</span><span class="sxs-lookup"><span data-stu-id="9ca46-174">All modules should be of compatible versions.</span></span> <span data-ttu-id="9ca46-175">Um tooensure de maneira fácil que todos os módulos são compatíveis é toouse Olá últimas versões de todos os módulos de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ca46-175">An easy way tooensure that all modules are compatible is toouse hello latest versions of all hello modules.</span></span>

### <a name="access-all-vms-of-hello-vmmap-in-a-loop"></a><span data-ttu-id="9ca46-176">Acessar todas as VMs de saudação VMMap em um loop</span><span class="sxs-lookup"><span data-stu-id="9ca46-176">Access all VMs of hello VMMap in a loop</span></span>
<span data-ttu-id="9ca46-177">Use Olá tooloop de código a seguir em todas as VMs de saudação VMMap Microsoft:</span><span class="sxs-lookup"><span data-stu-id="9ca46-177">Use hello following code tooloop across all VMs of hello Microsoft VMMap:</span></span>

```
$VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
$vmMap = $RecoveryPlanContext.VmMap
 foreach($VMID in $VMinfo)
 {
     $VM = $vmMap.$VMID                
             if( !(($VM -eq $Null) -Or ($VM.ResourceGroupName -eq $Null) -Or ($VM.RoleName -eq $Null))) {
         #this check is tooensure that we skip when some data is not available else it will fail
 Write-output "Resource group name ", $VM.ResourceGroupName
 Write-output "Rolename " = $VM.RoleName
     }
 }

```

> [!NOTE]
> <span data-ttu-id="9ca46-178">Olá recurso grupo nome e a função de valores de nome estão vazios ao script hello é um grupo de inicialização de pré-ação tooa.</span><span class="sxs-lookup"><span data-stu-id="9ca46-178">hello resource group name and role name values are empty when hello script is a pre-action tooa boot group.</span></span> <span data-ttu-id="9ca46-179">os valores Hello serão populados apenas se Olá VM desse grupo terá êxito em failover.</span><span class="sxs-lookup"><span data-stu-id="9ca46-179">hello values are populated only if hello VM of that group succeeds in failover.</span></span> <span data-ttu-id="9ca46-180">script Hello é uma ação após do grupo de inicialização de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ca46-180">hello script is a post-action of hello boot group.</span></span>

## <a name="use-hello-same-automation-runbook-in-multiple-recovery-plans"></a><span data-ttu-id="9ca46-181">Use Olá mesmo runbook de automação em vários planos de recuperação</span><span class="sxs-lookup"><span data-stu-id="9ca46-181">Use hello same Automation runbook in multiple recovery plans</span></span>

<span data-ttu-id="9ca46-182">Use um único script em vários planos de recuperação com variáveis externas.</span><span class="sxs-lookup"><span data-stu-id="9ca46-182">You can use a single script in multiple recovery plans by using external variables.</span></span> <span data-ttu-id="9ca46-183">Você pode usar [variáveis de automação do Azure](../automation/automation-variables.md) toostore parâmetros que você pode passar para a recuperação de uma plano de execução.</span><span class="sxs-lookup"><span data-stu-id="9ca46-183">You can use [Azure Automation variables](../automation/automation-variables.md) toostore parameters that you can pass for a recovery plan execution.</span></span> <span data-ttu-id="9ca46-184">Adicionando o nome do plano de recuperação hello como uma variável de toohello de prefixo, você pode criar variáveis individuais para cada plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="9ca46-184">By adding hello recovery plan name as a prefix toohello variable, you can create individual variables for each recovery plan.</span></span> <span data-ttu-id="9ca46-185">Em seguida, use variáveis de saudação como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="9ca46-185">Then, use hello variables as parameters.</span></span> <span data-ttu-id="9ca46-186">Você pode alterar um parâmetro sem alterar o script hello, mas ainda alterar Olá Olá forma script funciona.</span><span class="sxs-lookup"><span data-stu-id="9ca46-186">You can change a parameter without changing hello script, but still change hello way hello script works.</span></span>

### <a name="use-a-simple-string-variable-in-a-runbook-script"></a><span data-ttu-id="9ca46-187">Usar uma variável de cadeia de caracteres simples em um script de runbook</span><span class="sxs-lookup"><span data-stu-id="9ca46-187">Use a simple string variable in a runbook script</span></span>

<span data-ttu-id="9ca46-188">Neste exemplo, um script obtém dados de entrada hello de um grupo de segurança de rede (NSG) e o aplica toohello VMs de um plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="9ca46-188">In this example, a script takes hello input of a Network Security Group (NSG) and applies it toohello VMs of a recovery plan.</span></span>

<span data-ttu-id="9ca46-189">Para toodetect de script hello plano de recuperação que está em execução, use o contexto do plano de recuperação de saudação:</span><span class="sxs-lookup"><span data-stu-id="9ca46-189">For hello script toodetect which recovery plan is running, use hello recovery plan context:</span></span>

```
workflow AddPublicIPAndNSG {
    param (
          [parameter(Mandatory=$false)]
          [Object]$RecoveryPlanContext
    )

    $RPName = $RecoveryPlanContext.RecoveryPlanName
```

<span data-ttu-id="9ca46-190">tooapply um NSG existente, você deve saber o nome do NSG hello e nome do grupo de recursos do hello NSG.</span><span class="sxs-lookup"><span data-stu-id="9ca46-190">tooapply an existing NSG, you must know hello NSG name and hello NSG resource group name.</span></span> <span data-ttu-id="9ca46-191">Use essas variáveis como entradas para scripts do plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="9ca46-191">Use these variables as inputs for recovery plan scripts.</span></span> <span data-ttu-id="9ca46-192">toodo isso, crie duas variáveis em Olá ativos da conta de automação.</span><span class="sxs-lookup"><span data-stu-id="9ca46-192">toodo this, create two variables in hello Automation account assets.</span></span> <span data-ttu-id="9ca46-193">Adicione nome Olá Olá do plano de recuperação que você está criando parâmetros de saudação para como um nome de variável de toohello de prefixo.</span><span class="sxs-lookup"><span data-stu-id="9ca46-193">Add hello name of hello recovery plan that you are creating hello parameters for as a prefix toohello variable name.</span></span>

1. <span data-ttu-id="9ca46-194">Crie um nome NSG Olá toostore variável.</span><span class="sxs-lookup"><span data-stu-id="9ca46-194">Create a variable toostore hello NSG name.</span></span> <span data-ttu-id="9ca46-195">Adicione um nome de variável de toohello de prefixo usando nome Olá Olá do plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="9ca46-195">Add a prefix toohello variable name by using hello name of hello recovery plan.</span></span>

    ![Criar uma variável do nome do NSG](media/site-recovery-runbook-automation-new/var1.png)

2. <span data-ttu-id="9ca46-197">Crie o nome do grupo de recursos do NSG uma variável toostore hello.</span><span class="sxs-lookup"><span data-stu-id="9ca46-197">Create a variable toostore hello NSG's resource group name.</span></span> <span data-ttu-id="9ca46-198">Adicione um nome de variável de toohello de prefixo usando nome Olá Olá do plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="9ca46-198">Add a prefix toohello variable name by using hello name of hello recovery plan.</span></span>

    ![Criar um nome do grupo de recursos do NSG](media/site-recovery-runbook-automation-new/var2.png)


3.  <span data-ttu-id="9ca46-200">No script hello, use Olá referência código tooget Olá variável valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="9ca46-200">In hello script, use hello following reference code tooget hello variable values:</span></span>

    ```
    $NSGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSG"
    $NSGRGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSGRG"

    $NSGnameVar = Get-AutomationVariable -Name $NSGValue
    $RGnameVar = Get-AutomationVariable -Name $NSGRGValue
    ```

4.  <span data-ttu-id="9ca46-201">Use as variáveis Olá no hello runbook tooapply Olá NSG toohello interface de rede Olá failover VM:</span><span class="sxs-lookup"><span data-stu-id="9ca46-201">Use hello variables in hello runbook tooapply hello NSG toohello network interface of hello failed-over VM:</span></span>

    ```
    InlineScript {
    if (($Using:NSGname -ne $Null) -And ($Using:NSGRGname -ne $Null)) {
            $NSG = Get-AzureRmNetworkSecurityGroup -Name $Using:NSGname -ResourceGroupName $Using:NSGRGname
            Write-output $NSG.Id
            #Apply hello NSG tooa network interface
            #$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
            #Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
            #  -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $NSG
        }
    }
    ```

<span data-ttu-id="9ca46-202">Para cada plano de recuperação, crie variáveis independentes, para que você pode reutilizar o script hello.</span><span class="sxs-lookup"><span data-stu-id="9ca46-202">For each recovery plan, create independent variables so that you can reuse hello script.</span></span> <span data-ttu-id="9ca46-203">Adicione um prefixo usando o nome do plano de recuperação de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ca46-203">Add a prefix by using hello recovery plan name.</span></span> <span data-ttu-id="9ca46-204">Para um script completo e de ponta a ponta para este cenário, consulte [adicionar um tooVMs públicos de IP e NSG durante o failover de teste de um plano de recuperação do Site Recovery](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).</span><span class="sxs-lookup"><span data-stu-id="9ca46-204">For a complete, end-to-end script for this scenario, see [Add a public IP and NSG tooVMs during test failover of a Site Recovery recovery plan](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).</span></span>


### <a name="use-a-complex-variable-toostore-more-information"></a><span data-ttu-id="9ca46-205">Use um toostore complexo de variável mais informações</span><span class="sxs-lookup"><span data-stu-id="9ca46-205">Use a complex variable toostore more information</span></span>

<span data-ttu-id="9ca46-206">Considere um cenário no qual você deseja tooturn um único script em um IP público em máquinas virtuais específicas.</span><span class="sxs-lookup"><span data-stu-id="9ca46-206">Consider a scenario in which you want a single script tooturn on a public IP on specific VMs.</span></span> <span data-ttu-id="9ca46-207">Em outro cenário, você pode querer tooapply NSGs diferentes em VMs diferentes (não em todas as máquinas virtuais).</span><span class="sxs-lookup"><span data-stu-id="9ca46-207">In another scenario, you might want tooapply different NSGs on different VMs (not on all VMs).</span></span> <span data-ttu-id="9ca46-208">Você pode criar um script que é reutilizável para qualquer plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="9ca46-208">You can make a script that is reusable for any recovery plan.</span></span> <span data-ttu-id="9ca46-209">Cada plano de recuperação pode ter um número variável de VMs.</span><span class="sxs-lookup"><span data-stu-id="9ca46-209">Each recovery plan can have a variable number of VMs.</span></span> <span data-ttu-id="9ca46-210">Por exemplo, uma recuperação do SharePoint tem dois front-ends.</span><span class="sxs-lookup"><span data-stu-id="9ca46-210">For example, a SharePoint recovery has two front ends.</span></span> <span data-ttu-id="9ca46-211">Um aplicativo LOB (linha de negócios) básico tem apenas um front-end.</span><span class="sxs-lookup"><span data-stu-id="9ca46-211">A basic line-of-business (LOB) application has only one front end.</span></span> <span data-ttu-id="9ca46-212">Não é possível criar variáveis separadas para cada plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="9ca46-212">You cannot create separate variables for each recovery plan.</span></span> 

<span data-ttu-id="9ca46-213">Saudação de exemplo a seguir, vamos usar uma técnica de novo e criar um [complexo de variável](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) em ativos de conta de automação do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9ca46-213">In hello following example, we use a new technique and create a [complex variable](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) in hello Azure Automation account assets.</span></span> <span data-ttu-id="9ca46-214">Faça isso especificando vários valores.</span><span class="sxs-lookup"><span data-stu-id="9ca46-214">You do this by specifying multiple values.</span></span> <span data-ttu-id="9ca46-215">Você deve usar o Azure PowerShell toocomplete Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9ca46-215">You must use Azure PowerShell toocomplete hello following steps:</span></span>

1. <span data-ttu-id="9ca46-216">No PowerShell, entrar tooyour assinatura do Azure:</span><span class="sxs-lookup"><span data-stu-id="9ca46-216">In PowerShell, sign in tooyour Azure subscription:</span></span>

    ```
    login-azurermaccount
    $sub = Get-AzureRmSubscription -Name <SubscriptionName>
    $sub | Select-AzureRmSubscription
    ```

2. <span data-ttu-id="9ca46-217">parâmetros de saudação toostore, criar Olá complexo de variável usando nome Olá Olá do plano de recuperação:</span><span class="sxs-lookup"><span data-stu-id="9ca46-217">toostore hello parameters, create hello complex variable by using hello name of hello recovery plan:</span></span>

    ```
    $VMDetails = @{"VMGUID"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"};"VMGUID2"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"}}
        New-AzureRmAutomationVariable -ResourceGroupName <RG of Automation Account> -AutomationAccountName <AA Name> -Name <RecoveryPlanName> -Value $VMDetails -Encrypted $false
    ```

3. <span data-ttu-id="9ca46-218">Nessa variável complexo, **VMDetails** é hello ID da VM para Olá protegido VM.</span><span class="sxs-lookup"><span data-stu-id="9ca46-218">In this complex variable, **VMDetails** is hello VM ID for hello protected VM.</span></span> <span data-ttu-id="9ca46-219">Olá tooget ID da VM, em Olá portal do Azure, exibir propriedades da VM Olá.</span><span class="sxs-lookup"><span data-stu-id="9ca46-219">tooget hello VM ID, in hello Azure portal, view hello VM properties.</span></span> <span data-ttu-id="9ca46-220">Olá seguinte captura de tela mostra uma variável que armazena os detalhes de saudação de duas VMs:</span><span class="sxs-lookup"><span data-stu-id="9ca46-220">hello following screenshot shows a variable that stores hello details of two VMs:</span></span>

    ![Usar Olá ID da VM como Olá GUID](media/site-recovery-runbook-automation-new/vmguid.png)

4. <span data-ttu-id="9ca46-222">Use essa variável no runbook.</span><span class="sxs-lookup"><span data-stu-id="9ca46-222">Use this variable in your runbook.</span></span> <span data-ttu-id="9ca46-223">Se Olá indicado que GUID da VM foi encontrado no contexto de plano de recuperação hello, aplica Olá NSG Olá VM:</span><span class="sxs-lookup"><span data-stu-id="9ca46-223">If hello indicated VM GUID is found in hello recovery plan context, apply hello NSG on hello VM:</span></span>

    ```
    $VMDetailsObj = Get-AutomationVariable -Name $RecoveryPlanContext.RecoveryPlanName
    ```

4. <span data-ttu-id="9ca46-224">Em seu runbook, um loop VMs de saudação do contexto de plano de recuperação de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ca46-224">In your runbook, loop through hello VMs of hello recovery plan context.</span></span> <span data-ttu-id="9ca46-225">Verifique se Olá VM existe no **$VMDetailsObj**.</span><span class="sxs-lookup"><span data-stu-id="9ca46-225">Check whether hello VM exists in **$VMDetailsObj**.</span></span> <span data-ttu-id="9ca46-226">Se ele existir, propriedades de saudação do acesso de tooapply variável Olá Olá NSG:</span><span class="sxs-lookup"><span data-stu-id="9ca46-226">If it exists, access hello properties of hello variable tooapply hello NSG:</span></span>

    ```
        $VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
        $vmMap = $RecoveryPlanContext.VmMap

        foreach($VMID in $VMinfo) {
            Write-output $VMDetailsObj.value.$VMID

            if ($VMDetailsObj.value.$VMID -ne $Null) { #If hello VM exists in hello context, this will not b Null
                $VM = $vmMap.$VMID
                # Access hello properties of hello variable
                $NSGname = $VMDetailsObj.value.$VMID.'NSGName'
                $NSGRGname = $VMDetailsObj.value.$VMID.'NSGResourceGroupName'

                # Add code tooapply hello NSG properties toohello VM
            }
        }
    ```

<span data-ttu-id="9ca46-227">Você pode usar o hello mesmo script de planos de recuperação diferente.</span><span class="sxs-lookup"><span data-stu-id="9ca46-227">You can use hello same script for different recovery plans.</span></span> <span data-ttu-id="9ca46-228">Insira parâmetros diferentes, armazenando o valor de saudação que corresponde o plano de recuperação de tooa em variáveis diferentes.</span><span class="sxs-lookup"><span data-stu-id="9ca46-228">Enter different parameters by storing hello value that corresponds tooa recovery plan in different variables.</span></span>

## <a name="sample-scripts"></a><span data-ttu-id="9ca46-229">Exemplos de scripts</span><span class="sxs-lookup"><span data-stu-id="9ca46-229">Sample scripts</span></span>

<span data-ttu-id="9ca46-230">tooyour scripts de exemplo toodeploy conta de automação, clique em Olá **implantar tooAzure** botão.</span><span class="sxs-lookup"><span data-stu-id="9ca46-230">toodeploy sample scripts tooyour Automation account, click hello **Deploy tooAzure** button.</span></span>

<span data-ttu-id="9ca46-231">[![Implantar tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span><span class="sxs-lookup"><span data-stu-id="9ca46-231">[![Deploy tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span></span>

<span data-ttu-id="9ca46-232">Outro exemplo, consulte Olá vídeo a seguir.</span><span class="sxs-lookup"><span data-stu-id="9ca46-232">For another example, see hello following video.</span></span> <span data-ttu-id="9ca46-233">Ele demonstra como toorecover tooAzure de aplicativo de WordPress uma de duas camadas:</span><span class="sxs-lookup"><span data-stu-id="9ca46-233">It demonstrates how toorecover a two-tier WordPress application tooAzure:</span></span>


> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/One-click-failover-of-a-2-tier-WordPress-application-using-Azure-Site-Recovery/player]



## <a name="additional-resources"></a><span data-ttu-id="9ca46-234">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="9ca46-234">Additional resources</span></span>
* [<span data-ttu-id="9ca46-235">Conta Executar como do serviço de Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="9ca46-235">Azure Automation service Run As account</span></span>](../automation/automation-sec-configure-azure-runas-account.md)
* [<span data-ttu-id="9ca46-236">Visão geral da Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="9ca46-236">Azure Automation overview</span></span>](http://msdn.microsoft.com/library/azure/dn643629.aspx "Visão geral da Automação do Azure")
* [<span data-ttu-id="9ca46-237">Scripts de exemplo da Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="9ca46-237">Azure Automation sample scripts</span></span>](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Scripts de exemplo da Automação do Azure")
