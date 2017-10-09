---
title: aaaCreate e carregar um VHD do Linux com base em CentOS no Azure
description: "Saiba toocreate e carregar um Azure disco rígido virtual (VHD) que contém um sistema operacional baseado em CentOS Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 0e518e92-e981-43f4-b12c-9cba1064c4bb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 78f36be1d36e3d44cb836c912d143f2c9a72aab5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-centos-based-virtual-machine-for-azure"></a>Preparar uma máquina virtual baseada em CentOS para o Azure
* [Preparar uma máquina virtual CentOS 6.x para o Azure](#centos-6x)
* [Preparar uma máquina virtual CentOS 7.0 ou posterior para o Azure](#centos-70)

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a>Pré-requisitos
Este artigo pressupõe que você já tiver instalado um CentOS (ou derivado semelhante) Linux tooa rígido disco do sistema operacional. Várias ferramentas existem toocreate arquivos. vhd, por exemplo, uma solução de virtualização como o Hyper-V. Para obter instruções, consulte [instalar Olá função Hyper-V e configurar uma máquina Virtual](http://technet.microsoft.com/library/hh846766.aspx).

**Notas de instalação do CentOS**

* Veja também as [Notas de instalação gerais do Linux](create-upload-generic.md#general-linux-installation-notes) para obter mais dicas sobre como preparar o Linux para o Azure.
* formato do Hello VHDX não tem suporte apenas no Azure, **VHD fixo**.  Você pode converter Olá disco tooVHD formato usando o Gerenciador do Hyper-V ou Olá cmdlet convert-vhd. Se você estiver usando VirtualBox isso significa que selecionando **tamanho fixo** como oposição padrão toohello alocada dinamicamente durante a criação de disco de saudação.
* Ao instalar o sistema de Linux Olá é *recomendado* que você use partições padrão em vez de LVM (geralmente padrão Olá para muitas instalações). Isso evitará LVM nome conflita com VMs clonados, especialmente se um disco do sistema operacional nunca precisa tooanother toobe anexado VM idêntico para solução de problemas. [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) podem ser usados nos discos de dados.
* É necessário suporte a kernel para montar sistemas de arquivos UDF. Durante a primeira inicialização hello Azure configuração de provisionamento é passada toohello VM Linux por meio de mídia formatada UDF que é anexado toohello convidado. agente do Linux Azure Olá deve ser capaz de toomount Olá UDF arquivo sistema tooread sua configuração e provisionar Olá VM.
* Versões de kernel do Linux abaixo de 2.6.37 não dão suporte ao NUMA no Hyper-V com tamanhos maiores de VM. Esse problema principalmente impactos distribuições mais antigas usando Olá upstream kernel Red Hat 2.6.32 e foi corrigido em RHEL 6.6 (kernel-2.6.32-504). Sistemas que executam kernels personalizados anteriores 2.6.37 ou com base em RHEL kernels mais antigos que 2.6.32-504 deve definir Olá parâmetro de inicialização `numa=off` no kernel de saudação de linha de comando em grub.conf. Para obter mais informações, confira o [KB 436883](https://access.redhat.com/solutions/436883) do Red Hat.
* Não configure uma partição de troca no disco do sistema operacional hello. agente do Linux Olá pode ser configurado toocreate um arquivo de permuta em disco de recursos temporário hello.  Para obter mais informações sobre isso podem ser encontradas nas etapas de saudação abaixo.
* Todos os VHDs Olá devem ter tamanhos que sejam múltiplos de 1 MB.

## <a name="centos-6x"></a>CentOS 6.x

1. No Gerenciador do Hyper-V, selecione máquina virtual de saudação.

2. Clique em **conectar** tooopen uma janela do console da máquina virtual de saudação.

3. CentOS 6, Gerenciador pode interferir com o agente do Linux Azure hello. Desinstale esse pacote executando Olá comando a seguir:
   
        # sudo rpm -e --nodeps NetworkManager

4. Criar ou editar o arquivo hello `/etc/sysconfig/network` e adicione Olá texto a seguir:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. Criar ou editar o arquivo hello `/etc/sysconfig/network-scripts/ifcfg-eth0` e adicione Olá texto a seguir:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. Modificar udev regras tooavoid gerar regras estáticas para Olá interfaces Ethernet. Essas regras podem provocar problemas ao clonar uma máquina virtual no Microsoft Azure ou no Hyper-V:
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. Certifique-se de que o serviço de rede Olá será iniciado no momento da inicialização executando Olá comando a seguir:
   
        # sudo chkconfig network on

8. Se você quiser toouse espelhos de OpenLogic de saudação que são hospedados no hello datacenters do Azure, em seguida, substitua Olá `/etc/yum.repos.d/CentOS-Base.repo` arquivo com hello repositórios a seguir.  Isso também adicionará Olá **[openlogic]** repositório que inclui pacotes adicionais como o agente do Linux Azure hello:

        [openlogic]
        name=CentOS-$releasever - openlogic packages for $basearch
        baseurl=http://olcentgbl.trafficmanager.net/openlogic/$releasever/openlogic/$basearch/
        enabled=1
        gpgcheck=0
        
        [base]
        name=CentOS-$releasever - Base
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/os/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #released updates
        [updates]
        name=CentOS-$releasever - Updates
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/updates/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #additional packages that may be useful
        [extras]
        name=CentOS-$releasever - Extras
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/extras/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

        #additional packages that extend functionality of existing packages
        [centosplus]
        name=CentOS-$releasever - Plus
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/centosplus/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #contrib - packages by Centos Users
        [contrib]
        name=CentOS-$releasever - Contrib
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=contrib&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/contrib/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

    >[!Note]
    Olá restante deste guia assumirá que você está usando pelo menos Olá `[openlogic]` repositório, que será o agente do Linux Azure Olá tooinstall usado abaixo.


9. Adicione Olá too/etc/yum.conf linha a seguir:
    
        http_caching=packages

10. Execute Olá comando tooclear Olá yum metadados e atualização Olá sistema atual com pacotes de saudação mais recentes a seguir:
    
        # yum clean all

    A menos que você estiver criando uma imagem de uma versão mais antiga do CentOS, é recomendável tooupdate que Olá a todos os pacotes toohello mais recente:

        # sudo yum -y update

    Pode ser necessária uma reinicialização depois de executar esse comando.

11. (Opcional) Instale drivers de saudação para Olá Integration Services LIS (Linux).
   
    >[!IMPORTANT]
    Olá etapa é **necessária** para CentOS 6.3 e anteriores e opcionais para versões posteriores.

        # sudo rpm -e hypervkvpd  ## (may return error if not installed, that's OK)
        # sudo yum install microsoft-hyper-v

    Como alternativa, você pode seguir as instruções de instalação manual de saudação em Olá [página de download do LIS](https://go.microsoft.com/fwlink/?linkid=403033) tooinstall Olá RPM em sua VM.
 
12. Instale Olá agente Linux do Azure e as dependências:
    
        # sudo yum install python-pyasn1 WALinuxAgent
    
    pacote de WALinuxAgent Olá removerá hello Gerenciador e pacotes de Gerenciador gnome se eles já não foram removidos conforme descrito na etapa 3.


13. Modificar a linha de inicialização de kernel de saudação em seus parâmetros de kernel adicionais tooinclude grub configuração do Azure. toodo isso, abra `/boot/grub/menu.lst` em um editor de texto e certifique-se de que kernel de padrão de saudação inclui Olá parâmetros a seguir:
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    Isso garantirá todas as mensagens de console são enviadas toohello primeira porta serial, que pode ajudá-lo Azure suporte à depuração de problemas.
    
    Além disso toohello acima, recomenda-se muito*remover* Olá seguintes parâmetros:
    
        rhgb quiet crashkernel=auto
    
    Inicialização gráfica e silenciosa não são úteis em um ambiente de nuvem onde queremos que todos os toobe de logs de saudação enviada toohello de porta serial.  Olá `crashkernel` opção pode ser esquerda configurada, se desejado, mas observe que esse parâmetro será reduzir a quantidade de saudação de memória disponível em Olá VM em 128 MB ou mais, que pode ser problemático em tamanhos de VM menores hello.

    >[!Important]
    CentOS 6.5 e anteriores também devem definir o parâmetro de kernel hello `numa=off`. Consulte Red Hat [KB 436883](https://access.redhat.com/solutions/436883).

14. Certifique-se de servidor SSH hello está instalado e configurado toostart no momento da inicialização.  Geralmente, esse é o padrão de saudação.

15. Não crie espaço de permuta em disco do sistema operacional hello.
    
    Olá agente Linux do Azure pode configurar automaticamente o espaço de permuta usando Olá disco de recurso local que é anexado toohello VM após a configuração no Azure. Observe que esse disco de recurso local Olá é um *temporário* disco e pode ser esvaziada quando Olá VM for desprovisionada. Depois de instalar o hello agente Linux do Azure (consulte a etapa anterior), modifique Olá parâmetros a seguir `/etc/waagent.conf` adequadamente:
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. Execute Olá seguindo a máquina virtual do comandos toodeprovision hello e prepará-la para provisionamento no Azure:
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

17. Clique em **Ação -> Desligar** no Gerenciador do Hyper-V. O VHD Linux está agora pronto toobe carregado tooAzure.


- - -
## <a name="centos-70"></a>CentOS 7.0+
**Alterações no CentOS 7 (e em derivativos similares)**

Preparando uma máquina virtual de CentOS 7 para o Azure é muito semelhante tooCentOS 6, no entanto, há várias diferenças importantes, vale a pena observar:

* Olá Gerenciador do pacote não está em conflito com o agente do Linux Azure hello. Esse pacote é instalado por padrão e recomendamos que você não o remova.
* GRUB2 agora é usado como Olá carregador de inicialização padrão, para que o procedimento Olá para editar os parâmetros de kernel foi alterada (consulte abaixo).
* XFS agora é um sistema de arquivos padrão de saudação. sistema de arquivos ext4 Olá ainda pode ser usado, se desejado.

**Etapas da configuração**

1. No Gerenciador do Hyper-V, selecione máquina virtual de saudação.

2. Clique em **conectar** tooopen uma janela do console da máquina virtual de saudação.

3. Criar ou editar o arquivo hello `/etc/sysconfig/network` e adicione Olá texto a seguir:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. Criar ou editar o arquivo hello `/etc/sysconfig/network-scripts/ifcfg-eth0` e adicione Olá texto a seguir:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. Modificar udev regras tooavoid gerar regras estáticas para Olá interfaces Ethernet. Essas regras podem provocar problemas ao clonar uma máquina virtual no Microsoft Azure ou no Hyper-V:
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

6. Se você quiser toouse espelhos de OpenLogic de saudação que são hospedados no hello datacenters do Azure, em seguida, substitua Olá `/etc/yum.repos.d/CentOS-Base.repo` arquivo com hello repositórios a seguir.  Isso também adicionará Olá **[openlogic]** repositório que inclui pacotes de agente do Linux Azure hello:
   
        [openlogic]
        name=CentOS-$releasever - openlogic packages for $basearch
        baseurl=http://olcentgbl.trafficmanager.net/openlogic/$releasever/openlogic/$basearch/
        enabled=1
        gpgcheck=0
        
        [base]
        name=CentOS-$releasever - Base
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/os/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #released updates
        [updates]
        name=CentOS-$releasever - Updates
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/updates/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #additional packages that may be useful
        [extras]
        name=CentOS-$releasever - Extras
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/extras/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #additional packages that extend functionality of existing packages
        [centosplus]
        name=CentOS-$releasever - Plus
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/centosplus/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

    >[!Note]
    Olá restante deste guia assumirá que você está usando pelo menos Olá `[openlogic]` repositório, que será o agente do Linux Azure Olá tooinstall usado abaixo.

7. Execute Olá metadados Olá yum atuais tooclear comando a seguir e instale todas as atualizações:
   
        # sudo yum clean all

    A menos que você estiver criando uma imagem de uma versão mais antiga do CentOS, é recomendável tooupdate que Olá a todos os pacotes toohello mais recente:

        # sudo yum -y update

    Uma reinicialização necessária talvez depois de executar esse comando.

8. Modificar a linha de inicialização de kernel de saudação em seus parâmetros de kernel adicionais tooinclude grub configuração do Azure. toodo isso, abra `/etc/default/grub` em uma saudação de editor e editar texto `GRUB_CMDLINE_LINUX` parâmetro, por exemplo:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Isso garantirá todas as mensagens de console são enviadas toohello primeira porta serial, que pode ajudá-lo Azure suporte à depuração de problemas. Ela também desativa novas convenções de nomenclatura CentOS 7 Olá para as NICs. Além disso toohello acima, recomenda-se muito*remover* Olá seguintes parâmetros:
   
        rhgb quiet crashkernel=auto
   
    Inicialização gráfica e silenciosa não são úteis em um ambiente de nuvem onde queremos que todos os toobe de logs de saudação enviada toohello de porta serial. Olá `crashkernel` opção pode ser esquerda configurada, se desejado, mas observe que esse parâmetro será reduzir a quantidade de saudação de memória disponível em Olá VM em 128 MB ou mais, que pode ser problemático em tamanhos de VM menores hello.

9. Quando terminar edição `/etc/default/grub` por acima, execute Olá seguinte comando toorebuild Olá grub configuração:
   
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

10. Se a criação de imagem de saudação do **VMWare, VirtualBox ou KVM:** Certifique-se de Olá Hyper-V drivers é inclusos Olá initramfs:
   
   Edite `/etc/dracut.conf`e adicione o conteúdo:
   
        add_drivers+=”hv_vmbus hv_netvsc hv_storvsc”
   
   Recrie Olá initramfs:
   
        # sudo dracut –f -v

11. Instale Olá agente Linux do Azure e as dependências:

        # sudo yum install python-pyasn1 WALinuxAgent
        # sudo systemctl enable waagent

12. Não crie espaço de permuta em disco do sistema operacional hello.
   
   Olá agente Linux do Azure pode configurar automaticamente o espaço de permuta usando Olá disco de recurso local que é anexado toohello VM após a configuração no Azure. Observe que esse disco de recurso local Olá é um *temporário* disco e pode ser esvaziada quando Olá VM for desprovisionada. Depois de instalar o hello agente Linux do Azure (consulte a etapa anterior), modifique Olá parâmetros a seguir `/etc/waagent.conf` adequadamente:
   
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. Execute Olá seguindo a máquina virtual do comandos toodeprovision hello e prepará-la para provisionamento no Azure:
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

14. Clique em **Ação -> Desligar** no Gerenciador do Hyper-V. O VHD Linux está agora pronto toobe carregado tooAzure.

## <a name="next-steps"></a>Próximas etapas
Você está agora pronto toouse seu CentOS Linux disco rígido virtual toocreate novas máquinas virtuais no Azure. Se isso for Olá primeira vez que você está carregando tooAzure de arquivo. vhd hello, consulte as etapas 2 e 3 em [criando e carregando um disco rígido virtual que contém o sistema de operacional Linux Olá](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

