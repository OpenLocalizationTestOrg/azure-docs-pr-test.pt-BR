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
# <a name="use-azure-powershell-toocreate-a-service-principal-tooaccess-resources"></a><span data-ttu-id="d52d3-104">Usar Azure PowerShell toocreate um serviço principal tooaccess recursos</span><span class="sxs-lookup"><span data-stu-id="d52d3-104">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>

<span data-ttu-id="d52d3-105">Quando você tiver um aplicativo ou script que precisa de recursos de tooaccess, você pode configurar uma identidade para o aplicativo hello e autenticar o aplicativo hello com suas próprias credenciais.</span><span class="sxs-lookup"><span data-stu-id="d52d3-105">When you have an app or script that needs tooaccess resources, you can set up an identity for hello app and authenticate hello app with its own credentials.</span></span> <span data-ttu-id="d52d3-106">Essa identidade é conhecida como uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="d52d3-106">This identity is known as a service principal.</span></span> <span data-ttu-id="d52d3-107">Essa abordagem permite:</span><span class="sxs-lookup"><span data-stu-id="d52d3-107">This approach enables you to:</span></span>

* <span data-ttu-id="d52d3-108">Atribua permissões de identidade de aplicativo toohello que são diferentes de suas próprias permissões.</span><span class="sxs-lookup"><span data-stu-id="d52d3-108">Assign permissions toohello app identity that are different than your own permissions.</span></span> <span data-ttu-id="d52d3-109">Normalmente, essas permissões são restrito tooexactly toodo precisa de qual aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="d52d3-109">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span>
* <span data-ttu-id="d52d3-110">Use um certificado para a autenticação ao executar um script autônomo.</span><span class="sxs-lookup"><span data-stu-id="d52d3-110">Use a certificate for authentication when executing an unattended script.</span></span>

<span data-ttu-id="d52d3-111">Este tópico mostra como toouse [Azure PowerShell](/powershell/azure/overview) tooset backup de tudo que você precisa para toorun um aplicativo em suas próprias credenciais e identidade.</span><span class="sxs-lookup"><span data-stu-id="d52d3-111">This topic shows you how toouse [Azure PowerShell](/powershell/azure/overview) tooset up everything you need for an application toorun under its own credentials and identity.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="d52d3-112">Permissões necessárias</span><span class="sxs-lookup"><span data-stu-id="d52d3-112">Required permissions</span></span>
<span data-ttu-id="d52d3-113">toocomplete neste tópico, você deve ter permissões suficientes no Active Directory do Azure e sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="d52d3-113">toocomplete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span></span> <span data-ttu-id="d52d3-114">Especificamente, você deve ser capaz de toocreate um aplicativo de saudação do Active Directory do Azure e atribuir função de tooa principal do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="d52d3-114">Specifically, you must be able toocreate an app in hello Azure Active Directory, and assign hello service principal tooa role.</span></span> 

