---
title: " Corrigir Alertas da VM do Azure com Runbooks de Automação | Microsoft Docs"
description: "Este artigo demonstra como integrar os alertas de Máquina Virtual do Azure com runbooks de Automação do Azure e corrigir automaticamente os problemas"
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
ms.openlocfilehash: 738959b8e1ee5da989bb996d1ce8148cbf912781
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario---remediate-azure-vm-alerts"></a><span data-ttu-id="0d3a9-103">Cenário de Automação do Azure - corrigir alertas de VM do Azure</span><span class="sxs-lookup"><span data-stu-id="0d3a9-103">Azure Automation scenario - remediate Azure VM alerts</span></span>
<span data-ttu-id="0d3a9-104">As Máquinas Virtuais do Azure e a Automação do Azure lançaram um novo recurso que permite que você configure os alertas de VM (Máquina Virtual) para executar runbooks de Automação.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-104">Azure Automation and Azure Virtual Machines have released a new feature allowing you to configure Virtual Machine (VM) alerts to run Automation runbooks.</span></span> <span data-ttu-id="0d3a9-105">Essa nova funcionalidade permite que você execute a correção standard automaticamente em resposta a alertas de VM, como reiniciar ou parar a VM.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-105">This new capability allows you to automatically perform standard remediation in response to VM alerts, like restarting or stopping the VM.</span></span>

<span data-ttu-id="0d3a9-106">Anteriormente, durante a criação de regra de alerta de VM você podia [especificar um webhook de Automação](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) para um runbook para executar o runbook sempre que o alerta fosse disparado.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-106">Previously, during VM alert rule creation you were able to [specify an Automation webhook](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) to a runbook in order to run the runbook whenever the alert triggered.</span></span> <span data-ttu-id="0d3a9-107">No entanto, isso exigia que você realizasse o trabalho de criar o runbook, criar o webhook para o runbook e, em seguida, copiasse e colasse o webhook durante a criação da regra de alerta.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-107">However, this required you to do the work of creating the runbook, creating the webhook for the runbook, and then copying and pasting the webhook during alert rule creation.</span></span> <span data-ttu-id="0d3a9-108">Com essa nova versão, o processo é muito mais fácil, porque você pode escolher diretamente um runbook em uma lista durante a criação da regra de alerta e pode escolher uma conta de Automação que executará o runbook ou facilmente criar uma conta.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-108">With this new release, the process is much easier because you can directly choose a runbook from a list during alert rule creation, and you can choose an Automation account which will run the runbook or easily create an account.</span></span>

<span data-ttu-id="0d3a9-109">Neste artigo, mostraremos como é fácil configurar um alerta de VM do Azure e configurar um runbook de Automação para ser executado sempre que o alerta for disparado.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-109">In this article, we will show you how easy it is to set up an Azure VM alert and configure an Automation runbook to run whenever the alert triggers.</span></span> <span data-ttu-id="0d3a9-110">Os cenários de exemplo incluem reiniciar uma VM quando o uso de memória exceder algum limite devido a um aplicativo na VM com um vazamento de memória ou parar uma VM quando o tempo de usuário da CPU foi abaixo de 1% na hora anterior e não está em uso.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-110">Example scenarios include restarting a VM when the memory usage exceeds some threshold due to an application on the VM with a memory leak, or stopping a VM when the CPU user time has been below 1% for past hour and is not in use.</span></span> <span data-ttu-id="0d3a9-111">Explicaremos também como a criação automatizada de uma entidade de serviço em sua conta de Automação simplifica o uso de runbooks na correção de alerta do Azure.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-111">We’ll also explain how the automated creation of a service principal in your Automation account simplifies the use of runbooks in Azure alert remediation.</span></span>

## <a name="create-an-alert-on-a-vm"></a><span data-ttu-id="0d3a9-112">Criar um alerta em uma VM</span><span class="sxs-lookup"><span data-stu-id="0d3a9-112">Create an alert on a VM</span></span>
<span data-ttu-id="0d3a9-113">Execute as seguintes etapas para configurar um alerta para iniciar um runbook quando o limite for atingido.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-113">Perform the following steps to configure an alert to launch a runbook when its threshold has been met.</span></span>

