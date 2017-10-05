---
title: "Validar a conta de automação do Azure | Microsoft Docs"
description: "Este artigo descreve como confirmar se a configuração de sua conta de automação está configurada corretamente."
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
ms.openlocfilehash: 804e05f596e1d6d5f650e4c94a18eff6b7c3ba4e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="test-azure-automation-run-as-account-authentication"></a><span data-ttu-id="b7a80-103">Como testar a autenticação da conta Executar como de Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="b7a80-103">Test Azure Automation Run As account authentication</span></span>
<span data-ttu-id="b7a80-104">Depois que uma conta de automação é criada com êxito, você pode executar um teste simples para confirmar que você é capaz de autenticar com êxito no Azure Resource Manager ou na implantação clássica do Azure usando sua conta Executar como de Automação recém-criada ou atualizada.</span><span class="sxs-lookup"><span data-stu-id="b7a80-104">After an Automation account is successfully created, you can perform a simple test to confirm you are able to successfully authenticate in Azure Resource Manager or Azure classic deployment using your newly created or updated Automation Run As account.</span></span>    

## <a name="automation-run-as-authentication"></a><span data-ttu-id="b7a80-105">Autenticação da conta Executar como de automação</span><span class="sxs-lookup"><span data-stu-id="b7a80-105">Automation Run As authentication</span></span>
<span data-ttu-id="b7a80-106">Use o exemplo de código abaixo para [criar um runbook do PowerShell](automation-creating-importing-runbook.md) a fim de verificar a autenticação usando a conta Executar como e também em seus runbooks personalizados para autenticar e gerenciar os recursos do Resource Manager com sua conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="b7a80-106">Use the sample code below to [create a PowerShell runbook](automation-creating-importing-runbook.md) to verify authentication using the Run As account and also in your custom runbooks to authenticate and manage Resource Manager resources with your Automation account.</span></span>   

    $connectionName = "AzureRunAsConnection"
    try
    {
        # Get the connection "AzureRunAsConnection "
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

        "Logging in to Azure..."
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

<span data-ttu-id="b7a80-107">Observe que o cmdlet usado para autenticar o runbook - **Add-AzureRmAccount**, usa o conjunto de parâmetros *ServicePrincipalCertificate* .</span><span class="sxs-lookup"><span data-stu-id="b7a80-107">Notice the cmdlet used for authenticating in the runbook - **Add-AzureRmAccount**, uses the *ServicePrincipalCertificate* parameter set.</span></span>  <span data-ttu-id="b7a80-108">Ele se autentica usando o certificado de entidade de serviço, não as credenciais.</span><span class="sxs-lookup"><span data-stu-id="b7a80-108">It authenticates by using service principal certificate, not credentials.</span></span>  

<span data-ttu-id="b7a80-109">Quando você [executa o runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) para validar sua conta Executar como, um [trabalho de runbook](automation-runbook-execution.md) é criado, a folha Trabalho é exibida e o status do trabalho é mostrado no bloco **Resumo do Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="b7a80-109">When you [run the runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) to validate your Run As account, a [runbook job](automation-runbook-execution.md) is created, the Job blade is displayed, and the job status displayed in the **Job Summary** tile.</span></span> <span data-ttu-id="b7a80-110">O status do trabalho será iniciado como *Na fila* , indicando que ele está aguardando um runbook worker ficar disponível na nuvem.</span><span class="sxs-lookup"><span data-stu-id="b7a80-110">The job status will start as *Queued* indicating that it is waiting for a runbook worker in the cloud to become available.</span></span> <span data-ttu-id="b7a80-111">Mudará para *Iniciando* quando um trabalhador reivindicar o trabalho, em seguida, para *Executando* quando o runbook realmente começar a ser executado.</span><span class="sxs-lookup"><span data-stu-id="b7a80-111">It will then move to *Starting* when a worker claims the job, and then *Running* when the runbook actually starts running.</span></span>  <span data-ttu-id="b7a80-112">Quando o trabalho do runbook concluir, deveremos ver um status de **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="b7a80-112">When the runbook job completes, we should see a status of **Completed**.</span></span>

<span data-ttu-id="b7a80-113">Para ver os resultados detalhados do runbook, clique no bloco **Saída** .</span><span class="sxs-lookup"><span data-stu-id="b7a80-113">To see the detailed results of the runbook, click on the **Output** tile.</span></span>  <span data-ttu-id="b7a80-114">Na folha **Saída**, você deverá ver que ele foi autenticado com êxito e que retornou uma lista de todos os recursos em todos os grupos de recursos de sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="b7a80-114">On the **Output** blade, you should see it has successfully authenticated and returns a list of all resources in all resource groups in your subscription.</span></span>  

<span data-ttu-id="b7a80-115">Apenas lembre-se de remover o bloco de código que começa com o comentário `#Get all ARM resources from all resource groups` ao reutilizar o código para seus runbooks.</span><span class="sxs-lookup"><span data-stu-id="b7a80-115">Just remember to remove the block of code starting with the comment `#Get all ARM resources from all resource groups` when you reuse the code for your runbooks.</span></span>

## <a name="classic-run-as-authentication"></a><span data-ttu-id="b7a80-116">Autenticação da conta Executar como clássica</span><span class="sxs-lookup"><span data-stu-id="b7a80-116">Classic Run As authentication</span></span>
<span data-ttu-id="b7a80-117">Use o exemplo de código abaixo para [criar um runbook do PowerShell](automation-creating-importing-runbook.md) a fim de verificar a autenticação usando a conta Executar como clássica e também em seus runbooks personalizados para autenticar e gerenciar os recursos no modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="b7a80-117">Use the sample code below to [create a PowerShell runbook](automation-creating-importing-runbook.md) to verify authentication using the Classic Run As account and also in your custom runbooks to authenticate and manage resources in the classic deployment model.</span></span>  

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get the connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate to Azure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in the Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting the certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in the Automation account."
    }

    Write-Verbose "Authenticating to Azure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID
    
    #Get all VMs in the subscription and return list with name of each
    Get-AzureVM | ft Name