<span data-ttu-id="d52d3-115">Olá mais fácil toocheck de maneira se sua conta tem permissões suficientes é por meio do portal hello.</span><span class="sxs-lookup"><span data-stu-id="d52d3-115">hello easiest way toocheck whether your account has adequate permissions is through hello portal.</span></span> <span data-ttu-id="d52d3-116">Consulte [Verificar permissão necessária](resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="d52d3-116">See [Check required permission](resource-group-create-service-principal-portal.md#required-permissions).</span></span>

<span data-ttu-id="d52d3-117">Agora, faça a seção tooa para autenticar com:</span><span class="sxs-lookup"><span data-stu-id="d52d3-117">Now, proceed tooa section for authenticating with:</span></span>

* [<span data-ttu-id="d52d3-118">password</span><span class="sxs-lookup"><span data-stu-id="d52d3-118">password</span></span>](#create-service-principal-with-password)
* [<span data-ttu-id="d52d3-119">certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="d52d3-119">self-signed certificate</span></span>](#create-service-principal-with-self-signed-certificate)
* [<span data-ttu-id="d52d3-120">certificado da Autoridade de Certificação</span><span class="sxs-lookup"><span data-stu-id="d52d3-120">certificate from Certificate Authority</span></span>](#create-service-principal-with-certificate-from-certificate-authority)

## <a name="powershell-commands"></a><span data-ttu-id="d52d3-121">Comandos do PowerShell</span><span class="sxs-lookup"><span data-stu-id="d52d3-121">PowerShell commands</span></span>

<span data-ttu-id="d52d3-122">tooset a uma entidade de serviço, use:</span><span class="sxs-lookup"><span data-stu-id="d52d3-122">tooset up a service principal, you use:</span></span>

| <span data-ttu-id="d52d3-123">Command</span><span class="sxs-lookup"><span data-stu-id="d52d3-123">Command</span></span> | <span data-ttu-id="d52d3-124">Descrição</span><span class="sxs-lookup"><span data-stu-id="d52d3-124">Description</span></span> |
| ------- | ----------- | 
| [<span data-ttu-id="d52d3-125">New-AzureRmADServicePrincipal</span><span class="sxs-lookup"><span data-stu-id="d52d3-125">New-AzureRmADServicePrincipal</span></span>](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | <span data-ttu-id="d52d3-126">Cria uma entidade de serviço do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d52d3-126">Creates an Azure Active Directory service principal</span></span> |
| [<span data-ttu-id="d52d3-127">New-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="d52d3-127">New-AzureRmRoleAssignment</span></span>](/powershell/module/azurerm.resources/new-azurermroleassignment) | <span data-ttu-id="d52d3-128">Olá atribui especificado principal especificado do RBAC função toohello, a saudação especificado no escopo.</span><span class="sxs-lookup"><span data-stu-id="d52d3-128">Assigns hello specified RBAC role toohello specified principal, at hello specified scope.</span></span> |


## <a name="create-service-principal-with-password"></a><span data-ttu-id="d52d3-129">Criar a entidade de serviço com a senha</span><span class="sxs-lookup"><span data-stu-id="d52d3-129">Create service principal with password</span></span>

<span data-ttu-id="d52d3-130">toocreate uma entidade de serviço com a função de Colaborador Olá para sua assinatura, use:</span><span class="sxs-lookup"><span data-stu-id="d52d3-130">toocreate a service principal with hello Contributor role for your subscription, use:</span></span> 

```powershell
Login-AzureRmAccount
$sp = New-AzureRmADServicePrincipal -DisplayName exampleapp -Password "{provide-password}"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="d52d3-131">exemplo Hello suspenso por 20 segundos tooallow algum tempo para Olá novo serviço principal toopropagate em todo o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="d52d3-131">hello example sleeps for 20 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="d52d3-132">Se o script não Aguarde tempo suficiente, você verá um erro dizendo: "PrincipalNotFound: Principal {id} não existe no diretório hello."</span><span class="sxs-lookup"><span data-stu-id="d52d3-132">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>

<span data-ttu-id="d52d3-133">Olá script a seguir permite que você toospecify um escopo diferente de assinatura de padrão de saudação e repetições Olá atribuição de função se ocorrer um erro:</span><span class="sxs-lookup"><span data-stu-id="d52d3-133">hello following script enables you toospecify a scope other than hello default subscription, and retries hello role assignment if an error occurs:</span></span>

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

<span data-ttu-id="d52d3-134">Toonote de alguns itens sobre script hello:</span><span class="sxs-lookup"><span data-stu-id="d52d3-134">A few items toonote about hello script:</span></span>

* <span data-ttu-id="d52d3-135">assinatura toogrant Olá identidade acesso toohello padrão, você não precisa tooprovide ResourceGroup ou SubscriptionId parâmetros.</span><span class="sxs-lookup"><span data-stu-id="d52d3-135">toogrant hello identity access toohello default subscription, you do not need tooprovide either ResourceGroup or SubscriptionId parameters.</span></span>
* <span data-ttu-id="d52d3-136">Especifica parâmetro de ResourceGroup hello somente quando desejar que o escopo do toolimit Olá Olá função atribuição tooa do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d52d3-136">Specify hello ResourceGroup parameter only when you want toolimit hello scope of hello role assignment tooa resource group.</span></span>
*  <span data-ttu-id="d52d3-137">Neste exemplo, você deve adicionar função de Colaborador Olá serviço toohello principal.</span><span class="sxs-lookup"><span data-stu-id="d52d3-137">In this example, you add hello service principal toohello Contributor role.</span></span> <span data-ttu-id="d52d3-138">Para ver outras funções, confira [RBAC: funções internas](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="d52d3-138">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="d52d3-139">script Hello suspenso por 15 segundos tooallow algum tempo para Olá novo serviço principal toopropagate em todo o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="d52d3-139">hello script sleeps for 15 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="d52d3-140">Se o script não Aguarde tempo suficiente, você verá um erro dizendo: "PrincipalNotFound: Principal {id} não existe no diretório hello."</span><span class="sxs-lookup"><span data-stu-id="d52d3-140">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>
* <span data-ttu-id="d52d3-141">Se você precisar de assinaturas de toomore acesso principal do serviço de saudação toogrant ou grupos de recursos, execute Olá `New-AzureRMRoleAssignment` cmdlet novamente com escopos diferentes.</span><span class="sxs-lookup"><span data-stu-id="d52d3-141">If you need toogrant hello service principal access toomore subscriptions or resource groups, run hello `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>


### <a name="provide-credentials-through-powershell"></a><span data-ttu-id="d52d3-142">Fornecer as credenciais por meio do PowerShell</span><span class="sxs-lookup"><span data-stu-id="d52d3-142">Provide credentials through PowerShell</span></span>
<span data-ttu-id="d52d3-143">Agora, você precisa toolog em operações de tooperform aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="d52d3-143">Now, you need toolog in as hello application tooperform operations.</span></span> <span data-ttu-id="d52d3-144">Olá nome de usuário, use Olá `ApplicationId` que você criou para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="d52d3-144">For hello user name, use hello `ApplicationId` that you created for hello application.</span></span> <span data-ttu-id="d52d3-145">Senha hello, use Olá especificada ao criar conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="d52d3-145">For hello password, use hello one you specified when creating hello account.</span></span> 

```powershell   
$creds = Get-Credential
Login-AzureRmAccount -Credential $creds -ServicePrincipal -TenantId {tenant-id}
```

<span data-ttu-id="d52d3-146">Olá ID de locatário não é confidencial, portanto pode incorporá-lo diretamente no seu script.</span><span class="sxs-lookup"><span data-stu-id="d52d3-146">hello tenant ID is not sensitive, so you can embed it directly in your script.</span></span> <span data-ttu-id="d52d3-147">Se você precisar de ID de locatário tooretrieve Olá, use:</span><span class="sxs-lookup"><span data-stu-id="d52d3-147">If you need tooretrieve hello tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

## <a name="create-service-principal-with-self-signed-certificate"></a><span data-ttu-id="d52d3-148">Criar a entidade de serviço com um certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="d52d3-148">Create service principal with self-signed certificate</span></span>

<span data-ttu-id="d52d3-149">toocreate uma entidade de serviço com um certificado autoassinado e uma função de Colaborador Olá para sua assinatura, use:</span><span class="sxs-lookup"><span data-stu-id="d52d3-149">toocreate a service principal with a self-signed certificate and hello Contributor role for your subscription, use:</span></span> 

```powershell
Login-AzureRmAccount
$cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
$keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

$sp = New-AzureRMADServicePrincipal -DisplayName exampleapp -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="d52d3-150">exemplo Hello suspenso por 20 segundos tooallow algum tempo para Olá novo serviço principal toopropagate em todo o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="d52d3-150">hello example sleeps for 20 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="d52d3-151">Se o script não Aguarde tempo suficiente, você verá um erro dizendo: "PrincipalNotFound: Principal {id} não existe no diretório hello."</span><span class="sxs-lookup"><span data-stu-id="d52d3-151">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>

<span data-ttu-id="d52d3-152">Olá script a seguir permite que você toospecify um escopo diferente de assinatura de padrão de saudação e repetições Olá atribuição de função se ocorrer um erro.</span><span class="sxs-lookup"><span data-stu-id="d52d3-152">hello following script enables you toospecify a scope other than hello default subscription, and retries hello role assignment if an error occurs.</span></span> <span data-ttu-id="d52d3-153">Você deve ter o Azure PowerShell 2.0 no Windows 10 ou Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="d52d3-153">You must have Azure PowerShell 2.0 on Windows 10 or Windows Server 2016.</span></span>

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

<span data-ttu-id="d52d3-154">Toonote de alguns itens sobre script hello:</span><span class="sxs-lookup"><span data-stu-id="d52d3-154">A few items toonote about hello script:</span></span>

* <span data-ttu-id="d52d3-155">assinatura toogrant Olá identidade acesso toohello padrão, você não precisa tooprovide ResourceGroup ou SubscriptionId parâmetros.</span><span class="sxs-lookup"><span data-stu-id="d52d3-155">toogrant hello identity access toohello default subscription, you do not need tooprovide either ResourceGroup or SubscriptionId parameters.</span></span>
* <span data-ttu-id="d52d3-156">Especifica parâmetro de ResourceGroup hello somente quando desejar que o escopo do toolimit Olá Olá função atribuição tooa do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d52d3-156">Specify hello ResourceGroup parameter only when you want toolimit hello scope of hello role assignment tooa resource group.</span></span>
* <span data-ttu-id="d52d3-157">Neste exemplo, você deve adicionar função de Colaborador Olá serviço toohello principal.</span><span class="sxs-lookup"><span data-stu-id="d52d3-157">In this example, you add hello service principal toohello Contributor role.</span></span> <span data-ttu-id="d52d3-158">Para ver outras funções, confira [RBAC: funções internas](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="d52d3-158">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="d52d3-159">script Hello suspenso por 15 segundos tooallow algum tempo para Olá novo serviço principal toopropagate em todo o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="d52d3-159">hello script sleeps for 15 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="d52d3-160">Se o script não Aguarde tempo suficiente, você verá um erro dizendo: "PrincipalNotFound: Principal {id} não existe no diretório hello."</span><span class="sxs-lookup"><span data-stu-id="d52d3-160">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>
* <span data-ttu-id="d52d3-161">Se você precisar de assinaturas de toomore acesso principal do serviço de saudação toogrant ou grupos de recursos, execute Olá `New-AzureRMRoleAssignment` cmdlet novamente com escopos diferentes.</span><span class="sxs-lookup"><span data-stu-id="d52d3-161">If you need toogrant hello service principal access toomore subscriptions or resource groups, run hello `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>

<span data-ttu-id="d52d3-162">Se você **não tem Windows 10 ou Windows Server 2016 Technical Preview**, você precisa Olá toodownload [gerador de certificado autoassinado](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) do Microsoft Script Center.</span><span class="sxs-lookup"><span data-stu-id="d52d3-162">If you **do not have Windows 10 or Windows Server 2016 Technical Preview**, you need toodownload hello [Self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from Microsoft Script Center.</span></span> <span data-ttu-id="d52d3-163">Extraia o conteúdo e importar Olá cmdlet que é necessário.</span><span class="sxs-lookup"><span data-stu-id="d52d3-163">Extract its contents and import hello cmdlet you need.</span></span>

```powershell  
# Only run if you could not use New-SelfSignedCertificate
Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
```
  
<span data-ttu-id="d52d3-164">No script hello, substitua Olá dois certificados de saudação do toogenerate linhas a seguir.</span><span class="sxs-lookup"><span data-stu-id="d52d3-164">In hello script, substitute hello following two lines toogenerate hello certificate.</span></span>
  
```powershell
New-SelfSignedCertificateEx  -StoreLocation CurrentUser -StoreName My -Subject "CN=exampleapp" -KeySpec "Exchange" -FriendlyName "exampleapp"
$cert = Get-ChildItem -path Cert:\CurrentUser\my | where {$PSitem.Subject -eq 'CN=exampleapp' }
```

### <a name="provide-certificate-through-automated-powershell-script"></a><span data-ttu-id="d52d3-165">Fornecer certificado por meio do script PowerShell automatizado</span><span class="sxs-lookup"><span data-stu-id="d52d3-165">Provide certificate through automated PowerShell script</span></span>
<span data-ttu-id="d52d3-166">Sempre que você entrar como uma entidade de serviço, você precisa tooprovide id de locatário de saudação do diretório de saudação para seu aplicativo do AD.</span><span class="sxs-lookup"><span data-stu-id="d52d3-166">Whenever you sign in as a service principal, you need tooprovide hello tenant id of hello directory for your AD app.</span></span> <span data-ttu-id="d52d3-167">Um locatário é uma instância do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="d52d3-167">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="d52d3-168">Se você tiver apenas uma assinatura, poderá usar:</span><span class="sxs-lookup"><span data-stu-id="d52d3-168">If you only have one subscription, you can use:</span></span>

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

<span data-ttu-id="d52d3-169">aplicativo Hello ID e a ID de locatário não diferenciam minúsculas, portanto você pode inseri-los diretamente em seu script.</span><span class="sxs-lookup"><span data-stu-id="d52d3-169">hello application ID and tenant ID are not sensitive, so you can embed them directly in your script.</span></span> <span data-ttu-id="d52d3-170">Se você precisar de ID de locatário tooretrieve Olá, use:</span><span class="sxs-lookup"><span data-stu-id="d52d3-170">If you need tooretrieve hello tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

<span data-ttu-id="d52d3-171">Se você precisar de ID do aplicativo hello tooretrieve, use:</span><span class="sxs-lookup"><span data-stu-id="d52d3-171">If you need tooretrieve hello application ID, use:</span></span>

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="create-service-principal-with-certificate-from-certificate-authority"></a><span data-ttu-id="d52d3-172">Criar a entidade de serviço com um certificado da Autoridade de Certificação</span><span class="sxs-lookup"><span data-stu-id="d52d3-172">Create service principal with certificate from Certificate Authority</span></span>
<span data-ttu-id="d52d3-173">toouse um certificado emitido por uma entidade de serviço de toocreate da autoridade de certificação, use Olá script a seguir:</span><span class="sxs-lookup"><span data-stu-id="d52d3-173">toouse a certificate issued from a Certificate Authority toocreate service principal, use hello following script:</span></span>

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

<span data-ttu-id="d52d3-174">Toonote de alguns itens sobre script hello:</span><span class="sxs-lookup"><span data-stu-id="d52d3-174">A few items toonote about hello script:</span></span>

* <span data-ttu-id="d52d3-175">O acesso é toohello no escopo de assinatura.</span><span class="sxs-lookup"><span data-stu-id="d52d3-175">Access is scoped toohello subscription.</span></span>
* <span data-ttu-id="d52d3-176">Neste exemplo, você deve adicionar função de Colaborador Olá serviço toohello principal.</span><span class="sxs-lookup"><span data-stu-id="d52d3-176">In this example, you add hello service principal toohello Contributor role.</span></span> <span data-ttu-id="d52d3-177">Para ver outras funções, confira [RBAC: funções internas](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="d52d3-177">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="d52d3-178">script Hello suspenso por 15 segundos tooallow algum tempo para Olá novo serviço principal toopropagate em todo o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="d52d3-178">hello script sleeps for 15 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="d52d3-179">Se o script não Aguarde tempo suficiente, você verá um erro dizendo: "PrincipalNotFound: Principal {id} não existe no diretório hello."</span><span class="sxs-lookup"><span data-stu-id="d52d3-179">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>
* <span data-ttu-id="d52d3-180">Se você precisar de assinaturas de toomore acesso principal do serviço de saudação toogrant ou grupos de recursos, execute Olá `New-AzureRMRoleAssignment` cmdlet novamente com escopos diferentes.</span><span class="sxs-lookup"><span data-stu-id="d52d3-180">If you need toogrant hello service principal access toomore subscriptions or resource groups, run hello `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>

### <a name="provide-certificate-through-automated-powershell-script"></a><span data-ttu-id="d52d3-181">Fornecer certificado por meio do script PowerShell automatizado</span><span class="sxs-lookup"><span data-stu-id="d52d3-181">Provide certificate through automated PowerShell script</span></span>
<span data-ttu-id="d52d3-182">Sempre que você entrar como uma entidade de serviço, você precisa tooprovide id de locatário de saudação do diretório de saudação para seu aplicativo do AD.</span><span class="sxs-lookup"><span data-stu-id="d52d3-182">Whenever you sign in as a service principal, you need tooprovide hello tenant id of hello directory for your AD app.</span></span> <span data-ttu-id="d52d3-183">Um locatário é uma instância do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="d52d3-183">A tenant is an instance of Azure Active Directory.</span></span>

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

<span data-ttu-id="d52d3-184">aplicativo Hello ID e a ID de locatário não diferenciam minúsculas, portanto você pode inseri-los diretamente em seu script.</span><span class="sxs-lookup"><span data-stu-id="d52d3-184">hello application ID and tenant ID are not sensitive, so you can embed them directly in your script.</span></span> <span data-ttu-id="d52d3-185">Se você precisar de ID de locatário tooretrieve Olá, use:</span><span class="sxs-lookup"><span data-stu-id="d52d3-185">If you need tooretrieve hello tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

<span data-ttu-id="d52d3-186">Se você precisar de ID do aplicativo hello tooretrieve, use:</span><span class="sxs-lookup"><span data-stu-id="d52d3-186">If you need tooretrieve hello application ID, use:</span></span>

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="change-credentials"></a><span data-ttu-id="d52d3-187">Alterar credenciais</span><span class="sxs-lookup"><span data-stu-id="d52d3-187">Change credentials</span></span>

<span data-ttu-id="d52d3-188">credenciais de saudação toochange para um aplicativo do AD, devido a um comprometimento de segurança ou uma expiração de credencial, usam Olá [remover AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) e [AzureRmADAppCredential novo](/powershell/module/azurerm.resources/new-azurermadappcredential) cmdlets.</span><span class="sxs-lookup"><span data-stu-id="d52d3-188">toochange hello credentials for an AD app, either because of a security compromise or a credential expiration, use hello [Remove-AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) and [New-AzureRmADAppCredential](/powershell/module/azurerm.resources/new-azurermadappcredential) cmdlets.</span></span>

<span data-ttu-id="d52d3-189">tooremove todas as credenciais de saudação para um aplicativo, use:</span><span class="sxs-lookup"><span data-stu-id="d52d3-189">tooremove all hello credentials for an application, use:</span></span>

```powershell
Remove-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -All
```

<span data-ttu-id="d52d3-190">tooadd uma senha, use:</span><span class="sxs-lookup"><span data-stu-id="d52d3-190">tooadd a password, use:</span></span>

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -Password p@ssword!
```

<span data-ttu-id="d52d3-191">tooadd um valor de certificado, crie um certificado autoassinado, conforme mostrado neste tópico.</span><span class="sxs-lookup"><span data-stu-id="d52d3-191">tooadd a certificate value, create a self-signed certificate as shown in this topic.</span></span> <span data-ttu-id="d52d3-192">Em seguida, use:</span><span class="sxs-lookup"><span data-stu-id="d52d3-192">Then, use:</span></span>

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
```

## <a name="save-access-token-toosimplify-log-in"></a><span data-ttu-id="d52d3-193">Salvar o token toosimplify login de acesso</span><span class="sxs-lookup"><span data-stu-id="d52d3-193">Save access token toosimplify log in</span></span>
<span data-ttu-id="d52d3-194">tooavoid fornecendo Olá serviço principal credenciais sempre que ele precisa toolog no, você pode salvar o token de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="d52d3-194">tooavoid providing hello service principal credentials every time it needs toolog in, you can save hello access token.</span></span>

<span data-ttu-id="d52d3-195">toouse Olá token de acesso atual em uma sessão posterior, salvar perfil hello.</span><span class="sxs-lookup"><span data-stu-id="d52d3-195">toouse hello current access token in a later session, save hello profile.</span></span>
   
```powershell
Save-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```
   
<span data-ttu-id="d52d3-196">Abra o perfil hello e examine seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="d52d3-196">Open hello profile and examine its contents.</span></span> <span data-ttu-id="d52d3-197">Observe que ele contém um token de acesso.</span><span class="sxs-lookup"><span data-stu-id="d52d3-197">Notice that it contains an access token.</span></span> <span data-ttu-id="d52d3-198">Em vez de manualmente fazer logon novamente, basta carrega o perfil de saudação.</span><span class="sxs-lookup"><span data-stu-id="d52d3-198">Instead of manually logging in again, simply load hello profile.</span></span>
   
```powershell
Select-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```

> [!NOTE]
> <span data-ttu-id="d52d3-199">o token de acesso Olá expira, portanto usar um perfil salvo só funciona para como Olá token é válido.</span><span class="sxs-lookup"><span data-stu-id="d52d3-199">hello access token expires, so using a saved profile only works for as long as hello token is valid.</span></span>
>  

<span data-ttu-id="d52d3-200">Como alternativa, você pode chamar operações REST do PowerShell toolog no.</span><span class="sxs-lookup"><span data-stu-id="d52d3-200">Alternatively, you can invoke REST operations from PowerShell toolog in.</span></span> <span data-ttu-id="d52d3-201">De resposta de autenticação hello, você pode recuperar o token de acesso de saudação para uso com outras operações.</span><span class="sxs-lookup"><span data-stu-id="d52d3-201">From hello authentication response, you can retrieve hello access token for use with other operations.</span></span> <span data-ttu-id="d52d3-202">Para obter um exemplo de recuperar o token de acesso de saudação ao chamar operações REST, consulte [gerar um Token de acesso](resource-manager-rest-api.md#generating-an-access-token).</span><span class="sxs-lookup"><span data-stu-id="d52d3-202">For an example of retrieving hello access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span></span>

## <a name="debug"></a><span data-ttu-id="d52d3-203">Depurar</span><span class="sxs-lookup"><span data-stu-id="d52d3-203">Debug</span></span>

<span data-ttu-id="d52d3-204">Você pode encontrar hello os erros a seguir ao criar uma entidade de serviço:</span><span class="sxs-lookup"><span data-stu-id="d52d3-204">You may encounter hello following errors when creating a service principal:</span></span>

* <span data-ttu-id="d52d3-205">**"Authentication_Unauthorized"** ou **"nenhuma assinatura encontrada no contexto de Olá".**</span><span class="sxs-lookup"><span data-stu-id="d52d3-205">**"Authentication_Unauthorized"** or **"No subscription found in hello context."**</span></span> <span data-ttu-id="d52d3-206">-Você vir esse erro quando sua conta não tem Olá [as permissões necessárias](#required-permissions) no Active Directory do Azure de saudação tooregister um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d52d3-206">- You see this error when your account does not have hello [required permissions](#required-permissions) on hello Azure Active Directory tooregister an app.</span></span> <span data-ttu-id="d52d3-207">Normalmente, você verá esse erro somente quando os usuários administradores no Active Directory do Azure puderem registrar aplicativos e sua conta não for um administrador. Peça ao seu administrador tooeither atribuir a função administrador tooan ou tooenable usuários tooregister aplicativos.</span><span class="sxs-lookup"><span data-stu-id="d52d3-207">Typically, you see this error when only admin users in your Azure Active Directory can register apps, and your account is not an admin. Ask your administrator tooeither assign you tooan administrator role, or tooenable users tooregister apps.</span></span>

* <span data-ttu-id="d52d3-208">Sua conta **"não tem autorização tooperform ação 'Microsoft.Authorization/roleAssignments/write' no escopo 'assinaturas / {guid}'."**  -Consulte esse erro quando sua conta não tem suficientes tooassign de permissões uma identidade de tooan de função.</span><span class="sxs-lookup"><span data-stu-id="d52d3-208">Your account **"does not have authorization tooperform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions tooassign a role tooan identity.</span></span> <span data-ttu-id="d52d3-209">Peça ao seu tooadd do administrador de assinatura função administrador do acesso tooUser.</span><span class="sxs-lookup"><span data-stu-id="d52d3-209">Ask your subscription administrator tooadd you tooUser Access Administrator role.</span></span>

## <a name="sample-applications"></a><span data-ttu-id="d52d3-210">Aplicativos de exemplo</span><span class="sxs-lookup"><span data-stu-id="d52d3-210">Sample applications</span></span>
<span data-ttu-id="d52d3-211">Para obter informações sobre como fazer logon como um aplicativo hello através de diferentes plataformas, consulte:</span><span class="sxs-lookup"><span data-stu-id="d52d3-211">For information about logging in as hello application through different platforms, see:</span></span>

* [<span data-ttu-id="d52d3-212">.NET</span><span class="sxs-lookup"><span data-stu-id="d52d3-212">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="d52d3-213">Java</span><span class="sxs-lookup"><span data-stu-id="d52d3-213">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="d52d3-214">Node.js</span><span class="sxs-lookup"><span data-stu-id="d52d3-214">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="d52d3-215">Python</span><span class="sxs-lookup"><span data-stu-id="d52d3-215">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="d52d3-216">Ruby</span><span class="sxs-lookup"><span data-stu-id="d52d3-216">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a><span data-ttu-id="d52d3-217">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d52d3-217">Next steps</span></span>
* <span data-ttu-id="d52d3-218">Para obter etapas detalhadas sobre como integrar um aplicativo do Azure para gerenciar recursos, consulte [tooauthorization de guia do desenvolvedor com hello API do Gerenciador de recursos do Azure](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d52d3-218">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide tooauthorization with hello Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="d52d3-219">Para obter uma explicação mais detalhada de aplicativos e entidades de serviço, consulte [Objetos de aplicativo e de entidade de serviço](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="d52d3-219">For a more detailed explanation of applications and service principals, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span> 
* <span data-ttu-id="d52d3-220">Para obter mais informações sobre a autenticação do Active Directory do Azure, consulte [Cenários de Autenticação do Azure AD](../active-directory/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="d52d3-220">For more information about Azure Active Directory authentication, see [Authentication Scenarios for Azure AD](../active-directory/active-directory-authentication-scenarios.md).</span></span>
* <span data-ttu-id="d52d3-221">Para obter uma lista de ações disponíveis que podem ser concedidas ou negadas toousers, consulte [operações do provedor de recursos do Gerenciador de recursos do Azure](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="d52d3-221">For a list of available actions that can be granted or denied toousers, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>

