---
title: Preparar um VHD do Debian Linux no Azure | Microsoft Docs
description: "Aprenda a criar arquivos VHD no Debian 7 e 8 para implantação no Azure."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: a6de7a7c-cc70-44e7-aed0-2ae6884d401a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 63970d162c12984d6476bf0b9fc4ab70160eccdb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-a-debian-vhd-for-azure"></a><span data-ttu-id="7880c-103">Preparar um VHD do Debian para o Azure</span><span class="sxs-lookup"><span data-stu-id="7880c-103">Prepare a Debian VHD for Azure</span></span>
## <a name="prerequisites"></a><span data-ttu-id="7880c-104">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7880c-104">Prerequisites</span></span>
<span data-ttu-id="7880c-105">Esta seção pressupõe que você já instalou um sistema operacional Linux Debian a partir de um arquivo .iso baixado do [site do Debian](https://www.debian.org/distrib/) para um disco rígido virtual.</span><span class="sxs-lookup"><span data-stu-id="7880c-105">This section assumes that you have already installed a Debian Linux operating system from an .iso file downloaded from the [Debian website](https://www.debian.org/distrib/) to a virtual hard disk.</span></span> <span data-ttu-id="7880c-106">Existem várias ferramentas para criar arquivos .vhd; Hyper-V é apenas um exemplo.</span><span class="sxs-lookup"><span data-stu-id="7880c-106">Multiple tools exist to create .vhd files; Hyper-V is only one example.</span></span> <span data-ttu-id="7880c-107">Para obter instruções sobre como usar a Hyper-V, consulte [Instalar a função Hyper-V e configurar uma máquina Virtual](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="7880c-107">For instructions using Hyper-V, see [Install the Hyper-V Role and Configure a Virtual Machine](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

## <a name="installation-notes"></a><span data-ttu-id="7880c-108">Notas de instalação</span><span class="sxs-lookup"><span data-stu-id="7880c-108">Installation notes</span></span>
* <span data-ttu-id="7880c-109">Veja também [Notas de instalação gerais do Linux](create-upload-generic.md#general-linux-installation-notes) para obter mais dicas sobre como preparar o Linux para o Azure.</span><span class="sxs-lookup"><span data-stu-id="7880c-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="7880c-110">Não há suporte para o formato VHDX mais recente no Azure.</span><span class="sxs-lookup"><span data-stu-id="7880c-110">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="7880c-111">Você pode converter o disco em formato VHD usando o Gerenciador do Hyper-V ou o cmdlet **convert-vhd** .</span><span class="sxs-lookup"><span data-stu-id="7880c-111">You can convert the disk to VHD format using Hyper-V Manager or the **convert-vhd** cmdlet.</span></span>
* <span data-ttu-id="7880c-112">Ao instalar o sistema Linux, é recomendável que você use partições padrão em vez de LVM (geralmente o padrão para muitas instalações).</span><span class="sxs-lookup"><span data-stu-id="7880c-112">When installing the Linux system it is recommended that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="7880c-113">Isso irá evitar conflitos de nome LVM com VMs clonadas, especialmente se um disco do sistema operacional precisar ser anexado a outra VM para solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="7880c-113">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another VM for troubleshooting.</span></span> <span data-ttu-id="7880c-114">Se você preferir, é possível usar [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) em discos de dados.</span><span class="sxs-lookup"><span data-stu-id="7880c-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="7880c-115">Não configure uma partição de permuta no disco do SO.</span><span class="sxs-lookup"><span data-stu-id="7880c-115">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="7880c-116">O agente Linux do Azure pode ser configurado para criar um arquivo de permuta no disco de recursos temporários.</span><span class="sxs-lookup"><span data-stu-id="7880c-116">The Azure Linux agent can be configured to create a swap file on the temporary resource disk.</span></span> <span data-ttu-id="7880c-117">Verifique as etapas a seguir para obter mais informações a esse respeito.</span><span class="sxs-lookup"><span data-stu-id="7880c-117">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="7880c-118">Todos os VHDs devem ter tamanhos que sejam múltiplos de 1 MB.</span><span class="sxs-lookup"><span data-stu-id="7880c-118">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="use-azure-manage-to-create-debian-vhds"></a><span data-ttu-id="7880c-119">Usar o gerenciamento do Azure para criar VHDs Debian</span><span class="sxs-lookup"><span data-stu-id="7880c-119">Use Azure-Manage to create Debian VHDs</span></span>
<span data-ttu-id="7880c-120">Existem ferramentas disponíveis para gerar VHDs Debian para o Azure, como os scripts [azure-manage](https://github.com/credativ/azure-manage) do [credativ](http://www.credativ.com/).</span><span class="sxs-lookup"><span data-stu-id="7880c-120">There are tools available for generating Debian VHDs for Azure, such as the [azure-manage](https://github.com/credativ/azure-manage) scripts from [credativ](http://www.credativ.com/).</span></span> <span data-ttu-id="7880c-121">Essa é a abordagem recomendada em vez de criar uma imagem do zero.</span><span class="sxs-lookup"><span data-stu-id="7880c-121">This is the recommended approach versus creating an image from scratch.</span></span> <span data-ttu-id="7880c-122">Por exemplo, para criar um VHD no Debian 8, execute os seguintes comandos para baixar o gerenciamento do Azure (e dependências) e execute o script azure_build_image:</span><span class="sxs-lookup"><span data-stu-id="7880c-122">For example, to create a Debian 8 VHD run the following commands to download azure-manage (and dependencies) and run the azure_build_image script:</span></span>

    # sudo apt-get update
    # sudo apt-get install git qemu-utils mbr kpartx debootstrap

    # sudo apt-get install python3-pip python3-dateutil python3-cryptography
    # sudo pip3 install azure-storage azure-servicemanagement-legacy azure-common pytest pyyaml
    # git clone https://github.com/credativ/azure-manage.git
    # cd azure-manage
    # sudo pip3 install .

    # sudo azure_build_image --option release=jessie --option image_size_gb=30 --option image_prefix=debian-jessie-azure section


## <a name="manually-prepare-a-debian-vhd"></a><span data-ttu-id="7880c-123">Preparar manualmente um VHD do Debian</span><span class="sxs-lookup"><span data-stu-id="7880c-123">Manually prepare a Debian VHD</span></span>
1. <span data-ttu-id="7880c-124">No Gerenciador do Hyper-V, selecione a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7880c-124">In Hyper-V Manager, select the virtual machine.</span></span>
2. <span data-ttu-id="7880c-125">Clique em **Conectar** para abrir a janela do console para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7880c-125">Click **Connect** to open a console window for the virtual machine.</span></span>
3. <span data-ttu-id="7880c-126">Comente a linha para **deb cdrom** na `/etc/apt/source.list` se você configurar a VM relacionada a um arquivo ISO.</span><span class="sxs-lookup"><span data-stu-id="7880c-126">Comment out the line for **deb cdrom** in `/etc/apt/source.list` if you set up the VM against an ISO file.</span></span>
4. <span data-ttu-id="7880c-127">Edite o arquivo `/etc/default/grub` e modifique o parâmetro **GRUB_CMDLINE_LINUX** da seguinte maneira para incluir parâmetros adicionais de kernel para o Azure.</span><span class="sxs-lookup"><span data-stu-id="7880c-127">Edit the `/etc/default/grub` file and modify the **GRUB_CMDLINE_LINUX** parameter as follows to include additional kernel parameters for Azure.</span></span>
   
        GRUB_CMDLINE_LINUX="console=tty0 console=ttyS0,115200 earlyprintk=ttyS0,115200 rootdelay=30"
5. <span data-ttu-id="7880c-128">Recompile o grub e execute:</span><span class="sxs-lookup"><span data-stu-id="7880c-128">Rebuild the grub and run:</span></span>
   
        # sudo update-grub
6. <span data-ttu-id="7880c-129">Adicione repositórios do Azure do Debian a /etc/apt/sources.list para Debian 7 ou 8:</span><span class="sxs-lookup"><span data-stu-id="7880c-129">Add Debian's Azure repositories to /etc/apt/sources.list for either Debian 7 or 8:</span></span>
   
    <span data-ttu-id="7880c-130">**Debian 7.x "Wheezy"**</span><span class="sxs-lookup"><span data-stu-id="7880c-130">**Debian 7.x "Wheezy"**</span></span>
   
        deb http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb-src http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure wheezy main
        deb-src http://debian-archive.trafficmanager.net/debian-azure wheezy main

    <span data-ttu-id="7880c-131">**Debian 8.x "Jessie"**</span><span class="sxs-lookup"><span data-stu-id="7880c-131">**Debian 8.x "Jessie"**</span></span>

        deb http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb-src http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure jessie main
        deb-src http://debian-archive.trafficmanager.net/debian-azure jessie main


1. <span data-ttu-id="7880c-132">Instale o Agente Linux do Azure:</span><span class="sxs-lookup"><span data-stu-id="7880c-132">Install the Azure Linux Agent:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install waagent
2. <span data-ttu-id="7880c-133">Para o Debian 7, é necessário executar o kernel baseado no 3.16 do repositório de backports do wheezy.</span><span class="sxs-lookup"><span data-stu-id="7880c-133">For Debian 7, it is required to run the 3.16-based kernel from the wheezy-backports repository.</span></span> <span data-ttu-id="7880c-134">Primeiro, crie um arquivo chamado /etc/apt/preferences.d/linux.pref com o seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="7880c-134">First create a file called /etc/apt/preferences.d/linux.pref with the following contents:</span></span>
   
        Package: linux-image-amd64 initramfs-tools
        Pin: release n=wheezy-backports
        Pin-Priority: 500
   
    <span data-ttu-id="7880c-135">Em seguida, execute "sudo apt-get install linux-image-amd64" para instalar o novo kernel.</span><span class="sxs-lookup"><span data-stu-id="7880c-135">Then run "sudo apt-get install linux-image-amd64" to install the new kernel.</span></span>
3. <span data-ttu-id="7880c-136">Desprovisione a máquina virtual, prepare-a para provisionamento no Azure e execute:</span><span class="sxs-lookup"><span data-stu-id="7880c-136">Deprovision the virtual machine and prepare it for provisioning on Azure and run:</span></span>
   
        # sudo waagent –force -deprovision
        # export HISTSIZE=0
        # logout
4. <span data-ttu-id="7880c-137">Clique em **Ação** -> Desligar no Gerenciador do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="7880c-137">Click **Action** -> Shut Down in Hyper-V Manager.</span></span> <span data-ttu-id="7880c-138">Agora, seu VHD Linux está pronto para ser carregado no Azure.</span><span class="sxs-lookup"><span data-stu-id="7880c-138">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7880c-139">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7880c-139">Next steps</span></span>
<span data-ttu-id="7880c-140">Agora, você está pronto para usar o disco rígido virtual Debian para criar novas máquinas virtuais no Azure.</span><span class="sxs-lookup"><span data-stu-id="7880c-140">You're now ready to use your Debian virtual hard disk to create new virtual machines in Azure.</span></span> <span data-ttu-id="7880c-141">Se esta for a primeira vez que você estiver carregando o arquivo .vhd para o Azure, veja as etapas 2 e 3 em [Criando e carregando um disco rígido virtual que contém o sistema operacional Linux](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7880c-141">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

