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
# <a name="prepare-a-debian-vhd-for-azure"></a>Preparar um VHD do Debian para o Azure
## <a name="prerequisites"></a>Pré-requisitos
Esta seção pressupõe que você já instalou um sistema operacional Linux Debian de um arquivo. ISO baixado da saudação [site Debian](https://www.debian.org/distrib/) tooa do disco rígido virtual. Várias ferramentas existem toocreate arquivos. vhd; Hyper-V é apenas um exemplo. Para obter instruções sobre como usar o Hyper-V, consulte [instalar Olá função Hyper-V e configurar uma máquina Virtual](https://technet.microsoft.com/library/hh846766.aspx).

## <a name="installation-notes"></a>Notas de instalação
* Veja também as [Notas de instalação gerais do Linux](create-upload-generic.md#general-linux-installation-notes) para obter mais dicas sobre como preparar o Linux para o Azure.
* Não há suporte para o formato VHDX mais recente de saudação no Azure. Você pode converter o formato de tooVHD Olá de disco usando o Gerenciador do Hyper-V ou Olá **convert-vhd** cmdlet.
* Ao instalar o sistema de Linux Olá é recomendável que você use partições padrão em vez de LVM (geralmente padrão Olá para muitas instalações). Isso evitará LVM nome conflita com VMs clonados, especialmente se um sistema operacional de disco nunca precisa tooanother toobe anexado VMs para solução de problemas. Se você preferir, é possível usar [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) em discos de dados.
* Não configure uma partição de troca no disco do sistema operacional hello. agente do Linux Azure Olá pode ser configurado toocreate um arquivo de permuta em disco de recursos temporário hello. Para obter mais informações sobre isso podem ser encontradas nas etapas de saudação abaixo.
* Todos os VHDs Olá devem ter tamanhos que sejam múltiplos de 1 MB.

## <a name="use-azure-manage-toocreate-debian-vhds"></a>Usar toocreate de gerenciar o Azure Debian VHDs
Há ferramentas disponíveis para a geração de Debian VHDs do Azure, como Olá [azure-gerenciar](https://github.com/credativ/azure-manage) scripts de [credativ](http://www.credativ.com/). Isso é hello recomendado abordagem em vez de criar uma imagem a partir do zero. Por exemplo, toocreate um VHD 8 Debian executar hello azure-gerenciar toodownload de comandos a seguir (e dependências) e executar o script de azure_build_image hello:

    # sudo apt-get update
    # sudo apt-get install git qemu-utils mbr kpartx debootstrap

    # sudo apt-get install python3-pip python3-dateutil python3-cryptography
    # sudo pip3 install azure-storage azure-servicemanagement-legacy azure-common pytest pyyaml
    # git clone https://github.com/credativ/azure-manage.git
    # cd azure-manage
    # sudo pip3 install .

    # sudo azure_build_image --option release=jessie --option image_size_gb=30 --option image_prefix=debian-jessie-azure section


## <a name="manually-prepare-a-debian-vhd"></a>Preparar manualmente um VHD do Debian
1. No Gerenciador do Hyper-V, selecione máquina virtual de saudação.
2. Clique em **conectar** tooopen uma janela do console da máquina virtual de saudação.
3. Comente a linha hello para **deb cdrom** em `/etc/apt/source.list` se você configurar Olá VM em relação a um arquivo ISO.
4. Editar saudação `/etc/default/grub` de arquivo e modificar Olá **GRUB_CMDLINE_LINUX** parâmetro da seguinte maneira tooinclude parâmetros de kernel adicionais do Azure.
   
        GRUB_CMDLINE_LINUX="console=tty0 console=ttyS0,115200 earlyprintk=ttyS0,115200 rootdelay=30"
5. Recriar grub hello e execute:
   
        # sudo update-grub
6. Adicione Azure repositórios too/etc/apt/sources.list do Debian para Debian 7 ou 8:
   
    **Debian 7.x "Wheezy"**
   
        deb http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb-src http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure wheezy main
        deb-src http://debian-archive.trafficmanager.net/debian-azure wheezy main

    **Debian 8.x "Jessie"**

        deb http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb-src http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure jessie main
        deb-src http://debian-archive.trafficmanager.net/debian-azure jessie main


1. Instale Olá agente Linux do Azure:
   
        # sudo apt-get update
        # sudo apt-get install waagent
2. Debian 7, é kernel de baseado em 3.16 Olá toorun necessária do repositório de wheezy backports hello. Primeiro, crie um arquivo chamado /etc/apt/preferences.d/linux.pref com hello conteúdo a seguir:
   
        Package: linux-image-amd64 initramfs-tools
        Pin: release n=wheezy-backports
        Pin-Priority: 500
   
    Em seguida, execute "apt sudo get instalar linux-imagem-amd64" tooinstall hello novo kernel.
3. Cancelar o provisionamento de máquina virtual de saudação e prepará-la para provisionamento no Azure e execute:
   
        # sudo waagent –force -deprovision
        # export HISTSIZE=0
        # logout
4. Clique em **Ação** -> Desligar no Gerenciador do Hyper-V. O VHD Linux está agora pronto toobe carregado tooAzure.

## <a name="next-steps"></a>Próximas etapas
Você está agora pronto toouse seu Debian disco rígido virtual toocreate novas máquinas virtuais no Azure. Se isso for Olá primeira vez que você está carregando tooAzure de arquivo. vhd hello, consulte as etapas 2 e 3 em [criando e carregando um disco rígido virtual que contém o sistema de operacional Linux Olá](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

