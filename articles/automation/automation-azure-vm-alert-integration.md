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
# <a name="azure-automation-scenario---remediate-azure-vm-alerts"></a><span data-ttu-id="837f6-103">Cenário de Automação do Azure - corrigir alertas de VM do Azure</span><span class="sxs-lookup"><span data-stu-id="837f6-103">Azure Automation scenario - remediate Azure VM alerts</span></span>
<span data-ttu-id="837f6-104">Máquinas virtuais do Azure e automação do Azure ter lançado um novo recurso, permitindo que você runbooks de automação de toorun de alertas do tooconfigure Máquina Virtual (VM).</span><span class="sxs-lookup"><span data-stu-id="837f6-104">Azure Automation and Azure Virtual Machines have released a new feature allowing you tooconfigure Virtual Machine (VM) alerts toorun Automation runbooks.</span></span> <span data-ttu-id="837f6-105">Esse novo recurso permite que você tooautomatically executar a correção padrão em alertas de tooVM de resposta, como reiniciar ou interrupção Olá VM.</span><span class="sxs-lookup"><span data-stu-id="837f6-105">This new capability allows you tooautomatically perform standard remediation in response tooVM alerts, like restarting or stopping hello VM.</span></span>

<span data-ttu-id="837f6-106">Anteriormente, durante a criação de regra de alerta de VM era possível muito[especificar um webhook de automação](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) runbook tooa em ordem toorun Olá runbook sempre que disparou o alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="837f6-106">Previously, during VM alert rule creation you were able too[specify an Automation webhook](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) tooa runbook in order toorun hello runbook whenever hello alert triggered.</span></span> <span data-ttu-id="837f6-107">No entanto, isso necessário trabalho Olá toodo criando Olá runbook, criar webhook Olá Olá runbook, em seguida, copiar e colar Olá webhook durante a criação de regra de alerta.</span><span class="sxs-lookup"><span data-stu-id="837f6-107">However, this required you toodo hello work of creating hello runbook, creating hello webhook for hello runbook, and then copying and pasting hello webhook during alert rule creation.</span></span> <span data-ttu-id="837f6-108">Com essa nova versão, o processo de saudação é muito mais fácil porque você pode escolher diretamente um runbook de uma lista durante a criação de regra de alerta, e você pode escolher uma conta de automação que irá executar o runbook hello ou criar facilmente uma conta.</span><span class="sxs-lookup"><span data-stu-id="837f6-108">With this new release, hello process is much easier because you can directly choose a runbook from a list during alert rule creation, and you can choose an Automation account which will run hello runbook or easily create an account.</span></span>

<span data-ttu-id="837f6-109">Neste artigo, vamos mostrar como é fácil tooset se um alerta de VM do Azure e configurar um toorun de runbook de automação sempre que dispara o alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="837f6-109">In this article, we will show you how easy it is tooset up an Azure VM alert and configure an Automation runbook toorun whenever hello alert triggers.</span></span> <span data-ttu-id="837f6-110">Cenários de exemplo incluem reiniciar uma máquina virtual quando o uso de memória de saudação excede o limite devido tooan aplicativo hello VM com um vazamento de memória ou parar uma máquina virtual quando o tempo do usuário Olá CPU foi abaixo de % 1 para hora anterior e não está em uso.</span><span class="sxs-lookup"><span data-stu-id="837f6-110">Example scenarios include restarting a VM when hello memory usage exceeds some threshold due tooan application on hello VM with a memory leak, or stopping a VM when hello CPU user time has been below 1% for past hour and is not in use.</span></span> <span data-ttu-id="837f6-111">Explicaremos também como Olá automatizado criação de uma entidade de serviço na sua automação conta simplifica o uso de saudação de runbooks na correção de alerta do Azure.</span><span class="sxs-lookup"><span data-stu-id="837f6-111">We’ll also explain how hello automated creation of a service principal in your Automation account simplifies hello use of runbooks in Azure alert remediation.</span></span>

