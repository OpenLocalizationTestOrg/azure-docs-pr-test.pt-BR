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
# <a name="prepare-an-ubuntu-virtual-machine-for-azure"></a>Preparar uma máquina virtual do Ubuntu para o Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="official-ubuntu-cloud-images"></a>Imagens de nuvem oficiais do Ubuntu
O Ubuntu agora publica VHDs oficiais do Azure para download em [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/). Se precisar toobuild sua própria imagem Ubuntu especializada para o Azure em vez de usar o procedimento manual de saudação abaixo dele é recomendado toostart com esses conhecidos trabalhando VHDs e personalizar conforme necessário. as versões mais recentes de imagem Olá sempre podem ser encontradas em Olá locais a seguir:

* Ubuntu 12.04/Precise: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)
* Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)
* Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)

## <a name="prerequisites"></a>Pré-requisitos
Este artigo pressupõe que você já tiver instalado um disco rígido virtual Ubuntu Linux sistema operacional tooa. Várias ferramentas existem toocreate arquivos. vhd, por exemplo, uma solução de virtualização como o Hyper-V. Para obter instruções, consulte [instalar Olá função Hyper-V e configurar uma máquina Virtual](http://technet.microsoft.com/library/hh846766.aspx).

**Notas de instalação do Ubuntu**

* Veja também as [Notas de instalação gerais do Linux](create-upload-generic.md#general-linux-installation-notes) para obter mais dicas sobre como preparar o Linux para o Azure.
* formato do Hello VHDX não tem suporte apenas no Azure, **VHD fixo**.  Você pode converter Olá disco tooVHD formato usando o Gerenciador do Hyper-V ou Olá cmdlet convert-vhd.
* Ao instalar o sistema de Linux Olá é recomendável que você use partições padrão em vez de LVM (geralmente padrão Olá para muitas instalações). Isso evitará LVM nome conflita com VMs clonados, especialmente se um sistema operacional de disco nunca precisa tooanother toobe anexado VMs para solução de problemas. Se você preferir, é possível usar [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) em discos de dados.
* Não configure uma partição de troca no disco do sistema operacional hello. agente do Linux Olá pode ser configurado toocreate um arquivo de permuta em disco de recursos temporário hello.  Para obter mais informações sobre isso podem ser encontradas nas etapas de saudação abaixo.
* Todos os VHDs Olá devem ter tamanhos que sejam múltiplos de 1 MB.

## <a name="manual-steps"></a>Etapas manuais
> [!NOTE]
> Antes de tentar toocreate sua própria imagem Ubuntu personalizada do Azure, considere usar Olá previamente criados e testados imagens de [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) em vez disso.
> 
> 

1. No painel central de saudação do Gerenciador do Hyper-V, selecione máquina virtual de saudação.

2. Clique em **conectar** tooopen janela de saudação para a máquina virtual de saudação.

3. Substitua os repositórios de saudação atual no repositório do Azure do hello imagem toouse Ubuntu. etapas Olá variam um pouco dependendo da versão do Ubuntu hello.
   
    Antes de editar `/etc/apt/sources.list`, é recomendável toomake um backup:
   
        # sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak

    Ubuntu 12,04:
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    Ubuntu 14.04:
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    Ubuntu 16.04:
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

4. Olá imagens Ubuntu Azure estão seguindo Olá *habilitação de hardware* kernel (HWE). Atualize o kernel do mais recente de toohello do sistema operacional Olá executando Olá comandos a seguir:

    Ubuntu 12,04:
   
        # sudo apt-get update
        # sudo apt-get install linux-image-generic-lts-trusty linux-cloud-tools-generic-lts-trusty
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot
   
    Ubuntu 14.04:
   
        # sudo apt-get update
        # sudo apt-get install linux-image-virtual-lts-vivid linux-lts-vivid-tools-common
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot

    Ubuntu 16.04:
   
        # sudo apt-get update
        # sudo apt-get install linux-generic-hwe-16.04 linux-cloud-tools-generic-hwe-16.04
        (recommended) sudo apt-get dist-upgrade

        # sudo reboot

    **Consulte também:**
    - [https://wiki.ubuntu.com/Kernel/LTSEnablementStack](https://wiki.ubuntu.com/Kernel/LTSEnablementStack)
    - [https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack](https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack)


5. Modificar a linha de inicialização de kernel de saudação para parâmetros de kernel adicionais tooinclude Grub do Azure. toodo nesse abrir `/etc/default/grub` em um editor de texto, localizar variável Olá chamado `GRUB_CMDLINE_LINUX_DEFAULT` (ou adicioná-lo se necessário) e edite-Olá tooinclude parâmetros a seguir:
   
        GRUB_CMDLINE_LINUX_DEFAULT="console=tty1 console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300"

    Salve e feche esse arquivo e execute `sudo update-grub`. Isso garantirá que todas as mensagens de console são enviadas toohello primeira porta serial, que pode ajudar o suporte técnico do Azure com problemas de depuração.

6. Certifique-se de servidor SSH hello está instalado e configurado toostart no momento da inicialização.  Geralmente, esse é o padrão de saudação.

7. Instale Olá agente Linux do Azure:
   
        # sudo apt-get update
        # sudo apt-get install walinuxagent

    >[!Note]
    Olá `walinuxagent` pacote pode remover Olá `NetworkManager` e `NetworkManager-gnome` pacotes, se eles estiverem instalados.

8. Execute Olá seguindo a máquina virtual do comandos toodeprovision hello e prepará-la para provisionamento no Azure:
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

9. Clique em **Ação -> Desligar** no Gerenciador do Hyper-V. O VHD Linux está agora pronto toobe carregado tooAzure.

## <a name="next-steps"></a>Próximas etapas
Você está agora pronto toouse seu Ubuntu Linux disco rígido virtual toocreate novas máquinas virtuais no Azure. Se isso for Olá primeira vez que você está carregando tooAzure de arquivo. vhd hello, consulte as etapas 2 e 3 em [criando e carregando um disco rígido virtual que contém o sistema de operacional Linux Olá](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="references"></a>Referências
Kernel de Habilitação de Hardware do Ubuntu (HWE):

* [http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html](http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html)
* [http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html](http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html)