> [!NOTE]
> <span data-ttu-id="0d3a9-114">Com esta versão, damos suporte apenas a máquinas virtuais V2 e o suporte para VMs clássicas será adicionado em breve.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-114">With this release, we only support V2 virtual machines and support for classic VMs will be added soon.</span></span>  
> 
> 

1. <span data-ttu-id="0d3a9-115">Faça logon no portal do Azure e clique em **Máquinas Virtuais**.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-115">Log in to the Azure portal and click **Virtual Machines**.</span></span>  
2. <span data-ttu-id="0d3a9-116">Selecione uma das máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-116">Select one of your virtual machines.</span></span>  <span data-ttu-id="0d3a9-117">A folha do painel da máquina virtual será exibida e a folha **Configurações** à sua direita.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-117">The virtual machine dashboard blade will appear and the **Settings** blade to its right.</span></span>  
3. <span data-ttu-id="0d3a9-118">Na folha **Configurações**, na seção Monitoramento, selecione **Regras de alerta**.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-118">From the **Settings** blade, under the Monitoring section select **Alert rules**.</span></span>
4. <span data-ttu-id="0d3a9-119">Na folha **Regras de alerta**, clique em **Adicionar alerta**.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-119">On the **Alert rules** blade, click **Add alert**.</span></span>

<span data-ttu-id="0d3a9-120">Isso abrirá a folha **Adicionar uma regra de alerta** , na qual você pode configurar as condições para o alerta e escolher entre uma ou todas essas opções: enviar email para alguém, use um webhook para encaminhar o alerta para outro sistema de e/ou executar um runbook de Automação na tentativa de resposta para corrigir o problema.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-120">This opens up the **Add an alert rule** blade, where you can configure the conditions for the alert and choose among one or all of these options: send email to someone, use a webhook to forward the alert to another system, and/or run an Automation runbook in response attempt to remediate the issue.</span></span>

## <a name="configure-a-runbook"></a><span data-ttu-id="0d3a9-121">Configurar um runbook</span><span class="sxs-lookup"><span data-stu-id="0d3a9-121">Configure a runbook</span></span>
<span data-ttu-id="0d3a9-122">Para configurar um runbook para ser executado quando o limite de alerta da VM for atingido, selecione **Runbook de Automação**.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-122">To configure a runbook to run when the VM alert threshold is met, select **Automation Runbook**.</span></span> <span data-ttu-id="0d3a9-123">Na folha **Configurar runbook** , você pode selecionar o runbook para ser executado e a conta de Automação na qual executar o runbook.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-123">In the **Configure runbook** blade, you can select the runbook to run and the Automation account to run the runbook in.</span></span>

![Configurar um runbook de Automação e criar uma nova conta de Automação](media/automation-azure-vm-alert-integration/ConfigureRunbookNewAccount.png)

> [!NOTE]
> <span data-ttu-id="0d3a9-125">Para esta versão, você pode escolher entre três runbooks que o serviço fornece: Reiniciar VM, Parar VM ou Remover VM (excluí-la).</span><span class="sxs-lookup"><span data-stu-id="0d3a9-125">For this release you can choose from three runbooks that the service provides – Restart VM, Stop VM, or Remove VM (delete it).</span></span>  <span data-ttu-id="0d3a9-126">A capacidade de selecionar outros runbooks ou um de seus próprios runbooks estará disponível em uma versão futura.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-126">The ability to select other runbooks or one of your own runbooks will be available in a future release.</span></span>
> 
> 

![Runbooks dentre os quais escolher](media/automation-azure-vm-alert-integration/RunbooksToChoose.png)

