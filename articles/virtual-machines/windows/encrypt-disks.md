---
title: Criptografar discos em uma VM do Windows no Azure | Microsoft Docs
description: "Como criptografar discos virtuais em uma VM do Windows para aumentar a segurança usando o Azure PowerShell"
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
ms.openlocfilehash: 98b42b252a601af090579e3939f3c7ab91c3803b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-encrypt-virtual-disks-on-a-windows-vm"></a><span data-ttu-id="2d4ff-103">Como criptografar discos virtuais em uma VM do Windows</span><span class="sxs-lookup"><span data-stu-id="2d4ff-103">How to encrypt virtual disks on a Windows VM</span></span>
<span data-ttu-id="2d4ff-104">Para conformidade e segurança aprimorados da VM (máquina virtual), os discos virtuais no Azure podem ser criptografados.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted.</span></span> <span data-ttu-id="2d4ff-105">Discos são criptografados usando chaves criptográficas que são protegidas em um Cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="2d4ff-106">Você controla essas chaves criptográficas e pode auditar seu uso.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="2d4ff-107">Este artigo detalha como criptografar discos virtuais em uma VM do Windows usando o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-107">This article details how to encrypt virtual disks on a Windows VM using Azure PowerShell.</span></span> <span data-ttu-id="2d4ff-108">Também é possível [Criptografar uma VM do Linux usando a CLI 2.0 do Azure](../linux/encrypt-disks.md).</span><span class="sxs-lookup"><span data-stu-id="2d4ff-108">You can also [encrypt a Linux VM using the Azure CLI 2.0](../linux/encrypt-disks.md).</span></span>

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="2d4ff-109">Visão geral da criptografia de disco</span><span class="sxs-lookup"><span data-stu-id="2d4ff-109">Overview of disk encryption</span></span>
<span data-ttu-id="2d4ff-110">Discos virtuais em VMs do Windows são criptografados em repouso usando o Bitlocker.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-110">Virtual disks on Windows VMs are encrypted at rest using Bitlocker.</span></span> <span data-ttu-id="2d4ff-111">Não há nenhuma taxa para criptografar discos virtuais no Azure.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-111">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="2d4ff-112">Chaves e criptográficas são armazenadas no Cofre de chaves do Azure usando a proteção de software ou você pode importar ou gerar as chaves em Módulos de segurança de Hardware (HSMs) certificados para padrões de nível 2 de FIPS 140-2.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-112">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified to FIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="2d4ff-113">Essas chaves criptográficas são usadas para criptografar e descriptografar os discos virtuais conectados à sua VM.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-113">These cryptographic keys are used to encrypt and decrypt virtual disks attached to your VM.</span></span> <span data-ttu-id="2d4ff-114">Você mantém o controle dessas chaves criptográficas e pode auditar seu uso.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-114">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="2d4ff-115">Uma entidade de serviço do Azure Active Directory fornece um mecanismo seguro para emitir essas chaves de criptografia, enquanto as VMs são ligadas e desligadas.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-115">An Azure Active Directory service principal provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="2d4ff-116">O processo de criptografia de uma VM é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="2d4ff-116">The process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="2d4ff-117">Crie uma chave de criptografia em um Cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-117">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="2d4ff-118">Configure a chave de criptografia a ser usada para criptografar discos.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-118">Configure the cryptographic key to be usable for encrypting disks.</span></span>
3. <span data-ttu-id="2d4ff-119">Para ler a chave de criptografia do Azure Key Vault, crie uma entidade de serviço do Azure Active Directory com as permissões apropriadas.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-119">To read the cryptographic key from the Azure Key Vault, create an Azure Active Directory service principal with the appropriate permissions.</span></span>
4. <span data-ttu-id="2d4ff-120">Execute o comando para criptografar seus discos virtuais, especificando a entidade de serviço do Azure Active Directory e a chave de criptografia apropriada a ser usada.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-120">Issue the command to encrypt your virtual disks, specifying the Azure Active Directory service principal and appropriate cryptographic key to be used.</span></span>
5. <span data-ttu-id="2d4ff-121">A entidade de serviço do Azure Active Directory solicita a chave de criptografia necessária do Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-121">The Azure Active Directory service principal requests the required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="2d4ff-122">Os discos virtuais são criptografados usando a chave de criptografia fornecida.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-122">The virtual disks are encrypted using the provided cryptographic key.</span></span>

