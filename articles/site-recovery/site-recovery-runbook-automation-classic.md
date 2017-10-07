---
title: "planos de toorecovery de runbooks de automação do Azure de aaaAdd no portal clássico Olá | Microsoft Docs"
description: "Este artigo descreve como recuperação de Site do Azure agora permite que você tooextend planos de recuperação usando tarefas complexas de toocomplete de automação do Azure durante a recuperação tooAzure"
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: f24eaa62-9dea-4fce-92e1-a72513ca0289
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 3bb7420911afbce289b656f28823b1923e8af0c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans-in-hello-classic-portal"></a>Adicionar planos de toorecovery de runbooks de automação do Azure no portal clássico Olá
Este tutorial descreve como o Azure Site Recovery integra-se a automação do Azure tooprovide extensibilidade toorecovery planos. Planos de recuperação podem coordenar a recuperação das máquinas virtuais protegidas usando o Azure Site Recovery para a nuvem de toosecondary de replicação e cenários de tooAzure de replicação. Eles também ajudam a fazer a recuperação de saudação **precisas**, **repeatable**, e **automatizada**. Se você estiver realizando o failover tooAzure suas máquinas virtuais, integração com a automação do Azure estende os planos de recuperação e fornece funcionalidade tooexecute runbooks, permitindo assim que as tarefas de automação avançada.

