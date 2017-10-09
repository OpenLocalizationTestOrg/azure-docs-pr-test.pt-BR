---
title: aaaEncrypt discos em uma VM do Windows Azure | Microsoft Docs
description: "Como o tooencrypt de discos virtuais em uma VM do Windows para melhor segurança usando o PowerShell do Azure"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/10/2017
ms.author: iainfou
ms.openlocfilehash: 77c42a67cb57a9dc5fe3159fce0be75e3a965be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencrypt-virtual-disks-on-a-windows-vm"></a><span data-ttu-id="0a93d-103">Como tooencrypt de discos virtuais em uma VM do Windows</span><span class="sxs-lookup"><span data-stu-id="0a93d-103">How tooencrypt virtual disks on a Windows VM</span></span>
<span data-ttu-id="0a93d-104">Para conformidade e segurança aprimorados da VM (máquina virtual), os discos virtuais no Azure podem ser criptografados.</span><span class="sxs-lookup"><span data-stu-id="0a93d-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted.</span></span> <span data-ttu-id="0a93d-105">Discos são criptografados usando chaves criptográficas que são protegidas em um Cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="0a93d-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="0a93d-106">Você controla essas chaves criptográficas e pode auditar seu uso.</span><span class="sxs-lookup"><span data-stu-id="0a93d-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="0a93d-107">Este artigo detalhes como tooencrypt de discos virtuais em uma VM do Windows usando o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="0a93d-107">This article details how tooencrypt virtual disks on a Windows VM using Azure PowerShell.</span></span> <span data-ttu-id="0a93d-108">Você também pode [criptografar uma VM do Linux usando hello Azure CLI 2.0](../linux/encrypt-disks.md).</span><span class="sxs-lookup"><span data-stu-id="0a93d-108">You can also [encrypt a Linux VM using hello Azure CLI 2.0](../linux/encrypt-disks.md).</span></span>

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="0a93d-109">Visão geral da criptografia de disco</span><span class="sxs-lookup"><span data-stu-id="0a93d-109">Overview of disk encryption</span></span>
<span data-ttu-id="0a93d-110">Discos virtuais em VMs do Windows são criptografados em repouso usando o Bitlocker.</span><span class="sxs-lookup"><span data-stu-id="0a93d-110">Virtual disks on Windows VMs are encrypted at rest using Bitlocker.</span></span> <span data-ttu-id="0a93d-111">Não há nenhuma taxa para criptografar discos virtuais no Azure.</span><span class="sxs-lookup"><span data-stu-id="0a93d-111">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="0a93d-112">As chaves de criptografia são armazenadas no cofre de chaves do Azure usando a proteção de software, ou você pode importar ou gerar as chaves em módulos de segurança de Hardware (HSM) certificada tooFIPS padrões do 140-2 nível 2.</span><span class="sxs-lookup"><span data-stu-id="0a93d-112">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified tooFIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="0a93d-113">Essas chaves de criptografia são usada tooencrypt e descriptografar os discos virtuais anexados tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="0a93d-113">These cryptographic keys are used tooencrypt and decrypt virtual disks attached tooyour VM.</span></span> <span data-ttu-id="0a93d-114">Você mantém o controle dessas chaves criptográficas e pode auditar seu uso.</span><span class="sxs-lookup"><span data-stu-id="0a93d-114">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="0a93d-115">Uma entidade de serviço do Azure Active Directory fornece um mecanismo seguro para emitir essas chaves de criptografia, enquanto as VMs são ligadas e desligadas.</span><span class="sxs-lookup"><span data-stu-id="0a93d-115">An Azure Active Directory service principal provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="0a93d-116">processo de saudação de criptografia de uma VM é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="0a93d-116">hello process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="0a93d-117">Crie uma chave de criptografia em um Cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="0a93d-117">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="0a93d-118">Configure Olá criptográfico chave toobe pode ser usado para criptografia de discos.</span><span class="sxs-lookup"><span data-stu-id="0a93d-118">Configure hello cryptographic key toobe usable for encrypting disks.</span></span>
3. <span data-ttu-id="0a93d-119">chave de criptografia de saudação tooread de saudação Cofre de chaves do Azure, criar um serviço do Active Directory do Azure principal com as permissões adequadas hello.</span><span class="sxs-lookup"><span data-stu-id="0a93d-119">tooread hello cryptographic key from hello Azure Key Vault, create an Azure Active Directory service principal with hello appropriate permissions.</span></span>
4. <span data-ttu-id="0a93d-120">Emita Olá comando tooencrypt seus discos virtuais, especificação de entidade de serviço do Active Directory do Azure hello e adequado toobe chave criptográfica usada.</span><span class="sxs-lookup"><span data-stu-id="0a93d-120">Issue hello command tooencrypt your virtual disks, specifying hello Azure Active Directory service principal and appropriate cryptographic key toobe used.</span></span>
5. <span data-ttu-id="0a93d-121">solicitações do principais de serviço do Active Directory do Azure Olá Olá chave de criptografia necessária do Cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="0a93d-121">hello Azure Active Directory service principal requests hello required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="0a93d-122">discos virtuais Olá são criptografados usando a chave criptográfica Olá fornecido.</span><span class="sxs-lookup"><span data-stu-id="0a93d-122">hello virtual disks are encrypted using hello provided cryptographic key.</span></span>

