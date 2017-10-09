---
title: aaaPrepare um Debian Linux VHD no Azure | Microsoft Docs
description: "Saiba como arquivos de toocreate Debian 7 e 8 VHD para implantação no Azure."
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
ms.openlocfilehash: e67d126de3db146357a6509aedb5f478576768f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-debian-vhd-for-azure"></a><span data-ttu-id="ac63b-103">Preparar um VHD do Debian para o Azure</span><span class="sxs-lookup"><span data-stu-id="ac63b-103">Prepare a Debian VHD for Azure</span></span>
## <a name="prerequisites"></a><span data-ttu-id="ac63b-104">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ac63b-104">Prerequisites</span></span>
<span data-ttu-id="ac63b-105">Esta seção pressupõe que você já instalou um sistema operacional Linux Debian de um arquivo. ISO baixado da saudação [site Debian](https://www.debian.org/distrib/) tooa do disco rígido virtual.</span><span class="sxs-lookup"><span data-stu-id="ac63b-105">This section assumes that you have already installed a Debian Linux operating system from an .iso file downloaded from hello [Debian website](https://www.debian.org/distrib/) tooa virtual hard disk.</span></span> <span data-ttu-id="ac63b-106">Várias ferramentas existem toocreate arquivos. vhd; Hyper-V é apenas um exemplo.</span><span class="sxs-lookup"><span data-stu-id="ac63b-106">Multiple tools exist toocreate .vhd files; Hyper-V is only one example.</span></span> <span data-ttu-id="ac63b-107">Para obter instruções sobre como usar o Hyper-V, consulte [instalar Olá função Hyper-V e configurar uma máquina Virtual](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="ac63b-107">For instructions using Hyper-V, see [Install hello Hyper-V Role and Configure a Virtual Machine](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

## <a name="installation-notes"></a><span data-ttu-id="ac63b-108">Notas de instalação</span><span class="sxs-lookup"><span data-stu-id="ac63b-108">Installation notes</span></span>
* <span data-ttu-id="ac63b-109">Veja também as [Notas de instalação gerais do Linux](create-upload-generic.md#general-linux-installation-notes) para obter mais dicas sobre como preparar o Linux para o Azure.</span><span class="sxs-lookup"><span data-stu-id="ac63b-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="ac63b-110">Não há suporte para o formato VHDX mais recente de saudação no Azure.</span><span class="sxs-lookup"><span data-stu-id="ac63b-110">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="ac63b-111">Você pode converter o formato de tooVHD Olá de disco usando o Gerenciador do Hyper-V ou Olá **convert-vhd** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ac63b-111">You can convert hello disk tooVHD format using Hyper-V Manager or hello **convert-vhd** cmdlet.</span></span>
* <span data-ttu-id="ac63b-112">Ao instalar o sistema de Linux Olá é recomendável que você use partições padrão em vez de LVM (geralmente padrão Olá para muitas instalações).</span><span class="sxs-lookup"><span data-stu-id="ac63b-112">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="ac63b-113">Isso evitará LVM nome conflita com VMs clonados, especialmente se um sistema operacional de disco nunca precisa tooanother toobe anexado VMs para solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="ac63b-113">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="ac63b-114">Se você preferir, é possível usar [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) em discos de dados.</span><span class="sxs-lookup"><span data-stu-id="ac63b-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="ac63b-115">Não configure uma partição de troca no disco do sistema operacional hello.</span><span class="sxs-lookup"><span data-stu-id="ac63b-115">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="ac63b-116">agente do Linux Azure Olá pode ser configurado toocreate um arquivo de permuta em disco de recursos temporário hello.</span><span class="sxs-lookup"><span data-stu-id="ac63b-116">hello Azure Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span> <span data-ttu-id="ac63b-117">Para obter mais informações sobre isso podem ser encontradas nas etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="ac63b-117">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="ac63b-118">Todos os VHDs Olá devem ter tamanhos que sejam múltiplos de 1 MB.</span><span class="sxs-lookup"><span data-stu-id="ac63b-118">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="use-azure-manage-toocreate-debian-vhds"></a><span data-ttu-id="ac63b-119">Usar toocreate de gerenciar o Azure Debian VHDs</span><span class="sxs-lookup"><span data-stu-id="ac63b-119">Use Azure-Manage toocreate Debian VHDs</span></span>
<span data-ttu-id="ac63b-120">Há ferramentas disponíveis para a geração de Debian VHDs do Azure, como Olá [azure-gerenciar](https://github.com/credativ/azure-manage) scripts de [credativ](http://www.credativ.com/).</span><span class="sxs-lookup"><span data-stu-id="ac63b-120">There are tools available for generating Debian VHDs for Azure, such as hello [azure-manage](https://github.com/credativ/azure-manage) scripts from [credativ](http://www.credativ.com/).</span></span> <span data-ttu-id="ac63b-121">Isso é hello recomendado abordagem em vez de criar uma imagem a partir do zero.</span><span class="sxs-lookup"><span data-stu-id="ac63b-121">This is hello recommended approach versus creating an image from scratch.</span></span> <span data-ttu-id="ac63b-122">Por exemplo, toocreate um VHD 8 Debian executar hello azure-gerenciar toodownload de comandos a seguir (e dependências) e executar o script de azure_build_image hello:</span><span class="sxs-lookup"><span data-stu-id="ac63b-122">For example, toocreate a Debian 8 VHD run hello following commands toodownload azure-manage (and dependencies) and run hello azure_build_image script:</span></span>

    # sudo apt-get update
    # sudo apt-get install git qemu-utils mbr kpartx debootstrap

    # sudo apt-get install python3-pip python3-dateutil python3-cryptography
    # sudo pip3 install azure-storage azure-servicemanagement-legacy azure-common pytest pyyaml
    # git clone https://github.com/credativ/azure-manage.git
    # cd azure-manage
    # sudo pip3 install .

    # sudo azure_build_image --option release=jessie --option image_size_gb=30 --option image_prefix=debian-jessie-azure section


## <a name="manually-prepare-a-debian-vhd"></a><span data-ttu-id="ac63b-123">Preparar manualmente um VHD do Debian</span><span class="sxs-lookup"><span data-stu-id="ac63b-123">Manually prepare a Debian VHD</span></span>
1. <span data-ttu-id="ac63b-124">No Gerenciador do Hyper-V, selecione máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="ac63b-124">In Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="ac63b-125">Clique em **conectar** tooopen uma janela do console da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="ac63b-125">Click **Connect** tooopen a console window for hello virtual machine.</span></span>
3. <span data-ttu-id="ac63b-126">Comente a linha hello para **deb cdrom** em `/etc/apt/source.list` se você configurar Olá VM em relação a um arquivo ISO.</span><span class="sxs-lookup"><span data-stu-id="ac63b-126">Comment out hello line for **deb cdrom** in `/etc/apt/source.list` if you set up hello VM against an ISO file.</span></span>
4. <span data-ttu-id="ac63b-127">Editar saudação `/etc/default/grub` de arquivo e modificar Olá **GRUB_CMDLINE_LINUX** parâmetro da seguinte maneira tooinclude parâmetros de kernel adicionais do Azure.</span><span class="sxs-lookup"><span data-stu-id="ac63b-127">Edit hello `/etc/default/grub` file and modify hello **GRUB_CMDLINE_LINUX** parameter as follows tooinclude additional kernel parameters for Azure.</span></span>
   
        GRUB_CMDLINE_LINUX="console=tty0 console=ttyS0,115200 earlyprintk=ttyS0,115200 rootdelay=30"
5. <span data-ttu-id="ac63b-128">Recriar grub hello e execute:</span><span class="sxs-lookup"><span data-stu-id="ac63b-128">Rebuild hello grub and run:</span></span>
   
        # sudo update-grub
6. <span data-ttu-id="ac63b-129">Adicione Azure repositórios too/etc/apt/sources.list do Debian para Debian 7 ou 8:</span><span class="sxs-lookup"><span data-stu-id="ac63b-129">Add Debian's Azure repositories too/etc/apt/sources.list for either Debian 7 or 8:</span></span>
   
    <span data-ttu-id="ac63b-130">**Debian 7.x "Wheezy"**</span><span class="sxs-lookup"><span data-stu-id="ac63b-130">**Debian 7.x "Wheezy"**</span></span>
   
        deb http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb-src http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure wheezy main
        deb-src http://debian-archive.trafficmanager.net/debian-azure wheezy main

    <span data-ttu-id="ac63b-131">**Debian 8.x "Jessie"**</span><span class="sxs-lookup"><span data-stu-id="ac63b-131">**Debian 8.x "Jessie"**</span></span>

        deb http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb-src http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure jessie main
        deb-src http://debian-archive.trafficmanager.net/debian-azure jessie main


1. <span data-ttu-id="ac63b-132">Instale Olá agente Linux do Azure:</span><span class="sxs-lookup"><span data-stu-id="ac63b-132">Install hello Azure Linux Agent:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install waagent
2. <span data-ttu-id="ac63b-133">Debian 7, é kernel de baseado em 3.16 Olá toorun necessária do repositório de wheezy backports hello.</span><span class="sxs-lookup"><span data-stu-id="ac63b-133">For Debian 7, it is required toorun hello 3.16-based kernel from hello wheezy-backports repository.</span></span> <span data-ttu-id="ac63b-134">Primeiro, crie um arquivo chamado /etc/apt/preferences.d/linux.pref com hello conteúdo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ac63b-134">First create a file called /etc/apt/preferences.d/linux.pref with hello following contents:</span></span>
   
        Package: linux-image-amd64 initramfs-tools
        Pin: release n=wheezy-backports
        Pin-Priority: 500
   
    <span data-ttu-id="ac63b-135">Em seguida, execute "apt sudo get instalar linux-imagem-amd64" tooinstall hello novo kernel.</span><span class="sxs-lookup"><span data-stu-id="ac63b-135">Then run "sudo apt-get install linux-image-amd64" tooinstall hello new kernel.</span></span>
3. <span data-ttu-id="ac63b-136">Cancelar o provisionamento de máquina virtual de saudação e prepará-la para provisionamento no Azure e execute:</span><span class="sxs-lookup"><span data-stu-id="ac63b-136">Deprovision hello virtual machine and prepare it for provisioning on Azure and run:</span></span>
   
        # sudo waagent –force -deprovision
        # export HISTSIZE=0
        # logout
4. <span data-ttu-id="ac63b-137">Clique em **Ação** -> Desligar no Gerenciador do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="ac63b-137">Click **Action** -> Shut Down in Hyper-V Manager.</span></span> <span data-ttu-id="ac63b-138">O VHD Linux está agora pronto toobe carregado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ac63b-138">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac63b-139">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ac63b-139">Next steps</span></span>
<span data-ttu-id="ac63b-140">Você está agora pronto toouse seu Debian disco rígido virtual toocreate novas máquinas virtuais no Azure.</span><span class="sxs-lookup"><span data-stu-id="ac63b-140">You're now ready toouse your Debian virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="ac63b-141">Se isso for Olá primeira vez que você está carregando tooAzure de arquivo. vhd hello, consulte as etapas 2 e 3 em [criando e carregando um disco rígido virtual que contém o sistema de operacional Linux Olá](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ac63b-141">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