## <a name="create-an-alert-on-a-vm"></a><span data-ttu-id="837f6-112">Criar um alerta em uma VM</span><span class="sxs-lookup"><span data-stu-id="837f6-112">Create an alert on a VM</span></span>
<span data-ttu-id="837f6-113">Execute Olá etapas tooconfigure um alerta toolaunch um runbook a seguir ao seu limite foi atingido.</span><span class="sxs-lookup"><span data-stu-id="837f6-113">Perform hello following steps tooconfigure an alert toolaunch a runbook when its threshold has been met.</span></span>

> [!NOTE]
> <span data-ttu-id="837f6-114">Com esta versão, damos suporte apenas a máquinas virtuais V2 e o suporte para VMs clássicas será adicionado em breve.</span><span class="sxs-lookup"><span data-stu-id="837f6-114">With this release, we only support V2 virtual machines and support for classic VMs will be added soon.</span></span>  
> 
> 

1. <span data-ttu-id="837f6-115">Faça logon no portal do Azure de toohello e clique em **máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="837f6-115">Log in toohello Azure portal and click **Virtual Machines**.</span></span>  
2. <span data-ttu-id="837f6-116">Selecione uma das máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="837f6-116">Select one of your virtual machines.</span></span>  <span data-ttu-id="837f6-117">Olá folha do painel de máquina virtual aparecerá e Olá **configurações** direita de tooits de folha.</span><span class="sxs-lookup"><span data-stu-id="837f6-117">hello virtual machine dashboard blade will appear and hello **Settings** blade tooits right.</span></span>  
3. <span data-ttu-id="837f6-118">De saudação **configurações** folha sob Olá select de seção monitoramento **regras de alerta**.</span><span class="sxs-lookup"><span data-stu-id="837f6-118">From hello **Settings** blade, under hello Monitoring section select **Alert rules**.</span></span>
4. <span data-ttu-id="837f6-119">Em Olá **regras de alerta** folha, clique em **adicionar alerta**.</span><span class="sxs-lookup"><span data-stu-id="837f6-119">On hello **Alert rules** blade, click **Add alert**.</span></span>

<span data-ttu-id="837f6-120">Isso abre a saudação **adicionar uma regra de alerta** folha, onde você pode configurar condições de saudação do alerta hello e escolher entre uma ou todas essas opções: enviar email toosomeone, use um sistema de alerta tooanother webhook tooforward Olá, e/ou Execute um runbook de automação na edição de saudação de tooremediate de tentativa de resposta.</span><span class="sxs-lookup"><span data-stu-id="837f6-120">This opens up hello **Add an alert rule** blade, where you can configure hello conditions for hello alert and choose among one or all of these options: send email toosomeone, use a webhook tooforward hello alert tooanother system, and/or run an Automation runbook in response attempt tooremediate hello issue.</span></span>

## <a name="configure-a-runbook"></a><span data-ttu-id="837f6-121">Configurar um runbook</span><span class="sxs-lookup"><span data-stu-id="837f6-121">Configure a runbook</span></span>
<span data-ttu-id="837f6-122">tooconfigure toorun um runbook quando o limite de alerta de VM Olá for atendida, selecione **Runbook de automação**.</span><span class="sxs-lookup"><span data-stu-id="837f6-122">tooconfigure a runbook toorun when hello VM alert threshold is met, select **Automation Runbook**.</span></span> <span data-ttu-id="837f6-123">Em Olá **configurar runbook** folha, você pode selecionar Olá runbook toorun e Olá automação conta toorun Olá runbook no.</span><span class="sxs-lookup"><span data-stu-id="837f6-123">In hello **Configure runbook** blade, you can select hello runbook toorun and hello Automation account toorun hello runbook in.</span></span>

![Configurar um runbook de Automação e criar uma nova conta de Automação](media/automation-azure-vm-alert-integration/ConfigureRunbookNewAccount.png)