Se você ainda não souber o que é a Automação do Azure, inscreva-se [aqui](https://azure.microsoft.com/services/automation/) e baixe os exemplos de script [aqui](https://azure.microsoft.com/documentation/scripts/). Leia mais sobre [do Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) e como os planos de tooorchestrate tooAzure de recuperação com a recuperação de [aqui](https://azure.microsoft.com/blog/?p=166264).

Neste breve tutorial, veremos como você pode integrar os runbooks de automação do Azure aos planos de recuperação. Vamos automatizar tarefas simples, que anteriormente necessária intervenção manual e veja como um múltiplo de tooconvert intervir recuperação uma ação de recuperação de único clique. Também veremos como você pode solucionar problemas de um script simples, caso ocorra algum erro.

## <a name="protect-hello-application-tooazure"></a>Proteger a saudação aplicativo tooAzure
Vamos começa com um aplicativo simples composto por duas máquinas virtuais. Aqui, temos um aplicativo HRweb da Fabrikam. A Fabrikam de HRweb de front-end e Fabrikam-Hrweb-back-end são Olá duas VMs protegidas tooAzure usando o Azure Site Recovery. tooprotect Olá VMs usando o Azure Site Recovery, siga as etapas de saudação abaixo.

1. Habilite a proteção para as máquinas virtuais.
2. Verifique se as máquinas virtuais de saudação concluiu a replicação inicial e estiver replicando.
3. Aguarde até que Olá a replicação inicial for concluída e status de replicação de saudação diz protegidos.

## ![](media/site-recovery-runbook-automation/01.png)
Neste tutorial, vamos criar um plano de recuperação para Olá Fabrikam HRweb aplicativo toofailover Olá aplicativo tooAzure. Em seguida, integraremos-lo com um runbook que criará um ponto de extremidade em Olá failover da máquina virtual do Azure tooserve web páginas na porta 80.

Primeiro, vamos criar um plano de recuperação para nosso aplicativo.

## <a name="create-hello-recovery-plan"></a>Criar plano de recuperação de saudação
toorecover tooAzure de aplicativo hello, você precisa toocreate um plano de recuperação.
Usando um plano de recuperação que você pode especificar a ordem de saudação da recuperação das máquinas virtuais. máquina virtual de saudação colocada no grupo 1 será recuperar e inicie o primeiro e depois de máquina virtual de saudação no grupo 2.

Crie um Plano de recuperação parecido com o exibido abaixo.

![](media/site-recovery-runbook-automation/12.png)

mais informações sobre planos de recuperação, leia a documentação do tooread [aqui](https://msdn.microsoft.com/library/azure/dn788799.aspx "aqui").

Em seguida, vamos criar hello artefatos necessários na automação do Azure.

## <a name="create-hello-automation-account-and-its-assets"></a>Criar conta de automação hello e seus ativos
É necessário um runbooks de toocreate de conta de automação do Azure. Se você não tiver uma conta, navegar pelo guia de tooAzure de automação ![](media/site-recovery-runbook-automation/02.png)e criar uma nova conta.

1. Dar conta Olá tooidentify um nome com.
2. Especifique uma região geográfica onde deseja que a conta de saudação tooplace.

É recomendável tooplace conta Olá Olá mesma região do cofre Olá ASR.

![](media/site-recovery-runbook-automation/03.png)

Em seguida, crie Olá ativos em Olá conta a seguir.

### <a name="add-a-subscription-name-as-asset"></a>Adicionar um nome de assinatura como ativo
1. Adicionar uma nova configuração ![](media/site-recovery-runbook-automation/04.png) em Olá ativos de automação do Azure e selecione muito![](media/site-recovery-runbook-automation/05.png)
2. Selecione o tipo de variável hello como **cadeia de caracteres**
3. Especifique o nome da variável como **AzureSubscriptionName**

   ![](media/site-recovery-runbook-automation/06.png)
4. Especifique o nome real da assinatura do Azure como o valor da variável hello.

   ![](media/site-recovery-runbook-automation/07_1.png)

Você pode identificar o nome de saudação da sua assinatura na página de configurações de saudação da sua conta no hello portal do Azure.

### <a name="add-an-azure-login-credential-as-asset"></a>Adicionar uma credencial de logon do Azure como ativo
Automação do Azure usa a assinatura do Azure PowerShell tooconnect toothe e opera em artefatos de saudação existe. Para isso, você precisa autenticar usando sua conta da Microsoft ou uma conta corporativa ou de estudante.
Você pode armazenar as credenciais de conta de saudação em um toobe ativo com segurança usado pelo runbook hello.

1. Adicionar uma nova configuração ![](media/site-recovery-runbook-automation/04.png) em Olá ativos de automação do Azure e selecione![](media/site-recovery-runbook-automation/09.png)
2. Selecione o tipo de credencial hello como **credencial do Windows PowerShell**
3. Especifique nome hello como **AzureCredential**

   ![](media/site-recovery-runbook-automation/10.png)
4. Especifica Olá nome de usuário e senha toosign-em com.

Agora, essas duas configurações estão disponíveis em seus ativos.

![](media/site-recovery-runbook-automation/11.png)

Para obter mais informações sobre como tooconnect tooyour assinatura por meio do PowerShell é fornecida [aqui](/powershell/azure/overview).

Em seguida, você criará um runbook na automação do Azure que pode adicionar um ponto de extremidade da máquina virtual front-end de saudação após o failover.

## <a name="azure-automation-context"></a>Contexto de automação do Azure
ASR passa um toohelp do contexto toohello variável runbook gravar scripts determinísticas. Alguém poderia argumentar que nomes de saudação do hello serviço de nuvem e Olá Máquina Virtual são previsíveis, mas acontece que não é sempre caso Olá devido a cenários de toocertain como Olá um onde nome de saudação do nome da máquina virtual Olá pode ter sido alterado devido toounsupported caracteres no Azure. Portanto, essas informações são passadas toohello ASR plano de recuperação como parte da saudação *contexto*.

Abaixo está um exemplo da aparência de variável de contexto de saudação.

        {"RecoveryPlanName":"hrweb-recovery",

        "FailoverType":"Test",

        "FailoverDirection":"PrimaryToSecondary",

        "GroupId":"1",

        "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                {"CloudServiceName":"pod02hrweb-Chicago-test",

                "RoleName":"Fabrikam-Hrweb-frontend-test"}

                }

        }


tabela de saudação abaixo contém o nome e uma descrição para cada variável no contexto de saudação.