## <a name="encryption-process"></a><span data-ttu-id="2d4ff-123">Processo de criptografia</span><span class="sxs-lookup"><span data-stu-id="2d4ff-123">Encryption process</span></span>
<span data-ttu-id="2d4ff-124">A criptografia de disco depende dos seguintes componentes adicionais:</span><span class="sxs-lookup"><span data-stu-id="2d4ff-124">Disk encryption relies on the following additional components:</span></span>

* <span data-ttu-id="2d4ff-125">**Cofre de Chaves do Azure** – usado para proteger chaves criptográficas e segredos usados para o processo de criptografia/descriptografia do disco.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-125">**Azure Key Vault** - used to safeguard cryptographic keys and secrets used for the disk encryption/decryption process.</span></span> 
  * <span data-ttu-id="2d4ff-126">Se houver um, você pode usar um Cofre de Chaves do Azure existente.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-126">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="2d4ff-127">Não é necessário dedicar um Cofre de Chaves para criptografar discos.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-127">You do not have to dedicate a Key Vault to encrypting disks.</span></span>
  * <span data-ttu-id="2d4ff-128">Para separar os limites administrativos e visibilidade de chave, crie um Cofre de Chaves dedicado.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-128">To separate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="2d4ff-129">**Azure Active Directory** – realiza a troca segura de chaves criptográficas necessárias e a autenticação para ações solicitadas.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-129">**Azure Active Directory** - handles the secure exchanging of required cryptographic keys and authentication for requested actions.</span></span> 
  * <span data-ttu-id="2d4ff-130">Normalmente, você pode usar uma instância existente do Azure Active Directory para hospedar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-130">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="2d4ff-131">A entidade de serviço fornece um mecanismo seguro para solicitar e receber as chaves de criptografia apropriadas.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-131">The service principal provides a secure mechanism to request and be issued the appropriate cryptographic keys.</span></span> <span data-ttu-id="2d4ff-132">Você não está desenvolvendo um aplicativo real que se integra ao Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-132">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="2d4ff-133">Requisitos e limitações</span><span class="sxs-lookup"><span data-stu-id="2d4ff-133">Requirements and limitations</span></span>
<span data-ttu-id="2d4ff-134">Requisitos e cenários com suporte para criptografia de disco:</span><span class="sxs-lookup"><span data-stu-id="2d4ff-134">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="2d4ff-135">Habilitar a criptografia em novas VMs do Windows a partir de imagens do Azure Marketplace ou de uma imagem VHD personalizada.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-135">Enabling encryption on new Windows VMs from Azure Marketplace images or custom VHD image.</span></span>
* <span data-ttu-id="2d4ff-136">Habilitar a criptografia em VMs existentes do Windows no Azure.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-136">Enabling encryption on existing Windows VMs in Azure.</span></span>
* <span data-ttu-id="2d4ff-137">Habilitar a criptografia em VMs do Windows que são configuradas usando Espaços de Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-137">Enabling encryption on Windows VMs that are configured using Storage Spaces.</span></span>
* <span data-ttu-id="2d4ff-138">Como desabilitar a criptografia no OS e em unidades de dados para VMs do Windows.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-138">Disabling encryption on OS and data drives for Windows VMs.</span></span>
* <span data-ttu-id="2d4ff-139">Todos os recursos (por exemplo, Cofre de chaves, conta de Armazenamento e VM) devem pertencer à mesma assinatura e região do Azure.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-139">All resources (such as Key Vault, Storage account, and VM) must be in the same Azure region and subscription.</span></span>
* <span data-ttu-id="2d4ff-140">VMs de camada padrão, como as VMs da série A, D, DS, G e GS.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-140">Standard tier VMs, such as A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="2d4ff-141">A criptografia de disco não tem suporte atualmente nos seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="2d4ff-141">Disk encryption is not currently supported in the following scenarios:</span></span>

* <span data-ttu-id="2d4ff-142">VMs de camada básica.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-142">Basic tier VMs.</span></span>
* <span data-ttu-id="2d4ff-143">VMs criadas com o modelo de implantação Clássico.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-143">VMs created using the Classic deployment model.</span></span>
* <span data-ttu-id="2d4ff-144">Atualização das chaves de criptografia em uma VM já criptografada.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-144">Updating the cryptographic keys on an already encrypted VM.</span></span>
* <span data-ttu-id="2d4ff-145">Integração com o Serviço de Gerenciamento de Chaves local.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-145">Integration with on-prem Key Management Service.</span></span>