> [!NOTE]
> <span data-ttu-id="837f6-125">Para esta versão, você pode escolher entre três runbooks que fornece serviço hello – VM reiniciar, parar VM ou remover VM (excluir).</span><span class="sxs-lookup"><span data-stu-id="837f6-125">For this release you can choose from three runbooks that hello service provides – Restart VM, Stop VM, or Remove VM (delete it).</span></span>  <span data-ttu-id="837f6-126">Olá capacidade tooselect outros runbooks ou um de seus próprios runbooks estará disponível em uma versão futura.</span><span class="sxs-lookup"><span data-stu-id="837f6-126">hello ability tooselect other runbooks or one of your own runbooks will be available in a future release.</span></span>
> 
> 

![Toochoose runbooks do](media/automation-azure-vm-alert-integration/RunbooksToChoose.png)

<span data-ttu-id="837f6-128">Depois de selecionar um dos runbooks disponíveis Olá três, Olá **conta de automação** lista suspensa é exibida e você pode selecionar um objeto de automação conta Olá runbook será executado como.</span><span class="sxs-lookup"><span data-stu-id="837f6-128">After you select one of hello three available runbooks, hello **Automation account** drop-down list appears and you can select an automation account hello runbook will run as.</span></span> <span data-ttu-id="837f6-129">Runbooks necessário toorun no contexto de saudação de um [conta de automação](automation-security-overview.md) que está em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="837f6-129">Runbooks need toorun in hello context of an [Automation account](automation-security-overview.md) that is in your Azure subscription.</span></span> <span data-ttu-id="837f6-130">Você pode selecionar uma conta de Automação que já criou ou pode ter uma nova conta de Automação criada para você.</span><span class="sxs-lookup"><span data-stu-id="837f6-130">You can select an Automation account that you already created, or you can have a new Automation account created for you.</span></span>

<span data-ttu-id="837f6-131">Olá runbooks fornecidos autenticar tooAzure usando uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="837f6-131">hello runbooks that are provided authenticate tooAzure using a service principal.</span></span> <span data-ttu-id="837f6-132">Se você escolher toorun Olá runbook em uma de suas contas de automação existentes, podemos criará automaticamente serviço Olá principal para você.</span><span class="sxs-lookup"><span data-stu-id="837f6-132">If you choose toorun hello runbook in one of your existing Automation accounts, we will automatically create hello service principal for you.</span></span> <span data-ttu-id="837f6-133">Se você escolher uma nova conta de automação toocreate, em seguida, automaticamente criaremos conta hello e entidade de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="837f6-133">If you choose toocreate a new Automation account, then we will automatically create hello account and hello service principal.</span></span> <span data-ttu-id="837f6-134">Em ambos os casos, os dois ativos também serão criados no hello conta de automação – um ativo de certificado chamado **AzureRunAsCertificate** e um ativo de conexão denominada **AzureRunAsConnection**.</span><span class="sxs-lookup"><span data-stu-id="837f6-134">In both cases, two assets will also be created in hello Automation account – a certificate asset named **AzureRunAsCertificate** and a connection asset named **AzureRunAsConnection**.</span></span> <span data-ttu-id="837f6-135">Olá runbooks usará **AzureRunAsConnection** tooauthenticate com o Azure na ação de gerenciamento de saudação ordem tooperform contra Olá VM.</span><span class="sxs-lookup"><span data-stu-id="837f6-135">hello runbooks will use **AzureRunAsConnection** tooauthenticate with Azure in order tooperform hello management action against hello VM.</span></span>

> [!NOTE]
> <span data-ttu-id="837f6-136">entidade de serviço Olá é criada no escopo de assinatura de saudação e é atribuída a função de Colaborador hello.</span><span class="sxs-lookup"><span data-stu-id="837f6-136">hello service principal is created in hello subscription scope and is assigned hello Contributor role.</span></span> <span data-ttu-id="837f6-137">Essa função é necessária para que Olá conta toohave permissão toorun automação runbooks toomanage VMs do Azure.</span><span class="sxs-lookup"><span data-stu-id="837f6-137">This role is required in order for hello account toohave permission toorun Automation runbooks toomanage Azure VMs.</span></span>  <span data-ttu-id="837f6-138">criação de saudação de uma conta de automação e/ou entidade de serviço é um evento único.</span><span class="sxs-lookup"><span data-stu-id="837f6-138">hello creation of an Automaton account and/or service principal is a one-time event.</span></span> <span data-ttu-id="837f6-139">Quando eles são criados, você pode usar runbooks de toorun essa conta para outros alertas de VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="837f6-139">Once they are created, you can use that account toorun runbooks for other Azure VM alerts.</span></span>
> 
> 