## <a name="encryption-process"></a><span data-ttu-id="0a93d-123">Processo de criptografia</span><span class="sxs-lookup"><span data-stu-id="0a93d-123">Encryption process</span></span>
<span data-ttu-id="0a93d-124">Criptografia de disco se baseia em Olá componentes adicionais a seguir:</span><span class="sxs-lookup"><span data-stu-id="0a93d-124">Disk encryption relies on hello following additional components:</span></span>

* <span data-ttu-id="0a93d-125">**Cofre de chaves do Azure** -usado toosafeguard as chaves de criptografia e segredos usados no processo de criptografia/descriptografia de disco hello.</span><span class="sxs-lookup"><span data-stu-id="0a93d-125">**Azure Key Vault** - used toosafeguard cryptographic keys and secrets used for hello disk encryption/decryption process.</span></span> 
  * <span data-ttu-id="0a93d-126">Se houver um, você pode usar um Cofre de Chaves do Azure existente.</span><span class="sxs-lookup"><span data-stu-id="0a93d-126">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="0a93d-127">Você não tem toodedicate discos tooencrypting um cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="0a93d-127">You do not have toodedicate a Key Vault tooencrypting disks.</span></span>
  * <span data-ttu-id="0a93d-128">limites administrativos tooseparate e visibilidade de chave, você pode criar um cofre de chaves dedicado.</span><span class="sxs-lookup"><span data-stu-id="0a93d-128">tooseparate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="0a93d-129">**Active Directory do Azure** - identificadores Olá troca segura de chaves de criptografia necessárias e autenticação para ações de solicitada.</span><span class="sxs-lookup"><span data-stu-id="0a93d-129">**Azure Active Directory** - handles hello secure exchanging of required cryptographic keys and authentication for requested actions.</span></span> 
  * <span data-ttu-id="0a93d-130">Normalmente, você pode usar uma instância existente do Azure Active Directory para hospedar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0a93d-130">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="0a93d-131">entidade de serviço Olá fornece um mecanismo seguro toorequest e emitido chaves de criptografia apropriadas hello.</span><span class="sxs-lookup"><span data-stu-id="0a93d-131">hello service principal provides a secure mechanism toorequest and be issued hello appropriate cryptographic keys.</span></span> <span data-ttu-id="0a93d-132">Você não está desenvolvendo um aplicativo real que se integra ao Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0a93d-132">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="0a93d-133">Requisitos e limitações</span><span class="sxs-lookup"><span data-stu-id="0a93d-133">Requirements and limitations</span></span>
<span data-ttu-id="0a93d-134">Requisitos e cenários com suporte para criptografia de disco:</span><span class="sxs-lookup"><span data-stu-id="0a93d-134">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="0a93d-135">Habilitar a criptografia em novas VMs do Windows a partir de imagens do Azure Marketplace ou de uma imagem VHD personalizada.</span><span class="sxs-lookup"><span data-stu-id="0a93d-135">Enabling encryption on new Windows VMs from Azure Marketplace images or custom VHD image.</span></span>
* <span data-ttu-id="0a93d-136">Habilitar a criptografia em VMs existentes do Windows no Azure.</span><span class="sxs-lookup"><span data-stu-id="0a93d-136">Enabling encryption on existing Windows VMs in Azure.</span></span>
* <span data-ttu-id="0a93d-137">Habilitar a criptografia em VMs do Windows que são configuradas usando Espaços de Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="0a93d-137">Enabling encryption on Windows VMs that are configured using Storage Spaces.</span></span>
* <span data-ttu-id="0a93d-138">Como desabilitar a criptografia no OS e em unidades de dados para VMs do Windows.</span><span class="sxs-lookup"><span data-stu-id="0a93d-138">Disabling encryption on OS and data drives for Windows VMs.</span></span>
* <span data-ttu-id="0a93d-139">Todos os recursos (como o Cofre de chaves, a conta de armazenamento e VM) devem estar no hello mesma região do Azure e assinatura.</span><span class="sxs-lookup"><span data-stu-id="0a93d-139">All resources (such as Key Vault, Storage account, and VM) must be in hello same Azure region and subscription.</span></span>
* <span data-ttu-id="0a93d-140">VMs de camada padrão, como as VMs da série A, D, DS, G e GS.</span><span class="sxs-lookup"><span data-stu-id="0a93d-140">Standard tier VMs, such as A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="0a93d-141">Criptografia de disco não é suportada em Olá os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="0a93d-141">Disk encryption is not currently supported in hello following scenarios:</span></span>

