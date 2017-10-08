---
title: aaaUse estado de VM do Azure tooschedule marcas formatada em JSON | Microsoft Docs
description: "Este artigo demonstra como toouse JSON cadeias de caracteres em marcas tooautomate Olá agendamento do desligamento e a reinicialização VM."
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
ms.openlocfilehash: f6bbf1dea1c193e5d1010f12f3b1ed63562f9daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario-using-json-formatted-tags-toocreate-a-schedule-for-azure-vm-startup-and-shutdown"></a><span data-ttu-id="d1d03-103">Cenário de automação do Azure: usando o formato JSON marcas toocreate uma agenda para a VM do Azure inicialização e desligamento</span><span class="sxs-lookup"><span data-stu-id="d1d03-103">Azure Automation scenario: Using JSON-formatted tags toocreate a schedule for Azure VM startup and shutdown</span></span>
<span data-ttu-id="d1d03-104">Os clientes frequentemente querem tooschedule inicialização de saudação e reduzir os custos de assinatura de desligamento de máquinas virtuais toohelp ou dar suporte a requisitos comerciais e técnicos.</span><span class="sxs-lookup"><span data-stu-id="d1d03-104">Customers often want tooschedule hello startup and shutdown of virtual machines toohelp reduce subscription costs or support business and technical requirements.</span></span>

<span data-ttu-id="d1d03-105">Olá cenário a seguir permite que você tooset backup automatizado de inicialização e desligamento do suas VMs usando uma marca chamada agenda em nível de máquina virtual no Azure ou nível de grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d1d03-105">hello following scenario enables you tooset up automated startup and shutdown of your VMs by using a tag called Schedule at a resource group level or virtual machine level in Azure.</span></span> <span data-ttu-id="d1d03-106">Esta agenda pode ser configurada no domingo tooSaturday com um tempo de inicialização e o tempo de desligamento.</span><span class="sxs-lookup"><span data-stu-id="d1d03-106">This schedule can be configured from Sunday tooSaturday with a startup time and shutdown time.</span></span>

<span data-ttu-id="d1d03-107">Temos algumas opções imediatas.</span><span class="sxs-lookup"><span data-stu-id="d1d03-107">We do have some out-of-the-box options.</span></span> <span data-ttu-id="d1d03-108">Estão incluídos:</span><span class="sxs-lookup"><span data-stu-id="d1d03-108">These include:</span></span>

* <span data-ttu-id="d1d03-109">[Conjuntos de escala de máquina virtual](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) com configurações de dimensionamento automático que permitem que você tooscale in ou out.</span><span class="sxs-lookup"><span data-stu-id="d1d03-109">[Virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) with autoscale settings that enable you tooscale in or out.</span></span>
* <span data-ttu-id="d1d03-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) serviço, que tem o recurso interno de saudação do planejamento de operações de inicialização e desligamento.</span><span class="sxs-lookup"><span data-stu-id="d1d03-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) service, which has hello built-in capability of scheduling startup and shutdown operations.</span></span>

<span data-ttu-id="d1d03-111">No entanto, essas opções somente suportam a cenários específicos e não pode ser aplicado tooinfrastructure-como um serviço (IaaS) VMs.</span><span class="sxs-lookup"><span data-stu-id="d1d03-111">However, these options only support specific scenarios and cannot be applied tooinfrastructure-as-a-service (IaaS) VMs.</span></span>

<span data-ttu-id="d1d03-112">Quando Olá marca de agendamento for aplicado tooa grupo de recursos, também é aplicado tooall máquinas de virtuais dentro desse grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d1d03-112">When hello Schedule tag is applied tooa resource group, it's also applied tooall virtual machines inside that resource group.</span></span> <span data-ttu-id="d1d03-113">Se uma agenda também é aplicado diretamente tooa VM, o último agendamento de saudação tem precedência em Olá ordem a seguir:</span><span class="sxs-lookup"><span data-stu-id="d1d03-113">If a schedule is also directly applied tooa VM, hello last schedule takes precedence in hello following order:</span></span>

