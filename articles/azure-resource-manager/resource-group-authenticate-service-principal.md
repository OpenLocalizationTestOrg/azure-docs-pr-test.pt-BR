---
title: aaaCreate identidade para o aplicativo do Azure com o PowerShell | Microsoft Docs
description: "Descreve como controlam a toouse do Azure PowerShell toocreate um aplicativo do Active Directory do Azure e entidade de serviço e conceder acesso a tooresources por meio de acesso baseado em função. Ele mostra como tooauthenticate aplicativo com uma senha ou certificado."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: d2caf121-9fbe-4f00-bf9d-8f3d1f00a6ff
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: c534360799b590054a051e4426e5e27dccb559b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-powershell-toocreate-a-service-principal-tooaccess-resources"></a>Usar Azure PowerShell toocreate um serviço principal tooaccess recursos

Quando você tiver um aplicativo ou script que precisa de recursos de tooaccess, você pode configurar uma identidade para o aplicativo hello e autenticar o aplicativo hello com suas próprias credenciais. Essa identidade é conhecida como uma entidade de serviço. Essa abordagem permite:

* Atribua permissões de identidade de aplicativo toohello que são diferentes de suas próprias permissões. Normalmente, essas permissões são restrito tooexactly toodo precisa de qual aplicativo hello.
* Use um certificado para a autenticação ao executar um script autônomo.

Este tópico mostra como toouse [Azure PowerShell](/powershell/azure/overview) tooset backup de tudo que você precisa para toorun um aplicativo em suas próprias credenciais e identidade.

## <a name="required-permissions"></a>Permissões necessárias
toocomplete neste tópico, você deve ter permissões suficientes no Active Directory do Azure e sua assinatura do Azure. Especificamente, você deve ser capaz de toocreate um aplicativo de saudação do Active Directory do Azure e atribuir função de tooa principal do serviço de saudação. 

