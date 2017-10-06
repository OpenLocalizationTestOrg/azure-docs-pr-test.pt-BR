---
title: "AAA\"corrigir alertas VM do Azure com Runbooks de automação | Microsoft Docs\""
description: "Este artigo demonstra como toointegrate Máquina Virtual do Azure alertas com runbooks de automação do Azure e corrigir problemas"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 1f7baa7f-7283-4a4f-9385-3f5cd1062c7f
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/14/2016
ms.author: csand;magoedte
ms.openlocfilehash: c226368a5c4c51fbfb331f4b97f7f2f239e701c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---remediate-azure-vm-alerts"></a>Cenário de Automação do Azure - corrigir alertas de VM do Azure
Máquinas virtuais do Azure e automação do Azure ter lançado um novo recurso, permitindo que você runbooks de automação de toorun de alertas do tooconfigure Máquina Virtual (VM). Esse novo recurso permite que você tooautomatically executar a correção padrão em alertas de tooVM de resposta, como reiniciar ou interrupção Olá VM.

Anteriormente, durante a criação de regra de alerta de VM era possível muito[especificar um webhook de automação](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) runbook tooa em ordem toorun Olá runbook sempre que disparou o alerta de saudação. No entanto, isso necessário trabalho Olá toodo criando Olá runbook, criar webhook Olá Olá runbook, em seguida, copiar e colar Olá webhook durante a criação de regra de alerta. Com essa nova versão, o processo de saudação é muito mais fácil porque você pode escolher diretamente um runbook de uma lista durante a criação de regra de alerta, e você pode escolher uma conta de automação que irá executar o runbook hello ou criar facilmente uma conta.

Neste artigo, vamos mostrar como é fácil tooset se um alerta de VM do Azure e configurar um toorun de runbook de automação sempre que dispara o alerta de saudação. Cenários de exemplo incluem reiniciar uma máquina virtual quando o uso de memória de saudação excede o limite devido tooan aplicativo hello VM com um vazamento de memória ou parar uma máquina virtual quando o tempo do usuário Olá CPU foi abaixo de % 1 para hora anterior e não está em uso. Explicaremos também como Olá automatizado criação de uma entidade de serviço na sua automação conta simplifica o uso de saudação de runbooks na correção de alerta do Azure.

## <a name="create-an-alert-on-a-vm"></a>Criar um alerta em uma VM
Execute Olá etapas tooconfigure um alerta toolaunch um runbook a seguir ao seu limite foi atingido.

> [!NOTE]
> Com esta versão, damos suporte apenas a máquinas virtuais V2 e o suporte para VMs clássicas será adicionado em breve.  
> 
> 

1. Faça logon no portal do Azure de toohello e clique em **máquinas virtuais**.  
2. Selecione uma das máquinas virtuais.  Olá folha do painel de máquina virtual aparecerá e Olá **configurações** direita de tooits de folha.  
3. De saudação **configurações** folha sob Olá select de seção monitoramento **regras de alerta**.
4. Em Olá **regras de alerta** folha, clique em **adicionar alerta**.

Isso abre a saudação **adicionar uma regra de alerta** folha, onde você pode configurar condições de saudação do alerta hello e escolher entre uma ou todas essas opções: enviar email toosomeone, use um sistema de alerta tooanother webhook tooforward Olá, e/ou Execute um runbook de automação na edição de saudação de tooremediate de tentativa de resposta.

## <a name="configure-a-runbook"></a>Configurar um runbook
tooconfigure toorun um runbook quando o limite de alerta de VM Olá for atendida, selecione **Runbook de automação**. Em Olá **configurar runbook** folha, você pode selecionar Olá runbook toorun e Olá automação conta toorun Olá runbook no.

![Configurar um runbook de Automação e criar uma nova conta de Automação](media/automation-azure-vm-alert-integration/ConfigureRunbookNewAccount.png)

> [!NOTE]
> Para esta versão, você pode escolher entre três runbooks que fornece serviço hello – VM reiniciar, parar VM ou remover VM (excluir).  Olá capacidade tooselect outros runbooks ou um de seus próprios runbooks estará disponível em uma versão futura.
> 
> 

![Toochoose runbooks do](media/automation-azure-vm-alert-integration/RunbooksToChoose.png)

