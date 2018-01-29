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
ms.date: 11/28/2017
ms.author: ruturajd@microsoft.com
ms.openlocfilehash: af5de1c262bc55b1aa7513ca91b68eb50b44dbb7
ms.sourcegitcommit: f847fcbf7f89405c1e2d327702cbd3f2399c4bc2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2017
---
# <a name="add-azure-automation-runbooks-to-recovery-plans"></a>Adicionar runbooks de Automação do Azure aos planos de recuperação
Neste artigo, descrevemos como o Azure Site Recovery é integrado à Automação do Azure para ajudar você a estender seus planos de recuperação. Os planos de recuperação podem orquestrar a recuperação de VMs que são protegidas com o Site Recovery. Os planos de recuperação funcionam para a replicação em uma nuvem secundária e para a replicação no Azure. Os planos de recuperação também ajudam a tornar a recuperação **precisa de forma consistente**, **repetida** e **automatizada**. Se você fizer failover das VMs no Azure, a integração com a Automação do Azure estenderá os planos de recuperação. Você pode usá-la para executar runbooks, que oferecem tarefas de automação avançadas.

Se você estiver conhecendo a Automação do Azure agora, [inscreva-se](https://azure.microsoft.com/services/automation/) e [baixe scripts de exemplo](https://azure.microsoft.com/documentation/scripts/). Para obter mais informações e para saber como orquestrar a recuperação no Azure usando [planos de recuperação](https://azure.microsoft.com/blog/?p=166264), consulte [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).

Neste artigo, descrevemos como você pode integrar runbooks da Automação do Azure em planos de recuperação. Usamos exemplos para automatizar tarefas básicas que anteriormente necessitavam de intervenção manual. Também descrevemos como converter uma recuperação de várias etapas em uma ação de recuperação de clique simples.

## <a name="customize-the-recovery-plan"></a>Personalizar o plano de recuperação
1. Acesse a folha de recursos do plano de recuperação do **Site Recovery**. Neste exemplo, o plano de recuperação tem duas VMs adicionadas a ele, para recuperação. Para começar a adicionar um runbook, clique na guia **Personalizar**.

    ![Clicar no botão Personalizar](media/site-recovery-runbook-automation-new/essentials-rp.png)


2. Clique com o botão direito do mouse em **Grupo 1: Iniciar** e, em seguida, selecione **Adicionar pós-ação**.

    ![Clicar com o botão direito do mouse em Grupo 1: Iniciar e em Adicionar pós-ação](media/site-recovery-runbook-automation-new/customize-rp.png)

3. Clique em **Escolher um script**.

4. Na folha **Atualizar ação**, nomeie o script **Olá, Mundo**.

    ![A folha Atualizar ação](media/site-recovery-runbook-automation-new/update-rp.png)

5. Insira um nome para a conta de Automação.
    >[!NOTE]
    > A conta de Automação pode estar em qualquer região do Azure. A conta de Automação deve estar na mesma assinatura do cofre do Azure Site Recovery.

6. Na conta de Automação, selecione um runbook. Esse runbook é o script que é executado durante a execução do plano de recuperação, após a recuperação do primeiro grupo.

7. Para salvar o script, clique em **OK**. O script é adicionado ao **Grupo 1: Pós-etapas**.

    ![Grupo 1: Iniciar de pós-ação](media/site-recovery-runbook-automation-new/addedscript-rp.PNG)


## <a name="considerations-for-adding-a-script"></a>Considerações sobre a adição de um script

* Para obter opções para **excluir uma etapa** ou **atualizar o script**, clique com o botão direito do mouse no script.
* Um script pode ser executado no Azure durante o failover de um computador local para o Azure. Ele também pode ser executado no Azure como um script do site primário antes do desligamento, durante o failback do Azure para um computador local.
* Quando um script é executado, ele injeta um contexto do plano de recuperação. O seguinte exemplo mostra uma variável de contexto:

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

    A tabela a seguir lista o nome e a descrição de cada variável no contexto.

    | **Nome da variável** | **Descrição** |
    | --- | --- |
    | RecoveryPlanName |O nome do plano em execução. Essa variável ajuda você a executar ações diferentes com base no nome do plano de recuperação. Também é possível reutilizar o script. |
    | FailoverType |Especifica se o failover é um teste, planejado ou não planejado. |
    | FailoverDirection |Especifica se a recuperação é feita em um site primário ou secundário. |
    | GroupID |Identifica o número de grupo no plano de recuperação quando o plano está em execução. |
    | VmMap |Uma matriz de todas as VMs do grupo. |
    | Chave VMMap |Uma chave exclusiva (GUID) para cada VM. Igual à ID do Azure VMM (Virtual Machine Manager) da VM, quando aplicável. |
    | SubscriptionId |A ID da assinatura do Azure em que a VM foi criada. |
    | RoleName |O nome da VM do Azure que está sendo recuperada. |
    | CloudServiceName |O nome de serviço de nuvem do Azure no qual a VM foi criada. |
    | ResourceGroupName|O nome do grupo de recursos do Azure no qual a VM foi criada. |
    | RecoveryPointId|O carimbo de data/hora de quando a VM foi recuperada. |

* Garanta que a conta de Automação tem os seguintes módulos:
    * AzureRM.profile
    * AzureRM.Resources
    * AzureRM.Automation
    * AzureRM.Network
    * AzureRM.Compute

Todos os módulos devem ser de versões compatíveis. Uma maneira fácil de garantir que todos os módulos são compatíveis é usar as últimas versões de todos os módulos.

### <a name="access-all-vms-of-the-vmmap-in-a-loop"></a>Acessar todas as VMs do VMMap em um loop
Use o seguinte código para criar um loop em todas as VMs do Microsoft VMMap:

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
> O nome do grupo de recursos e os valores do nome da função ficam vazios quando o script é uma pré-ação de um grupo de inicialização. Os valores são populados somente se a VM do grupo tem êxito no failover. O script é uma pós-ação do grupo de inicialização.

## <a name="use-the-same-automation-runbook-in-multiple-recovery-plans"></a>Usar o mesmo runbook de Automação em vários planos de recuperação

Use um único script em vários planos de recuperação com variáveis externas. Use as [variáveis da Automação do Azure](../automation/automation-variables.md) para armazenar os parâmetros que podem ser passados para a execução de um plano de recuperação. Adicionando o nome do plano de recuperação como um prefixo da variável, você pode criar variáveis individuais para cada plano de recuperação. Em seguida, use as variáveis como parâmetros. Altere um parâmetro sem alterar o script, mas ainda altere a maneira como o script funciona.

### <a name="use-a-simple-string-variable-in-a-runbook-script"></a>Usar uma variável de cadeia de caracteres simples em um script de runbook

Neste exemplo, um script usa a entrada de um NSG (Grupo de Segurança de Rede) e a aplica às VMs de um plano de recuperação.

Para que o script detecte qual plano de recuperação está em execução, use o contexto do plano de recuperação:

```
workflow AddPublicIPAndNSG {
    param (
          [parameter(Mandatory=$false)]
          [Object]$RecoveryPlanContext
    )

    $RPName = $RecoveryPlanContext.RecoveryPlanName
```

Para aplicar um NSG existente, você deve saber o nome do NSG e o nome do grupo de recursos do NSG. Use essas variáveis como entradas para scripts do plano de recuperação. Para fazer isso, crie duas variáveis nos ativos da conta de Automação. Adicione o nome do plano de recuperação para o qual os parâmetros estão sendo criados como um prefixo do nome da variável.

1. Crie uma variável para armazenar o nome do NSG. Adicione um prefixo ao nome da variável usando o nome do plano de recuperação.

    ![Criar uma variável do nome do NSG](media/site-recovery-runbook-automation-new/var1.png)

2. Crie uma variável para armazenar o nome do grupo de recursos do NSG. Adicione um prefixo ao nome da variável usando o nome do plano de recuperação.

    ![Criar um nome do grupo de recursos do NSG](media/site-recovery-runbook-automation-new/var2.png)


3.  No script, use o seguinte código de referência para obter os valores de variáveis:

    ```
    $NSGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSG"
    $NSGRGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSGRG"

    $NSGnameVar = Get-AutomationVariable -Name $NSGValue
    $RGnameVar = Get-AutomationVariable -Name $NSGRGValue
    ```

4.  Use as variáveis no runbook para aplicar o NSG ao adaptador de rede da VM com failover:

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

Para cada plano de recuperação, crie variáveis independentes, de modo que você possa reutilizar o script. Adicione um prefixo usando o nome do plano de recuperação. Para obter um script completo de ponta a ponta para este cenário, consulte [Adicionar um IP público e um NSG a VMs durante o failover de teste de um plano de recuperação do Site Recovery](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).


### <a name="use-a-complex-variable-to-store-more-information"></a>Usar uma variável complexa para armazenar mais informações

Considere um cenário no qual você deseja que um único script ative um IP público em VMs específicas. Em outro cenário, talvez você deseje aplicar NSGs diferentes a VMs diferentes (não em todas as VMs). Você pode criar um script que é reutilizável para qualquer plano de recuperação. Cada plano de recuperação pode ter um número variável de VMs. Por exemplo, uma recuperação do SharePoint tem dois front-ends. Um aplicativo LOB (linha de negócios) básico tem apenas um front-end. Não é possível criar variáveis separadas para cada plano de recuperação. 

No exemplo a seguir, usamos uma nova técnica e criamos uma [variável complexa](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) nos ativos da conta de Automação do Azure. Faça isso especificando vários valores. Use o Azure PowerShell para concluir as seguintes etapas:

1. No PowerShell, entre em sua assinatura do Azure:

    ```
    login-azurermaccount
    $sub = Get-AzureRmSubscription -Name <SubscriptionName>
    $sub | Select-AzureRmSubscription
    ```

2. Para armazenar os parâmetros, crie uma variável complexa usando o mesmo nome do plano de recuperação:

    ```
    $VMDetails = @{"VMGUID"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"};"VMGUID2"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"}}
        New-AzureRmAutomationVariable -ResourceGroupName <RG of Automation Account> -AutomationAccountName <AA Name> -Name <RecoveryPlanName> -Value $VMDetails -Encrypted $false
    ```

3. Nessa variável complexa, **VMDetails** é a ID de VM da VM protegida. Para obter a ID de VM, no portal do Azure, exiba as propriedades da VM. A seguinte captura de tela mostra uma variável que armazena os detalhes de duas VMs:

    ![Usar a ID de VM como o GUID](media/site-recovery-runbook-automation-new/vmguid.png)

4. Use essa variável no runbook. Se o GUID de VM indicado for encontrado no contexto do plano de recuperação, aplique o NSG à VM:

    ```
    $VMDetailsObj = Get-AutomationVariable -Name $RecoveryPlanContext.RecoveryPlanName
    ```

4. No runbook, percorra as VMs do contexto do plano de recuperação. Verifique se a VM existe em **$VMDetailsObj**. Se ela existir, acesse as propriedades da variável para aplicar o NSG:

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

Use o mesmo script para planos de recuperação diferentes. Insira parâmetros diferentes armazenando o valor que corresponde a um plano de recuperação em variáveis diferentes.

## <a name="sample-scripts"></a>Exemplos de scripts

Para implantar scripts de exemplo em sua conta de Automação, clique no botão **Implantar no Azure**.

[![Implantar no Azure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)

Para obter outro exemplo, assista ao vídeo a seguir. Ele demonstra como recuperar um aplicativo do WordPress de duas camadas no Azure:


> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/One-click-failover-of-a-2-tier-WordPress-application-using-Azure-Site-Recovery/player]



## <a name="additional-resources"></a>Recursos adicionais
* [Conta Executar como do serviço de Automação do Azure](../automation/automation-sec-configure-azure-runas-account.md)
* [Visão geral da Automação do Azure](http://msdn.microsoft.com/library/azure/dn643629.aspx "Visão geral da Automação do Azure")
* [Scripts de exemplo da Automação do Azure](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Scripts de exemplo da Automação do Azure")
