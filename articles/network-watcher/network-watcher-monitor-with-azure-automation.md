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
# <a name="monitor-vpn-gateways-with-network-watcher-troubleshooting"></a>Monitorar os gateways de VPN com a solução de problemas do Observador de Rede

Obter informações sobre o desempenho de rede é crítico tooprovide serviços confiáveis toocustomers. É, portanto, toodetect crítico condições de interrupção de rede rapidamente e levar a condição de interrupção de saudação de toomitigate ação corretiva. Automação do Azure permite que você tooimplement e executar uma tarefa de modo programático por meio de runbooks. Usar a Automação do Azure cria uma receita perfeita para realizar um monitoramento contínuo e proativo da rede e alertas.

## <a name="scenario"></a>Cenário

cenário Olá Olá a imagem a seguir é um aplicativo de várias camadas, com conectividade local estabelecida usando um Gateway de VPN e túnel. Garantindo Olá que gateway de VPN está ativo e em execução são o desempenho de aplicativos críticos toohello.

Um runbook é criado com um toocheck de script para o status de conexão do túnel VPN hello, usando Olá toocheck de API de recursos de solução de problemas para status do túnel de conexão. Se o status de saudação não está íntegro, um gatilho de email é enviado tooadministrators.

![Cenário de exemplo][scenario]

Este cenário:

- Criar uma saudação chamada runbook `Start-AzureRmNetworkWatcherResourceTroubleshooting` status de conexão do cmdlet tootroubleshoot
- Vincula um runbook toohello de agenda

## <a name="before-you-begin"></a>Antes de começar

Antes de começar este cenário, você deve ter Olá os pré-requisitos a seguir:

- uma conta de automação no Azure. Verifique se o conta de automação de saudação tem mais recentes de módulos hello e também tem o módulo de AzureRM.Network hello. Olá AzureRM.Network módulo está disponível na Galeria de módulo Olá se você precisar tooadd-tooyour conta de automação.
- deve ter um conjunto de credenciais configurado na Automação do Azure. Saiba mais em [Segurança da Automação do Azure](../automation/automation-security-overview.md)
- Um servidor SMTP válido (Office 365, seu email local ou outro) e credenciais definidas na Automação do Azure
- Um Gateway de Rede Virtual configurado no Azure.
- Uma conta de armazenamento existente com uma saudação de toostore contêiner existente fizer logon.

> [!NOTE]
> infraestrutura de Olá descrita nos Olá anterior a imagem é para fins ilustrativos e não são criados com etapas Olá contidas neste artigo.

### <a name="create-hello-runbook"></a>Criar hello runbook

exemplo de saudação do Hello primeira etapa tooconfiguring é toocreate Olá runbook. Este exemplo usa uma conta do tipo executar como. toolearn sobre contas executar como, visite [Runbooks autenticar com a conta executar como do Azure](../automation/automation-sec-configure-azure-runas-account.md)

### <a name="step-1"></a>Etapa 1

Navegue tooAzure automação em Olá [portal do Azure](https://portal.azure.com) e clique em **Runbooks**

![visão geral da conta de automação][1]

### <a name="step-2"></a>Etapa 2

Clique em **adicionar um runbook** toostart processo de criação de saudação do runbook Olá.

![folha de runbooks][2]

### <a name="step-3"></a>Etapa 3

Em **criação rápida**, clique em **criar um novo runbook** toocreate Olá runbook.

![adicionar uma folha de runbook][3]

### <a name="step-4"></a>Etapa 4

Nesta etapa, fornecemos Olá runbook um nome, no exemplo hello, ele é chamado **Get-VPNGatewayStatus**. Ele é importante toogive Olá runbook um nome descritivo e recomendável dar a ele um nome que segue os padrões de nomenclatura padrão do PowerShell. saudação de tipo de runbook para este exemplo é **PowerShell**, hello, outras opções são gráfico, o fluxo de trabalho do PowerShell e o fluxo de trabalho do PowerShell gráfica.

![folha de runbook][4]

### <a name="step-5"></a>Etapa 5

Nesta etapa hello runbook é criado, Olá exemplo de código a seguir fornece que todos os Olá código necessário para o exemplo hello. Olá itens no código de saudação que contêm \<valor\> necessário toobe substituído por valores de saudação da sua assinatura.

Código a seguir de saudação de uso como **salvar**

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

### <a name="step-6"></a>Etapa 6

Uma vez Olá runbook é salvo, uma agenda deve ser vinculado tooit tooautomate Olá início Olá runbook. processo de saudação toostart, clique em **agenda**.

![Etapa 6][6]

## <a name="link-a-schedule-toohello-runbook"></a>Vincula um runbook toohello de agenda

Deve ser criada uma nova agenda. Clique em **vincula um runbook do agendamento tooyour**.

![Etapa 7][7]

### <a name="step-1"></a>Etapa 1

Em Olá **agenda** folha, clique em **criar uma nova agenda**

![Etapa 8][8]

### <a name="step-2"></a>Etapa 2

Em Olá **nova agenda** folha preencher informações de agenda hello. valores de saudação que podem ser definidos são em Olá lista a seguir:

- **Nome** -nome amigável de saudação da agenda de saudação.
- **Descrição** -uma descrição da agenda de saudação.
- **Inicia** -esse valor é uma combinação de data, hora e fuso horário que compõem Olá Olá agenda disparadores agendados.
- **Recorrência** -este valor determina Olá agendas repetição.  Os valores válidos são **Uma vez** ou **Recorrente**.
- **Repetir a cada** -intervalo de recorrência de saudação da agenda de saudação em horas, dias, semanas ou meses.
- **Validade do conjunto** -valor Olá determina se a agenda de saudação deverá expirar ou não. Pode ser definido muito**Sim** ou **não**. Uma data e hora válidas são toobe fornecido se Sim for escolhida.

> [!NOTE]
> Se você precisar toohave um runbook executado com mais frequência do que a cada hora, várias agendas devem ser criadas em intervalos diferentes (ou seja, 15, 30, 45 minutos após a hora de saudação)

![Etapa 9][9]

### <a name="step-3"></a>Etapa 3

Clique em Salvar toosave Olá agenda toohello runbook.

![Etapa 10][10]

## <a name="next-steps"></a>Próximas etapas

Agora que você tenha um entendimento sobre como toointegrate Solucionando problemas do observador de rede com a automação do Azure, saiba como o pacote tootrigger captura alertas VM visitando [criar uma captura de pacote de disparo de alerta com o observador de rede do Azure](network-watcher-alert-triggered-packet-capture.md).

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
