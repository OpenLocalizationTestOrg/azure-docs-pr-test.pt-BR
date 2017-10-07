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
# <a name="test-azure-automation-run-as-account-authentication"></a><span data-ttu-id="916f2-103">Como testar a autenticação da conta Executar como de Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="916f2-103">Test Azure Automation Run As account authentication</span></span>
<span data-ttu-id="916f2-104">Depois que uma conta de automação é criada com êxito, você pode executar um tooconfirm de teste simples que você é capaz de autenticar o toosuccessfully no Gerenciador de recursos do Azure ou implantação clássica do Azure usando sua conta executar como automação recentemente criada ou atualizada.</span><span class="sxs-lookup"><span data-stu-id="916f2-104">After an Automation account is successfully created, you can perform a simple test tooconfirm you are able toosuccessfully authenticate in Azure Resource Manager or Azure classic deployment using your newly created or updated Automation Run As account.</span></span>    

## <a name="automation-run-as-authentication"></a><span data-ttu-id="916f2-105">Autenticação da conta Executar como de automação</span><span class="sxs-lookup"><span data-stu-id="916f2-105">Automation Run As authentication</span></span>
<span data-ttu-id="916f2-106">Use o código de exemplo hello abaixo muito[criar um runbook do PowerShell](automation-creating-importing-runbook.md) tooverify autenticação usando Olá executado como conta e também em seu runbooks personalizado tooauthenticate e gerenciar recursos do Gerenciador de recursos com sua conta de automação.</span><span class="sxs-lookup"><span data-stu-id="916f2-106">Use hello sample code below too[create a PowerShell runbook](automation-creating-importing-runbook.md) tooverify authentication using hello Run As account and also in your custom runbooks tooauthenticate and manage Resource Manager resources with your Automation account.</span></span>   

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

<span data-ttu-id="916f2-107">Observe Olá cmdlet usado para autenticar no runbook Olá - **adicionar AzureRmAccount**, Olá usa *ServicePrincipalCertificate* conjunto de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="916f2-107">Notice hello cmdlet used for authenticating in hello runbook - **Add-AzureRmAccount**, uses hello *ServicePrincipalCertificate* parameter set.</span></span>  <span data-ttu-id="916f2-108">Ele se autentica usando o certificado de entidade de serviço, não as credenciais.</span><span class="sxs-lookup"><span data-stu-id="916f2-108">It authenticates by using service principal certificate, not credentials.</span></span>  

