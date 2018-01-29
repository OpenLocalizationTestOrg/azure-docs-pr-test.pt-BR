---
title: "Criar contas Executar como da Automação do Azure | Microsoft Docs"
description: "Este artigo descreve como atualizar sua conta de Automação e criar contas Executar como com o PowerShell ou a partir do portal."
services: automation
documentationcenter: 
author: georgewallace
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/27/2017
ms.author: magoedte
ms.openlocfilehash: 74d363be48972b40ba6a50b845acea78e1b5cc20
ms.sourcegitcommit: 9292e15fc80cc9df3e62731bafdcb0bb98c256e1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/10/2018
---
# <a name="update-your-automation-account-authentication-with-run-as-accounts"></a>Atualizar a autenticação de conta de Automação com contas Executar como 
Você pode atualizar sua conta de Automação existente no portal do Azure ou usar o PowerShell se:

* Você criar uma conta de Automação, mas se recusar a criar a conta Executar como.
* Você já usa uma conta de Automação para gerenciar recursos do Resource Manager e quer atualizá-la para incluir a conta Executar como para autenticação de runbook.
* Você já usar uma conta de Automação para gerenciar os recursos clássicos e quiser atualizá-la para usar a conta Executar como Clássica em vez de criar uma nova conta e migrar seus runbooks e ativos para ela.   

O processo cria os seguintes itens na sua conta de Automação.

**Para contas Executar como:**

* Cria um aplicativo do Azure AD com um certificado autoassinado, cria uma conta de entidade de serviço para o aplicativo no Azure AD e atribui a função de Colaborador à conta na assinatura atual. Você pode alterar essa configuração para Proprietário ou qualquer outra função. Para obter mais informações, confira [Controle de acesso baseado em função na Automação do Azure](automation-role-based-access-control.md).
* Cria um ativo de certificado de Automação chamado *AzureRunAsCertificate* na conta de Automação especificada. O ativo de certificado contém a chave privada do certificado que é usada pelo aplicativo do Azure AD.
* Cria um ativo de conexão de Automação chamado *AzureRunAsConnection* na conta de Automação especificada. O ativo de conexão contém applicationId, tenantId, subscriptionId e a impressão digital do certificado.

**Para contas Executar como clássicas:**

* Cria um ativo de certificado de Automação chamado *AzureClassicRunAsCertificate* na conta de Automação especificada. O ativo de certificado contém a chave privada do certificado usada pelo certificado de gerenciamento.
* Cria um ativo de conexão de Automação chamado *AzureClassicRunAsConnection* na conta de Automação especificada. O ativo de conexão contém o nome da assinatura, subscriptionId e o nome do ativo de certificado.

