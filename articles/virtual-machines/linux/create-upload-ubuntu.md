---
title: aaaCreate e carregar um VHD do Ubuntu Linux no Azure
description: "Saiba toocreate e carregar um Azure disco rígido virtual (VHD) que contém um sistema de operacional Ubuntu Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 3e097959-84fc-4f6a-8cc8-35e087fd1542
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: cc546a487f769b32432a7e80ddcd0f6af44e201f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-an-ubuntu-virtual-machine-for-azure"></a><span data-ttu-id="eeb99-103">Preparar uma máquina virtual do Ubuntu para o Azure</span><span class="sxs-lookup"><span data-stu-id="eeb99-103">Prepare an Ubuntu virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="official-ubuntu-cloud-images"></a><span data-ttu-id="eeb99-104">Imagens de nuvem oficiais do Ubuntu</span><span class="sxs-lookup"><span data-stu-id="eeb99-104">Official Ubuntu cloud images</span></span>
<span data-ttu-id="eeb99-105">O Ubuntu agora publica VHDs oficiais do Azure para download em [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/).</span><span class="sxs-lookup"><span data-stu-id="eeb99-105">Ubuntu now publishes official Azure VHDs for download at [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/).</span></span> <span data-ttu-id="eeb99-106">Se precisar toobuild sua própria imagem Ubuntu especializada para o Azure em vez de usar o procedimento manual de saudação abaixo dele é recomendado toostart com esses conhecidos trabalhando VHDs e personalizar conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="eeb99-106">If you need toobuild your own specialized Ubuntu image for Azure, rather than use hello manual procedure below it is recommended toostart with these known working VHDs and customize as needed.</span></span> <span data-ttu-id="eeb99-107">as versões mais recentes de imagem Olá sempre podem ser encontradas em Olá locais a seguir:</span><span class="sxs-lookup"><span data-stu-id="eeb99-107">hello latest image releases can always be found at hello following locations:</span></span>

