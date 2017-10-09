---
title: "aaaMonitor gateways VPN com a solução de problemas do observador de rede do Azure | Microsoft Docs"
description: "Este artigo descreve como diagnosticar a conectividade local com a Automação e o Observador de Rede do Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: a607d0c862ea1be63c687717f0c5dc137db58a43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-vpn-gateways-with-network-watcher-troubleshooting"></a><span data-ttu-id="4ce7e-103">Monitorar os gateways de VPN com a solução de problemas do Observador de Rede</span><span class="sxs-lookup"><span data-stu-id="4ce7e-103">Monitor VPN gateways with Network Watcher troubleshooting</span></span>

<span data-ttu-id="4ce7e-104">Obter informações sobre o desempenho de rede é crítico tooprovide serviços confiáveis toocustomers.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-104">Gaining deep insights on your network performance is critical tooprovide reliable services toocustomers.</span></span> <span data-ttu-id="4ce7e-105">É, portanto, toodetect crítico condições de interrupção de rede rapidamente e levar a condição de interrupção de saudação de toomitigate ação corretiva.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-105">It is therefore critical toodetect network outage conditions quickly and take corrective action toomitigate hello outage condition.</span></span> <span data-ttu-id="4ce7e-106">Automação do Azure permite que você tooimplement e executar uma tarefa de modo programático por meio de runbooks.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-106">Azure Automation enables you tooimplement and run a task in a programmatic fashion through runbooks.</span></span> <span data-ttu-id="4ce7e-107">Usar a Automação do Azure cria uma receita perfeita para realizar um monitoramento contínuo e proativo da rede e alertas.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-107">Using Azure Automation creates a perfect recipe for performing continuous and proactive network monitoring and alerting.</span></span>

## <a name="scenario"></a><span data-ttu-id="4ce7e-108">Cenário</span><span class="sxs-lookup"><span data-stu-id="4ce7e-108">Scenario</span></span>

<span data-ttu-id="4ce7e-109">cenário Olá Olá a imagem a seguir é um aplicativo de várias camadas, com conectividade local estabelecida usando um Gateway de VPN e túnel.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-109">hello scenario in hello following image is a multi-tiered application, with on premises connectivity established using a VPN Gateway and tunnel.</span></span> <span data-ttu-id="4ce7e-110">Garantindo Olá que gateway de VPN está ativo e em execução são o desempenho de aplicativos críticos toohello.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-110">Ensuring hello VPN Gateway is up and running is critical toohello applications performance.</span></span>

<span data-ttu-id="4ce7e-111">Um runbook é criado com um toocheck de script para o status de conexão do túnel VPN hello, usando Olá toocheck de API de recursos de solução de problemas para status do túnel de conexão.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-111">A runbook is created with a script toocheck for connection status of hello VPN tunnel, using hello Resource Troubleshooting API toocheck for connection tunnel status.</span></span> <span data-ttu-id="4ce7e-112">Se o status de saudação não está íntegro, um gatilho de email é enviado tooadministrators.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-112">If hello status is not healthy, an email trigger is sent tooadministrators.</span></span>

![Cenário de exemplo][scenario]

<span data-ttu-id="4ce7e-114">Este cenário:</span><span class="sxs-lookup"><span data-stu-id="4ce7e-114">This scenario will:</span></span>

- <span data-ttu-id="4ce7e-115">Criar uma saudação chamada runbook `Start-AzureRmNetworkWatcherResourceTroubleshooting` status de conexão do cmdlet tootroubleshoot</span><span class="sxs-lookup"><span data-stu-id="4ce7e-115">Create a runbook calling hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet tootroubleshoot connection status</span></span>
- <span data-ttu-id="4ce7e-116">Vincula um runbook toohello de agenda</span><span class="sxs-lookup"><span data-stu-id="4ce7e-116">Link a schedule toohello runbook</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4ce7e-117">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="4ce7e-117">Before you begin</span></span>

