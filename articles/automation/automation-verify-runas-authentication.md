---
title: "configuração de conta de automação do Azure aaaValidate | Microsoft Docs"
description: "Este artigo descreve como configuração de saudação tooconfirm de sua conta de automação está configurado corretamente."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: magoedte
ms.openlocfilehash: 3a990dcc6661cf67c4b62592ce03d55a3791053a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="test-azure-automation-run-as-account-authentication"></a>Como testar a autenticação da conta Executar como de Automação do Azure
Depois que uma conta de automação é criada com êxito, você pode executar um tooconfirm de teste simples que você é capaz de autenticar o toosuccessfully no Gerenciador de recursos do Azure ou implantação clássica do Azure usando sua conta executar como automação recentemente criada ou atualizada.    

## <a name="automation-run-as-authentication"></a>Autenticação da conta Executar como de automação
Use o código de exemplo hello abaixo muito[criar um runbook do PowerShell](automation-creating-importing-runbook.md) tooverify autenticação usando Olá executado como conta e também em seu runbooks personalizado tooauthenticate e gerenciar recursos do Gerenciador de recursos com sua conta de automação.   

    $connectionName = "AzureRunAsConnection"
    try
    {
        # Get hello connection "AzureRunAsConnection "
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

        "Logging in tooAzure..."
        Add-AzureRmAccount `
           -ServicePrincipal `
           -TenantId $servicePrincipalConnection.TenantId `
           -ApplicationId $servicePrincipalConnection.ApplicationId `
           -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
    }
    catch {
       if (!$servicePrincipalConnection)
       {
          $ErrorMessage = "Connection $connectionName not found."
          throw $ErrorMessage
      } else{
          Write-Error -Message $_.Exception
          throw $_.Exception
      }
    }

    #Get all ARM resources from all resource groups
    $ResourceGroups = Get-AzureRmResourceGroup 

    foreach ($ResourceGroup in $ResourceGroups)
    {    
       Write-Output ("Showing resources in resource group " + $ResourceGroup.ResourceGroupName)
       $Resources = Find-AzureRmResource -ResourceGroupNameContains $ResourceGroup.ResourceGroupName | Select ResourceName, ResourceType
       ForEach ($Resource in $Resources)
       {
          Write-Output ($Resource.ResourceName + " of type " +  $Resource.ResourceType)
       }
       Write-Output ("")
    } 

Observe Olá cmdlet usado para autenticar no runbook Olá - **adicionar AzureRmAccount**, Olá usa *ServicePrincipalCertificate* conjunto de parâmetros.  Ele se autentica usando o certificado de entidade de serviço, não as credenciais.  

Quando você [executar Olá runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate sua conta executar como, um [trabalho de runbook](automation-runbook-execution.md) é criado, folha de trabalho Olá é exibida e status do trabalho Olá exibido no hello **resumo do trabalho**lado a lado. status do trabalho Olá será iniciado como *na fila* indicando que ele está aguardando um trabalho de runbook no hello toobecome de nuvem disponível. Em seguida, ele move muito*iniciando* quando um trabalhador declarações trabalho Olá e, em seguida, *executando* quando Olá runbook realmente começa a ser executado.  Quando o trabalho de runbook Olá for concluído, podemos verificar o status de **concluído**.

toosee Olá resultados detalhados da saudação runbook, clique em Olá **saída** lado a lado.  Em Olá **saída** folha, você verá ele foi autenticado com êxito e retorna uma lista de todos os recursos em todos os grupos de recursos em sua assinatura.  

Apenas lembre-se o bloco de saudação tooremove de código, começando com o comentário hello `#Get all ARM resources from all resource groups` quando você reutilizar o código de saudação para seus runbooks.

## <a name="classic-run-as-authentication"></a>Autenticação da conta Executar como clássica
Use o código de exemplo hello abaixo muito[criar um runbook do PowerShell](automation-creating-importing-runbook.md) tooverify autenticação usando Olá clássico executado como conta e também em seu runbooks personalizado tooauthenticate e gerenciar recursos no modelo de implantação clássico hello.  

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get hello connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate tooAzure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in hello Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting hello certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in hello Automation account."
    }

    Write-Verbose "Authenticating tooAzure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID
    
    #Get all VMs in hello subscription and return list with name of each
    Get-AzureVM | ft Name

Quando você [executar Olá runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate sua conta executar como, um [trabalho de runbook](automation-runbook-execution.md) é criado, folha de trabalho Olá é exibida e status do trabalho Olá exibido no hello **resumo do trabalho**lado a lado. status do trabalho Olá será iniciado como *na fila* indicando que ele está aguardando um trabalho de runbook no hello toobecome de nuvem disponível. Em seguida, ele move muito*iniciando* quando um trabalhador declarações trabalho Olá e, em seguida, *executando* quando Olá runbook realmente começa a ser executado.  Quando o trabalho de runbook Olá for concluído, podemos verificar o status de **concluído**.

toosee Olá resultados detalhados da saudação runbook, clique em Olá **saída** lado a lado.  Em Olá **saída** folha, você deve ver que autenticou com êxito e retorna uma lista de todas as VMs do Azure por VMName que são implantados na sua assinatura.  

Lembre-se tooremove Olá cmdlet **Get-AzureVM** quando você reutilizar o código de saudação para seus runbooks.

## <a name="next-steps"></a>Próximas etapas
* tooget iniciado com runbooks do PowerShell, consulte [meu primeiro runbook do PowerShell](automation-first-runbook-textual-powershell.md).
* toolearn mais sobre a criação de gráficos, consulte [criação gráfica na automação do Azure](automation-graphical-authoring-intro.md).
