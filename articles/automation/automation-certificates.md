---
title: "ativos de aaaCertificate na automação do Azure | Microsoft Docs"
description: "Certificados podem ser armazenados com segurança na automação do Azure para que eles possam ser acessados por runbooks ou tooauthenticate de configurações DSC no Azure e os recursos de terceiros.  Este artigo explica detalhes de saudação de certificados e como toowork-los na criação de texto e gráfico."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: ac9c22ae-501f-42b9-9543-ac841cf2cc36
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/19/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 2c25bee937890438ea9022669be2c24c77a110b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="certificate-assets-in-azure-automation"></a>Ativos de certificado na Automação do Azure

Certificados podem ser armazenados com segurança na automação do Azure para que eles possam ser acessados por runbooks ou configurações de DSC usando Olá **AzureRmAutomationRmCertificate Get** atividade para recursos do Gerenciador de recursos do Azure. Isso permite que você toocreate runbooks e as configurações de DSC que usam certificados para autenticação ou adiciona recursos tooAzure ou de terceiros.

> [!NOTE] 
> Os ativos protegidos na Automação do Azure incluem credenciais, certificados, conexões e variáveis criptografadas. Esses ativos são criptografados e armazenados em Olá automação do Azure usando uma chave exclusiva que é gerada para cada conta de automação. Essa chave é criptografada por um certificado mestre e armazenada na Automação do Azure. Antes de armazenar um ativo seguro, chave Olá para conta de automação de saudação é descriptografado usando certificado mestre hello e usado tooencrypt ativo de saudação.
> 

## <a name="windows-powershell-cmdlets"></a>Cmdlets do Windows PowerShell

cmdlets Olá Olá a tabela a seguir são usada toocreate e gerenciar ativos de certificado de automação com o Windows PowerShell. Eles são fornecidos como parte da saudação [módulo Azure PowerShell](../powershell-install-configure.md) que está disponível para uso em runbooks de automação e configurações de DSC.

|Cmdlets|Descrição|
|:---|:---|
|[Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx)|Recupera informações sobre toouse um certificado em um runbook ou a configuração DSC. Você só pode recuperar o certificado de saudação da atividade de Get-AutomationCertificate.|
|[New-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603604.aspx)|Cria um novo certificado para a Automação do Azure.|
[Remove-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603529.aspx)|Remove um certificado da Automação do Azure.|Cria um novo certificado para a Automação do Azure.
|[Set-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603760.aspx)|Define as propriedades de saudação para um certificado existente, incluindo o carregamento de arquivo de certificado hello e a senha de saudação de configuração para um. pfx.|
|[Add-AzureCertificate](https://msdn.microsoft.com/library/azure/dn495214.aspx)|Carrega um serviço de certificado para Olá especificado serviço de nuvem.|


## <a name="creating-a-new-certificate"></a>Criando um novo certificado

Quando você cria um novo certificado, você pode carregar um tooAzure de arquivo. cer ou. pfx automação. Se você marcar certificado hello como exportável, você pode transferi-lo fora do repositório de certificados de automação do Azure hello. Se não for exportável, ele pode apenas ser usado para assinatura no runbook hello ou configuração de DSC.


### <a name="toocreate-a-new-certificate-with-hello-azure-portal"></a>toocreate um novo certificado com hello portal do Azure

1. Na sua conta de automação, clique em Olá **ativos** bloco tooopen Olá **ativos** folha.
1. Clique em Olá **certificados** bloco tooopen Olá **certificados** folha.
1. Clique em **adicionar um certificado** na parte superior de saudação da folha de saudação.
2. Digite um nome para o certificado de saudação Olá **nome** caixa.
2. Clique em **selecionar um arquivo** em **carregar um arquivo de certificado** toobrowse para um arquivo. cer ou. pfx.  Se você selecionar um arquivo. pfx, especifique uma senha e se ele deve ter permissão toobe exportado.
1. Clique em **criar** toosave Olá novo certificado ativo.


### <a name="toocreate-a-new-certificate-with-windows-powershell"></a>toocreate um novo certificado com o Windows PowerShell

Olá exemplo a seguir demonstra como toocreate automação uma novo certificado e marcá-la exportável. Isso importa um arquivo .pfx existente.

    $certName = 'MyCertificate'
    $certPath = '.\MyCert.pfx'
    $certPwd = ConvertTo-SecureString -String 'P@$$w0rd' -AsPlainText -Force
    $ResourceGroup = "ResourceGroup01"
    
    New-AzureRmAutomationCertificate -AutomationAccountName "MyAutomationAccount" -Name $certName -Path $certPath –Password $certPwd -Exportable -ResourceGroupName $ResourceGroup

## <a name="using-a-certificate"></a>Usando um certificado

Você deve usar o hello **Get-AutomationCertificate** toouse de atividade um certificado. Você não pode usar o hello [AzureRmAutomationCertificate Get](https://msdn.microsoft.com/library/mt603765.aspx) cmdlet desde que ele retorna informações sobre o ativo de certificado hello, mas não Olá próprio certificado.

### <a name="textual-runbook-sample"></a>Exemplo de runbook textual

Olá, código de exemplo a seguir mostra como o serviço em um runbook de nuvem tooadd tooa um certificado. Neste exemplo, a senha Olá é recuperada de uma variável de automação criptografada.

    $serviceName = 'MyCloudService'
    $cert = Get-AutomationCertificate -Name 'MyCertificate'
    $certPwd = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyCertPassword'
    Add-AzureCertificate -ServiceName $serviceName -CertToDeploy $cert

### <a name="graphical-runbook-sample"></a>Exemplo de runbook gráfico

Adicionar um **Get-AutomationCertificate** tooa runbook gráfico clicando no certificado de saudação no painel de biblioteca de saudação do editor gráfico hello e selecionando **adicionar toocanvas**.

![Adicionar certificado toohello tela](media/automation-certificates/automation-certificate-add-to-canvas.png)

Olá imagem a seguir mostra um exemplo de como usar um certificado em um runbook gráfico.  Isso é hello mesmo exemplo mostrado acima para adicionar um serviço de nuvem tooa certificado de um runbook textual.

![Exemplo de criação gráfica ](media/automation-certificates/graphical-runbook-add-certificate.png)


## <a name="next-steps"></a>Próximas etapas

- toolearn mais sobre como trabalhar com o fluxo lógico de saudação do toocontrol de links de atividades de runbook é projetado tooperform, consulte [Links no gráfico de criação](automation-graphical-authoring-intro.md#links-and-workflow). 