<span data-ttu-id="4ce7e-118">Antes de começar este cenário, você deve ter Olá os pré-requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ce7e-118">Before you start this scenario, you must have hello following pre-requisites:</span></span>

- <span data-ttu-id="4ce7e-119">uma conta de automação no Azure.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-119">An Azure automation account in Azure.</span></span> <span data-ttu-id="4ce7e-120">Verifique se o conta de automação de saudação tem mais recentes de módulos hello e também tem o módulo de AzureRM.Network hello.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-120">Ensure that hello automation account has hello latest modules and also has hello AzureRM.Network module.</span></span> <span data-ttu-id="4ce7e-121">Olá AzureRM.Network módulo está disponível na Galeria de módulo Olá se você precisar tooadd-tooyour conta de automação.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-121">hello AzureRM.Network module is available in hello module gallery if you need tooadd it tooyour automation account.</span></span>
- <span data-ttu-id="4ce7e-122">deve ter um conjunto de credenciais configurado na Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-122">You must have a set of credentials configure in Azure Automation.</span></span> <span data-ttu-id="4ce7e-123">Saiba mais em [Segurança da Automação do Azure](../automation/automation-security-overview.md)</span><span class="sxs-lookup"><span data-stu-id="4ce7e-123">Learn more at [Azure Automation security](../automation/automation-security-overview.md)</span></span>
- <span data-ttu-id="4ce7e-124">Um servidor SMTP válido (Office 365, seu email local ou outro) e credenciais definidas na Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="4ce7e-124">A valid SMTP server (Office 365, your on-premises email or another) and credentials defined in Azure Automation</span></span>
- <span data-ttu-id="4ce7e-125">Um Gateway de Rede Virtual configurado no Azure.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-125">A configured Virtual Network Gateway in Azure.</span></span>
- <span data-ttu-id="4ce7e-126">Uma conta de armazenamento existente com uma saudação de toostore contêiner existente fizer logon.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-126">An existing storage account with an existing container toostore hello logs in.</span></span>

> [!NOTE]
> <span data-ttu-id="4ce7e-127">infraestrutura de Olá descrita nos Olá anterior a imagem é para fins ilustrativos e não são criados com etapas Olá contidas neste artigo.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-127">hello infrastructure depicted in hello preceding image is for illustration purposes and are not created with hello steps contained in this article.</span></span>

### <a name="create-hello-runbook"></a><span data-ttu-id="4ce7e-128">Criar hello runbook</span><span class="sxs-lookup"><span data-stu-id="4ce7e-128">Create hello runbook</span></span>

<span data-ttu-id="4ce7e-129">exemplo de saudação do Hello primeira etapa tooconfiguring é toocreate Olá runbook.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-129">hello first step tooconfiguring hello example is toocreate hello runbook.</span></span> <span data-ttu-id="4ce7e-130">Este exemplo usa uma conta do tipo executar como.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-130">This example uses a run-as account.</span></span> <span data-ttu-id="4ce7e-131">toolearn sobre contas executar como, visite [Runbooks autenticar com a conta executar como do Azure](../automation/automation-sec-configure-azure-runas-account.md)</span><span class="sxs-lookup"><span data-stu-id="4ce7e-131">toolearn about run-as accounts, visit [Authenticate Runbooks with Azure Run As account](../automation/automation-sec-configure-azure-runas-account.md)</span></span>

### <a name="step-1"></a><span data-ttu-id="4ce7e-132">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="4ce7e-132">Step 1</span></span>

