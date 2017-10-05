---
title: Usar marcas formatada em JSON para agendar o estado da VM do Azure | Microsoft Docs
description: "Este artigo demonstra como usar cadeias de caracteres JSON em marcações para automatizar o agendamento do desligamento e inicialização de VM."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 6afed5d2-e939-4749-8b2c-9312b4c16fb2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: magoedte;paulomarquesc
ms.openlocfilehash: f8d9563318c3afe299cebb7c889874392f114f84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario-using-json-formatted-tags-to-create-a-schedule-for-azure-vm-startup-and-shutdown"></a><span data-ttu-id="8aa99-103">Cenário de Automação do Azure: usando marcações formatadas JSON para criar um agendamento para inicialização e desligamento de VM do Azure</span><span class="sxs-lookup"><span data-stu-id="8aa99-103">Azure Automation scenario: Using JSON-formatted tags to create a schedule for Azure VM startup and shutdown</span></span>
<span data-ttu-id="8aa99-104">Muitas vezes, os clientes desejam agendar a inicialização e desligamento de máquinas virtuais para ajudar a reduzir os custos de assinatura ou dar suporte a requisitos técnicos e de negócios.</span><span class="sxs-lookup"><span data-stu-id="8aa99-104">Customers often want to schedule the startup and shutdown of virtual machines to help reduce subscription costs or support business and technical requirements.</span></span>

<span data-ttu-id="8aa99-105">O cenário a seguir permite a você configurar a inicialização e o desligamento automatizados de suas VMs usando uma marcação chamada de Agendamento no nível do grupo de recursos ou da máquina virtual no Azure.</span><span class="sxs-lookup"><span data-stu-id="8aa99-105">The following scenario enables you to set up automated startup and shutdown of your VMs by using a tag called Schedule at a resource group level or virtual machine level in Azure.</span></span> <span data-ttu-id="8aa99-106">Esse agendamento pode ser configurado de domingo a sábado com hora de inicialização e de desligamento.</span><span class="sxs-lookup"><span data-stu-id="8aa99-106">This schedule can be configured from Sunday to Saturday with a startup time and shutdown time.</span></span>

<span data-ttu-id="8aa99-107">Temos algumas opções imediatas.</span><span class="sxs-lookup"><span data-stu-id="8aa99-107">We do have some out-of-the-box options.</span></span> <span data-ttu-id="8aa99-108">Estão incluídos:</span><span class="sxs-lookup"><span data-stu-id="8aa99-108">These include:</span></span>

* <span data-ttu-id="8aa99-109">[Conjuntos de escala de máquina Virtual](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) com configurações de dimensionamento automático que permitem a você escalar ou reduzir horizontalmente.</span><span class="sxs-lookup"><span data-stu-id="8aa99-109">[Virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) with autoscale settings that enable you to scale in or out.</span></span>
* <span data-ttu-id="8aa99-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) , que tem o recurso interno de agendamento de operações de inicialização e desligamento.</span><span class="sxs-lookup"><span data-stu-id="8aa99-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) service, which has the built-in capability of scheduling startup and shutdown operations.</span></span>

<span data-ttu-id="8aa99-111">No entanto, essas opções dão suporte somente a cenários específicos e não podem ser aplicadas às VMs de IaaS (infraestrutura como serviço).</span><span class="sxs-lookup"><span data-stu-id="8aa99-111">However, these options only support specific scenarios and cannot be applied to infrastructure-as-a-service (IaaS) VMs.</span></span>

<span data-ttu-id="8aa99-112">Quando a marcação Agendamento for aplicada a um grupo de recursos, ela também será aplicada a todas as máquinas virtuais dentro daquele grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8aa99-112">When the Schedule tag is applied to a resource group, it's also applied to all virtual machines inside that resource group.</span></span> <span data-ttu-id="8aa99-113">Se um agendamento também for aplicado diretamente a uma VM, o último agendamento terá precedência na seguinte ordem:</span><span class="sxs-lookup"><span data-stu-id="8aa99-113">If a schedule is also directly applied to a VM, the last schedule takes precedence in the following order:</span></span>

