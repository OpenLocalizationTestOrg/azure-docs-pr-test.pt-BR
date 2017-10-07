---
title: "contas de automação executar como do Azure aaaCreate | Microsoft Docs"
description: "Este artigo descreve como tooupdate à automação da conta e criar contas executar como com o PowerShell ou do portal de saudação."
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
ms.date: 07/27/2017
ms.author: magoedte
ms.openlocfilehash: 94eb54fa0b518056a726d17146c63411e248273b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-automation-account-authentication-with-run-as-accounts"></a>Atualizar a autenticação de conta de Automação com contas Executar como 
Você pode atualizar sua conta de automação existente do portal de saudação ou usar o PowerShell se:

* Criar uma conta de automação, mas recusar toocreate Olá executar como conta.
* Você já usa uma recursos de Gerenciador de recursos de toomanage de conta de automação e deseja tooupdate Olá tooinclude Olá executar como conta para autenticação de runbook.
* Você já usa uma automação conta toomanage os recursos clássicos e você deseja tooupdate-Olá toouse clássico executar como conta em vez de criar uma nova conta e migrar seu tooit runbooks e ativos.   
* Você quer toocreate executar como e uma conta clássico executar como usando um certificado emitido por sua autoridade de certificação (CA).

## <a name="prerequisites"></a>Pré-requisitos

* script Hello pode ser executada somente no Windows 10 e Windows Server 2016 com módulos do Azure Resource Manager 3.0.0 e posterior. Não há suporte nas versões anteriores do Windows.
* Azure PowerShell 1.0 e posterior. Para obter informações sobre versão Olá PowerShell 1.0, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs).
* Uma conta de automação, que é referenciada como valor Olá Olá *– AutomationAccountName* e *- ApplicationDisplayName* parâmetros em Olá script do PowerShell a seguir.

Olá tooget valores para *SubscriptionID*, *ResourceGroup*, e *AutomationAccountName*, que são parâmetros obrigatórios para o script hello, Olá a seguir:

1. No hello portal do Azure, selecione sua conta de automação Olá **conta de automação** folha e, em seguida, selecione **todas as configurações**.  
2. Em Olá **todas as configurações** folha, em **configurações de conta**, selecione **propriedades**. 
3. Observe os valores hello Olá **propriedades** folha.<br><br> ![folha de "Propriedades" Hello automação conta](media/automation-create-runas-account/automation-account-properties.png)  

### <a name="required-permissions-tooupdate-your-automation-account"></a>Necessário tooupdate permissões de sua conta de automação
tooupdate uma conta de automação, você deve ter Olá privilégios específicos a seguir e as permissões necessárias toocomplete neste tópico.   
 
