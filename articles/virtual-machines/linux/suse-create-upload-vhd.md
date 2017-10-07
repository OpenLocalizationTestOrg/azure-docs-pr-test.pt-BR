---
title: aaaCreate e carregar um VHD do SUSE Linux no Azure
description: "Saiba toocreate e carregar um Azure disco rígido virtual (VHD) que contém um sistema operacional SUSE Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 066d01a6-2a54-4718-bcd0-90fe7a5303a1
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: szark
ms.openlocfilehash: 9185c7e67279357f00db0f43e944e96c58f0dd60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-sles-or-opensuse-virtual-machine-for-azure"></a>Preparar uma máquina virtual do SLES ou openSUSE para o Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a>Pré-requisitos
Este artigo pressupõe que você já instalou um SUSE ou openSUSE Linux tooa rígido disco do sistema operacional. Várias ferramentas existem toocreate arquivos. vhd, por exemplo, uma solução de virtualização como o Hyper-V. Para obter instruções, consulte [instalar Olá função Hyper-V e configurar uma máquina Virtual](http://technet.microsoft.com/library/hh846766.aspx).

### <a name="sles--opensuse-installation-notes"></a>Notas de instalação do SLES / openSUSE
* Veja também as [Notas de instalação gerais do Linux](create-upload-generic.md#general-linux-installation-notes) para obter mais dicas sobre como preparar o Linux para o Azure.
* formato do Hello VHDX não tem suporte apenas no Azure, **VHD fixo**.  Você pode converter Olá disco tooVHD formato usando o Gerenciador do Hyper-V ou Olá cmdlet convert-vhd.
* Ao instalar o sistema de Linux Olá é recomendável que você use partições padrão em vez de LVM (geralmente padrão Olá para muitas instalações). Isso evitará LVM nome conflita com VMs clonados, especialmente se um sistema operacional de disco nunca precisa tooanother toobe anexado VMs para solução de problemas. Se você preferir, é possível usar [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) em discos de dados.
* Não configure uma partição de troca no disco do sistema operacional hello. agente do Linux Olá pode ser configurado toocreate um arquivo de permuta em disco de recursos temporário hello.  Para obter mais informações sobre isso podem ser encontradas nas etapas de saudação abaixo.
* Todos os VHDs Olá devem ter tamanhos que sejam múltiplos de 1 MB.

## <a name="use-suse-studio"></a>Use o SUSE Studio
[SUSE Studio](http://www.susestudio.com) pode criar e gerenciar facilmente suas imagens SLES e openSUSE no Azure e no Hyper-V. Isso é hello abordagem para personalizar suas próprias imagens SLES e openSUSE recomendada.

Como uma alternativa toobuilding seu próprio VHD, SUSE também publica imagens BYOS (Traga sua própria assinatura) para SLES em [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007).

## <a name="prepare-suse-linux-enterprise-server-11-sp4"></a>Preparar o SUSE Linux Enterprise Server 11 SP4
1. No painel central de saudação do Gerenciador do Hyper-V, selecione máquina virtual de saudação.
2. Clique em **conectar** tooopen janela de saudação para a máquina virtual de saudação.
3. Registrar seu tooallow de sistema do SUSE Linux Enterprise-toodownload atualizações e pacotes de instalação.
4. Atualize o sistema de saudação com os patches mais recentes hello:
   
        # sudo zypper update
5. Instale hello Azure Linux Agent do repositório SLES hello:
   
        # sudo zypper install WALinuxAgent
6. Verifique se waagent está definido muito "no" comando chkconfig e se não, habilitá-la para iniciar automaticamente:
   
        # sudo chkconfig waagent on
7. Verifique se o serviço de waagent está sendo executado e se não, inicie-o: 
   
        # sudo service waagent start
8. Modificar a linha de inicialização de kernel de saudação em seus parâmetros de kernel adicionais tooinclude grub configuração do Azure. toodo nesse abra "/ boot/grub/menu.lst" em um editor de texto e certifique-se de que kernel de padrão de saudação inclui Olá parâmetros a seguir:
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
   
    Isso garantirá que todas as mensagens de console são enviadas toohello primeira porta serial, que pode ajudá-lo Azure suporte à depuração de problemas.
9. Confirme que fstab /boot/grub/menu.lst e/etc/ambos os disco de saudação de referência usando sua UUID (por uuid) em vez de ID do disco hello (por id). 
   
    Obter o UUID do disco
   
        # ls /dev/disk/by-uuid/
   
    Se /dev/disk/by-id é usado, atualizar fstab /boot/grub/menu.lst e/etc/com o valor de adequado por uuid de saudação
   
    Antes da alteração
   
        root=/dev/disk/by-id/SCSI-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxxx-part1
   
    Depois da alteração
   
        root=/dev/disk/by-uuid/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
10. Modificar udev regras tooavoid gerar regras estáticas para Olá interfaces Ethernet. Essas regras podem provocar problemas ao clonar uma máquina virtual no Microsoft Azure ou no Hyper-V:
    
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
11. É recomendável tooedit arquivo de hello "/ etc/sysconfig/rede/dhcp" e alterar Olá `DHCLIENT_SET_HOSTNAME` a seguir toohello parâmetro:
    
     DHCLIENT_SET_HOSTNAME="no"
12. Em "/ etc/sudoers", comente ou remova Olá linhas a seguir se eles existirem:
    
     Padrões targetpw # solicitará a senha de saudação do usuário de destino Olá raiz ou seja, todos os ALL=(ALL) todos # aviso! Deve ser usado somente em conjunto com 'Defaults targetpw'!
13. Certifique-se de servidor SSH hello está instalado e configurado toostart no momento da inicialização.  Geralmente, esse é o padrão de saudação.
14. Não crie espaço de permuta em disco do sistema operacional hello.
    
    Olá agente Linux do Azure pode configurar automaticamente o espaço de permuta usando Olá disco de recurso local que é anexado toohello VM após a configuração no Azure. Observe que esse disco de recurso local Olá é um *temporário* disco e pode ser esvaziada quando Olá VM for desprovisionada. Depois de instalar o hello agente Linux do Azure (consulte a etapa anterior), modifique Olá seguintes parâmetros em /etc/waagent.conf adequadamente:
    
     ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048; # nota: Defina esse toowhatever precisar toobe.
15. Execute Olá seguindo a máquina virtual do comandos toodeprovision hello e prepará-la para provisionamento no Azure:
    
    # <a name="sudo-waagent--force--deprovision"></a>sudo waagent -force -deprovision
    # <a name="export-histsize0"></a>export HISTSIZE=0
    # <a name="logout"></a>logout
16. Clique em **Ação -> Desligar** no Gerenciador do Hyper-V. O VHD Linux está agora pronto toobe carregado tooAzure.

- - -
## <a name="prepare-opensuse-131"></a>Preparar o openSUSE 13.1+
1. No painel central de saudação do Gerenciador do Hyper-V, selecione máquina virtual de saudação.
2. Clique em **conectar** tooopen janela de saudação para a máquina virtual de saudação.
3. Shell do hello, execute o comando de saudação '`zypper lr`'. Se esse comando retorna saída toohello semelhante a seguir, repositórios de saudação serão configurado conforme o esperado – sem ajustes são necessárias (Observe que os números de versão podem variar):
   
        # | Alias                 | Name                  | Enabled | Refresh
        --+-----------------------+-----------------------+---------+--------
        1 | Cloud:Tools_13.1      | Cloud:Tools_13.1      | Yes     | Yes
        2 | openSUSE_13.1_OSS     | openSUSE_13.1_OSS     | Yes     | Yes
        3 | openSUSE_13.1_Updates | openSUSE_13.1_Updates | Yes     | Yes
   
    Se o comando Olá não retorna "Nenhum repositório definido...", em seguida, use Olá tooadd comandos a seguir esses repositórios:
   
        # sudo zypper ar -f http://download.opensuse.org/repositories/Cloud:Tools/openSUSE_13.1 Cloud:Tools_13.1
        # sudo zypper ar -f http://download.opensuse.org/distribution/13.1/repo/oss openSUSE_13.1_OSS
        # sudo zypper ar -f http://download.opensuse.org/update/13.1 openSUSE_13.1_Updates
   
    Em seguida, você pode verificar a repositórios de saudação foram adicionados ao executar o comando de saudação '`zypper lr`' novamente. No caso de um dos repositórios de atualização relevante Olá não estiver habilitado, habilite-o com o seguinte comando:
   
        # sudo zypper mr -e [NUMBER OF REPOSITORY]
4. Atualize Olá kernel toohello versão mais recente disponível:
   
        # sudo zypper up kernel-default
   
    Sistema de saudação tooupdate com todos os patches mais recentes de saudação ou:
   
        # sudo zypper update
5. Instale Olá agente Linux do Azure.
   
   # <a name="sudo-zypper-install-walinuxagent"></a>sudo zypper install WALinuxAgent
6. Modificar a linha de inicialização de kernel de saudação em seus parâmetros de kernel adicionais tooinclude grub configuração do Azure. toodo isso, abra "/ boot/grub/menu.lst" em um editor de texto e certifique-se de que kernel de padrão de saudação inclui Olá parâmetros a seguir:
   
     console=ttyS0 earlyprintk=ttyS0 rootdelay=300
   
   Isso garantirá que todas as mensagens de console são enviadas toohello primeira porta serial, que pode ajudá-lo Azure suporte à depuração de problemas. Além disso, remova Olá seguir parâmetros de linha de inicialização do kernel Olá se existirem:
   
     libata.atapi_enabled=0 reserve=0x1f0,0x8
7. É recomendável tooedit arquivo de hello "/ etc/sysconfig/rede/dhcp" e alterar Olá `DHCLIENT_SET_HOSTNAME` a seguir toohello parâmetro:
   
     DHCLIENT_SET_HOSTNAME="no"
8. **Importante:** em "/ etc/sudoers", comentar ou remover Olá linhas a seguir se eles existirem:
   
     Padrões targetpw # solicitará a senha de saudação do usuário de destino Olá raiz ou seja, todos os ALL=(ALL) todos # aviso! Deve ser usado somente em conjunto com 'Defaults targetpw'!
9. Certifique-se de servidor SSH hello está instalado e configurado toostart no momento da inicialização.  Geralmente, esse é o padrão de saudação.
10. Não crie espaço de permuta em disco do sistema operacional hello.
    
    Olá agente Linux do Azure pode configurar automaticamente o espaço de permuta usando Olá disco de recurso local que é anexado toohello VM após a configuração no Azure. Observe que esse disco de recurso local Olá é um *temporário* disco e pode ser esvaziada quando Olá VM for desprovisionada. Depois de instalar o hello agente Linux do Azure (consulte a etapa anterior), modifique Olá seguintes parâmetros em /etc/waagent.conf adequadamente:
    
     ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048; # nota: Defina esse toowhatever precisar toobe.
11. Execute Olá seguindo a máquina virtual do comandos toodeprovision hello e prepará-la para provisionamento no Azure:
    
    # <a name="sudo-waagent--force--deprovision"></a>sudo waagent -force -deprovision
    # <a name="export-histsize0"></a>export HISTSIZE=0
    # <a name="logout"></a>logout
12. Certifique-se de hello que Azure Linux Agent executa durante a inicialização:
    
        # sudo systemctl enable waagent.service
13. Clique em **Ação -> Desligar** no Gerenciador do Hyper-V. O VHD Linux está agora pronto toobe carregado tooAzure.

## <a name="next-steps"></a>Próximas etapas
Você está agora pronto toouse as SUSE Linux disco rígido virtual toocreate novas máquinas virtuais no Azure. Se isso for Olá primeira vez que você está carregando tooAzure de arquivo. vhd hello, consulte as etapas 2 e 3 em [criando e carregando um disco rígido virtual que contém o sistema de operacional Linux Olá](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

