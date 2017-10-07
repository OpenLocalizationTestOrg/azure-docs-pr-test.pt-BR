---
title: aaaCreate e carregar um VHD do Linux no Azure
description: "Saiba toocreate e carregar um Azure disco rígido virtual (VHD) que contém um sistema operacional Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: d351396c-95a0-4092-b7bf-c6aae0bbd112
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 208e15c035edb5520fc29ba8e4e71c42b041864d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="information-for-non-endorsed-distributions"></a>Informações para as distribuições não endossadas
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

a plataforma Windows Azure SLA Hello aplica toovirtual máquinas em execução Olá SO Linux somente quando um de saudação [aprovados distribuições](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) é usado. Todas as distribuições do Linux que são fornecidas no hello Azure Galeria de imagens são aprovados distribuições com a configuração solicitada hello.

* [Linux no Azure - Distribuições endossadas](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Suporte para imagens Linux no Microsoft Azure](https://support.microsoft.com/kb/2941892)

Todas as distribuições em execução no Azure serão necessário toomeet um número de pré-requisitos toohave um tooproperly chance executado na plataforma de saudação.  Este artigo não é abrangente como cada distribuição é diferente; e é bem possível que, mesmo se você atender a todos os Olá critérios abaixo que você ainda precisará toosignificantly ajustar sua tooensure de sistema do Linux que ele é executado corretamente na plataforma de saudação.

Por isso, recomendamos que você inicie com uma das nossas [distribuições endossadas do Linux no Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) sempre que possível. Olá artigos a seguir orientará como tooprepare Olá vários aprovados distribuições do Linux com suporte no Azure:

* **[Distribuições com base em CentOS](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**

restante Olá deste artigo se concentrará em diretrizes gerais para executar sua distribuição do Linux no Azure.

## <a name="general-linux-installation-notes"></a>Notas de instalação gerais do Linux
* formato do Hello VHDX não tem suporte apenas no Azure, **VHD fixo**.  Você pode converter Olá disco tooVHD formato usando o Gerenciador do Hyper-V ou Olá cmdlet convert-vhd. Se você estiver usando VirtualBox isso significa que selecionando **tamanho fixo** como oposição padrão toohello alocada dinamicamente durante a criação de disco de saudação.
* O Azure oferece suporte somente para máquinas virtuais de geração 1. Você pode converter uma geração 1 máquina virtual de formato de arquivo VHD VHDX toohello em expansão dinâmica tooa fixada em tamanho de disco. Mas não é possível alterar a geração de uma máquina virtual. Para saber mais, confira [Devo criar uma máquina virtual de geração 1 ou 2 no Hyper-V?](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v)
* tamanho máximo de saudação permitido para Olá que VHD é 1.023 GB.
* Ao instalar o sistema de Linux Olá é *recomendado* que você use partições padrão em vez de LVM (geralmente padrão Olá para muitas instalações). Isso evitará LVM nome conflita com VMs clonados, especialmente se um disco do sistema operacional nunca precisa tooanother toobe anexado VM idêntico para solução de problemas. [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) podem ser usados nos discos de dados.
* É necessário suporte a kernel para montar sistemas de arquivos UDF. Durante a primeira inicialização hello Azure configuração de provisionamento é passada toohello VM Linux por meio de mídia formatada UDF que é anexado toohello convidado. agente do Linux Azure Olá deve ser capaz de toomount Olá UDF arquivo sistema tooread sua configuração e provisionar Olá VM.
* Versões de kernel do Linux abaixo de 2.6.37 não dão suporte ao NUMA no Hyper-V com tamanhos maiores de VM. Esse problema principalmente impactos distribuições mais antigas usando Olá upstream kernel Red Hat 2.6.32 e foi corrigido em RHEL 6.6 (kernel-2.6.32-504). Sistemas que executam kernels personalizados anteriores 2.6.37 ou com base em RHEL kernels mais antigos que 2.6.32-504 deve definir Olá parâmetro de inicialização `numa=off` no kernel de saudação de linha de comando em grub.conf. Para obter mais informações, confira o [KB 436883](https://access.redhat.com/solutions/436883) do Red Hat.
* Não configure uma partição de troca no disco do sistema operacional hello. agente do Linux Olá pode ser configurado toocreate um arquivo de permuta em disco de recursos temporário hello.  Para obter mais informações sobre isso podem ser encontradas nas etapas de saudação abaixo.
* Todos os VHDs Olá devem ter tamanhos que sejam múltiplos de 1 MB.

### <a name="installing-kernel-modules-without-hyper-v"></a>Instalação dos módulos de kernel sem Hyper-V
Azure é executado no hipervisor do Hyper-V hello, para que Linux requer que determinados módulos de kernel estão instalados na ordem toorun no Azure. Se você tiver uma VM que foi criada fora do Hyper-V, instaladores de Linux Olá não inclua drivers de saudação do Hyper-V ramdisk de saudação inicial (initrd ou initramfs), a menos que ele detecta que está executando um um ambiente Hyper-V. Ao usar um tooprepare do sistema (ou seja, Virtualbox, KVM, etc.) de virtualização diferente em sua imagem do Linux, talvez seja necessário toorebuild Olá initrd tooensure que pelo menos Olá `hv_vmbus` e `hv_storvsc` módulos de kernel estão disponíveis no ramdisk de saudação inicial.  Isso é um problema conhecido pelo menos em sistemas com base na distribuição de Red Hat upstream hello.

mecanismo de saudação para a recriação de imagem de saudação initrd ou initramfs pode variar dependendo distribuição hello. Por favor, consulte a documentação da distribuição ou suporte para procedimento adequado hello.  Aqui está um exemplo de como toorebuild Olá initrd usando Olá `mkinitrd` utilitário:

Primeiro, fazer backup de imagem existente de initrd hello:

    # cd /boot
    # sudo cp initrd-`uname -r`.img  initrd-`uname -r`.img.bak

Em seguida, recrie initrd Olá com hello `hv_vmbus` e `hv_storvsc` módulos de kernel:

    # sudo mkinitrd --preload=hv_storvsc --preload=hv_vmbus -v -f initrd-`uname -r`.img `uname -r`


### <a name="resizing-vhds"></a>Redimensionando VHDs
Imagens de VHD no Azure devem ter um tamanho virtual alinhado too1MB.  Normalmente, os VHDs criados usando o Hyper-V já foram alinhados corretamente.  Se Olá VHD não está alinhado corretamente em seguida, você poderá receber um erro mensagem semelhante toohello a seguir ao tentar toocreate um *imagem* de seu VHD:

    "hello VHD http://<mystorageaccount>.blob.core.windows.net/vhds/MyLinuxVM.vhd has an unsupported virtual size of 21475270656 bytes. hello size must be a whole number (in MBs).”

tooremedy isso você pode redimensionar Olá VM usando o console do Gerenciador do Hyper-V hello ou hello [Resize-VHD](http://technet.microsoft.com/library/hh848535.aspx) cmdlet do Powershell.  Se você não estiver executando em um ambiente Windows, em seguida, ele é recomendado toouse img qemu tooconvert (se necessário) e redimensionar Olá VHD.

> [!NOTE]
> Há um bug conhecido nas versões qemu-img > = 2.2.1 que resulta em um VHD formatado incorretamente. Olá problema foi corrigido na versão 2.6 do QEMU. É recomendável toouse qemu-img 2.2.0 ou inferior ou atualização too2.6 ou superior. Referência: https://bugs.launchpad.net/qemu/+bug/1490611.
> 
> 

1. Redimensionando Olá VHD diretamente usando ferramentas como `qemu-img` ou `vbox-manage` pode resultar em um VHD não inicializável.  Ele é recomendado toofirst convert Olá imagem de disco VHD tooa.  Se a imagem da VM Olá já foi criada como imagem de disco (padrão de saudação para alguns hipervisores como KVM), você pode ignorar esta etapa:
   
       # qemu-img convert -f vpc -O raw MyLinuxVM.vhd MyLinuxVM.raw

2. Calcule Olá necessário tamanho de saudação tooensure de imagem de disco que Olá tamanho virtual é too1MB alinhados.  Olá após o script de shell bash pode ajudar com isso.  Olá script usa "`qemu-img info`" toodetermine Olá virtual tamanho da imagem de disco de saudação e, em seguida, calcula Olá tamanho toohello Avançar 1 MB:
   
       rawdisk="MyLinuxVM.raw"
       vhddisk="MyLinuxVM.vhd"
   
       MB=$((1024*1024))
       size=$(qemu-img info -f raw --output json "$rawdisk" | \
              gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')
   
       rounded_size=$((($size/$MB + 1)*$MB))
       echo "Rounded Size = $rounded_size"

3. Redimensione disco bruto de saudação usando $rounded_size como definido no hello acima script:
   
       # qemu-img resize MyLinuxVM.raw $rounded_size

4. Agora, converta Olá disco RAW back tooa VHD de tamanho fixo:
   
       # qemu-img convert -f raw -o subformat=fixed -O vpc MyLinuxVM.raw MyLinuxVM.vhd

   Ou, com a versão de qemu **2.6 +** incluem hello `force_size` opção:

       # qemu-img convert -f raw -o subformat=fixed,force_size -O vpc MyLinuxVM.raw MyLinuxVM.vhd

## <a name="linux-kernel-requirements"></a>Requisitos do kernel do Linux
Olá drivers do Integration Services LIS (Linux) do Hyper-V e do Azure são a contribuição diretamente toohello upstream kernel do Linux. Muitas distribuições que contam com uma versão recente do kernel do Linux (por exemplo, versões 3.x) já terão esses drivers ou fornecerão versões revertidas desses drivers com seus kernels.  Esses drivers constantemente estão sendo atualizados no kernel de upstream Olá com novas correções e recursos, portanto quando possível, é recomendável toorun um [aprovados distribuição](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) que incluirá essas correções e atualizações.

Se você estiver executando uma variante do Red Hat Enterprise Linux versões **6.0 6.3**, será necessário tooinstall Olá LIS drivers de Hyper-v. Olá drivers podem ser encontrados [neste local](http://go.microsoft.com/fwlink/p/?LinkID=254263&clcid=0x409). A partir do RHEL **6.4 +** (e derivados) drivers LIS Olá já são incluídos no kernel Olá e portanto, não há pacotes de instalação adicionais é necessária toorun esses sistemas no Azure.

Se um kernel personalizado for necessário, é recomendável toouse uma versão mais recente do kernel (ou seja, **3.8 +**). Para as distribuições ou fornecedores que mantêm seu próprios kernel, alguns esforço será necessário tooregularly backport Olá LIS drivers do kernel personalizado do tooyour Olá kernel upstream.  Mesmo se você já estiver executando uma versão de kernel relativamente recentes, é altamente recomendável tookeep controlar qualquer upstream correções backport e drivers LIS Olá aqueles conforme necessário. local de Olá Olá LIS driver de arquivos de origem está disponível no hello [MANTENEDORES](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/MAINTAINERS) arquivo na árvore de origem de kernel Olá Linux:

    F:    arch/x86/include/asm/mshyperv.h
    F:    arch/x86/include/uapi/asm/hyperv.h
    F:    arch/x86/kernel/cpu/mshyperv.c
    F:    drivers/hid/hid-hyperv.c
    F:    drivers/hv/
    F:    drivers/input/serio/hyperv-keyboard.c
    F:    drivers/net/hyperv/
    F:    drivers/scsi/storvsc_drv.c
    F:    drivers/video/fbdev/hyperv_fb.c
    F:    include/linux/hyperv.h
    F:    tools/hv/

Em um mínimo, ausência Olá Olá patches a seguir são conhecidos toocause problemas no Azure e então eles devem ser incluídos no kernel hello. De forma alguma essa lista pode ser considerada completa para todas as distribuições:

* [ata_piix: adiar drivers toohello Hyper-V de discos por padrão](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/drivers/ata/ata_piix.c?id=cd006086fa5d91414d8ff9ff2b78fbb593878e3c)
* [storvsc: conta para os pacotes em trânsito no caminho de redefinição de saudação](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/drivers/scsi/storvsc_drv.c?id=5c1b10ab7f93d24f29b5630286e323d1c5802d5c)
* [storvsc: evite o uso de WRITE_SAME](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=3e8f4f4065901c8dfc51407e1984495e1748c090)
* [storvsc: desabilite WRITE SAME para RAID e drivers do adaptador de host virtual](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=54b2b50c20a61b51199bedb6e5d2f8ec2568fb43)
* [storvsc: correção de desreferência de ponteiro NULL](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=b12bb60d6c350b348a4e1460cd68f97ccae9822e)
* [storvsc: as falhas do buffer de anéis podem resultar em congelamento de E/S](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=e86fb5e8ab95f10ec5f2e9430119d5d35020c951)
* [scsi_sysfs: proteger contra a execução dupla de __scsi_remove_device](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/scsi_sysfs.c?id=be821fd8e62765de43cc4f0e2db363d0e30a7e9b)

## <a name="hello-azure-linux-agent"></a>Olá agente Linux do Azure
Olá [agente Linux do Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (waagent) é necessário tooproperly provisionar uma máquina virtual do Linux no Azure. Obter a versão mais recente do hello, problemas de arquivos ou enviar solicitações de recepção no hello [repositório GitHub de agente Linux](https://github.com/Azure/WALinuxAgent).

* agente do Linux Olá foi lançado sob licença Olá Apache 2.0. Muitas distribuições já fornecem RPM ou deb pacotes para agente Olá, e então em alguns casos isso pode ser instalado e atualizado com pouco esforço.
* Olá agente Linux do Azure requer Python v 2.6 +.
* Agente de Olá também requer o módulo de python pyasn1 hello. A maioria das distribuições fornece esse módulo como uma pacote autônomo instalável.
* Em alguns casos Olá agente Linux do Azure pode não ser compatível com o Gerenciador. Vários pacotes RPM/Deb Olá fornecidos pelo distribuições de configurar Gerenciador como um pacote de waagent toohello conflito e, portanto, serão desinstalado Gerenciador quando você instala o pacote do agente Linux hello.

## <a name="general-linux-system-requirements"></a>Requisitos gerais do sistema Linux

* Modifique a linha de inicialização de kernel de saudação no GRUB ou GRUB2 Olá tooinclude parâmetros a seguir. Isso garantirá todas as mensagens de console são enviadas toohello primeira porta serial, que pode ajudá-lo Azure suporte à depuração de problemas:
  
        console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300
  
    Isso garantirá todas as mensagens de console são enviadas toohello primeira porta serial, que pode ajudá-lo Azure suporte à depuração de problemas.
  
    Além disso toohello acima, recomenda-se muito*remover* Olá parâmetros a seguir se eles existirem:
  
        rhgb quiet crashkernel=auto
  
    Inicialização gráfica e silenciosa não são úteis em um ambiente de nuvem onde queremos que todos os toobe de logs de saudação enviada toohello de porta serial. Olá `crashkernel` opção pode ser esquerda configurada, se desejado, mas observe que esse parâmetro será reduzir a quantidade de saudação de memória disponível em Olá VM em 128 MB ou mais, que pode ser problemático em tamanhos de VM menores hello.

* Olá instalar agente Linux do Azure
  
    Olá agente Linux do Azure é necessária para o provisionamento de uma imagem do Linux no Azure.  Muitas distribuições fornecem agente hello como um pacote RPM ou Deb (pacote de saudação é geralmente chamado 'WALinuxAgent' ou 'walinuxagent').  Olá agente também pode ser instalado manualmente seguindo as etapas Olá Olá [guia do agente Linux](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

* Certifique-se de servidor SSH hello está instalado e configurado toostart no momento da inicialização.  Geralmente, esse é o padrão de saudação.

* Não crie espaço de permuta em disco do sistema operacional Olá
  
    Olá agente Linux do Azure pode configurar automaticamente o espaço de permuta usando Olá disco de recurso local que é anexado toohello VM após a configuração no Azure. Observe que esse disco de recurso local Olá é um *temporário* disco e pode ser esvaziada quando Olá VM for desprovisionada. Depois de instalar o hello agente Linux do Azure (consulte a etapa anterior), modifique Olá seguintes parâmetros em /etc/waagent.conf adequadamente:
  
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

* Como etapa final, execute Olá comandos toodeprovision Olá virtual máquina a seguir:
  
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
  
  > [!NOTE]
  > Em Virtualbox, você poderá ver Olá erro a seguir depois de executar ' waagent-force - desprovisionamento ': `[Errno 5] Input/output error`. Essa mensagem de erro não é crítica e pode ser ignorada.
  > 
  > 

* Em seguida, será necessário tooshut máquina virtual do hello e carregar Olá VHD tooAzure.

