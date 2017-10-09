---
title: aaaCreate e carregar um VHD do Oracle Linux | Microsoft Docs
description: "Saiba toocreate e carregar um Azure disco rígido virtual (VHD) que contém um sistema operacional de Oracle Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-service-management,azure-resource-manager
ms.assetid: dd96f771-26eb-4391-9a89-8c8b6d691822
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: szark
ms.openlocfilehash: be9cf284d7f5e7122a106506a343e53e9f1ac56e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-an-oracle-linux-virtual-machine-for-azure"></a>Preparar uma máquina virtual Oracle Linux para o Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a>Pré-requisitos
Este artigo pressupõe que você já tiver instalado um disco rígido virtual Oracle Linux sistema operacional tooa. Várias ferramentas existem toocreate arquivos. vhd, por exemplo, uma solução de virtualização como o Hyper-V. Para obter instruções, consulte [instalar Olá função Hyper-V e configurar uma máquina Virtual](http://technet.microsoft.com/library/hh846766.aspx).

### <a name="oracle-linux-installation-notes"></a>Notas de instalação do Oracle Linux
* Veja também [Notas de instalação gerais do Linux](create-upload-generic.md#general-linux-installation-notes) para obter mais dicas sobre como preparar o Linux para o Azure.
* O kernel da Oracle, compatível com Red Hat, e seu UEK3 (Unbreakable Enterprise Kernel) têm suporte no Hyper-V e no Azure. Para obter melhores resultados, esteja kernel mais recente do toohello tooupdate-se ao preparar o VHD do Oracle Linux.
* UEK2 da Oracle não tem suporte no Hyper-V e o Azure como não inclui drivers Olá necessário.
* formato do Hello VHDX não tem suporte apenas no Azure, **VHD fixo**.  Você pode converter Olá disco tooVHD formato usando o Gerenciador do Hyper-V ou Olá cmdlet convert-vhd.
* Ao instalar o sistema de Linux Olá é recomendável que você use partições padrão em vez de LVM (geralmente padrão Olá para muitas instalações). Isso evitará LVM nome conflita com VMs clonados, especialmente se um sistema operacional de disco nunca precisa tooanother toobe anexado VMs para solução de problemas. Se você preferir, é possível usar [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) em discos de dados.
* Não há suporte para para tamanhos de VM maiores devido tooa bug nas versões de kernel do Linux abaixo 2.6.37. Esse problema principalmente os impactos distribuições usando Olá vermelho upstream kernel Hat 2.6.32. Instalação manual de agente Linux do Azure de saudação (waagent) desabilitará automaticamente o na configuração de GRUB Olá para o kernel do Linux hello. Para obter mais informações sobre isso podem ser encontradas nas etapas de saudação abaixo.
* Não configure uma partição de troca no disco do sistema operacional hello. agente do Linux Olá pode ser configurado toocreate um arquivo de permuta em disco de recursos temporário hello.  Para obter mais informações sobre isso podem ser encontradas nas etapas de saudação abaixo.
* Todos os VHDs Olá devem ter tamanhos que sejam múltiplos de 1 MB.
* Certifique-se de que Olá `Addons` repositório está habilitado. Editar arquivo hello `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) ou `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux) e altere a linha hello `enabled=0` muito`enabled=1` em **[ol6_addons]** ou **[ol7_addons]** neste arquivo.

## <a name="oracle-linux-64"></a>Oracle Linux 6.4+
Você deve concluir as etapas de configuração específico no sistema operacional Olá Olá toorun de máquina virtual no Azure.

1. No painel central de saudação do Gerenciador do Hyper-V, selecione máquina virtual de saudação.
2. Clique em **conectar** tooopen janela de saudação para a máquina virtual de saudação.
3. Desinstale o Gerenciador executando Olá comando a seguir:
   
        # sudo rpm -e --nodeps NetworkManager
   
    **Observação:** se o pacote de saudação já não estiver instalado, esse comando falhará com uma mensagem de erro. Isso é esperado.
4. Crie um arquivo chamado **rede** em Olá `/etc/sysconfig/` diretório que contém a saudação texto a seguir:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
5. Crie um arquivo chamado **ifcfg eth0** em Olá `/etc/sysconfig/network-scripts/` diretório que contém a saudação texto a seguir:
   
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
   
        # chkconfig network on
8. Instale o python pyasn1 executando Olá comando a seguir:
   
        # sudo yum install python-pyasn1
9. Modificar a linha de inicialização de kernel de saudação em seus parâmetros de kernel adicionais tooinclude grub configuração do Azure. toodo nesse abra "/ boot/grub/menu.lst" em um editor de texto e certifique-se de que kernel de padrão de saudação inclui Olá parâmetros a seguir:
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300 numa=off
   
   Isso garantirá todas as mensagens de console são enviadas toohello primeira porta serial, que pode ajudá-lo Azure suporte à depuração de problemas. Isso irá desabilitar o NUMA devido tooa bug no kernel compatível do Red Hat da Oracle.
   
   Além disso toohello acima, recomenda-se muito*remover* Olá seguintes parâmetros:
   
        rhgb quiet crashkernel=auto
   
   Inicialização gráfica e silenciosa não são úteis em um ambiente de nuvem onde queremos que todos os toobe de logs de saudação enviada toohello de porta serial.
   
   Olá `crashkernel` opção pode ser esquerda configurada, se desejado, mas observe que esse parâmetro será reduzir a quantidade de saudação de memória disponível em Olá VM em 128 MB ou mais, que pode ser problemático em tamanhos de VM menores hello.
10. Certifique-se de servidor SSH hello está instalado e configurado toostart no momento da inicialização.  Geralmente, esse é o padrão de saudação.
11. Instale Olá agente Linux do Azure executando o comando a seguir de saudação. versão mais recente da saudação é 2.0.15.
    
        # sudo yum install WALinuxAgent
    
    Observe que instalar pacote de WALinuxAgent Olá removerá Olá Gerenciador e pacotes de Gerenciador gnome se eles já não foram removidos conforme descrito na etapa 2.
12. Não crie espaço de permuta em disco do sistema operacional hello.
    
    Olá agente Linux do Azure pode configurar automaticamente o espaço de permuta usando Olá disco de recurso local que é anexado toohello VM após a configuração no Azure. Observe que esse disco de recurso local Olá é um *temporário* disco e pode ser esvaziada quando Olá VM for desprovisionada. Depois de instalar o hello agente Linux do Azure (consulte a etapa anterior), modifique Olá seguintes parâmetros em /etc/waagent.conf adequadamente:
    
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

- - -
## <a name="oracle-linux-70"></a>Oracle Linux 7.0 ou posterior
**Alterações no Oracle Linux 7**

Preparando uma máquina de virtual Oracle Linux 7 para o Azure é muito semelhante tooOracle Linux 6, no entanto, há várias diferenças importantes, vale a pena observar:

* Kernel compatível do Red Hat hello e UEK3 da Oracle têm suporte no Azure.  núcleo de UEK3 Olá é recomendado.
* Olá Gerenciador do pacote não está em conflito com o agente do Linux Azure hello. Esse pacote é instalado por padrão e recomendamos que você não o remova.
* GRUB2 agora é usado como Olá carregador de inicialização padrão, para que o procedimento Olá para editar os parâmetros de kernel foi alterada (consulte abaixo).
* XFS agora é um sistema de arquivos padrão de saudação. sistema de arquivos ext4 Olá ainda pode ser usado, se desejado.

**Etapas da configuração**

1. No Gerenciador do Hyper-V, selecione máquina virtual de saudação.
2. Clique em **conectar** tooopen uma janela do console da máquina virtual de saudação.
3. Crie um arquivo chamado **rede** em Olá `/etc/sysconfig/` diretório que contém a saudação texto a seguir:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
4. Crie um arquivo chamado **ifcfg eth0** em Olá `/etc/sysconfig/network-scripts/` diretório que contém a saudação texto a seguir:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
5. Modificar udev regras tooavoid gerar regras estáticas para Olá interfaces Ethernet. Essas regras podem provocar problemas ao clonar uma máquina virtual no Microsoft Azure ou no Hyper-V:
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
6. Certifique-se de que o serviço de rede Olá será iniciado no momento da inicialização executando Olá comando a seguir:
   
        # sudo chkconfig network on
7. Instale o pacote de python pyasn1 de saudação executando Olá comando a seguir:
   
        # sudo yum install python-pyasn1
8. Execute Olá metadados Olá yum atuais tooclear comando a seguir e instale todas as atualizações:
   
        # sudo yum clean all
        # sudo yum -y update
9. Modificar a linha de inicialização de kernel de saudação em seus parâmetros de kernel adicionais tooinclude grub configuração do Azure. toodo nesse abrir "/ padrão/etc/grub" em uma saudação de editor e editar texto `GRUB_CMDLINE_LINUX` parâmetro, por exemplo:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Isso garantirá todas as mensagens de console são enviadas toohello primeira porta serial, que pode ajudá-lo Azure suporte à depuração de problemas. Ela também desativa novas convenções de nomenclatura OEL 7 Olá para as NICs. Além disso toohello acima, recomenda-se muito*remover* Olá seguintes parâmetros:
   
       rhgb quiet crashkernel=auto
   
   Inicialização gráfica e silenciosa não são úteis em um ambiente de nuvem onde queremos que todos os toobe de logs de saudação enviada toohello de porta serial.
   
   Olá `crashkernel` opção pode ser esquerda configurada, se desejado, mas observe que esse parâmetro será reduzir a quantidade de saudação de memória disponível em Olá VM em 128 MB ou mais, que pode ser problemático em tamanhos de VM menores hello.
10. Quando tiver terminado a edição "/ padrão/etc/grub" por acima, execute Olá seguinte comando toorebuild Olá grub configuração:
    
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg
11. Certifique-se de servidor SSH hello está instalado e configurado toostart no momento da inicialização.  Geralmente, esse é o padrão de saudação.
12. Instale Olá agente Linux do Azure executando Olá comando a seguir:
    
        # sudo yum install WALinuxAgent
        # sudo systemctl enable waagent
13. Não crie espaço de permuta em disco do sistema operacional hello.
    
    Olá agente Linux do Azure pode configurar automaticamente o espaço de permuta usando Olá disco de recurso local que é anexado toohello VM após a configuração no Azure. Observe que esse disco de recurso local Olá é um *temporário* disco e pode ser esvaziada quando Olá VM for desprovisionada. Depois de instalar o hello agente Linux do Azure (consulte a etapa anterior Olá), modificar Olá seguintes parâmetros em /etc/waagent.conf adequadamente:
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.
14. Execute Olá seguindo a máquina virtual do comandos toodeprovision hello e prepará-la para provisionamento no Azure:
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
15. Clique em **Ação -> Desligar** no Gerenciador do Hyper-V. O VHD Linux está agora pronto toobe carregado tooAzure.

## <a name="next-steps"></a>Próximas etapas
Você está agora pronto toouse seu Oracle Linux. vhd toocreate novas máquinas virtuais no Azure. Se isso for Olá primeira vez que você está carregando tooAzure de arquivo. vhd hello, consulte as etapas 2 e 3 em [criando e carregando um disco rígido virtual que contém o sistema de operacional Linux Olá](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

