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
# <a name="azure-automation-scenario-using-json-formatted-tags-toocreate-a-schedule-for-azure-vm-startup-and-shutdown"></a>Cenário de automação do Azure: usando o formato JSON marcas toocreate uma agenda para a VM do Azure inicialização e desligamento
Os clientes frequentemente querem tooschedule inicialização de saudação e reduzir os custos de assinatura de desligamento de máquinas virtuais toohelp ou dar suporte a requisitos comerciais e técnicos.

Olá cenário a seguir permite que você tooset backup automatizado de inicialização e desligamento do suas VMs usando uma marca chamada agenda em nível de máquina virtual no Azure ou nível de grupo de recursos. Esta agenda pode ser configurada no domingo tooSaturday com um tempo de inicialização e o tempo de desligamento.

Temos algumas opções imediatas. Estão incluídos:

* [Conjuntos de escala de máquina virtual](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) com configurações de dimensionamento automático que permitem que você tooscale in ou out.
* [DevTest Labs](../devtest-lab/devtest-lab-overview.md) serviço, que tem o recurso interno de saudação do planejamento de operações de inicialização e desligamento.

No entanto, essas opções somente suportam a cenários específicos e não pode ser aplicado tooinfrastructure-como um serviço (IaaS) VMs.

Quando Olá marca de agendamento for aplicado tooa grupo de recursos, também é aplicado tooall máquinas de virtuais dentro desse grupo de recursos. Se uma agenda também é aplicado diretamente tooa VM, o último agendamento de saudação tem precedência em Olá ordem a seguir:

1. Grupo de recursos do agendamento tooa aplicado
2. Agendar o grupo de recursos de tooa aplicado e a máquina virtual no grupo de recursos de saudação
3. Agendar a máquina virtual de tooa aplicado

Este cenário essencialmente usa uma cadeia de caracteres JSON com um formato especificado e o adiciona como valor Olá para uma marca chamada agenda. Em seguida, um runbook lista todos os grupos de recursos e as máquinas virtuais e identifica agendas Olá para cada VM com base em cenários de saudação listados anteriormente. Em seguida, ele percorre Olá VMs que têm agendas anexadas e avalia a ação que deve ser executada. Por exemplo, ele determina que VMs precisam toobe parado, desligar ou ignorado.

Esses runbooks autenticar usando Olá [conta executar como do Azure](automation-sec-configure-azure-runas-account.md).

## <a name="download-hello-runbooks-for-hello-scenario"></a>Baixar runbooks Olá para o cenário de saudação
Este cenário consiste em quatro runbooks de fluxo de trabalho do PowerShell que você pode baixar do hello [Galeria do TechNet](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) ou hello [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) repositório para este projeto.

| Runbook | Descrição |
| --- | --- |
| Test-ResourceSchedule |Verifica cada agenda de máquina virtual e executa o desligamento ou inicialização dependendo da agenda de saudação. |
| Add-ResourceSchedule |Adiciona Olá agenda marca tooa VM ou grupo de recursos. |
| Update-ResourceSchedule |Modifica a marca de agendamento existente Olá substituindo-o com um novo. |
| Remove-ResourceSchedule |Remove a marca de agenda de saudação de um VM ou grupo de recursos. |

## <a name="install-and-configure-this-scenario"></a>Instalar e configurar esse cenário
### <a name="install-and-publish-hello-runbooks"></a>Instalar e publicar runbooks Olá
Depois de baixar runbooks hello, você pode importá-los usando o procedimento Olá [criar ou importar um runbook na automação do Azure](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).  Publica cada runbook depois que ele é importado com êxito para sua conta de Automação.

### <a name="add-a-schedule-toohello-test-resourceschedule-runbook"></a>Adicionar um runbook de toohello ResourceSchedule de teste do agendamento
Seguir essas agendamento de saudação tooenable etapas de runbook de teste ResourceSchedule hello. Isso é runbook Olá que verifica que máquinas virtuais deve ser iniciadas, encerrada, ou esquerda como está.

1. De Olá portal do Azure, abra sua conta de automação e clique em Olá **Runbooks** lado a lado.
2. Em Olá **teste ResourceSchedule** folha, clique em Olá **agendas** lado a lado.
3. Em Olá **agendas** folha, clique em **adicionar uma agenda**.
4. Em Olá **agendas** folha, selecione **vincula um runbook do agendamento tooyour**. Em seguida, selecione **Criar um nova agendamento**.
5. Em Olá **nova agenda** folha, digite o nome de saudação desse agendamento, por exemplo: *HourlyExecution*.
6. Para agendamento Olá **iniciar**, definir o incremento de hora do hello início tempo tooan.
7. Selecione **Recorrência** e em **Repetir a cada intervalo**, selecione **1 hora**.
8. Verifique **validade do conjunto de** está definido muito**não**e, em seguida, clique em **criar** toosave nova agenda.
9. Em Olá **agenda Runbook** folha de opções, selecione **parâmetros e configurações de execução**. Em Olá teste ResourceSchedule **parâmetros** folha, insira o nome de saudação da sua assinatura no hello **SubscriptionName** campo.  Este é o único parâmetro do hello necessária para o runbook hello.  Quando tiver terminado, clique em **OK**.