1. <span data-ttu-id="d1d03-114">Grupo de recursos do agendamento tooa aplicado</span><span class="sxs-lookup"><span data-stu-id="d1d03-114">Schedule applied tooa resource group</span></span>
2. <span data-ttu-id="d1d03-115">Agendar o grupo de recursos de tooa aplicado e a máquina virtual no grupo de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="d1d03-115">Schedule applied tooa resource group and virtual machine in hello resource group</span></span>
3. <span data-ttu-id="d1d03-116">Agendar a máquina virtual de tooa aplicado</span><span class="sxs-lookup"><span data-stu-id="d1d03-116">Schedule applied tooa virtual machine</span></span>

<span data-ttu-id="d1d03-117">Este cenário essencialmente usa uma cadeia de caracteres JSON com um formato especificado e o adiciona como valor Olá para uma marca chamada agenda.</span><span class="sxs-lookup"><span data-stu-id="d1d03-117">This scenario essentially takes a JSON string with a specified format and adds it as hello value for a tag called Schedule.</span></span> <span data-ttu-id="d1d03-118">Em seguida, um runbook lista todos os grupos de recursos e as máquinas virtuais e identifica agendas Olá para cada VM com base em cenários de saudação listados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d1d03-118">Then a runbook lists all resource groups and virtual machines and identifies hello schedules for each VM based on hello scenarios listed earlier.</span></span> <span data-ttu-id="d1d03-119">Em seguida, ele percorre Olá VMs que têm agendas anexadas e avalia a ação que deve ser executada.</span><span class="sxs-lookup"><span data-stu-id="d1d03-119">Next it loops through hello VMs that have schedules attached and evaluates what action should be taken.</span></span> <span data-ttu-id="d1d03-120">Por exemplo, ele determina que VMs precisam toobe parado, desligar ou ignorado.</span><span class="sxs-lookup"><span data-stu-id="d1d03-120">For example, it determines which VMs need toobe stopped, shut down, or ignored.</span></span>