* <span data-ttu-id="0a93d-142">VMs de camada básica.</span><span class="sxs-lookup"><span data-stu-id="0a93d-142">Basic tier VMs.</span></span>
* <span data-ttu-id="0a93d-143">Máquinas virtuais criadas usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="0a93d-143">VMs created using hello Classic deployment model.</span></span>
* <span data-ttu-id="0a93d-144">Atualizando chaves de criptografia de saudação em uma VM já criptografada.</span><span class="sxs-lookup"><span data-stu-id="0a93d-144">Updating hello cryptographic keys on an already encrypted VM.</span></span>
* <span data-ttu-id="0a93d-145">Integração com o Serviço de Gerenciamento de Chaves local.</span><span class="sxs-lookup"><span data-stu-id="0a93d-145">Integration with on-prem Key Management Service.</span></span>

## <a name="create-azure-key-vault-and-keys"></a><span data-ttu-id="0a93d-146">Criar o Azure Key Vault e as chaves</span><span class="sxs-lookup"><span data-stu-id="0a93d-146">Create Azure Key Vault and keys</span></span>
<span data-ttu-id="0a93d-147">Antes de começar, certifique-se se Olá a última versão de hello Azure PowerShell módulo foi instalado.</span><span class="sxs-lookup"><span data-stu-id="0a93d-147">Before you start, make sure that hello latest version of hello Azure PowerShell module has been installed.</span></span> <span data-ttu-id="0a93d-148">Para obter mais informações, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0a93d-148">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="0a93d-149">Ao longo de exemplos de comando hello, substitua todos os parâmetros de exemplo com seus próprios nomes, o local e valores de chave.</span><span class="sxs-lookup"><span data-stu-id="0a93d-149">Throughout hello command examples, replace all example parameters with your own names, location, and key values.</span></span> <span data-ttu-id="0a93d-150">Olá, exemplos a seguir usam uma convenção de *myResourceGroup*, *myKeyVault*, *myVM*, etc.</span><span class="sxs-lookup"><span data-stu-id="0a93d-150">hello following examples use a convention of *myResourceGroup*, *myKeyVault*, *myVM*, etc.</span></span>

<span data-ttu-id="0a93d-151">primeira etapa de saudação é toocreate toostore um cofre de chaves do Azure as chaves criptográficas.</span><span class="sxs-lookup"><span data-stu-id="0a93d-151">hello first step is toocreate an Azure Key Vault toostore your cryptographic keys.</span></span> <span data-ttu-id="0a93d-152">Cofre de chaves do Azure pode armazenar segredos, chaves ou senhas que permitem que você toosecurely implementação-las em seus aplicativos e serviços.</span><span class="sxs-lookup"><span data-stu-id="0a93d-152">Azure Key Vault can store keys, secrets, or passwords that allow you toosecurely implement them in your applications and services.</span></span> <span data-ttu-id="0a93d-153">Para criptografia de disco virtual, crie um cofre de chaves toostore uma chave criptográfica que é usada tooencrypt ou descriptografar os discos virtuais.</span><span class="sxs-lookup"><span data-stu-id="0a93d-153">For virtual disk encryption, you create a Key Vault toostore a cryptographic key that is used tooencrypt or decrypt your virtual disks.</span></span> 