agenda do runbook Olá deve ter aparência seguinte hello quando ela estiver concluída:

![Runbook de Test-ResourceSchedule configurado](./media/automation-scenario-start-stop-vm-wjson-tags/automation-schedule-config.png)<br>

## <a name="format-hello-json-string"></a>Saudação de formato cadeia de caracteres JSON
Essa solução basicamente terá JSON de cadeia de caracteres com um formato especificado e o adiciona como valor de saudação de uma marca chamada agenda. Em seguida, um runbook lista todos os grupos de recursos e as máquinas virtuais e identifica as agendas de saudação para cada máquina virtual.

Olá runbook circula por máquinas virtuais Olá que possuem agendas anexadas e verifica as ações que devem ser tomadas. a seguir Olá é um exemplo de como soluções Olá devem ser formatadas:

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

Veja algumas informações detalhadas sobre esta estrutura:

1. formato de saudação dessa estrutura JSON é otimizada toowork em torno de limitação de 256 caracteres de saudação de um valor de marca única no Azure.
2. *TzId* representa Olá fuso horário da máquina virtual de saudação. Essa ID pode ser obtida usando a classe do .NET TimeZoneInfo Olá em uma sessão do PowerShell –**[System.TimeZoneInfo]:: GetSystemTimeZones()**.

   ![GetSystemTimeZones no PowerShell](./media/automation-scenario-start-stop-vm-wjson-tags/automation-get-timzone-powershell.png)

   * Dias da semana são representados por um valor numérico de zero toosix. o valor de saudação zero é igual a domingo.
   * Olá hora de início é representada por hello **S** atributo e seu valor está em um formato de 24 horas.
   * Olá hora de término ou desligamento é representada por hello **E** atributo e seu valor está em um formato de 24 horas.

     Se hello **S** e **E** cada atributo tem um valor de zero (0), Olá virtual machine será deixado no estado atual no tempo de saudação da avaliação.
3. Se você quiser tooskip avaliação durante um dia específico da semana hello, não adicione uma seção para esse dia da semana hello. No hello seguinte exemplo, somente a segunda é avaliado e hello outros dias da semana Olá são ignorados:

    ```json
    {
        "TzId": "Eastern Standard Time",
        "1": {
            "S": "11",
            "E": "17"
        }
    }
    ```

## <a name="tag-resource-groups-or-vms"></a>Marcar grupos de recursos ou VMs
tooshut para baixo de VMs, você precisa tootag Olá VMs ou grupos de recursos de saudação em que está localizados. Máquinas virtuais que não têm uma marcação de Agenda não são avaliadas. Portanto, elas não iniciadas ou desligadas.

Há dois grupos de recursos tootag maneiras ou VMs com essa solução. Você pode fazer isso diretamente do portal de saudação. Ou você pode usar o hello adicionar ResourceSchedule, ResourceSchedule de atualização e remover ResourceSchedule runbooks.

### <a name="tag-through-hello-portal"></a>Marca por meio do portal Olá
Siga estas etapas tootag uma máquina virtual ou um grupo de recursos no portal de saudação:

1. Mesclar a cadeia de caracteres JSON hello e verificar que não existem espaços.  A cadeia de caracteres JSON deve ter esta aparência:

    ```json
    {"TzId":"Eastern Standard Time","0":{"S":"11","E":"17"},"1":{"S":"9","E":"19"},"2": {"S":"9","E":"19"},"3":{"S":"9","E":"19"},"4":{"S":"9","E":"19"},"5":{"S":"9","E":"19"},"6":{"S":"11","E":"17"}}
    ```

2. Selecione Olá **marca** ícone de uma VM ou o recurso grupo tooapply essa agenda.

   ![Opção de marcação de VM](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-tag-option.png)

3. As marcas são definidas seguindo um par chave/valor. Tipo **agenda** em Olá **chave** campo e, em seguida, cole cadeia de caracteres JSON Olá Olá **valor** campo. Clique em **Salvar**. A nova marca agora deve aparecer na lista de saudação de marcas de recurso.

   ![Marcação de agendamento de VM](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-schedule-tag.png)