<span data-ttu-id="d1d03-121">Esses runbooks autenticar usando Olá [conta executar como do Azure](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="d1d03-121">These runbooks authenticate by using hello [Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>

## <a name="download-hello-runbooks-for-hello-scenario"></a><span data-ttu-id="d1d03-122">Baixar runbooks Olá para o cenário de saudação</span><span class="sxs-lookup"><span data-stu-id="d1d03-122">Download hello runbooks for hello scenario</span></span>
<span data-ttu-id="d1d03-123">Este cenário consiste em quatro runbooks de fluxo de trabalho do PowerShell que você pode baixar do hello [Galeria do TechNet](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) ou hello [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) repositório para este projeto.</span><span class="sxs-lookup"><span data-stu-id="d1d03-123">This scenario consists of four PowerShell Workflow runbooks that you can download from hello [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) or hello [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) repository for this project.</span></span>

| <span data-ttu-id="d1d03-124">Runbook</span><span class="sxs-lookup"><span data-stu-id="d1d03-124">Runbook</span></span> | <span data-ttu-id="d1d03-125">Descrição</span><span class="sxs-lookup"><span data-stu-id="d1d03-125">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d1d03-126">Test-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="d1d03-126">Test-ResourceSchedule</span></span> |<span data-ttu-id="d1d03-127">Verifica cada agenda de máquina virtual e executa o desligamento ou inicialização dependendo da agenda de saudação.</span><span class="sxs-lookup"><span data-stu-id="d1d03-127">Checks each virtual machine schedule and performs shutdown or startup depending on hello schedule.</span></span> |
| <span data-ttu-id="d1d03-128">Add-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="d1d03-128">Add-ResourceSchedule</span></span> |<span data-ttu-id="d1d03-129">Adiciona Olá agenda marca tooa VM ou grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d1d03-129">Adds hello Schedule tag tooa VM or resource group.</span></span> |
| <span data-ttu-id="d1d03-130">Update-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="d1d03-130">Update-ResourceSchedule</span></span> |<span data-ttu-id="d1d03-131">Modifica a marca de agendamento existente Olá substituindo-o com um novo.</span><span class="sxs-lookup"><span data-stu-id="d1d03-131">Modifies hello existing Schedule tag by replacing it with a new one.</span></span> |
| <span data-ttu-id="d1d03-132">Remove-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="d1d03-132">Remove-ResourceSchedule</span></span> |<span data-ttu-id="d1d03-133">Remove a marca de agenda de saudação de um VM ou grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d1d03-133">Removes hello Schedule tag from a VM or resource group.</span></span> |

## <a name="install-and-configure-this-scenario"></a><span data-ttu-id="d1d03-134">Instalar e configurar esse cenário</span><span class="sxs-lookup"><span data-stu-id="d1d03-134">Install and configure this scenario</span></span>
### <a name="install-and-publish-hello-runbooks"></a><span data-ttu-id="d1d03-135">Instalar e publicar runbooks Olá</span><span class="sxs-lookup"><span data-stu-id="d1d03-135">Install and publish hello runbooks</span></span>
<span data-ttu-id="d1d03-136">Depois de baixar runbooks hello, você pode importá-los usando o procedimento Olá [criar ou importar um runbook na automação do Azure](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).</span><span class="sxs-lookup"><span data-stu-id="d1d03-136">After downloading hello runbooks, you can import them by using hello procedure in [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).</span></span>  <span data-ttu-id="d1d03-137">Publica cada runbook depois que ele é importado com êxito para sua conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="d1d03-137">Publish each runbook after it has been successfully imported into your Automation account.</span></span>

### <a name="add-a-schedule-toohello-test-resourceschedule-runbook"></a><span data-ttu-id="d1d03-138">Adicionar um runbook de toohello ResourceSchedule de teste do agendamento</span><span class="sxs-lookup"><span data-stu-id="d1d03-138">Add a schedule toohello Test-ResourceSchedule runbook</span></span>
<span data-ttu-id="d1d03-139">Seguir essas agendamento de saudação tooenable etapas de runbook de teste ResourceSchedule hello.</span><span class="sxs-lookup"><span data-stu-id="d1d03-139">Follow these steps tooenable hello schedule for hello Test-ResourceSchedule runbook.</span></span> <span data-ttu-id="d1d03-140">Isso é runbook Olá que verifica que máquinas virtuais deve ser iniciadas, encerrada, ou esquerda como está.</span><span class="sxs-lookup"><span data-stu-id="d1d03-140">This is hello runbook that verifies which virtual machines should be started, shut down, or left as is.</span></span>

1. <span data-ttu-id="d1d03-141">De Olá portal do Azure, abra sua conta de automação e clique em Olá **Runbooks** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="d1d03-141">From hello Azure portal, open your Automation account, and then click hello **Runbooks** tile.</span></span>
2. <span data-ttu-id="d1d03-142">Em Olá **teste ResourceSchedule** folha, clique em Olá **agendas** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="d1d03-142">On hello **Test-ResourceSchedule** blade, click hello **Schedules** tile.</span></span>
3. <span data-ttu-id="d1d03-143">Em Olá **agendas** folha, clique em **adicionar uma agenda**.</span><span class="sxs-lookup"><span data-stu-id="d1d03-143">On hello **Schedules** blade, click **Add a schedule**.</span></span>
4. <span data-ttu-id="d1d03-144">Em Olá **agendas** folha, selecione **vincula um runbook do agendamento tooyour**.</span><span class="sxs-lookup"><span data-stu-id="d1d03-144">On hello **Schedules** blade, select **Link a schedule tooyour runbook**.</span></span> <span data-ttu-id="d1d03-145">Em seguida, selecione **Criar um nova agendamento**.</span><span class="sxs-lookup"><span data-stu-id="d1d03-145">Then select **Create a new schedule**.</span></span>
5. <span data-ttu-id="d1d03-146">Em Olá **nova agenda** folha, digite o nome de saudação desse agendamento, por exemplo: *HourlyExecution*.</span><span class="sxs-lookup"><span data-stu-id="d1d03-146">On hello **New schedule** blade, type in hello name of this schedule, for example: *HourlyExecution*.</span></span>
6. <span data-ttu-id="d1d03-147">Para agendamento Olá **iniciar**, definir o incremento de hora do hello início tempo tooan.</span><span class="sxs-lookup"><span data-stu-id="d1d03-147">For hello schedule **Start**, set hello start time tooan hour increment.</span></span>
7. <span data-ttu-id="d1d03-148">Selecione **Recorrência** e em **Repetir a cada intervalo**, selecione **1 hora**.</span><span class="sxs-lookup"><span data-stu-id="d1d03-148">Select **Recurrence**, and then for **Recur every interval**, select **1 hour**.</span></span>
8. <span data-ttu-id="d1d03-149">Verifique **validade do conjunto de** está definido muito**não**e, em seguida, clique em **criar** toosave nova agenda.</span><span class="sxs-lookup"><span data-stu-id="d1d03-149">Verify that **Set expiration** is set too**No**, and then click **Create** toosave your new schedule.</span></span>
9. <span data-ttu-id="d1d03-150">Em Olá **agenda Runbook** folha de opções, selecione **parâmetros e configurações de execução**.</span><span class="sxs-lookup"><span data-stu-id="d1d03-150">On hello **Schedule Runbook** options blade, select **Parameters and run settings**.</span></span> <span data-ttu-id="d1d03-151">Em Olá teste ResourceSchedule **parâmetros** folha, insira o nome de saudação da sua assinatura no hello **SubscriptionName** campo.</span><span class="sxs-lookup"><span data-stu-id="d1d03-151">In hello Test-ResourceSchedule **Parameters** blade, enter hello name of your subscription in hello **SubscriptionName** field.</span></span>  <span data-ttu-id="d1d03-152">Este é o único parâmetro do hello necessária para o runbook hello.</span><span class="sxs-lookup"><span data-stu-id="d1d03-152">This is hello only parameter that's required for hello runbook.</span></span>  <span data-ttu-id="d1d03-153">Quando tiver terminado, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="d1d03-153">When you're finished, click **OK**.</span></span>

<span data-ttu-id="d1d03-154">agenda do runbook Olá deve ter aparência seguinte hello quando ela estiver concluída:</span><span class="sxs-lookup"><span data-stu-id="d1d03-154">hello runbook schedule should look like hello following when it's completed:</span></span>

![Runbook de Test-ResourceSchedule configurado](./media/automation-scenario-start-stop-vm-wjson-tags/automation-schedule-config.png)<br>

## <a name="format-hello-json-string"></a><span data-ttu-id="d1d03-156">Saudação de formato cadeia de caracteres JSON</span><span class="sxs-lookup"><span data-stu-id="d1d03-156">Format hello JSON string</span></span>
<span data-ttu-id="d1d03-157">Essa solução basicamente terá JSON de cadeia de caracteres com um formato especificado e o adiciona como valor de saudação de uma marca chamada agenda.</span><span class="sxs-lookup"><span data-stu-id="d1d03-157">This solution basically takes a JSON string with a specified format and adds it as hello value for a tag called Schedule.</span></span> <span data-ttu-id="d1d03-158">Em seguida, um runbook lista todos os grupos de recursos e as máquinas virtuais e identifica as agendas de saudação para cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d1d03-158">Then a runbook lists all resource groups and virtual machines and identifies hello schedules for each virtual machine.</span></span>

<span data-ttu-id="d1d03-159">Olá runbook circula por máquinas virtuais Olá que possuem agendas anexadas e verifica as ações que devem ser tomadas.</span><span class="sxs-lookup"><span data-stu-id="d1d03-159">hello runbook loops over hello virtual machines that have schedules attached and checks what actions should be taken.</span></span> <span data-ttu-id="d1d03-160">a seguir Olá é um exemplo de como soluções Olá devem ser formatadas:</span><span class="sxs-lookup"><span data-stu-id="d1d03-160">hello following is an example of how hello solutions should be formatted:</span></span>

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

<span data-ttu-id="d1d03-161">Veja algumas informações detalhadas sobre esta estrutura:</span><span class="sxs-lookup"><span data-stu-id="d1d03-161">Here is some detailed information about this structure:</span></span>

1. <span data-ttu-id="d1d03-162">formato de saudação dessa estrutura JSON é otimizada toowork em torno de limitação de 256 caracteres de saudação de um valor de marca única no Azure.</span><span class="sxs-lookup"><span data-stu-id="d1d03-162">hello format of this JSON structure is optimized toowork around hello 256-character limitation of a single tag value in Azure.</span></span>
2. <span data-ttu-id="d1d03-163">*TzId* representa Olá fuso horário da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="d1d03-163">*TzId* represents hello time zone of hello virtual machine.</span></span> <span data-ttu-id="d1d03-164">Essa ID pode ser obtida usando a classe do .NET TimeZoneInfo Olá em uma sessão do PowerShell –**[System.TimeZoneInfo]:: GetSystemTimeZones()**.</span><span class="sxs-lookup"><span data-stu-id="d1d03-164">This ID can be obtained by using hello TimeZoneInfo .NET class in a PowerShell session--**[System.TimeZoneInfo]::GetSystemTimeZones()**.</span></span>

   ![GetSystemTimeZones no PowerShell](./media/automation-scenario-start-stop-vm-wjson-tags/automation-get-timzone-powershell.png)

   * <span data-ttu-id="d1d03-166">Dias da semana são representados por um valor numérico de zero toosix.</span><span class="sxs-lookup"><span data-stu-id="d1d03-166">Weekdays are represented with a numeric value of zero toosix.</span></span> <span data-ttu-id="d1d03-167">o valor de saudação zero é igual a domingo.</span><span class="sxs-lookup"><span data-stu-id="d1d03-167">hello value zero equals Sunday.</span></span>
   * <span data-ttu-id="d1d03-168">Olá hora de início é representada por hello **S** atributo e seu valor está em um formato de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="d1d03-168">hello start time is represented with hello **S** attribute, and its value is in a 24-hour format.</span></span>
   * <span data-ttu-id="d1d03-169">Olá hora de término ou desligamento é representada por hello **E** atributo e seu valor está em um formato de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="d1d03-169">hello end or shutdown time is represented with hello **E** attribute, and its value is in a 24-hour format.</span></span>

     <span data-ttu-id="d1d03-170">Se hello **S** e **E** cada atributo tem um valor de zero (0), Olá virtual machine será deixado no estado atual no tempo de saudação da avaliação.</span><span class="sxs-lookup"><span data-stu-id="d1d03-170">If hello **S** and **E** attributes each have a value of zero (0), hello virtual machine will be left in its present state at hello time of evaluation.</span></span>
3. <span data-ttu-id="d1d03-171">Se você quiser tooskip avaliação durante um dia específico da semana hello, não adicione uma seção para esse dia da semana hello.</span><span class="sxs-lookup"><span data-stu-id="d1d03-171">If you want tooskip evaluation for a specific day of hello week, don’t add a section for that day of hello week.</span></span> <span data-ttu-id="d1d03-172">No hello seguinte exemplo, somente a segunda é avaliado e hello outros dias da semana Olá são ignorados:</span><span class="sxs-lookup"><span data-stu-id="d1d03-172">In hello following example, only Monday is evaluated, and hello other days of hello week are ignored:</span></span>

    ```json
    {
        "TzId": "Eastern Standard Time",
        "1": {
            "S": "11",
            "E": "17"
        }
    }
    ```

## <a name="tag-resource-groups-or-vms"></a><span data-ttu-id="d1d03-173">Marcar grupos de recursos ou VMs</span><span class="sxs-lookup"><span data-stu-id="d1d03-173">Tag resource groups or VMs</span></span>
<span data-ttu-id="d1d03-174">tooshut para baixo de VMs, você precisa tootag Olá VMs ou grupos de recursos de saudação em que está localizados.</span><span class="sxs-lookup"><span data-stu-id="d1d03-174">tooshut down VMs, you need tootag either hello VMs or hello resource groups in which they're located.</span></span> <span data-ttu-id="d1d03-175">Máquinas virtuais que não têm uma marcação de Agenda não são avaliadas.</span><span class="sxs-lookup"><span data-stu-id="d1d03-175">Virtual machines that don't have a Schedule tag are not evaluated.</span></span> <span data-ttu-id="d1d03-176">Portanto, elas não iniciadas ou desligadas.</span><span class="sxs-lookup"><span data-stu-id="d1d03-176">Therefore, they aren't started or shut down.</span></span>

<span data-ttu-id="d1d03-177">Há dois grupos de recursos tootag maneiras ou VMs com essa solução.</span><span class="sxs-lookup"><span data-stu-id="d1d03-177">There are two ways tootag resource groups or VMs with this solution.</span></span> <span data-ttu-id="d1d03-178">Você pode fazer isso diretamente do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="d1d03-178">You can do it directly from hello portal.</span></span> <span data-ttu-id="d1d03-179">Ou você pode usar o hello adicionar ResourceSchedule, ResourceSchedule de atualização e remover ResourceSchedule runbooks.</span><span class="sxs-lookup"><span data-stu-id="d1d03-179">Or you can use hello Add-ResourceSchedule, Update-ResourceSchedule, and Remove-ResourceSchedule runbooks.</span></span>

### <a name="tag-through-hello-portal"></a><span data-ttu-id="d1d03-180">Marca por meio do portal Olá</span><span class="sxs-lookup"><span data-stu-id="d1d03-180">Tag through hello portal</span></span>
<span data-ttu-id="d1d03-181">Siga estas etapas tootag uma máquina virtual ou um grupo de recursos no portal de saudação:</span><span class="sxs-lookup"><span data-stu-id="d1d03-181">Follow these steps tootag a virtual machine or resource group in hello portal:</span></span>

1. <span data-ttu-id="d1d03-182">Mesclar a cadeia de caracteres JSON hello e verificar que não existem espaços.</span><span class="sxs-lookup"><span data-stu-id="d1d03-182">Flatten hello JSON string and verify that there aren't any spaces.</span></span>  <span data-ttu-id="d1d03-183">A cadeia de caracteres JSON deve ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="d1d03-183">Your JSON string should look like this:</span></span>

    ```json
    {"TzId":"Eastern Standard Time","0":{"S":"11","E":"17"},"1":{"S":"9","E":"19"},"2": {"S":"9","E":"19"},"3":{"S":"9","E":"19"},"4":{"S":"9","E":"19"},"5":{"S":"9","E":"19"},"6":{"S":"11","E":"17"}}
    ```

2. <span data-ttu-id="d1d03-184">Selecione Olá **marca** ícone de uma VM ou o recurso grupo tooapply essa agenda.</span><span class="sxs-lookup"><span data-stu-id="d1d03-184">Select hello **Tag** icon for a VM or resource group tooapply this schedule.</span></span>

   ![Opção de marcação de VM](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-tag-option.png)

3. <span data-ttu-id="d1d03-186">As marcas são definidas seguindo um par chave/valor.</span><span class="sxs-lookup"><span data-stu-id="d1d03-186">Tags are defined following a key/value pair.</span></span> <span data-ttu-id="d1d03-187">Tipo **agenda** em Olá **chave** campo e, em seguida, cole cadeia de caracteres JSON Olá Olá **valor** campo.</span><span class="sxs-lookup"><span data-stu-id="d1d03-187">Type **Schedule** in hello **Key** field, and then paste hello JSON string into hello **Value** field.</span></span> <span data-ttu-id="d1d03-188">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="d1d03-188">Click **Save**.</span></span> <span data-ttu-id="d1d03-189">A nova marca agora deve aparecer na lista de saudação de marcas de recurso.</span><span class="sxs-lookup"><span data-stu-id="d1d03-189">Your new tag should now appear in hello list of tags for your resource.</span></span>

   ![Marcação de agendamento de VM](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-schedule-tag.png)

### <a name="tag-from-powershell"></a><span data-ttu-id="d1d03-191">Marcar do PowerShell</span><span class="sxs-lookup"><span data-stu-id="d1d03-191">Tag from PowerShell</span></span>
<span data-ttu-id="d1d03-192">Todos os runbooks importados contêm informações de Ajuda no início de saudação do script hello que descreve como tooexecute Olá runbooks diretamente do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d1d03-192">All imported runbooks contain help information at hello beginning of hello script that describes how tooexecute hello runbooks directly from PowerShell.</span></span> <span data-ttu-id="d1d03-193">Você pode chamar runbooks adicionar ScheduleResource e ScheduleResource de atualização de saudação do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d1d03-193">You can call hello Add-ScheduleResource and Update-ScheduleResource runbooks from PowerShell.</span></span> <span data-ttu-id="d1d03-194">Para fazer isso, passando parâmetros necessários que permitem que você marca de agenda Olá toocreate ou atualização em um VM ou grupo de recursos fora do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="d1d03-194">You do this by passing required parameters that enable you toocreate or update hello Schedule tag on a VM or resource group outside of hello portal.</span></span>

<span data-ttu-id="d1d03-195">toocreate, adicionar e excluir marcas por meio do PowerShell, você primeiro precisa muito[configurar seu ambiente do PowerShell para Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d1d03-195">toocreate, add, and delete tags through PowerShell, you first need too[set up your PowerShell environment for Azure](/powershell/azure/overview).</span></span> <span data-ttu-id="d1d03-196">Depois de concluir a instalação hello, você poderá continuar com hello etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="d1d03-196">After you complete hello setup, you can proceed with hello following steps.</span></span>

### <a name="create-a-schedule-tag-with-powershell"></a><span data-ttu-id="d1d03-197">Criar uma marcação de agendamento com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="d1d03-197">Create a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="d1d03-198">Abra uma sessão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d1d03-198">Open a PowerShell session.</span></span> <span data-ttu-id="d1d03-199">Em seguida, use Olá tooauthenticate de exemplo com sua conta executar como e toospecify uma assinatura a seguir:</span><span class="sxs-lookup"><span data-stu-id="d1d03-199">Then use hello following example tooauthenticate with your Run As account and toospecify a subscription:</span></span>

    ```powershell
    $Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="d1d03-200">Defina uma tabela de hash de agendamento.</span><span class="sxs-lookup"><span data-stu-id="d1d03-200">Define a schedule hash table.</span></span> <span data-ttu-id="d1d03-201">Aqui está um exemplo de como deve ser criado:</span><span class="sxs-lookup"><span data-stu-id="d1d03-201">Here is an example of how it should be constructed:</span></span>

    ```powershell
    $schedule= @{ "TzId"="Eastern Standard Time"; "0"= @{"S"="11";"E"="17"};"1"= @{"S"="9";"E"="19"};"2"= @{"S"="9";"E"="19"};"3"= @{"S"="9";"E"="19"};"4"= @{"S"="9";"E"="19"};"5"= @{"S"="9";"E"="19"};"6"= @{"S"="11";"E"="17"}}
    ```

3. <span data-ttu-id="d1d03-202">Defina parâmetros de saudação que são exigidos pelo runbook hello.</span><span class="sxs-lookup"><span data-stu-id="d1d03-202">Define hello parameters that are required by hello runbook.</span></span> <span data-ttu-id="d1d03-203">Saudação de exemplo a seguir, pretendemos uma VM:</span><span class="sxs-lookup"><span data-stu-id="d1d03-203">In hello following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "VmName"="VM01";"Schedule"=$schedule}
    ```

    <span data-ttu-id="d1d03-204">Se a marcação de um grupo de recursos, remova Olá *VMName* parâmetro do hash Olá $params tabela da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d1d03-204">If you’re tagging a resource group, remove hello *VMName* parameter from hello $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "Schedule"=$schedule}
    ```

4. <span data-ttu-id="d1d03-205">Execute o runbook Olá ResourceSchedule adicionar com Olá após parâmetros toocreate Olá agenda marca:</span><span class="sxs-lookup"><span data-stu-id="d1d03-205">Run hello Add-ResourceSchedule runbook with hello following parameters toocreate hello Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Add-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

5. <span data-ttu-id="d1d03-206">tooupdate uma marca de máquina virtual ou grupo de recursos, execute Olá **ResourceSchedule atualização** runbook com hello parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="d1d03-206">tooupdate a resource group or virtual machine tag, execute hello **Update-ResourceSchedule** runbook with hello following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Update-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

### <a name="remove-a-schedule-tag-with-powershell"></a><span data-ttu-id="d1d03-207">Remover uma marcação de agendamento com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="d1d03-207">Remove a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="d1d03-208">Abra uma sessão do PowerShell e execute Olá tooauthenticate com sua conta executar como e tooselect a seguir e especifique uma assinatura:</span><span class="sxs-lookup"><span data-stu-id="d1d03-208">Open a PowerShell session and run hello following tooauthenticate with your Run As account and tooselect and specify a subscription:</span></span>

    ```powershell
    Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="d1d03-209">Defina parâmetros de saudação que são exigidos pelo runbook hello.</span><span class="sxs-lookup"><span data-stu-id="d1d03-209">Define hello parameters that are required by hello runbook.</span></span> <span data-ttu-id="d1d03-210">Saudação de exemplo a seguir, pretendemos uma VM:</span><span class="sxs-lookup"><span data-stu-id="d1d03-210">In hello following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01";"VmName"="VM01"}
    ```

    <span data-ttu-id="d1d03-211">Se você estiver removendo uma marca de um grupo de recursos, remover Olá *VMName* parâmetro do hash Olá $params tabela da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d1d03-211">If you’re removing a tag from a resource group, remove hello *VMName* parameter from hello $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"}
    ```

3. <span data-ttu-id="d1d03-212">Execute a marca de agendamento de Olá Olá ResourceSchedule remover runbook tooremove:</span><span class="sxs-lookup"><span data-stu-id="d1d03-212">Execute hello Remove-ResourceSchedule runbook tooremove hello Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

4. <span data-ttu-id="d1d03-213">tooupdate uma marca de máquina virtual ou grupo de recursos, execute o runbook Olá remover ResourceSchedule com hello parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="d1d03-213">tooupdate a resource group or virtual machine tag, execute hello Remove-ResourceSchedule runbook with hello following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

> [!NOTE]
> <span data-ttu-id="d1d03-214">Recomendamos monitorar proativamente Esses runbooks (e estados de máquina virtual Olá) tooverify que suas máquinas virtuais estão sendo desligado e iniciou adequadamente.</span><span class="sxs-lookup"><span data-stu-id="d1d03-214">We recommend that you proactively monitor these runbooks (and hello virtual machine states) tooverify that your virtual machines are being shut down and started accordingly.</span></span>
>

<span data-ttu-id="d1d03-215">detalhes de saudação tooview de runbook Olá ResourceSchedule de teste de trabalho no hello portal do Azure, selecione Olá **trabalhos** bloco de runbook hello.</span><span class="sxs-lookup"><span data-stu-id="d1d03-215">tooview hello details of hello Test-ResourceSchedule runbook job in hello Azure portal, select hello **Jobs** tile of hello runbook.</span></span> <span data-ttu-id="d1d03-216">parâmetros de entrada do Hello trabalho Resumo exibe hello e saída de hello transmitir, além de toogeneral informações sobre o trabalho de saudação e todas as exceções que tenham ocorrido.</span><span class="sxs-lookup"><span data-stu-id="d1d03-216">hello job summary displays hello input parameters and hello output stream, in addition toogeneral information about hello job and any exceptions if they occurred.</span></span>

<span data-ttu-id="d1d03-217">Olá **resumo do trabalho** inclui mensagens de fluxos de saída, aviso e erro hello.</span><span class="sxs-lookup"><span data-stu-id="d1d03-217">hello **Job Summary** includes messages from hello output, warning, and error streams.</span></span> <span data-ttu-id="d1d03-218">Selecione Olá **saída** bloco tooview resultados da execução de runbook Olá detalhados.</span><span class="sxs-lookup"><span data-stu-id="d1d03-218">Select hello **Output** tile tooview detailed results from hello runbook execution.</span></span>

![Saída do Test-ResourceSchedule](./media/automation-scenario-start-stop-vm-wjson-tags/automation-job-output.png)

## <a name="next-steps"></a><span data-ttu-id="d1d03-220">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d1d03-220">Next steps</span></span>
* <span data-ttu-id="d1d03-221">tooget iniciado com runbooks do fluxo de trabalho do PowerShell, consulte [meu primeiro runbook de fluxo de trabalho do PowerShell](automation-first-runbook-textual.md).</span><span class="sxs-lookup"><span data-stu-id="d1d03-221">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md).</span></span>
* <span data-ttu-id="d1d03-222">toolearn mais informações sobre tipos de runbook e suas vantagens e limitações, consulte [tipos de runbook de automação do Azure](automation-runbook-types.md).</span><span class="sxs-lookup"><span data-stu-id="d1d03-222">toolearn more about runbook types, and their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md).</span></span>
* <span data-ttu-id="d1d03-223">Para saber mais sobre o recurso de suporte a scripts do PowerShell, veja [Suporte a scripts nativos do PowerShell na Automação do Azure](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/).</span><span class="sxs-lookup"><span data-stu-id="d1d03-223">For more information about PowerShell script support features, see [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/).</span></span>
* <span data-ttu-id="d1d03-224">toolearn mais sobre o log de runbook e de saída, consulte [Runbook mensagens na automação do Azure e a saída](automation-runbook-output-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="d1d03-224">toolearn more about runbook logging and output, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md).</span></span>
* <span data-ttu-id="d1d03-225">toolearn mais informações sobre uma conta executar como do Azure e como tooauthenticate seus runbooks ao usá-lo, consulte [autenticar runbooks com a conta executar como do Azure](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="d1d03-225">toolearn more about an Azure Run As account and how tooauthenticate your runbooks by using it, see [Authenticate runbooks with Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>