* Sua conta de usuário do AD precisa toobe tooa adicionado função com a função de Colaborador de toohello equivalente de permissões para recursos do Microsoft conforme descrito no artigo [controle de acesso baseado em função no Azure Automation](automation-role-based-access-control.md#contributor-role-permissions).  
* Usuários não administrativos em seu locatário do AD do Azure podem [registrar aplicativos AD](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions) se registros do aplicativo hello configuração está definido muito**Sim**.  Se os registros do aplicativo hello configuração está definido muito**não**, usuário Olá executar essa ação deve ser um administrador global no AD do Azure. 

Se você não for um membro da instância do Active Directory da assinatura Olá antes que sejam adicionadas toohello administrador/coadministrador função global da assinatura hello, são adicionados o tooActive diretório como convidado. Nessa situação, você receberá um "você não tem permissões toocreate..." saudação de aviso **adicionar conta de automação** folha. Os usuários que foram adicionados toohello administrador/coadministrador função global primeiro pode ser removida da instância do Active Directory da assinatura hello e adicionado novamente toomake-los como um usuário completo no Active Directory. tooverify nesta situação, do hello **Active Directory do Azure** painel Olá portal do Azure, selecione **usuários e grupos**, selecione **todos os usuários** e, depois de selecionar Olá usuário específico, selecione **perfil**. Olá valor Olá **o tipo de usuário** atributo sob o perfil de usuários Olá não deve ser iguais **convidado**.

## <a name="create-run-as-account-from-hello-portal"></a>Criar conta executar como do portal de saudação
Nesta seção, execute Olá tooupdate as etapas a seguir sua conta de automação do Azure da saudação portal do Azure.  Você cria Olá contas executar como e clássico executar como individualmente, e se não precisar de recursos toomanage no portal do Azure clássico de hello, assim você pode criar conta executar como do Azure de saudação.  

processo de saudação cria Olá itens a seguir na sua conta de automação.

**Para contas Executar como:**

* Cria um aplicativo do AD do Azure com um certificado autoassinado, cria uma conta de serviço principal para o aplicativo hello no AD do Azure e atribui a função de Colaborador de saudação para conta de saudação em sua assinatura atual. Você pode alterar essa configuração tooOwner ou qualquer outra função. Para obter mais informações, confira [Controle de acesso baseado em função na Automação do Azure](automation-role-based-access-control.md).
* Cria um ativo de certificado de automação chamado *AzureRunAsCertificate* em Olá especificado na conta de automação. ativo de certificado Olá mantém Olá chave privada do certificado que é usado pelo aplicativo hello AD do Azure.
* Cria um ativo de conexão de automação chamado *AzureRunAsConnection* em Olá especificado na conta de automação. ativo de conexão Olá mantém applicationId hello, tenantId, subscriptionId e a impressão digital do certificado.

**Para contas Executar como clássicas:**

* Cria um ativo de certificado de automação chamado *AzureClassicRunAsCertificate* em Olá especificado na conta de automação. ativo de certificado Olá mantém a chave privada do certificado Olá usado pelo certificado de gerenciamento de saudação.
* Cria um ativo de conexão de automação chamado *AzureClassicRunAsConnection* em Olá especificado na conta de automação. ativo de conexão Olá contém o nome da assinatura hello, subscriptionId e nome do ativo de certificado.

1. Entrar toohello portal do Azure com uma conta que seja membro da função de administradores de assinatura hello e coadministrador da assinatura de saudação.
2. Na folha de conta de automação hello, selecione **contas executar como** na seção Olá **configurações de conta**.  
3. Dependendo da conta de que você precisa, selecione **Conta Executar como do Azure** ou **Conta Executar como Clássica do Azure**.  Depois de selecionar qualquer Olá **adicionar executar como do Azure** ou **adicionar Azure clássico conta executar como** lâmina aparece e depois de revisar as informações de visão geral de saudação, clique em **criar** tooproceed com a criação da conta executar como.  
4. Enquanto o Azure cria uma conta executar como do hello, você pode acompanhar o progresso de saudação em **notificações** de saudação menu e uma faixa é exibida informando Olá conta está sendo criada.  Esse processo pode levar alguns toocomplete de minutos.  

## <a name="create-run-as-account-using-powershell-script"></a>Criar conta Executar como usando um script do PowerShell
Este script do PowerShell inclui suporte para Olá configurações a seguir:

* Crie uma conta Executar como usando um certificado autoassinado.
* Crie uma conta Executar como e uma conta Executar como Clássica usando um certificado autoassinado.
* Crie uma conta Executar como e uma conta Executar como Clássica usando um certificado corporativo.
* Crie uma conta executar como e uma conta clássico executar como usando um certificado autoassinado no hello nuvem do Azure governamental.

Dependendo da opção de configuração de saudação que selecionar script hello cria Olá itens a seguir.

**Para contas Executar como:**

* Cria um Azure AD aplicativo toobe exportado com a saudação autoassinada ou chave pública do certificado da empresa, cria uma conta de serviço principal para o aplicativo hello no AD do Azure e atribui Olá função Colaborador para conta Olá no seu atual assinatura. Você pode alterar essa configuração tooOwner ou qualquer outra função. Para obter mais informações, confira [Controle de acesso baseado em função na Automação do Azure](automation-role-based-access-control.md).
* Cria um ativo de certificado de automação chamado *AzureRunAsCertificate* em Olá especificado na conta de automação. ativo de certificado Olá mantém Olá chave privada do certificado que é usado pelo aplicativo hello AD do Azure.
* Cria um ativo de conexão de automação chamado *AzureRunAsConnection* em Olá especificado na conta de automação. ativo de conexão Olá mantém applicationId hello, tenantId, subscriptionId e a impressão digital do certificado.

**Para contas Executar como clássicas:**

* Cria um ativo de certificado de automação chamado *AzureClassicRunAsCertificate* em Olá especificado na conta de automação. ativo de certificado Olá mantém a chave privada do certificado Olá usado pelo certificado de gerenciamento de saudação.
* Cria um ativo de conexão de automação chamado *AzureClassicRunAsConnection* em Olá especificado na conta de automação. ativo de conexão Olá contém o nome da assinatura hello, subscriptionId e nome do ativo de certificado.

>[!NOTE]
> Se você selecionar a opção para criar uma conta clássico executar como, após a execução do script hello, carregamento Olá pública repositório de certificados gerenciamento de toohello (extensão de nome de arquivo. cer) para a assinatura de saudação que Olá conta de automação foi criado no.
> 

1. Salve Olá script a seguir em seu computador. Neste exemplo, salve-o com o nome de arquivo hello *RunAsAccount.ps1 novo*.

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
        $KeyCredential.EndDate = Get-Date $PfxCert.GetExpirationDateString()
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
        if (!(($AzureRMProfileVersion.Major -ge 3 -and $AzureRMProfileVersion.Minor -ge 0) -or ($AzureRMProfileVersion.Major -gt 3)))
        {
            Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
            return
        }

        Login-AzureRmAccount -Environment $EnvironmentName 
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
        $SubscriptionName = $subscription.Subscription.Name
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. Em seu computador, inicie **do Windows PowerShell** de saudação **iniciar** tela com direitos de usuário elevados.
3. De saudação elevado shell de linha de comando, vá toohello pasta que contém o script hello criado na etapa 1.  
4. Execute script hello usando valores de parâmetro de saudação para configuração Olá que precisar.

    **Criar uma conta Executar como usando um certificado autoassinado**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    **Criar uma conta Executar como e uma conta Executar como Clássica usando um certificado autoassinado**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    **Criar uma conta Executar como e uma conta Executar como Clássica usando um certificado corporativo**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    **Criar uma conta executar como e uma conta clássico executar como usando um certificado autoassinado no hello nuvem Azure Government**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > Depois que o script hello executado, será tooauthenticate solicitado com o Azure. Entrar com uma conta que seja membro da função de administradores de assinatura hello e coadministrador da assinatura de saudação.
    >
    >

Depois que o script hello foi executada com êxito, observe o seguinte Olá:
* Se você criou uma conta clássico executar como com um certificado autoassinado público (arquivo. cer), script hello cria e salva-a pasta de arquivos temporários toohello no computador em que o perfil de usuário Olá *%USERPROFILE%\AppData\Local\Temp*, que você usou a sessão do PowerShell Olá tooexecute.
* Se tiver criado uma conta Executar como Clássica com um certificado público corporativo (arquivo .cer), use este certificado. Siga as instruções de saudação de [carregar um certificado de API de gerenciamento toohello portal clássico do Azure](../azure-api-management-certs.md)e, em seguida, validar a configuração de credencial de saudação com recursos de implantação clássico usando Olá [código de exemplo tooauthenticate com recursos de implantação clássico do Azure](automation-verify-runas-authentication.md#classic-run-as-authentication). 
* Se você fez *não* criar uma conta clássico executar como, autenticar com recursos de Gerenciador de recursos e validar a configuração de credencial de saudação usando Olá [código para autenticar com o serviço de gerenciamento de exemplo recursos](automation-verify-runas-authentication.md#automation-run-as-authentication).

## <a name="next-steps"></a>Próximas etapas
* Para obter mais informações sobre entidades de serviço, consulte muito[objetos Application e entidade de serviço](../active-directory/active-directory-application-objects.md).
* Para obter mais informações sobre certificados e serviços do Azure, consulte muito[visão geral de certificados para serviços de nuvem do Azure](../cloud-services/cloud-services-certs-create.md).