<span data-ttu-id="4ce7e-133">Navegue tooAzure automação em Olá [portal do Azure](https://portal.azure.com) e clique em **Runbooks**</span><span class="sxs-lookup"><span data-stu-id="4ce7e-133">Navigate tooAzure Automation in hello [Azure portal](https://portal.azure.com) and click **Runbooks**</span></span>

![visão geral da conta de automação][1]

### <a name="step-2"></a><span data-ttu-id="4ce7e-135">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="4ce7e-135">Step 2</span></span>

<span data-ttu-id="4ce7e-136">Clique em **adicionar um runbook** toostart processo de criação de saudação do runbook Olá.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-136">Click **Add a runbook** toostart hello creation process of hello runbook.</span></span>

![folha de runbooks][2]

### <a name="step-3"></a><span data-ttu-id="4ce7e-138">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="4ce7e-138">Step 3</span></span>

<span data-ttu-id="4ce7e-139">Em **criação rápida**, clique em **criar um novo runbook** toocreate Olá runbook.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-139">Under **Quick Create**, click **Create a new runbook** toocreate hello runbook.</span></span>

![adicionar uma folha de runbook][3]

### <a name="step-4"></a><span data-ttu-id="4ce7e-141">Etapa 4</span><span class="sxs-lookup"><span data-stu-id="4ce7e-141">Step 4</span></span>

<span data-ttu-id="4ce7e-142">Nesta etapa, fornecemos Olá runbook um nome, no exemplo hello, ele é chamado **Get-VPNGatewayStatus**.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-142">In this step, we give hello runbook a name, in hello example it is called **Get-VPNGatewayStatus**.</span></span> <span data-ttu-id="4ce7e-143">Ele é importante toogive Olá runbook um nome descritivo e recomendável dar a ele um nome que segue os padrões de nomenclatura padrão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-143">It is important toogive hello runbook a descriptive name, and recommended giving it a name that follows standard PowerShell naming standards.</span></span> <span data-ttu-id="4ce7e-144">saudação de tipo de runbook para este exemplo é **PowerShell**, hello, outras opções são gráfico, o fluxo de trabalho do PowerShell e o fluxo de trabalho do PowerShell gráfica.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-144">hello runbook type for this example is **PowerShell**, hello other options are Graphical, PowerShell workflow, and Graphical PowerShell workflow.</span></span>

![folha de runbook][4]

### <a name="step-5"></a><span data-ttu-id="4ce7e-146">Etapa 5</span><span class="sxs-lookup"><span data-stu-id="4ce7e-146">Step 5</span></span>

<span data-ttu-id="4ce7e-147">Nesta etapa hello runbook é criado, Olá exemplo de código a seguir fornece que todos os Olá código necessário para o exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-147">In this step hello runbook is created, hello following code example provides all hello code needed for hello example.</span></span> <span data-ttu-id="4ce7e-148">Olá itens no código de saudação que contêm \<valor\> necessário toobe substituído por valores de saudação da sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-148">hello items in hello code that contain \<value\> need toobe replaced with hello values from your subscription.</span></span>

<span data-ttu-id="4ce7e-149">Código a seguir de saudação de uso como **salvar**</span><span class="sxs-lookup"><span data-stu-id="4ce7e-149">Use hello following code as click **Save**</span></span>

```PowerShell
# Set these variables toohello proper values for your environment
$o365AutomationCredential = "<Office 365 account>"
$fromEmail = "<from email address>"
$toEmail = "<tooemail address>"
$smtpServer = "<smtp.office365.com>"
$smtpPort = 587
$runAsConnectionName = "<AzureRunAsConnection>"
$subscriptionId = "<subscription id>"
$region = "<Azure region>"
$vpnConnectionName = "<vpn connection name>"
$vpnConnectionResourceGroup = "<resource group name>"
$storageAccountName = "<storage account name>"
$storageAccountResourceGroup = "<resource group name>"
$storageAccountContainer = "<container name>"

# Get credentials for Office 365 account
$cred = Get-AutomationPSCredential -Name $o365AutomationCredential

# Get hello connection "AzureRunAsConnection "
$servicePrincipalConnection=Get-AutomationConnection -Name $runAsConnectionName

"Logging in tooAzure..."
Add-AzureRmAccount `
    -ServicePrincipal `
    -TenantId $servicePrincipalConnection.TenantId `
    -ApplicationId $servicePrincipalConnection.ApplicationId `
    -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
"Setting context tooa specific subscription"
Set-AzureRmContext -SubscriptionId $subscriptionId

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $region }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name $vpnConnectionName -ResourceGroupName $vpnConnectionResourceGroup
$sa = Get-AzureRmStorageAccount -Name $storageAccountName -ResourceGroupName $storageAccountResourceGroup 
$storagePath = "$($sa.PrimaryEndpoints.Blob)$($storageAccountContainer)"
$result = Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath $storagePath

if($result.code -ne "Healthy")
    {
        $body = "Connection for $($connection.name) is: $($result.code) `n$($result.results[0].summary) `nView hello logs at $($storagePath) toolearn more."
        Write-Output $body
        $subject = "$($connection.name) Status"
        Send-MailMessage `
        -too$toEmail `
        -Subject $subject `
        -Body $body `
        -UseSsl `
        -Port $smtpPort `
        -SmtpServer $smtpServer `
        -From $fromEmail `
        -BodyAsHtml `
        -Credential $cred
    }
