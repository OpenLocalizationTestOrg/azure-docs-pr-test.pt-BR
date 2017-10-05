---
title: Criar identidade para o aplicativo do Azure com o PowerShell | Microsoft Docs
description: "Descreve como usar o Azure PowerShell para criar um aplicativo do Active Directory do Azure e uma entidade de serviço, e conceder acesso a recursos por meio do controle de acesso baseado em função. Ele mostra como autenticar um aplicativo com uma senha ou certificado."
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
ms.openlocfilehash: 55e83b0742652abbb42100a11a468bc13a7a8aed
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="use-azure-powershell-to-create-a-service-principal-to-access-resources"></a><span data-ttu-id="0543c-104">Usar o Azure PowerShell para criar uma entidade de serviço a fim de acessar recursos</span><span class="sxs-lookup"><span data-stu-id="0543c-104">Use Azure PowerShell to create a service principal to access resources</span></span>

<span data-ttu-id="0543c-105">Quando você tiver um aplicativo ou script que precisa acessar recursos, poderá configurar uma identidade para o aplicativo e autenticá-lo com suas próprias credenciais.</span><span class="sxs-lookup"><span data-stu-id="0543c-105">When you have an app or script that needs to access resources, you can set up an identity for the app and authenticate the app with its own credentials.</span></span> <span data-ttu-id="0543c-106">Essa identidade é conhecida como uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="0543c-106">This identity is known as a service principal.</span></span> <span data-ttu-id="0543c-107">Essa abordagem permite:</span><span class="sxs-lookup"><span data-stu-id="0543c-107">This approach enables you to:</span></span>

* <span data-ttu-id="0543c-108">Atribuir permissões à identidade do aplicativo que são diferentes de suas próprias permissões.</span><span class="sxs-lookup"><span data-stu-id="0543c-108">Assign permissions to the app identity that are different than your own permissions.</span></span> <span data-ttu-id="0543c-109">Normalmente, essas permissões são restritas a exatamente o que o aplicativo precisa fazer.</span><span class="sxs-lookup"><span data-stu-id="0543c-109">Typically, these permissions are restricted to exactly what the app needs to do.</span></span>
* <span data-ttu-id="0543c-110">Use um certificado para a autenticação ao executar um script autônomo.</span><span class="sxs-lookup"><span data-stu-id="0543c-110">Use a certificate for authentication when executing an unattended script.</span></span>

<span data-ttu-id="0543c-111">Este tópico mostra como usar o [Azure PowerShell](/powershell/azure/overview) para configurar tudo que você precisa para um aplicativo ser executado com suas próprias credenciais e identidade.</span><span class="sxs-lookup"><span data-stu-id="0543c-111">This topic shows you how to use [Azure PowerShell](/powershell/azure/overview) to set up everything you need for an application to run under its own credentials and identity.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="0543c-112">Permissões necessárias</span><span class="sxs-lookup"><span data-stu-id="0543c-112">Required permissions</span></span>
<span data-ttu-id="0543c-113">Para concluir este tópico, você deve ter permissões suficientes no Azure Active Directory e em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="0543c-113">To complete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span></span> <span data-ttu-id="0543c-114">Especificamente, você deve ser capaz de criar um aplicativo no Active Directory do Azure e atribuir a entidade de serviço a uma função.</span><span class="sxs-lookup"><span data-stu-id="0543c-114">Specifically, you must be able to create an app in the Azure Active Directory, and assign the service principal to a role.</span></span> 