Depois de selecionar um dos runbooks disponíveis Olá três, Olá **conta de automação** lista suspensa é exibida e você pode selecionar um objeto de automação conta Olá runbook será executado como. Runbooks necessário toorun no contexto de saudação de um [conta de automação](automation-security-overview.md) que está em sua assinatura do Azure. Você pode selecionar uma conta de Automação que já criou ou pode ter uma nova conta de Automação criada para você.

Olá runbooks fornecidos autenticar tooAzure usando uma entidade de serviço. Se você escolher toorun Olá runbook em uma de suas contas de automação existentes, podemos criará automaticamente serviço Olá principal para você. Se você escolher uma nova conta de automação toocreate, em seguida, automaticamente criaremos conta hello e entidade de serviço hello. Em ambos os casos, os dois ativos também serão criados no hello conta de automação – um ativo de certificado chamado **AzureRunAsCertificate** e um ativo de conexão denominada **AzureRunAsConnection**. Olá runbooks usará **AzureRunAsConnection** tooauthenticate com o Azure na ação de gerenciamento de saudação ordem tooperform contra Olá VM.

> [!NOTE]
> entidade de serviço Olá é criada no escopo de assinatura de saudação e é atribuída a função de Colaborador hello. Essa função é necessária para que Olá conta toohave permissão toorun automação runbooks toomanage VMs do Azure.  criação de saudação de uma conta de automação e/ou entidade de serviço é um evento único. Quando eles são criados, você pode usar runbooks de toorun essa conta para outros alertas de VM do Azure.
> 
> 

Quando você clica em **Okey** Olá alerta está configurado e se você selecionou a opção de saudação toocreate uma nova conta de automação, ele será criado juntamente com a entidade de serviço hello.  Isso pode levar alguns segundos toocomplete.  

![Runbook sendo configurado](media/automation-azure-vm-alert-integration/RunbookBeingConfigured.png)

Após a configuração de saudação você verá Olá nome de runbook Olá aparecem no hello **adicionar uma regra de alerta** folha.

![Runbook configurado](media/automation-azure-vm-alert-integration/RunbookConfigured.png)

Clique em **Okey** em Olá **adicionar uma regra de alerta** regra de alerta de folha e hello será criado e ativado se a máquina virtual de saudação está em um estado de execução.

### <a name="enable-or-disable-a-runbook"></a>Habilitar ou desabilitar um runbook
Se você tiver um runbook configurado para um alerta, você pode desabilitá-lo sem remover a configuração de runbook hello. Isso permite tookeep alerta de saudação em execução e testar talvez algumas das regras de alerta hello e posteriormente reabilitá-Olá runbook.

## <a name="create-a-runbook-that-works-with-an-azure-alert"></a>Criar um runbook que funciona com um alerta do Azure
Quando você escolhe um runbook como parte de uma regra de alerta do Azure, Olá runbook precisa toohave lógica toomanage Olá dados de alerta que são passados tooit.  Quando um runbook é configurado em uma regra de alerta, um webhook é criado para Olá runbook; Esse webhook é então usado toostart Olá runbook cada gatilhos de alerta de saudação do tempo.  Olá chamada real toostart Olá runbook é uma URL de webhook de toohello de solicitação HTTP POST. corpo de saudação de solicitação POST Olá contém um objeto JSON formatado que contém propriedades úteis relacionados toohello alerta.  Como você pode ver abaixo, os dados de alerta de saudação contém detalhes como subscriptionID, resourceGroupName, resourceName e tipo de recurso.

### <a name="example-of-alert-data"></a>Exemplo de Dados de alerta
```
{
    "WebhookName": "AzureAlertTest",
    "RequestBody": "{
    \"status\":\"Activated\",
    \"context\": {
        \"id\":\"/subscriptions/<subscriptionId>/resourceGroups/MyResourceGroup/providers/microsoft.insights/alertrules/AlertTest\",
        \"name\":\"AlertTest\",
        \"description\":\"\",
        \"condition\": {
            \"metricName\":\"CPU percentage guest OS\",
            \"metricUnit\":\"Percent\",
            \"metricValue\":\"4.26337916666667\",
            \"threshold\":\"1\",
            \"windowSize\":\"60\",
            \"timeAggregation\":\"Average\",
            \"operator\":\"GreaterThan\"},
        \"subscriptionId\":\<subscriptionID> \",
        \"resourceGroupName\":\"TestResourceGroup\",
        \"timestamp\":\"2016-04-24T23:19:50.1440170Z\",
        \"resourceName\":\"TestVM\",
        \"resourceType\":\"microsoft.compute/virtualmachines\",
        \"resourceRegion\":\"westus\",
        \"resourceId\":\"/subscriptions/<subscriptionId>/resourceGroups/TestResourceGroup/providers/Microsoft.Compute/virtualMachines/TestVM\",
        \"portalLink\":\"https://portal.azure.com/#resource/subscriptions/<subscriptionId>/resourceGroups/TestResourceGroup/providers/Microsoft.Compute/virtualMachines/TestVM\"
        },
    \"properties\":{}
    }",
    "RequestHeader": {
        "Connection": "Keep-Alive",
        "Host": "<webhookURL>"
    }
}
```

