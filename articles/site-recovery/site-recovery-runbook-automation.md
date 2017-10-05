---
title: "Adicionar runbooks de Automação do Azure aos planos de recuperação no Azure Site Recovery | Microsoft Docs"
description: "Saiba como o Azure Site Recovery pode ajudar você a estender planos de recuperação usando a Automação do Azure. Saiba como concluir tarefas complexas durante a recuperação no Azure."
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
ms.openlocfilehash: 064a6782970b950543f93c24800998c1f104c8df
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="add-azure-automation-runbooks-to-recovery-plans"></a><span data-ttu-id="38662-104">Adicionar runbooks de Automação do Azure aos planos de recuperação</span><span class="sxs-lookup"><span data-stu-id="38662-104">Add Azure Automation runbooks to recovery plans</span></span>
<span data-ttu-id="38662-105">Neste artigo, descrevemos como o Azure Site Recovery é integrado à Automação do Azure para ajudar você a estender seus planos de recuperação.</span><span class="sxs-lookup"><span data-stu-id="38662-105">In this article, we describe how Azure Site Recovery integrates with Azure Automation to help you extend your recovery plans.</span></span> <span data-ttu-id="38662-106">Os planos de recuperação podem orquestrar a recuperação de VMs que são protegidas com o Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="38662-106">Recovery plans can orchestrate recovery of VMs that are protected with Site Recovery.</span></span> <span data-ttu-id="38662-107">Os planos de recuperação funcionam para a replicação em uma nuvem secundária e para a replicação no Azure.</span><span class="sxs-lookup"><span data-stu-id="38662-107">Recovery plans work both for replication to a secondary cloud, and for replication to Azure.</span></span> <span data-ttu-id="38662-108">Os planos de recuperação também ajudam a tornar a recuperação **precisa de forma consistente**, **repetida** e **automatizada**.</span><span class="sxs-lookup"><span data-stu-id="38662-108">Recovery plans also help make the recovery **consistently accurate**, **repeatable**, and **automated**.</span></span> <span data-ttu-id="38662-109">Se você fizer failover das VMs no Azure, a integração com a Automação do Azure estenderá os planos de recuperação.</span><span class="sxs-lookup"><span data-stu-id="38662-109">If you fail over your VMs to Azure, integration with Azure Automation extends your recovery plans.</span></span> <span data-ttu-id="38662-110">Você pode usá-la para executar runbooks, que oferecem tarefas de automação avançadas.</span><span class="sxs-lookup"><span data-stu-id="38662-110">You can use it to execute runbooks, which offer powerful automation tasks.</span></span>