<span data-ttu-id="0a93d-154">Habilitar provedor de Azure Key Vault hello dentro de sua assinatura do Azure com [registro AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider), em seguida, crie um grupo de recursos com [AzureRmResourceGroup novo](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="0a93d-154">Enable hello Azure Key Vault provider within your Azure subscription with [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider), then create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="0a93d-155">Olá, exemplo a seguir cria um nome de grupo de recursos *myResourceGroup* em Olá *Leste dos EUA* local:</span><span class="sxs-lookup"><span data-stu-id="0a93d-155">hello following example creates a resource group name *myResourceGroup* in hello *East US* location:</span></span>

```powershell
$rgName = "myResourceGroup"
$location = "East US"

Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"
New-AzureRmResourceGroup -Location $location -Name $rgName
```

<span data-ttu-id="0a93d-156">Hello Azure Key Vault contendo Olá chaves criptográficas e computação associada recursos, como armazenamento e hello própria máquina virtual devem residir no hello mesma região.</span><span class="sxs-lookup"><span data-stu-id="0a93d-156">hello Azure Key Vault containing hello cryptographic keys and associated compute resources such as storage and hello VM itself must reside in hello same region.</span></span> <span data-ttu-id="0a93d-157">Criar um cofre de chaves do Azure com [AzureRmKeyVault novo](/powershell/module/azurerm.keyvault/new-azurermkeyvault) e habilitar Olá Cofre de chaves para uso com criptografia de disco.</span><span class="sxs-lookup"><span data-stu-id="0a93d-157">Create an Azure Key Vault with [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) and enable hello Key Vault for use with disk encryption.</span></span> <span data-ttu-id="0a93d-158">Especifique um nome exclusivo de Key Vault para *keyVaultName* da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0a93d-158">Specify a unique Key Vault name for *keyVaultName* as follows:</span></span>

```powershell
$keyVaultName = "myUniqueKeyVaultName"
New-AzureRmKeyVault -Location $location `
    -ResourceGroupName $rgName `
    -VaultName $keyVaultName `
    -EnabledForDiskEncryption
```

<span data-ttu-id="0a93d-159">É possível armazenar chaves de criptografia usando a proteção do Modelo de segurança de Hardware (HSM) ou software.</span><span class="sxs-lookup"><span data-stu-id="0a93d-159">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="0a93d-160">Usar um HSM requer um Cofre de Chaves premium.</span><span class="sxs-lookup"><span data-stu-id="0a93d-160">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="0a93d-161">Há um custo adicional toocreating um premium Cofre de chaves em vez de Cofre de chave padrão que armazena as chaves protegidas por software.</span><span class="sxs-lookup"><span data-stu-id="0a93d-161">There is an additional cost toocreating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="0a93d-162">toocreate um cofre de chaves, premium em Olá anterior etapa Adicionar Olá *- Sku "Premium"* parâmetros.</span><span class="sxs-lookup"><span data-stu-id="0a93d-162">toocreate a premium Key Vault, in hello preceding step add hello *-Sku "Premium"* parameters.</span></span> <span data-ttu-id="0a93d-163">Olá exemplo a seguir usa chaves protegidas por software pois criamos um cofre de chaves padrão.</span><span class="sxs-lookup"><span data-stu-id="0a93d-163">hello following example uses software-protected keys since we created a standard Key Vault.</span></span> 

<span data-ttu-id="0a93d-164">Para ambos os modelos de proteção, Olá plataforma Windows Azure precisa toobe concedida chaves de criptografia de saudação do acesso toorequest quando Olá VM inicializa os discos virtuais toodecrypt hello.</span><span class="sxs-lookup"><span data-stu-id="0a93d-164">For both protection models, hello Azure platform needs toobe granted access toorequest hello cryptographic keys when hello VM boots toodecrypt hello virtual disks.</span></span> <span data-ttu-id="0a93d-165">Crie uma chave de criptografia em seu Key Vault com [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey).</span><span class="sxs-lookup"><span data-stu-id="0a93d-165">Create a cryptographic key in your Key Vault with [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey).</span></span> <span data-ttu-id="0a93d-166">Olá, exemplo a seguir cria uma chave chamada *myKey*:</span><span class="sxs-lookup"><span data-stu-id="0a93d-166">hello following example creates a key named *myKey*:</span></span>

```powershell
Add-AzureKeyVaultKey -VaultName $keyVaultName `
    -Name "myKey" `
    -Destination "Software"
```


## <a name="create-hello-azure-active-directory-service-principal"></a><span data-ttu-id="0a93d-167">Criar hello entidade de serviço do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="0a93d-167">Create hello Azure Active Directory service principal</span></span>
<span data-ttu-id="0a93d-168">Quando discos virtuais são criptografados ou descriptografados, especifique um conta toohandle Olá de autenticação e troca de chaves de criptografia do Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="0a93d-168">When virtual disks are encrypted or decrypted, you specify an account toohandle hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="0a93d-169">Essa conta, uma entidade de serviço do Active Directory do Azure, permite Olá plataforma Windows Azure toorequest chaves de criptografia apropriado Olá em nome hello VM.</span><span class="sxs-lookup"><span data-stu-id="0a93d-169">This account, an Azure Active Directory service principal, allows hello Azure platform toorequest hello appropriate cryptographic keys on behalf of hello VM.</span></span> <span data-ttu-id="0a93d-170">Uma instância do Azure Active Directory padrão está disponível em sua assinatura, embora muitas organizações tenham diretórios do Azure Active Directory dedicados.</span><span class="sxs-lookup"><span data-stu-id="0a93d-170">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="0a93d-171">Crie uma entidade de serviço no Azure Active Directory com [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal).</span><span class="sxs-lookup"><span data-stu-id="0a93d-171">Create a service principal in Azure Active Directory with [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal).</span></span> <span data-ttu-id="0a93d-172">toospecify uma senha segura, execute Olá [políticas de senha e restrições do Active Directory do Azure](../../active-directory/active-directory-passwords-policy.md):</span><span class="sxs-lookup"><span data-stu-id="0a93d-172">toospecify a secure password, follow hello [Password policies and restrictions in Azure Active Directory](../../active-directory/active-directory-passwords-policy.md):</span></span>

```powershell
$appName = "My App"
$securePassword = "P@ssword!"
$app = New-AzureRmADApplication -DisplayName $appName `
    -HomePage "https://myapp.contoso.com" `
    -IdentifierUris "https://contoso.com/myapp" `
    -Password $securePassword
New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
```

<span data-ttu-id="0a93d-173">toosuccessfully criptografar ou descriptografar discos virtuais, as permissões na chave de criptografia Olá armazenadas no cofre de chaves devem ser conjunto toopermit hello Azure Active Directory tooread principal Olá as chaves de serviço.</span><span class="sxs-lookup"><span data-stu-id="0a93d-173">toosuccessfully encrypt or decrypt virtual disks, permissions on hello cryptographic key stored in Key Vault must be set toopermit hello Azure Active Directory service principal tooread hello keys.</span></span> <span data-ttu-id="0a93d-174">Defina permissões no Key Vault com [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy):</span><span class="sxs-lookup"><span data-stu-id="0a93d-174">Set permissions on your Key Vault with [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy):</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName $keyvaultName `
    -ServicePrincipalName $app.ApplicationId `
    -PermissionsToKeys "WrapKey" `
    -PermissionsToSecrets "Set"
```


## <a name="create-virtual-machine"></a><span data-ttu-id="0a93d-175">Criar máquina virtual</span><span class="sxs-lookup"><span data-stu-id="0a93d-175">Create virtual machine</span></span>
<span data-ttu-id="0a93d-176">tootest Olá o processo de criptografia, vamos criar uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0a93d-176">tootest hello encryption process, let's create a VM.</span></span> <span data-ttu-id="0a93d-177">Olá, exemplo a seguir cria uma VM denominada *myVM* usando um *Datacenter do Windows Server 2016* imagem:</span><span class="sxs-lookup"><span data-stu-id="0a93d-177">hello following example creates a VM named *myVM* using a *Windows Server 2016 Datacenter* image:</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

$vnet = New-AzureRmVirtualNetwork -ResourceGroupName $rgName `
    -Location $location `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

$pip = New-AzureRmPublicIpAddress -ResourceGroupName $rgName `
    -Location $location `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "mypublicdns$(Get-Random)"

$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName `
    -Location $location `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP

$nic = New-AzureRmNetworkInterface -Name myNic `
    -ResourceGroupName $rgName `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $pip.Id `
    -NetworkSecurityGroupId $nsg.Id

$cred = Get-Credential

$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize Standard_D1 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2016-Datacenter -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vmConfig
```


## <a name="encrypt-virtual-machine"></a><span data-ttu-id="0a93d-178">Criptografar máquina virtual</span><span class="sxs-lookup"><span data-stu-id="0a93d-178">Encrypt virtual machine</span></span>
<span data-ttu-id="0a93d-179">discos virtuais do tooencrypt hello, você reúne todos os componentes anteriores do hello:</span><span class="sxs-lookup"><span data-stu-id="0a93d-179">tooencrypt hello virtual disks, you bring together all hello previous components:</span></span>

1. <span data-ttu-id="0a93d-180">Especifique Olá entidade de serviço do Active Directory do Azure e a senha.</span><span class="sxs-lookup"><span data-stu-id="0a93d-180">Specify hello Azure Active Directory service principal and password.</span></span>
2. <span data-ttu-id="0a93d-181">Especifica Olá Cofre de chaves toostore Olá metadados para os discos criptografados.</span><span class="sxs-lookup"><span data-stu-id="0a93d-181">Specify hello Key Vault toostore hello metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="0a93d-182">Especifique Olá toouse de chaves de criptografia para criptografia hello e descriptografia.</span><span class="sxs-lookup"><span data-stu-id="0a93d-182">Specify hello cryptographic keys toouse for hello actual encryption and decryption.</span></span>
4. <span data-ttu-id="0a93d-183">Especifique se você deseja tooencrypt disco de saudação SO, discos de dados de saudação ou todos.</span><span class="sxs-lookup"><span data-stu-id="0a93d-183">Specify whether you want tooencrypt hello OS disk, hello data disks, or all.</span></span>

<span data-ttu-id="0a93d-184">Criptografar sua VM com [AzureRmVMDiskEncryptionExtension conjunto](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) usando a chave de Cofre de chaves do Azure hello e credenciais de entidade de serviço do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="0a93d-184">Encrypt your VM with [Set-AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) using hello Azure Key Vault key and Azure Active Directory service principal credentials.</span></span> <span data-ttu-id="0a93d-185">Olá exemplo a seguir recupera todas as informações de chave hello, em seguida, criptografa Olá VM denominada *myVM*:</span><span class="sxs-lookup"><span data-stu-id="0a93d-185">hello following example retrieves all hello key information then encrypts hello VM named *myVM*:</span></span>

```powershell
$keyVault = Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $rgName;
$diskEncryptionKeyVaultUrl = $keyVault.VaultUri;
$keyVaultResourceId = $keyVault.ResourceId;
$keyEncryptionKeyUrl = (Get-AzureKeyVaultKey -VaultName $keyVaultName -Name myKey).Key.kid;

Set-AzureRmVMDiskEncryptionExtension -ResourceGroupName $rgName `
    -VMName $vmName `
    -AadClientID $app.ApplicationId `
    -AadClientSecret $securePassword `
    -DiskEncryptionKeyVaultUrl $diskEncryptionKeyVaultUrl `
    -DiskEncryptionKeyVaultId $keyVaultResourceId `
    -KeyEncryptionKeyUrl $keyEncryptionKeyUrl `
    -KeyEncryptionKeyVaultId $keyVaultResourceId
```

<span data-ttu-id="0a93d-186">Aceite Olá toocontinue de prompt com criptografia de VM hello.</span><span class="sxs-lookup"><span data-stu-id="0a93d-186">Accept hello prompt toocontinue with hello VM encryption.</span></span> <span data-ttu-id="0a93d-187">Olá VM reinicia durante o processo de saudação.</span><span class="sxs-lookup"><span data-stu-id="0a93d-187">hello VM restarts during hello process.</span></span> <span data-ttu-id="0a93d-188">Depois de conclusão do processo de criptografia hello e hello VM será reinicializado, examinar o status de criptografia de saudação com [Get-AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):</span><span class="sxs-lookup"><span data-stu-id="0a93d-188">Once hello encryption process completes and hello VM has rebooted, review hello encryption status with [Get-AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):</span></span>

```powershell
Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $rgName -VMName $vmName
```

<span data-ttu-id="0a93d-189">saudação de saída é similar toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="0a93d-189">hello output is similar toohello following example:</span></span>

```powershell
OsVolumeEncrypted          : Encrypted
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OsVolume: Encrypted, DataVolumes: Encrypted
```

## <a name="next-steps"></a><span data-ttu-id="0a93d-190">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0a93d-190">Next steps</span></span>
* <span data-ttu-id="0a93d-191">Para saber mais sobre como gerenciar o Azure Key Vault, confira [Configurar o Key Vault para máquinas virtuais](key-vault-setup.md).</span><span class="sxs-lookup"><span data-stu-id="0a93d-191">For more information about managing Azure Key Vault, see [Set up Key Vault for virtual machines](key-vault-setup.md).</span></span>
* <span data-ttu-id="0a93d-192">Para obter mais informações sobre criptografia de disco, como preparar um tooAzure da tooupload VM personalizado criptografado, consulte [criptografia de disco do Azure](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="0a93d-192">For more information about disk encryption, such as preparing an encrypted custom VM tooupload tooAzure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