<span data-ttu-id="916f2-109">Quando você [executar Olá runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate sua conta executar como, um [trabalho de runbook](automation-runbook-execution.md) é criado, folha de trabalho Olá é exibida e status do trabalho Olá exibido no hello **resumo do trabalho**lado a lado.</span><span class="sxs-lookup"><span data-stu-id="916f2-109">When you [run hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate your Run As account, a [runbook job](automation-runbook-execution.md) is created, hello Job blade is displayed, and hello job status displayed in hello **Job Summary** tile.</span></span> <span data-ttu-id="916f2-110">status do trabalho Olá será iniciado como *na fila* indicando que ele está aguardando um trabalho de runbook no hello toobecome de nuvem disponível.</span><span class="sxs-lookup"><span data-stu-id="916f2-110">hello job status will start as *Queued* indicating that it is waiting for a runbook worker in hello cloud toobecome available.</span></span> <span data-ttu-id="916f2-111">Em seguida, ele move muito*iniciando* quando um trabalhador declarações trabalho Olá e, em seguida, *executando* quando Olá runbook realmente começa a ser executado.</span><span class="sxs-lookup"><span data-stu-id="916f2-111">It will then move too*Starting* when a worker claims hello job, and then *Running* when hello runbook actually starts running.</span></span>  <span data-ttu-id="916f2-112">Quando o trabalho de runbook Olá for concluído, podemos verificar o status de **concluído**.</span><span class="sxs-lookup"><span data-stu-id="916f2-112">When hello runbook job completes, we should see a status of **Completed**.</span></span>

<span data-ttu-id="916f2-113">toosee Olá resultados detalhados da saudação runbook, clique em Olá **saída** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="916f2-113">toosee hello detailed results of hello runbook, click on hello **Output** tile.</span></span>  <span data-ttu-id="916f2-114">Em Olá **saída** folha, você verá ele foi autenticado com êxito e retorna uma lista de todos os recursos em todos os grupos de recursos em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="916f2-114">On hello **Output** blade, you should see it has successfully authenticated and returns a list of all resources in all resource groups in your subscription.</span></span>  

<span data-ttu-id="916f2-115">Apenas lembre-se o bloco de saudação tooremove de código, começando com o comentário hello `#Get all ARM resources from all resource groups` quando você reutilizar o código de saudação para seus runbooks.</span><span class="sxs-lookup"><span data-stu-id="916f2-115">Just remember tooremove hello block of code starting with hello comment `#Get all ARM resources from all resource groups` when you reuse hello code for your runbooks.</span></span>

## <a name="classic-run-as-authentication"></a><span data-ttu-id="916f2-116">Autenticação da conta Executar como clássica</span><span class="sxs-lookup"><span data-stu-id="916f2-116">Classic Run As authentication</span></span>
<span data-ttu-id="916f2-117">Use o código de exemplo hello abaixo muito[criar um runbook do PowerShell](automation-creating-importing-runbook.md) tooverify autenticação usando Olá clássico executado como conta e também em seu runbooks personalizado tooauthenticate e gerenciar recursos no modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="916f2-117">Use hello sample code below too[create a PowerShell runbook](automation-creating-importing-runbook.md) tooverify authentication using hello Classic Run As account and also in your custom runbooks tooauthenticate and manage resources in hello classic deployment model.</span></span>  

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

<span data-ttu-id="916f2-118">Quando você [executar Olá runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate sua conta executar como, um [trabalho de runbook](automation-runbook-execution.md) é criado, folha de trabalho Olá é exibida e status do trabalho Olá exibido no hello **resumo do trabalho**lado a lado.</span><span class="sxs-lookup"><span data-stu-id="916f2-118">When you [run hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate your Run As account, a [runbook job](automation-runbook-execution.md) is created, hello Job blade is displayed, and hello job status displayed in hello **Job Summary** tile.</span></span> <span data-ttu-id="916f2-119">status do trabalho Olá será iniciado como *na fila* indicando que ele está aguardando um trabalho de runbook no hello toobecome de nuvem disponível.</span><span class="sxs-lookup"><span data-stu-id="916f2-119">hello job status will start as *Queued* indicating that it is waiting for a runbook worker in hello cloud toobecome available.</span></span> <span data-ttu-id="916f2-120">Em seguida, ele move muito*iniciando* quando um trabalhador declarações trabalho Olá e, em seguida, *executando* quando Olá runbook realmente começa a ser executado.</span><span class="sxs-lookup"><span data-stu-id="916f2-120">It will then move too*Starting* when a worker claims hello job, and then *Running* when hello runbook actually starts running.</span></span>  <span data-ttu-id="916f2-121">Quando o trabalho de runbook Olá for concluído, podemos verificar o status de **concluído**.</span><span class="sxs-lookup"><span data-stu-id="916f2-121">When hello runbook job completes, we should see a status of **Completed**.</span></span>

<span data-ttu-id="916f2-122">toosee Olá resultados detalhados da saudação runbook, clique em Olá **saída** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="916f2-122">toosee hello detailed results of hello runbook, click on hello **Output** tile.</span></span>  <span data-ttu-id="916f2-123">Em Olá **saída** folha, você deve ver que autenticou com êxito e retorna uma lista de todas as VMs do Azure por VMName que são implantados na sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="916f2-123">On hello **Output** blade, you should see it has successfully authenticated and returns a list of all Azure VMs by VMName that are deployed in your subscription.</span></span>  

<span data-ttu-id="916f2-124">Lembre-se tooremove Olá cmdlet **Get-AzureVM** quando você reutilizar o código de saudação para seus runbooks.</span><span class="sxs-lookup"><span data-stu-id="916f2-124">Just remember tooremove hello cmdlet **Get-AzureVM** when you reuse hello code for your runbooks.</span></span>

## <a name="next-steps"></a><span data-ttu-id="916f2-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="916f2-125">Next steps</span></span>
* <span data-ttu-id="916f2-126">tooget iniciado com runbooks do PowerShell, consulte [meu primeiro runbook do PowerShell](automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="916f2-126">tooget started with PowerShell runbooks, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span></span>
* <span data-ttu-id="916f2-127">toolearn mais sobre a criação de gráficos, consulte [criação gráfica na automação do Azure](automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="916f2-127">toolearn more about Graphical Authoring, see [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>
