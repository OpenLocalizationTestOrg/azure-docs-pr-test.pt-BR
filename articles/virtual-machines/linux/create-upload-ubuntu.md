---
title: Criar e carregar um VHD do Ubuntu Linux no Azure
description: "Saiba como criar e carregar um disco rígido virtual (VHD) do Azure que contém o sistema operacional Ubuntu Linux."
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
ms.openlocfilehash: 4496b34ff88ca1e08cc74788ae09d787d4399eaf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="prepare-an-ubuntu-virtual-machine-for-azure"></a><span data-ttu-id="0cc9d-103">Preparar uma máquina virtual do Ubuntu para o Azure</span><span class="sxs-lookup"><span data-stu-id="0cc9d-103">Prepare an Ubuntu virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="official-ubuntu-cloud-images"></a><span data-ttu-id="0cc9d-104">Imagens de nuvem oficiais do Ubuntu</span><span class="sxs-lookup"><span data-stu-id="0cc9d-104">Official Ubuntu cloud images</span></span>
<span data-ttu-id="0cc9d-105">O Ubuntu agora publica VHDs oficiais do Azure para download em [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/).</span><span class="sxs-lookup"><span data-stu-id="0cc9d-105">Ubuntu now publishes official Azure VHDs for download at [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/).</span></span> <span data-ttu-id="0cc9d-106">Se você precisar compilar sua própria imagem do Ubuntu especializada para o Azure, em vez de usar o procedimento manual abaixo, é recomendável começar com esses VHDs de trabalho conhecidos e personalizá-los conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="0cc9d-106">If you need to build your own specialized Ubuntu image for Azure, rather than use the manual procedure below it is recommended to start with these known working VHDs and customize as needed.</span></span> <span data-ttu-id="0cc9d-107">As versões mais recentes da imagem sempre podem ser encontradas nos seguintes locais:</span><span class="sxs-lookup"><span data-stu-id="0cc9d-107">The latest image releases can always be found at the following locations:</span></span>