else
    {
    Write-Output ("Connection Status is: $($result.code)")
    }
```

### <a name="step-6"></a><span data-ttu-id="4ce7e-150">Etapa 6</span><span class="sxs-lookup"><span data-stu-id="4ce7e-150">Step 6</span></span>

<span data-ttu-id="4ce7e-151">Uma vez Olá runbook é salvo, uma agenda deve ser vinculado tooit tooautomate Olá início Olá runbook.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-151">Once hello runbook is saved, a schedule must be linked tooit tooautomate hello start of hello runbook.</span></span> <span data-ttu-id="4ce7e-152">processo de saudação toostart, clique em **agenda**.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-152">toostart hello process, click **Schedule**.</span></span>

![Etapa 6][6]

## <a name="link-a-schedule-toohello-runbook"></a><span data-ttu-id="4ce7e-154">Vincula um runbook toohello de agenda</span><span class="sxs-lookup"><span data-stu-id="4ce7e-154">Link a schedule toohello runbook</span></span>

<span data-ttu-id="4ce7e-155">Deve ser criada uma nova agenda.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-155">A new schedule must be created.</span></span> <span data-ttu-id="4ce7e-156">Clique em **vincula um runbook do agendamento tooyour**.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-156">Click **Link a schedule tooyour runbook**.</span></span>

![Etapa 7][7]

### <a name="step-1"></a><span data-ttu-id="4ce7e-158">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="4ce7e-158">Step 1</span></span>

<span data-ttu-id="4ce7e-159">Em Olá **agenda** folha, clique em **criar uma nova agenda**</span><span class="sxs-lookup"><span data-stu-id="4ce7e-159">On hello **Schedule** blade, click **Create a new schedule**</span></span>

![Etapa 8][8]

### <a name="step-2"></a><span data-ttu-id="4ce7e-161">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="4ce7e-161">Step 2</span></span>

<span data-ttu-id="4ce7e-162">Em Olá **nova agenda** folha preencher informações de agenda hello.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-162">On hello **New Schedule** blade fill out hello schedule information.</span></span> <span data-ttu-id="4ce7e-163">valores de saudação que podem ser definidos são em Olá lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ce7e-163">hello values that can be set are in hello following list:</span></span>

- <span data-ttu-id="4ce7e-164">**Nome** -nome amigável de saudação da agenda de saudação.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-164">**Name** - hello friendly name of hello schedule.</span></span>
- <span data-ttu-id="4ce7e-165">**Descrição** -uma descrição da agenda de saudação.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-165">**Description** - A description of hello schedule.</span></span>
- <span data-ttu-id="4ce7e-166">**Inicia** -esse valor é uma combinação de data, hora e fuso horário que compõem Olá Olá agenda disparadores agendados.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-166">**Starts** - This value is a combination of date, time, and time zone that make up hello time hello schedule triggers.</span></span>
- <span data-ttu-id="4ce7e-167">**Recorrência** -este valor determina Olá agendas repetição.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-167">**Recurrence** - This value determines hello schedules repetition.</span></span>  <span data-ttu-id="4ce7e-168">Os valores válidos são **Uma vez** ou **Recorrente**.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-168">Valid values are **Once** or **Recurring**.</span></span>
- <span data-ttu-id="4ce7e-169">**Repetir a cada** -intervalo de recorrência de saudação da agenda de saudação em horas, dias, semanas ou meses.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-169">**Recur every** - hello recurrence interval of hello schedule in hours, days, weeks, or months.</span></span>
- <span data-ttu-id="4ce7e-170">**Validade do conjunto** -valor Olá determina se a agenda de saudação deverá expirar ou não.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-170">**Set Expiration** - hello value determines if hello schedule should expire or not.</span></span> <span data-ttu-id="4ce7e-171">Pode ser definido muito**Sim** ou **não**.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-171">Can be set too**Yes** or **No**.</span></span> <span data-ttu-id="4ce7e-172">Uma data e hora válidas são toobe fornecido se Sim for escolhida.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-172">A valid date and time are toobe provided if yes is chosen.</span></span>

> [!NOTE]
> <span data-ttu-id="4ce7e-173">Se você precisar toohave um runbook executado com mais frequência do que a cada hora, várias agendas devem ser criadas em intervalos diferentes (ou seja, 15, 30, 45 minutos após a hora de saudação)</span><span class="sxs-lookup"><span data-stu-id="4ce7e-173">If you need toohave a runbook run more often than every hour, multiple schedules must be created at different intervals (that is, 15, 30, 45 minutes after hello hour)</span></span>

![Etapa 9][9]

### <a name="step-3"></a><span data-ttu-id="4ce7e-175">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="4ce7e-175">Step 3</span></span>

<span data-ttu-id="4ce7e-176">Clique em Salvar toosave Olá agenda toohello runbook.</span><span class="sxs-lookup"><span data-stu-id="4ce7e-176">Click Save toosave hello schedule toohello runbook.</span></span>

![Etapa 10][10]

## <a name="next-steps"></a><span data-ttu-id="4ce7e-178">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4ce7e-178">Next steps</span></span>

<span data-ttu-id="4ce7e-179">Agora que você tenha um entendimento sobre como toointegrate Solucionando problemas do observador de rede com a automação do Azure, saiba como o pacote tootrigger captura alertas VM visitando [criar uma captura de pacote de disparo de alerta com o observador de rede do Azure](network-watcher-alert-triggered-packet-capture.md).</span><span class="sxs-lookup"><span data-stu-id="4ce7e-179">Now that you have an understanding on how toointegrate Network Watcher troubleshooting with Azure Automation, learn how tootrigger packet captures on VM alerts by visiting [Create an alert triggered packet capture with Azure Network Watcher](network-watcher-alert-triggered-packet-capture.md).</span></span>

<!-- images -->
[scenario]: ./media/network-watcher-monitor-with-azure-automation/scenario.png
[1]: ./media/network-watcher-monitor-with-azure-automation/figure1.png
[2]: ./media/network-watcher-monitor-with-azure-automation/figure2.png
[3]: ./media/network-watcher-monitor-with-azure-automation/figure3.png
[4]: ./media/network-watcher-monitor-with-azure-automation/figure4.png
[5]: ./media/network-watcher-monitor-with-azure-automation/figure5.png
[6]: ./media/network-watcher-monitor-with-azure-automation/figure6.png
[7]: ./media/network-watcher-monitor-with-azure-automation/figure7.png
[8]: ./media/network-watcher-monitor-with-azure-automation/figure8.png
[9]: ./media/network-watcher-monitor-with-azure-automation/figure9.png
[10]: ./media/network-watcher-monitor-with-azure-automation/figure10.png