## <a name="create-azure-key-vault-and-keys"></a><span data-ttu-id="2d4ff-146">Criar o Azure Key Vault e as chaves</span><span class="sxs-lookup"><span data-stu-id="2d4ff-146">Create Azure Key Vault and keys</span></span>
<span data-ttu-id="2d4ff-147">Antes de começar, verifique se você tem a versão mais recente do módulo Azure PowerShell instalar.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-147">Before you start, make sure that the latest version of the Azure PowerShell module has been installed.</span></span> <span data-ttu-id="2d4ff-148">Para saber mais, consulte [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview):</span><span class="sxs-lookup"><span data-stu-id="2d4ff-148">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="2d4ff-149">Em todos os exemplos de comando, substitua todos os parâmetros de exemplo pelos seus próprios valores de nome, localização e chave.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-149">Throughout the command examples, replace all example parameters with your own names, location, and key values.</span></span> <span data-ttu-id="2d4ff-150">Os exemplos a seguir usam uma convenção de *myResourceGroup*, *myKeyVault*, *myVM*, etc.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-150">The following examples use a convention of *myResourceGroup*, *myKeyVault*, *myVM*, etc.</span></span>

<span data-ttu-id="2d4ff-151">A primeira etapa é criar um Cofre de Chaves do Azure para armazenar as chaves criptográficas.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-151">The first step is to create an Azure Key Vault to store your cryptographic keys.</span></span> <span data-ttu-id="2d4ff-152">O Cofre de Chaves do Azure pode armazenar chaves, segredos ou senhas que permitem implementá-los de forma segura em seus aplicativos e serviços.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-152">Azure Key Vault can store keys, secrets, or passwords that allow you to securely implement them in your applications and services.</span></span> <span data-ttu-id="2d4ff-153">Para criptografia de disco virtual, crie o Key Vault para armazenar uma chave de criptografia que é usada para criptografar ou descriptografar seus discos virtuais.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-153">For virtual disk encryption, you create a Key Vault to store a cryptographic key that is used to encrypt or decrypt your virtual disks.</span></span> 