<span data-ttu-id="0d3a9-128">Depois de selecionar um dos três runbooks disponíveis, a lista suspensa **Conta de Automação** é exibida e você pode selecionar uma conta de automação como a qual o runbook será executado.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-128">After you select one of the three available runbooks, the **Automation account** drop-down list appears and you can select an automation account the runbook will run as.</span></span> <span data-ttu-id="0d3a9-129">Os runbooks precisam ser executados no contexto de uma [Conta de Automação](automation-security-overview.md) que esteja na sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-129">Runbooks need to run in the context of an [Automation account](automation-security-overview.md) that is in your Azure subscription.</span></span> <span data-ttu-id="0d3a9-130">Você pode selecionar uma conta de Automação que já criou ou pode ter uma nova conta de Automação criada para você.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-130">You can select an Automation account that you already created, or you can have a new Automation account created for you.</span></span>

<span data-ttu-id="0d3a9-131">Os runbooks fornecidos se autenticam no Azure usando uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-131">The runbooks that are provided authenticate to Azure using a service principal.</span></span> <span data-ttu-id="0d3a9-132">Se você optar por executar o runbook em uma de suas contas de Automação existentes, criaremos automaticamente a entidade de serviço para você.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-132">If you choose to run the runbook in one of your existing Automation accounts, we will automatically create the service principal for you.</span></span> <span data-ttu-id="0d3a9-133">Se você optar por criar uma nova conta de Automação, criaremos automaticamente a conta e a entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-133">If you choose to create a new Automation account, then we will automatically create the account and the service principal.</span></span> <span data-ttu-id="0d3a9-134">Em ambos os casos, os dois ativos também serão criados na conta de Automação – um ativo de certificado denominado **AzureRunAsCertificate** e um ativo de conexão denominado **AzureRunAsConnection**.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-134">In both cases, two assets will also be created in the Automation account – a certificate asset named **AzureRunAsCertificate** and a connection asset named **AzureRunAsConnection**.</span></span> <span data-ttu-id="0d3a9-135">Os runbooks usarão o **AzureRunAsConnection** para se autenticar com o Azure para executar a ação de gerenciamento na VM.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-135">The runbooks will use **AzureRunAsConnection** to authenticate with Azure in order to perform the management action against the VM.</span></span>

> [!NOTE]
> <span data-ttu-id="0d3a9-136">A entidade de serviço é criada no escopo de assinatura e é atribuída à função de Colaborador.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-136">The service principal is created in the subscription scope and is assigned the Contributor role.</span></span> <span data-ttu-id="0d3a9-137">Essa função é necessária para a conta ter permissão para executar runbooks de Automação para gerenciar VMs do Azure.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-137">This role is required in order for the account to have permission to run Automation runbooks to manage Azure VMs.</span></span>  <span data-ttu-id="0d3a9-138">A criação de uma conta de Automação e/ou entidade de serviço é um evento único.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-138">The creation of an Automaton account and/or service principal is a one-time event.</span></span> <span data-ttu-id="0d3a9-139">Depois que elas forem criadas, você poderá usar essa conta para executar runbooks para outros alertas de VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-139">Once they are created, you can use that account to run runbooks for other Azure VM alerts.</span></span>
> 
> 

<span data-ttu-id="0d3a9-140">Quando você clica em **OK** , o alerta é configurado e, se você selecionou a opção para criar uma nova conta de automação, ela é criada junto com a entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-140">When you click **OK** the alert is configured and if you selected the option to create a new Automation account, it is created along with the service principal.</span></span>  <span data-ttu-id="0d3a9-141">Isso pode levar alguns segundos para ser concluído.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-141">This can take a few seconds to complete.</span></span>  

![Runbook sendo configurado](media/automation-azure-vm-alert-integration/RunbookBeingConfigured.png)

<span data-ttu-id="0d3a9-143">Após a configuração ser concluída, você verá o nome do runbook aparecer na folha **Adicionar uma regra de alerta** .</span><span class="sxs-lookup"><span data-stu-id="0d3a9-143">After the configuration is completed you will see the name of the runbook appear in the **Add an alert rule** blade.</span></span>

![Runbook configurado](media/automation-azure-vm-alert-integration/RunbookConfigured.png)

