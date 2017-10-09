---
title: aaaMount armazenamento de arquivo do Azure em VMs do Linux usando SMB com 1.0 da CLI do Azure | Microsoft Docs
description: Como toomount armazenamento de arquivo do Azure em VMs do Linux usando o SMB
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
ms.date: 12/07/2016
ms.author: v-livech
ms.openlocfilehash: 14a4224228cadb0ae2f05e8e5c8022ee84f138a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-by-using-smb-with-azure-cli-10"></a><span data-ttu-id="c408c-103">Montar o Armazenamento de arquivos do Azure em VMs Linux ao usar SMB com CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="c408c-103">Mount Azure File storage on Linux VMs by using SMB with Azure CLI 1.0</span></span>

<span data-ttu-id="c408c-104">Este artigo mostra como toomount armazenamento de arquivo do Azure em uma VM do Linux usando Olá protocolo de bloco de mensagens de servidor (SMB).</span><span class="sxs-lookup"><span data-stu-id="c408c-104">This article shows how toomount Azure File storage on a Linux VM by using hello Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="c408c-105">Armazenamento de arquivos oferece os compartilhamentos de arquivos na nuvem Olá por meio do protocolo SMB padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="c408c-105">File storage offers file shares in hello cloud via hello standard SMB protocol.</span></span> <span data-ttu-id="c408c-106">requisitos de saudação são:</span><span class="sxs-lookup"><span data-stu-id="c408c-106">hello requirements are:</span></span>