## <a name="prerequisites"></a>Pré-requisitos
Se você optar por [usar o PowerShell para criar as contas Executar como](#create-run-as-account-using-powershell), esse processo requer:

* O Windows 10 e Windows Server 2016 com módulos do Azure Resource Manager 3.4.1 e posterior. O script do PowerShell não oferece suporte a versões anteriores do Windows.
* Azure PowerShell 1.0 e posterior. Para obter informações sobre a versão 1.0 do PowerShell, confira [Como instalar e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs).
* Uma conta de Automação, que é referenciada como o valor para os parâmetros *– AutomationAccountName* e *- ApplicationDisplayName*.

Para obter os valores para *SubscriptionID*, *ResourceGroup* e *AutomationAccountName*, que são parâmetros obrigatórios para o script, faça o seguinte:

1. No portal do Azure, clique em **Mais serviços** encontrado no canto inferior esquerdo. Na lista de recursos, digite **Automação**. Quando você começa a digitar, a lista é filtrada com base em sua entrada. Selecione **Contas de Automação**.
2. Na página conta de Automação, selecione sua conta de Automação e, em seguida, em **Configurações de conta** selecione **Propriedades**.  
3. Observe os valores na página **Propriedades**.<br><br> ![A folha "Propriedades" da conta de Automação](media/automation-create-runas-account/automation-account-properties.png)  

### <a name="required-permissions-to-update-your-automation-account"></a>Permissões necessárias para atualizar sua conta da Automação
Para atualizar uma conta da Automação, você deve ter os seguintes privilégios e permissões específicas necessárias para concluir este tópico.   
 
* Sua conta de usuário do AD precisa ser adicionada a uma função com permissões equivalentes à função de Colaborador para recursos Microsoft.Automation conforme descrito no artigo [Controle de acesso baseado em função na Automação do Azure](automation-role-based-access-control.md#contributor-role-permissions).  
* Usuários não administradores em seu locatário do Azure AD podem [registrar aplicativos do AD](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions) se a opção **Os usuários podem registrar aplicativos** do o locatário do Azure AD na página **Configurações do usuário** está definida como **Sim**. Se a configuração de registros do aplicativo estiver definido como **Não**, o usuário que executa esta ação deverá ser um administrador global no Azure AD.

Caso não seja membro da instância do Active Directory da assinatura antes de ser adicionados à função de administrador global/coadministrador da assinatura, você será adicionado ao Active Directory como convidado. Nesse caso, você receberá um aviso "Você não tem permissões para criar..." na folha **Adicionar Conta de Automação**. Os usuários adicionados à função de administrador global/coadministrador primeiro podem ser removidos das assinaturas da instância do Active Directory e adicionados novamente para torná-los Usuários completos no Active Directory. Para verificar essa situação, no painel **Azure Active Directory** no portal do Azure, selecione **Usuários e grupos**, selecione **Todos os usuários** e, depois de selecionar o usuário específico, selecione **Perfil**. O valor do atributo **Tipo de usuário** sob o perfil de usuários não deve ser igual a **Convidado**.

## <a name="create-run-as-account-from-the-portal"></a>Criar a conta Executar como no portal
Nesta seção, execute as seguintes etapas para atualizar sua conta de Automação do Azure no portal do Azure.  Você pode criar as contas Executar Como e Executar Como Clássicas individualmente. Se você não precisa gerenciar recursos clássicos, é possível criar apenas a conta Executar Como do Azure.  

1. Conecte-se no Portal do Azure com uma conta que seja membro da função Administradores da Assinatura e coadministradora da assinatura.
2. No portal do Azure, clique em **Mais serviços** encontrado no canto inferior esquerdo. Na lista de recursos, digite **Automação**. Quando você começa a digitar, a lista é filtrada com base em sua entrada. Selecione **Contas de Automação**.
3. Na página **Contas de Automação**, selecione sua conta de Automação da lista de contas de Automação.
4. No painel do lado esquerdo, selecione **Contas Executar como** na seção **Configurações de conta**.  
5. Dependendo da conta de que você precisa, selecione **Conta Executar como do Azure** ou **Conta Executar como Clássica do Azure**.  Após a seleção, o painel **Adicionar Executar como do Azure** ou **Adicionar conta Executar como Clássica do Azure** aparecerá e após a revisão das informações de visão geral, clique em **Criar** para prosseguir com a criação da conta Executar como.  
6. Enquanto o Azure cria a conta Executar como, você poderá acompanhar o andamento em **Notificações** no menu.  Uma faixa também é exibida informando que a conta está sendo criada.  A conclusão desse processo pode levar alguns minutos.  

## <a name="create-run-as-account-using-powershell-script"></a>Criar conta Executar como usando um script do PowerShell
Este script do PowerShell inclui suporte para as seguintes configurações:

* Crie uma conta Executar como usando um certificado autoassinado.
* Crie uma conta Executar como e uma conta Executar como Clássica usando um certificado autoassinado.
* Criar uma conta Executar como e uma conta Clássica Executar como usando um certificado emitido por sua autoridade de certificação corporativa (CA).
* Crie uma conta Executar como e uma conta Executar como Clássica usando um certificado autoassinado na nuvem do Azure Governamental.

>[!NOTE]
> Se selecionar a opção para criar uma conta Executar como Clássica, depois que o script for executado, carregue o certificado público (extensão de nome de arquivo .cer) para o repositório de gerenciamento da assinatura em que a conta de Automação foi criada.
> 

1. Salve o script a seguir em seu computador. Neste exemplo, salve-o com o nome de arquivo *New-RunAsAccount.ps1*.

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

         function CreateSelfSignedCertificate([string] $certificateName, [string] $selfSignedCertPlainPassword,
                                        [string] $certPath, [string] $certPathCer, [string] $selfSignedCertNoOfMonthsUntilExpired ) {
         $Cert = New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation cert:\LocalMachine\My `
             -KeyExportPolicy Exportable -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
             -NotAfter (Get-Date).AddMonths($selfSignedCertNoOfMonthsUntilExpired) -HashAlgorithm SHA256

         $CertPassword = ConvertTo-SecureString $selfSignedCertPlainPassword -AsPlainText -Force
         Export-PfxCertificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPath -Password $CertPassword -Force | Write-Verbose
         Export-Certificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPathCer -Type CERT | Write-Verbose
         }

         function CreateServicePrincipal([System.Security.Cryptography.X509Certificates.X509Certificate2] $PfxCert, [string] $applicationDisplayName) {  
         $keyValue = [System.Convert]::ToBase64String($PfxCert.GetRawCertData())
         $keyId = (New-Guid).Guid

         $startDate = Get-Date
         $endDate = (Get-Date $PfxCert.GetExpirationDateString()).AddDays(-1)
         
         #Create an Azure AD application, AD App Credential, AD ServicePrincipal
         $Application = New-AzureRmADApplication -DisplayName $ApplicationDisplayName -HomePage ("http://" + $applicationDisplayName) -IdentifierUris ("http://" + $keyId) 
         $ApplicationCredential = New-AzureRmADAppCredential -ApplicationId $Application.ApplicationId -CertValue $keyValue -StartDate $startDate -EndDate $endDate 
         $ServicePrincipal = New-AzureRMADServicePrincipal -ApplicationId $Application.ApplicationId 
         $GetServicePrincipal = Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id

         # Sleep here for a few seconds to allow the service principal application to become active (ordinarily takes a few seconds)
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
         if (!(($AzureRMProfileVersion.Major -ge 3 -and $AzureRMProfileVersion.Minor -ge 4) -or ($AzureRMProfileVersion.Major -gt 3)))
         {
             Write-Error -Message "Please install the latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
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
            CreateSelfSignedCertificate $CertificateName $PfxCertPlainPasswordForRunAsAccount $PfxCertPathForRunAsAccount $CerCertPathForRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
         }

         # Create a service principal
         $PfxCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($PfxCertPathForRunAsAccount, $PfxCertPlainPasswordForRunAsAccount)
         $ApplicationId=CreateServicePrincipal $PfxCert $ApplicationDisplayName

         # Create the Automation certificate asset
         CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

         # Populate the ConnectionFieldValues
         $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
         $TenantID = $SubscriptionInfo | Select TenantId -First 1
         $Thumbprint = $PfxCert.Thumbprint
         $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

         # Create an Automation connection asset named AzureRunAsConnection in the Automation account. This connection uses the service principal.
         CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

         if ($CreateClassicRunAsAccount) {
              # Create a Run As account by using a service principal
              $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
              $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
              $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
              $UploadMessage = "Please upload the .cer format of #CERT# to the Management store by following the steps below." + [Environment]::NewLine +
                      "Log in to the Microsoft Azure portal (https://portal.azure.com) and select Subscriptions -> Management Certificates." + [Environment]::NewLine +
                      "Then click Upload and upload the .cer format of #CERT#"

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
               CreateSelfSignedCertificate $ClassicRunAsAccountCertificateName $PfxCertPlainPasswordForClassicRunAsAccount $PfxCertPathForClassicRunAsAccount $CerCertPathForClassicRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
         }

         # Create the Automation certificate asset
         CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

         # Populate the ConnectionFieldValues
         $SubscriptionName = $subscription.Subscription.Name
         $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

         # Create an Automation connection asset named AzureRunAsConnection in the Automation account. This connection uses the service principal.
         CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

         Write-Host -ForegroundColor red $UploadMessage
         }

2. Em sua máquina, inicie o **Windows PowerShell** na tela **Iniciar** com direitos de usuário elevados.
3. A partir do shell da linha de comando com privilégios elevados, acesse a pasta que contém o script que você criou na etapa 1.  
4. Execute o script usando os valores de parâmetro para a configuração necessária.

    **Criar uma conta Executar como usando um certificado autoassinado**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    **Criar uma conta Executar como e uma conta Executar como Clássica usando um certificado autoassinado**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    **Criar uma conta Executar como e uma conta Executar como Clássica usando um certificado corporativo**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    **Criar uma conta Executar como e uma conta Executar como Clássica usando um certificado autoassinado na nuvem do Azure Governamental**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > Depois que o script for executado, você deverá se autenticar no Azure. Ente com uma conta que seja membro da função de administradores de assinatura e coadministrador da assinatura.
    >
    >

Depois que o script for executado com êxito, observe o seguinte:
* Se você tiver criado uma conta Executar como Clássica com um certificado autoassinado público (arquivo .cer), o script a criará e salvará na pasta de arquivos temporários no computador sob o perfil de usuário *%USERPROFILE%\AppData\Local\Temp*, que é usado para executar a sessão do PowerShell.
* Se tiver criado uma conta Executar como Clássica com um certificado público corporativo (arquivo .cer), use este certificado. Siga as instruções para [carregar um certificado de API de gerenciamento no Portal do Azure](../azure-api-management-certs.md) e, então, valide a configuração de credencial com recursos de implantação clássicos usando o [código de exemplo para se autenticar com os Recursos de implantação clássica do Azure](automation-verify-runas-authentication.md#classic-run-as-authentication). 
* Se *não* criou uma conta Executar como Clássica, autentique-se com os recursos do Resource Manager e valide a configuração de credenciais usando o [código de exemplo para autenticação com recursos de Gerenciamento de Serviços](automation-verify-runas-authentication.md#automation-run-as-authentication).

## <a name="next-steps"></a>Próximas etapas
* Para saber mais sobre Entidades de Serviço, veja [Objetos de aplicativo e objetos de entidade de serviço](../active-directory/active-directory-application-objects.md).
* Para saber mais sobre certificados e serviços do Azure, confira [Visão geral dos certificados de serviços de nuvem do Azure](../cloud-services/cloud-services-certs-create.md).