1. <span data-ttu-id="8aa99-114">Agendamento aplicado a um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="8aa99-114">Schedule applied to a resource group</span></span>
2. <span data-ttu-id="8aa99-115">Agendamento aplicado a um grupo de recursos e à máquina virtual no grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="8aa99-115">Schedule applied to a resource group and virtual machine in the resource group</span></span>
3. <span data-ttu-id="8aa99-116">Agendamento aplicado a uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="8aa99-116">Schedule applied to a virtual machine</span></span>

<span data-ttu-id="8aa99-117">Essencialmente, esse cenário usa uma cadeia de caracteres JSON com um formato especificado e a adiciona como um valor de uma marcação chamada Agendamento.</span><span class="sxs-lookup"><span data-stu-id="8aa99-117">This scenario essentially takes a JSON string with a specified format and adds it as the value for a tag called Schedule.</span></span> <span data-ttu-id="8aa99-118">Em seguida, um runbook lista todos os grupos de recursos e máquinas virtuais e identifica as agendas para cada VM com base nos cenários listados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8aa99-118">Then a runbook lists all resource groups and virtual machines and identifies the schedules for each VM based on the scenarios listed earlier.</span></span> <span data-ttu-id="8aa99-119">Em seguida, ele percorre as VMs que têm agendas anexadas e avalia a ação que deve ser executada.</span><span class="sxs-lookup"><span data-stu-id="8aa99-119">Next it loops through the VMs that have schedules attached and evaluates what action should be taken.</span></span> <span data-ttu-id="8aa99-120">Por exemplo, ele determina quais máquinas virtuais precisam ser interrompidas, desligadas ou ignoradas.</span><span class="sxs-lookup"><span data-stu-id="8aa99-120">For example, it determines which VMs need to be stopped, shut down, or ignored.</span></span>

