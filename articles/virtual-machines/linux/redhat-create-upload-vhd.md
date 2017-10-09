---
title: aaaCreate e carregar um VHD do Red Hat Enterprise Linux para uso no Azure | Microsoft Docs
description: "Saiba toocreate e carregar um Azure disco rígido virtual (VHD) que contém um sistema operacional Red Hat Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 6c6b8f72-32d3-47fa-be94-6cb54537c69f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/28/2017
ms.author: szark
ms.openlocfilehash: bdd1bbfbee55b5cc61d69a09b06b6bd2c3de362b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-red-hat-based-virtual-machine-for-azure"></a>Preparar uma máquina virtual baseada no Red Hat para o Azure
Neste artigo, você aprenderá como tooprepare uma máquina virtual de Red Hat Enterprise Linux (RHEL) para uso no Azure. versões de saudação do RHEL que são abordadas neste artigo são 6.7 + e 7.1 +. Olá hipervisores de preparação que são abordados neste artigo são máquinas virtuais Hyper-V, baseado no kernel (KVM) e VMware. Para saber mais informações sobre os requisitos de qualificação para participação no programa Red Hat Cloud Access, confira o [site Red Hat Cloud Access](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) e o artigo[Como executar o RHEL no Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).

## <a name="prepare-a-red-hat-based-virtual-machine-from-hyper-v-manager"></a>Preparar uma máquina virtual baseada em Red Hat a partir do Gerenciador do Hyper-V