<span data-ttu-id="0d3a9-145">Clique em **OK** in the **Adicionar uma regra de alerta** e a regra de alerta será criada e ativada se a máquina virtual estiver em estado de execução.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-145">Click **OK** in the **Add an alert rule** blade and the alert rule will be created and activate if the virtual machine is in a running state.</span></span>

### <a name="enable-or-disable-a-runbook"></a><span data-ttu-id="0d3a9-146">Habilitar ou desabilitar um runbook</span><span class="sxs-lookup"><span data-stu-id="0d3a9-146">Enable or disable a runbook</span></span>
<span data-ttu-id="0d3a9-147">Se você tiver um runbook configurado para um alerta, poderá desabilitá-lo sem remover a configuração do runbook.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-147">If you have a runbook configured for an alert, you can disable it without removing the runbook configuration.</span></span> <span data-ttu-id="0d3a9-148">Isso permite que você mantenha o alerta em execução e talvez teste algumas das regras de alerta e depois habilite novamente o runbook.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-148">This allows you to keep the alert running and perhaps test some of the alert rules and then later re-enable the runbook.</span></span>

## <a name="create-a-runbook-that-works-with-an-azure-alert"></a><span data-ttu-id="0d3a9-149">Criar um runbook que funciona com um alerta do Azure</span><span class="sxs-lookup"><span data-stu-id="0d3a9-149">Create a runbook that works with an Azure alert</span></span>
<span data-ttu-id="0d3a9-150">Quando você escolhe um runbook como parte de uma regra de alerta do Azure, o runbook deve conter lógica para gerenciar os dados de alerta que são passados para ele.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-150">When you choose a runbook as part of an Azure alert rule, the runbook needs to have logic in it to manage the alert data that is passed to it.</span></span>  <span data-ttu-id="0d3a9-151">Quando um runbook é configurado em uma regra de alerta, um Webhook é criado para o runbook; esse Webhook, em seguida, é usado para iniciar o runbook toda vez o alerta é disparado.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-151">When a runbook is configured in an alert rule, a webhook is created for the runbook; that webhook is then used to start the runbook each time the alert triggers.</span></span>  <span data-ttu-id="0d3a9-152">A chamada real para iniciar o runbook é uma solicitação HTTP POST para a URL do Webhook.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-152">The actual call to start the runbook is an HTTP POST request to the webhook URL.</span></span> <span data-ttu-id="0d3a9-153">O corpo da solicitação POST contém um objeto com o formato JSON que contém propriedades úteis relacionadas ao alerta.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-153">The body of the POST request contains a JSON-formated object that contains useful properties related to the alert.</span></span>  <span data-ttu-id="0d3a9-154">Como você pode ver abaixo, os dados de alerta contém detalhes como subscriptionID, resourceGroupName, resourceName e resourceType.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-154">As you can see below, the alert data contains details like subscriptionID, resourceGroupName, resourceName, and resourceType.</span></span>

### <a name="example-of-alert-data"></a><span data-ttu-id="0d3a9-155">Exemplo de Dados de alerta</span><span class="sxs-lookup"><span data-stu-id="0d3a9-155">Example of Alert data</span></span>
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

<span data-ttu-id="0d3a9-156">Quando o serviço de Automação de Webhook recebe o HTTP POST, ele extrai os dados de alerta e passa-os para o runbook no parâmetro de entrada de runbook WebhookData.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-156">When the Automation webhook service receives the HTTP POST it extracts the alert data and passes it to the runbook in the WebhookData runbook input parameter.</span></span>  <span data-ttu-id="0d3a9-157">Abaixo está um exemplo de runbook que mostra como usar o parâmetro WebhookData, extrair os dados de alerta e usá-lo para gerenciar os recursos do Azure que disparou o alerta.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-157">Below is a sample runbook that shows how to use the WebhookData parameter and extract the alert data and use it to manage the Azure resource that triggered the alert.</span></span>

