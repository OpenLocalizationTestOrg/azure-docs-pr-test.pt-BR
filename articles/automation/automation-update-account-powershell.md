---
title: "aaaCreate conta de automação executar como do Azure com o PowerShell | Microsoft Docs"
description: "Este artigo descreve como tooupgrade sua conta de automação com PowerShell toocreate Olá executados como contas se você não executou esta etapa durante a criação inicial do portal de saudação."
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
ms.date: 04/14/2017
ms.author: magoedte
ms.openlocfilehash: 1049601321d2bc1e5f9d982f622788f8e4e4d797
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="update-automation-run-as-account-using-powershell"></a><span data-ttu-id="e87be-103">Como atualizar conta Executar como de Automação usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="e87be-103">Update Automation Run As account using PowerShell</span></span>
<span data-ttu-id="e87be-104">Você pode usar sua conta de automação existente de PowerShell tooupdate se:</span><span class="sxs-lookup"><span data-stu-id="e87be-104">You can use PowerShell tooupdate your existing Automation account if:</span></span>

* <span data-ttu-id="e87be-105">Criar uma conta de automação, mas recusar toocreate Olá executar como conta.</span><span class="sxs-lookup"><span data-stu-id="e87be-105">You create an Automation account but decline toocreate hello Run As account.</span></span>
* <span data-ttu-id="e87be-106">Você já usa uma recursos de Gerenciador de recursos de toomanage de conta de automação e deseja tooupdate Olá tooinclude Olá executar como conta para autenticação de runbook.</span><span class="sxs-lookup"><span data-stu-id="e87be-106">You already use an Automation account toomanage Resource Manager resources and you want tooupdate hello account tooinclude hello Run As account for runbook authentication.</span></span>
* <span data-ttu-id="e87be-107">Você já usa uma automação conta toomanage os recursos clássicos e você deseja tooupdate-Olá toouse clássico executar como conta em vez de criar uma nova conta e migrar seu tooit runbooks e ativos.</span><span class="sxs-lookup"><span data-stu-id="e87be-107">You already use an Automation account toomanage classic resources and you want tooupdate it toouse hello Classic Run As account instead of creating a new account and migrating your runbooks and assets tooit.</span></span>   
* <span data-ttu-id="e87be-108">Você quer toocreate executar como e uma conta clássico executar como usando um certificado emitido por sua autoridade de certificação (CA).</span><span class="sxs-lookup"><span data-stu-id="e87be-108">You want toocreate a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e87be-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e87be-109">Prerequisites</span></span>

* <span data-ttu-id="e87be-110">script Hello pode ser executado somente no Windows 10 e Windows Server 2016 com módulos do Azure Resource Manager 2.01 e posteriores.</span><span class="sxs-lookup"><span data-stu-id="e87be-110">hello script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 2.01 and later.</span></span> <span data-ttu-id="e87be-111">Não há suporte nas versões anteriores do Windows.</span><span class="sxs-lookup"><span data-stu-id="e87be-111">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="e87be-112">Azure PowerShell 1.0 e posterior.</span><span class="sxs-lookup"><span data-stu-id="e87be-112">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="e87be-113">Para obter informações sobre versão Olá PowerShell 1.0, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e87be-113">For information about hello PowerShell 1.0 release, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="e87be-114">Uma conta de automação, que é referenciada como valor Olá Olá *– AutomationAccountName* e *- ApplicationDisplayName* parâmetros em Olá script do PowerShell a seguir.</span><span class="sxs-lookup"><span data-stu-id="e87be-114">An Automation account, which is referenced as hello value for hello *–AutomationAccountName* and *-ApplicationDisplayName* parameters in hello following PowerShell script.</span></span>

<span data-ttu-id="e87be-115">Olá tooget valores para *SubscriptionID*, *ResourceGroup*, e *AutomationAccountName*, que são parâmetros obrigatórios para scripts hello, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="e87be-115">tooget hello values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for hello scripts, do hello following:</span></span>
1. <span data-ttu-id="e87be-116">No hello portal do Azure, selecione sua conta de automação Olá **conta de automação** folha e, em seguida, selecione **todas as configurações**.</span><span class="sxs-lookup"><span data-stu-id="e87be-116">In hello Azure portal, select your Automation account on hello **Automation account** blade, and then select **All settings**.</span></span> 
2. <span data-ttu-id="e87be-117">Em Olá **todas as configurações** folha, em **configurações de conta**, selecione **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="e87be-117">On hello **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="e87be-118">Observe os valores hello Olá **propriedades** folha.</span><span class="sxs-lookup"><span data-stu-id="e87be-118">Note hello values on hello **Properties** blade.</span></span>