<span data-ttu-id="38662-111">Se você estiver conhecendo a Automação do Azure agora, [inscreva-se](https://azure.microsoft.com/services/automation/) e [baixe scripts de exemplo](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="38662-111">If you are new to Azure Automation, you can [sign up](https://azure.microsoft.com/services/automation/) and [download sample scripts](https://azure.microsoft.com/documentation/scripts/).</span></span> <span data-ttu-id="38662-112">Para obter mais informações e para saber como orquestrar a recuperação no Azure usando [planos de recuperação](https://azure.microsoft.com/blog/?p=166264), consulte [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="38662-112">For more information, and to learn how to orchestrate recovery to Azure by using [recovery plans](https://azure.microsoft.com/blog/?p=166264), see [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).</span></span>

<span data-ttu-id="38662-113">Neste artigo, descrevemos como você pode integrar runbooks da Automação do Azure em planos de recuperação.</span><span class="sxs-lookup"><span data-stu-id="38662-113">In this article, we describe how you can integrate Azure Automation runbooks into your recovery plans.</span></span> <span data-ttu-id="38662-114">Usamos exemplos para automatizar tarefas básicas que anteriormente necessitavam de intervenção manual.</span><span class="sxs-lookup"><span data-stu-id="38662-114">We use examples to automate basic tasks that previously required manual intervention.</span></span> <span data-ttu-id="38662-115">Também descrevemos como converter uma recuperação de várias etapas em uma ação de recuperação de clique simples.</span><span class="sxs-lookup"><span data-stu-id="38662-115">We also describe how to convert a multi-step recovery to a single-click recovery action.</span></span>

## <a name="customize-the-recovery-plan"></a><span data-ttu-id="38662-116">Personalizar o plano de recuperação</span><span class="sxs-lookup"><span data-stu-id="38662-116">Customize the recovery plan</span></span>
1. <span data-ttu-id="38662-117">Acesse a folha de recursos do plano de recuperação do **Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="38662-117">Go to the **Site Recovery** recovery plan resource blade.</span></span> <span data-ttu-id="38662-118">Neste exemplo, o plano de recuperação tem duas VMs adicionadas a ele, para recuperação.</span><span class="sxs-lookup"><span data-stu-id="38662-118">For this example, the recovery plan has two VMs added to it, for recovery.</span></span> <span data-ttu-id="38662-119">Para começar a adicionar um runbook, clique na guia **Personalizar**.</span><span class="sxs-lookup"><span data-stu-id="38662-119">To begin adding a runbook, click the **Customize** tab.</span></span>

    ![Clicar no botão Personalizar](media/site-recovery-runbook-automation-new/essentials-rp.png)


2. <span data-ttu-id="38662-121">Clique com o botão direito do mouse em **Grupo 1: Iniciar** e, em seguida, selecione **Adicionar pós-ação**.</span><span class="sxs-lookup"><span data-stu-id="38662-121">Right-click **Group 1: Start**, and then select **Add post action**.</span></span>

    ![Clicar com o botão direito do mouse em Grupo 1: Iniciar e em Adicionar pós-ação](media/site-recovery-runbook-automation-new/customize-rp.png)

3. <span data-ttu-id="38662-123">Clique em **Escolher um script**.</span><span class="sxs-lookup"><span data-stu-id="38662-123">Click **Choose a script**.</span></span>

4. <span data-ttu-id="38662-124">Na folha **Atualizar ação**, nomeie o script **Olá, Mundo**.</span><span class="sxs-lookup"><span data-stu-id="38662-124">On the **Update action** blade, name the script **Hello World**.</span></span>

    ![A folha Atualizar ação](media/site-recovery-runbook-automation-new/update-rp.png)

5. <span data-ttu-id="38662-126">Insira um nome para a conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="38662-126">Enter an Automation account name.</span></span>
    >[!NOTE]
    > <span data-ttu-id="38662-127">A conta de Automação pode estar em qualquer região do Azure.</span><span class="sxs-lookup"><span data-stu-id="38662-127">The Automation account can be in any Azure region.</span></span> <span data-ttu-id="38662-128">A conta de Automação deve estar na mesma assinatura do cofre do Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="38662-128">The Automation account must be in the same subscription as the Azure Site Recovery vault.</span></span>

6. <span data-ttu-id="38662-129">Na conta de Automação, selecione um runbook.</span><span class="sxs-lookup"><span data-stu-id="38662-129">In your Automation account, select a runbook.</span></span> <span data-ttu-id="38662-130">Esse runbook é o script que é executado durante a execução do plano de recuperação, após a recuperação do primeiro grupo.</span><span class="sxs-lookup"><span data-stu-id="38662-130">This runbook is the script that runs during the execution of the recovery plan, after the recovery of the first group.</span></span>

7. <span data-ttu-id="38662-131">Para salvar o script, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="38662-131">To save the script, click **OK**.</span></span> <span data-ttu-id="38662-132">O script é adicionado ao **Grupo 1: Pós-etapas**.</span><span class="sxs-lookup"><span data-stu-id="38662-132">The script is added to **Group 1: Post-steps**.</span></span>

    ![Grupo 1: Iniciar de pós-ação](media/site-recovery-runbook-automation-new/addedscript-rp.PNG)


## <a name="considerations-for-adding-a-script"></a><span data-ttu-id="38662-134">Considerações sobre a adição de um script</span><span class="sxs-lookup"><span data-stu-id="38662-134">Considerations for adding a script</span></span>

* <span data-ttu-id="38662-135">Para obter opções para **excluir uma etapa** ou **atualizar o script**, clique com o botão direito do mouse no script.</span><span class="sxs-lookup"><span data-stu-id="38662-135">For options to **delete a step** or **update the script**, right-click the script.</span></span>
* <span data-ttu-id="38662-136">Um script pode ser executado no Azure durante o failover de um computador local para o Azure.</span><span class="sxs-lookup"><span data-stu-id="38662-136">A script can run on Azure during failover from an on-premises machine to Azure.</span></span> <span data-ttu-id="38662-137">Ele também pode ser executado no Azure como um script do site primário antes do desligamento, durante o failback do Azure para um computador local.</span><span class="sxs-lookup"><span data-stu-id="38662-137">It also can run on Azure as a primary-site script before shutdown, during failback from Azure to an on-premises machine.</span></span>
* <span data-ttu-id="38662-138">Quando um script é executado, ele injeta um contexto do plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="38662-138">When a script runs, it injects a recovery plan context.</span></span> <span data-ttu-id="38662-139">O seguinte exemplo mostra uma variável de contexto:</span><span class="sxs-lookup"><span data-stu-id="38662-139">The following example shows a context variable:</span></span>

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

    <span data-ttu-id="38662-140">A tabela a seguir lista o nome e a descrição de cada variável no contexto.</span><span class="sxs-lookup"><span data-stu-id="38662-140">The following table lists the name and description of each variable in the context.</span></span>

    | <span data-ttu-id="38662-141">**Nome da variável**</span><span class="sxs-lookup"><span data-stu-id="38662-141">**Variable name**</span></span> | <span data-ttu-id="38662-142">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="38662-142">**Description**</span></span> |
    | --- | --- |
    | <span data-ttu-id="38662-143">RecoveryPlanName</span><span class="sxs-lookup"><span data-stu-id="38662-143">RecoveryPlanName</span></span> |<span data-ttu-id="38662-144">O nome do plano em execução.</span><span class="sxs-lookup"><span data-stu-id="38662-144">The name of the plan being run.</span></span> <span data-ttu-id="38662-145">Essa variável ajuda você a executar ações diferentes com base no nome do plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="38662-145">This variable helps you take different actions based on the recovery plan name.</span></span> <span data-ttu-id="38662-146">Também é possível reutilizar o script.</span><span class="sxs-lookup"><span data-stu-id="38662-146">You also can reuse the script.</span></span> |
    | <span data-ttu-id="38662-147">FailoverType</span><span class="sxs-lookup"><span data-stu-id="38662-147">FailoverType</span></span> |<span data-ttu-id="38662-148">Especifica se o failover é um teste, planejado ou não planejado.</span><span class="sxs-lookup"><span data-stu-id="38662-148">Specifies whether the failover is a test, planned, or unplanned.</span></span> |
    | <span data-ttu-id="38662-149">FailoverDirection</span><span class="sxs-lookup"><span data-stu-id="38662-149">FailoverDirection</span></span> |<span data-ttu-id="38662-150">Especifica se a recuperação é feita em um site primário ou secundário.</span><span class="sxs-lookup"><span data-stu-id="38662-150">Specifies whether recovery is to a primary or secondary site.</span></span> |
    | <span data-ttu-id="38662-151">GroupID</span><span class="sxs-lookup"><span data-stu-id="38662-151">GroupID</span></span> |<span data-ttu-id="38662-152">Identifica o número de grupo no plano de recuperação quando o plano está em execução.</span><span class="sxs-lookup"><span data-stu-id="38662-152">Identifies the group number in the recovery plan when the plan is running.</span></span> |
    | <span data-ttu-id="38662-153">VmMap</span><span class="sxs-lookup"><span data-stu-id="38662-153">VmMap</span></span> |<span data-ttu-id="38662-154">Uma matriz de todas as VMs do grupo.</span><span class="sxs-lookup"><span data-stu-id="38662-154">An array of all VMs in the group.</span></span> |
    | <span data-ttu-id="38662-155">Chave VMMap</span><span class="sxs-lookup"><span data-stu-id="38662-155">VMMap key</span></span> |<span data-ttu-id="38662-156">Uma chave exclusiva (GUID) para cada VM.</span><span class="sxs-lookup"><span data-stu-id="38662-156">A unique key (GUID) for each VM.</span></span> <span data-ttu-id="38662-157">Igual à ID do Azure VMM (Virtual Machine Manager) da VM, quando aplicável.</span><span class="sxs-lookup"><span data-stu-id="38662-157">It's the same as the Azure Virtual Machine Manager (VMM) ID of the VM, where applicable.</span></span> |
    | <span data-ttu-id="38662-158">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="38662-158">SubscriptionId</span></span> |<span data-ttu-id="38662-159">A ID da assinatura do Azure em que a VM foi criada.</span><span class="sxs-lookup"><span data-stu-id="38662-159">The Azure subscription ID in which the VM was created.</span></span> |
    | <span data-ttu-id="38662-160">RoleName</span><span class="sxs-lookup"><span data-stu-id="38662-160">RoleName</span></span> |<span data-ttu-id="38662-161">O nome da VM do Azure que está sendo recuperada.</span><span class="sxs-lookup"><span data-stu-id="38662-161">The name of the Azure VM that's being recovered.</span></span> |
    | <span data-ttu-id="38662-162">CloudServiceName</span><span class="sxs-lookup"><span data-stu-id="38662-162">CloudServiceName</span></span> |<span data-ttu-id="38662-163">O nome de serviço de nuvem do Azure no qual a VM foi criada.</span><span class="sxs-lookup"><span data-stu-id="38662-163">The Azure cloud service name under which the VM was created.</span></span> |
    | <span data-ttu-id="38662-164">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="38662-164">ResourceGroupName</span></span>|<span data-ttu-id="38662-165">O nome do grupo de recursos do Azure no qual a VM foi criada.</span><span class="sxs-lookup"><span data-stu-id="38662-165">The Azure resource group name under which the VM was created.</span></span> |
    | <span data-ttu-id="38662-166">RecoveryPointId</span><span class="sxs-lookup"><span data-stu-id="38662-166">RecoveryPointId</span></span>|<span data-ttu-id="38662-167">O carimbo de data/hora de quando a VM foi recuperada.</span><span class="sxs-lookup"><span data-stu-id="38662-167">The timestamp for when the VM is recovered.</span></span> |

* <span data-ttu-id="38662-168">Garanta que a conta de Automação tem os seguintes módulos:</span><span class="sxs-lookup"><span data-stu-id="38662-168">Ensure that the Automation account has the following modules:</span></span>
    * <span data-ttu-id="38662-169">AzureRM.profile</span><span class="sxs-lookup"><span data-stu-id="38662-169">AzureRM.profile</span></span>
    * <span data-ttu-id="38662-170">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="38662-170">AzureRM.Resources</span></span>
    * <span data-ttu-id="38662-171">AzureRM.Automation</span><span class="sxs-lookup"><span data-stu-id="38662-171">AzureRM.Automation</span></span>
    * <span data-ttu-id="38662-172">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="38662-172">AzureRM.Network</span></span>
    * <span data-ttu-id="38662-173">AzureRM.Compute</span><span class="sxs-lookup"><span data-stu-id="38662-173">AzureRM.Compute</span></span>

<span data-ttu-id="38662-174">Todos os módulos devem ser de versões compatíveis.</span><span class="sxs-lookup"><span data-stu-id="38662-174">All modules should be of compatible versions.</span></span> <span data-ttu-id="38662-175">Uma maneira fácil de garantir que todos os módulos são compatíveis é usar as últimas versões de todos os módulos.</span><span class="sxs-lookup"><span data-stu-id="38662-175">An easy way to ensure that all modules are compatible is to use the latest versions of all the modules.</span></span>

### <a name="access-all-vms-of-the-vmmap-in-a-loop"></a><span data-ttu-id="38662-176">Acessar todas as VMs do VMMap em um loop</span><span class="sxs-lookup"><span data-stu-id="38662-176">Access all VMs of the VMMap in a loop</span></span>
<span data-ttu-id="38662-177">Use o seguinte código para criar um loop em todas as VMs do Microsoft VMMap:</span><span class="sxs-lookup"><span data-stu-id="38662-177">Use the following code to loop across all VMs of the Microsoft VMMap:</span></span>

```
$VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
$vmMap = $RecoveryPlanContext.VmMap
 foreach($VMID in $VMinfo)
 {
     $VM = $vmMap.$VMID                
             if( !(($VM -eq $Null) -Or ($VM.ResourceGroupName -eq $Null) -Or ($VM.RoleName -eq $Null))) {
         #this check is to ensure that we skip when some data is not available else it will fail
 Write-output "Resource group name ", $VM.ResourceGroupName
 Write-output "Rolename " = $VM.RoleName
     }
 }

```

> [!NOTE]
> <span data-ttu-id="38662-178">O nome do grupo de recursos e os valores do nome da função ficam vazios quando o script é uma pré-ação de um grupo de inicialização.</span><span class="sxs-lookup"><span data-stu-id="38662-178">The resource group name and role name values are empty when the script is a pre-action to a boot group.</span></span> <span data-ttu-id="38662-179">Os valores são populados somente se a VM do grupo tem êxito no failover.</span><span class="sxs-lookup"><span data-stu-id="38662-179">The values are populated only if the VM of that group succeeds in failover.</span></span> <span data-ttu-id="38662-180">O script é uma pós-ação do grupo de inicialização.</span><span class="sxs-lookup"><span data-stu-id="38662-180">The script is a post-action of the boot group.</span></span>

## <a name="use-the-same-automation-runbook-in-multiple-recovery-plans"></a><span data-ttu-id="38662-181">Usar o mesmo runbook de Automação em vários planos de recuperação</span><span class="sxs-lookup"><span data-stu-id="38662-181">Use the same Automation runbook in multiple recovery plans</span></span>

<span data-ttu-id="38662-182">Use um único script em vários planos de recuperação com variáveis externas.</span><span class="sxs-lookup"><span data-stu-id="38662-182">You can use a single script in multiple recovery plans by using external variables.</span></span> <span data-ttu-id="38662-183">Use as [variáveis da Automação do Azure](../automation/automation-variables.md) para armazenar os parâmetros que podem ser passados para a execução de um plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="38662-183">You can use [Azure Automation variables](../automation/automation-variables.md) to store parameters that you can pass for a recovery plan execution.</span></span> <span data-ttu-id="38662-184">Adicionando o nome do plano de recuperação como um prefixo da variável, você pode criar variáveis individuais para cada plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="38662-184">By adding the recovery plan name as a prefix to the variable, you can create individual variables for each recovery plan.</span></span> <span data-ttu-id="38662-185">Em seguida, use as variáveis como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="38662-185">Then, use the variables as parameters.</span></span> <span data-ttu-id="38662-186">Altere um parâmetro sem alterar o script, mas ainda altere a maneira como o script funciona.</span><span class="sxs-lookup"><span data-stu-id="38662-186">You can change a parameter without changing the script, but still change the way the script works.</span></span>

### <a name="use-a-simple-string-variable-in-a-runbook-script"></a><span data-ttu-id="38662-187">Usar uma variável de cadeia de caracteres simples em um script de runbook</span><span class="sxs-lookup"><span data-stu-id="38662-187">Use a simple string variable in a runbook script</span></span>

<span data-ttu-id="38662-188">Neste exemplo, um script usa a entrada de um NSG (Grupo de Segurança de Rede) e a aplica às VMs de um plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="38662-188">In this example, a script takes the input of a Network Security Group (NSG) and applies it to the VMs of a recovery plan.</span></span>

<span data-ttu-id="38662-189">Para que o script detecte qual plano de recuperação está em execução, use o contexto do plano de recuperação:</span><span class="sxs-lookup"><span data-stu-id="38662-189">For the script to detect which recovery plan is running, use the recovery plan context:</span></span>

```
workflow AddPublicIPAndNSG {
    param (
          [parameter(Mandatory=$false)]
          [Object]$RecoveryPlanContext
    )

    $RPName = $RecoveryPlanContext.RecoveryPlanName
```

<span data-ttu-id="38662-190">Para aplicar um NSG existente, você deve saber o nome do NSG e o nome do grupo de recursos do NSG.</span><span class="sxs-lookup"><span data-stu-id="38662-190">To apply an existing NSG, you must know the NSG name and the NSG resource group name.</span></span> <span data-ttu-id="38662-191">Use essas variáveis como entradas para scripts do plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="38662-191">Use these variables as inputs for recovery plan scripts.</span></span> <span data-ttu-id="38662-192">Para fazer isso, crie duas variáveis nos ativos da conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="38662-192">To do this, create two variables in the Automation account assets.</span></span> <span data-ttu-id="38662-193">Adicione o nome do plano de recuperação para o qual os parâmetros estão sendo criados como um prefixo do nome da variável.</span><span class="sxs-lookup"><span data-stu-id="38662-193">Add the name of the recovery plan that you are creating the parameters for as a prefix to the variable name.</span></span>

1. <span data-ttu-id="38662-194">Crie uma variável para armazenar o nome do NSG.</span><span class="sxs-lookup"><span data-stu-id="38662-194">Create a variable to store the NSG name.</span></span> <span data-ttu-id="38662-195">Adicione um prefixo ao nome da variável usando o nome do plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="38662-195">Add a prefix to the variable name by using the name of the recovery plan.</span></span>

    ![Criar uma variável do nome do NSG](media/site-recovery-runbook-automation-new/var1.png)

2. <span data-ttu-id="38662-197">Crie uma variável para armazenar o nome do grupo de recursos do NSG.</span><span class="sxs-lookup"><span data-stu-id="38662-197">Create a variable to store the NSG's resource group name.</span></span> <span data-ttu-id="38662-198">Adicione um prefixo ao nome da variável usando o nome do plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="38662-198">Add a prefix to the variable name by using the name of the recovery plan.</span></span>

    ![Criar um nome do grupo de recursos do NSG](media/site-recovery-runbook-automation-new/var2.png)


3.  <span data-ttu-id="38662-200">No script, use o seguinte código de referência para obter os valores de variáveis:</span><span class="sxs-lookup"><span data-stu-id="38662-200">In the script, use the following reference code to get the variable values:</span></span>

    ```
    $NSGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSG"
    $NSGRGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSGRG"

    $NSGnameVar = Get-AutomationVariable -Name $NSGValue
    $RGnameVar = Get-AutomationVariable -Name $NSGRGValue
    ```

4.  <span data-ttu-id="38662-201">Use as variáveis no runbook para aplicar o NSG ao adaptador de rede da VM com failover:</span><span class="sxs-lookup"><span data-stu-id="38662-201">Use the variables in the runbook to apply the NSG to the network interface of the failed-over VM:</span></span>

    ```
    InlineScript {
    if (($Using:NSGname -ne $Null) -And ($Using:NSGRGname -ne $Null)) {
            $NSG = Get-AzureRmNetworkSecurityGroup -Name $Using:NSGname -ResourceGroupName $Using:NSGRGname
            Write-output $NSG.Id
            #Apply the NSG to a network interface
            #$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
            #Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
            #  -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $NSG
        }
    }
    ```

<span data-ttu-id="38662-202">Para cada plano de recuperação, crie variáveis independentes, de modo que você possa reutilizar o script.</span><span class="sxs-lookup"><span data-stu-id="38662-202">For each recovery plan, create independent variables so that you can reuse the script.</span></span> <span data-ttu-id="38662-203">Adicione um prefixo usando o nome do plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="38662-203">Add a prefix by using the recovery plan name.</span></span> <span data-ttu-id="38662-204">Para obter um script completo de ponta a ponta para este cenário, consulte [Adicionar um IP público e um NSG a VMs durante o failover de teste de um plano de recuperação do Site Recovery](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).</span><span class="sxs-lookup"><span data-stu-id="38662-204">For a complete, end-to-end script for this scenario, see [Add a public IP and NSG to VMs during test failover of a Site Recovery recovery plan](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).</span></span>


### <a name="use-a-complex-variable-to-store-more-information"></a><span data-ttu-id="38662-205">Usar uma variável complexa para armazenar mais informações</span><span class="sxs-lookup"><span data-stu-id="38662-205">Use a complex variable to store more information</span></span>

<span data-ttu-id="38662-206">Considere um cenário no qual você deseja que um único script ative um IP público em VMs específicas.</span><span class="sxs-lookup"><span data-stu-id="38662-206">Consider a scenario in which you want a single script to turn on a public IP on specific VMs.</span></span> <span data-ttu-id="38662-207">Em outro cenário, talvez você deseje aplicar NSGs diferentes a VMs diferentes (não em todas as VMs).</span><span class="sxs-lookup"><span data-stu-id="38662-207">In another scenario, you might want to apply different NSGs on different VMs (not on all VMs).</span></span> <span data-ttu-id="38662-208">Você pode criar um script que é reutilizável para qualquer plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="38662-208">You can make a script that is reusable for any recovery plan.</span></span> <span data-ttu-id="38662-209">Cada plano de recuperação pode ter um número variável de VMs.</span><span class="sxs-lookup"><span data-stu-id="38662-209">Each recovery plan can have a variable number of VMs.</span></span> <span data-ttu-id="38662-210">Por exemplo, uma recuperação do SharePoint tem dois front-ends.</span><span class="sxs-lookup"><span data-stu-id="38662-210">For example, a SharePoint recovery has two front ends.</span></span> <span data-ttu-id="38662-211">Um aplicativo LOB (linha de negócios) básico tem apenas um front-end.</span><span class="sxs-lookup"><span data-stu-id="38662-211">A basic line-of-business (LOB) application has only one front end.</span></span> <span data-ttu-id="38662-212">Não é possível criar variáveis separadas para cada plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="38662-212">You cannot create separate variables for each recovery plan.</span></span> 

<span data-ttu-id="38662-213">No exemplo a seguir, usamos uma nova técnica e criamos uma [variável complexa](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) nos ativos da conta de Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="38662-213">In the following example, we use a new technique and create a [complex variable](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) in the Azure Automation account assets.</span></span> <span data-ttu-id="38662-214">Faça isso especificando vários valores.</span><span class="sxs-lookup"><span data-stu-id="38662-214">You do this by specifying multiple values.</span></span> <span data-ttu-id="38662-215">Use o Azure PowerShell para concluir as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="38662-215">You must use Azure PowerShell to complete the following steps:</span></span>

1. <span data-ttu-id="38662-216">No PowerShell, entre em sua assinatura do Azure:</span><span class="sxs-lookup"><span data-stu-id="38662-216">In PowerShell, sign in to your Azure subscription:</span></span>

    ```
    login-azurermaccount
    $sub = Get-AzureRmSubscription -Name <SubscriptionName>
    $sub | Select-AzureRmSubscription
    ```

2. <span data-ttu-id="38662-217">Para armazenar os parâmetros, crie uma variável complexa usando o mesmo nome do plano de recuperação:</span><span class="sxs-lookup"><span data-stu-id="38662-217">To store the parameters, create the complex variable by using the name of the recovery plan:</span></span>

    ```
    $VMDetails = @{"VMGUID"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"};"VMGUID2"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"}}
        New-AzureRmAutomationVariable -ResourceGroupName <RG of Automation Account> -AutomationAccountName <AA Name> -Name <RecoveryPlanName> -Value $VMDetails -Encrypted $false
    ```

3. <span data-ttu-id="38662-218">Nessa variável complexa, **VMDetails** é a ID de VM da VM protegida.</span><span class="sxs-lookup"><span data-stu-id="38662-218">In this complex variable, **VMDetails** is the VM ID for the protected VM.</span></span> <span data-ttu-id="38662-219">Para obter a ID de VM, no portal do Azure, exiba as propriedades da VM.</span><span class="sxs-lookup"><span data-stu-id="38662-219">To get the VM ID, in the Azure portal, view the VM properties.</span></span> <span data-ttu-id="38662-220">A seguinte captura de tela mostra uma variável que armazena os detalhes de duas VMs:</span><span class="sxs-lookup"><span data-stu-id="38662-220">The following screenshot shows a variable that stores the details of two VMs:</span></span>

    ![Usar a ID de VM como o GUID](media/site-recovery-runbook-automation-new/vmguid.png)

4. <span data-ttu-id="38662-222">Use essa variável no runbook.</span><span class="sxs-lookup"><span data-stu-id="38662-222">Use this variable in your runbook.</span></span> <span data-ttu-id="38662-223">Se o GUID de VM indicado for encontrado no contexto do plano de recuperação, aplique o NSG à VM:</span><span class="sxs-lookup"><span data-stu-id="38662-223">If the indicated VM GUID is found in the recovery plan context, apply the NSG on the VM:</span></span>

    ```
    $VMDetailsObj = Get-AutomationVariable -Name $RecoveryPlanContext.RecoveryPlanName
    ```

4. <span data-ttu-id="38662-224">No runbook, percorra as VMs do contexto do plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="38662-224">In your runbook, loop through the VMs of the recovery plan context.</span></span> <span data-ttu-id="38662-225">Verifique se a VM existe em **$VMDetailsObj**.</span><span class="sxs-lookup"><span data-stu-id="38662-225">Check whether the VM exists in **$VMDetailsObj**.</span></span> <span data-ttu-id="38662-226">Se ela existir, acesse as propriedades da variável para aplicar o NSG:</span><span class="sxs-lookup"><span data-stu-id="38662-226">If it exists, access the properties of the variable to apply the NSG:</span></span>

    ```
        $VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
        $vmMap = $RecoveryPlanContext.VmMap

        foreach($VMID in $VMinfo) {
            Write-output $VMDetailsObj.value.$VMID

            if ($VMDetailsObj.value.$VMID -ne $Null) { #If the VM exists in the context, this will not b Null
                $VM = $vmMap.$VMID
                # Access the properties of the variable
                $NSGname = $VMDetailsObj.value.$VMID.'NSGName'
                $NSGRGname = $VMDetailsObj.value.$VMID.'NSGResourceGroupName'

                # Add code to apply the NSG properties to the VM
            }
        }
    ```

<span data-ttu-id="38662-227">Use o mesmo script para planos de recuperação diferentes.</span><span class="sxs-lookup"><span data-stu-id="38662-227">You can use the same script for different recovery plans.</span></span> <span data-ttu-id="38662-228">Insira parâmetros diferentes armazenando o valor que corresponde a um plano de recuperação em variáveis diferentes.</span><span class="sxs-lookup"><span data-stu-id="38662-228">Enter different parameters by storing the value that corresponds to a recovery plan in different variables.</span></span>

## <a name="sample-scripts"></a><span data-ttu-id="38662-229">Exemplos de scripts</span><span class="sxs-lookup"><span data-stu-id="38662-229">Sample scripts</span></span>

<span data-ttu-id="38662-230">Para implantar scripts de exemplo em sua conta de Automação, clique no botão **Implantar no Azure**.</span><span class="sxs-lookup"><span data-stu-id="38662-230">To deploy sample scripts to your Automation account, click the **Deploy to Azure** button.</span></span>

<span data-ttu-id="38662-231">[![Implantar no Azure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span><span class="sxs-lookup"><span data-stu-id="38662-231">[![Deploy to Azure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span></span>

<span data-ttu-id="38662-232">Para obter outro exemplo, assista ao vídeo a seguir.</span><span class="sxs-lookup"><span data-stu-id="38662-232">For another example, see the following video.</span></span> <span data-ttu-id="38662-233">Ele demonstra como recuperar um aplicativo do WordPress de duas camadas no Azure:</span><span class="sxs-lookup"><span data-stu-id="38662-233">It demonstrates how to recover a two-tier WordPress application to Azure:</span></span>


> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/One-click-failover-of-a-2-tier-WordPress-application-using-Azure-Site-Recovery/player]



## <a name="additional-resources"></a><span data-ttu-id="38662-234">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="38662-234">Additional resources</span></span>
* [<span data-ttu-id="38662-235">Conta Executar como do serviço de Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="38662-235">Azure Automation service Run As account</span></span>](../automation/automation-sec-configure-azure-runas-account.md)
* [<span data-ttu-id="38662-236">Visão geral da Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="38662-236">Azure Automation overview</span></span>](http://msdn.microsoft.com/library/azure/dn643629.aspx "Visão geral da Automação do Azure")
* [<span data-ttu-id="38662-237">Scripts de exemplo da Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="38662-237">Azure Automation sample scripts</span></span>](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Scripts de exemplo da Automação do Azure")