* <span data-ttu-id="0cc9d-108">Ubuntu 12.04/Precise: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="0cc9d-108">Ubuntu 12.04/Precise: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="0cc9d-109">Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="0cc9d-109">Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="0cc9d-110">Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="0cc9d-110">Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0cc9d-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0cc9d-111">Prerequisites</span></span>
<span data-ttu-id="0cc9d-112">Este artigo pressupõe que você já instalou um sistema operacional Ubuntu Linux em um disco rígido virtual.</span><span class="sxs-lookup"><span data-stu-id="0cc9d-112">This article assumes that you have already installed an Ubuntu Linux operating system to a virtual hard disk.</span></span> <span data-ttu-id="0cc9d-113">Existem várias ferramentas para criar arquivos .vhd, por exemplo, uma solução de virtualização como o Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="0cc9d-113">Multiple tools exist to create .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="0cc9d-114">Para obter instruções, consulte [Instalar a função Hyper-V e configurar uma máquina Virtual](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="0cc9d-114">For instructions, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="0cc9d-115">**Notas de instalação do Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="0cc9d-115">**Ubuntu installation notes**</span></span>

* <span data-ttu-id="0cc9d-116">Veja também as [Notas de instalação gerais do Linux](create-upload-generic.md#general-linux-installation-notes) para obter mais dicas sobre como preparar o Linux para o Azure.</span><span class="sxs-lookup"><span data-stu-id="0cc9d-116">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="0cc9d-117">O formato VHDX não tem suporte no Azure, somente o **VHD fixo**.</span><span class="sxs-lookup"><span data-stu-id="0cc9d-117">The VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="0cc9d-118">Você pode converter o disco em formato VHD usando o Gerenciador do Hyper-V ou o cmdlet convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="0cc9d-118">You can convert the disk to VHD format using Hyper-V Manager or the convert-vhd cmdlet.</span></span>
* <span data-ttu-id="0cc9d-119">Ao instalar o sistema Linux, é recomendável que você use partições padrão em vez de LVM (geralmente o padrão para muitas instalações).</span><span class="sxs-lookup"><span data-stu-id="0cc9d-119">When installing the Linux system it is recommended that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="0cc9d-120">Isso irá evitar conflitos de nome LVM com VMs clonadas, especialmente se um disco do sistema operacional precisar ser anexado a outra VM para solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="0cc9d-120">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another VM for troubleshooting.</span></span> <span data-ttu-id="0cc9d-121">Se você preferir, é possível usar [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) em discos de dados.</span><span class="sxs-lookup"><span data-stu-id="0cc9d-121">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="0cc9d-122">Não configure uma partição de permuta no disco do SO.</span><span class="sxs-lookup"><span data-stu-id="0cc9d-122">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="0cc9d-123">O agente Linux pode ser configurado para criar um arquivo de permuta no disco de recursos temporários.</span><span class="sxs-lookup"><span data-stu-id="0cc9d-123">The Linux agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="0cc9d-124">Verifique as etapas a seguir para obter mais informações a esse respeito.</span><span class="sxs-lookup"><span data-stu-id="0cc9d-124">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="0cc9d-125">Todos os VHDs devem ter tamanhos que sejam múltiplos de 1 MB.</span><span class="sxs-lookup"><span data-stu-id="0cc9d-125">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="manual-steps"></a><span data-ttu-id="0cc9d-126">Etapas manuais</span><span class="sxs-lookup"><span data-stu-id="0cc9d-126">Manual steps</span></span>
> [!NOTE]
> <span data-ttu-id="0cc9d-127">Antes de tentar criar sua própria imagem personalizada do Ubuntu para o Azure, considere usar as imagens criadas previamente e testadas de [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) em vez disso.</span><span class="sxs-lookup"><span data-stu-id="0cc9d-127">Before attempting to create your own custom Ubuntu image for Azure, please consider using the pre-built and tested images from [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) instead.</span></span>
> 
> 

1. <span data-ttu-id="0cc9d-128">No painel central do Gerenciador do Hyper-V, selecione a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0cc9d-128">In the center pane of Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="0cc9d-129">Clique em **Conectar** para abrir a janela da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0cc9d-129">Click **Connect** to open the window for the virtual machine.</span></span>

3. <span data-ttu-id="0cc9d-130">Substitua os repositórios atuais na imagem para usar os repositórios do Azure no Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="0cc9d-130">Replace the current repositories in the image to use Ubuntu's Azure repos.</span></span> <span data-ttu-id="0cc9d-131">As etapas variam um pouco dependendo da versão do Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="0cc9d-131">The steps vary slightly depending on the Ubuntu version.</span></span>
   
    <span data-ttu-id="0cc9d-132">Antes de editar `/etc/apt/sources.list`, é recomendável fazer um backup:</span><span class="sxs-lookup"><span data-stu-id="0cc9d-132">Before editing `/etc/apt/sources.list`, it is recommended to make a backup:</span></span>
   
        # sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak

    <span data-ttu-id="0cc9d-133">Ubuntu 12,04:</span><span class="sxs-lookup"><span data-stu-id="0cc9d-133">Ubuntu 12.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="0cc9d-134">Ubuntu 14.04:</span><span class="sxs-lookup"><span data-stu-id="0cc9d-134">Ubuntu 14.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="0cc9d-135">Ubuntu 16.04:</span><span class="sxs-lookup"><span data-stu-id="0cc9d-135">Ubuntu 16.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

4. <span data-ttu-id="0cc9d-136">As imagens do Ubuntu Azure estão seguindo o kernel *Habilitação de Hardware* (HWE).</span><span class="sxs-lookup"><span data-stu-id="0cc9d-136">The Ubuntu Azure images are now following the *hardware enablement* (HWE) kernel.</span></span> <span data-ttu-id="0cc9d-137">Atualize o sistema operacional para o kernel mais recente, executando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="0cc9d-137">Update the operating system to the latest kernel by running the following commands:</span></span>

    <span data-ttu-id="0cc9d-138">Ubuntu 12,04:</span><span class="sxs-lookup"><span data-stu-id="0cc9d-138">Ubuntu 12.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-generic-lts-trusty linux-cloud-tools-generic-lts-trusty
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot
   
    <span data-ttu-id="0cc9d-139">Ubuntu 14.04:</span><span class="sxs-lookup"><span data-stu-id="0cc9d-139">Ubuntu 14.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-virtual-lts-vivid linux-lts-vivid-tools-common
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot

    <span data-ttu-id="0cc9d-140">Ubuntu 16.04:</span><span class="sxs-lookup"><span data-stu-id="0cc9d-140">Ubuntu 16.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-generic-hwe-16.04 linux-cloud-tools-generic-hwe-16.04
        (recommended) sudo apt-get dist-upgrade

        # sudo reboot

    <span data-ttu-id="0cc9d-141">**Consulte também:**</span><span class="sxs-lookup"><span data-stu-id="0cc9d-141">**See also:**</span></span>
    - [<span data-ttu-id="0cc9d-142">https://wiki.ubuntu.com/Kernel/LTSEnablementStack</span><span class="sxs-lookup"><span data-stu-id="0cc9d-142">https://wiki.ubuntu.com/Kernel/LTSEnablementStack</span></span>](https://wiki.ubuntu.com/Kernel/LTSEnablementStack)
    - [<span data-ttu-id="0cc9d-143">https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack</span><span class="sxs-lookup"><span data-stu-id="0cc9d-143">https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack</span></span>](https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack)


5. <span data-ttu-id="0cc9d-144">Modifique a linha de inicialização para o Grub para incluir parâmetros adicionais de kernel para o Azure.</span><span class="sxs-lookup"><span data-stu-id="0cc9d-144">Modify the kernel boot line for Grub to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="0cc9d-145">Para fazer isso, abra `/etc/default/grub` em um editor de texto, localize a variável chamada `GRUB_CMDLINE_LINUX_DEFAULT` (ou adicione-a, se necessário) e edite-a para incluir os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="0cc9d-145">To do this open `/etc/default/grub` in a text editor, find the variable called `GRUB_CMDLINE_LINUX_DEFAULT` (or add it if needed) and edit it to include the following parameters:</span></span>
   
        GRUB_CMDLINE_LINUX_DEFAULT="console=tty1 console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300"

    <span data-ttu-id="0cc9d-146">Salve e feche esse arquivo e execute `sudo update-grub`.</span><span class="sxs-lookup"><span data-stu-id="0cc9d-146">Save and close this file, and then run `sudo update-grub`.</span></span> <span data-ttu-id="0cc9d-147">Isso garantirá que todas as mensagens do console sejam enviadas para a primeira porta serial, que pode auxiliar o suporte técnico do Azure com problemas de depuração.</span><span class="sxs-lookup"><span data-stu-id="0cc9d-147">This will ensure all console messages are sent to the first serial port, which can assist Azure technical support with debugging issues.</span></span>

6. <span data-ttu-id="0cc9d-148">Confira se o servidor SSH está instalado e configurado para iniciar no tempo de inicialização.</span><span class="sxs-lookup"><span data-stu-id="0cc9d-148">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="0cc9d-149">Geralmente, esse é o padrão.</span><span class="sxs-lookup"><span data-stu-id="0cc9d-149">This is usually the default.</span></span>

7. <span data-ttu-id="0cc9d-150">Instale o Agente Linux do Azure:</span><span class="sxs-lookup"><span data-stu-id="0cc9d-150">Install the Azure Linux Agent:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install walinuxagent

    >[!Note]
    <span data-ttu-id="0cc9d-151">O `walinuxagent` pacote pode remover o `NetworkManager` e `NetworkManager-gnome` pacotes, se estiverem instalados.</span><span class="sxs-lookup"><span data-stu-id="0cc9d-151">The `walinuxagent` package may remove the `NetworkManager` and `NetworkManager-gnome` packages, if they are installed.</span></span>

8. <span data-ttu-id="0cc9d-152">Execute os comandos a seguir para desprovisionar a máquina virtual e prepará-la para provisionamento no Azure:</span><span class="sxs-lookup"><span data-stu-id="0cc9d-152">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

9. <span data-ttu-id="0cc9d-153">Clique em **Ação -> Desligar** no Gerenciador do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="0cc9d-153">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="0cc9d-154">Agora, seu VHD Linux está pronto para ser carregado no Azure.</span><span class="sxs-lookup"><span data-stu-id="0cc9d-154">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0cc9d-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0cc9d-155">Next steps</span></span>
<span data-ttu-id="0cc9d-156">Agora, você está pronto para usar o disco rígido virtual Ubuntu Linux para criar novas máquinas virtuais no Azure.</span><span class="sxs-lookup"><span data-stu-id="0cc9d-156">You're now ready to use your Ubuntu Linux virtual hard disk to create new virtual machines in Azure.</span></span> <span data-ttu-id="0cc9d-157">Se esta for a primeira vez que você estiver carregando o arquivo .vhd para o Azure, veja as etapas 2 e 3 em [Criando e carregando um disco rígido virtual que contém o sistema operacional Linux](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0cc9d-157">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="references"></a><span data-ttu-id="0cc9d-158">Referências</span><span class="sxs-lookup"><span data-stu-id="0cc9d-158">References</span></span>
<span data-ttu-id="0cc9d-159">Kernel de Habilitação de Hardware do Ubuntu (HWE):</span><span class="sxs-lookup"><span data-stu-id="0cc9d-159">Ubuntu hardware enablement (HWE) kernel:</span></span>

* [<span data-ttu-id="0cc9d-160">http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html</span><span class="sxs-lookup"><span data-stu-id="0cc9d-160">http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html</span></span>](http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html)
* [<span data-ttu-id="0cc9d-161">http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html</span><span class="sxs-lookup"><span data-stu-id="0cc9d-161">http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html</span></span>](http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html)