### <a name="tag-from-powershell"></a>Marcar do PowerShell
Todos os runbooks importados contêm informações de Ajuda no início de saudação do script hello que descreve como tooexecute Olá runbooks diretamente do PowerShell. Você pode chamar runbooks adicionar ScheduleResource e ScheduleResource de atualização de saudação do PowerShell. Para fazer isso, passando parâmetros necessários que permitem que você marca de agenda Olá toocreate ou atualização em um VM ou grupo de recursos fora do portal de saudação.

toocreate, adicionar e excluir marcas por meio do PowerShell, você primeiro precisa muito[configurar seu ambiente do PowerShell para Azure](/powershell/azure/overview). Depois de concluir a instalação hello, você poderá continuar com hello etapas a seguir.

### <a name="create-a-schedule-tag-with-powershell"></a>Criar uma marcação de agendamento com o PowerShell
1. Abra uma sessão do PowerShell. Em seguida, use Olá tooauthenticate de exemplo com sua conta executar como e toospecify uma assinatura a seguir:

    ```powershell
    $Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. Defina uma tabela de hash de agendamento. Aqui está um exemplo de como deve ser criado:

    ```powershell
    $schedule= @{ "TzId"="Eastern Standard Time"; "0"= @{"S"="11";"E"="17"};"1"= @{"S"="9";"E"="19"};"2"= @{"S"="9";"E"="19"};"3"= @{"S"="9";"E"="19"};"4"= @{"S"="9";"E"="19"};"5"= @{"S"="9";"E"="19"};"6"= @{"S"="11";"E"="17"}}
    ```

3. Defina parâmetros de saudação que são exigidos pelo runbook hello. Saudação de exemplo a seguir, pretendemos uma VM:

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "VmName"="VM01";"Schedule"=$schedule}
    ```

    Se a marcação de um grupo de recursos, remova Olá *VMName* parâmetro do hash Olá $params tabela da seguinte maneira:

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "Schedule"=$schedule}
    ```

4. Execute o runbook Olá ResourceSchedule adicionar com Olá após parâmetros toocreate Olá agenda marca:

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Add-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

5. tooupdate uma marca de máquina virtual ou grupo de recursos, execute Olá **ResourceSchedule atualização** runbook com hello parâmetros a seguir:

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Update-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

### <a name="remove-a-schedule-tag-with-powershell"></a>Remover uma marcação de agendamento com o PowerShell
1. Abra uma sessão do PowerShell e execute Olá tooauthenticate com sua conta executar como e tooselect a seguir e especifique uma assinatura:

    ```powershell
    Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. Defina parâmetros de saudação que são exigidos pelo runbook hello. Saudação de exemplo a seguir, pretendemos uma VM:

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01";"VmName"="VM01"}
    ```

    Se você estiver removendo uma marca de um grupo de recursos, remover Olá *VMName* parâmetro do hash Olá $params tabela da seguinte maneira:

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"}
    ```

3. Execute a marca de agendamento de Olá Olá ResourceSchedule remover runbook tooremove:

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

4. tooupdate uma marca de máquina virtual ou grupo de recursos, execute o runbook Olá remover ResourceSchedule com hello parâmetros a seguir:

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

> [!NOTE]
> Recomendamos monitorar proativamente Esses runbooks (e estados de máquina virtual Olá) tooverify que suas máquinas virtuais estão sendo desligado e iniciou adequadamente.
>

detalhes de saudação tooview de runbook Olá ResourceSchedule de teste de trabalho no hello portal do Azure, selecione Olá **trabalhos** bloco de runbook hello. parâmetros de entrada do Hello trabalho Resumo exibe hello e saída de hello transmitir, além de toogeneral informações sobre o trabalho de saudação e todas as exceções que tenham ocorrido.

Olá **resumo do trabalho** inclui mensagens de fluxos de saída, aviso e erro hello. Selecione Olá **saída** bloco tooview resultados da execução de runbook Olá detalhados.

![Saída do Test-ResourceSchedule](./media/automation-scenario-start-stop-vm-wjson-tags/automation-job-output.png)

## <a name="next-steps"></a>Próximas etapas
* tooget iniciado com runbooks do fluxo de trabalho do PowerShell, consulte [meu primeiro runbook de fluxo de trabalho do PowerShell](automation-first-runbook-textual.md).
* toolearn mais informações sobre tipos de runbook e suas vantagens e limitações, consulte [tipos de runbook de automação do Azure](automation-runbook-types.md).
* Para saber mais sobre o recurso de suporte a scripts do PowerShell, veja [Suporte a scripts nativos do PowerShell na Automação do Azure](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/).
* toolearn mais sobre o log de runbook e de saída, consulte [Runbook mensagens na automação do Azure e a saída](automation-runbook-output-and-messages.md).
* toolearn mais informações sobre uma conta executar como do Azure e como tooauthenticate seus runbooks ao usá-lo, consulte [autenticar runbooks com a conta executar como do Azure](automation-sec-configure-azure-runas-account.md).