| **Nome da variável** | **Descrição** |
| --- | --- |
| RecoveryPlanName |Nome do plano de execução. Ajuda a você tomar uma ação com base no nome usando Olá mesmo script |
| FailoverType |Especifica se o failover Olá é testar, planejado ou não planejado. |
| FailoverDirection |Especifique se a recuperação é tooprimary ou secundário |
| GroupID |Identifique o número de grupo de saudação no plano de recuperação de saudação quando plano hello está em execução |
| VmMap |Matriz de todas as máquinas virtuais de saudação no grupo de saudação |
| Chave VMMap |Chave exclusiva (GUID) para cada VM. Ele tem Olá mesmas Olá VMM ID da máquina virtual de saudação onde aplicável. |
| RoleName |Nome da saudação VM do Azure que está sendo recuperado |
| CloudServiceName |Nome do serviço de nuvem do Azure, sob o qual Olá máquina virtual é criada. |

Olá tooidentify VmMap Key no contexto de saudação também poderia acesse a página de propriedades VM toohello em ASR e examinar Olá propriedade GUID da VM.

![](media/site-recovery-runbook-automation/13.png)

## <a name="author-an-automation-runbook"></a>Criar um runbook de automação
Agora crie Olá runbook tooopen a porta 80 em máquina virtual front-end de saudação.

1. Criar um novo runbook em Olá conta de automação do Azure com o nome da saudação **OpenPort80**

   ![](media/site-recovery-runbook-automation/14.png)
2. Navegue toohello exibição autor de runbook hello e entrar no modo de rascunho hello.
3. Primeiro, especifique toouse variável hello como contexto de plano de recuperação de saudação

   ```
       param (
           [Object]$RecoveryPlanContext
       )

   ```
4. Em seguida conectar toohello assinatura usando o nome de credencial e assinatura Olá

   ```
       $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

       # Connect tooAzure
       $AzureAccount = Add-AzureAccount -Credential $Cred
       $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
       Select-AzureSubscription -SubscriptionName $AzureSubscriptionName
   ```

   Observe que você usa hello Azure ativos – **AzureCredential** e **AzureSubscriptionName** aqui.
5. Agora especifique os detalhes do ponto de extremidade hello e Olá GUID da máquina virtual de saudação do qual você deseja que o ponto de extremidade de saudação tooexpose. Na saudação casos front-end da máquina virtual.

   ```
       # Specify hello parameters toobe used by hello script
       $AEProtocol = "TCP"
       $AELocalPort = 80
       $AEPublicPort = 80
       $AEName = "Port 80 for HTTP"
       $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"
   ```

   Isso especifica hello protocolo de ponto de extremidade do Azure, porta local Olá VM e sua porta pública mapeada. Essas variáveis são parâmetros exigidos pelo Olá comandos do Azure que adicionar tooVMs de pontos de extremidade. Olá VMGUID mantém Olá GUID da máquina virtual de saudação que precisar toooperate.
6. script Hello agora extrair contexto Olá Olá fornecido GUID da VM e criar um ponto de extremidade na máquina virtual de saudação referenciada por ele.

   ```
       #Read hello VM GUID from hello context
       $VM = $RecoveryPlanContext.VmMap.$VMGUID

       if ($VM -ne $null)
       {
           # Invoke pipeline commands within an InlineScript

           $EndpointStatus = InlineScript {
               # Invoke hello necessary pipeline commands tooadd a Azure Endpoint tooa specified Virtual Machine
               # Commands include: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including parameters)

               $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                   Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                   Update-AzureVM
               Write-Output $Status
           }
       }
   ```
7. Depois que isso for concluído, ocorrências publicar ![](media/site-recovery-runbook-automation/20.png) tooallow sua toobe de script disponível para execução.

script completo Olá é fornecido abaixo para sua referência

```
  workflow OpenPort80
  {
    param (
        [Object]$RecoveryPlanContext
    )

    $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

    # Connect tooAzure
    $AzureAccount = Add-AzureAccount -Credential $Cred
    $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
    Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

    # Specify hello parameters toobe used by hello script
    $AEProtocol = "TCP"
    $AELocalPort = 80
    $AEPublicPort = 80
    $AEName = "Port 80 for HTTP"
    $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"

    #Read hello VM GUID from hello context
    $VM = $RecoveryPlanContext.VmMap.$VMGUID

    if ($VM -ne $null)
    {
        # Invoke pipeline commands within an InlineScript

        $EndpointStatus = InlineScript {
            # Invoke hello necessary pipeline commands tooadd an Azure Endpoint tooa specified Virtual Machine
            # This set of commands includes: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including necessary parameters)

            $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                Update-AzureVM
            Write-Output $Status
        }
    }
  }
```