### <a name="prerequisites"></a>Pré-requisitos
Esta seção pressupõe que você já tiver obtido um arquivo ISO de site do Red Hat hello e Olá instalado RHEL imagem tooa disco rígido virtual (VHD). Para obter mais detalhes sobre como toouse Gerenciador Hyper-V tooinstall uma imagem do sistema operacional, consulte [instalar Olá função Hyper-V e configurar uma máquina Virtual](http://technet.microsoft.com/library/hh846766.aspx).

**Notas de instalação do RHEL**

* Azure não oferece suporte a no formato VHDX hello. O Azure suporta apenas VHD fixo. Você pode usar o formato de tooVHD do Gerenciador do Hyper-V tooconvert Olá disco, ou você pode usar o cmdlet convert-vhd de saudação. Se você usar VirtualBox, selecione **tamanho fixo** contrário como padrão toohello alocada dinamicamente a opção ao criar o disco de saudação.
* O Azure suporta somente as máquinas virtuais de geração 1. Você pode converter uma máquina virtual geração 1 de formato de arquivo VHD VHDX toohello em disco de tamanho fixo de tooa de expansão dinâmica. Mas observe não é possível alterar a geração de uma máquina virtual. Para saber mais informações, confira [Devo criar uma máquina virtual de geração 1 ou 2 no Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).
* tamanho máximo de saudação que é permitido para Olá VHD é 1.023 GB.
* Quando você instala o sistema de operacional Linux hello, recomendamos que você use partições padrão em vez de Gerenciador de Volume lógico (LVM), que geralmente é o padrão de saudação para muitas instalações. Essa prática evitará LVM nome conflita com máquinas virtuais, especialmente se você alguma vez precisar tooattach uma máquina virtual idêntica sistema operacional disco tooanother para solução de problemas. [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) podem ser usados nos discos de dados.
* É necessário suporte de kernel para montar sistemas de arquivos de formato de disco universal (UDF). Na primeira inicialização na mídia do Azure, Olá UDF formatado que é anexado toohello convidado passa Olá toohello provisionamento da configuração máquina virtual do Linux. Olá agente Linux do Azure deve ser capaz de toomount Olá UDF arquivo sistema tooread sua configuração e provisionar a máquina virtual de saudação.
* Versões do kernel do Linux Olá 2.6.37 anteriores não dão acesso não uniforme a memória (NUMA) no Hyper-V com os maiores tamanhos de máquina virtual. Esse problema principalmente impactos distribuições mais antigas que usam Olá upstream kernel Red Hat 2.6.32 e foi corrigido em RHEL 6.6 (kernel-2.6.32-504). Sistemas que executam kernels personalizados que são mais antigos que 2.6.37 ou kernels com base em RHEL mais antigos que 2.6.32-504 devem definir Olá `numa=off` parâmetro de inicialização na linha de comando de kernel Olá em grub.conf. Para obter mais informações, confira o [KB 436883](https://access.redhat.com/solutions/436883) do Red Hat.
* Não configure uma partição de troca no disco do sistema operacional hello. Olá agente Linux pode ser configurado toocreate um arquivo de permuta em disco de recursos temporário hello.  Para obter mais informações sobre isso podem ser encontradas no hello etapas a seguir.
* Todos os VHDs devem ter tamanhos que sejam múltiplos de 1 MB.

### <a name="prepare-a-rhel-6-virtual-machine-from-hyper-v-manager"></a>Preparar uma máquina virtual RHEL 6 do Gerenciador do Hyper-V

1. No Gerenciador do Hyper-V, selecione máquina virtual de saudação.

2. Clique em **conectar** tooopen uma janela do console da máquina virtual de saudação.

3. RHEL 6, Gerenciador pode interferir com o agente do Linux Azure hello. Desinstale esse pacote executando Olá comando a seguir:
   
        # sudo rpm -e --nodeps NetworkManager

4. Criar ou editar Olá `/etc/sysconfig/network` de arquivo e, em seguida, adicione Olá texto a seguir:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. Criar ou editar Olá `/etc/sysconfig/network-scripts/ifcfg-eth0` de arquivo e, em seguida, adicione Olá texto a seguir:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. Mover (ou remover) Olá udev regras tooavoid gerar regras estáticas para interface de Ethernet hello. Essas regras causam problemas ao clonar uma máquina virtual no Microsoft Azure ou no Hyper-V:

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. Certifique-se de que o serviço de rede Olá iniciará no momento da inicialização executando Olá comando a seguir:

        # sudo chkconfig network on

8. Registre a instalação de saudação Red Hat assinatura tooenable de pacotes do repositório do RHEL Olá executando Olá comando a seguir:

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

9. pacote de WALinuxAgent Hello, `WALinuxAgent-<version>`, foi introduzido repositório do toohello Red Hat extras. Habilite o repositório de extras Olá executando Olá comando a seguir:

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

10. Modificar a linha de inicialização de kernel de saudação em seus parâmetros de kernel adicionais tooinclude grub configuração do Azure. toodo essa modificação, abra `/boot/grub/menu.lst` em um editor de texto e certifique-se de que kernel de padrão de saudação inclui Olá parâmetros a seguir:
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    Isso garantirá que todas as mensagens de console são enviadas toohello primeira porta serial, que pode ajudá-lo Azure suporte à depuração de problemas.
    
    Além disso, é recomendável que você remova Olá parâmetros a seguir:
    
        rhgb quiet crashkernel=auto
    
    Inicialização gráfica e silenciosa não são úteis em um ambiente de nuvem onde queremos que todos os toobe de logs de saudação enviada toohello de porta serial.  Você pode deixar Olá `crashkernel` opção de configuração, se desejado. Observe que esse parâmetro reduz a quantidade de saudação de memória disponível na máquina virtual Olá 128 MB ou mais. Essa configuração pode ser um problema em máquinas virtuais menores.

    >[!Important]
    RHEL 6.5 e anterior também deve definir Olá `numa=off` parâmetro de kernel. Consulte Red Hat [KB 436883](https://access.redhat.com/solutions/436883).

11. Certifique-se de servidor SSH (secure shell) hello está instalado e configurado toostart no momento da inicialização, que normalmente é o padrão de saudação. Modificar /etc/ssh/sshd_config tooinclude Olá seguinte linha:

        ClientAliveInterval 180

12. Instale Olá agente Linux do Azure executando Olá comando a seguir:

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

    Instalar pacote de WALinuxAgent Olá remove hello Gerenciador e pacotes de Gerenciador gnome se eles já não foram removidos na etapa 3.

13. Não crie espaço de permuta no disco do sistema operacional hello.

    Olá agente Linux do Azure pode configurar automaticamente o espaço de permuta usando Olá disco de recurso local que é anexado toohello máquina de virtual depois de máquina virtual de saudação é provisionada no Azure. Observe que Olá local do disco de recurso é temporária e que talvez esvaziada quando a máquina virtual de saudação desprovisionada. Depois de instalar o hello Azure Linux Agent na etapa anterior hello, modificar Olá seguintes parâmetros em /etc/waagent.conf adequadamente:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

14. Cancelar o registro de assinatura de saudação (se necessário) executando Olá comando a seguir:

        # sudo subscription-manager unregister

15. Execute Olá seguindo a máquina virtual do comandos toodeprovision hello e prepará-la para provisionamento no Azure:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

16. Clique em **Ação** > **Desligar** no Gerenciador do Hyper-V. O VHD Linux está agora pronto toobe carregado tooAzure.


### <a name="prepare-a-rhel-7-virtual-machine-from-hyper-v-manager"></a>Preparar uma máquina virtual RHEL 7 do Gerenciador do Hyper-V

1. No Gerenciador do Hyper-V, selecione máquina virtual de saudação.

2. Clique em **conectar** tooopen uma janela do console da máquina virtual de saudação.

3. Criar ou editar Olá `/etc/sysconfig/network` de arquivo e, em seguida, adicione Olá texto a seguir:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. Criar ou editar Olá `/etc/sysconfig/network-scripts/ifcfg-eth0` de arquivo e, em seguida, adicione Olá texto a seguir:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. Certifique-se de que o serviço de rede Olá iniciará no momento da inicialização executando Olá comando a seguir:

        # sudo chkconfig network on

6. Registre a instalação de saudação Red Hat assinatura tooenable de pacotes do repositório do RHEL Olá executando Olá comando a seguir:

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. Modificar a linha de inicialização de kernel de saudação em seus parâmetros de kernel adicionais tooinclude grub configuração do Azure. toodo essa modificação, abra `/etc/default/grub` em um editor de texto e edição Olá `GRUB_CMDLINE_LINUX` parâmetro. Por exemplo:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Isso garantirá que todas as mensagens de console são enviadas toohello primeira porta serial, que pode ajudá-lo Azure suporte à depuração de problemas. Essa configuração também desativa novas convenções de nomenclatura RHEL 7 Olá para as NICs. Além disso, recomendamos que você remova Olá parâmetros a seguir:
   
        rhgb quiet crashkernel=auto
   
    Inicialização gráfica e silenciosa não são úteis em um ambiente de nuvem onde queremos que todos os toobe de logs de saudação enviada toohello de porta serial. Você pode deixar Olá `crashkernel` opção de configuração, se desejado. Observe que esse parâmetro reduz a quantidade de saudação de memória disponível na máquina virtual Olá 128 MB ou mais, que pode ser problemático em tamanhos menores de máquina virtual.

8. Depois de terminar edição `/etc/default/grub`, execute hello toorebuild Olá grub configuração dos comandos a seguir:

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

9. Certifique-se de servidor SSH hello está instalado e configurado toostart no momento da inicialização, que normalmente é o padrão de saudação. Modificar `/etc/ssh/sshd_config` tooinclude Olá seguinte linha:

        ClientAliveInterval 180

10. pacote de WALinuxAgent Hello, `WALinuxAgent-<version>`, foi introduzido repositório do toohello Red Hat extras. Habilite o repositório de extras Olá executando Olá comando a seguir:

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

11. Instale Olá agente Linux do Azure executando Olá comando a seguir:

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

12. Não crie espaço de permuta no disco do sistema operacional hello.

    Olá agente Linux do Azure pode configurar automaticamente o espaço de permuta usando Olá disco de recurso local que é anexado toohello máquina de virtual depois de máquina virtual de saudação é provisionada no Azure. Observe que hello, disco de recurso local é um disco temporário, e pode ser esvaziada quando a máquina virtual de saudação desprovisionada. Depois de instalar o hello Azure Linux Agent na etapa anterior Olá, modificar Olá parâmetros a seguir `/etc/waagent.conf` adequadamente:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. Se desejar que a assinatura de saudação toounregister, execute Olá comando a seguir:

        # sudo subscription-manager unregister

14. Execute Olá seguindo a máquina virtual do comandos toodeprovision hello e prepará-la para provisionamento no Azure:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. Clique em **Ação** > **Desligar** no Gerenciador do Hyper-V. O VHD Linux está agora pronto toobe carregado tooAzure.


## <a name="prepare-a-red-hat-based-virtual-machine-from-kvm"></a>Preparar uma máquina virtual baseada no Red Hat para KVM
### <a name="prepare-a-rhel-6-virtual-machine-from-kvm"></a>Preparar uma máquina virtual RHEL 6 do KVM

1. Baixe imagem KVM de saudação do RHEL 6 do site do Red Hat hello.

2. Definir uma senha raiz.

    Gerar uma senha criptografada e copie a saída de saudação do comando hello:

        # openssl passwd -1 changeme

    Defina uma senha raiz com guestfish:
        
        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   Alteração Olá segundo campo de usuário raiz hello "!" toohello senha criptografada.

3. Crie uma máquina virtual em KVM da imagem de qcow2 hello. Definir o tipo de disco Olá muito**qcow2**e defina o modelo de dispositivo de interface de rede virtual Olá muito**virtio**. Em seguida, iniciar a máquina virtual de saudação e entre como raiz.

4. Criar ou editar Olá `/etc/sysconfig/network` de arquivo e, em seguida, adicione Olá texto a seguir:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. Criar ou editar Olá `/etc/sysconfig/network-scripts/ifcfg-eth0` de arquivo e, em seguida, adicione Olá texto a seguir:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. Mover (ou remover) Olá udev regras tooavoid gerar regras estáticas para interface de Ethernet hello. Essas regras causam problemas ao clonar uma máquina virtual no Azure ou no Hyper-V:

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. Certifique-se de que o serviço de rede Olá iniciará no momento da inicialização executando Olá comando a seguir:

        # chkconfig network on

8. Registre a instalação de saudação Red Hat assinatura tooenable de pacotes do repositório do RHEL Olá executando Olá comando a seguir:

        # subscription-manager register --auto-attach --username=XXX --password=XXX

9. Modificar a linha de inicialização de kernel de saudação em seus parâmetros de kernel adicionais tooinclude grub configuração do Azure. toodo essa configuração, abra `/boot/grub/menu.lst` em um editor de texto e certifique-se de que kernel de padrão de saudação inclui Olá parâmetros a seguir:
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    Isso garantirá que todas as mensagens de console são enviadas toohello primeira porta serial, que pode ajudá-lo Azure suporte à depuração de problemas.
    
    Além disso, recomendamos que você remova Olá parâmetros a seguir:
    
        rhgb quiet crashkernel=auto
    
    Inicialização gráfica e silenciosa não são úteis em um ambiente de nuvem onde queremos que todos os toobe de logs de saudação enviada toohello de porta serial. Você pode deixar Olá `crashkernel` opção de configuração, se desejado. Observe que esse parâmetro reduz a quantidade de saudação de memória disponível na máquina virtual Olá 128 MB ou mais, que pode ser problemático em tamanhos menores de máquina virtual.

    >[!Important]
    RHEL 6.5 e anterior também deve definir Olá `numa=off` parâmetro de kernel. Consulte Red Hat [KB 436883](https://access.redhat.com/solutions/436883).

10. Adicione tooinitramfs de módulos do Hyper-V:  

    Editar `/etc/dracut.conf`e adicione Olá conteúdo a seguir:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    Recrie initramfs:

        # dracut -f -v

11. Desinstale cloud-init:

        # yum remove cloud-init

12. Certifique-se de servidor SSH hello está instalado e configurado toostart durante a inicialização:

        # chkconfig sshd on

    Modificar /etc/ssh/sshd_config tooinclude Olá linhas seguintes:

        PasswordAuthentication yes
        ClientAliveInterval 180

13. pacote de WALinuxAgent Hello, `WALinuxAgent-<version>`, foi introduzido repositório do toohello Red Hat extras. Habilite o repositório de extras Olá executando Olá comando a seguir:

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

14. Instale Olá agente Linux do Azure executando Olá comando a seguir:

        # yum install WALinuxAgent

        # chkconfig waagent on

15. Olá agente Linux do Azure pode configurar automaticamente o espaço de permuta usando Olá disco de recurso local que é anexado toohello máquina de virtual depois de máquina virtual de saudação é provisionada no Azure. Observe que hello, disco de recurso local é um disco temporário, e pode ser esvaziada quando a máquina virtual de saudação desprovisionada. Depois de instalar o hello Azure Linux Agent na etapa anterior Olá, modificar Olá parâmetros a seguir **/etc/waagent.conf** adequadamente:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. Cancelar o registro de assinatura de saudação (se necessário) executando Olá comando a seguir:

        # subscription-manager unregister

17. Execute Olá seguindo a máquina virtual do comandos toodeprovision hello e prepará-la para provisionamento no Azure:

        # waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. Desligar a máquina virtual Olá KVM.

19. Converta o formato VHD Olá qcow2 imagem toohello.

    Primeiro converter o formato de tooraw Olá imagem:

        # qemu-img convert -f qcow2 -O raw rhel-6.8.qcow2 rhel-6.8.raw

    Certifique-se de que tamanho Olá da imagem brutos hello está alinhado com 1 MB. Caso contrário, arredonde Olá tamanho tooalign com 1 MB:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Converter Olá disco raw tooa tamanho fixo VHD:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd


### <a name="prepare-a-rhel-7-virtual-machine-from-kvm"></a>Preparar uma máquina virtual RHEL 7 do KVM

1. Baixe imagem KVM de saudação do RHEL 7 do site do Red Hat hello. Esse procedimento usa RHEL 7 como exemplo hello.

2. Definir uma senha raiz.

    Gerar uma senha criptografada e copie a saída de saudação do comando hello:

        # openssl passwd -1 changeme

    Defina uma senha raiz com guestfish:

        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   Alteração Olá segundo campo de usuário de raiz de "!" toohello senha criptografada.

3. Crie uma máquina virtual em KVM da imagem de qcow2 hello. Definir o tipo de disco Olá muito**qcow2**e defina o modelo de dispositivo de interface de rede virtual Olá muito**virtio**. Em seguida, iniciar a máquina virtual de saudação e entre como raiz.

4. Criar ou editar Olá `/etc/sysconfig/network` de arquivo e, em seguida, adicione Olá texto a seguir:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. Criar ou editar Olá `/etc/sysconfig/network-scripts/ifcfg-eth0` de arquivo e, em seguida, adicione Olá texto a seguir:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

6. Certifique-se de que o serviço de rede Olá iniciará no momento da inicialização executando Olá comando a seguir:

        # chkconfig network on

7. Registre a instalação do Red Hat assinatura tooenable de pacotes do repositório do RHEL Olá executando Olá comando a seguir:

        # subscription-manager register --auto-attach --username=XXX --password=XXX

8. Modificar a linha de inicialização de kernel de saudação em seus parâmetros de kernel adicionais tooinclude grub configuração do Azure. toodo essa configuração, abra `/etc/default/grub` em um editor de texto e edição Olá `GRUB_CMDLINE_LINUX` parâmetro. Por exemplo:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Esse comando também garante que todas as mensagens de console são enviadas toohello primeira porta serial, que pode ajudá-lo Azure suporte à depuração de problemas. comando Olá também desativa novas convenções de nomenclatura RHEL 7 Olá para as NICs. Além disso, recomendamos que você remova Olá parâmetros a seguir:
   
        rhgb quiet crashkernel=auto
   
    Inicialização gráfica e silenciosa não são úteis em um ambiente de nuvem onde queremos que todos os toobe de logs de saudação enviada toohello de porta serial. Você pode deixar Olá `crashkernel` opção de configuração, se desejado. Observe que esse parâmetro reduz a quantidade de saudação de memória disponível na máquina virtual Olá 128 MB ou mais, que pode ser problemático em tamanhos menores de máquina virtual.

9. Depois de terminar edição `/etc/default/grub`, execute hello toorebuild Olá grub configuração dos comandos a seguir:

        # grub2-mkconfig -o /boot/grub2/grub.cfg

10. Adicione os módulos do Hyper-V em initramfs.

    Edite `/etc/dracut.conf` e adicione o conteúdo:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    Recrie initramfs:

        # dracut -f -v

11. Desinstale cloud-init:

        # yum remove cloud-init

12. Certifique-se de servidor SSH hello está instalado e configurado toostart durante a inicialização:

        # systemctl enable sshd

    Modificar /etc/ssh/sshd_config tooinclude Olá linhas seguintes:

        PasswordAuthentication yes
        ClientAliveInterval 180

13. pacote de WALinuxAgent Hello, `WALinuxAgent-<version>`, foi introduzido repositório do toohello Red Hat extras. Habilite o repositório de extras Olá executando Olá comando a seguir:

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

14. Instale Olá agente Linux do Azure executando Olá comando a seguir:

        # yum install WALinuxAgent

    Habilite o serviço de waagent hello:

        # systemctl enable waagent.service

15. Não crie espaço de permuta no disco do sistema operacional hello.

    Olá agente Linux do Azure pode configurar automaticamente o espaço de permuta usando Olá disco de recurso local que é anexado toohello máquina de virtual depois de máquina virtual de saudação é provisionada no Azure. Observe que hello, disco de recurso local é um disco temporário, e pode ser esvaziada quando a máquina virtual de saudação desprovisionada. Depois de instalar o hello Azure Linux Agent na etapa anterior Olá, modificar Olá parâmetros a seguir `/etc/waagent.conf` adequadamente:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. Cancelar o registro de assinatura de saudação (se necessário) executando Olá comando a seguir:

        # subscription-manager unregister

17. Execute Olá seguindo a máquina virtual do comandos toodeprovision hello e prepará-la para provisionamento no Azure:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. Desligar a máquina virtual Olá KVM.

19. Converta o formato VHD Olá qcow2 imagem toohello.

    Primeiro converter o formato de tooraw Olá imagem:

        # qemu-img convert -f qcow2 -O raw rhel-7.3.qcow2 rhel-7.3.raw

    Certifique-se de que tamanho Olá da imagem brutos hello está alinhado com 1 MB. Caso contrário, arredonde Olá tamanho tooalign com 1 MB:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Converter Olá disco raw tooa tamanho fixo VHD:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-vmware"></a>Preparar uma máquina virtual baseada no Red Hat do VMware
### <a name="prerequisites"></a>Pré-requisitos
Esta seção pressupõe que você já instalou uma máquina virtual RHEL no VMware. Para obter detalhes sobre como tooinstall um sistema operacional em VMware, consulte [guia de instalação de sistema operacional de convidado do VMware](http://partnerweb.vmware.com/GOSIG/home.html).

* Quando você instala o sistema de operacional Linux hello, recomendamos que você use partições padrão em vez de LVM, que geralmente é o padrão de saudação para muitas instalações. Isso evitará LVM nome está em conflito com a máquina virtual clonada, especialmente se um disco do sistema operacional nunca precisa de máquina de virtual tooanother toobe anexado para solução de problemas. Se você preferir, é possível usar LVM ou RAID em discos de dados.
* Não configure uma partição de troca no disco do sistema operacional hello. Você pode configurar Olá Linux agent toocreate um arquivo de permuta em disco de recursos temporário hello. Você encontrará mais informações sobre isso nas etapas Olá seguir.
* Quando você cria um disco rígido virtual de saudação, selecione **disco virtual de armazenamento como um único arquivo**.

### <a name="prepare-a-rhel-6-virtual-machine-from-vmware"></a>Preparar uma máquina virtual RHEL 6 do VMware
1. RHEL 6, Gerenciador pode interferir com o agente do Linux Azure hello. Desinstale esse pacote executando Olá comando a seguir:
   
        # sudo rpm -e --nodeps NetworkManager

2. Crie um arquivo chamado **rede** Olá Olá /etc/hosts sysconfig/diretório que contém texto a seguir:

        NETWORKING=yes
        HOSTNAME=localhost.localdomain

3. Criar ou editar Olá `/etc/sysconfig/network-scripts/ifcfg-eth0` de arquivo e, em seguida, adicione Olá texto a seguir:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

4. Mover (ou remover) Olá udev regras tooavoid gerar regras estáticas para interface de Ethernet hello. Essas regras causam problemas ao clonar uma máquina virtual no Azure ou no Hyper-V:

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

5. Certifique-se de que o serviço de rede Olá iniciará no momento da inicialização executando Olá comando a seguir:

        # sudo chkconfig network on

6. Registre a instalação de saudação Red Hat assinatura tooenable de pacotes do repositório do RHEL Olá executando Olá comando a seguir:

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. pacote de WALinuxAgent Hello, `WALinuxAgent-<version>`, foi introduzido repositório do toohello Red Hat extras. Habilite o repositório de extras Olá executando Olá comando a seguir:

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

8. Modificar a linha de inicialização de kernel de saudação em seus parâmetros de kernel adicionais tooinclude grub configuração do Azure. toodo isso, abra `/etc/default/grub` em um editor de texto e edição Olá `GRUB_CMDLINE_LINUX` parâmetro. Por exemplo:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0"
   
   Isso garantirá que todas as mensagens de console são enviadas toohello primeira porta serial, que pode ajudá-lo Azure suporte à depuração de problemas. Além disso, recomendamos que você remova Olá parâmetros a seguir:
   
        rhgb quiet crashkernel=auto
   
    Inicialização gráfica e silenciosa não são úteis em um ambiente de nuvem onde queremos que todos os toobe de logs de saudação enviada toohello de porta serial. Você pode deixar Olá `crashkernel` opção de configuração, se desejado. Observe que esse parâmetro reduz a quantidade de saudação de memória disponível na máquina virtual Olá 128 MB ou mais, que pode ser problemático em tamanhos menores de máquina virtual.

9. Adicione tooinitramfs de módulos do Hyper-V:

    Editar `/etc/dracut.conf`e adicione Olá conteúdo a seguir:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    Recrie initramfs:

        # dracut -f -v

10. Certifique-se de servidor SSH hello está instalado e configurado toostart no momento da inicialização, que normalmente é o padrão de saudação. Modificar `/etc/ssh/sshd_config` tooinclude Olá seguinte linha:

    ClientAliveInterval 180

11. Instale Olá agente Linux do Azure executando Olá comando a seguir:

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

12. Não crie espaço de permuta no disco do sistema operacional hello.

    Olá agente Linux do Azure pode configurar automaticamente o espaço de permuta usando Olá disco de recurso local que é anexado toohello máquina de virtual depois de máquina virtual de saudação é provisionada no Azure. Observe que hello, disco de recurso local é um disco temporário, e pode ser esvaziada quando a máquina virtual de saudação desprovisionada. Depois de instalar o hello Azure Linux Agent na etapa anterior Olá, modificar Olá parâmetros a seguir `/etc/waagent.conf` adequadamente:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. Cancelar o registro de assinatura de saudação (se necessário) executando Olá comando a seguir:

        # sudo subscription-manager unregister

14. Execute Olá seguindo a máquina virtual do comandos toodeprovision hello e prepará-la para provisionamento no Azure:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. Desligar a máquina virtual de saudação e converter o arquivo. vhd do hello VMDK arquivo tooa.

    Primeiro converter o formato de tooraw Olá imagem:

        # qemu-img convert -f vmdk -O raw rhel-6.8.vmdk rhel-6.8.raw

    Certifique-se de que tamanho Olá da imagem brutos hello está alinhado com 1 MB. Caso contrário, arredonde Olá tamanho tooalign com 1 MB:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Converter Olá disco raw tooa tamanho fixo VHD:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd

### <a name="prepare-a-rhel-7-virtual-machine-from-vmware"></a>Preparar uma máquina virtual RHEL 7 do VMware
1. Criar ou editar Olá `/etc/sysconfig/network` de arquivo e, em seguida, adicione Olá texto a seguir:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

2. Criar ou editar Olá `/etc/sysconfig/network-scripts/ifcfg-eth0` de arquivo e, em seguida, adicione Olá texto a seguir:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

3. Certifique-se de que o serviço de rede Olá iniciará no momento da inicialização executando Olá comando a seguir:

        # sudo chkconfig network on

4. Registre a instalação de saudação Red Hat assinatura tooenable de pacotes do repositório do RHEL Olá executando Olá comando a seguir:

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

5. Modificar a linha de inicialização de kernel de saudação em seus parâmetros de kernel adicionais tooinclude grub configuração do Azure. toodo essa modificação, abra `/etc/default/grub` em um editor de texto e edição Olá `GRUB_CMDLINE_LINUX` parâmetro. Por exemplo:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Essa configuração também garante que todas as mensagens de console são enviadas toohello primeira porta serial, que pode ajudá-lo Azure suporte à depuração de problemas. Ela também desativa novas convenções de nomenclatura RHEL 7 Olá para as NICs. Além disso, recomendamos que você remova Olá parâmetros a seguir:
   
        rhgb quiet crashkernel=auto
   
    Inicialização gráfica e silenciosa não são úteis em um ambiente de nuvem onde queremos que todos os toobe de logs de saudação enviada toohello de porta serial. Você pode deixar Olá `crashkernel` opção de configuração, se desejado. Observe que esse parâmetro reduz a quantidade de saudação de memória disponível na máquina virtual Olá 128 MB ou mais, que pode ser problemático em tamanhos menores de máquina virtual.

6. Depois de terminar edição `/etc/default/grub`, execute hello toorebuild Olá grub configuração dos comandos a seguir:

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

7. Adicione tooinitramfs de módulos do Hyper-V.

    Edite `/etc/dracut.conf`e adicione o conteúdo:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    Recrie initramfs:

        # dracut -f -v

8. Certifique-se de servidor SSH hello está instalado e configurado toostart no momento da inicialização. Essa configuração é geralmente padrão hello. Modificar `/etc/ssh/sshd_config` tooinclude Olá seguinte linha:

        ClientAliveInterval 180

9. pacote de WALinuxAgent Hello, `WALinuxAgent-<version>`, foi introduzido repositório do toohello Red Hat extras. Habilite o repositório de extras Olá executando Olá comando a seguir:

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

10. Instale Olá agente Linux do Azure executando Olá comando a seguir:

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

11. Não crie espaço de permuta no disco do sistema operacional hello.

    Olá agente Linux do Azure pode configurar automaticamente o espaço de permuta usando Olá disco de recurso local que é anexado toohello máquina de virtual depois de máquina virtual de saudação é provisionada no Azure. Observe que hello, disco de recurso local é um disco temporário, e pode ser esvaziada quando a máquina virtual de saudação desprovisionada. Depois de instalar o hello Azure Linux Agent na etapa anterior Olá, modificar Olá parâmetros a seguir `/etc/waagent.conf` adequadamente:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

12. Se desejar que a assinatura de saudação toounregister, execute Olá comando a seguir:

        # sudo subscription-manager unregister

13. Execute Olá seguindo a máquina virtual do comandos toodeprovision hello e prepará-la para provisionamento no Azure:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

14. Desligar a máquina virtual de saudação e converter o formato de VHD do hello VMDK arquivo toohello.

    Primeiro converter o formato de tooraw Olá imagem:

        # qemu-img convert -f vmdk -O raw rhel-7.3.vmdk rhel-7.3.raw

    Certifique-se de que tamanho Olá da imagem brutos hello está alinhado com 1 MB. Caso contrário, arredonde Olá tamanho tooalign com 1 MB:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Converter Olá disco raw tooa tamanho fixo VHD:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-an-iso-by-using-a-kickstart-file-automatically"></a>Preparar uma máquina virtual baseada em Red Hat de um arquivo ISO, usando um arquivo de início rápido automaticamente
### <a name="prepare-a-rhel-7-virtual-machine-from-a-kickstart-file"></a>Preparar uma máquina virtual RHEL 7 de um arquivo de início rápido

1.  Criar um arquivo de início rápido que inclui Olá conteúdo a seguir e salve o arquivo hello. Para obter detalhes sobre a instalação de início rápido, consulte Olá [guia de instalação de início rápido](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).

        # Kickstart for provisioning a RHEL 7 Azure VM

        # System authorization information
          auth --enableshadow --passalgo=sha512

        # Use graphical install
        text

        # Do not run hello Setup Agent on first boot
        firstboot --disable

        # Keyboard layouts
        keyboard --vckeymap=us --xlayouts='us'

        # System language
        lang en_US.UTF-8

        # Network information
        network  --bootproto=dhcp

        # Root password
        rootpw --plaintext "to_be_disabled"

        # System services
        services --enabled="sshd,waagent,NetworkManager"

        # System timezone
        timezone Etc/UTC --isUtc --ntpservers 0.rhel.pool.ntp.org,1.rhel.pool.ntp.org,2.rhel.pool.ntp.org,3.rhel.pool.ntp.org

        # Partition clearing information
        clearpart --all --initlabel

        # Clear hello MBR
        zerombr

        # Disk partitioning information
        part /boot --fstype="xfs" --size=500
        part / --fstyp="xfs" --size=1 --grow --asprimary

        # System bootloader configuration
        bootloader --location=mbr

        # Firewall configuration
        firewall --disabled

        # Enable SELinux
        selinux --enforcing

        # Don't configure X
        skipx

        # Power down hello machine after install
        poweroff

        %packages
        @base
        @console-internet
        chrony
        sudo
        parted
        -dracut-config-rescue

        %end

        %post --log=/var/log/anaconda/post-install.log

        #!/bin/bash

        # Register Red Hat Subscription
        subscription-manager register --username=XXX --password=XXX --auto-attach --force

        # Install latest repo update
        yum update -y

        # Enable extras repo
        subscription-manager repos --enable=rhel-7-server-extras-rpms

        # Install WALinuxAgent
        yum install -y WALinuxAgent

        # Unregister Red Hat subscription
        subscription-manager unregister

        # Enable waaagent at boot-up
        systemctl enable waagent

        # Disable hello root account
        usermod root -p '!!'

        # Configure swap in WALinuxAgent
        sed -i 's/^\(ResourceDisk\.EnableSwap\)=[Nn]$/\1=y/g' /etc/waagent.conf
        sed -i 's/^\(ResourceDisk\.SwapSizeMB\)=[0-9]*$/\1=2048/g' /etc/waagent.conf

        # Set hello cmdline
        sed -i 's/^\(GRUB_CMDLINE_LINUX\)=".*"$/\1="console=tty1 console=ttyS0 earlyprintk=ttyS0 rootdelay=300"/g' /etc/default/grub

        # Enable SSH keepalive
        sed -i 's/^#\(ClientAliveInterval\).*$/\1 180/g' /etc/ssh/sshd_config

        # Build hello grub cfg
        grub2-mkconfig -o /boot/grub2/grub.cfg

        # Configure network
        cat << EOF > /etc/sysconfig/network-scripts/ifcfg-eth0
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no
        EOF

        # Deprovision and prepare for Azure
        waagent -force -deprovision

        %end

2. Arquivo de início rápido de saudação local em que o sistema de instalação Olá pode acessá-lo.

3. Crie uma nova máquina virtual no Gerenciador do Hyper-V. Em Olá **conectar disco rígido Virtual** página, selecione **anexar um disco rígido virtual mais tarde**e hello concluir assistente de nova máquina Virtual.

4. Abra as configurações de máquina virtual de saudação:

    a.  Anexe uma nova máquina virtual de toohello disco rígido virtual. Certifique-se de que tooselect **formato VHD** e **tamanho fixo**.

    b.  Anexe instalação Olá unidade de DVD toohello ISO.

    c.  Olá BIOS tooboot do conjunto de CD.

5. Inicie a máquina virtual de saudação. Guia de instalação do hello, pressione **guia** tooconfigure opções de inicialização de saudação.

6. Insira `inst.ks=<hello location of hello kickstart file>` final Olá das opções de inicialização de Olá e pressione **Enter**.

7. Aguarde Olá toofinish de instalação. Quando ele for concluído, máquina virtual de saudação será desligada automaticamente. O VHD Linux está agora pronto toobe carregado tooAzure.

## <a name="known-issues"></a>Problemas conhecidos
### <a name="hello-hyper-v-driver-could-not-be-included-in-hello-initial-ram-disk-when-using-a-non-hyper-v-hypervisor"></a>Olá Hyper-V driver não pode ser incluído no disco de RAM saudação inicial ao usar um hipervisor não Hyper-V

Em alguns casos, instaladores Linux podem não incluir drivers de saudação do Hyper-V no disco de RAM inicial hello (initrd ou initramfs), a menos que Linux detecta que está sendo executado em um ambiente Hyper-V.

Quando você estiver usando um tooprepare do sistema (ou seja, Virtualbox, Xen, etc.) de virtualização diferente em sua imagem do Linux, talvez seja necessário toorebuild initrd tooensure que pelo menos Olá hv_vmbus e módulos de kernel hv_storvsc estão disponíveis no disco de RAM saudação inicial. Isso é um problema conhecido pelo menos em sistemas baseados em distribuição de Red Hat upstream hello.

tooresolve esse problema, adicione tooinitramfs de módulos do Hyper-V e recriá-lo:

Editar `/etc/dracut.conf`e adicione Olá conteúdo a seguir:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

Recrie initramfs:

        # dracut -f -v

Para obter mais detalhes, consulte as informações de saudação sobre [recriação initramfs](https://access.redhat.com/solutions/1958).

## <a name="next-steps"></a>Próximas etapas
Você está agora pronto toouse as Red Hat Enterprise Linux disco rígido virtual toocreate novas máquinas virtuais no Azure. Se isso for Olá primeira vez que você está carregando tooAzure de arquivo. vhd hello, consulte as etapas 2 e 3 em [criando e carregando um disco rígido virtual que contém o sistema de operacional Linux Olá](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

Para obter mais detalhes sobre os hipervisores Olá que são certificadas toorun Red Hat Enterprise Linux, consulte [site do Red Hat Olá](https://access.redhat.com/certified-hypervisors).