### <a name="example-runbook"></a><span data-ttu-id="0d3a9-158">Runbook de exemplo</span><span class="sxs-lookup"><span data-stu-id="0d3a9-158">Example runbook</span></span>
```
#  This runbook will restart an ARM (V2) VM in response to an Azure VM alert.

[OutputType("PSAzureOperationResponse")]

param ( [object] $WebhookData )

if ($WebhookData)
{
    # Get the data object from WebhookData
    $WebhookBody = (ConvertFrom-Json -InputObject $WebhookData.RequestBody)

    # Assure that the alert status is 'Activated' (alert condition went from false to true)
    # and not 'Resolved' (alert condition went from true to false)
    if ($WebhookBody.status -eq "Activated")
    {
        # Get the info needed to identify the VM
        $AlertContext = [object] $WebhookBody.context
        $ResourceName = $AlertContext.resourceName
        $ResourceType = $AlertContext.resourceType
        $ResourceGroupName = $AlertContext.resourceGroupName
        $SubId = $AlertContext.subscriptionId

        # Assure that this is the expected resource type
        Write-Verbose "ResourceType: $ResourceType"
        if ($ResourceType -eq "microsoft.compute/virtualmachines")
        {
            # This is an ARM (V2) VM

            # Authenticate to Azure with service principal and certificate
            $ConnectionAssetName = "AzureRunAsConnection"
            $Conn = Get-AutomationConnection -Name $ConnectionAssetName
            if ($Conn -eq $null) {
                throw "Could not retrieve connection asset: $ConnectionAssetName. Check that this asset exists in the Automation account."
            }
            Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint | Write-Verbose
            Set-AzureRmContext -SubscriptionId $SubId -ErrorAction Stop | Write-Verbose

            # Restart the VM
            Restart-AzureRmVM -Name $ResourceName -ResourceGroupName $ResourceGroupName
        } else {
            Write-Error "$ResourceType is not a supported resource type for this runbook."
        }
    } else {
        # The alert status was not 'Activated' so no action taken
        Write-Verbose ("No action taken. Alert status: " + $WebhookBody.status)
    }
} else {
    Write-Error "This runbook is meant to be started from an Azure alert only."
}
```

## <a name="summary"></a><span data-ttu-id="0d3a9-159">Resumo</span><span class="sxs-lookup"><span data-stu-id="0d3a9-159">Summary</span></span>
<span data-ttu-id="0d3a9-160">Quando você configura um alerta em uma VM do Azure, agora você tem a capacidade de configurar facilmente um runbook de Automação para executar a ação de correção automaticamente quando o alerta for disparado.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-160">When you configure an alert on an Azure VM, you now have the ability to easily configure an Automation runbook to automatically perform remediation action when the alert triggers.</span></span> <span data-ttu-id="0d3a9-161">Para esta versão, você pode escolher dentre runbooks para reiniciar, parar ou excluir uma VM dependendo do cenário de alerta.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-161">For this release, you can choose from runbooks to restart, stop, or delete a VM depending on your alert scenario.</span></span> <span data-ttu-id="0d3a9-162">Isso é apenas o começo da habilitação de cenários em que você controla as ações (notificação, solução de problemas, correção) que serão executadas automaticamente quando um alerta for disparado.</span><span class="sxs-lookup"><span data-stu-id="0d3a9-162">This is just the beginning of enabling scenarios where you control the actions (notification, troubleshooting, remediation) that will be taken automatically when an alert triggers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d3a9-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0d3a9-163">Next Steps</span></span>
* <span data-ttu-id="0d3a9-164">Para começar a usar runbooks gráficos, veja [O meu primeiro runbook gráfico](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="0d3a9-164">To get started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span>
* <span data-ttu-id="0d3a9-165">Para começar a usar os runbooks de fluxo de trabalho do PowerShell, confira [Meu primeiro runbook de fluxo de trabalho do PowerShell](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="0d3a9-165">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="0d3a9-166">Para saber mais sobre os tipos de runbook, suas vantagens e limitações, veja [Tipos de runbook da Automação do Azure](automation-runbook-types.md)</span><span class="sxs-lookup"><span data-stu-id="0d3a9-166">To learn more about runbook types, their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md)</span></span>