<span data-ttu-id="8aa99-121">Esses runbooks são autenticados usando a [conta Run As do Azure](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="8aa99-121">These runbooks authenticate by using the [Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>

## <a name="download-the-runbooks-for-the-scenario"></a><span data-ttu-id="8aa99-122">Baixar os runbooks para o cenário</span><span class="sxs-lookup"><span data-stu-id="8aa99-122">Download the runbooks for the scenario</span></span>
<span data-ttu-id="8aa99-123">Este cenário consiste em quatro runbooks de Fluxo de Trabalho do PowerShell que podem ser baixados da [Galeria do TechNet](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) ou do repositório do [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) para esse projeto.</span><span class="sxs-lookup"><span data-stu-id="8aa99-123">This scenario consists of four PowerShell Workflow runbooks that you can download from the [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) or the [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) repository for this project.</span></span>

| <span data-ttu-id="8aa99-124">Runbook</span><span class="sxs-lookup"><span data-stu-id="8aa99-124">Runbook</span></span> | <span data-ttu-id="8aa99-125">Descrição</span><span class="sxs-lookup"><span data-stu-id="8aa99-125">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8aa99-126">Test-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="8aa99-126">Test-ResourceSchedule</span></span> |<span data-ttu-id="8aa99-127">Verifica cada agenda de máquina virtual e executa o desligamento ou inicialização, dependendo do agendamento.</span><span class="sxs-lookup"><span data-stu-id="8aa99-127">Checks each virtual machine schedule and performs shutdown or startup depending on the schedule.</span></span> |
| <span data-ttu-id="8aa99-128">Add-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="8aa99-128">Add-ResourceSchedule</span></span> |<span data-ttu-id="8aa99-129">Adiciona a marcação Agendamento a uma VM ou grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8aa99-129">Adds the Schedule tag to a VM or resource group.</span></span> |
| <span data-ttu-id="8aa99-130">Update-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="8aa99-130">Update-ResourceSchedule</span></span> |<span data-ttu-id="8aa99-131">Modifica a marcação Agendamento existente substituindo-a por uma nova.</span><span class="sxs-lookup"><span data-stu-id="8aa99-131">Modifies the existing Schedule tag by replacing it with a new one.</span></span> |
| <span data-ttu-id="8aa99-132">Remove-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="8aa99-132">Remove-ResourceSchedule</span></span> |<span data-ttu-id="8aa99-133">Remove a marcação Agendamento de uma VM ou grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8aa99-133">Removes the Schedule tag from a VM or resource group.</span></span> |

## <a name="install-and-configure-this-scenario"></a><span data-ttu-id="8aa99-134">Instalar e configurar esse cenário</span><span class="sxs-lookup"><span data-stu-id="8aa99-134">Install and configure this scenario</span></span>
### <a name="install-and-publish-the-runbooks"></a><span data-ttu-id="8aa99-135">Instalar e publicar os runbooks</span><span class="sxs-lookup"><span data-stu-id="8aa99-135">Install and publish the runbooks</span></span>
<span data-ttu-id="8aa99-136">Depois de baixar os runbooks, você poderá importá-los usando o procedimento em [Criando ou importando um runbook na Automação do Azure](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).</span><span class="sxs-lookup"><span data-stu-id="8aa99-136">After downloading the runbooks, you can import them by using the procedure in [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).</span></span>  <span data-ttu-id="8aa99-137">Publica cada runbook depois que ele é importado com êxito para sua conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="8aa99-137">Publish each runbook after it has been successfully imported into your Automation account.</span></span>

### <a name="add-a-schedule-to-the-test-resourceschedule-runbook"></a><span data-ttu-id="8aa99-138">Adicionar uma agenda ao runbook Test-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="8aa99-138">Add a schedule to the Test-ResourceSchedule runbook</span></span>
<span data-ttu-id="8aa99-139">Siga estas etapas para habilitar o agendamento para o runbook Test-ResourceSchedule.</span><span class="sxs-lookup"><span data-stu-id="8aa99-139">Follow these steps to enable the schedule for the Test-ResourceSchedule runbook.</span></span> <span data-ttu-id="8aa99-140">Esse é o runbook que verifica quais máquinas virtuais devem ser iniciadas, desligadas ou deixadas como estão.</span><span class="sxs-lookup"><span data-stu-id="8aa99-140">This is the runbook that verifies which virtual machines should be started, shut down, or left as is.</span></span>

1. <span data-ttu-id="8aa99-141">No portal do Azure, abra sua conta da Automação e clique no bloco **Runbooks** .</span><span class="sxs-lookup"><span data-stu-id="8aa99-141">From the Azure portal, open your Automation account, and then click the **Runbooks** tile.</span></span>
2. <span data-ttu-id="8aa99-142">Na folha **Test-ResourceSchedule**, clique no bloco **Agendamentos**.</span><span class="sxs-lookup"><span data-stu-id="8aa99-142">On the **Test-ResourceSchedule** blade, click the **Schedules** tile.</span></span>
3. <span data-ttu-id="8aa99-143">Na folha **Agendamentos**, clique em **Adicionar um agendamento**.</span><span class="sxs-lookup"><span data-stu-id="8aa99-143">On the **Schedules** blade, click **Add a schedule**.</span></span>
4. <span data-ttu-id="8aa99-144">Na folha **Agendamentos**, selecione **Associar um agendamento ao runbook**.</span><span class="sxs-lookup"><span data-stu-id="8aa99-144">On the **Schedules** blade, select **Link a schedule to your runbook**.</span></span> <span data-ttu-id="8aa99-145">Em seguida, selecione **Criar um nova agendamento**.</span><span class="sxs-lookup"><span data-stu-id="8aa99-145">Then select **Create a new schedule**.</span></span>
5. <span data-ttu-id="8aa99-146">Na folha **Nova agenda** , digite o nome dela, por exemplo: *HourlyExecution*.</span><span class="sxs-lookup"><span data-stu-id="8aa99-146">On the **New schedule** blade, type in the name of this schedule, for example: *HourlyExecution*.</span></span>
6. <span data-ttu-id="8aa99-147">Para o **Início**do agendamento, defina a hora de início como um incremento de hora.</span><span class="sxs-lookup"><span data-stu-id="8aa99-147">For the schedule **Start**, set the start time to an hour increment.</span></span>
7. <span data-ttu-id="8aa99-148">Selecione **Recorrência** e em **Repetir a cada intervalo**, selecione **1 hora**.</span><span class="sxs-lookup"><span data-stu-id="8aa99-148">Select **Recurrence**, and then for **Recur every interval**, select **1 hour**.</span></span>
8. <span data-ttu-id="8aa99-149">Verifique se **Definir expiração** está definido como **Não** e clique em **Criar** para salvar seu novo agendamento.</span><span class="sxs-lookup"><span data-stu-id="8aa99-149">Verify that **Set expiration** is set to **No**, and then click **Create** to save your new schedule.</span></span>
9. <span data-ttu-id="8aa99-150">Na folha de opções **Agendar Runbook**, selecione **Definições de parâmetros e de execução**.</span><span class="sxs-lookup"><span data-stu-id="8aa99-150">On the **Schedule Runbook** options blade, select **Parameters and run settings**.</span></span> <span data-ttu-id="8aa99-151">Na folha Test-ResourceSchedule **Parâmetros**, insira o nome da sua assinatura no campo **SubscriptionName**.</span><span class="sxs-lookup"><span data-stu-id="8aa99-151">In the Test-ResourceSchedule **Parameters** blade, enter the name of your subscription in the **SubscriptionName** field.</span></span>  <span data-ttu-id="8aa99-152">Esse é o único parâmetro necessário para o runbook.</span><span class="sxs-lookup"><span data-stu-id="8aa99-152">This is the only parameter that's required for the runbook.</span></span>  <span data-ttu-id="8aa99-153">Quando tiver terminado, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="8aa99-153">When you're finished, click **OK**.</span></span>

<span data-ttu-id="8aa99-154">O agendamento de runbook deverá parecer com o seguinte quando concluído:</span><span class="sxs-lookup"><span data-stu-id="8aa99-154">The runbook schedule should look like the following when it's completed:</span></span>

![Runbook de Test-ResourceSchedule configurado](./media/automation-scenario-start-stop-vm-wjson-tags/automation-schedule-config.png)<br>

## <a name="format-the-json-string"></a><span data-ttu-id="8aa99-156">Formatar cadeia de caracteres JSON</span><span class="sxs-lookup"><span data-stu-id="8aa99-156">Format the JSON string</span></span>
<span data-ttu-id="8aa99-157">Essa solução basicamente usa uma cadeia de caracteres JSON com um formato especificado e adiciona-a como um valor de uma marcação chamada Agendamento.</span><span class="sxs-lookup"><span data-stu-id="8aa99-157">This solution basically takes a JSON string with a specified format and adds it as the value for a tag called Schedule.</span></span> <span data-ttu-id="8aa99-158">Em seguida, um runbook lista todos os grupos de recursos e máquinas virtuais e identifica os agendamentos para cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8aa99-158">Then a runbook lists all resource groups and virtual machines and identifies the schedules for each virtual machine.</span></span>

<span data-ttu-id="8aa99-159">O runbook faz um loop sobre as máquinas virtuais que possuem agendas anexadas e verifica quais ações devem ser executadas.</span><span class="sxs-lookup"><span data-stu-id="8aa99-159">The runbook loops over the virtual machines that have schedules attached and checks what actions should be taken.</span></span> <span data-ttu-id="8aa99-160">Veja um exemplo abaixo de como as soluções devem ser formatadas:</span><span class="sxs-lookup"><span data-stu-id="8aa99-160">The following is an example of how the solutions should be formatted:</span></span>

```json
{
    "TzId": "Eastern Standard Time",
    "0": {
        "S": "11",
        "E": "17"
    },
    "1": {
        "S": "9",
        "E": "19"
    },
    "2": {
        "S": "9",
        "E": "19"
    },
}
```

<span data-ttu-id="8aa99-161">Veja algumas informações detalhadas sobre esta estrutura:</span><span class="sxs-lookup"><span data-stu-id="8aa99-161">Here is some detailed information about this structure:</span></span>

1. <span data-ttu-id="8aa99-162">O formato dessa estrutura JSON é otimizado para contornar a limitação de 256 caracteres de um valor de marcação única no Azure.</span><span class="sxs-lookup"><span data-stu-id="8aa99-162">The format of this JSON structure is optimized to work around the 256-character limitation of a single tag value in Azure.</span></span>
2. <span data-ttu-id="8aa99-163">*TzId* representa o fuso horário da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8aa99-163">*TzId* represents the time zone of the virtual machine.</span></span> <span data-ttu-id="8aa99-164">Essa ID pode ser obtida usando a classe .NET TimeZoneInfo em uma sessão do PowerShell -**[System.TimeZoneInfo]:: GetSystemTimeZones()**.</span><span class="sxs-lookup"><span data-stu-id="8aa99-164">This ID can be obtained by using the TimeZoneInfo .NET class in a PowerShell session--**[System.TimeZoneInfo]::GetSystemTimeZones()**.</span></span>

   ![GetSystemTimeZones no PowerShell](./media/automation-scenario-start-stop-vm-wjson-tags/automation-get-timzone-powershell.png)

   * <span data-ttu-id="8aa99-166">Dias da semana são representados com um valor numérico de zero a seis.</span><span class="sxs-lookup"><span data-stu-id="8aa99-166">Weekdays are represented with a numeric value of zero to six.</span></span> <span data-ttu-id="8aa99-167">O valor zero é igual a domingo.</span><span class="sxs-lookup"><span data-stu-id="8aa99-167">The value zero equals Sunday.</span></span>
   * <span data-ttu-id="8aa99-168">A hora de início é representada pelo atributo **S** e seu valor está no formato de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="8aa99-168">The start time is represented with the **S** attribute, and its value is in a 24-hour format.</span></span>
   * <span data-ttu-id="8aa99-169">A hora de término é representada pelo atributo **E** e seu valor está no formato de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="8aa99-169">The end or shutdown time is represented with the **E** attribute, and its value is in a 24-hour format.</span></span>

     <span data-ttu-id="8aa99-170">Se os atributos **S** e **E** tiverem o valor zero (0), a máquina virtual será deixada em seu estado atual no momento da avaliação.</span><span class="sxs-lookup"><span data-stu-id="8aa99-170">If the **S** and **E** attributes each have a value of zero (0), the virtual machine will be left in its present state at the time of evaluation.</span></span>
3. <span data-ttu-id="8aa99-171">Se você quiser ignorar a avaliação de um dia específico da semana, não adicione uma seção para esse dia da semana.</span><span class="sxs-lookup"><span data-stu-id="8aa99-171">If you want to skip evaluation for a specific day of the week, don’t add a section for that day of the week.</span></span> <span data-ttu-id="8aa99-172">No exemplo abaixo, apenas a segunda-feira é avaliada; os outros dias da semana são ignorados:</span><span class="sxs-lookup"><span data-stu-id="8aa99-172">In the following example, only Monday is evaluated, and the other days of the week are ignored:</span></span>

    ```json
    {
        "TzId": "Eastern Standard Time",
        "1": {
            "S": "11",
            "E": "17"
        }
    }
    ```

## <a name="tag-resource-groups-or-vms"></a><span data-ttu-id="8aa99-173">Marcar grupos de recursos ou VMs</span><span class="sxs-lookup"><span data-stu-id="8aa99-173">Tag resource groups or VMs</span></span>
<span data-ttu-id="8aa99-174">Para desligar as VMs, você precisa marcar as VMs ou os grupos de recursos nos quais elas estão localizadas.</span><span class="sxs-lookup"><span data-stu-id="8aa99-174">To shut down VMs, you need to tag either the VMs or the resource groups in which they're located.</span></span> <span data-ttu-id="8aa99-175">Máquinas virtuais que não têm uma marcação de Agenda não são avaliadas.</span><span class="sxs-lookup"><span data-stu-id="8aa99-175">Virtual machines that don't have a Schedule tag are not evaluated.</span></span> <span data-ttu-id="8aa99-176">Portanto, elas não iniciadas ou desligadas.</span><span class="sxs-lookup"><span data-stu-id="8aa99-176">Therefore, they aren't started or shut down.</span></span>

<span data-ttu-id="8aa99-177">Há duas maneiras de marcar grupos de recursos ou VMs com essa solução.</span><span class="sxs-lookup"><span data-stu-id="8aa99-177">There are two ways to tag resource groups or VMs with this solution.</span></span> <span data-ttu-id="8aa99-178">Você pode fazer isso diretamente do portal.</span><span class="sxs-lookup"><span data-stu-id="8aa99-178">You can do it directly from the portal.</span></span> <span data-ttu-id="8aa99-179">Ou pode usar os runbooks Add-ResourceSchedule, Update-ResourceSchedule de e Remove-ResourceSchedule.</span><span class="sxs-lookup"><span data-stu-id="8aa99-179">Or you can use the Add-ResourceSchedule, Update-ResourceSchedule, and Remove-ResourceSchedule runbooks.</span></span>

### <a name="tag-through-the-portal"></a><span data-ttu-id="8aa99-180">Marcar pelo portal</span><span class="sxs-lookup"><span data-stu-id="8aa99-180">Tag through the portal</span></span>
<span data-ttu-id="8aa99-181">Siga estas etapas para marcar uma máquina virtual ou um grupo de recursos no portal:</span><span class="sxs-lookup"><span data-stu-id="8aa99-181">Follow these steps to tag a virtual machine or resource group in the portal:</span></span>

1. <span data-ttu-id="8aa99-182">Nivele a cadeia de caracteres JSON e verifique se não há espaços.</span><span class="sxs-lookup"><span data-stu-id="8aa99-182">Flatten the JSON string and verify that there aren't any spaces.</span></span>  <span data-ttu-id="8aa99-183">A cadeia de caracteres JSON deve ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="8aa99-183">Your JSON string should look like this:</span></span>

    ```json
    {"TzId":"Eastern Standard Time","0":{"S":"11","E":"17"},"1":{"S":"9","E":"19"},"2": {"S":"9","E":"19"},"3":{"S":"9","E":"19"},"4":{"S":"9","E":"19"},"5":{"S":"9","E":"19"},"6":{"S":"11","E":"17"}}
    ```

2. <span data-ttu-id="8aa99-184">Selecione o ícone **Marcação** de uma VM ou um grupo de recursos para aplicar este agendamento.</span><span class="sxs-lookup"><span data-stu-id="8aa99-184">Select the **Tag** icon for a VM or resource group to apply this schedule.</span></span>

   ![Opção de marcação de VM](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-tag-option.png)

3. <span data-ttu-id="8aa99-186">As marcas são definidas seguindo um par chave/valor.</span><span class="sxs-lookup"><span data-stu-id="8aa99-186">Tags are defined following a key/value pair.</span></span> <span data-ttu-id="8aa99-187">Digite **Agendamento** no campo **Chave** e cole a cadeia de caracteres JSON no campo **Valor**.</span><span class="sxs-lookup"><span data-stu-id="8aa99-187">Type **Schedule** in the **Key** field, and then paste the JSON string into the **Value** field.</span></span> <span data-ttu-id="8aa99-188">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="8aa99-188">Click **Save**.</span></span> <span data-ttu-id="8aa99-189">Agora, a nova marca deve aparecer na lista de marcas do seu recurso.</span><span class="sxs-lookup"><span data-stu-id="8aa99-189">Your new tag should now appear in the list of tags for your resource.</span></span>

   ![Marcação de agendamento de VM](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-schedule-tag.png)

### <a name="tag-from-powershell"></a><span data-ttu-id="8aa99-191">Marcar do PowerShell</span><span class="sxs-lookup"><span data-stu-id="8aa99-191">Tag from PowerShell</span></span>
<span data-ttu-id="8aa99-192">Todos os runbooks importados contém informações de Ajuda no início do script para descrever como executar runbooks diretamente do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8aa99-192">All imported runbooks contain help information at the beginning of the script that describes how to execute the runbooks directly from PowerShell.</span></span> <span data-ttu-id="8aa99-193">Você pode chamar os runbooks Add-ScheduleResource e Update-ScheduleResource do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8aa99-193">You can call the Add-ScheduleResource and Update-ScheduleResource runbooks from PowerShell.</span></span> <span data-ttu-id="8aa99-194">Você pode fazer isso transmitindo parâmetros necessários que permitem a você criar ou atualizar a marcação de Agendamento em uma VM ou em um grupo de recursos fora do portal.</span><span class="sxs-lookup"><span data-stu-id="8aa99-194">You do this by passing required parameters that enable you to create or update the Schedule tag on a VM or resource group outside of the portal.</span></span>

<span data-ttu-id="8aa99-195">Para criar, adicionar e excluir marcações pelo PowerShell, primeiramente você precisa [configurar seu ambiente do PowerShell para o Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8aa99-195">To create, add, and delete tags through PowerShell, you first need to [set up your PowerShell environment for Azure](/powershell/azure/overview).</span></span> <span data-ttu-id="8aa99-196">Depois de concluir a instalação, você poderá continuar com as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="8aa99-196">After you complete the setup, you can proceed with the following steps.</span></span>

### <a name="create-a-schedule-tag-with-powershell"></a><span data-ttu-id="8aa99-197">Criar uma marcação de agendamento com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="8aa99-197">Create a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="8aa99-198">Abra uma sessão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8aa99-198">Open a PowerShell session.</span></span> <span data-ttu-id="8aa99-199">Em seguida, use o exemplo abaixo para autenticar com sua conta Executar como e para especificar uma assinatura:</span><span class="sxs-lookup"><span data-stu-id="8aa99-199">Then use the following example to authenticate with your Run As account and to specify a subscription:</span></span>

    ```powershell
    $Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="8aa99-200">Defina uma tabela de hash de agendamento.</span><span class="sxs-lookup"><span data-stu-id="8aa99-200">Define a schedule hash table.</span></span> <span data-ttu-id="8aa99-201">Aqui está um exemplo de como deve ser criado:</span><span class="sxs-lookup"><span data-stu-id="8aa99-201">Here is an example of how it should be constructed:</span></span>

    ```powershell
    $schedule= @{ "TzId"="Eastern Standard Time"; "0"= @{"S"="11";"E"="17"};"1"= @{"S"="9";"E"="19"};"2"= @{"S"="9";"E"="19"};"3"= @{"S"="9";"E"="19"};"4"= @{"S"="9";"E"="19"};"5"= @{"S"="9";"E"="19"};"6"= @{"S"="11";"E"="17"}}
    ```

3. <span data-ttu-id="8aa99-202">Defina os parâmetros exigidos para o runbook.</span><span class="sxs-lookup"><span data-stu-id="8aa99-202">Define the parameters that are required by the runbook.</span></span> <span data-ttu-id="8aa99-203">O exemplo a seguir destina-se a uma VM:</span><span class="sxs-lookup"><span data-stu-id="8aa99-203">In the following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "VmName"="VM01";"Schedule"=$schedule}
    ```

    <span data-ttu-id="8aa99-204">Se você estiver marcando um grupo de recursos, remova o parâmetro *VMName* da tabela de hash $params da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="8aa99-204">If you’re tagging a resource group, remove the *VMName* parameter from the $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "Schedule"=$schedule}
    ```

4. <span data-ttu-id="8aa99-205">Execute o runbook Add-ResourceSchedule com os seguintes parâmetros para criar a marcação Agendamento:</span><span class="sxs-lookup"><span data-stu-id="8aa99-205">Run the Add-ResourceSchedule runbook with the following parameters to create the Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Add-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

5. <span data-ttu-id="8aa99-206">Para atualizar um grupo de recursos ou marcação de máquina virtual, execute o runbook **Update-ResourceSchedule** com os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="8aa99-206">To update a resource group or virtual machine tag, execute the **Update-ResourceSchedule** runbook with the following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Update-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

### <a name="remove-a-schedule-tag-with-powershell"></a><span data-ttu-id="8aa99-207">Remover uma marcação de agendamento com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="8aa99-207">Remove a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="8aa99-208">Abra uma sessão do PowerShell e execute o seguinte para autenticar com sua conta Executar como, selecionar e especificar uma assinatura:</span><span class="sxs-lookup"><span data-stu-id="8aa99-208">Open a PowerShell session and run the following to authenticate with your Run As account and to select and specify a subscription:</span></span>

    ```powershell
    Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="8aa99-209">Defina os parâmetros exigidos para o runbook.</span><span class="sxs-lookup"><span data-stu-id="8aa99-209">Define the parameters that are required by the runbook.</span></span> <span data-ttu-id="8aa99-210">O exemplo a seguir destina-se a uma VM:</span><span class="sxs-lookup"><span data-stu-id="8aa99-210">In the following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01";"VmName"="VM01"}
    ```

    <span data-ttu-id="8aa99-211">Se você estiver removendo uma marcação de um grupo de recursos, remova o parâmetro *VMName* da tabela de hash $params da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="8aa99-211">If you’re removing a tag from a resource group, remove the *VMName* parameter from the $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"}
    ```

3. <span data-ttu-id="8aa99-212">Execute o runbook Remove-ResourceSchedule para remover a marcação Agendamento:</span><span class="sxs-lookup"><span data-stu-id="8aa99-212">Execute the Remove-ResourceSchedule runbook to remove the Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

4. <span data-ttu-id="8aa99-213">Para atualizar um grupo de recursos ou marcação de máquina virtual, execute o runbook Remove-ResourceSchedule com os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="8aa99-213">To update a resource group or virtual machine tag, execute the Remove-ResourceSchedule runbook with the following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

> [!NOTE]
> <span data-ttu-id="8aa99-214">Recomendamos monitorar proativamente esses runbooks (e o estado da máquina virtual) para verificar se as máquinas virtuais estão sendo devidamente encerradas e iniciadas.</span><span class="sxs-lookup"><span data-stu-id="8aa99-214">We recommend that you proactively monitor these runbooks (and the virtual machine states) to verify that your virtual machines are being shut down and started accordingly.</span></span>
>

<span data-ttu-id="8aa99-215">Para exibir os detalhes do trabalho do runbook Test-ResourceSchedule no Portal do Azure, selecione o bloco **Trabalhos** do runbook.</span><span class="sxs-lookup"><span data-stu-id="8aa99-215">To view the details of the Test-ResourceSchedule runbook job in the Azure portal, select the **Jobs** tile of the runbook.</span></span> <span data-ttu-id="8aa99-216">O resumo do trabalho exibe os parâmetros de entrada e o fluxo de saída, além de informações gerais sobre o trabalho e todas as exceções, caso tenham ocorrido.</span><span class="sxs-lookup"><span data-stu-id="8aa99-216">The job summary displays the input parameters and the output stream, in addition to general information about the job and any exceptions if they occurred.</span></span>

<span data-ttu-id="8aa99-217">O **Resumo do Trabalho** inclui mensagens de fluxos de saída, de aviso e de erro.</span><span class="sxs-lookup"><span data-stu-id="8aa99-217">The **Job Summary** includes messages from the output, warning, and error streams.</span></span> <span data-ttu-id="8aa99-218">Selecione o bloco de **Saída** para exibir os resultados detalhados da execução do runbook.</span><span class="sxs-lookup"><span data-stu-id="8aa99-218">Select the **Output** tile to view detailed results from the runbook execution.</span></span>

![Saída do Test-ResourceSchedule](./media/automation-scenario-start-stop-vm-wjson-tags/automation-job-output.png)

## <a name="next-steps"></a><span data-ttu-id="8aa99-220">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8aa99-220">Next steps</span></span>
* <span data-ttu-id="8aa99-221">Para começar a usar os runbooks do fluxo de trabalho do PowerShell, veja [Meu primeiro runbook do fluxo de trabalho do PowerShell](automation-first-runbook-textual.md).</span><span class="sxs-lookup"><span data-stu-id="8aa99-221">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md).</span></span>
* <span data-ttu-id="8aa99-222">Para aprender mais sobre os tipos de runbook, suas vantagens e limitações, veja [Tipos de runbook da Automação do Azure](automation-runbook-types.md).</span><span class="sxs-lookup"><span data-stu-id="8aa99-222">To learn more about runbook types, and their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md).</span></span>
* <span data-ttu-id="8aa99-223">Para saber mais sobre o recurso de suporte a scripts do PowerShell, veja [Suporte a scripts nativos do PowerShell na Automação do Azure](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/).</span><span class="sxs-lookup"><span data-stu-id="8aa99-223">For more information about PowerShell script support features, see [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/).</span></span>
* <span data-ttu-id="8aa99-224">Para saber mais sobre o registro em log de runbook e de saída, consulte [Saída e mensagens de runbook na Automação do Azure](automation-runbook-output-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="8aa99-224">To learn more about runbook logging and output, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md).</span></span>
* <span data-ttu-id="8aa99-225">Para saber mais sobre uma conta Run As do Azure e como autenticar seus runbooks usando essa conta, consulte [Autenticar runbooks com a conta Run As do Azure](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="8aa99-225">To learn more about an Azure Run As account and how to authenticate your runbooks by using it, see [Authenticate runbooks with Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>