* <span data-ttu-id="eeb99-108">Ubuntu 12.04/Precise: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="eeb99-108">Ubuntu 12.04/Precise: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="eeb99-109">Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="eeb99-109">Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="eeb99-110">Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="eeb99-110">Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eeb99-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="eeb99-111">Prerequisites</span></span>
<span data-ttu-id="eeb99-112">Este artigo pressupõe que você já tiver instalado um disco rígido virtual Ubuntu Linux sistema operacional tooa.</span><span class="sxs-lookup"><span data-stu-id="eeb99-112">This article assumes that you have already installed an Ubuntu Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="eeb99-113">Várias ferramentas existem toocreate arquivos. vhd, por exemplo, uma solução de virtualização como o Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="eeb99-113">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="eeb99-114">Para obter instruções, consulte [instalar Olá função Hyper-V e configurar uma máquina Virtual](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="eeb99-114">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="eeb99-115">**Notas de instalação do Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="eeb99-115">**Ubuntu installation notes**</span></span>

* <span data-ttu-id="eeb99-116">Veja também as [Notas de instalação gerais do Linux](create-upload-generic.md#general-linux-installation-notes) para obter mais dicas sobre como preparar o Linux para o Azure.</span><span class="sxs-lookup"><span data-stu-id="eeb99-116">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="eeb99-117">formato do Hello VHDX não tem suporte apenas no Azure, **VHD fixo**.</span><span class="sxs-lookup"><span data-stu-id="eeb99-117">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="eeb99-118">Você pode converter Olá disco tooVHD formato usando o Gerenciador do Hyper-V ou Olá cmdlet convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="eeb99-118">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span>
* <span data-ttu-id="eeb99-119">Ao instalar o sistema de Linux Olá é recomendável que você use partições padrão em vez de LVM (geralmente padrão Olá para muitas instalações).</span><span class="sxs-lookup"><span data-stu-id="eeb99-119">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="eeb99-120">Isso evitará LVM nome conflita com VMs clonados, especialmente se um sistema operacional de disco nunca precisa tooanother toobe anexado VMs para solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="eeb99-120">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="eeb99-121">Se você preferir, é possível usar [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) em discos de dados.</span><span class="sxs-lookup"><span data-stu-id="eeb99-121">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="eeb99-122">Não configure uma partição de troca no disco do sistema operacional hello.</span><span class="sxs-lookup"><span data-stu-id="eeb99-122">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="eeb99-123">agente do Linux Olá pode ser configurado toocreate um arquivo de permuta em disco de recursos temporário hello.</span><span class="sxs-lookup"><span data-stu-id="eeb99-123">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="eeb99-124">Para obter mais informações sobre isso podem ser encontradas nas etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="eeb99-124">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="eeb99-125">Todos os VHDs Olá devem ter tamanhos que sejam múltiplos de 1 MB.</span><span class="sxs-lookup"><span data-stu-id="eeb99-125">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="manual-steps"></a><span data-ttu-id="eeb99-126">Etapas manuais</span><span class="sxs-lookup"><span data-stu-id="eeb99-126">Manual steps</span></span>
> [!NOTE]
> <span data-ttu-id="eeb99-127">Antes de tentar toocreate sua própria imagem Ubuntu personalizada do Azure, considere usar Olá previamente criados e testados imagens de [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) em vez disso.</span><span class="sxs-lookup"><span data-stu-id="eeb99-127">Before attempting toocreate your own custom Ubuntu image for Azure, please consider using hello pre-built and tested images from [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) instead.</span></span>
> 
> 

1. <span data-ttu-id="eeb99-128">No painel central de saudação do Gerenciador do Hyper-V, selecione máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="eeb99-128">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="eeb99-129">Clique em **conectar** tooopen janela de saudação para a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="eeb99-129">Click **Connect** tooopen hello window for hello virtual machine.</span></span>

3. <span data-ttu-id="eeb99-130">Substitua os repositórios de saudação atual no repositório do Azure do hello imagem toouse Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="eeb99-130">Replace hello current repositories in hello image toouse Ubuntu's Azure repos.</span></span> <span data-ttu-id="eeb99-131">etapas Olá variam um pouco dependendo da versão do Ubuntu hello.</span><span class="sxs-lookup"><span data-stu-id="eeb99-131">hello steps vary slightly depending on hello Ubuntu version.</span></span>
   
    <span data-ttu-id="eeb99-132">Antes de editar `/etc/apt/sources.list`, é recomendável toomake um backup:</span><span class="sxs-lookup"><span data-stu-id="eeb99-132">Before editing `/etc/apt/sources.list`, it is recommended toomake a backup:</span></span>
   
        # sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak

    <span data-ttu-id="eeb99-133">Ubuntu 12,04:</span><span class="sxs-lookup"><span data-stu-id="eeb99-133">Ubuntu 12.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="eeb99-134">Ubuntu 14.04:</span><span class="sxs-lookup"><span data-stu-id="eeb99-134">Ubuntu 14.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="eeb99-135">Ubuntu 16.04:</span><span class="sxs-lookup"><span data-stu-id="eeb99-135">Ubuntu 16.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

4. <span data-ttu-id="eeb99-136">Olá imagens Ubuntu Azure estão seguindo Olá *habilitação de hardware* kernel (HWE).</span><span class="sxs-lookup"><span data-stu-id="eeb99-136">hello Ubuntu Azure images are now following hello *hardware enablement* (HWE) kernel.</span></span> <span data-ttu-id="eeb99-137">Atualize o kernel do mais recente de toohello do sistema operacional Olá executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="eeb99-137">Update hello operating system toohello latest kernel by running hello following commands:</span></span>

    <span data-ttu-id="eeb99-138">Ubuntu 12,04:</span><span class="sxs-lookup"><span data-stu-id="eeb99-138">Ubuntu 12.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-generic-lts-trusty linux-cloud-tools-generic-lts-trusty
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot
   
    <span data-ttu-id="eeb99-139">Ubuntu 14.04:</span><span class="sxs-lookup"><span data-stu-id="eeb99-139">Ubuntu 14.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-virtual-lts-vivid linux-lts-vivid-tools-common
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot

    <span data-ttu-id="eeb99-140">Ubuntu 16.04:</span><span class="sxs-lookup"><span data-stu-id="eeb99-140">Ubuntu 16.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-generic-hwe-16.04 linux-cloud-tools-generic-hwe-16.04
        (recommended) sudo apt-get dist-upgrade

        # sudo reboot

    <span data-ttu-id="eeb99-141">**Consulte também:**</span><span class="sxs-lookup"><span data-stu-id="eeb99-141">**See also:**</span></span>
    - [<span data-ttu-id="eeb99-142">https://wiki.ubuntu.com/Kernel/LTSEnablementStack</span><span class="sxs-lookup"><span data-stu-id="eeb99-142">https://wiki.ubuntu.com/Kernel/LTSEnablementStack</span></span>](https://wiki.ubuntu.com/Kernel/LTSEnablementStack)
    - [<span data-ttu-id="eeb99-143">https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack</span><span class="sxs-lookup"><span data-stu-id="eeb99-143">https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack</span></span>](https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack)


5. <span data-ttu-id="eeb99-144">Modificar a linha de inicialização de kernel de saudação para parâmetros de kernel adicionais tooinclude Grub do Azure.</span><span class="sxs-lookup"><span data-stu-id="eeb99-144">Modify hello kernel boot line for Grub tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="eeb99-145">toodo nesse abrir `/etc/default/grub` em um editor de texto, localizar variável Olá chamado `GRUB_CMDLINE_LINUX_DEFAULT` (ou adicioná-lo se necessário) e edite-Olá tooinclude parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="eeb99-145">toodo this open `/etc/default/grub` in a text editor, find hello variable called `GRUB_CMDLINE_LINUX_DEFAULT` (or add it if needed) and edit it tooinclude hello following parameters:</span></span>
   
        GRUB_CMDLINE_LINUX_DEFAULT="console=tty1 console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300"

    <span data-ttu-id="eeb99-146">Salve e feche esse arquivo e execute `sudo update-grub`.</span><span class="sxs-lookup"><span data-stu-id="eeb99-146">Save and close this file, and then run `sudo update-grub`.</span></span> <span data-ttu-id="eeb99-147">Isso garantirá que todas as mensagens de console são enviadas toohello primeira porta serial, que pode ajudar o suporte técnico do Azure com problemas de depuração.</span><span class="sxs-lookup"><span data-stu-id="eeb99-147">This will ensure all console messages are sent toohello first serial port, which can assist Azure technical support with debugging issues.</span></span>

6. <span data-ttu-id="eeb99-148">Certifique-se de servidor SSH hello está instalado e configurado toostart no momento da inicialização.</span><span class="sxs-lookup"><span data-stu-id="eeb99-148">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="eeb99-149">Geralmente, esse é o padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="eeb99-149">This is usually hello default.</span></span>

7. <span data-ttu-id="eeb99-150">Instale Olá agente Linux do Azure:</span><span class="sxs-lookup"><span data-stu-id="eeb99-150">Install hello Azure Linux Agent:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install walinuxagent

    >[!Note]
    <span data-ttu-id="eeb99-151">Olá `walinuxagent` pacote pode remover Olá `NetworkManager` e `NetworkManager-gnome` pacotes, se eles estiverem instalados.</span><span class="sxs-lookup"><span data-stu-id="eeb99-151">hello `walinuxagent` package may remove hello `NetworkManager` and `NetworkManager-gnome` packages, if they are installed.</span></span>

8. <span data-ttu-id="eeb99-152">Execute Olá seguindo a máquina virtual do comandos toodeprovision hello e prepará-la para provisionamento no Azure:</span><span class="sxs-lookup"><span data-stu-id="eeb99-152">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

9. <span data-ttu-id="eeb99-153">Clique em **Ação -> Desligar** no Gerenciador do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="eeb99-153">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="eeb99-154">O VHD Linux está agora pronto toobe carregado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="eeb99-154">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eeb99-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="eeb99-155">Next steps</span></span>
<span data-ttu-id="eeb99-156">Você está agora pronto toouse seu Ubuntu Linux disco rígido virtual toocreate novas máquinas virtuais no Azure.</span><span class="sxs-lookup"><span data-stu-id="eeb99-156">You're now ready toouse your Ubuntu Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="eeb99-157">Se isso for Olá primeira vez que você está carregando tooAzure de arquivo. vhd hello, consulte as etapas 2 e 3 em [criando e carregando um disco rígido virtual que contém o sistema de operacional Linux Olá](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="eeb99-157">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="references"></a><span data-ttu-id="eeb99-158">Referências</span><span class="sxs-lookup"><span data-stu-id="eeb99-158">References</span></span>
<span data-ttu-id="eeb99-159">Kernel de Habilitação de Hardware do Ubuntu (HWE):</span><span class="sxs-lookup"><span data-stu-id="eeb99-159">Ubuntu hardware enablement (HWE) kernel:</span></span>

* [<span data-ttu-id="eeb99-160">http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html</span><span class="sxs-lookup"><span data-stu-id="eeb99-160">http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html</span></span>](http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html)
* [<span data-ttu-id="eeb99-161">http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html</span><span class="sxs-lookup"><span data-stu-id="eeb99-161">http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html</span></span>](http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html)