Olá mais fácil toocheck de maneira se sua conta tem permissões suficientes é por meio do portal hello. Consulte [Verificar permissão necessária](resource-group-create-service-principal-portal.md#required-permissions).

Agora, faça a seção tooa para autenticar com:

* [password](#create-service-principal-with-password)
* [certificado autoassinado](#create-service-principal-with-self-signed-certificate)
* [certificado da Autoridade de Certificação](#create-service-principal-with-certificate-from-certificate-authority)

## <a name="powershell-commands"></a>Comandos do PowerShell

tooset a uma entidade de serviço, use:

| Command | Descrição |
| ------- | ----------- | 
| [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | Cria uma entidade de serviço do Azure Active Directory |
| [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment) | Olá atribui especificado principal especificado do RBAC função toohello, a saudação especificado no escopo. |


## <a name="create-service-principal-with-password"></a>Criar a entidade de serviço com a senha

toocreate uma entidade de serviço com a função de Colaborador Olá para sua assinatura, use: 

```powershell
Login-AzureRmAccount
$sp = New-AzureRmADServicePrincipal -DisplayName exampleapp -Password "{provide-password}"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

exemplo Hello suspenso por 20 segundos tooallow algum tempo para Olá novo serviço principal toopropagate em todo o Active Directory do Azure. Se o script não Aguarde tempo suficiente, você verá um erro dizendo: "PrincipalNotFound: Principal {id} não existe no diretório hello."

Olá script a seguir permite que você toospecify um escopo diferente de assinatura de padrão de saudação e repetições Olá atribuição de função se ocorrer um erro:

```powershell
Param (

 # Use tooset scope tooresource group. If no value is provided, scope is set toosubscription.
 [Parameter(Mandatory=$false)]
 [String] $ResourceGroup,

 # Use tooset subscription. If no value is provided, default subscription is used. 
 [Parameter(Mandatory=$false)]
 [String] $SubscriptionId,

 [Parameter(Mandatory=$true)]
 [String] $ApplicationDisplayName,

 [Parameter(Mandatory=$true)]
 [String] $Password
)

 Login-AzureRmAccount
 Import-Module AzureRM.Resources

 if ($SubscriptionId -eq "") 
 {
    $SubscriptionId = (Get-AzureRmContext).Subscription.Id
 }
 else
 {
    Set-AzureRmContext -SubscriptionId $SubscriptionId
 }

 if ($ResourceGroup -eq "")
 {
    $Scope = "/subscriptions/" + $SubscriptionId
 }
 else
 {
    $Scope = (Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop).ResourceId
 }

 
 # Create Service Principal for hello AD app
 $ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -Password $Password
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
```

Toonote de alguns itens sobre script hello:

* assinatura toogrant Olá identidade acesso toohello padrão, você não precisa tooprovide ResourceGroup ou SubscriptionId parâmetros.
* Especifica parâmetro de ResourceGroup hello somente quando desejar que o escopo do toolimit Olá Olá função atribuição tooa do grupo de recursos.
*  Neste exemplo, você deve adicionar função de Colaborador Olá serviço toohello principal. Para ver outras funções, confira [RBAC: funções internas](../active-directory/role-based-access-built-in-roles.md).
* script Hello suspenso por 15 segundos tooallow algum tempo para Olá novo serviço principal toopropagate em todo o Active Directory do Azure. Se o script não Aguarde tempo suficiente, você verá um erro dizendo: "PrincipalNotFound: Principal {id} não existe no diretório hello."
* Se você precisar de assinaturas de toomore acesso principal do serviço de saudação toogrant ou grupos de recursos, execute Olá `New-AzureRMRoleAssignment` cmdlet novamente com escopos diferentes.


### <a name="provide-credentials-through-powershell"></a>Fornecer as credenciais por meio do PowerShell
Agora, você precisa toolog em operações de tooperform aplicativo hello. Olá nome de usuário, use Olá `ApplicationId` que você criou para o aplicativo hello. Senha hello, use Olá especificada ao criar conta de saudação. 

```powershell   
$creds = Get-Credential
Login-AzureRmAccount -Credential $creds -ServicePrincipal -TenantId {tenant-id}
```

Olá ID de locatário não é confidencial, portanto pode incorporá-lo diretamente no seu script. Se você precisar de ID de locatário tooretrieve Olá, use:

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

## <a name="create-service-principal-with-self-signed-certificate"></a>Criar a entidade de serviço com um certificado autoassinado

toocreate uma entidade de serviço com um certificado autoassinado e uma função de Colaborador Olá para sua assinatura, use: 

```powershell
Login-AzureRmAccount
$cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
$keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

$sp = New-AzureRMADServicePrincipal -DisplayName exampleapp -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

exemplo Hello suspenso por 20 segundos tooallow algum tempo para Olá novo serviço principal toopropagate em todo o Active Directory do Azure. Se o script não Aguarde tempo suficiente, você verá um erro dizendo: "PrincipalNotFound: Principal {id} não existe no diretório hello."

Olá script a seguir permite que você toospecify um escopo diferente de assinatura de padrão de saudação e repetições Olá atribuição de função se ocorrer um erro. Você deve ter o Azure PowerShell 2.0 no Windows 10 ou Windows Server 2016.

```powershell
Param (

 # Use tooset scope tooresource group. If no value is provided, scope is set toosubscription.
 [Parameter(Mandatory=$false)]
 [String] $ResourceGroup,

 # Use tooset subscription. If no value is provided, default subscription is used. 
 [Parameter(Mandatory=$false)]
 [String] $SubscriptionId,

 [Parameter(Mandatory=$true)]
 [String] $ApplicationDisplayName
 )

 Login-AzureRmAccount
 Import-Module AzureRM.Resources

 if ($SubscriptionId -eq "") 
 {
    $SubscriptionId = (Get-AzureRmContext).Subscription.Id
 }
 else
 {
    Set-AzureRmContext -SubscriptionId $SubscriptionId
 }

 if ($ResourceGroup -eq "")
 {
    $Scope = "/subscriptions/" + $SubscriptionId
 }
 else
 {
    $Scope = (Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop).ResourceId
 }

 $cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
 $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

 $ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
```

Toonote de alguns itens sobre script hello:

* assinatura toogrant Olá identidade acesso toohello padrão, você não precisa tooprovide ResourceGroup ou SubscriptionId parâmetros.
* Especifica parâmetro de ResourceGroup hello somente quando desejar que o escopo do toolimit Olá Olá função atribuição tooa do grupo de recursos.
* Neste exemplo, você deve adicionar função de Colaborador Olá serviço toohello principal. Para ver outras funções, confira [RBAC: funções internas](../active-directory/role-based-access-built-in-roles.md).
* script Hello suspenso por 15 segundos tooallow algum tempo para Olá novo serviço principal toopropagate em todo o Active Directory do Azure. Se o script não Aguarde tempo suficiente, você verá um erro dizendo: "PrincipalNotFound: Principal {id} não existe no diretório hello."
* Se você precisar de assinaturas de toomore acesso principal do serviço de saudação toogrant ou grupos de recursos, execute Olá `New-AzureRMRoleAssignment` cmdlet novamente com escopos diferentes.

Se você **não tem Windows 10 ou Windows Server 2016 Technical Preview**, você precisa Olá toodownload [gerador de certificado autoassinado](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) do Microsoft Script Center. Extraia o conteúdo e importar Olá cmdlet que é necessário.

```powershell  
# Only run if you could not use New-SelfSignedCertificate
Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
```
  
No script hello, substitua Olá dois certificados de saudação do toogenerate linhas a seguir.
  
```powershell
New-SelfSignedCertificateEx  -StoreLocation CurrentUser -StoreName My -Subject "CN=exampleapp" -KeySpec "Exchange" -FriendlyName "exampleapp"
$cert = Get-ChildItem -path Cert:\CurrentUser\my | where {$PSitem.Subject -eq 'CN=exampleapp' }
```

### <a name="provide-certificate-through-automated-powershell-script"></a>Fornecer certificado por meio do script PowerShell automatizado
Sempre que você entrar como uma entidade de serviço, você precisa tooprovide id de locatário de saudação do diretório de saudação para seu aplicativo do AD. Um locatário é uma instância do Active Directory do Azure. Se você tiver apenas uma assinatura, poderá usar:

```powershell
Param (
 
 [Parameter(Mandatory=$true)]
 [String] $CertSubject,
 
 [Parameter(Mandatory=$true)]
 [String] $ApplicationId,

 [Parameter(Mandatory=$true)]
 [String] $TenantId
 )

 $Thumbprint = (Get-ChildItem cert:\CurrentUser\My\ | Where-Object {$_.Subject -match $CertSubject }).Thumbprint
 Login-AzureRmAccount -ServicePrincipal -CertificateThumbprint $Thumbprint -ApplicationId $ApplicationId -TenantId $TenantId
```

aplicativo Hello ID e a ID de locatário não diferenciam minúsculas, portanto você pode inseri-los diretamente em seu script. Se você precisar de ID de locatário tooretrieve Olá, use:

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

Se você precisar de ID do aplicativo hello tooretrieve, use:

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="create-service-principal-with-certificate-from-certificate-authority"></a>Criar a entidade de serviço com um certificado da Autoridade de Certificação
toouse um certificado emitido por uma entidade de serviço de toocreate da autoridade de certificação, use Olá script a seguir:

```powershell
Param (
 [Parameter(Mandatory=$true)]
 [String] $ApplicationDisplayName,

 [Parameter(Mandatory=$true)]
 [String] $SubscriptionId,

 [Parameter(Mandatory=$true)]
 [String] $CertPath,

 [Parameter(Mandatory=$true)]
 [String] $CertPlainPassword
 )

 Login-AzureRmAccount
 Import-Module AzureRM.Resources
 Set-AzureRmContext -SubscriptionId $SubscriptionId

 $KeyId = (New-Guid).Guid
 $CertPassword = ConvertTo-SecureString $CertPlainPassword -AsPlainText -Force

 $PFXCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($CertPath, $CertPassword)
 $KeyValue = [System.Convert]::ToBase64String($PFXCert.GetRawCertData())

 $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
 $KeyCredential.StartDate = $PFXCert.NotBefore
 $KeyCredential.EndDate= $PFXCert.NotAfter
 $KeyCredential.KeyId = $KeyId
 $KeyCredential.CertValue = $KeyValue

 $ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -KeyCredentials $keyCredential
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
 
 $NewRole
```

Toonote de alguns itens sobre script hello:

* O acesso é toohello no escopo de assinatura.
* Neste exemplo, você deve adicionar função de Colaborador Olá serviço toohello principal. Para ver outras funções, confira [RBAC: funções internas](../active-directory/role-based-access-built-in-roles.md).
* script Hello suspenso por 15 segundos tooallow algum tempo para Olá novo serviço principal toopropagate em todo o Active Directory do Azure. Se o script não Aguarde tempo suficiente, você verá um erro dizendo: "PrincipalNotFound: Principal {id} não existe no diretório hello."
* Se você precisar de assinaturas de toomore acesso principal do serviço de saudação toogrant ou grupos de recursos, execute Olá `New-AzureRMRoleAssignment` cmdlet novamente com escopos diferentes.

### <a name="provide-certificate-through-automated-powershell-script"></a>Fornecer certificado por meio do script PowerShell automatizado
Sempre que você entrar como uma entidade de serviço, você precisa tooprovide id de locatário de saudação do diretório de saudação para seu aplicativo do AD. Um locatário é uma instância do Active Directory do Azure.

```powershell
Param (
 
 [Parameter(Mandatory=$true)]
 [String] $CertPath,

 [Parameter(Mandatory=$true)]
 [String] $CertPlainPassword,
 
 [Parameter(Mandatory=$true)]
 [String] $ApplicationId,

 [Parameter(Mandatory=$true)]
 [String] $TenantId
 )

 $CertPassword = ConvertTo-SecureString $CertPlainPassword -AsPlainText -Force
 $PFXCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($CertPath, $CertPassword)
 $Thumbprint = $PFXCert.Thumbprint

 Login-AzureRmAccount -ServicePrincipal -CertificateThumbprint $Thumbprint -ApplicationId $ApplicationId -TenantId $TenantId
```

aplicativo Hello ID e a ID de locatário não diferenciam minúsculas, portanto você pode inseri-los diretamente em seu script. Se você precisar de ID de locatário tooretrieve Olá, use:

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

Se você precisar de ID do aplicativo hello tooretrieve, use:

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="change-credentials"></a>Alterar credenciais

credenciais de saudação toochange para um aplicativo do AD, devido a um comprometimento de segurança ou uma expiração de credencial, usam Olá [remover AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) e [AzureRmADAppCredential novo](/powershell/module/azurerm.resources/new-azurermadappcredential) cmdlets.

tooremove todas as credenciais de saudação para um aplicativo, use:

```powershell
Remove-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -All
```

tooadd uma senha, use:

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -Password p@ssword!
```

tooadd um valor de certificado, crie um certificado autoassinado, conforme mostrado neste tópico. Em seguida, use:

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
```

## <a name="save-access-token-toosimplify-log-in"></a>Salvar o token toosimplify login de acesso
tooavoid fornecendo Olá serviço principal credenciais sempre que ele precisa toolog no, você pode salvar o token de acesso de saudação.

toouse Olá token de acesso atual em uma sessão posterior, salvar perfil hello.
   
```powershell
Save-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```
   
Abra o perfil hello e examine seu conteúdo. Observe que ele contém um token de acesso. Em vez de manualmente fazer logon novamente, basta carrega o perfil de saudação.
   
```powershell
Select-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```

> [!NOTE]
> o token de acesso Olá expira, portanto usar um perfil salvo só funciona para como Olá token é válido.
>  

Como alternativa, você pode chamar operações REST do PowerShell toolog no. De resposta de autenticação hello, você pode recuperar o token de acesso de saudação para uso com outras operações. Para obter um exemplo de recuperar o token de acesso de saudação ao chamar operações REST, consulte [gerar um Token de acesso](resource-manager-rest-api.md#generating-an-access-token).

## <a name="debug"></a>Depurar

Você pode encontrar hello os erros a seguir ao criar uma entidade de serviço:

* **"Authentication_Unauthorized"** ou **"nenhuma assinatura encontrada no contexto de Olá".** -Você vir esse erro quando sua conta não tem Olá [as permissões necessárias](#required-permissions) no Active Directory do Azure de saudação tooregister um aplicativo. Normalmente, você verá esse erro somente quando os usuários administradores no Active Directory do Azure puderem registrar aplicativos e sua conta não for um administrador. Peça ao seu administrador tooeither atribuir a função administrador tooan ou tooenable usuários tooregister aplicativos.

* Sua conta **"não tem autorização tooperform ação 'Microsoft.Authorization/roleAssignments/write' no escopo 'assinaturas / {guid}'."**  -Consulte esse erro quando sua conta não tem suficientes tooassign de permissões uma identidade de tooan de função. Peça ao seu tooadd do administrador de assinatura função administrador do acesso tooUser.

## <a name="sample-applications"></a>Aplicativos de exemplo
Para obter informações sobre como fazer logon como um aplicativo hello através de diferentes plataformas, consulte:

* [.NET](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [Java](/java/azure/java-sdk-azure-authenticate)
* [Node.js](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [Python](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [Ruby](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a>Próximas etapas
* Para obter etapas detalhadas sobre como integrar um aplicativo do Azure para gerenciar recursos, consulte [tooauthorization de guia do desenvolvedor com hello API do Gerenciador de recursos do Azure](resource-manager-api-authentication.md).
* Para obter uma explicação mais detalhada de aplicativos e entidades de serviço, consulte [Objetos de aplicativo e de entidade de serviço](../active-directory/active-directory-application-objects.md). 
* Para obter mais informações sobre a autenticação do Active Directory do Azure, consulte [Cenários de Autenticação do Azure AD](../active-directory/active-directory-authentication-scenarios.md).
* Para obter uma lista de ações disponíveis que podem ser concedidas ou negadas toousers, consulte [operações do provedor de recursos do Gerenciador de recursos do Azure](../active-directory/role-based-access-control-resource-provider-operations.md).

