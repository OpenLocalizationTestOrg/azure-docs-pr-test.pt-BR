---
title: armazenamento de arquivo do Azure em VMs do Linux usando SMB de aaaMount | Microsoft Docs
description: Como toomount armazenamento de arquivo do Azure em VMs do Linux usando SMB com hello 2.0 do CLI do Azure
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/13/2017
ms.author: v-livech
ms.openlocfilehash: 7b34c81e602748b78c924f44a54b876744c28f56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-using-smb"></a><span data-ttu-id="d99f3-103">Montar o Armazenamento de Arquivos do Azure em VMs Linux usando SMB</span><span class="sxs-lookup"><span data-stu-id="d99f3-103">Mount Azure File storage on Linux VMs using SMB</span></span>

<span data-ttu-id="d99f3-104">Este artigo mostra como Olá tooutilize serviço de armazenamento de arquivo do Azure em uma VM do Linux usando SMB montar com hello 2.0 do CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="d99f3-104">This article shows you how tooutilize hello Azure File storage service on a Linux VM using an SMB mount with hello Azure CLI 2.0.</span></span> <span data-ttu-id="d99f3-105">Armazenamento de arquivo do Azure oferece compartilhamentos de arquivos na nuvem hello usando o protocolo SMB padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="d99f3-105">Azure File storage offers file shares in hello cloud using hello standard SMB protocol.</span></span> <span data-ttu-id="d99f3-106">Você também pode executar essas etapas com hello [Azure CLI 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d99f3-106">You can also perform these steps with hello [Azure CLI 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="d99f3-107">requisitos de saudação são:</span><span class="sxs-lookup"><span data-stu-id="d99f3-107">hello requirements are:</span></span>

- [<span data-ttu-id="d99f3-108">uma conta do Azure</span><span class="sxs-lookup"><span data-stu-id="d99f3-108">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="d99f3-109">arquivos de chave SSH pública e privada</span><span class="sxs-lookup"><span data-stu-id="d99f3-109">SSH public and private key files</span></span>](mac-create-ssh-keys.md)

## <a name="quick-commands"></a><span data-ttu-id="d99f3-110">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="d99f3-110">Quick Commands</span></span>

* <span data-ttu-id="d99f3-111">Um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="d99f3-111">A resource group</span></span>
* <span data-ttu-id="d99f3-112">Uma Rede virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="d99f3-112">An Azure virtual network</span></span>
* <span data-ttu-id="d99f3-113">Um grupo de segurança de rede com uma entrada SSH</span><span class="sxs-lookup"><span data-stu-id="d99f3-113">A network security group with an SSH inbound</span></span>
* <span data-ttu-id="d99f3-114">Uma sub-rede</span><span class="sxs-lookup"><span data-stu-id="d99f3-114">A subnet</span></span>
* <span data-ttu-id="d99f3-115">Uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="d99f3-115">An Azure storage account</span></span>
* <span data-ttu-id="d99f3-116">Chaves de conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="d99f3-116">Azure storage account keys</span></span>
* <span data-ttu-id="d99f3-117">Um compartilhamento do Armazenamento de arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="d99f3-117">An Azure File storage share</span></span>
* <span data-ttu-id="d99f3-118">Uma VM do Linux</span><span class="sxs-lookup"><span data-stu-id="d99f3-118">A Linux VM</span></span>

<span data-ttu-id="d99f3-119">Substitua os exemplos por suas próprias configurações.</span><span class="sxs-lookup"><span data-stu-id="d99f3-119">Replace any examples with your own settings.</span></span>

### <a name="create-a-directory-for-hello-local-mount"></a><span data-ttu-id="d99f3-120">Crie um diretório de montagem local Olá</span><span class="sxs-lookup"><span data-stu-id="d99f3-120">Create a directory for hello local mount</span></span>

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-hello-file-storage-smb-share-toohello-mount-point"></a><span data-ttu-id="d99f3-121">Armazenamento de arquivo hello SMB compartilhamento toohello montagem ponto de montagem</span><span class="sxs-lookup"><span data-stu-id="d99f3-121">Mount hello File storage SMB share toohello mount point</span></span>

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-hello-mount-after-a-reboot"></a><span data-ttu-id="d99f3-122">Manter Olá montagem após uma reinicialização</span><span class="sxs-lookup"><span data-stu-id="d99f3-122">Persist hello mount after a reboot</span></span>
<span data-ttu-id="d99f3-123">toodo, então, adicionar Olá toohello linha a seguir `/etc/fstab`:</span><span class="sxs-lookup"><span data-stu-id="d99f3-123">toodo so, add hello following line toohello `/etc/fstab`:</span></span>

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="d99f3-124">Passo a passo detalhado</span><span class="sxs-lookup"><span data-stu-id="d99f3-124">Detailed walkthrough</span></span>

<span data-ttu-id="d99f3-125">Armazenamento de arquivos oferece os compartilhamentos de arquivos na nuvem Olá que usam protocolo SMB padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="d99f3-125">File storage offers file shares in hello cloud that use hello standard SMB protocol.</span></span> <span data-ttu-id="d99f3-126">Com a versão mais recente de saudação do armazenamento de arquivos, você também pode montar um compartilhamento de arquivos de qualquer sistema operacional que dá suporte a SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="d99f3-126">With hello latest release of File storage, you can also mount a file share from any OS that supports SMB 3.0.</span></span> <span data-ttu-id="d99f3-127">Quando você usa uma montagem SMB no Linux, você obter backups fácil tooa robusto e permanente arquivamento local de armazenamento que é suportado por um SLA.</span><span class="sxs-lookup"><span data-stu-id="d99f3-127">When you use an SMB mount on Linux, you get easy backups tooa robust, permanent archiving storage location that is supported by an SLA.</span></span>

<span data-ttu-id="d99f3-128">Movendo os arquivos de uma montagem SMB tooan VM que é hospedada no armazenamento de arquivo é que uma ótima maneira toodebug logs.</span><span class="sxs-lookup"><span data-stu-id="d99f3-128">Moving files from a VM tooan SMB mount that's hosted on File storage is a great way toodebug logs.</span></span> <span data-ttu-id="d99f3-129">Isso ocorre porque Olá compartilhamento SMB mesmo pode ser montado localmente tooyour estação de trabalho de Mac, Linux ou Windows.</span><span class="sxs-lookup"><span data-stu-id="d99f3-129">That's because hello same SMB share can be mounted locally tooyour Mac, Linux, or Windows workstation.</span></span> <span data-ttu-id="d99f3-130">SMB não é a melhor solução Olá para streaming Linux ou logs do aplicativo em tempo real, porque Olá protocolo SMB não está compilado toohandle tais direitos pesada de registro em log.</span><span class="sxs-lookup"><span data-stu-id="d99f3-130">SMB isn't hello best solution for streaming Linux or application logs in real time, because hello SMB protocol is not built toohandle such heavy logging duties.</span></span> <span data-ttu-id="d99f3-131">Uma ferramenta de camada de log unificada dedicada, como o Fluentd, poderá ser uma escolha melhor em relação ao SMB para coletar a saída de log do Linux e de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d99f3-131">A dedicated, unified logging layer tool such as Fluentd would be a better choice than SMB for collecting Linux and application logging output.</span></span>

<span data-ttu-id="d99f3-132">Para este passo a passo detalhada, criamos pré-requisitos Olá necessário toofirst criar compartilhamento de armazenamento de arquivo hello e, em seguida, recriá-lo por meio do SMB em uma VM Linux.</span><span class="sxs-lookup"><span data-stu-id="d99f3-132">For this detailed walkthrough, we create hello prerequisites needed toofirst create hello File storage share, and then mount it via SMB on a Linux VM.</span></span>

1. <span data-ttu-id="d99f3-133">Criar um grupo de recursos com [criar grupo az](/cli/azure/group#create) toohold compartilhamento de arquivos de saudação.</span><span class="sxs-lookup"><span data-stu-id="d99f3-133">Create a resource group with [az group create](/cli/azure/group#create) toohold hello file share.</span></span>

    <span data-ttu-id="d99f3-134">toocreate um grupo de recursos denominado `myResourceGroup` em Olá local "US West", use Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="d99f3-134">toocreate a resource group named `myResourceGroup` in hello "West US" location, use hello following example:</span></span>

    ```azurecli
    az group create --name myResourceGroup --location westus
    ```

2. <span data-ttu-id="d99f3-135">Criar uma conta de armazenamento do Azure com [criar conta de armazenamento az](/cli/azure/storage/account#create) toostore Olá arquivos reais.</span><span class="sxs-lookup"><span data-stu-id="d99f3-135">Create an Azure storage account with [az storage account create](/cli/azure/storage/account#create) toostore hello actual files.</span></span>

    <span data-ttu-id="d99f3-136">toocreate uma conta de armazenamento denominada mystorageaccount usando o armazenamento de Standard_LRS Olá SKU, use Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="d99f3-136">toocreate a storage account named mystorageaccount by using hello Standard_LRS storage SKU, use hello following example:</span></span>

    ```azurecli
    az storage account create --resource-group myResourceGroup \
        --name mystorageaccount \
        --location westus \
        --sku Standard_LRS
    ```

3. <span data-ttu-id="d99f3-137">Mostra chaves de conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="d99f3-137">Show hello storage account keys.</span></span>

    <span data-ttu-id="d99f3-138">Quando você cria uma conta de armazenamento, chaves de conta Olá são criadas em pares para que eles podem ser girados sem qualquer interrupção do serviço.</span><span class="sxs-lookup"><span data-stu-id="d99f3-138">When you create a storage account, hello account keys are created in pairs so that they can be rotated without any service interruption.</span></span> <span data-ttu-id="d99f3-139">Quando você alternar toohello segunda chave no par hello, você pode criar um novo par de chaves.</span><span class="sxs-lookup"><span data-stu-id="d99f3-139">When you switch toohello second key in hello pair, you create a new key pair.</span></span> <span data-ttu-id="d99f3-140">Novas chaves de conta de armazenamento sempre são criadas em pares, garantindo que você sempre tenha pelo menos um armazenamento não usado conta chave pronto tooswitch para.</span><span class="sxs-lookup"><span data-stu-id="d99f3-140">New storage account keys are always created in pairs, ensuring that you always have at least one unused storage account key ready tooswitch to.</span></span>

    <span data-ttu-id="d99f3-141">Exibir chaves de conta de armazenamento Olá com hello [lista de chaves de conta de armazenamento az](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="d99f3-141">View hello storage account keys with hello [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span> <span data-ttu-id="d99f3-142">Olá chaves de conta de armazenamento para Olá chamado `mystorageaccount` são listadas na saudação de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="d99f3-142">hello storage account keys for hello named `mystorageaccount` are listed in hello following example:</span></span>

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount
    ```

    <span data-ttu-id="d99f3-143">tooextract uma única chave, use Olá `--query` sinalizador.</span><span class="sxs-lookup"><span data-stu-id="d99f3-143">tooextract a single key, use hello `--query` flag.</span></span> <span data-ttu-id="d99f3-144">Olá, exemplo a seguir extrai chave primeiro hello (`[0]`):</span><span class="sxs-lookup"><span data-stu-id="d99f3-144">hello following example extracts hello first key (`[0]`):</span></span>

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount \
        --query '[0].{Key:value}' --output tsv
    ```

4. <span data-ttu-id="d99f3-145">Crie compartilhamento de armazenamento de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="d99f3-145">Create hello File storage share.</span></span>

    <span data-ttu-id="d99f3-146">compartilhamento de armazenamento de arquivo Hello contém Olá compartilhamento SMB com [criar compartilhamento de armazenamento az](/cli/azure/storage/share#create).</span><span class="sxs-lookup"><span data-stu-id="d99f3-146">hello File storage share contains hello SMB share with [az storage share create](/cli/azure/storage/share#create).</span></span> <span data-ttu-id="d99f3-147">cota de saudação sempre é expresso em gigabytes (GB).</span><span class="sxs-lookup"><span data-stu-id="d99f3-147">hello quota is always expressed in gigabytes (GB).</span></span> <span data-ttu-id="d99f3-148">Passar em uma das chaves de saudação da saudação anterior `az storage account keys list` comando.</span><span class="sxs-lookup"><span data-stu-id="d99f3-148">Pass in one of hello keys from hello preceding `az storage account keys list` command.</span></span> <span data-ttu-id="d99f3-149">Crie um compartilhamento chamado mystorageshare com uma cota de 10 GB usando Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="d99f3-149">Create a share named mystorageshare with a 10-GB quota by using hello following example:</span></span>

    ```azurecli
    az storage share create --name mystorageshare \
        --quota 10 \
        --account-name mystorageaccount \
        --account-key nPOgPR<--snip-->4Q==
    ```

5. <span data-ttu-id="d99f3-150">Crie um diretório de ponto de montagem.</span><span class="sxs-lookup"><span data-stu-id="d99f3-150">Create a mount-point directory.</span></span>

    <span data-ttu-id="d99f3-151">Crie um diretório local no Olá Olá Linux arquivo sistema toomount compartilhamento de SMB.</span><span class="sxs-lookup"><span data-stu-id="d99f3-151">Create a local directory in hello Linux file system toomount hello SMB share to.</span></span> <span data-ttu-id="d99f3-152">Qualquer coisa gravados ou lidos do diretório de montagem local de saudação é encaminhada toohello compartilhamento SMB que é hospedado no armazenamento de arquivo.</span><span class="sxs-lookup"><span data-stu-id="d99f3-152">Anything written or read from hello local mount directory is forwarded toohello SMB share that's hosted on File storage.</span></span> <span data-ttu-id="d99f3-153">toocreate um diretório local no /mnt/Retention/ mymountdirectory, use Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="d99f3-153">toocreate a local directory at /mnt/mymountdirectory, use hello following example:</span></span>

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

6. <span data-ttu-id="d99f3-154">Monte o diretório local de toohello Olá de compartilhamento SMB.</span><span class="sxs-lookup"><span data-stu-id="d99f3-154">Mount hello SMB share toohello local directory.</span></span>

    <span data-ttu-id="d99f3-155">Fornece seu próprio nome de usuário de conta de armazenamento e a chave de conta de armazenamento de credenciais de montagem de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d99f3-155">Provide your own storage account username and storage account key for hello mount credentials as follows:</span></span>

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=mystorageaccount,password=mystorageaccountkey,dir_mode=0777,file_mode=0777
    ```

7. <span data-ttu-id="d99f3-156">Manter Olá montar SMB por meio de reinicializações.</span><span class="sxs-lookup"><span data-stu-id="d99f3-156">Persist hello SMB mount through reboots.</span></span>

    <span data-ttu-id="d99f3-157">Quando você reinicializa Olá VM do Linux, hello montado compartilhamento SMB é desmontado durante o desligamento.</span><span class="sxs-lookup"><span data-stu-id="d99f3-157">When you reboot hello Linux VM, hello mounted SMB share is unmounted during shutdown.</span></span> <span data-ttu-id="d99f3-158">Olá tooremount compartilhamento SMB na inicialização, adicionar uma linha de toohello /etc/fstab Linux.</span><span class="sxs-lookup"><span data-stu-id="d99f3-158">tooremount hello SMB share on boot, add a line toohello Linux /etc/fstab.</span></span> <span data-ttu-id="d99f3-159">Linux usa Olá fstab arquivo toolist Olá sistemas de arquivos que ele precisa toomount durante o processo de inicialização hello.</span><span class="sxs-lookup"><span data-stu-id="d99f3-159">Linux uses hello fstab file toolist hello file systems that it needs toomount during hello boot process.</span></span> <span data-ttu-id="d99f3-160">Adicionando compartilhamento SMB Olá garante que esse compartilhamento de armazenamento de arquivo hello é um sistema de arquivos montados permanentemente para Olá VM do Linux.</span><span class="sxs-lookup"><span data-stu-id="d99f3-160">Adding hello SMB share ensures that hello File storage share is a permanently mounted file system for hello Linux VM.</span></span> <span data-ttu-id="d99f3-161">Adicionando Olá arquivo armazenamento SMB compartilhamento tooa nova VM é possível quando você usa a inicialização de nuvem.</span><span class="sxs-lookup"><span data-stu-id="d99f3-161">Adding hello File storage SMB share tooa new VM is possible when you use cloud-init.</span></span>

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a><span data-ttu-id="d99f3-162">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d99f3-162">Next steps</span></span>

- [<span data-ttu-id="d99f3-163">Usando a nuvem init toocustomize uma VM do Linux durante a criação</span><span class="sxs-lookup"><span data-stu-id="d99f3-163">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="d99f3-164">Adicionar um disco tooa VM do Linux</span><span class="sxs-lookup"><span data-stu-id="d99f3-164">Add a disk tooa Linux VM</span></span>](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="d99f3-165">Criptografar discos em uma VM Linux usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="d99f3-165">Encrypt disks on a Linux VM by using hello Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
