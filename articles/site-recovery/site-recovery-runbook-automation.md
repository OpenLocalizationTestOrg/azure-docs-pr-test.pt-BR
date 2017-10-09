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
# <a name="add-azure-automation-runbooks-toorecovery-plans"></a>Adicionar planos de toorecovery de runbooks de automação do Azure
Neste artigo, descreveremos como o Azure Site Recovery integra toohelp de automação do Azure estender seus planos de recuperação. Os planos de recuperação podem orquestrar a recuperação de VMs que são protegidas com o Site Recovery. Planos de recuperação de trabalho para a nuvem secundária de tooa de replicação e de replicação tooAzure. Planos de recuperação também ajudam a tornar a recuperação Olá **precisas**, **repeatable**, e **automatizada**. Se você fizer failover tooAzure suas VMs, integração com a automação do Azure estende os planos de recuperação. Você pode usá-lo tooexecute runbooks, que oferecem tarefas de automação avançada.

Se você for novo tooAzure automação, você pode [inscrever](https://azure.microsoft.com/services/automation/) e [Baixe scripts de exemplo](https://azure.microsoft.com/documentation/scripts/). Para obter mais informações e toolearn como tooorchestrate recuperação tooAzure usando [planos de recuperação](https://azure.microsoft.com/blog/?p=166264), consulte [do Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).

Neste artigo, descrevemos como você pode integrar runbooks da Automação do Azure em planos de recuperação. Podemos usar exemplos tooautomate tarefas básicas que previamente necessitaram de intervenção manual. Podemos também descrevem como tooconvert tooa uma recuperação de várias etapas clicar uma ação de recuperação.

## <a name="customize-hello-recovery-plan"></a>Personalizar plano de recuperação de saudação
1. Vá toohello **recuperação de Site** folha de recursos do plano de recuperação. Neste exemplo, o plano de recuperação de saudação possui tooit adicionado VMs dois, para recuperação. toobegin adicionando um runbook, clique em Olá **personalizar** guia.

    ![Botão de personalizar Olá](media/site-recovery-runbook-automation-new/essentials-rp.png)


2. Clique com o botão direito do mouse em **Grupo 1: Iniciar** e, em seguida, selecione **Adicionar pós-ação**.

    ![Clicar com o botão direito do mouse em Grupo 1: Iniciar e em Adicionar pós-ação](media/site-recovery-runbook-automation-new/customize-rp.png)

3. Clique em **Escolher um script**.

4. Em Olá **atualizar ação** folha, script de saudação do nome **Hello World**.

    ![folha de ação de atualização de saudação](media/site-recovery-runbook-automation-new/update-rp.png)

5. Insira um nome para a conta de Automação.
    >[!NOTE]
    > Olá conta de automação pode estar em qualquer região do Azure. Olá conta de automação deve estar no hello mesma assinatura que o cofre do Azure Site Recovery hello.

6. Na conta de Automação, selecione um runbook. Este runbook é o script hello executado durante a execução de Olá Olá do plano de recuperação, após a recuperação de saudação do primeiro grupo de saudação.

7. script de saudação toosave, clique em **Okey**. saudação de script é adicionada muito**grupo 1: pós-etapas**.

    ![Grupo 1: Iniciar de pós-ação](media/site-recovery-runbook-automation-new/addedscript-rp.PNG)


## <a name="considerations-for-adding-a-script"></a>Considerações sobre a adição de um script

* Para opções muito**excluir uma etapa** ou **Atualizar script hello**, clique com botão direito script hello.
* Um script pode executar no Azure durante o failover de um tooAzure de máquina local. Ele também pode executar no Azure como um script do site primário antes do desligamento, durante o failback da máquina do Azure tooan local.
* Quando um script é executado, ele injeta um contexto do plano de recuperação. saudação de exemplo a seguir mostra uma variável de contexto:

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

    Olá, a tabela a seguir lista o nome de saudação e descrição de cada variável no contexto de saudação.

    | **Nome da variável** | **Descrição** |
    | --- | --- |
    | RecoveryPlanName |nome de saudação do plano hello está sendo executado. Essa variável ajuda você a executar ações diferentes com base no nome do plano de recuperação de saudação. Você também pode reutilizar o script hello. |
    | FailoverType |Especifica se o failover de saudação é um teste, planejado ou não planejado. |
    | FailoverDirection |Especifica se a recuperação é site primário ou secundário do tooa. |
    | GroupID |Identifica o número de grupo de saudação no plano de recuperação de saudação quando plano hello está sendo executado. |
    | VmMap |Uma matriz de todas as máquinas virtuais no grupo de saudação. |
    | Chave VMMap |Uma chave exclusiva (GUID) para cada VM. Seu Olá igual Olá ID Azure Virtual Machine Manager (VMM) do hello VM, onde aplicável. |
    | SubscriptionId |ID de assinatura do Azure Olá Olá a VM no qual foi criado. |
    | RoleName |nome de saudação do hello VM do Azure que está sendo recuperado. |
    | CloudServiceName |nome do serviço de nuvem do Azure Olá que sob a qual Olá VM foi criada. |
    | ResourceGroupName|nome do grupo de recursos do Azure Olá que sob a qual Olá VM foi criada. |
    | RecoveryPointId|Olá carimbo de hora de quando Olá VM é recuperado. |

* Certifique-se de que essa conta de automação Olá tem Olá módulos a seguir:
    * AzureRM.profile
    * AzureRM.Resources
    * AzureRM.Automation
    * AzureRM.Network
    * AzureRM.Compute

Todos os módulos devem ser de versões compatíveis. Um tooensure de maneira fácil que todos os módulos são compatíveis é toouse Olá últimas versões de todos os módulos de saudação.

### <a name="access-all-vms-of-hello-vmmap-in-a-loop"></a>Acessar todas as VMs de saudação VMMap em um loop
Use Olá tooloop de código a seguir em todas as VMs de saudação VMMap Microsoft:

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
> Olá recurso grupo nome e a função de valores de nome estão vazios ao script hello é um grupo de inicialização de pré-ação tooa. os valores Hello serão populados apenas se Olá VM desse grupo terá êxito em failover. script Hello é uma ação após do grupo de inicialização de saudação.

## <a name="use-hello-same-automation-runbook-in-multiple-recovery-plans"></a>Use Olá mesmo runbook de automação em vários planos de recuperação

Use um único script em vários planos de recuperação com variáveis externas. Você pode usar [variáveis de automação do Azure](../automation/automation-variables.md) toostore parâmetros que você pode passar para a recuperação de uma plano de execução. Adicionando o nome do plano de recuperação hello como uma variável de toohello de prefixo, você pode criar variáveis individuais para cada plano de recuperação. Em seguida, use variáveis de saudação como parâmetros. Você pode alterar um parâmetro sem alterar o script hello, mas ainda alterar Olá Olá forma script funciona.

### <a name="use-a-simple-string-variable-in-a-runbook-script"></a>Usar uma variável de cadeia de caracteres simples em um script de runbook

Neste exemplo, um script obtém dados de entrada hello de um grupo de segurança de rede (NSG) e o aplica toohello VMs de um plano de recuperação.

Para toodetect de script hello plano de recuperação que está em execução, use o contexto do plano de recuperação de saudação:

```
workflow AddPublicIPAndNSG {
    param (
          [parameter(Mandatory=$false)]
          [Object]$RecoveryPlanContext
    )

    $RPName = $RecoveryPlanContext.RecoveryPlanName
```

tooapply um NSG existente, você deve saber o nome do NSG hello e nome do grupo de recursos do hello NSG. Use essas variáveis como entradas para scripts do plano de recuperação. toodo isso, crie duas variáveis em Olá ativos da conta de automação. Adicione nome Olá Olá do plano de recuperação que você está criando parâmetros de saudação para como um nome de variável de toohello de prefixo.

1. Crie um nome NSG Olá toostore variável. Adicione um nome de variável de toohello de prefixo usando nome Olá Olá do plano de recuperação.

    ![Criar uma variável do nome do NSG](media/site-recovery-runbook-automation-new/var1.png)

2. Crie o nome do grupo de recursos do NSG uma variável toostore hello. Adicione um nome de variável de toohello de prefixo usando nome Olá Olá do plano de recuperação.

    ![Criar um nome do grupo de recursos do NSG](media/site-recovery-runbook-automation-new/var2.png)


3.  No script hello, use Olá referência código tooget Olá variável valores a seguir:

    ```
    $NSGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSG"
    $NSGRGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSGRG"

    $NSGnameVar = Get-AutomationVariable -Name $NSGValue
    $RGnameVar = Get-AutomationVariable -Name $NSGRGValue
    ```

4.  Use as variáveis Olá no hello runbook tooapply Olá NSG toohello interface de rede Olá failover VM:

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

Para cada plano de recuperação, crie variáveis independentes, para que você pode reutilizar o script hello. Adicione um prefixo usando o nome do plano de recuperação de saudação. Para um script completo e de ponta a ponta para este cenário, consulte [adicionar um tooVMs públicos de IP e NSG durante o failover de teste de um plano de recuperação do Site Recovery](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).


### <a name="use-a-complex-variable-toostore-more-information"></a>Use um toostore complexo de variável mais informações

Considere um cenário no qual você deseja tooturn um único script em um IP público em máquinas virtuais específicas. Em outro cenário, você pode querer tooapply NSGs diferentes em VMs diferentes (não em todas as máquinas virtuais). Você pode criar um script que é reutilizável para qualquer plano de recuperação. Cada plano de recuperação pode ter um número variável de VMs. Por exemplo, uma recuperação do SharePoint tem dois front-ends. Um aplicativo LOB (linha de negócios) básico tem apenas um front-end. Não é possível criar variáveis separadas para cada plano de recuperação. 

Saudação de exemplo a seguir, vamos usar uma técnica de novo e criar um [complexo de variável](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) em ativos de conta de automação do Azure hello. Faça isso especificando vários valores. Você deve usar o Azure PowerShell toocomplete Olá etapas a seguir:

1. No PowerShell, entrar tooyour assinatura do Azure:

    ```
    login-azurermaccount
    $sub = Get-AzureRmSubscription -Name <SubscriptionName>
    $sub | Select-AzureRmSubscription
    ```

2. parâmetros de saudação toostore, criar Olá complexo de variável usando nome Olá Olá do plano de recuperação:

    ```
    $VMDetails = @{"VMGUID"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"};"VMGUID2"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"}}
        New-AzureRmAutomationVariable -ResourceGroupName <RG of Automation Account> -AutomationAccountName <AA Name> -Name <RecoveryPlanName> -Value $VMDetails -Encrypted $false
    ```

3. Nessa variável complexo, **VMDetails** é hello ID da VM para Olá protegido VM. Olá tooget ID da VM, em Olá portal do Azure, exibir propriedades da VM Olá. Olá seguinte captura de tela mostra uma variável que armazena os detalhes de saudação de duas VMs:

    ![Usar Olá ID da VM como Olá GUID](media/site-recovery-runbook-automation-new/vmguid.png)

4. Use essa variável no runbook. Se Olá indicado que GUID da VM foi encontrado no contexto de plano de recuperação hello, aplica Olá NSG Olá VM:

    ```
    $VMDetailsObj = Get-AutomationVariable -Name $RecoveryPlanContext.RecoveryPlanName
    ```

4. Em seu runbook, um loop VMs de saudação do contexto de plano de recuperação de saudação. Verifique se Olá VM existe no **$VMDetailsObj**. Se ele existir, propriedades de saudação do acesso de tooapply variável Olá Olá NSG:

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

Você pode usar o hello mesmo script de planos de recuperação diferente. Insira parâmetros diferentes, armazenando o valor de saudação que corresponde o plano de recuperação de tooa em variáveis diferentes.

## <a name="sample-scripts"></a>Exemplos de scripts

tooyour scripts de exemplo toodeploy conta de automação, clique em Olá **implantar tooAzure** botão.

[![Implantar tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)

Outro exemplo, consulte Olá vídeo a seguir. Ele demonstra como toorecover tooAzure de aplicativo de WordPress uma de duas camadas:


> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/One-click-failover-of-a-2-tier-WordPress-application-using-Azure-Site-Recovery/player]



## <a name="additional-resources"></a>Recursos adicionais
* [Conta Executar como do serviço de Automação do Azure](../automation/automation-sec-configure-azure-runas-account.md)
* [Visão geral da Automação do Azure](http://msdn.microsoft.com/library/azure/dn643629.aspx "Visão geral da Automação do Azure")
* [Scripts de exemplo da Automação do Azure](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Scripts de exemplo da Automação do Azure")