* <span data-ttu-id="c408c-107">Uma [conta do Azure](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="c408c-107">An [Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>
* [<span data-ttu-id="c408c-108">Arquivos de chave Secure Shell (SSH) pública e privada</span><span class="sxs-lookup"><span data-stu-id="c408c-108">Secure Shell (SSH) public and private key files</span></span>](mac-create-ssh-keys.md)

## <a name="cli-versions-toouse"></a><span data-ttu-id="c408c-109">CLI versões toouse</span><span class="sxs-lookup"><span data-stu-id="c408c-109">CLI versions toouse</span></span>
<span data-ttu-id="c408c-110">Você pode concluir a tarefa de saudação usando uma saudação versões de interface de linha de comando (CLI) a seguir:</span><span class="sxs-lookup"><span data-stu-id="c408c-110">You can complete hello task by using one of hello following command-line interface (CLI) versions:</span></span>

- <span data-ttu-id="c408c-111">[1.0 de CLI do Azure](#quick-commands) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)</span><span class="sxs-lookup"><span data-stu-id="c408c-111">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="c408c-112">[2.0 do CLI do Azure](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)-nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="c408c-112">[Azure CLI 2.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)- our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="c408c-113">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="c408c-113">Quick commands</span></span>
<span data-ttu-id="c408c-114">tarefa de saudação tooaccomplish rapidamente, execute as etapas de saudação nesta seção.</span><span class="sxs-lookup"><span data-stu-id="c408c-114">tooaccomplish hello task quickly, follow hello steps in this section.</span></span> <span data-ttu-id="c408c-115">Para obter mais informações e o contexto, começam com hello ["Passo a passo detalhado"](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) seção.</span><span class="sxs-lookup"><span data-stu-id="c408c-115">For more detailed information and context, begin at hello ["Detailed walkthrough"](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) section.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="c408c-116">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c408c-116">Prerequisites</span></span>
* <span data-ttu-id="c408c-117">Um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="c408c-117">A resource group</span></span>
* <span data-ttu-id="c408c-118">Uma Rede virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="c408c-118">An Azure virtual network</span></span>
* <span data-ttu-id="c408c-119">Um grupo de segurança de rede com uma entrada SSH</span><span class="sxs-lookup"><span data-stu-id="c408c-119">A network security group with an SSH inbound</span></span>
* <span data-ttu-id="c408c-120">Uma sub-rede</span><span class="sxs-lookup"><span data-stu-id="c408c-120">A subnet</span></span>
* <span data-ttu-id="c408c-121">Uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="c408c-121">An Azure storage account</span></span>
* <span data-ttu-id="c408c-122">Chaves de conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="c408c-122">Azure storage account keys</span></span>
* <span data-ttu-id="c408c-123">Um compartilhamento do Armazenamento de arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="c408c-123">An Azure File storage share</span></span>
* <span data-ttu-id="c408c-124">Uma VM do Linux</span><span class="sxs-lookup"><span data-stu-id="c408c-124">A Linux VM</span></span>

<span data-ttu-id="c408c-125">Substitua os exemplos por suas próprias configurações.</span><span class="sxs-lookup"><span data-stu-id="c408c-125">Replace any examples with your own settings.</span></span>

### <a name="create-a-directory-for-hello-local-mount"></a><span data-ttu-id="c408c-126">Crie um diretório de montagem local Olá</span><span class="sxs-lookup"><span data-stu-id="c408c-126">Create a directory for hello local mount</span></span>

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-hello-file-storage-smb-share-toohello-mount-point"></a><span data-ttu-id="c408c-127">Armazenamento de arquivo hello SMB compartilhamento toohello montagem ponto de montagem</span><span class="sxs-lookup"><span data-stu-id="c408c-127">Mount hello File storage SMB share toohello mount point</span></span>

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-hello-mount-after-a-reboot"></a><span data-ttu-id="c408c-128">Manter Olá montagem após uma reinicialização</span><span class="sxs-lookup"><span data-stu-id="c408c-128">Persist hello mount after a reboot</span></span>
<span data-ttu-id="c408c-129">Adicionar Olá seguinte linha muito`/etc/fstab`:</span><span class="sxs-lookup"><span data-stu-id="c408c-129">Add hello following line too`/etc/fstab`:</span></span>

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="c408c-130">Passo a passo detalhado</span><span class="sxs-lookup"><span data-stu-id="c408c-130">Detailed walkthrough</span></span>

<span data-ttu-id="c408c-131">Armazenamento de arquivos oferece os compartilhamentos de arquivos na nuvem Olá que usam protocolo SMB padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="c408c-131">File storage offers file shares in hello cloud that use hello standard SMB protocol.</span></span> <span data-ttu-id="c408c-132">Com a versão mais recente de saudação do armazenamento de arquivos, você também pode montar um compartilhamento de arquivos de qualquer sistema operacional que dá suporte a SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="c408c-132">With hello latest release of File storage, you can also mount a file share from any OS that supports SMB 3.0.</span></span> <span data-ttu-id="c408c-133">Quando você usa uma montagem SMB no Linux, você obter backups fácil tooa robusto e permanente arquivamento local de armazenamento que é suportado por um SLA.</span><span class="sxs-lookup"><span data-stu-id="c408c-133">When you use an SMB mount on Linux, you get easy backups tooa robust, permanent archiving storage location that is supported by an SLA.</span></span>

<span data-ttu-id="c408c-134">Movendo os arquivos de uma montagem SMB tooan VM que é hospedada no armazenamento de arquivo é que uma ótima maneira toodebug logs.</span><span class="sxs-lookup"><span data-stu-id="c408c-134">Moving files from a VM tooan SMB mount that's hosted on File storage is a great way toodebug logs.</span></span> <span data-ttu-id="c408c-135">Isso ocorre porque Olá compartilhamento SMB mesmo pode ser montado localmente tooyour estação de trabalho de Mac, Linux ou Windows.</span><span class="sxs-lookup"><span data-stu-id="c408c-135">That's because hello same SMB share can be mounted locally tooyour Mac, Linux, or Windows workstation.</span></span> <span data-ttu-id="c408c-136">SMB não é a melhor solução Olá para streaming Linux ou logs do aplicativo em tempo real, porque Olá protocolo SMB não está compilado toohandle tais direitos pesada de registro em log.</span><span class="sxs-lookup"><span data-stu-id="c408c-136">SMB isn't hello best solution for streaming Linux or application logs in real time, because hello SMB protocol is not built toohandle such heavy logging duties.</span></span> <span data-ttu-id="c408c-137">Uma ferramenta de camada de log unificada dedicada, como o Fluentd, poderá ser uma escolha melhor em relação ao SMB para coletar a saída de log do Linux e de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c408c-137">A dedicated, unified logging layer tool such as Fluentd would be a better choice than SMB for collecting Linux and application logging output.</span></span>

<span data-ttu-id="c408c-138">Para este passo a passo detalhada, criamos pré-requisitos Olá necessário toofirst criar compartilhamento de armazenamento de arquivo hello e, em seguida, recriá-lo por meio do SMB em uma VM Linux.</span><span class="sxs-lookup"><span data-stu-id="c408c-138">For this detailed walkthrough, we create hello prerequisites needed toofirst create hello File storage share, and then mount it via SMB on a Linux VM.</span></span>

1. <span data-ttu-id="c408c-139">Crie uma conta de armazenamento do Azure usando Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="c408c-139">Create an Azure storage account by using hello following code:</span></span>

    ```azurecli
    azure storage account create myStorageAccount \
    --sku-name lrs \
    --kind storage \
    -l westus \
    -g myResourceGroup
    ```

2. <span data-ttu-id="c408c-140">Mostra chaves de conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="c408c-140">Show hello storage account keys.</span></span>

    <span data-ttu-id="c408c-141">Quando você cria uma conta de armazenamento, chaves de conta Olá são criadas em pares para que eles podem ser girados sem qualquer interrupção do serviço.</span><span class="sxs-lookup"><span data-stu-id="c408c-141">When you create a storage account, hello account keys are created in pairs so that they can be rotated without any service interruption.</span></span> <span data-ttu-id="c408c-142">Quando você alternar toohello segunda chave no par hello, você pode criar um novo par de chaves.</span><span class="sxs-lookup"><span data-stu-id="c408c-142">When you switch toohello second key in hello pair, you create a new key pair.</span></span> <span data-ttu-id="c408c-143">Novas chaves de conta de armazenamento sempre são criadas em pares, garantindo que você sempre tenha pelo menos um armazenamento sem uso chave pronto tooswitch para.</span><span class="sxs-lookup"><span data-stu-id="c408c-143">New storage account keys are always created in pairs, ensuring that you always have at least one unused storage key ready tooswitch to.</span></span> <span data-ttu-id="c408c-144">chaves de conta de armazenamento do tooshow hello, use Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="c408c-144">tooshow hello storage account keys, use hello following code:</span></span>

    ```azurecli
    azure storage account keys list myStorageAccount \
    --resource-group myResourceGroup
    ```
3. <span data-ttu-id="c408c-145">Crie compartilhamento de armazenamento de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="c408c-145">Create hello File storage share.</span></span>

    <span data-ttu-id="c408c-146">compartilhamento de armazenamento de arquivo Hello contém um compartilhamento SMB hello.</span><span class="sxs-lookup"><span data-stu-id="c408c-146">hello File storage share contains hello SMB share.</span></span> <span data-ttu-id="c408c-147">cota de saudação sempre é expresso em gigabytes (GB).</span><span class="sxs-lookup"><span data-stu-id="c408c-147">hello quota is always expressed in gigabytes (GB).</span></span> <span data-ttu-id="c408c-148">toocreate Olá compartilhamento de arquivo de armazenamento, use Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="c408c-148">toocreate hello File storage share, use hello following code:</span></span>

    ```azurecli
    azure storage share create mystorageshare \
    --quota 10 \
    --account-name myStorageAccount \
    --account-key nPOgPR<--snip-->4Q==
    ```

4. <span data-ttu-id="c408c-149">Crie diretório de ponto de montagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="c408c-149">Create hello mount-point directory.</span></span>

    <span data-ttu-id="c408c-150">Você deve criar um diretório local no Olá Olá Linux arquivo sistema toomount compartilhamento de SMB.</span><span class="sxs-lookup"><span data-stu-id="c408c-150">You must create a local directory in hello Linux file system toomount hello SMB share to.</span></span> <span data-ttu-id="c408c-151">Qualquer coisa gravados ou lidos do diretório de montagem local de saudação é encaminhada toohello compartilhamento SMB que é hospedado no armazenamento de arquivo.</span><span class="sxs-lookup"><span data-stu-id="c408c-151">Anything written or read from hello local mount directory is forwarded toohello SMB share that's hosted on File storage.</span></span> <span data-ttu-id="c408c-152">diretório de saudação toocreate, use Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="c408c-152">toocreate hello directory, use hello following code:</span></span>

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

5. <span data-ttu-id="c408c-153">Monte Olá compartilhamento SMB usando Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="c408c-153">Mount hello SMB share by using hello following code:</span></span>

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=myStorageAccount,password=myStorageAccountkey,dir_mode=0777,file_mode=0777
    ```

6. <span data-ttu-id="c408c-154">Manter Olá montar SMB por meio de reinicializações.</span><span class="sxs-lookup"><span data-stu-id="c408c-154">Persist hello SMB mount through reboots.</span></span>

    <span data-ttu-id="c408c-155">Quando você reinicializa Olá VM do Linux, hello montado compartilhamento SMB é desmontado durante o desligamento.</span><span class="sxs-lookup"><span data-stu-id="c408c-155">When you reboot hello Linux VM, hello mounted SMB share is unmounted during shutdown.</span></span> <span data-ttu-id="c408c-156">compartilhamento SMB tooremount Olá na inicialização, você deve adicionar uma linha de toohello /etc/fstab Linux.</span><span class="sxs-lookup"><span data-stu-id="c408c-156">tooremount hello SMB share on boot, you must add a line toohello Linux /etc/fstab.</span></span> <span data-ttu-id="c408c-157">Linux usa Olá fstab arquivo toolist Olá sistemas de arquivos que ele precisa toomount durante o processo de inicialização hello.</span><span class="sxs-lookup"><span data-stu-id="c408c-157">Linux uses hello fstab file toolist hello file systems that it needs toomount during hello boot process.</span></span> <span data-ttu-id="c408c-158">Adicionando compartilhamento SMB Olá garante que esse compartilhamento de armazenamento de arquivo hello é um sistema de arquivos montados permanentemente para Olá VM do Linux.</span><span class="sxs-lookup"><span data-stu-id="c408c-158">Adding hello SMB share ensures that hello File storage share is a permanently mounted file system for hello Linux VM.</span></span> <span data-ttu-id="c408c-159">Adicionando Olá arquivo armazenamento SMB compartilhamento tooa nova VM é possível quando você usa a inicialização de nuvem.</span><span class="sxs-lookup"><span data-stu-id="c408c-159">Adding hello File storage SMB share tooa new VM is possible when you use cloud-init.</span></span>

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a><span data-ttu-id="c408c-160">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c408c-160">Next steps</span></span>

- [<span data-ttu-id="c408c-161">Usando a nuvem init toocustomize uma VM do Linux durante a criação</span><span class="sxs-lookup"><span data-stu-id="c408c-161">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="c408c-162">Adicionar um disco tooa VM do Linux</span><span class="sxs-lookup"><span data-stu-id="c408c-162">Add a disk tooa Linux VM</span></span>](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="c408c-163">Criptografar discos em uma VM Linux usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="c408c-163">Encrypt disks on a Linux VM by using hello Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