<span data-ttu-id="b7a80-118">Quando você [executa o runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) para validar sua conta Executar como, um [trabalho de runbook](automation-runbook-execution.md) é criado, a folha Trabalho é exibida e o status do trabalho é mostrado no bloco **Resumo do Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="b7a80-118">When you [run the runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) to validate your Run As account, a [runbook job](automation-runbook-execution.md) is created, the Job blade is displayed, and the job status displayed in the **Job Summary** tile.</span></span> <span data-ttu-id="b7a80-119">O status do trabalho será iniciado como *Na fila* , indicando que ele está aguardando um runbook worker ficar disponível na nuvem.</span><span class="sxs-lookup"><span data-stu-id="b7a80-119">The job status will start as *Queued* indicating that it is waiting for a runbook worker in the cloud to become available.</span></span> <span data-ttu-id="b7a80-120">Mudará para *Iniciando* quando um trabalhador reivindicar o trabalho, em seguida, para *Executando* quando o runbook realmente começar a ser executado.</span><span class="sxs-lookup"><span data-stu-id="b7a80-120">It will then move to *Starting* when a worker claims the job, and then *Running* when the runbook actually starts running.</span></span>  <span data-ttu-id="b7a80-121">Quando o trabalho do runbook concluir, deveremos ver um status de **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="b7a80-121">When the runbook job completes, we should see a status of **Completed**.</span></span>

<span data-ttu-id="b7a80-122">Para ver os resultados detalhados do runbook, clique no bloco **Saída** .</span><span class="sxs-lookup"><span data-stu-id="b7a80-122">To see the detailed results of the runbook, click on the **Output** tile.</span></span>  <span data-ttu-id="b7a80-123">Na folha **Saída**, você deverá ver que ele foi autenticado com êxito e que retornou uma lista de todas as VMs do Azure por VMName implantadas em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="b7a80-123">On the **Output** blade, you should see it has successfully authenticated and returns a list of all Azure VMs by VMName that are deployed in your subscription.</span></span>  

<span data-ttu-id="b7a80-124">Apenas lembre-se de remover o cmdlet **Get-AzureVM** ao reutilizar o código para seus runbooks.</span><span class="sxs-lookup"><span data-stu-id="b7a80-124">Just remember to remove the cmdlet **Get-AzureVM** when you reuse the code for your runbooks.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7a80-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b7a80-125">Next steps</span></span>
* <span data-ttu-id="b7a80-126">Para começar a usar os runbooks do PowerShell, confira [Meu primeiro runbook do PowerShell](automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="b7a80-126">To get started with PowerShell runbooks, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span></span>
* <span data-ttu-id="b7a80-127">Para saber mais sobre a autorização gráfica, confira [Criação gráfica na automação do Azure](automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="b7a80-127">To learn more about Graphical Authoring, see [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>
