---
title: Criptografar discos em uma VM do Linux no Azure | Microsoft Docs
description: "Como criptografar discos virtuais em uma VM Linux para aumentar a segurança usando a CLI do Azure 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 2a23b6fa-6941-4998-9804-8efe93b647b3
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: 172b4c8f5c098d776cb689543f5d8f163b8895b4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-encrypt-virtual-disks-on-a-linux-vm"></a><span data-ttu-id="d7e4c-103">Como criptografar discos virtuais em uma VM Linux</span><span class="sxs-lookup"><span data-stu-id="d7e4c-103">How to encrypt virtual disks on a Linux VM</span></span>
<span data-ttu-id="d7e4c-104">Para conformidade e segurança aprimorados da VM (máquina virtual), os discos virtuais no Azure podem ser criptografados.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted.</span></span> <span data-ttu-id="d7e4c-105">Discos são criptografados usando chaves criptográficas que são protegidas em um Cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="d7e4c-106">Você controla essas chaves criptográficas e pode auditar seu uso.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="d7e4c-107">Este artigo detalha como criptografar discos virtuais em uma VM Linux usando a CLI do Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-107">This article details how to encrypt virtual disks on a Linux VM using the Azure CLI 2.0.</span></span> <span data-ttu-id="d7e4c-108">Você também pode executar essas etapas com a [CLI do Azure 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d7e4c-108">You can also perform these steps with the [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="d7e4c-109">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="d7e4c-109">Quick commands</span></span>
<span data-ttu-id="d7e4c-110">Se você precisar realizar rapidamente a tarefa, a seção a seguir detalha a base de dados de comandos para criptografar discos virtuais em sua VM.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-110">If you need to quickly accomplish the task, the following section details the base commands to encrypt virtual disks on your VM.</span></span> <span data-ttu-id="d7e4c-111">Mais informações detalhadas e contexto para cada etapa podem ser encontrados no restante do documento, [começando aqui](#overview-of-disk-encryption).</span><span class="sxs-lookup"><span data-stu-id="d7e4c-111">More detailed information and context for each step can be found the rest of the document, [starting here](#overview-of-disk-encryption).</span></span>

<span data-ttu-id="d7e4c-112">É necessário ter a última [CLI 2.0 do Azure](/cli/azure/install-az-cli2) instalada e conectada a uma conta do Azure usando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="d7e4c-112">You need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="d7e4c-113">Nos exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-113">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="d7e4c-114">Os nomes de parâmetro de exemplo incluem *myResourceGroup*, *myKey* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-114">Example parameter names include *myResourceGroup*, *myKey*, and *myVM*.</span></span>

<span data-ttu-id="d7e4c-115">Primeiro, habilite o provedor do Azure Key Vault dentro de sua assinatura do Azure com [az provider register](/cli/azure/provider#register) e crie um grupo de recursos com [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="d7e4c-115">First, enable the Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="d7e4c-116">O exemplo a seguir cria um grupo de recursos chamado *myResourceGroup* no local *eastus*:</span><span class="sxs-lookup"><span data-stu-id="d7e4c-116">The following example creates a resource group name *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="d7e4c-117">Crie um Azure Key Vault com [az keyvault create](/cli/azure/keyvault#create) e habilite o Key Vault para uso com criptografia de disco.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-117">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable the Key Vault for use with disk encryption.</span></span> <span data-ttu-id="d7e4c-118">Especifique um nome exclusivo de Key Vault para *keyvault_name* da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d7e4c-118">Specify a unique Key Vault name for *keyvault_name* as follows:</span></span>

```azurecli
keyvault_name=mykeyvaultikf
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

<span data-ttu-id="d7e4c-119">Criar uma chave de criptografia em seu Key Vault com [az keyvault key create](/cli/azure/keyvault/key#create).</span><span class="sxs-lookup"><span data-stu-id="d7e4c-119">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span></span> <span data-ttu-id="d7e4c-120">O exemplo a seguir cria uma chave chamada *myKey*:</span><span class="sxs-lookup"><span data-stu-id="d7e4c-120">The following example creates a key named *myKey*:</span></span>

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```

<span data-ttu-id="d7e4c-121">Crie uma entidade de serviço usando o Azure Active Directory com [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span><span class="sxs-lookup"><span data-stu-id="d7e4c-121">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span></span> <span data-ttu-id="d7e4c-122">A entidade de serviço manipula a autenticação e a troca de chaves de criptografia do Key Vault.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-122">The service principal handles the authentication and exchange of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="d7e4c-123">O exemplo a seguir lê os valores da ID e senha da entidade de serviço para uso em comandos posteriores:</span><span class="sxs-lookup"><span data-stu-id="d7e4c-123">The following example reads in the values for the service principal Id and password for use in later commands:</span></span>

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

<span data-ttu-id="d7e4c-124">A senha só será gerada quando você criar a entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-124">The password is only output when you create the service principal.</span></span> <span data-ttu-id="d7e4c-125">Se desejar, exiba e grave a senha (`echo $sp_password`).</span><span class="sxs-lookup"><span data-stu-id="d7e4c-125">If desired, view and record the password (`echo $sp_password`).</span></span> <span data-ttu-id="d7e4c-126">Você pode listar suas entidades de serviço com [az ad sp list](/cli/azure/ad/sp#list) e exibir informações adicionais sobre uma entidade de serviço específica com [az ad sp show](/cli/azure/ad/sp#show).</span><span class="sxs-lookup"><span data-stu-id="d7e4c-126">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span></span>

<span data-ttu-id="d7e4c-127">Defina permissões em seu Key Vault com [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span><span class="sxs-lookup"><span data-stu-id="d7e4c-127">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span></span> <span data-ttu-id="d7e4c-128">No exemplo a seguir, a ID da entidade de serviço é fornecida por meio do comando anterior:</span><span class="sxs-lookup"><span data-stu-id="d7e4c-128">In the following example, the service principal ID is supplied from the preceding command:</span></span>

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
    --key-permissions wrapKey \
    --secret-permissions set
```

<span data-ttu-id="d7e4c-129">Crie uma VM com [az vm create](/cli/azure/vm#create) e anexe um disco de dados de 5 GB.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-129">Create a VM with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span></span> <span data-ttu-id="d7e4c-130">Somente determinadas imagens do marketplace dão suporte à criptografia de disco.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-130">Only certain marketplace images support disk encryption.</span></span> <span data-ttu-id="d7e4c-131">O exemplo a seguir cria uma VM chamada `myVM` usando uma imagem do **CentOS 7.2n**:</span><span class="sxs-lookup"><span data-stu-id="d7e4c-131">The following example creates a VM named `myVM` using a **CentOS 7.2n** image:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

<span data-ttu-id="d7e4c-132">SSH para a VM usando o `publicIpAddress` mostrado na saída do comando anterior.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-132">SSH to your VM using the `publicIpAddress` shown in the output of the preceding command.</span></span> <span data-ttu-id="d7e4c-133">Crie uma partição e o sistema de arquivos e, em seguida, monte o disco de dados.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-133">Create a partition and filesystem, then mount the data disk.</span></span> <span data-ttu-id="d7e4c-134">Para obter mais informações, consulte [Conectar-se a uma VM Linux para montar o novo disco](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="d7e4c-134">For more information, see [Connect to a Linux VM to mount the new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> <span data-ttu-id="d7e4c-135">Feche a sessão SSH.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-135">Close your SSH session.</span></span>

<span data-ttu-id="d7e4c-136">Criptografe sua VM com [az vm encryption enable](/cli/azure/vm/encryption#enable).</span><span class="sxs-lookup"><span data-stu-id="d7e4c-136">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span></span> <span data-ttu-id="d7e4c-137">O exemplo a seguir usa as variáveis `$sp_id` e `$sp_password` do comando `ad sp create-for-rbac` anterior:</span><span class="sxs-lookup"><span data-stu-id="d7e4c-137">The following example uses the `$sp_id` and `$sp_password` variables from the preceding `ad sp create-for-rbac` command:</span></span>

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

<span data-ttu-id="d7e4c-138">Leva algum tempo para o processo de criptografia de disco ser concluído.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-138">It takes some time for the disk encryption process to complete.</span></span> <span data-ttu-id="d7e4c-139">Monitorar o status do processo com [az vm encryption show](/cli/azure/vm/encryption#show):</span><span class="sxs-lookup"><span data-stu-id="d7e4c-139">Monitor the status of the process with [az vm encryption show](/cli/azure/vm/encryption#show):</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="d7e4c-140">O status mostra **EncryptionInProgress**.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-140">The status shows **EncryptionInProgress**.</span></span> <span data-ttu-id="d7e4c-141">Aguarde até que o status para o sistema operacional disco relate **VMRestartPending**, então reinicie a VM com [az vm restart](/cli/azure/vm#restart):</span><span class="sxs-lookup"><span data-stu-id="d7e4c-141">Wait until the status for the OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="d7e4c-142">O processo de criptografia de disco é finalizado durante o processo de inicialização, portanto, aguarde alguns minutos antes de verificar o status de criptografia novamente com **az vm encryption show**:</span><span class="sxs-lookup"><span data-stu-id="d7e4c-142">The disk encryption process is finalized during the boot process, so wait a few minutes before checking the status of encryption again with **az vm encryption show**:</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="d7e4c-143">O status agora deve relatar o disco do sistema operacional e o disco de dados como **Criptografado**.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-143">The status should now report both the OS disk and data disk as **Encrypted**.</span></span>

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="d7e4c-144">Visão geral da criptografia de disco</span><span class="sxs-lookup"><span data-stu-id="d7e4c-144">Overview of disk encryption</span></span>
<span data-ttu-id="d7e4c-145">Discos virtuais em VMs do Linux são criptografados em repouso usando [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span><span class="sxs-lookup"><span data-stu-id="d7e4c-145">Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span></span> <span data-ttu-id="d7e4c-146">Não há nenhuma taxa para criptografar discos virtuais no Azure.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-146">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="d7e4c-147">Chaves e criptográficas são armazenadas no Cofre de chaves do Azure usando a proteção de software ou você pode importar ou gerar as chaves em Módulos de segurança de Hardware (HSMs) certificados para padrões de nível 2 de FIPS 140-2.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-147">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified to FIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="d7e4c-148">Você mantém o controle dessas chaves criptográficas e pode auditar seu uso.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-148">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="d7e4c-149">Essas chaves criptográficas são usadas para criptografar e descriptografar os discos virtuais conectados à sua VM.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-149">These cryptographic keys are used to encrypt and decrypt virtual disks attached to your VM.</span></span> <span data-ttu-id="d7e4c-150">Uma entidade de serviço do Azure Active Directory fornece um mecanismo seguro para emitir essas chaves de criptografia, enquanto as VMs são ligadas e desligadas.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-150">An Azure Active Directory service principal provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="d7e4c-151">O processo de criptografia de uma VM é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="d7e4c-151">The process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="d7e4c-152">Crie uma chave de criptografia em um Cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-152">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="d7e4c-153">Configure a chave de criptografia a ser usada para criptografar discos.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-153">Configure the cryptographic key to be usable for encrypting disks.</span></span>
3. <span data-ttu-id="d7e4c-154">Para ler a chave de criptografia do Azure Key Vault, crie uma entidade de serviço do Azure Active Directory com as permissões apropriadas.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-154">To read the cryptographic key from the Azure Key Vault, create an Azure Active Directory service principal with the appropriate permissions.</span></span>
4. <span data-ttu-id="d7e4c-155">Execute o comando para criptografar seus discos virtuais, especificando a entidade de serviço do Azure Active Directory e a chave de criptografia apropriada a ser usada.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-155">Issue the command to encrypt your virtual disks, specifying the Azure Active Directory service principal and appropriate cryptographic key to be used.</span></span>
5. <span data-ttu-id="d7e4c-156">A entidade de serviço do Azure Active Directory solicita a chave de criptografia necessária do Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-156">The Azure Active Directory service principal requests the required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="d7e4c-157">Os discos virtuais são criptografados usando a chave de criptografia fornecida.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-157">The virtual disks are encrypted using the provided cryptographic key.</span></span>

## <a name="encryption-process"></a><span data-ttu-id="d7e4c-158">Processo de criptografia</span><span class="sxs-lookup"><span data-stu-id="d7e4c-158">Encryption process</span></span>
<span data-ttu-id="d7e4c-159">A criptografia de disco depende dos seguintes componentes adicionais:</span><span class="sxs-lookup"><span data-stu-id="d7e4c-159">Disk encryption relies on the following additional components:</span></span>

* <span data-ttu-id="d7e4c-160">**Cofre de Chaves do Azure** – usado para proteger chaves criptográficas e segredos usados para o processo de criptografia/descriptografia do disco.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-160">**Azure Key Vault** - used to safeguard cryptographic keys and secrets used for the disk encryption/decryption process.</span></span>
  * <span data-ttu-id="d7e4c-161">Se houver um, você pode usar um Cofre de Chaves do Azure existente.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-161">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="d7e4c-162">Não é necessário dedicar um Cofre de Chaves para criptografar discos.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-162">You do not have to dedicate a Key Vault to encrypting disks.</span></span>
  * <span data-ttu-id="d7e4c-163">Para separar os limites administrativos e visibilidade de chave, crie um Cofre de Chaves dedicado.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-163">To separate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="d7e4c-164">**Azure Active Directory** – realiza a troca segura de chaves criptográficas necessárias e a autenticação para ações solicitadas.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-164">**Azure Active Directory** - handles the secure exchanging of required cryptographic keys and authentication for requested actions.</span></span>
  * <span data-ttu-id="d7e4c-165">Normalmente, você pode usar uma instância existente do Azure Active Directory para hospedar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-165">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="d7e4c-166">A entidade de serviço fornece um mecanismo seguro para solicitar e receber as chaves de criptografia apropriadas.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-166">The service principal provides a secure mechanism to request and be issued the appropriate cryptographic keys.</span></span> <span data-ttu-id="d7e4c-167">Você não está desenvolvendo um aplicativo real que se integra ao Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-167">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="d7e4c-168">Requisitos e limitações</span><span class="sxs-lookup"><span data-stu-id="d7e4c-168">Requirements and limitations</span></span>
<span data-ttu-id="d7e4c-169">Requisitos e cenários com suporte para criptografia de disco:</span><span class="sxs-lookup"><span data-stu-id="d7e4c-169">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="d7e4c-170">Os seguintes SKUs de servidor Linux – Ubuntu, CentOS, SUSE e SLES (SUSE Linux Enterprise Server) e Red Hat Enterprise Linux.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-170">The following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.</span></span>
* <span data-ttu-id="d7e4c-171">Todos os recursos (por exemplo, Cofre de chaves, conta de Armazenamento e VM) devem pertencer à mesma assinatura e região do Azure.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-171">All resources (such as Key Vault, Storage account, and VM) must be in the same Azure region and subscription.</span></span>
* <span data-ttu-id="d7e4c-172">VMs Standard das séries A, D, DS, G e GS.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-172">Standard A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="d7e4c-173">A criptografia de disco não tem suporte atualmente nos seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="d7e4c-173">Disk encryption is not currently supported in the following scenarios:</span></span>

* <span data-ttu-id="d7e4c-174">VMs de camada básica.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-174">Basic tier VMs.</span></span>
* <span data-ttu-id="d7e4c-175">VMs criadas com o modelo de implantação Clássico.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-175">VMs created using the Classic deployment model.</span></span>
* <span data-ttu-id="d7e4c-176">Desabilitação da criptografia de disco do OS em VMs do Linux.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-176">Disabling OS disk encryption on Linux VMs.</span></span>
* <span data-ttu-id="d7e4c-177">Atualização das chaves de criptografia em uma VM Linux já está criptografado.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-177">Updating the cryptographic keys on an already encrypted Linux VM.</span></span>

## <a name="create-azure-key-vault-and-keys"></a><span data-ttu-id="d7e4c-178">Criar o Azure Key Vault e as chaves</span><span class="sxs-lookup"><span data-stu-id="d7e4c-178">Create Azure Key Vault and keys</span></span>
<span data-ttu-id="d7e4c-179">É preciso ter a [CLI 2.0 do Azure](/cli/azure/install-az-cli2) mais recente instalada e conectada a uma conta do Azure usando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="d7e4c-179">You need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="d7e4c-180">Nos exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-180">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="d7e4c-181">Os nomes de parâmetro de exemplo incluem *myResourceGroup*, *myKey* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-181">Example parameter names include *myResourceGroup*, *myKey*, and *myVM*.</span></span>

<span data-ttu-id="d7e4c-182">A primeira etapa é criar um Cofre de Chaves do Azure para armazenar as chaves criptográficas.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-182">The first step is to create an Azure Key Vault to store your cryptographic keys.</span></span> <span data-ttu-id="d7e4c-183">O Cofre de Chaves do Azure pode armazenar chaves, segredos ou senhas que permitem implementá-los de forma segura em seus aplicativos e serviços.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-183">Azure Key Vault can store keys, secrets, or passwords that allow you to securely implement them in your applications and services.</span></span> <span data-ttu-id="d7e4c-184">Para criptografia de disco virtual, use o Cofre de chaves para armazenar uma chave de criptografia que é usada para criptografar ou descriptografar seus discos virtuais.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-184">For virtual disk encryption, you use Key Vault to store a cryptographic key that is used to encrypt or decrypt your virtual disks.</span></span>

<span data-ttu-id="d7e4c-185">Habilite o provedor do Azure Key Vault dentro de sua assinatura do Azure com [az provider register](/cli/azure/provider#register) e crie um grupo de recursos com [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="d7e4c-185">Enable the Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="d7e4c-186">O exemplo a seguir cria um grupo de recursos chamado *myResourceGroup* no local `eastus`:</span><span class="sxs-lookup"><span data-stu-id="d7e4c-186">The following example creates a resource group name *myResourceGroup* in the `eastus` location:</span></span>

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="d7e4c-187">O Cofre de chaves do Azure que contém as chaves criptográficas e recursos de computação associados, como armazenamento e a própria VM deve residir na mesma região.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-187">The Azure Key Vault containing the cryptographic keys and associated compute resources such as storage and the VM itself must reside in the same region.</span></span> <span data-ttu-id="d7e4c-188">Crie um Azure Key Vault com [az keyvault create](/cli/azure/keyvault#create) e habilite o Key Vault para uso com criptografia de disco.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-188">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable the Key Vault for use with disk encryption.</span></span> <span data-ttu-id="d7e4c-189">Especifique um nome exclusivo de Key Vault para *keyvault_name* da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d7e4c-189">Specify a unique Key Vault name for *keyvault_name* as follows:</span></span>

```azurecli
keyvault_name=myUniqueKeyVaultName
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

<span data-ttu-id="d7e4c-190">É possível armazenar chaves de criptografia usando a proteção do Modelo de segurança de Hardware (HSM) ou software.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-190">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="d7e4c-191">Usar um HSM requer um Cofre de Chaves premium.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-191">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="d7e4c-192">Há um custo adicional para a criação de um Cofre de Chaves premium em vez do Cofre de Chaves padrão que armazena as chaves protegidas por software.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-192">There is an additional cost to creating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="d7e4c-193">Para criar um Cofre de Chaves premium, na etapa anterior, adicione `--sku Premium` ao comando.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-193">To create a premium Key Vault, in the preceding step add `--sku Premium` to the command.</span></span> <span data-ttu-id="d7e4c-194">O exemplo a seguir usa chaves protegidas por software, desde que criamos um Cofre de Chaves padrão.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-194">The following example uses software-protected keys since we created a standard Key Vault.</span></span>

<span data-ttu-id="d7e4c-195">Para ambos os modelos de proteção, a plataforma do Azure deve ter acesso para solicitar as chaves criptográficas quando a VM é inicializada para descriptografar os discos virtuais.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-195">For both protection models, the Azure platform needs to be granted access to request the cryptographic keys when the VM boots to decrypt the virtual disks.</span></span> <span data-ttu-id="d7e4c-196">Criar uma chave de criptografia em seu Key Vault com [az keyvault key create](/cli/azure/keyvault/key#create).</span><span class="sxs-lookup"><span data-stu-id="d7e4c-196">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span></span> <span data-ttu-id="d7e4c-197">O exemplo a seguir cria uma chave chamada *myKey*:</span><span class="sxs-lookup"><span data-stu-id="d7e4c-197">The following example creates a key named *myKey*:</span></span>

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```


## <a name="create-the-azure-active-directory-service-principal"></a><span data-ttu-id="d7e4c-198">Criar a entidade de serviço do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d7e4c-198">Create the Azure Active Directory service principal</span></span>
<span data-ttu-id="d7e4c-199">Quando os discos virtuais são criptografados ou descriptografados, especifique uma conta para lidar com a autenticação e a troca de chaves de criptografia do Key Vault.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-199">When virtual disks are encrypted or decrypted, you specify an account to handle the authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="d7e4c-200">Essa conta, uma entidade de serviço do Azure Active Directory, permite que a plataforma do Azure solicite as chaves de criptografia apropriadas em nome da VM.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-200">This account, an Azure Active Directory service principal, allows the Azure platform to request the appropriate cryptographic keys on behalf of the VM.</span></span> <span data-ttu-id="d7e4c-201">Uma instância do Azure Active Directory padrão está disponível em sua assinatura, embora muitas organizações tenham diretórios do Azure Active Directory dedicados.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-201">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="d7e4c-202">Crie uma entidade de serviço usando o Azure Active Directory com [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span><span class="sxs-lookup"><span data-stu-id="d7e4c-202">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span></span> <span data-ttu-id="d7e4c-203">O exemplo a seguir lê os valores da ID e senha da entidade de serviço para uso em comandos posteriores:</span><span class="sxs-lookup"><span data-stu-id="d7e4c-203">The following example reads in the values for the service principal Id and password for use in later commands:</span></span>

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

<span data-ttu-id="d7e4c-204">A senha só será exibida quando você criar a entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-204">The password is only displayed when you create the service principal.</span></span> <span data-ttu-id="d7e4c-205">Se desejar, exiba e grave a senha (`echo $sp_password`).</span><span class="sxs-lookup"><span data-stu-id="d7e4c-205">If desired, view and record the password (`echo $sp_password`).</span></span> <span data-ttu-id="d7e4c-206">Você pode listar suas entidades de serviço com [az ad sp list](/cli/azure/ad/sp#list) e exibir informações adicionais sobre uma entidade de serviço específica com [az ad sp show](/cli/azure/ad/sp#show).</span><span class="sxs-lookup"><span data-stu-id="d7e4c-206">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span></span>

<span data-ttu-id="d7e4c-207">Para criptografar ou descriptografar discos virtuais com êxito, as permissões na chave de criptografia armazenada no Key Vault devem ser definidas para permitir que a entidade de serviço do Azure Active Directory leia as chaves.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-207">To successfully encrypt or decrypt virtual disks, permissions on the cryptographic key stored in Key Vault must be set to permit the Azure Active Directory service principal to read the keys.</span></span> <span data-ttu-id="d7e4c-208">Defina permissões em seu Key Vault com [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span><span class="sxs-lookup"><span data-stu-id="d7e4c-208">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span></span> <span data-ttu-id="d7e4c-209">No exemplo a seguir, a ID da entidade de serviço é fornecida por meio do comando anterior:</span><span class="sxs-lookup"><span data-stu-id="d7e4c-209">In the following example, the service principal ID is supplied from the preceding command:</span></span>

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
  --key-permissions wrapKey \
  --secret-permissions set
```


## <a name="create-virtual-machine"></a><span data-ttu-id="d7e4c-210">Criar máquina virtual</span><span class="sxs-lookup"><span data-stu-id="d7e4c-210">Create virtual machine</span></span>
<span data-ttu-id="d7e4c-211">Para criptografar alguns discos virtuais, vamos criar uma VM e adicionar um disco de dados.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-211">To actually encrypt some virtual disks, lets create a VM and add a data disk.</span></span> <span data-ttu-id="d7e4c-212">Crie uma VM para criptografar com [az vm create](/cli/azure/vm#create) e anexe um disco de dados de 5 GB.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-212">Create a VM to encrypt with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span></span> <span data-ttu-id="d7e4c-213">Somente determinadas imagens do marketplace dão suporte à criptografia de disco.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-213">Only certain marketplace images support disk encryption.</span></span> <span data-ttu-id="d7e4c-214">O exemplo a seguir cria uma VM chamada *myVM* usando uma imagem do **CentOS 7.2n**:</span><span class="sxs-lookup"><span data-stu-id="d7e4c-214">The following example creates a VM named *myVM* using a **CentOS 7.2n** image:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

<span data-ttu-id="d7e4c-215">SSH para a VM usando o `publicIpAddress` mostrado na saída do comando anterior.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-215">SSH to your VM using the `publicIpAddress` shown in the output of the preceding command.</span></span> <span data-ttu-id="d7e4c-216">Crie uma partição e o sistema de arquivos e, em seguida, monte o disco de dados.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-216">Create a partition and filesystem, then mount the data disk.</span></span> <span data-ttu-id="d7e4c-217">Para obter mais informações, consulte [Conectar-se a uma VM Linux para montar o novo disco](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="d7e4c-217">For more information, see [Connect to a Linux VM to mount the new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> <span data-ttu-id="d7e4c-218">Feche a sessão SSH.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-218">Close your SSH session.</span></span>


## <a name="encrypt-virtual-machine"></a><span data-ttu-id="d7e4c-219">Criptografar máquina virtual</span><span class="sxs-lookup"><span data-stu-id="d7e4c-219">Encrypt virtual machine</span></span>
<span data-ttu-id="d7e4c-220">Para criptografar os discos virtuais, reúna todos os componentes anteriores:</span><span class="sxs-lookup"><span data-stu-id="d7e4c-220">To encrypt the virtual disks, you bring together all the previous components:</span></span>

1. <span data-ttu-id="d7e4c-221">Especifique a entidade de serviço e senha do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-221">Specify the Azure Active Directory service principal and password.</span></span>
2. <span data-ttu-id="d7e4c-222">Especifique o Cofre de chaves para armazenar os metadados para os discos criptografados.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-222">Specify the Key Vault to store the metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="d7e4c-223">Especifique as chaves de criptografia a serem usadas para criptografia e descriptografia.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-223">Specify the cryptographic keys to use for the actual encryption and decryption.</span></span>
4. <span data-ttu-id="d7e4c-224">Especifique se deseja criptografar o disco do sistema operacional, os discos de dados ou todos.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-224">Specify whether you want to encrypt the OS disk, the data disks, or all.</span></span>

<span data-ttu-id="d7e4c-225">Criptografe sua VM com [az vm encryption enable](/cli/azure/vm/encryption#enable).</span><span class="sxs-lookup"><span data-stu-id="d7e4c-225">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span></span> <span data-ttu-id="d7e4c-226">O exemplo a seguir usa as variáveis `$sp_id` e `$sp_password` do comando `ad sp create-for-rbac` anterior:</span><span class="sxs-lookup"><span data-stu-id="d7e4c-226">The following example uses the `$sp_id` and `$sp_password` variables from the preceding `ad sp create-for-rbac` command:</span></span>

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

<span data-ttu-id="d7e4c-227">Leva algum tempo para o processo de criptografia de disco ser concluído.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-227">It takes some time for the disk encryption process to complete.</span></span> <span data-ttu-id="d7e4c-228">Monitorar o status do processo com [az vm encryption show](/cli/azure/vm/encryption#show):</span><span class="sxs-lookup"><span data-stu-id="d7e4c-228">Monitor the status of the process with [az vm encryption show](/cli/azure/vm/encryption#show):</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="d7e4c-229">A saída deverá ser semelhante ao seguinte exemplo truncado:</span><span class="sxs-lookup"><span data-stu-id="d7e4c-229">The output is similar to the following truncated example:</span></span>

```json
[
  "dataDisk": "EncryptionInProgress",
  "osDisk": "EncryptionInProgress",
]
```

<span data-ttu-id="d7e4c-230">Aguarde até que o status para o sistema operacional disco relate **VMRestartPending**, então reinicie a VM com [az vm restart](/cli/azure/vm#restart):</span><span class="sxs-lookup"><span data-stu-id="d7e4c-230">Wait until the status for the OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="d7e4c-231">O processo de criptografia de disco é finalizado durante o processo de inicialização, portanto, aguarde alguns minutos antes de verificar o status de criptografia novamente com **az vm encryption show**:</span><span class="sxs-lookup"><span data-stu-id="d7e4c-231">The disk encryption process is finalized during the boot process, so wait a few minutes before checking the status of encryption again with **az vm encryption show**:</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="d7e4c-232">O status agora deve relatar o disco do sistema operacional e o disco de dados como **Criptografado**.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-232">The status should now report both the OS disk and data disk as **Encrypted**.</span></span>


## <a name="add-additional-data-disks"></a><span data-ttu-id="d7e4c-233">Adicionar discos de dados adicionais</span><span class="sxs-lookup"><span data-stu-id="d7e4c-233">Add additional data disks</span></span>
<span data-ttu-id="d7e4c-234">Depois de criptografar seus discos de dados, é possível adicionar discos virtuais à sua VM e criptografá-los também.</span><span class="sxs-lookup"><span data-stu-id="d7e4c-234">Once you have encrypted your data disks, you can later add additional virtual disks to your VM and also encrypt them.</span></span> <span data-ttu-id="d7e4c-235">Por exemplo, permite adicionar um segundo disco virtual à VM da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d7e4c-235">For example, lets add a second virtual disk to your VM as follows:</span></span>

```azurecli
az vm disk attach-new --resource-group myResourceGroup --vm-name myVM --size-in-gb 5
```

<span data-ttu-id="d7e4c-236">Execute novamente o comando para criptografar os discos virtuais como se segue:</span><span class="sxs-lookup"><span data-stu-id="d7e4c-236">Re-run the command to encrypt the virtual disks as follows:</span></span>

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```


## <a name="next-steps"></a><span data-ttu-id="d7e4c-237">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d7e4c-237">Next steps</span></span>
* <span data-ttu-id="d7e4c-238">Para obter mais informações sobre como gerenciar o Cofre de Chaves do Azure, incluindo a exclusão de chaves criptográficas e cofres, consulte [Gerenciar Cofres de Chaves usando a CLI](../../key-vault/key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="d7e4c-238">For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md).</span></span>
* <span data-ttu-id="d7e4c-239">Para obter mais informações sobre criptografia de disco, como preparar uma VM personalizada criptografada para carregar no Azure, consulte [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="d7e4c-239">For more information about disk encryption, such as preparing an encrypted custom VM to upload to Azure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