Quando Olá serviço de webhook de automação recebe Olá HTTP POST ele extrai dados de alerta hello e passa toohello runbook no parâmetro de entrada hello WebhookData runbook.  Abaixo está um exemplo de runbook que mostra como toouse Olá WebhookData parâmetro e extrair dados de alerta hello e usá-lo toomanage Olá recursos do Azure que disparou o alerta de saudação.

### <a name="example-runbook"></a>Runbook de exemplo
```
#  This runbook will restart an ARM (V2) VM in response tooan Azure VM alert.

[OutputType("PSAzureOperationResponse")]

param ( [object] $WebhookData )

if ($WebhookData)
{
    # Get hello data object from WebhookData
    $WebhookBody = (ConvertFrom-Json -InputObject $WebhookData.RequestBody)

    # Assure that hello alert status is 'Activated' (alert condition went from false tootrue)
    # and not 'Resolved' (alert condition went from true toofalse)
    if ($WebhookBody.status -eq "Activated")
    {
        # Get hello info needed tooidentify hello VM
        $AlertContext = [object] $WebhookBody.context
        $ResourceName = $AlertContext.resourceName
        $ResourceType = $AlertContext.resourceType
        $ResourceGroupName = $AlertContext.resourceGroupName
        $SubId = $AlertContext.subscriptionId

        # Assure that this is hello expected resource type
        Write-Verbose "ResourceType: $ResourceType"
        if ($ResourceType -eq "microsoft.compute/virtualmachines")
        {
            # This is an ARM (V2) VM

            # Authenticate tooAzure with service principal and certificate
            $ConnectionAssetName = "AzureRunAsConnection"
            $Conn = Get-AutomationConnection -Name $ConnectionAssetName
            if ($Conn -eq $null) {
                throw "Could not retrieve connection asset: $ConnectionAssetName. Check that this asset exists in hello Automation account."
            }
            Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint | Write-Verbose
            Set-AzureRmContext -SubscriptionId $SubId -ErrorAction Stop | Write-Verbose

            # Restart hello VM
            Restart-AzureRmVM -Name $ResourceName -ResourceGroupName $ResourceGroupName
        } else {
            Write-Error "$ResourceType is not a supported resource type for this runbook."
        }
    } else {
        # hello alert status was not 'Activated' so no action taken
        Write-Verbose ("No action taken. Alert status: " + $WebhookBody.status)
    }
} else {
    Write-Error "This runbook is meant toobe started from an Azure alert only."
}
```

## <a name="summary"></a>Resumo
Quando você configurar um alerta em uma VM do Azure, agora você tem Olá capacidade tooeasily configurar uma automação de runbook tooautomatically executar a ação de correção ao alerta Olá gatilhos. Para esta versão, você pode escolher entre runbooks toorestart, interromper ou excluir uma VM dependendo do cenário de alerta. Este é o início de saudação apenas de habilitar cenários onde você pode controlar ações de saudação (notificação, solução de problemas, a correção) que serão executadas automaticamente quando dispara um alerta.

## <a name="next-steps"></a>Próximas etapas
* tooget iniciado com runbooks gráficos, consulte [meu primeiro runbook gráfico](automation-first-runbook-graphical.md)
* tooget iniciado com runbooks do fluxo de trabalho do PowerShell, consulte [meu primeiro runbook de fluxo de trabalho do PowerShell](automation-first-runbook-textual.md)
* toolearn mais sobre os tipos de runbook, suas vantagens e limitações, consulte [tipos de runbook de automação do Azure](automation-runbook-types.md)