<span data-ttu-id="2d4ff-154">Habilite o provedor do Azure Key Vault em sua assinatura do Azure com [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider) e crie um grupo de recursos com [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="2d4ff-154">Enable the Azure Key Vault provider within your Azure subscription with [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider), then create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="2d4ff-155">O exemplo a seguir cria um grupo de recursos chamado *myResourceGroup* no local *Leste dos EUA*:</span><span class="sxs-lookup"><span data-stu-id="2d4ff-155">The following example creates a resource group name *myResourceGroup* in the *East US* location:</span></span>

```powershell
$rgName = "myResourceGroup"
$location = "East US"

Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"
New-AzureRmResourceGroup -Location $location -Name $rgName
```

<span data-ttu-id="2d4ff-156">O Cofre de chaves do Azure que contém as chaves criptográficas e recursos de computação associados, como armazenamento e a própria VM deve residir na mesma região.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-156">The Azure Key Vault containing the cryptographic keys and associated compute resources such as storage and the VM itself must reside in the same region.</span></span> <span data-ttu-id="2d4ff-157">Crie um Azure Key Vault com [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) e habilite o Key Vault para uso com criptografia de disco.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-157">Create an Azure Key Vault with [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) and enable the Key Vault for use with disk encryption.</span></span> <span data-ttu-id="2d4ff-158">Especifique um nome exclusivo de Key Vault para *keyVaultName* da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="2d4ff-158">Specify a unique Key Vault name for *keyVaultName* as follows:</span></span>

```powershell
$keyVaultName = "myUniqueKeyVaultName"
New-AzureRmKeyVault -Location $location `
    -ResourceGroupName $rgName `
    -VaultName $keyVaultName `
    -EnabledForDiskEncryption
```

<span data-ttu-id="2d4ff-159">É possível armazenar chaves de criptografia usando a proteção do Modelo de segurança de Hardware (HSM) ou software.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-159">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="2d4ff-160">Usar um HSM requer um Cofre de Chaves premium.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-160">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="2d4ff-161">Há um custo adicional para a criação de um Cofre de Chaves premium em vez do Cofre de Chaves padrão que armazena as chaves protegidas por software.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-161">There is an additional cost to creating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="2d4ff-162">Para criar um Key Vault Premium, na etapa anterior, adicione os parâmetros *-SKU "Premium"*.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-162">To create a premium Key Vault, in the preceding step add the *-Sku "Premium"* parameters.</span></span> <span data-ttu-id="2d4ff-163">O exemplo a seguir usa chaves protegidas por software, desde que criamos um Cofre de Chaves padrão.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-163">The following example uses software-protected keys since we created a standard Key Vault.</span></span> 

<span data-ttu-id="2d4ff-164">Para ambos os modelos de proteção, a plataforma do Azure deve ter acesso para solicitar as chaves criptográficas quando a VM é inicializada para descriptografar os discos virtuais.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-164">For both protection models, the Azure platform needs to be granted access to request the cryptographic keys when the VM boots to decrypt the virtual disks.</span></span> <span data-ttu-id="2d4ff-165">Crie uma chave de criptografia em seu Key Vault com [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey).</span><span class="sxs-lookup"><span data-stu-id="2d4ff-165">Create a cryptographic key in your Key Vault with [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey).</span></span> <span data-ttu-id="2d4ff-166">O exemplo a seguir cria uma chave chamada *myKey*:</span><span class="sxs-lookup"><span data-stu-id="2d4ff-166">The following example creates a key named *myKey*:</span></span>

```powershell
Add-AzureKeyVaultKey -VaultName $keyVaultName `
    -Name "myKey" `
    -Destination "Software"
```


## <a name="create-the-azure-active-directory-service-principal"></a><span data-ttu-id="2d4ff-167">Criar a entidade de serviço do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2d4ff-167">Create the Azure Active Directory service principal</span></span>
<span data-ttu-id="2d4ff-168">Quando os discos virtuais são criptografados ou descriptografados, especifique uma conta para lidar com a autenticação e a troca de chaves de criptografia do Key Vault.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-168">When virtual disks are encrypted or decrypted, you specify an account to handle the authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="2d4ff-169">Essa conta, uma entidade de serviço do Azure Active Directory, permite que a plataforma do Azure solicite as chaves de criptografia apropriadas em nome da VM.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-169">This account, an Azure Active Directory service principal, allows the Azure platform to request the appropriate cryptographic keys on behalf of the VM.</span></span> <span data-ttu-id="2d4ff-170">Uma instância do Azure Active Directory padrão está disponível em sua assinatura, embora muitas organizações tenham diretórios do Azure Active Directory dedicados.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-170">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="2d4ff-171">Crie uma entidade de serviço no Azure Active Directory com [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal).</span><span class="sxs-lookup"><span data-stu-id="2d4ff-171">Create a service principal in Azure Active Directory with [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal).</span></span> <span data-ttu-id="2d4ff-172">Para especificar uma senha segura, siga as [Políticas e restrições de senha do Azure Active Directory](../../active-directory/active-directory-passwords-policy.md):</span><span class="sxs-lookup"><span data-stu-id="2d4ff-172">To specify a secure password, follow the [Password policies and restrictions in Azure Active Directory](../../active-directory/active-directory-passwords-policy.md):</span></span>

```powershell
$appName = "My App"
$securePassword = "P@ssword!"
$app = New-AzureRmADApplication -DisplayName $appName `
    -HomePage "https://myapp.contoso.com" `
    -IdentifierUris "https://contoso.com/myapp" `
    -Password $securePassword
New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
```

<span data-ttu-id="2d4ff-173">Para criptografar ou descriptografar discos virtuais com êxito, as permissões na chave de criptografia armazenada no Key Vault devem ser definidas para permitir que a entidade de serviço do Azure Active Directory leia as chaves.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-173">To successfully encrypt or decrypt virtual disks, permissions on the cryptographic key stored in Key Vault must be set to permit the Azure Active Directory service principal to read the keys.</span></span> <span data-ttu-id="2d4ff-174">Defina permissões no Key Vault com [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy):</span><span class="sxs-lookup"><span data-stu-id="2d4ff-174">Set permissions on your Key Vault with [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy):</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName $keyvaultName `
    -ServicePrincipalName $app.ApplicationId `
    -PermissionsToKeys "WrapKey" `
    -PermissionsToSecrets "Set"
```


## <a name="create-virtual-machine"></a><span data-ttu-id="2d4ff-175">Criar máquina virtual</span><span class="sxs-lookup"><span data-stu-id="2d4ff-175">Create virtual machine</span></span>
<span data-ttu-id="2d4ff-176">Para testar o processo de criptografia, vamos criar uma VM.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-176">To test the encryption process, let's create a VM.</span></span> <span data-ttu-id="2d4ff-177">O exemplo a seguir cria uma VM chamada *myVM* usando uma imagem do *Datacenter do Windows Server 2016*:</span><span class="sxs-lookup"><span data-stu-id="2d4ff-177">The following example creates a VM named *myVM* using a *Windows Server 2016 Datacenter* image:</span></span>

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


## <a name="encrypt-virtual-machine"></a><span data-ttu-id="2d4ff-178">Criptografar máquina virtual</span><span class="sxs-lookup"><span data-stu-id="2d4ff-178">Encrypt virtual machine</span></span>
<span data-ttu-id="2d4ff-179">Para criptografar os discos virtuais, reúna todos os componentes anteriores:</span><span class="sxs-lookup"><span data-stu-id="2d4ff-179">To encrypt the virtual disks, you bring together all the previous components:</span></span>

1. <span data-ttu-id="2d4ff-180">Especifique a entidade de serviço e senha do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-180">Specify the Azure Active Directory service principal and password.</span></span>
2. <span data-ttu-id="2d4ff-181">Especifique o Cofre de chaves para armazenar os metadados para os discos criptografados.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-181">Specify the Key Vault to store the metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="2d4ff-182">Especifique as chaves de criptografia a serem usadas para criptografia e descriptografia.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-182">Specify the cryptographic keys to use for the actual encryption and decryption.</span></span>
4. <span data-ttu-id="2d4ff-183">Especifique se deseja criptografar o disco do sistema operacional, os discos de dados ou todos.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-183">Specify whether you want to encrypt the OS disk, the data disks, or all.</span></span>

<span data-ttu-id="2d4ff-184">Criptografe sua VM com [Set-AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) usando a chave do Azure Key Vault e as credenciais de entidade de serviço do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-184">Encrypt your VM with [Set-AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) using the Azure Key Vault key and Azure Active Directory service principal credentials.</span></span> <span data-ttu-id="2d4ff-185">O exemplo a seguir recupera todas as informações de chave e depois criptografa a VM chamada *myVM*:</span><span class="sxs-lookup"><span data-stu-id="2d4ff-185">The following example retrieves all the key information then encrypts the VM named *myVM*:</span></span>

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

<span data-ttu-id="2d4ff-186">Aceite o aviso para continuar com a criptografia da VM.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-186">Accept the prompt to continue with the VM encryption.</span></span> <span data-ttu-id="2d4ff-187">A VM é reiniciada durante o processo.</span><span class="sxs-lookup"><span data-stu-id="2d4ff-187">The VM restarts during the process.</span></span> <span data-ttu-id="2d4ff-188">Após a conclusão do processo de criptografia e reinicialização da VM, examine o status de criptografia com [Get-AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):</span><span class="sxs-lookup"><span data-stu-id="2d4ff-188">Once the encryption process completes and the VM has rebooted, review the encryption status with [Get-AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):</span></span>

```powershell
Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $rgName -VMName $vmName
```

<span data-ttu-id="2d4ff-189">A saída deverá ser semelhante ao seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="2d4ff-189">The output is similar to the following example:</span></span>

```powershell
OsVolumeEncrypted          : Encrypted
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OsVolume: Encrypted, DataVolumes: Encrypted
```

## <a name="next-steps"></a><span data-ttu-id="2d4ff-190">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2d4ff-190">Next steps</span></span>
* <span data-ttu-id="2d4ff-191">Para saber mais sobre como gerenciar o Azure Key Vault, confira [Configurar o Key Vault para máquinas virtuais](key-vault-setup.md).</span><span class="sxs-lookup"><span data-stu-id="2d4ff-191">For more information about managing Azure Key Vault, see [Set up Key Vault for virtual machines](key-vault-setup.md).</span></span>
* <span data-ttu-id="2d4ff-192">Para obter mais informações sobre criptografia de disco, como preparar uma VM personalizada criptografada para carregar no Azure, consulte [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="2d4ff-192">For more information about disk encryption, such as preparing an encrypted custom VM to upload to Azure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