<span data-ttu-id="837f6-140">Quando você clica em **Okey** Olá alerta está configurado e se você selecionou a opção de saudação toocreate uma nova conta de automação, ele será criado juntamente com a entidade de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="837f6-140">When you click **OK** hello alert is configured and if you selected hello option toocreate a new Automation account, it is created along with hello service principal.</span></span>  <span data-ttu-id="837f6-141">Isso pode levar alguns segundos toocomplete.</span><span class="sxs-lookup"><span data-stu-id="837f6-141">This can take a few seconds toocomplete.</span></span>  

![Runbook sendo configurado](media/automation-azure-vm-alert-integration/RunbookBeingConfigured.png)

<span data-ttu-id="837f6-143">Após a configuração de saudação você verá Olá nome de runbook Olá aparecem no hello **adicionar uma regra de alerta** folha.</span><span class="sxs-lookup"><span data-stu-id="837f6-143">After hello configuration is completed you will see hello name of hello runbook appear in hello **Add an alert rule** blade.</span></span>

![Runbook configurado](media/automation-azure-vm-alert-integration/RunbookConfigured.png)

<span data-ttu-id="837f6-145">Clique em **Okey** em Olá **adicionar uma regra de alerta** regra de alerta de folha e hello será criado e ativado se a máquina virtual de saudação está em um estado de execução.</span><span class="sxs-lookup"><span data-stu-id="837f6-145">Click **OK** in hello **Add an alert rule** blade and hello alert rule will be created and activate if hello virtual machine is in a running state.</span></span>

### <a name="enable-or-disable-a-runbook"></a><span data-ttu-id="837f6-146">Habilitar ou desabilitar um runbook</span><span class="sxs-lookup"><span data-stu-id="837f6-146">Enable or disable a runbook</span></span>
<span data-ttu-id="837f6-147">Se você tiver um runbook configurado para um alerta, você pode desabilitá-lo sem remover a configuração de runbook hello.</span><span class="sxs-lookup"><span data-stu-id="837f6-147">If you have a runbook configured for an alert, you can disable it without removing hello runbook configuration.</span></span> <span data-ttu-id="837f6-148">Isso permite tookeep alerta de saudação em execução e testar talvez algumas das regras de alerta hello e posteriormente reabilitá-Olá runbook.</span><span class="sxs-lookup"><span data-stu-id="837f6-148">This allows you tookeep hello alert running and perhaps test some of hello alert rules and then later re-enable hello runbook.</span></span>

## <a name="create-a-runbook-that-works-with-an-azure-alert"></a><span data-ttu-id="837f6-149">Criar um runbook que funciona com um alerta do Azure</span><span class="sxs-lookup"><span data-stu-id="837f6-149">Create a runbook that works with an Azure alert</span></span>
<span data-ttu-id="837f6-150">Quando você escolhe um runbook como parte de uma regra de alerta do Azure, Olá runbook precisa toohave lógica toomanage Olá dados de alerta que são passados tooit.</span><span class="sxs-lookup"><span data-stu-id="837f6-150">When you choose a runbook as part of an Azure alert rule, hello runbook needs toohave logic in it toomanage hello alert data that is passed tooit.</span></span>  <span data-ttu-id="837f6-151">Quando um runbook é configurado em uma regra de alerta, um webhook é criado para Olá runbook; Esse webhook é então usado toostart Olá runbook cada gatilhos de alerta de saudação do tempo.</span><span class="sxs-lookup"><span data-stu-id="837f6-151">When a runbook is configured in an alert rule, a webhook is created for hello runbook; that webhook is then used toostart hello runbook each time hello alert triggers.</span></span>  <span data-ttu-id="837f6-152">Olá chamada real toostart Olá runbook é uma URL de webhook de toohello de solicitação HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="837f6-152">hello actual call toostart hello runbook is an HTTP POST request toohello webhook URL.</span></span> <span data-ttu-id="837f6-153">corpo de saudação de solicitação POST Olá contém um objeto JSON formatado que contém propriedades úteis relacionados toohello alerta.</span><span class="sxs-lookup"><span data-stu-id="837f6-153">hello body of hello POST request contains a JSON-formated object that contains useful properties related toohello alert.</span></span>  <span data-ttu-id="837f6-154">Como você pode ver abaixo, os dados de alerta de saudação contém detalhes como subscriptionID, resourceGroupName, resourceName e tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="837f6-154">As you can see below, hello alert data contains details like subscriptionID, resourceGroupName, resourceName, and resourceType.</span></span>