## <a name="add-hello-script-toohello-recovery-plan"></a>Adicionar um plano de recuperação Olá script toohello
Depois que o script hello estiver pronto, você pode adicionar toohello plano de recuperação que você criou anteriormente.

1. No plano de recuperação de saudação que você criou, escolha tooadd um script após o grupo 2. ![](media/site-recovery-runbook-automation/15.png)
2. Especifique um nome de script. Isso é apenas um nome amigável para este script para mostrar no plano de recuperação de saudação.
3. No script de tooAzure de failover hello – selecione o nome da conta de automação do Azure Olá.
4. No hello Runbooks do Azure, selecione Olá runbook criado por você.

![](media/site-recovery-runbook-automation/16.png)

## <a name="primary-side-scripts"></a>Scripts do lado principal
Quando você estiver executando um failover tooAzure, também é possível tooexecute scripts do lado primário. Esses scripts serão executados no servidor do VMM Olá durante o failover.
Scripts do lado principal só ficam disponíveis para estágios pré-desligamento e pós-desligamento. Isso ocorre porque espera-se que Olá site primário toobe normalmente não está disponível quando um desastre ocorrer.
Durante um failover não planejado, somente se você aceitar participar de operações do site primário, ele tentará scripts do toorun Olá lado primário. Se eles não estão acessíveis ou tempo limite, o failover de saudação continuarão toorecover Olá máquinas virtuais.
Scripts do lado primário estão não disponíveis para Sites VMware/físicos/Hyper-v sem tooAzure VMM protegido - ao tooAzure do failover.
No entanto, quando você failback de instalações do Azure tooon, scripts do lado primário (Runbooks) pode ser usado para todos os destinos, exceto o VMware.

## <a name="test-hello-recovery-plan"></a>Plano de recuperação de saudação do teste
Depois que você adicionou Olá runbook toohello plano, poderá iniciar um failover de teste e ver em ação. É sempre recomendável toorun um tootest de failover de teste sua tooensure de plano de recuperação de aplicativos e Olá que não existem erros.

1. Selecione o plano de recuperação de saudação e iniciar um failover de teste.
2. Durante a execução do plano de saudação, você pode ver se o runbook Olá foi executado ou não por meio de seu status.

   ![](media/site-recovery-runbook-automation/17.png)
3. Você também pode ver Olá detalhadas de status de execução de runbook na página de trabalhos de automação do Azure Olá Olá runbook.

   ![](media/site-recovery-runbook-automation/18.png)
4. Após a conclusão do failover hello, além de resultado da execução do runbook Olá, você pode ver se Olá execução for bem-sucedida ou não visitar a página de máquina virtual do Azure hello e olhando para pontos de extremidade de saudação.

![](media/site-recovery-runbook-automation/19.png)

## <a name="sample-scripts"></a>Exemplos de scripts
Enquanto percorremos automatizar um comumente usada tarefa de adicionar um ponto de extremidade tooan máquina virtual do Azure neste tutorial, você pode fazer um número de outras tarefas de automação avançada usando a automação do Azure. A Microsoft e Olá comunidade de automação do Azure fornecem runbooks de exemplo que podem ajudá-lo a começar a criar suas próprias soluções e runbooks do utilitário, que você pode usar como blocos de construção para tarefas de automação maior. Começar a usá-los na Galeria de saudação e criar planos de recuperação de um clique poderosa para seus aplicativos usando o Azure Site Recovery.

## <a name="additional-resources"></a>Recursos adicionais
[Visão geral da Automação](http://msdn.microsoft.com/library/azure/dn643629.aspx "Visão geral da Automação")

[Exemplos de scripts da Automação do Azure](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Exemplos de scripts da Automação do Azure")