<span data-ttu-id="0543c-115">A maneira mais fácil de verificar se a sua conta tem as permissões adequadas é por meio do portal.</span><span class="sxs-lookup"><span data-stu-id="0543c-115">The easiest way to check whether your account has adequate permissions is through the portal.</span></span> <span data-ttu-id="0543c-116">Consulte [Verificar permissão necessária](resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="0543c-116">See [Check required permission](resource-group-create-service-principal-portal.md#required-permissions).</span></span>

<span data-ttu-id="0543c-117">Agora, vá para uma seção para se autenticar com:</span><span class="sxs-lookup"><span data-stu-id="0543c-117">Now, proceed to a section for authenticating with:</span></span>

* [<span data-ttu-id="0543c-118">password</span><span class="sxs-lookup"><span data-stu-id="0543c-118">password</span></span>](#create-service-principal-with-password)
* [<span data-ttu-id="0543c-119">certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="0543c-119">self-signed certificate</span></span>](#create-service-principal-with-self-signed-certificate)
* [<span data-ttu-id="0543c-120">certificado da Autoridade de Certificação</span><span class="sxs-lookup"><span data-stu-id="0543c-120">certificate from Certificate Authority</span></span>](#create-service-principal-with-certificate-from-certificate-authority)

## <a name="powershell-commands"></a><span data-ttu-id="0543c-121">Comandos do PowerShell</span><span class="sxs-lookup"><span data-stu-id="0543c-121">PowerShell commands</span></span>

<span data-ttu-id="0543c-122">Para configurar uma entidade de serviço, use:</span><span class="sxs-lookup"><span data-stu-id="0543c-122">To set up a service principal, you use:</span></span>

| <span data-ttu-id="0543c-123">Command</span><span class="sxs-lookup"><span data-stu-id="0543c-123">Command</span></span> | <span data-ttu-id="0543c-124">Descrição</span><span class="sxs-lookup"><span data-stu-id="0543c-124">Description</span></span> |
| ------- | ----------- | 
| [<span data-ttu-id="0543c-125">New-AzureRmADServicePrincipal</span><span class="sxs-lookup"><span data-stu-id="0543c-125">New-AzureRmADServicePrincipal</span></span>](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | <span data-ttu-id="0543c-126">Cria uma entidade de serviço do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0543c-126">Creates an Azure Active Directory service principal</span></span> |
| [<span data-ttu-id="0543c-127">New-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="0543c-127">New-AzureRmRoleAssignment</span></span>](/powershell/module/azurerm.resources/new-azurermroleassignment) | <span data-ttu-id="0543c-128">Atribui a função RBAC especificada à entidade se segurança especificada no escopo especificado.</span><span class="sxs-lookup"><span data-stu-id="0543c-128">Assigns the specified RBAC role to the specified principal, at the specified scope.</span></span> |


## <a name="create-service-principal-with-password"></a><span data-ttu-id="0543c-129">Criar a entidade de serviço com a senha</span><span class="sxs-lookup"><span data-stu-id="0543c-129">Create service principal with password</span></span>

<span data-ttu-id="0543c-130">Para criar uma entidade de serviço com a função de Colaborador para sua assinatura, use:</span><span class="sxs-lookup"><span data-stu-id="0543c-130">To create a service principal with the Contributor role for your subscription, use:</span></span> 

```powershell
Login-AzureRmAccount
$sp = New-AzureRmADServicePrincipal -DisplayName exampleapp -Password "{provide-password}"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="0543c-131">O exemplo fica suspenso por 20 segundos para dar tempo para a nova entidade de serviço propagar-se pelo Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0543c-131">The example sleeps for 20 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="0543c-132">Se o script não esperar tempo suficiente, você verá um erro dizendo: "PrincipalNotFound: a {id} da entidade não existe no diretório”.</span><span class="sxs-lookup"><span data-stu-id="0543c-132">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span></span>

<span data-ttu-id="0543c-133">O script a seguir permite que você especifique um escopo diferente da assinatura padrão e tenta realizar a atribuição de função novamente no caso de erro:</span><span class="sxs-lookup"><span data-stu-id="0543c-133">The following script enables you to specify a scope other than the default subscription, and retries the role assignment if an error occurs:</span></span>

```powershell
Param (

 # Use to set scope to resource group. If no value is provided, scope is set to subscription.
 [Parameter(Mandatory=$false)]
 [String] $ResourceGroup,

 # Use to set subscription. If no value is provided, default subscription is used. 
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

 
 # Create Service Principal for the AD app
 $ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -Password $Password
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds to allow the service principal application to become active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
```

<span data-ttu-id="0543c-134">Alguns itens a serem observados sobre o script:</span><span class="sxs-lookup"><span data-stu-id="0543c-134">A few items to note about the script:</span></span>

* <span data-ttu-id="0543c-135">Para conceder o acesso da identidade à assinatura padrão, não é necessário fornecer os parâmetros ResourceGroup ou SubscriptionId.</span><span class="sxs-lookup"><span data-stu-id="0543c-135">To grant the identity access to the default subscription, you do not need to provide either ResourceGroup or SubscriptionId parameters.</span></span>
* <span data-ttu-id="0543c-136">Especifique o parâmetro ResourceGroup somente quando desejar limitar o escopo da atribuição de função a um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0543c-136">Specify the ResourceGroup parameter only when you want to limit the scope of the role assignment to a resource group.</span></span>
*  <span data-ttu-id="0543c-137">Neste exemplo, você adiciona a entidade de serviço à função Colaborador.</span><span class="sxs-lookup"><span data-stu-id="0543c-137">In this example, you add the service principal to the Contributor role.</span></span> <span data-ttu-id="0543c-138">Para ver outras funções, confira [RBAC: funções internas](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="0543c-138">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="0543c-139">O script fica suspenso 15 segundos para dar tempo à nova entidade de serviço de se propagar pelo Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="0543c-139">The script sleeps for 15 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="0543c-140">Se o script não esperar tempo suficiente, você verá um erro dizendo: "PrincipalNotFound: a {id} da entidade não existe no diretório”.</span><span class="sxs-lookup"><span data-stu-id="0543c-140">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span></span>
* <span data-ttu-id="0543c-141">Se precisar conceder o acesso à entidade de serviço a mais assinaturas ou grupos de recursos, execute o cmdlet `New-AzureRMRoleAssignment` novamente com escopos diferentes.</span><span class="sxs-lookup"><span data-stu-id="0543c-141">If you need to grant the service principal access to more subscriptions or resource groups, run the `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>


### <a name="provide-credentials-through-powershell"></a><span data-ttu-id="0543c-142">Fornecer as credenciais por meio do PowerShell</span><span class="sxs-lookup"><span data-stu-id="0543c-142">Provide credentials through PowerShell</span></span>
<span data-ttu-id="0543c-143">Agora, você precisa fazer logon como o aplicativo para executar as operações.</span><span class="sxs-lookup"><span data-stu-id="0543c-143">Now, you need to log in as the application to perform operations.</span></span> <span data-ttu-id="0543c-144">Para o nome de usuário, use a `ApplicationId` que você criou para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0543c-144">For the user name, use the `ApplicationId` that you created for the application.</span></span> <span data-ttu-id="0543c-145">Como senha, use aquela especificada ao criar a conta.</span><span class="sxs-lookup"><span data-stu-id="0543c-145">For the password, use the one you specified when creating the account.</span></span> 

```powershell   
$creds = Get-Credential
Login-AzureRmAccount -Credential $creds -ServicePrincipal -TenantId {tenant-id}
```

<span data-ttu-id="0543c-146">A ID de locatário não diferencia maiúsculas de minúsculas e, portanto, você pode inseri-la diretamente no script.</span><span class="sxs-lookup"><span data-stu-id="0543c-146">The tenant ID is not sensitive, so you can embed it directly in your script.</span></span> <span data-ttu-id="0543c-147">Se precisar recuperar a ID de locatário, use:</span><span class="sxs-lookup"><span data-stu-id="0543c-147">If you need to retrieve the tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

## <a name="create-service-principal-with-self-signed-certificate"></a><span data-ttu-id="0543c-148">Criar a entidade de serviço com um certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="0543c-148">Create service principal with self-signed certificate</span></span>

<span data-ttu-id="0543c-149">Para criar uma entidade de serviço com um certificado autoassinado e a função de Colaborador para sua assinatura, use:</span><span class="sxs-lookup"><span data-stu-id="0543c-149">To create a service principal with a self-signed certificate and the Contributor role for your subscription, use:</span></span> 

```powershell
Login-AzureRmAccount
$cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
$keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

$sp = New-AzureRMADServicePrincipal -DisplayName exampleapp -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="0543c-150">O exemplo fica suspenso por 20 segundos para dar tempo para a nova entidade de serviço propagar-se pelo Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0543c-150">The example sleeps for 20 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="0543c-151">Se o script não esperar tempo suficiente, você verá um erro dizendo: "PrincipalNotFound: a {id} da entidade não existe no diretório”.</span><span class="sxs-lookup"><span data-stu-id="0543c-151">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span></span>

<span data-ttu-id="0543c-152">O script a seguir permite que você especifique um escopo diferente da assinatura padrão e tenta realizar a atribuição de função novamente no caso de erro.</span><span class="sxs-lookup"><span data-stu-id="0543c-152">The following script enables you to specify a scope other than the default subscription, and retries the role assignment if an error occurs.</span></span> <span data-ttu-id="0543c-153">Você deve ter o Azure PowerShell 2.0 no Windows 10 ou Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="0543c-153">You must have Azure PowerShell 2.0 on Windows 10 or Windows Server 2016.</span></span>

```powershell
Param (

 # Use to set scope to resource group. If no value is provided, scope is set to subscription.
 [Parameter(Mandatory=$false)]
 [String] $ResourceGroup,

 # Use to set subscription. If no value is provided, default subscription is used. 
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
    # Sleep here for a few seconds to allow the service principal application to become active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
```

<span data-ttu-id="0543c-154">Alguns itens a serem observados sobre o script:</span><span class="sxs-lookup"><span data-stu-id="0543c-154">A few items to note about the script:</span></span>

* <span data-ttu-id="0543c-155">Para conceder o acesso da identidade à assinatura padrão, não é necessário fornecer os parâmetros ResourceGroup ou SubscriptionId.</span><span class="sxs-lookup"><span data-stu-id="0543c-155">To grant the identity access to the default subscription, you do not need to provide either ResourceGroup or SubscriptionId parameters.</span></span>
* <span data-ttu-id="0543c-156">Especifique o parâmetro ResourceGroup somente quando desejar limitar o escopo da atribuição de função a um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0543c-156">Specify the ResourceGroup parameter only when you want to limit the scope of the role assignment to a resource group.</span></span>
* <span data-ttu-id="0543c-157">Neste exemplo, você adiciona a entidade de serviço à função Colaborador.</span><span class="sxs-lookup"><span data-stu-id="0543c-157">In this example, you add the service principal to the Contributor role.</span></span> <span data-ttu-id="0543c-158">Para ver outras funções, confira [RBAC: funções internas](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="0543c-158">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="0543c-159">O script fica suspenso 15 segundos para dar tempo à nova entidade de serviço de se propagar pelo Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="0543c-159">The script sleeps for 15 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="0543c-160">Se o script não esperar tempo suficiente, você verá um erro dizendo: "PrincipalNotFound: a {id} da entidade não existe no diretório”.</span><span class="sxs-lookup"><span data-stu-id="0543c-160">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span></span>
* <span data-ttu-id="0543c-161">Se precisar conceder o acesso à entidade de serviço a mais assinaturas ou grupos de recursos, execute o cmdlet `New-AzureRMRoleAssignment` novamente com escopos diferentes.</span><span class="sxs-lookup"><span data-stu-id="0543c-161">If you need to grant the service principal access to more subscriptions or resource groups, run the `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>

<span data-ttu-id="0543c-162">Se você **não tiver o Windows 10 ou o Windows Server 2016 Technical Preview**, precisará baixar o [Gerador de certificado autoassinado](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) no Script Center da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0543c-162">If you **do not have Windows 10 or Windows Server 2016 Technical Preview**, you need to download the [Self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from Microsoft Script Center.</span></span> <span data-ttu-id="0543c-163">Extraia seu conteúdo e importe o cmdlet necessário.</span><span class="sxs-lookup"><span data-stu-id="0543c-163">Extract its contents and import the cmdlet you need.</span></span>

```powershell  
# Only run if you could not use New-SelfSignedCertificate
Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
```
  
<span data-ttu-id="0543c-164">No script, substitua as duas linhas a seguir para gerar o certificado.</span><span class="sxs-lookup"><span data-stu-id="0543c-164">In the script, substitute the following two lines to generate the certificate.</span></span>
  
```powershell
New-SelfSignedCertificateEx  -StoreLocation CurrentUser -StoreName My -Subject "CN=exampleapp" -KeySpec "Exchange" -FriendlyName "exampleapp"
$cert = Get-ChildItem -path Cert:\CurrentUser\my | where {$PSitem.Subject -eq 'CN=exampleapp' }
```

### <a name="provide-certificate-through-automated-powershell-script"></a><span data-ttu-id="0543c-165">Fornecer certificado por meio do script PowerShell automatizado</span><span class="sxs-lookup"><span data-stu-id="0543c-165">Provide certificate through automated PowerShell script</span></span>
<span data-ttu-id="0543c-166">Sempre que você entrar como uma entidade de serviço, precisará fornecer a ID do locatário do diretório para seu aplicativo do AD.</span><span class="sxs-lookup"><span data-stu-id="0543c-166">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span></span> <span data-ttu-id="0543c-167">Um locatário é uma instância do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="0543c-167">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="0543c-168">Se você tiver apenas uma assinatura, poderá usar:</span><span class="sxs-lookup"><span data-stu-id="0543c-168">If you only have one subscription, you can use:</span></span>

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

<span data-ttu-id="0543c-169">A ID do aplicativo e a ID de locatário não diferenciam maiúsculas de minúsculas e, portanto, você pode inseri-las diretamente no script.</span><span class="sxs-lookup"><span data-stu-id="0543c-169">The application ID and tenant ID are not sensitive, so you can embed them directly in your script.</span></span> <span data-ttu-id="0543c-170">Se precisar recuperar a ID de locatário, use:</span><span class="sxs-lookup"><span data-stu-id="0543c-170">If you need to retrieve the tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

<span data-ttu-id="0543c-171">Se precisar recuperar a ID do aplicativo, use:</span><span class="sxs-lookup"><span data-stu-id="0543c-171">If you need to retrieve the application ID, use:</span></span>

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="create-service-principal-with-certificate-from-certificate-authority"></a><span data-ttu-id="0543c-172">Criar a entidade de serviço com um certificado da Autoridade de Certificação</span><span class="sxs-lookup"><span data-stu-id="0543c-172">Create service principal with certificate from Certificate Authority</span></span>
<span data-ttu-id="0543c-173">Para usar um certificado emitido por uma Autoridade de Certificação para criar a entidade de serviço, use o seguinte script:</span><span class="sxs-lookup"><span data-stu-id="0543c-173">To use a certificate issued from a Certificate Authority to create service principal, use the following script:</span></span>

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
    # Sleep here for a few seconds to allow the service principal application to become active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
 
 $NewRole
```

<span data-ttu-id="0543c-174">Alguns itens a serem observados sobre o script:</span><span class="sxs-lookup"><span data-stu-id="0543c-174">A few items to note about the script:</span></span>

* <span data-ttu-id="0543c-175">O acesso é restrito à assinatura.</span><span class="sxs-lookup"><span data-stu-id="0543c-175">Access is scoped to the subscription.</span></span>
* <span data-ttu-id="0543c-176">Neste exemplo, você adiciona a entidade de serviço à função Colaborador.</span><span class="sxs-lookup"><span data-stu-id="0543c-176">In this example, you add the service principal to the Contributor role.</span></span> <span data-ttu-id="0543c-177">Para ver outras funções, confira [RBAC: funções internas](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="0543c-177">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="0543c-178">O script fica suspenso 15 segundos para dar tempo à nova entidade de serviço de se propagar pelo Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="0543c-178">The script sleeps for 15 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="0543c-179">Se o script não esperar tempo suficiente, você verá um erro dizendo: "PrincipalNotFound: a {id} da entidade não existe no diretório”.</span><span class="sxs-lookup"><span data-stu-id="0543c-179">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span></span>
* <span data-ttu-id="0543c-180">Se precisar conceder o acesso à entidade de serviço a mais assinaturas ou grupos de recursos, execute o cmdlet `New-AzureRMRoleAssignment` novamente com escopos diferentes.</span><span class="sxs-lookup"><span data-stu-id="0543c-180">If you need to grant the service principal access to more subscriptions or resource groups, run the `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>

### <a name="provide-certificate-through-automated-powershell-script"></a><span data-ttu-id="0543c-181">Fornecer certificado por meio do script PowerShell automatizado</span><span class="sxs-lookup"><span data-stu-id="0543c-181">Provide certificate through automated PowerShell script</span></span>
<span data-ttu-id="0543c-182">Sempre que você entrar como uma entidade de serviço, precisará fornecer a ID do locatário do diretório para seu aplicativo do AD.</span><span class="sxs-lookup"><span data-stu-id="0543c-182">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span></span> <span data-ttu-id="0543c-183">Um locatário é uma instância do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="0543c-183">A tenant is an instance of Azure Active Directory.</span></span>

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

<span data-ttu-id="0543c-184">A ID do aplicativo e a ID de locatário não diferenciam maiúsculas de minúsculas e, portanto, você pode inseri-las diretamente no script.</span><span class="sxs-lookup"><span data-stu-id="0543c-184">The application ID and tenant ID are not sensitive, so you can embed them directly in your script.</span></span> <span data-ttu-id="0543c-185">Se precisar recuperar a ID de locatário, use:</span><span class="sxs-lookup"><span data-stu-id="0543c-185">If you need to retrieve the tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

<span data-ttu-id="0543c-186">Se precisar recuperar a ID do aplicativo, use:</span><span class="sxs-lookup"><span data-stu-id="0543c-186">If you need to retrieve the application ID, use:</span></span>

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="change-credentials"></a><span data-ttu-id="0543c-187">Alterar credenciais</span><span class="sxs-lookup"><span data-stu-id="0543c-187">Change credentials</span></span>

<span data-ttu-id="0543c-188">Para alterar as credenciais para um aplicativo do AD, por causa de uma violação de segurança ou expiração de credencial, use os cmdlets [Remove-AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) e [New-AzureRmADAppCredential](/powershell/module/azurerm.resources/new-azurermadappcredential).</span><span class="sxs-lookup"><span data-stu-id="0543c-188">To change the credentials for an AD app, either because of a security compromise or a credential expiration, use the [Remove-AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) and [New-AzureRmADAppCredential](/powershell/module/azurerm.resources/new-azurermadappcredential) cmdlets.</span></span>

<span data-ttu-id="0543c-189">Para remover todas as credenciais de um aplicativo, use:</span><span class="sxs-lookup"><span data-stu-id="0543c-189">To remove all the credentials for an application, use:</span></span>

```powershell
Remove-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -All
```

<span data-ttu-id="0543c-190">Para adicionar uma senha, use:</span><span class="sxs-lookup"><span data-stu-id="0543c-190">To add a password, use:</span></span>

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -Password p@ssword!
```

<span data-ttu-id="0543c-191">Para adicionar um valor de certificado, crie um certificado autoassinado conforme mostrado neste tópico.</span><span class="sxs-lookup"><span data-stu-id="0543c-191">To add a certificate value, create a self-signed certificate as shown in this topic.</span></span> <span data-ttu-id="0543c-192">Em seguida, use:</span><span class="sxs-lookup"><span data-stu-id="0543c-192">Then, use:</span></span>

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
```

## <a name="save-access-token-to-simplify-log-in"></a><span data-ttu-id="0543c-193">Salvar o token de acesso para simplificar o logon</span><span class="sxs-lookup"><span data-stu-id="0543c-193">Save access token to simplify log in</span></span>
<span data-ttu-id="0543c-194">Para evitar fornecer as credenciais de serviço principal toda vez que precisar fazer logon, você poderá salvar o token de acesso.</span><span class="sxs-lookup"><span data-stu-id="0543c-194">To avoid providing the service principal credentials every time it needs to log in, you can save the access token.</span></span>

<span data-ttu-id="0543c-195">Para usar o token de acesso atual em uma sessão posterior, salve o perfil.</span><span class="sxs-lookup"><span data-stu-id="0543c-195">To use the current access token in a later session, save the profile.</span></span>
   
```powershell
Save-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```
   
<span data-ttu-id="0543c-196">Abra o perfil e examine seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="0543c-196">Open the profile and examine its contents.</span></span> <span data-ttu-id="0543c-197">Observe que ele contém um token de acesso.</span><span class="sxs-lookup"><span data-stu-id="0543c-197">Notice that it contains an access token.</span></span> <span data-ttu-id="0543c-198">Em vez fazer o logon manualmente de novo, basta carregar o perfil.</span><span class="sxs-lookup"><span data-stu-id="0543c-198">Instead of manually logging in again, simply load the profile.</span></span>
   
```powershell
Select-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```

> [!NOTE]
> <span data-ttu-id="0543c-199">O token de acesso expira, portanto, usar um perfil salvo funcionará somente se o token for válido.</span><span class="sxs-lookup"><span data-stu-id="0543c-199">The access token expires, so using a saved profile only works for as long as the token is valid.</span></span>
>  

<span data-ttu-id="0543c-200">Como alternativa, você pode invocar operações REST do PowerShell para fazer logon.</span><span class="sxs-lookup"><span data-stu-id="0543c-200">Alternatively, you can invoke REST operations from PowerShell to log in.</span></span> <span data-ttu-id="0543c-201">Na resposta de autenticação, você pode recuperar o token de acesso para uso com outras operações.</span><span class="sxs-lookup"><span data-stu-id="0543c-201">From the authentication response, you can retrieve the access token for use with other operations.</span></span> <span data-ttu-id="0543c-202">Para obter um exemplo de como recuperar o token de acesso invocando operações REST, consulte [Gerar um token de acesso](resource-manager-rest-api.md#generating-an-access-token).</span><span class="sxs-lookup"><span data-stu-id="0543c-202">For an example of retrieving the access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span></span>

## <a name="debug"></a><span data-ttu-id="0543c-203">Depurar</span><span class="sxs-lookup"><span data-stu-id="0543c-203">Debug</span></span>

<span data-ttu-id="0543c-204">Você pode receber os seguintes erros ao criar uma entidade de serviço:</span><span class="sxs-lookup"><span data-stu-id="0543c-204">You may encounter the following errors when creating a service principal:</span></span>

* <span data-ttu-id="0543c-205">**"Authentication_Unauthorized"** ou **"Nenhuma assinatura encontrada no contexto".**</span><span class="sxs-lookup"><span data-stu-id="0543c-205">**"Authentication_Unauthorized"** or **"No subscription found in the context."**</span></span> <span data-ttu-id="0543c-206">– Você verá esse erro quando sua conta não tiver as [permissões necessárias](#required-permissions) no Active Directory do Azure para registrar um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0543c-206">- You see this error when your account does not have the [required permissions](#required-permissions) on the Azure Active Directory to register an app.</span></span> <span data-ttu-id="0543c-207">Normalmente, você verá esse erro somente quando os usuários administradores no Active Directory do Azure puderem registrar aplicativos e sua conta não for um administrador.</span><span class="sxs-lookup"><span data-stu-id="0543c-207">Typically, you see this error when only admin users in your Azure Active Directory can register apps, and your account is not an admin.</span></span> <span data-ttu-id="0543c-208">Solicite ao administrador para lhe atribuir uma função de administrador ou para permitir que os usuários registrem aplicativos.</span><span class="sxs-lookup"><span data-stu-id="0543c-208">Ask your administrator to either assign you to an administrator role, or to enable users to register apps.</span></span>

* <span data-ttu-id="0543c-209">Sua conta **"não tem autorização para executar a ação 'Microsoft.Authorization/roleAssignments/write' no escopo '/subscriptions/{guid}'".**  – Você verá esse erro quando sua conta não tiver permissões suficientes para atribuir uma função a uma identidade.</span><span class="sxs-lookup"><span data-stu-id="0543c-209">Your account **"does not have authorization to perform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions to assign a role to an identity.</span></span> <span data-ttu-id="0543c-210">Solicite ao administrador da assinatura para adicioná-lo à função Administrador de Acesso do Usuário.</span><span class="sxs-lookup"><span data-stu-id="0543c-210">Ask your subscription administrator to add you to User Access Administrator role.</span></span>

## <a name="sample-applications"></a><span data-ttu-id="0543c-211">Aplicativos de exemplo</span><span class="sxs-lookup"><span data-stu-id="0543c-211">Sample applications</span></span>
<span data-ttu-id="0543c-212">Para obter informações sobre como fazer logon no aplicativo por meio de diferentes plataformas, consulte:</span><span class="sxs-lookup"><span data-stu-id="0543c-212">For information about logging in as the application through different platforms, see:</span></span>

* [<span data-ttu-id="0543c-213">.NET</span><span class="sxs-lookup"><span data-stu-id="0543c-213">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="0543c-214">Java</span><span class="sxs-lookup"><span data-stu-id="0543c-214">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="0543c-215">Node.js</span><span class="sxs-lookup"><span data-stu-id="0543c-215">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="0543c-216">Python</span><span class="sxs-lookup"><span data-stu-id="0543c-216">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="0543c-217">Ruby</span><span class="sxs-lookup"><span data-stu-id="0543c-217">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a><span data-ttu-id="0543c-218">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0543c-218">Next steps</span></span>
* <span data-ttu-id="0543c-219">Para ver as etapas detalhadas sobre como integrar um aplicativo no Azure para gerenciar os recursos, consulte [Guia do desenvolvedor para a autorização com a API do Azure Resource Manager](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="0543c-219">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide to authorization with the Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="0543c-220">Para obter uma explicação mais detalhada de aplicativos e entidades de serviço, consulte [Objetos de aplicativo e de entidade de serviço](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="0543c-220">For a more detailed explanation of applications and service principals, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span> 
* <span data-ttu-id="0543c-221">Para obter mais informações sobre a autenticação do Active Directory do Azure, consulte [Cenários de Autenticação do Azure AD](../active-directory/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="0543c-221">For more information about Azure Active Directory authentication, see [Authentication Scenarios for Azure AD](../active-directory/active-directory-authentication-scenarios.md).</span></span>
* <span data-ttu-id="0543c-222">Para obter uma lista de ações disponíveis que podem ser concedidas ou negadas a usuários, consulte [Operações do Provedor de Recursos do Azure Resource Manager](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="0543c-222">For a list of available actions that can be granted or denied to users, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>