### <a name="example-of-alert-data"></a><span data-ttu-id="837f6-155">Exemplo de Dados de alerta</span><span class="sxs-lookup"><span data-stu-id="837f6-155">Example of Alert data</span></span>
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

<span data-ttu-id="837f6-156">Quando Olá serviço de webhook de automação recebe Olá HTTP POST ele extrai dados de alerta hello e passa toohello runbook no parâmetro de entrada hello WebhookData runbook.</span><span class="sxs-lookup"><span data-stu-id="837f6-156">When hello Automation webhook service receives hello HTTP POST it extracts hello alert data and passes it toohello runbook in hello WebhookData runbook input parameter.</span></span>  <span data-ttu-id="837f6-157">Abaixo está um exemplo de runbook que mostra como toouse Olá WebhookData parâmetro e extrair dados de alerta hello e usá-lo toomanage Olá recursos do Azure que disparou o alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="837f6-157">Below is a sample runbook that shows how toouse hello WebhookData parameter and extract hello alert data and use it toomanage hello Azure resource that triggered hello alert.</span></span>

### <a name="example-runbook"></a><span data-ttu-id="837f6-158">Runbook de exemplo</span><span class="sxs-lookup"><span data-stu-id="837f6-158">Example runbook</span></span>
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

## <a name="summary"></a><span data-ttu-id="837f6-159">Resumo</span><span class="sxs-lookup"><span data-stu-id="837f6-159">Summary</span></span>
<span data-ttu-id="837f6-160">Quando você configurar um alerta em uma VM do Azure, agora você tem Olá capacidade tooeasily configurar uma automação de runbook tooautomatically executar a ação de correção ao alerta Olá gatilhos.</span><span class="sxs-lookup"><span data-stu-id="837f6-160">When you configure an alert on an Azure VM, you now have hello ability tooeasily configure an Automation runbook tooautomatically perform remediation action when hello alert triggers.</span></span> <span data-ttu-id="837f6-161">Para esta versão, você pode escolher entre runbooks toorestart, interromper ou excluir uma VM dependendo do cenário de alerta.</span><span class="sxs-lookup"><span data-stu-id="837f6-161">For this release, you can choose from runbooks toorestart, stop, or delete a VM depending on your alert scenario.</span></span> <span data-ttu-id="837f6-162">Este é o início de saudação apenas de habilitar cenários onde você pode controlar ações de saudação (notificação, solução de problemas, a correção) que serão executadas automaticamente quando dispara um alerta.</span><span class="sxs-lookup"><span data-stu-id="837f6-162">This is just hello beginning of enabling scenarios where you control hello actions (notification, troubleshooting, remediation) that will be taken automatically when an alert triggers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="837f6-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="837f6-163">Next Steps</span></span>
* <span data-ttu-id="837f6-164">tooget iniciado com runbooks gráficos, consulte [meu primeiro runbook gráfico](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="837f6-164">tooget started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span>
* <span data-ttu-id="837f6-165">tooget iniciado com runbooks do fluxo de trabalho do PowerShell, consulte [meu primeiro runbook de fluxo de trabalho do PowerShell](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="837f6-165">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="837f6-166">toolearn mais sobre os tipos de runbook, suas vantagens e limitações, consulte [tipos de runbook de automação do Azure](automation-runbook-types.md)</span><span class="sxs-lookup"><span data-stu-id="837f6-166">toolearn more about runbook types, their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md)</span></span>

