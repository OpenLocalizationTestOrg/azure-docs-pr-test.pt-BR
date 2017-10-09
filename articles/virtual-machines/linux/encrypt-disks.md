---
title: aaaEncrypt discos em uma VM do Linux no Azure | Microsoft Docs
description: "Como tooencrypt de discos virtuais em uma VM Linux para segurança aprimorada usando Olá 2.0 do CLI do Azure"
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
ms.openlocfilehash: d6197742bc8562630e8395588c072093fc01d614
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencrypt-virtual-disks-on-a-linux-vm"></a><span data-ttu-id="8ae6b-103">Como tooencrypt de discos virtuais em uma VM do Linux</span><span class="sxs-lookup"><span data-stu-id="8ae6b-103">How tooencrypt virtual disks on a Linux VM</span></span>
<span data-ttu-id="8ae6b-104">Para conformidade e segurança aprimorados da VM (máquina virtual), os discos virtuais no Azure podem ser criptografados.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted.</span></span> <span data-ttu-id="8ae6b-105">Discos são criptografados usando chaves criptográficas que são protegidas em um Cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="8ae6b-106">Você controla essas chaves criptográficas e pode auditar seu uso.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="8ae6b-107">Este artigo fornece detalhes sobre como tooencrypt de discos virtuais em uma VM do Linux usando Olá 2.0 do CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-107">This article details how tooencrypt virtual disks on a Linux VM using hello Azure CLI 2.0.</span></span> <span data-ttu-id="8ae6b-108">Você também pode executar essas etapas com hello [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8ae6b-108">You can also perform these steps with hello [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="8ae6b-109">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="8ae6b-109">Quick commands</span></span>
<span data-ttu-id="8ae6b-110">Se você precisar tooquickly realizar tarefa hello, Olá Olá de detalhes da seção base a seguir comandos tooencrypt de discos virtuais na sua VM.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-110">If you need tooquickly accomplish hello task, hello following section details hello base commands tooencrypt virtual disks on your VM.</span></span> <span data-ttu-id="8ae6b-111">Obter mais informações e o contexto para cada etapa pode ser encontrada restante de saudação do documento hello, [Iniciar aqui](#overview-of-disk-encryption).</span><span class="sxs-lookup"><span data-stu-id="8ae6b-111">More detailed information and context for each step can be found hello rest of hello document, [starting here](#overview-of-disk-encryption).</span></span>

<span data-ttu-id="8ae6b-112">Você precisa hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e conectado através de conta do Azure tooan [logon az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="8ae6b-112">You need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="8ae6b-113">Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-113">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="8ae6b-114">Os nomes de parâmetro de exemplo incluem *myResourceGroup*, *myKey* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-114">Example parameter names include *myResourceGroup*, *myKey*, and *myVM*.</span></span>

<span data-ttu-id="8ae6b-115">Primeiro, habilite o provedor do Azure Key Vault hello dentro de sua assinatura do Azure com [registro de provedor az](/cli/azure/provider#register) e criar um grupo de recursos com [criar grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="8ae6b-115">First, enable hello Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="8ae6b-116">Olá, exemplo a seguir cria um nome de grupo de recursos *myResourceGroup* em Olá *eastus* local:</span><span class="sxs-lookup"><span data-stu-id="8ae6b-116">hello following example creates a resource group name *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="8ae6b-117">Criar um cofre de chaves do Azure com [keyvault az criar](/cli/azure/keyvault#create) e habilitar Olá Cofre de chaves para uso com criptografia de disco.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-117">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable hello Key Vault for use with disk encryption.</span></span> <span data-ttu-id="8ae6b-118">Especifique um nome exclusivo de Key Vault para *keyvault_name* da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="8ae6b-118">Specify a unique Key Vault name for *keyvault_name* as follows:</span></span>

```azurecli
keyvault_name=mykeyvaultikf
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

<span data-ttu-id="8ae6b-119">Criar uma chave de criptografia em seu Key Vault com [az keyvault key create](/cli/azure/keyvault/key#create).</span><span class="sxs-lookup"><span data-stu-id="8ae6b-119">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span></span> <span data-ttu-id="8ae6b-120">Olá, exemplo a seguir cria uma chave chamada *myKey*:</span><span class="sxs-lookup"><span data-stu-id="8ae6b-120">hello following example creates a key named *myKey*:</span></span>

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```

<span data-ttu-id="8ae6b-121">Crie uma entidade de serviço usando o Azure Active Directory com [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span><span class="sxs-lookup"><span data-stu-id="8ae6b-121">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span></span> <span data-ttu-id="8ae6b-122">identificadores de entidade de serviço Olá Olá autenticação e troca de chaves de criptografia do Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-122">hello service principal handles hello authentication and exchange of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="8ae6b-123">saudação de exemplo a seguir lê valores Olá Olá entidade de serviço Id e a senha para uso em comandos posteriores:</span><span class="sxs-lookup"><span data-stu-id="8ae6b-123">hello following example reads in hello values for hello service principal Id and password for use in later commands:</span></span>

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

<span data-ttu-id="8ae6b-124">senha Olá é somente de saída quando você cria Olá entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-124">hello password is only output when you create hello service principal.</span></span> <span data-ttu-id="8ae6b-125">Se desejar, exibir e registro Olá senha (`echo $sp_password`).</span><span class="sxs-lookup"><span data-stu-id="8ae6b-125">If desired, view and record hello password (`echo $sp_password`).</span></span> <span data-ttu-id="8ae6b-126">Você pode listar suas entidades de serviço com [az ad sp list](/cli/azure/ad/sp#list) e exibir informações adicionais sobre uma entidade de serviço específica com [az ad sp show](/cli/azure/ad/sp#show).</span><span class="sxs-lookup"><span data-stu-id="8ae6b-126">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span></span>

<span data-ttu-id="8ae6b-127">Defina permissões em seu Key Vault com [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span><span class="sxs-lookup"><span data-stu-id="8ae6b-127">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span></span> <span data-ttu-id="8ae6b-128">Olá exemplo a seguir, hello ID de entidade de serviço é fornecido de saudação que precedem o comando:</span><span class="sxs-lookup"><span data-stu-id="8ae6b-128">In hello following example, hello service principal ID is supplied from hello preceding command:</span></span>

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
    --key-permissions wrapKey \
    --secret-permissions set
```

<span data-ttu-id="8ae6b-129">Crie uma VM com [az vm create](/cli/azure/vm#create) e anexe um disco de dados de 5 GB.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-129">Create a VM with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span></span> <span data-ttu-id="8ae6b-130">Somente determinadas imagens do marketplace dão suporte à criptografia de disco.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-130">Only certain marketplace images support disk encryption.</span></span> <span data-ttu-id="8ae6b-131">Olá, exemplo a seguir cria uma VM denominada `myVM` usando um **CentOS 7.2n** imagem:</span><span class="sxs-lookup"><span data-stu-id="8ae6b-131">hello following example creates a VM named `myVM` using a **CentOS 7.2n** image:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

<span data-ttu-id="8ae6b-132">SSH tooyour VM usando Olá `publicIpAddress` mostrado na saída Olá Olá precede o comando.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-132">SSH tooyour VM using hello `publicIpAddress` shown in hello output of hello preceding command.</span></span> <span data-ttu-id="8ae6b-133">Criar uma partição e sistema de arquivos, em seguida, montar o disco de dados hello.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-133">Create a partition and filesystem, then mount hello data disk.</span></span> <span data-ttu-id="8ae6b-134">Para obter mais informações, consulte [conectar tooa novo disco de VM do Linux toomount Olá](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="8ae6b-134">For more information, see [Connect tooa Linux VM toomount hello new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> <span data-ttu-id="8ae6b-135">Feche a sessão SSH.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-135">Close your SSH session.</span></span>

<span data-ttu-id="8ae6b-136">Criptografe sua VM com [az vm encryption enable](/cli/azure/vm/encryption#enable).</span><span class="sxs-lookup"><span data-stu-id="8ae6b-136">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span></span> <span data-ttu-id="8ae6b-137">Olá, exemplo a seguir usa Olá `$sp_id` e `$sp_password` variáveis de saudação anterior `ad sp create-for-rbac` comando:</span><span class="sxs-lookup"><span data-stu-id="8ae6b-137">hello following example uses hello `$sp_id` and `$sp_password` variables from hello preceding `ad sp create-for-rbac` command:</span></span>

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

<span data-ttu-id="8ae6b-138">Levará algum tempo para Olá toocomplete de processo de criptografia de disco.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-138">It takes some time for hello disk encryption process toocomplete.</span></span> <span data-ttu-id="8ae6b-139">Monitorar o status de saudação do processo de saudação com [Mostrar de criptografia de vm az](/cli/azure/vm/encryption#show):</span><span class="sxs-lookup"><span data-stu-id="8ae6b-139">Monitor hello status of hello process with [az vm encryption show](/cli/azure/vm/encryption#show):</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="8ae6b-140">Olá status mostra **EncryptionInProgress**.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-140">hello status shows **EncryptionInProgress**.</span></span> <span data-ttu-id="8ae6b-141">Aguarde até que o status de Olá Olá OS relatórios de disco **VMRestartPending**, em seguida, reiniciar a VM com [reinicialização de vm az](/cli/azure/vm#restart):</span><span class="sxs-lookup"><span data-stu-id="8ae6b-141">Wait until hello status for hello OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="8ae6b-142">Olá processo de criptografia de disco é finalizado durante o processo de inicialização hello, então, aguarde alguns minutos antes de verificar o status de saudação do encryption novamente com **Mostrar de criptografia de vm az**:</span><span class="sxs-lookup"><span data-stu-id="8ae6b-142">hello disk encryption process is finalized during hello boot process, so wait a few minutes before checking hello status of encryption again with **az vm encryption show**:</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="8ae6b-143">status de saudação agora devem relatar disco Olá SO e discos de dados como **criptografado**.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-143">hello status should now report both hello OS disk and data disk as **Encrypted**.</span></span>

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="8ae6b-144">Visão geral da criptografia de disco</span><span class="sxs-lookup"><span data-stu-id="8ae6b-144">Overview of disk encryption</span></span>
<span data-ttu-id="8ae6b-145">Discos virtuais em VMs do Linux são criptografados em repouso usando [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span><span class="sxs-lookup"><span data-stu-id="8ae6b-145">Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span></span> <span data-ttu-id="8ae6b-146">Não há nenhuma taxa para criptografar discos virtuais no Azure.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-146">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="8ae6b-147">As chaves de criptografia são armazenadas no cofre de chaves do Azure usando a proteção de software, ou você pode importar ou gerar as chaves em módulos de segurança de Hardware (HSM) certificada tooFIPS padrões do 140-2 nível 2.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-147">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified tooFIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="8ae6b-148">Você mantém o controle dessas chaves criptográficas e pode auditar seu uso.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-148">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="8ae6b-149">Essas chaves de criptografia são usada tooencrypt e descriptografar os discos virtuais anexados tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-149">These cryptographic keys are used tooencrypt and decrypt virtual disks attached tooyour VM.</span></span> <span data-ttu-id="8ae6b-150">Uma entidade de serviço do Azure Active Directory fornece um mecanismo seguro para emitir essas chaves de criptografia, enquanto as VMs são ligadas e desligadas.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-150">An Azure Active Directory service principal provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="8ae6b-151">processo de saudação de criptografia de uma VM é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="8ae6b-151">hello process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="8ae6b-152">Crie uma chave de criptografia em um Cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-152">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="8ae6b-153">Configure Olá criptográfico chave toobe pode ser usado para criptografia de discos.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-153">Configure hello cryptographic key toobe usable for encrypting disks.</span></span>
3. <span data-ttu-id="8ae6b-154">chave de criptografia de saudação tooread de saudação Cofre de chaves do Azure, criar um serviço do Active Directory do Azure principal com as permissões adequadas hello.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-154">tooread hello cryptographic key from hello Azure Key Vault, create an Azure Active Directory service principal with hello appropriate permissions.</span></span>
4. <span data-ttu-id="8ae6b-155">Emita Olá comando tooencrypt seus discos virtuais, especificação de entidade de serviço do Active Directory do Azure hello e adequado toobe chave criptográfica usada.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-155">Issue hello command tooencrypt your virtual disks, specifying hello Azure Active Directory service principal and appropriate cryptographic key toobe used.</span></span>
5. <span data-ttu-id="8ae6b-156">solicitações do principais de serviço do Active Directory do Azure Olá Olá chave de criptografia necessária do Cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-156">hello Azure Active Directory service principal requests hello required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="8ae6b-157">discos virtuais Olá são criptografados usando a chave criptográfica Olá fornecido.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-157">hello virtual disks are encrypted using hello provided cryptographic key.</span></span>

## <a name="encryption-process"></a><span data-ttu-id="8ae6b-158">Processo de criptografia</span><span class="sxs-lookup"><span data-stu-id="8ae6b-158">Encryption process</span></span>
<span data-ttu-id="8ae6b-159">Criptografia de disco se baseia em Olá componentes adicionais a seguir:</span><span class="sxs-lookup"><span data-stu-id="8ae6b-159">Disk encryption relies on hello following additional components:</span></span>

* <span data-ttu-id="8ae6b-160">**Cofre de chaves do Azure** -usado toosafeguard as chaves de criptografia e segredos usados no processo de criptografia/descriptografia de disco hello.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-160">**Azure Key Vault** - used toosafeguard cryptographic keys and secrets used for hello disk encryption/decryption process.</span></span>
  * <span data-ttu-id="8ae6b-161">Se houver um, você pode usar um Cofre de Chaves do Azure existente.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-161">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="8ae6b-162">Você não tem toodedicate discos tooencrypting um cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-162">You do not have toodedicate a Key Vault tooencrypting disks.</span></span>
  * <span data-ttu-id="8ae6b-163">limites administrativos tooseparate e visibilidade de chave, você pode criar um cofre de chaves dedicado.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-163">tooseparate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="8ae6b-164">**Active Directory do Azure** - identificadores Olá troca segura de chaves de criptografia necessárias e autenticação para ações de solicitada.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-164">**Azure Active Directory** - handles hello secure exchanging of required cryptographic keys and authentication for requested actions.</span></span>
  * <span data-ttu-id="8ae6b-165">Normalmente, você pode usar uma instância existente do Azure Active Directory para hospedar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-165">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="8ae6b-166">entidade de serviço Olá fornece um mecanismo seguro toorequest e emitido chaves de criptografia apropriadas hello.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-166">hello service principal provides a secure mechanism toorequest and be issued hello appropriate cryptographic keys.</span></span> <span data-ttu-id="8ae6b-167">Você não está desenvolvendo um aplicativo real que se integra ao Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-167">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="8ae6b-168">Requisitos e limitações</span><span class="sxs-lookup"><span data-stu-id="8ae6b-168">Requirements and limitations</span></span>
<span data-ttu-id="8ae6b-169">Requisitos e cenários com suporte para criptografia de disco:</span><span class="sxs-lookup"><span data-stu-id="8ae6b-169">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="8ae6b-170">saudação do servidor Linux SKUs - Red Hat Enterprise Linux, CentOS, SUSE e SUSE Linux Enterprise Server (SLES) e Ubuntu a seguir.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-170">hello following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.</span></span>
* <span data-ttu-id="8ae6b-171">Todos os recursos (como o Cofre de chaves, a conta de armazenamento e VM) devem estar no hello mesma região do Azure e assinatura.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-171">All resources (such as Key Vault, Storage account, and VM) must be in hello same Azure region and subscription.</span></span>
* <span data-ttu-id="8ae6b-172">VMs Standard das séries A, D, DS, G e GS.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-172">Standard A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="8ae6b-173">Criptografia de disco não é suportada em Olá os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="8ae6b-173">Disk encryption is not currently supported in hello following scenarios:</span></span>

* <span data-ttu-id="8ae6b-174">VMs de camada básica.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-174">Basic tier VMs.</span></span>
* <span data-ttu-id="8ae6b-175">Máquinas virtuais criadas usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-175">VMs created using hello Classic deployment model.</span></span>
* <span data-ttu-id="8ae6b-176">Desabilitação da criptografia de disco do OS em VMs do Linux.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-176">Disabling OS disk encryption on Linux VMs.</span></span>
* <span data-ttu-id="8ae6b-177">Atualizando chaves de criptografia de saudação em uma VM Linux já criptografados.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-177">Updating hello cryptographic keys on an already encrypted Linux VM.</span></span>

## <a name="create-azure-key-vault-and-keys"></a><span data-ttu-id="8ae6b-178">Criar o Azure Key Vault e as chaves</span><span class="sxs-lookup"><span data-stu-id="8ae6b-178">Create Azure Key Vault and keys</span></span>
<span data-ttu-id="8ae6b-179">Você precisa hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e conectado através de conta do Azure tooan [logon az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="8ae6b-179">You need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="8ae6b-180">Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-180">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="8ae6b-181">Os nomes de parâmetro de exemplo incluem *myResourceGroup*, *myKey* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-181">Example parameter names include *myResourceGroup*, *myKey*, and *myVM*.</span></span>

<span data-ttu-id="8ae6b-182">primeira etapa de saudação é toocreate toostore um cofre de chaves do Azure as chaves criptográficas.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-182">hello first step is toocreate an Azure Key Vault toostore your cryptographic keys.</span></span> <span data-ttu-id="8ae6b-183">Cofre de chaves do Azure pode armazenar segredos, chaves ou senhas que permitem que você toosecurely implementação-las em seus aplicativos e serviços.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-183">Azure Key Vault can store keys, secrets, or passwords that allow you toosecurely implement them in your applications and services.</span></span> <span data-ttu-id="8ae6b-184">Para criptografia de disco virtual, use o Cofre de chaves toostore uma chave criptográfica que é usada tooencrypt ou descriptografar os discos virtuais.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-184">For virtual disk encryption, you use Key Vault toostore a cryptographic key that is used tooencrypt or decrypt your virtual disks.</span></span>

<span data-ttu-id="8ae6b-185">Habilitar provedor de Azure Key Vault hello dentro de sua assinatura do Azure com [registro de provedor az](/cli/azure/provider#register) e criar um grupo de recursos com [criar grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="8ae6b-185">Enable hello Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="8ae6b-186">Olá, exemplo a seguir cria um nome de grupo de recursos *myResourceGroup* em Olá `eastus` local:</span><span class="sxs-lookup"><span data-stu-id="8ae6b-186">hello following example creates a resource group name *myResourceGroup* in hello `eastus` location:</span></span>

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="8ae6b-187">Hello Azure Key Vault contendo Olá chaves criptográficas e computação associada recursos, como armazenamento e hello própria máquina virtual devem residir no hello mesma região.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-187">hello Azure Key Vault containing hello cryptographic keys and associated compute resources such as storage and hello VM itself must reside in hello same region.</span></span> <span data-ttu-id="8ae6b-188">Criar um cofre de chaves do Azure com [keyvault az criar](/cli/azure/keyvault#create) e habilitar Olá Cofre de chaves para uso com criptografia de disco.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-188">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable hello Key Vault for use with disk encryption.</span></span> <span data-ttu-id="8ae6b-189">Especifique um nome exclusivo de Key Vault para *keyvault_name* da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="8ae6b-189">Specify a unique Key Vault name for *keyvault_name* as follows:</span></span>

```azurecli
keyvault_name=myUniqueKeyVaultName
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

<span data-ttu-id="8ae6b-190">É possível armazenar chaves de criptografia usando a proteção do Modelo de segurança de Hardware (HSM) ou software.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-190">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="8ae6b-191">Usar um HSM requer um Cofre de Chaves premium.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-191">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="8ae6b-192">Há um custo adicional toocreating um premium Cofre de chaves em vez de Cofre de chave padrão que armazena as chaves protegidas por software.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-192">There is an additional cost toocreating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="8ae6b-193">toocreate adicionar um cofre de chaves, premium em Olá anterior etapa `--sku Premium` toohello comando.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-193">toocreate a premium Key Vault, in hello preceding step add `--sku Premium` toohello command.</span></span> <span data-ttu-id="8ae6b-194">Olá exemplo a seguir usa chaves protegidas por software pois criamos um cofre de chaves padrão.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-194">hello following example uses software-protected keys since we created a standard Key Vault.</span></span>

<span data-ttu-id="8ae6b-195">Para ambos os modelos de proteção, Olá plataforma Windows Azure precisa toobe concedida chaves de criptografia de saudação do acesso toorequest quando Olá VM inicializa os discos virtuais toodecrypt hello.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-195">For both protection models, hello Azure platform needs toobe granted access toorequest hello cryptographic keys when hello VM boots toodecrypt hello virtual disks.</span></span> <span data-ttu-id="8ae6b-196">Criar uma chave de criptografia em seu Key Vault com [az keyvault key create](/cli/azure/keyvault/key#create).</span><span class="sxs-lookup"><span data-stu-id="8ae6b-196">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span></span> <span data-ttu-id="8ae6b-197">Olá, exemplo a seguir cria uma chave chamada *myKey*:</span><span class="sxs-lookup"><span data-stu-id="8ae6b-197">hello following example creates a key named *myKey*:</span></span>

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```


## <a name="create-hello-azure-active-directory-service-principal"></a><span data-ttu-id="8ae6b-198">Criar hello entidade de serviço do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="8ae6b-198">Create hello Azure Active Directory service principal</span></span>
<span data-ttu-id="8ae6b-199">Quando discos virtuais são criptografados ou descriptografados, especifique um conta toohandle Olá de autenticação e troca de chaves de criptografia do Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-199">When virtual disks are encrypted or decrypted, you specify an account toohandle hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="8ae6b-200">Essa conta, uma entidade de serviço do Active Directory do Azure, permite Olá plataforma Windows Azure toorequest chaves de criptografia apropriado Olá em nome hello VM.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-200">This account, an Azure Active Directory service principal, allows hello Azure platform toorequest hello appropriate cryptographic keys on behalf of hello VM.</span></span> <span data-ttu-id="8ae6b-201">Uma instância do Azure Active Directory padrão está disponível em sua assinatura, embora muitas organizações tenham diretórios do Azure Active Directory dedicados.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-201">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="8ae6b-202">Crie uma entidade de serviço usando o Azure Active Directory com [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span><span class="sxs-lookup"><span data-stu-id="8ae6b-202">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span></span> <span data-ttu-id="8ae6b-203">saudação de exemplo a seguir lê valores Olá Olá entidade de serviço Id e a senha para uso em comandos posteriores:</span><span class="sxs-lookup"><span data-stu-id="8ae6b-203">hello following example reads in hello values for hello service principal Id and password for use in later commands:</span></span>

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

<span data-ttu-id="8ae6b-204">senha de saudação é exibida apenas quando você cria hello entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-204">hello password is only displayed when you create hello service principal.</span></span> <span data-ttu-id="8ae6b-205">Se desejar, exibir e registro Olá senha (`echo $sp_password`).</span><span class="sxs-lookup"><span data-stu-id="8ae6b-205">If desired, view and record hello password (`echo $sp_password`).</span></span> <span data-ttu-id="8ae6b-206">Você pode listar suas entidades de serviço com [az ad sp list](/cli/azure/ad/sp#list) e exibir informações adicionais sobre uma entidade de serviço específica com [az ad sp show](/cli/azure/ad/sp#show).</span><span class="sxs-lookup"><span data-stu-id="8ae6b-206">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span></span>

<span data-ttu-id="8ae6b-207">toosuccessfully criptografar ou descriptografar discos virtuais, as permissões na chave de criptografia Olá armazenadas no cofre de chaves devem ser conjunto toopermit hello Azure Active Directory tooread principal Olá as chaves de serviço.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-207">toosuccessfully encrypt or decrypt virtual disks, permissions on hello cryptographic key stored in Key Vault must be set toopermit hello Azure Active Directory service principal tooread hello keys.</span></span> <span data-ttu-id="8ae6b-208">Defina permissões em seu Key Vault com [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span><span class="sxs-lookup"><span data-stu-id="8ae6b-208">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span></span> <span data-ttu-id="8ae6b-209">Olá exemplo a seguir, hello ID de entidade de serviço é fornecido de saudação que precedem o comando:</span><span class="sxs-lookup"><span data-stu-id="8ae6b-209">In hello following example, hello service principal ID is supplied from hello preceding command:</span></span>

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
  --key-permissions wrapKey \
  --secret-permissions set
```


## <a name="create-virtual-machine"></a><span data-ttu-id="8ae6b-210">Criar máquina virtual</span><span class="sxs-lookup"><span data-stu-id="8ae6b-210">Create virtual machine</span></span>
<span data-ttu-id="8ae6b-211">tooactually criptografar alguns discos virtuais, permite criar uma máquina virtual e adicionar um disco de dados.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-211">tooactually encrypt some virtual disks, lets create a VM and add a data disk.</span></span> <span data-ttu-id="8ae6b-212">Criar um tooencrypt VM com [criar vm az](/cli/azure/vm#create) e anexar um disco de dados de 5 Gb.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-212">Create a VM tooencrypt with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span></span> <span data-ttu-id="8ae6b-213">Somente determinadas imagens do marketplace dão suporte à criptografia de disco.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-213">Only certain marketplace images support disk encryption.</span></span> <span data-ttu-id="8ae6b-214">Olá, exemplo a seguir cria uma VM denominada *myVM* usando um **CentOS 7.2n** imagem:</span><span class="sxs-lookup"><span data-stu-id="8ae6b-214">hello following example creates a VM named *myVM* using a **CentOS 7.2n** image:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

<span data-ttu-id="8ae6b-215">SSH tooyour VM usando Olá `publicIpAddress` mostrado na saída Olá Olá precede o comando.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-215">SSH tooyour VM using hello `publicIpAddress` shown in hello output of hello preceding command.</span></span> <span data-ttu-id="8ae6b-216">Criar uma partição e sistema de arquivos, em seguida, montar o disco de dados hello.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-216">Create a partition and filesystem, then mount hello data disk.</span></span> <span data-ttu-id="8ae6b-217">Para obter mais informações, consulte [conectar tooa novo disco de VM do Linux toomount Olá](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="8ae6b-217">For more information, see [Connect tooa Linux VM toomount hello new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> <span data-ttu-id="8ae6b-218">Feche a sessão SSH.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-218">Close your SSH session.</span></span>


## <a name="encrypt-virtual-machine"></a><span data-ttu-id="8ae6b-219">Criptografar máquina virtual</span><span class="sxs-lookup"><span data-stu-id="8ae6b-219">Encrypt virtual machine</span></span>
<span data-ttu-id="8ae6b-220">discos virtuais do tooencrypt hello, você reúne todos os componentes anteriores do hello:</span><span class="sxs-lookup"><span data-stu-id="8ae6b-220">tooencrypt hello virtual disks, you bring together all hello previous components:</span></span>

1. <span data-ttu-id="8ae6b-221">Especifique Olá entidade de serviço do Active Directory do Azure e a senha.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-221">Specify hello Azure Active Directory service principal and password.</span></span>
2. <span data-ttu-id="8ae6b-222">Especifica Olá Cofre de chaves toostore Olá metadados para os discos criptografados.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-222">Specify hello Key Vault toostore hello metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="8ae6b-223">Especifique Olá toouse de chaves de criptografia para criptografia hello e descriptografia.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-223">Specify hello cryptographic keys toouse for hello actual encryption and decryption.</span></span>
4. <span data-ttu-id="8ae6b-224">Especifique se você deseja tooencrypt disco de saudação SO, discos de dados de saudação ou todos.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-224">Specify whether you want tooencrypt hello OS disk, hello data disks, or all.</span></span>

<span data-ttu-id="8ae6b-225">Criptografe sua VM com [az vm encryption enable](/cli/azure/vm/encryption#enable).</span><span class="sxs-lookup"><span data-stu-id="8ae6b-225">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span></span> <span data-ttu-id="8ae6b-226">Olá, exemplo a seguir usa Olá `$sp_id` e `$sp_password` variáveis de saudação anterior `ad sp create-for-rbac` comando:</span><span class="sxs-lookup"><span data-stu-id="8ae6b-226">hello following example uses hello `$sp_id` and `$sp_password` variables from hello preceding `ad sp create-for-rbac` command:</span></span>

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

<span data-ttu-id="8ae6b-227">Levará algum tempo para Olá toocomplete de processo de criptografia de disco.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-227">It takes some time for hello disk encryption process toocomplete.</span></span> <span data-ttu-id="8ae6b-228">Monitorar o status de saudação do processo de saudação com [Mostrar de criptografia de vm az](/cli/azure/vm/encryption#show):</span><span class="sxs-lookup"><span data-stu-id="8ae6b-228">Monitor hello status of hello process with [az vm encryption show](/cli/azure/vm/encryption#show):</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="8ae6b-229">saudação de saída é similar toohello truncada de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="8ae6b-229">hello output is similar toohello following truncated example:</span></span>

```json
[
  "dataDisk": "EncryptionInProgress",
  "osDisk": "EncryptionInProgress",
]
```

<span data-ttu-id="8ae6b-230">Aguarde até que o status de Olá Olá OS relatórios de disco **VMRestartPending**, em seguida, reiniciar a VM com [reinicialização de vm az](/cli/azure/vm#restart):</span><span class="sxs-lookup"><span data-stu-id="8ae6b-230">Wait until hello status for hello OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="8ae6b-231">Olá processo de criptografia de disco é finalizado durante o processo de inicialização hello, então, aguarde alguns minutos antes de verificar o status de saudação do encryption novamente com **Mostrar de criptografia de vm az**:</span><span class="sxs-lookup"><span data-stu-id="8ae6b-231">hello disk encryption process is finalized during hello boot process, so wait a few minutes before checking hello status of encryption again with **az vm encryption show**:</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="8ae6b-232">status de saudação agora devem relatar disco Olá SO e discos de dados como **criptografado**.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-232">hello status should now report both hello OS disk and data disk as **Encrypted**.</span></span>


## <a name="add-additional-data-disks"></a><span data-ttu-id="8ae6b-233">Adicionar discos de dados adicionais</span><span class="sxs-lookup"><span data-stu-id="8ae6b-233">Add additional data disks</span></span>
<span data-ttu-id="8ae6b-234">Depois que você criptografou os discos de dados, você pode posteriormente adicionar discos virtuais adicionais tooyour VM e também criptografá-los.</span><span class="sxs-lookup"><span data-stu-id="8ae6b-234">Once you have encrypted your data disks, you can later add additional virtual disks tooyour VM and also encrypt them.</span></span> <span data-ttu-id="8ae6b-235">Por exemplo, permite adicionar uma segunda tooyour de disco virtual VM da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="8ae6b-235">For example, lets add a second virtual disk tooyour VM as follows:</span></span>

```azurecli
az vm disk attach-new --resource-group myResourceGroup --vm-name myVM --size-in-gb 5
```

<span data-ttu-id="8ae6b-236">Execute novamente Olá comando tooencrypt Olá os discos virtuais da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="8ae6b-236">Re-run hello command tooencrypt hello virtual disks as follows:</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="8ae6b-237">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8ae6b-237">Next steps</span></span>
* <span data-ttu-id="8ae6b-238">Para obter mais informações sobre como gerenciar o Cofre de Chaves do Azure, incluindo a exclusão de chaves criptográficas e cofres, consulte [Gerenciar Cofres de Chaves usando a CLI](../../key-vault/key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="8ae6b-238">For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md).</span></span>
* <span data-ttu-id="8ae6b-239">Para obter mais informações sobre criptografia de disco, como preparar um tooAzure da tooupload VM personalizado criptografado, consulte [criptografia de disco do Azure](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="8ae6b-239">For more information about disk encryption, such as preparing an encrypted custom VM tooupload tooAzure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