![folha de "Propriedades" Hello automação conta](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

## <a name="create-run-as-account-powershell-script"></a><span data-ttu-id="e87be-120">Criar o script do PowerShell da conta Executar como</span><span class="sxs-lookup"><span data-stu-id="e87be-120">Create Run As Account PowerShell script</span></span>
<span data-ttu-id="e87be-121">Este script do PowerShell inclui suporte para Olá configurações a seguir:</span><span class="sxs-lookup"><span data-stu-id="e87be-121">This PowerShell script includes support for hello following configurations:</span></span>

* <span data-ttu-id="e87be-122">Crie uma conta Executar como usando um certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="e87be-122">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="e87be-123">Crie uma conta Executar como e uma conta Executar como Clássica usando um certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="e87be-123">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="e87be-124">Crie uma conta Executar como e uma conta Executar como Clássica usando um certificado corporativo.</span><span class="sxs-lookup"><span data-stu-id="e87be-124">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="e87be-125">Crie uma conta executar como e uma conta clássico executar como usando um certificado autoassinado no hello nuvem do Azure governamental.</span><span class="sxs-lookup"><span data-stu-id="e87be-125">Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud.</span></span>

<span data-ttu-id="e87be-126">Dependendo da opção de configuração de saudação que selecionar script hello cria Olá itens a seguir.</span><span class="sxs-lookup"><span data-stu-id="e87be-126">Depending on hello configuration option you select, hello script creates hello following items.</span></span>

<span data-ttu-id="e87be-127">**Para contas Executar como:**</span><span class="sxs-lookup"><span data-stu-id="e87be-127">**For Run As accounts:**</span></span>

* <span data-ttu-id="e87be-128">Cria um Azure AD aplicativo toobe exportado com a saudação autoassinada ou chave pública do certificado da empresa, cria uma conta de serviço principal para o aplicativo hello no AD do Azure e atribui Olá função Colaborador para conta Olá no seu atual assinatura.</span><span class="sxs-lookup"><span data-stu-id="e87be-128">Creates an Azure AD application toobe exported with either hello self-signed or enterprise certificate public key, creates a service principal account for hello application in Azure AD, and assigns hello Contributor role for hello account in your current subscription.</span></span> <span data-ttu-id="e87be-129">Você pode alterar essa configuração tooOwner ou qualquer outra função.</span><span class="sxs-lookup"><span data-stu-id="e87be-129">You can change this setting tooOwner or any other role.</span></span> <span data-ttu-id="e87be-130">Para obter mais informações, confira [Controle de acesso baseado em função na Automação do Azure](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="e87be-130">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="e87be-131">Cria um ativo de certificado de automação chamado *AzureRunAsCertificate* em Olá especificado na conta de automação.</span><span class="sxs-lookup"><span data-stu-id="e87be-131">Creates an Automation certificate asset named *AzureRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="e87be-132">ativo de certificado Olá mantém Olá chave privada do certificado que é usado pelo aplicativo hello AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e87be-132">hello certificate asset holds hello certificate private key that's used by hello Azure AD application.</span></span>
* <span data-ttu-id="e87be-133">Cria um ativo de conexão de automação chamado *AzureRunAsConnection* em Olá especificado na conta de automação.</span><span class="sxs-lookup"><span data-stu-id="e87be-133">Creates an Automation connection asset named *AzureRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="e87be-134">ativo de conexão Olá mantém applicationId hello, tenantId, subscriptionId e a impressão digital do certificado.</span><span class="sxs-lookup"><span data-stu-id="e87be-134">hello connection asset holds hello applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="e87be-135">**Para contas Executar como clássicas:**</span><span class="sxs-lookup"><span data-stu-id="e87be-135">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="e87be-136">Cria um ativo de certificado de automação chamado *AzureClassicRunAsCertificate* em Olá especificado na conta de automação.</span><span class="sxs-lookup"><span data-stu-id="e87be-136">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="e87be-137">ativo de certificado Olá mantém a chave privada do certificado Olá usado pelo certificado de gerenciamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="e87be-137">hello certificate asset holds hello certificate private key used by hello management certificate.</span></span>
* <span data-ttu-id="e87be-138">Cria um ativo de conexão de automação chamado *AzureClassicRunAsConnection* em Olá especificado na conta de automação.</span><span class="sxs-lookup"><span data-stu-id="e87be-138">Creates an Automation connection asset named *AzureClassicRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="e87be-139">ativo de conexão Olá contém o nome da assinatura hello, subscriptionId e nome do ativo de certificado.</span><span class="sxs-lookup"><span data-stu-id="e87be-139">hello connection asset holds hello subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="e87be-140">Se você selecionar a opção para criar uma conta clássico executar como, após a execução do script hello, carregamento Olá pública repositório de certificados gerenciamento de toohello (extensão de nome de arquivo. cer) para a assinatura de saudação que Olá conta de automação foi criado no.</span><span class="sxs-lookup"><span data-stu-id="e87be-140">If you select either option for creating a Classic Run As account, after hello script is executed, upload hello public certificate (.cer file name extension) toohello management store for hello subscription that hello Automation account was created in.</span></span>
> 

1. <span data-ttu-id="e87be-141">Salve Olá script a seguir em seu computador.</span><span class="sxs-lookup"><span data-stu-id="e87be-141">Save hello following script on your computer.</span></span> <span data-ttu-id="e87be-142">Neste exemplo, salve-o com o nome de arquivo hello *RunAsAccount.ps1 novo*.</span><span class="sxs-lookup"><span data-stu-id="e87be-142">In this example, save it with hello filename *New-RunAsAccount.ps1*.</span></span>

        #Requires -RunAsAdministrator
         Param (
        [Parameter(Mandatory=$true)]
        [String] $ResourceGroup,

        [Parameter(Mandatory=$true)]
        [String] $AutomationAccountName,

        [Parameter(Mandatory=$true)]
        [String] $ApplicationDisplayName,

        [Parameter(Mandatory=$true)]
        [String] $SubscriptionId,

        [Parameter(Mandatory=$true)]
        [Boolean] $CreateClassicRunAsAccount,

        [Parameter(Mandatory=$true)]
        [String] $SelfSignedCertPlainPassword,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$EnvironmentName="AzureCloud",

        [Parameter(Mandatory=$false)]
        [int] $SelfSignedCertNoOfMonthsUntilExpired = 12
        )

        function CreateSelfSignedCertificate([string] $keyVaultName, [string] $certificateName, [string] $selfSignedCertPlainPassword,
                                      [string] $certPath, [string] $certPathCer, [string] $selfSignedCertNoOfMonthsUntilExpired ) {
        $Cert = New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation cert:\LocalMachine\My `
           -KeyExportPolicy Exportable -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
           -NotAfter (Get-Date).AddMonths($selfSignedCertNoOfMonthsUntilExpired)

        $CertPassword = ConvertTo-SecureString $selfSignedCertPlainPassword -AsPlainText -Force
        Export-PfxCertificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPath -Password $CertPassword -Force | Write-Verbose
        Export-Certificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPathCer -Type CERT | Write-Verbose
        }

        function CreateServicePrincipal([System.Security.Cryptography.X509Certificates.X509Certificate2] $PfxCert, [string] $applicationDisplayName) {  
        $CurrentDate = Get-Date
        $keyValue = [System.Convert]::ToBase64String($PfxCert.GetRawCertData())
        $KeyId = (New-Guid).Guid

        $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
        $KeyCredential.StartDate = $CurrentDate
        $KeyCredential.EndDate= [DateTime]$PfxCert.GetExpirationDateString()
        $KeyCredential.EndDate = $KeyCredential.EndDate.AddDays(-1)
        $KeyCredential.KeyId = $KeyId
        $KeyCredential.CertValue  = $keyValue

        # Use key credentials and create an Azure AD application
        $Application = New-AzureRmADApplication -DisplayName $ApplicationDisplayName -HomePage ("http://" + $applicationDisplayName) -IdentifierUris ("http://" + $KeyId) -KeyCredentials $KeyCredential
        $ServicePrincipal = New-AzureRMADServicePrincipal -ApplicationId $Application.ApplicationId
        $GetServicePrincipal = Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id

        # Sleep here for a few seconds tooallow hello service principal application toobecome active (ordinarily takes a few seconds)
        Sleep -s 15
        $NewRole = New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
        $Retries = 0;
        While ($NewRole -eq $null -and $Retries -le 6)
        {
           Sleep -s 10
           New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
           $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
           $Retries++;
        }
           return $Application.ApplicationId.ToString();
        }

        function CreateAutomationCertificateAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $certifcateAssetName,[string] $certPath, [string] $certPlainPassword, [Boolean] $Exportable) {
        $CertPassword = ConvertTo-SecureString $certPlainPassword -AsPlainText -Force   
        Remove-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $certifcateAssetName -ErrorAction SilentlyContinue
        New-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Path $certPath -Name $certifcateAssetName -Password $CertPassword -Exportable:$Exportable  | write-verbose
        }

        function CreateAutomationConnectionAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $connectionAssetName, [string] $connectionTypeName, [System.Collections.Hashtable] $connectionFieldValues ) {
        Remove-AzureRmAutomationConnection -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -Force -ErrorAction SilentlyContinue
        New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -ConnectionTypeName $connectionTypeName -ConnectionFieldValues $connectionFieldValues
        }

        Import-Module AzureRM.Profile
        Import-Module AzureRM.Resources

        $AzureRMProfileVersion= (Get-Module AzureRM.Profile).Version
        if (!(($AzureRMProfileVersion.Major -ge 2 -and $AzureRMProfileVersion.Minor -ge 1) -or ($AzureRMProfileVersion.Major -gt 2)))
        {
           Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
           return
        }

        Login-AzureRmAccount -EnvironmentName $EnvironmentName
        $Subscription = Select-AzureRmSubscription -SubscriptionId $SubscriptionId

        # Create a Run As account by using a service principal
        $CertifcateAssetName = "AzureRunAsCertificate"
        $ConnectionAssetName = "AzureRunAsConnection"
        $ConnectionTypeName = "AzureServicePrincipal"

        if ($EnterpriseCertPathForRunAsAccount -and $EnterpriseCertPlainPasswordForRunAsAccount) {
        $PfxCertPathForRunAsAccount = $EnterpriseCertPathForRunAsAccount
        $PfxCertPlainPasswordForRunAsAccount = $EnterpriseCertPlainPasswordForRunAsAccount
        } else {
          $CertificateName = $AutomationAccountName+$CertifcateAssetName
          $PfxCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".pfx")
          $PfxCertPlainPasswordForRunAsAccount = $SelfSignedCertPlainPassword
          $CerCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".cer")
          CreateSelfSignedCertificate $KeyVaultName $CertificateName $PfxCertPlainPasswordForRunAsAccount $PfxCertPathForRunAsAccount $CerCertPathForRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create a service principal
        $PfxCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($PfxCertPathForRunAsAccount, $PfxCertPlainPasswordForRunAsAccount)
        $ApplicationId=CreateServicePrincipal $PfxCert $ApplicationDisplayName

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate hello ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
            # Create a Run As account by using a service principal
            $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
            $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
            $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
            $UploadMessage = "Please upload hello .cer format of #CERT# toohello Management store by following hello steps below." + [Environment]::NewLine +
                    "Log in toohello Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                    "Then click Upload and upload hello .cer format of #CERT#"

             if ($EnterpriseCertPathForClassicRunAsAccount -and $EnterpriseCertPlainPasswordForClassicRunAsAccount ) {
             $PfxCertPathForClassicRunAsAccount = $EnterpriseCertPathForClassicRunAsAccount
             $PfxCertPlainPasswordForClassicRunAsAccount = $EnterpriseCertPlainPasswordForClassicRunAsAccount
             $UploadMessage = $UploadMessage.Replace("#CERT#", $PfxCertPathForClassicRunAsAccount)
        } else {
             $ClassicRunAsAccountCertificateName = $AutomationAccountName+$ClassicRunAsAccountCertifcateAssetName
             $PfxCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".pfx")
             $PfxCertPlainPasswordForClassicRunAsAccount = $SelfSignedCertPlainPassword
             $CerCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".cer")
             $UploadMessage = $UploadMessage.Replace("#CERT#", $CerCertPathForClassicRunAsAccount)
             CreateSelfSignedCertificate $KeyVaultName $ClassicRunAsAccountCertificateName $PfxCertPlainPasswordForClassicRunAsAccount $PfxCertPathForClassicRunAsAccount $CerCertPathForClassicRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate hello ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="e87be-143">Em seu computador, inicie **do Windows PowerShell** de saudação **iniciar** tela com direitos de usuário elevados.</span><span class="sxs-lookup"><span data-stu-id="e87be-143">On your computer, start **Windows PowerShell** from hello **Start** screen with elevated user rights.</span></span>
3. <span data-ttu-id="e87be-144">De saudação elevado shell de linha de comando, vá toohello pasta que contém o script hello criado na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="e87be-144">From hello elevated command-line shell, go toohello folder that contains hello script you created in step 1.</span></span>  
4. <span data-ttu-id="e87be-145">Execute script hello usando valores de parâmetro de saudação para configuração Olá que precisar.</span><span class="sxs-lookup"><span data-stu-id="e87be-145">Execute hello script by using hello parameter values for hello configuration you require.</span></span>

    <span data-ttu-id="e87be-146">**Criar uma conta Executar como usando um certificado autoassinado**</span><span class="sxs-lookup"><span data-stu-id="e87be-146">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="e87be-147">**Criar uma conta Executar como e uma conta Executar como Clássica usando um certificado autoassinado**</span><span class="sxs-lookup"><span data-stu-id="e87be-147">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="e87be-148">**Criar uma conta Executar como e uma conta Executar como Clássica usando um certificado corporativo**</span><span class="sxs-lookup"><span data-stu-id="e87be-148">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="e87be-149">**Criar uma conta executar como e uma conta clássico executar como usando um certificado autoassinado no hello nuvem Azure Government**</span><span class="sxs-lookup"><span data-stu-id="e87be-149">**Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="e87be-150">Depois que o script hello executado, será tooauthenticate solicitado com o Azure.</span><span class="sxs-lookup"><span data-stu-id="e87be-150">After hello script has executed, you will be prompted tooauthenticate with Azure.</span></span> <span data-ttu-id="e87be-151">Entrar com uma conta que seja membro da função de administradores de assinatura hello e coadministrador da assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="e87be-151">Sign in with an account that is a member of hello subscription administrators role and co-administrator of hello subscription.</span></span>
    >
    >

<span data-ttu-id="e87be-152">Depois que o script hello foi executada com êxito, observe o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="e87be-152">After hello script has executed successfully, note hello following:</span></span>
* <span data-ttu-id="e87be-153">Se você criou uma conta clássico executar como com um certificado autoassinado público (arquivo. cer), script hello cria e salva-a pasta de arquivos temporários toohello no computador em que o perfil de usuário Olá *%USERPROFILE%\AppData\Local\Temp*, que você usou a sessão do PowerShell Olá tooexecute.</span><span class="sxs-lookup"><span data-stu-id="e87be-153">If you created a Classic Run As account with a self-signed public certificate (.cer file), hello script creates and saves it toohello temporary files folder on your computer under hello user profile *%USERPROFILE%\AppData\Local\Temp*, which you used tooexecute hello PowerShell session.</span></span>
* <span data-ttu-id="e87be-154">Se tiver criado uma conta Executar como Clássica com um certificado público corporativo (arquivo .cer), use este certificado.</span><span class="sxs-lookup"><span data-stu-id="e87be-154">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="e87be-155">Siga as instruções de saudação de [carregar um certificado de API de gerenciamento toohello portal clássico do Azure](../azure-api-management-certs.md)e, em seguida, validar a configuração de credencial de saudação com recursos de implantação clássico usando Olá [código de exemplo tooauthenticate com recursos de implantação clássico do Azure](automation-verify-runas-authentication.md#classic-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="e87be-155">Follow hello instructions for [uploading a management API certificate toohello Azure classic portal](../azure-api-management-certs.md), and then validate hello credential configuration with classic deployment resources by using hello [sample code tooauthenticate with Azure Classic Deployment Resources](automation-verify-runas-authentication.md#classic-run-as-authentication).</span></span> 
* <span data-ttu-id="e87be-156">Se você fez *não* criar uma conta clássico executar como, autenticar com recursos de Gerenciador de recursos e validar a configuração de credencial de saudação usando Olá [código para autenticar com o serviço de gerenciamento de exemplo recursos](automation-verify-runas-authentication.md#automation-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="e87be-156">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate hello credential configuration by using hello [sample code for authenticating with Service Management resources](automation-verify-runas-authentication.md#automation-run-as-authentication).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e87be-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e87be-157">Next steps</span></span>
* <span data-ttu-id="e87be-158">Para obter mais informações sobre entidades de serviço, consulte muito[objetos Application e entidade de serviço](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="e87be-158">For more information about Service Principals, refer too[Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="e87be-159">Para obter mais informações sobre certificados e serviços do Azure, consulte muito[visão geral de certificados para serviços de nuvem do Azure](../cloud-services/cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="e87be-159">For more information about certificates and Azure services, refer too[Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>
