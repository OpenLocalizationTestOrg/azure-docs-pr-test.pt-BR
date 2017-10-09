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
# <a name="prepare-a-centos-based-virtual-machine-for-azure"></a><span data-ttu-id="b3094-103">Preparar uma máquina virtual baseada em CentOS para o Azure</span><span class="sxs-lookup"><span data-stu-id="b3094-103">Prepare a CentOS-based virtual machine for Azure</span></span>
* [<span data-ttu-id="b3094-104">Preparar uma máquina virtual CentOS 6.x para o Azure</span><span class="sxs-lookup"><span data-stu-id="b3094-104">Prepare a CentOS 6.x virtual machine for Azure</span></span>](#centos-6x)
* [<span data-ttu-id="b3094-105">Preparar uma máquina virtual CentOS 7.0 ou posterior para o Azure</span><span class="sxs-lookup"><span data-stu-id="b3094-105">Prepare a CentOS 7.0+ virtual machine for Azure</span></span>](#centos-70)

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="b3094-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b3094-106">Prerequisites</span></span>
<span data-ttu-id="b3094-107">Este artigo pressupõe que você já tiver instalado um CentOS (ou derivado semelhante) Linux tooa rígido disco do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="b3094-107">This article assumes that you have already installed a CentOS (or similar derivative) Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="b3094-108">Várias ferramentas existem toocreate arquivos. vhd, por exemplo, uma solução de virtualização como o Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="b3094-108">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="b3094-109">Para obter instruções, consulte [instalar Olá função Hyper-V e configurar uma máquina Virtual](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="b3094-109">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="b3094-110">**Notas de instalação do CentOS**</span><span class="sxs-lookup"><span data-stu-id="b3094-110">**CentOS installation notes**</span></span>

* <span data-ttu-id="b3094-111">Veja também as [Notas de instalação gerais do Linux](create-upload-generic.md#general-linux-installation-notes) para obter mais dicas sobre como preparar o Linux para o Azure.</span><span class="sxs-lookup"><span data-stu-id="b3094-111">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="b3094-112">formato do Hello VHDX não tem suporte apenas no Azure, **VHD fixo**.</span><span class="sxs-lookup"><span data-stu-id="b3094-112">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="b3094-113">Você pode converter Olá disco tooVHD formato usando o Gerenciador do Hyper-V ou Olá cmdlet convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="b3094-113">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span> <span data-ttu-id="b3094-114">Se você estiver usando VirtualBox isso significa que selecionando **tamanho fixo** como oposição padrão toohello alocada dinamicamente durante a criação de disco de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3094-114">If you are using VirtualBox this means selecting **Fixed size** as opposed toohello default dynamically allocated when creating hello disk.</span></span>
* <span data-ttu-id="b3094-115">Ao instalar o sistema de Linux Olá é *recomendado* que você use partições padrão em vez de LVM (geralmente padrão Olá para muitas instalações).</span><span class="sxs-lookup"><span data-stu-id="b3094-115">When installing hello Linux system it is *recommended* that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="b3094-116">Isso evitará LVM nome conflita com VMs clonados, especialmente se um disco do sistema operacional nunca precisa tooanother toobe anexado VM idêntico para solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="b3094-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother identical VM for troubleshooting.</span></span> <span data-ttu-id="b3094-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) podem ser usados nos discos de dados.</span><span class="sxs-lookup"><span data-stu-id="b3094-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="b3094-118">É necessário suporte a kernel para montar sistemas de arquivos UDF.</span><span class="sxs-lookup"><span data-stu-id="b3094-118">Kernel support for mounting UDF file systems is required.</span></span> <span data-ttu-id="b3094-119">Durante a primeira inicialização hello Azure configuração de provisionamento é passada toohello VM Linux por meio de mídia formatada UDF que é anexado toohello convidado.</span><span class="sxs-lookup"><span data-stu-id="b3094-119">At first boot on Azure hello provisioning configuration is passed toohello Linux VM via UDF-formatted media that is attached toohello guest.</span></span> <span data-ttu-id="b3094-120">agente do Linux Azure Olá deve ser capaz de toomount Olá UDF arquivo sistema tooread sua configuração e provisionar Olá VM.</span><span class="sxs-lookup"><span data-stu-id="b3094-120">hello Azure Linux agent must be able toomount hello UDF file system tooread its configuration and provision hello VM.</span></span>
* <span data-ttu-id="b3094-121">Versões de kernel do Linux abaixo de 2.6.37 não dão suporte ao NUMA no Hyper-V com tamanhos maiores de VM.</span><span class="sxs-lookup"><span data-stu-id="b3094-121">Linux kernel versions below 2.6.37 do not support NUMA on Hyper-V with larger VM sizes.</span></span> <span data-ttu-id="b3094-122">Esse problema principalmente impactos distribuições mais antigas usando Olá upstream kernel Red Hat 2.6.32 e foi corrigido em RHEL 6.6 (kernel-2.6.32-504).</span><span class="sxs-lookup"><span data-stu-id="b3094-122">This issue primarily impacts older distributions using hello upstream Red Hat 2.6.32 kernel, and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="b3094-123">Sistemas que executam kernels personalizados anteriores 2.6.37 ou com base em RHEL kernels mais antigos que 2.6.32-504 deve definir Olá parâmetro de inicialização `numa=off` no kernel de saudação de linha de comando em grub.conf.</span><span class="sxs-lookup"><span data-stu-id="b3094-123">Systems running custom kernels older than 2.6.37, or RHEL-based kernels older than 2.6.32-504 must set hello boot parameter `numa=off` on hello kernel command-line in grub.conf.</span></span> <span data-ttu-id="b3094-124">Para obter mais informações, confira o [KB 436883](https://access.redhat.com/solutions/436883) do Red Hat.</span><span class="sxs-lookup"><span data-stu-id="b3094-124">For more information see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="b3094-125">Não configure uma partição de troca no disco do sistema operacional hello.</span><span class="sxs-lookup"><span data-stu-id="b3094-125">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="b3094-126">agente do Linux Olá pode ser configurado toocreate um arquivo de permuta em disco de recursos temporário hello.</span><span class="sxs-lookup"><span data-stu-id="b3094-126">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="b3094-127">Para obter mais informações sobre isso podem ser encontradas nas etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="b3094-127">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="b3094-128">Todos os VHDs Olá devem ter tamanhos que sejam múltiplos de 1 MB.</span><span class="sxs-lookup"><span data-stu-id="b3094-128">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="centos-6x"></a><span data-ttu-id="b3094-129">CentOS 6.x</span><span class="sxs-lookup"><span data-stu-id="b3094-129">CentOS 6.x</span></span>

1. <span data-ttu-id="b3094-130">No Gerenciador do Hyper-V, selecione máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3094-130">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="b3094-131">Clique em **conectar** tooopen uma janela do console da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3094-131">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="b3094-132">CentOS 6, Gerenciador pode interferir com o agente do Linux Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b3094-132">In CentOS 6, NetworkManager can interfere with hello Azure Linux agent.</span></span> <span data-ttu-id="b3094-133">Desinstale esse pacote executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="b3094-133">Uninstall this package by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

4. <span data-ttu-id="b3094-134">Criar ou editar o arquivo hello `/etc/sysconfig/network` e adicione Olá texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="b3094-134">Create or edit hello file `/etc/sysconfig/network` and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="b3094-135">Criar ou editar o arquivo hello `/etc/sysconfig/network-scripts/ifcfg-eth0` e adicione Olá texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="b3094-135">Create or edit hello file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="b3094-136">Modificar udev regras tooavoid gerar regras estáticas para Olá interfaces Ethernet.</span><span class="sxs-lookup"><span data-stu-id="b3094-136">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="b3094-137">Essas regras podem provocar problemas ao clonar uma máquina virtual no Microsoft Azure ou no Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="b3094-137">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="b3094-138">Certifique-se de que o serviço de rede Olá será iniciado no momento da inicialização executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="b3094-138">Ensure hello network service will start at boot time by running hello following command:</span></span>
   
        # sudo chkconfig network on

8. <span data-ttu-id="b3094-139">Se você quiser toouse espelhos de OpenLogic de saudação que são hospedados no hello datacenters do Azure, em seguida, substitua Olá `/etc/yum.repos.d/CentOS-Base.repo` arquivo com hello repositórios a seguir.</span><span class="sxs-lookup"><span data-stu-id="b3094-139">If you would like toouse hello OpenLogic mirrors that are hosted within hello Azure datacenters, then replace hello `/etc/yum.repos.d/CentOS-Base.repo` file with hello following repositories.</span></span>  <span data-ttu-id="b3094-140">Isso também adicionará Olá **[openlogic]** repositório que inclui pacotes adicionais como o agente do Linux Azure hello:</span><span class="sxs-lookup"><span data-stu-id="b3094-140">This will also add hello **[openlogic]** repository that includes additional packages such as hello Azure Linux agent:</span></span>

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
    <span data-ttu-id="b3094-141">Olá restante deste guia assumirá que você está usando pelo menos Olá `[openlogic]` repositório, que será o agente do Linux Azure Olá tooinstall usado abaixo.</span><span class="sxs-lookup"><span data-stu-id="b3094-141">hello rest of this guide will assume you are using at least hello `[openlogic]` repo, which will be used tooinstall hello Azure Linux agent below.</span></span>


9. <span data-ttu-id="b3094-142">Adicione Olá too/etc/yum.conf linha a seguir:</span><span class="sxs-lookup"><span data-stu-id="b3094-142">Add hello following line too/etc/yum.conf:</span></span>
    
        http_caching=packages

10. <span data-ttu-id="b3094-143">Execute Olá comando tooclear Olá yum metadados e atualização Olá sistema atual com pacotes de saudação mais recentes a seguir:</span><span class="sxs-lookup"><span data-stu-id="b3094-143">Run hello following command tooclear hello current yum metadata and update hello system with hello latest packages:</span></span>
    
        # yum clean all

    <span data-ttu-id="b3094-144">A menos que você estiver criando uma imagem de uma versão mais antiga do CentOS, é recomendável tooupdate que Olá a todos os pacotes toohello mais recente:</span><span class="sxs-lookup"><span data-stu-id="b3094-144">Unless you are creating an image for an older version of CentOS, it is recommended tooupdate all hello packages toohello latest:</span></span>

        # sudo yum -y update

    <span data-ttu-id="b3094-145">Pode ser necessária uma reinicialização depois de executar esse comando.</span><span class="sxs-lookup"><span data-stu-id="b3094-145">A reboot may be required after running this command.</span></span>

11. <span data-ttu-id="b3094-146">(Opcional) Instale drivers de saudação para Olá Integration Services LIS (Linux).</span><span class="sxs-lookup"><span data-stu-id="b3094-146">(Optional) Install hello drivers for hello Linux Integration Services (LIS).</span></span>
   
    >[!IMPORTANT]
    <span data-ttu-id="b3094-147">Olá etapa é **necessária** para CentOS 6.3 e anteriores e opcionais para versões posteriores.</span><span class="sxs-lookup"><span data-stu-id="b3094-147">hello step is **required** for CentOS 6.3 and earlier, and optional for later releases.</span></span>

        # sudo rpm -e hypervkvpd  ## (may return error if not installed, that's OK)
        # sudo yum install microsoft-hyper-v

    <span data-ttu-id="b3094-148">Como alternativa, você pode seguir as instruções de instalação manual de saudação em Olá [página de download do LIS](https://go.microsoft.com/fwlink/?linkid=403033) tooinstall Olá RPM em sua VM.</span><span class="sxs-lookup"><span data-stu-id="b3094-148">Alternatively, you can follow hello manual installation instructions on hello [LIS download page](https://go.microsoft.com/fwlink/?linkid=403033) tooinstall hello RPM onto your VM.</span></span>
 
12. <span data-ttu-id="b3094-149">Instale Olá agente Linux do Azure e as dependências:</span><span class="sxs-lookup"><span data-stu-id="b3094-149">Install hello Azure Linux Agent and dependencies:</span></span>
    
        # sudo yum install python-pyasn1 WALinuxAgent
    
    <span data-ttu-id="b3094-150">pacote de WALinuxAgent Olá removerá hello Gerenciador e pacotes de Gerenciador gnome se eles já não foram removidos conforme descrito na etapa 3.</span><span class="sxs-lookup"><span data-stu-id="b3094-150">hello WALinuxAgent package will remove hello NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 3.</span></span>


13. <span data-ttu-id="b3094-151">Modificar a linha de inicialização de kernel de saudação em seus parâmetros de kernel adicionais tooinclude grub configuração do Azure.</span><span class="sxs-lookup"><span data-stu-id="b3094-151">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="b3094-152">toodo isso, abra `/boot/grub/menu.lst` em um editor de texto e certifique-se de que kernel de padrão de saudação inclui Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="b3094-152">toodo this, open `/boot/grub/menu.lst` in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="b3094-153">Isso garantirá todas as mensagens de console são enviadas toohello primeira porta serial, que pode ajudá-lo Azure suporte à depuração de problemas.</span><span class="sxs-lookup"><span data-stu-id="b3094-153">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="b3094-154">Além disso toohello acima, recomenda-se muito*remover* Olá seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="b3094-154">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="b3094-155">Inicialização gráfica e silenciosa não são úteis em um ambiente de nuvem onde queremos que todos os toobe de logs de saudação enviada toohello de porta serial.</span><span class="sxs-lookup"><span data-stu-id="b3094-155">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>  <span data-ttu-id="b3094-156">Olá `crashkernel` opção pode ser esquerda configurada, se desejado, mas observe que esse parâmetro será reduzir a quantidade de saudação de memória disponível em Olá VM em 128 MB ou mais, que pode ser problemático em tamanhos de VM menores hello.</span><span class="sxs-lookup"><span data-stu-id="b3094-156">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>

    >[!Important]
    <span data-ttu-id="b3094-157">CentOS 6.5 e anteriores também devem definir o parâmetro de kernel hello `numa=off`.</span><span class="sxs-lookup"><span data-stu-id="b3094-157">CentOS 6.5 and earlier must also set hello kernel parameter `numa=off`.</span></span> <span data-ttu-id="b3094-158">Consulte Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="b3094-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

14. <span data-ttu-id="b3094-159">Certifique-se de servidor SSH hello está instalado e configurado toostart no momento da inicialização.</span><span class="sxs-lookup"><span data-stu-id="b3094-159">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="b3094-160">Geralmente, esse é o padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3094-160">This is usually hello default.</span></span>

15. <span data-ttu-id="b3094-161">Não crie espaço de permuta em disco do sistema operacional hello.</span><span class="sxs-lookup"><span data-stu-id="b3094-161">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="b3094-162">Olá agente Linux do Azure pode configurar automaticamente o espaço de permuta usando Olá disco de recurso local que é anexado toohello VM após a configuração no Azure.</span><span class="sxs-lookup"><span data-stu-id="b3094-162">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="b3094-163">Observe que esse disco de recurso local Olá é um *temporário* disco e pode ser esvaziada quando Olá VM for desprovisionada.</span><span class="sxs-lookup"><span data-stu-id="b3094-163">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="b3094-164">Depois de instalar o hello agente Linux do Azure (consulte a etapa anterior), modifique Olá parâmetros a seguir `/etc/waagent.conf` adequadamente:</span><span class="sxs-lookup"><span data-stu-id="b3094-164">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. <span data-ttu-id="b3094-165">Execute Olá seguindo a máquina virtual do comandos toodeprovision hello e prepará-la para provisionamento no Azure:</span><span class="sxs-lookup"><span data-stu-id="b3094-165">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

17. <span data-ttu-id="b3094-166">Clique em **Ação -> Desligar** no Gerenciador do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="b3094-166">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="b3094-167">O VHD Linux está agora pronto toobe carregado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b3094-167">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>


- - -
## <a name="centos-70"></a><span data-ttu-id="b3094-168">CentOS 7.0+</span><span class="sxs-lookup"><span data-stu-id="b3094-168">CentOS 7.0+</span></span>
<span data-ttu-id="b3094-169">**Alterações no CentOS 7 (e em derivativos similares)**</span><span class="sxs-lookup"><span data-stu-id="b3094-169">**Changes in CentOS 7 (and similar derivatives)**</span></span>

<span data-ttu-id="b3094-170">Preparando uma máquina virtual de CentOS 7 para o Azure é muito semelhante tooCentOS 6, no entanto, há várias diferenças importantes, vale a pena observar:</span><span class="sxs-lookup"><span data-stu-id="b3094-170">Preparing a CentOS 7 virtual machine for Azure is very similar tooCentOS 6, however there are several important differences worth noting:</span></span>

* <span data-ttu-id="b3094-171">Olá Gerenciador do pacote não está em conflito com o agente do Linux Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b3094-171">hello NetworkManager package no longer conflicts with hello Azure Linux agent.</span></span> <span data-ttu-id="b3094-172">Esse pacote é instalado por padrão e recomendamos que você não o remova.</span><span class="sxs-lookup"><span data-stu-id="b3094-172">This package is installed by default and we recommend that it is not removed.</span></span>
* <span data-ttu-id="b3094-173">GRUB2 agora é usado como Olá carregador de inicialização padrão, para que o procedimento Olá para editar os parâmetros de kernel foi alterada (consulte abaixo).</span><span class="sxs-lookup"><span data-stu-id="b3094-173">GRUB2 is now used as hello default bootloader, so hello procedure for editing kernel parameters has changed (see below).</span></span>
* <span data-ttu-id="b3094-174">XFS agora é um sistema de arquivos padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3094-174">XFS is now hello default file system.</span></span> <span data-ttu-id="b3094-175">sistema de arquivos ext4 Olá ainda pode ser usado, se desejado.</span><span class="sxs-lookup"><span data-stu-id="b3094-175">hello ext4 file system can still be used if desired.</span></span>

<span data-ttu-id="b3094-176">**Etapas da configuração**</span><span class="sxs-lookup"><span data-stu-id="b3094-176">**Configuration Steps**</span></span>

1. <span data-ttu-id="b3094-177">No Gerenciador do Hyper-V, selecione máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3094-177">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="b3094-178">Clique em **conectar** tooopen uma janela do console da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3094-178">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="b3094-179">Criar ou editar o arquivo hello `/etc/sysconfig/network` e adicione Olá texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="b3094-179">Create or edit hello file `/etc/sysconfig/network` and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. <span data-ttu-id="b3094-180">Criar ou editar o arquivo hello `/etc/sysconfig/network-scripts/ifcfg-eth0` e adicione Olá texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="b3094-180">Create or edit hello file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. <span data-ttu-id="b3094-181">Modificar udev regras tooavoid gerar regras estáticas para Olá interfaces Ethernet.</span><span class="sxs-lookup"><span data-stu-id="b3094-181">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="b3094-182">Essas regras podem provocar problemas ao clonar uma máquina virtual no Microsoft Azure ou no Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="b3094-182">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

6. <span data-ttu-id="b3094-183">Se você quiser toouse espelhos de OpenLogic de saudação que são hospedados no hello datacenters do Azure, em seguida, substitua Olá `/etc/yum.repos.d/CentOS-Base.repo` arquivo com hello repositórios a seguir.</span><span class="sxs-lookup"><span data-stu-id="b3094-183">If you would like toouse hello OpenLogic mirrors that are hosted within hello Azure datacenters, then replace hello `/etc/yum.repos.d/CentOS-Base.repo` file with hello following repositories.</span></span>  <span data-ttu-id="b3094-184">Isso também adicionará Olá **[openlogic]** repositório que inclui pacotes de agente do Linux Azure hello:</span><span class="sxs-lookup"><span data-stu-id="b3094-184">This will also add hello **[openlogic]** repository that includes packages for hello Azure Linux agent:</span></span>
   
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
    <span data-ttu-id="b3094-185">Olá restante deste guia assumirá que você está usando pelo menos Olá `[openlogic]` repositório, que será o agente do Linux Azure Olá tooinstall usado abaixo.</span><span class="sxs-lookup"><span data-stu-id="b3094-185">hello rest of this guide will assume you are using at least hello `[openlogic]` repo, which will be used tooinstall hello Azure Linux agent below.</span></span>

7. <span data-ttu-id="b3094-186">Execute Olá metadados Olá yum atuais tooclear comando a seguir e instale todas as atualizações:</span><span class="sxs-lookup"><span data-stu-id="b3094-186">Run hello following command tooclear hello current yum metadata and install any updates:</span></span>
   
        # sudo yum clean all

    <span data-ttu-id="b3094-187">A menos que você estiver criando uma imagem de uma versão mais antiga do CentOS, é recomendável tooupdate que Olá a todos os pacotes toohello mais recente:</span><span class="sxs-lookup"><span data-stu-id="b3094-187">Unless you are creating an image for an older version of CentOS, it is recommended tooupdate all hello packages toohello latest:</span></span>

        # sudo yum -y update

    <span data-ttu-id="b3094-188">Uma reinicialização necessária talvez depois de executar esse comando.</span><span class="sxs-lookup"><span data-stu-id="b3094-188">A reboot maybe required after running this command.</span></span>

8. <span data-ttu-id="b3094-189">Modificar a linha de inicialização de kernel de saudação em seus parâmetros de kernel adicionais tooinclude grub configuração do Azure.</span><span class="sxs-lookup"><span data-stu-id="b3094-189">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="b3094-190">toodo isso, abra `/etc/default/grub` em uma saudação de editor e editar texto `GRUB_CMDLINE_LINUX` parâmetro, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b3094-190">toodo this, open `/etc/default/grub` in a text editor and edit hello `GRUB_CMDLINE_LINUX` parameter, for example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="b3094-191">Isso garantirá todas as mensagens de console são enviadas toohello primeira porta serial, que pode ajudá-lo Azure suporte à depuração de problemas.</span><span class="sxs-lookup"><span data-stu-id="b3094-191">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="b3094-192">Ela também desativa novas convenções de nomenclatura CentOS 7 Olá para as NICs.</span><span class="sxs-lookup"><span data-stu-id="b3094-192">It also turns off hello new CentOS 7 naming conventions for NICs.</span></span> <span data-ttu-id="b3094-193">Além disso toohello acima, recomenda-se muito*remover* Olá seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="b3094-193">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="b3094-194">Inicialização gráfica e silenciosa não são úteis em um ambiente de nuvem onde queremos que todos os toobe de logs de saudação enviada toohello de porta serial.</span><span class="sxs-lookup"><span data-stu-id="b3094-194">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="b3094-195">Olá `crashkernel` opção pode ser esquerda configurada, se desejado, mas observe que esse parâmetro será reduzir a quantidade de saudação de memória disponível em Olá VM em 128 MB ou mais, que pode ser problemático em tamanhos de VM menores hello.</span><span class="sxs-lookup"><span data-stu-id="b3094-195">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>

9. <span data-ttu-id="b3094-196">Quando terminar edição `/etc/default/grub` por acima, execute Olá seguinte comando toorebuild Olá grub configuração:</span><span class="sxs-lookup"><span data-stu-id="b3094-196">Once you are done editing `/etc/default/grub` per above, run hello following command toorebuild hello grub configuration:</span></span>
   
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

10. <span data-ttu-id="b3094-197">Se a criação de imagem de saudação do **VMWare, VirtualBox ou KVM:** Certifique-se de Olá Hyper-V drivers é inclusos Olá initramfs:</span><span class="sxs-lookup"><span data-stu-id="b3094-197">If building hello image from **VMWare, VirtualBox or KVM:** Ensure hello Hyper-V drivers are included in hello initramfs:</span></span>
   
   <span data-ttu-id="b3094-198">Edite `/etc/dracut.conf`e adicione o conteúdo:</span><span class="sxs-lookup"><span data-stu-id="b3094-198">Edit `/etc/dracut.conf`, add content:</span></span>
   
        add_drivers+=”hv_vmbus hv_netvsc hv_storvsc”
   
   <span data-ttu-id="b3094-199">Recrie Olá initramfs:</span><span class="sxs-lookup"><span data-stu-id="b3094-199">Rebuild hello initramfs:</span></span>
   
        # sudo dracut –f -v

11. <span data-ttu-id="b3094-200">Instale Olá agente Linux do Azure e as dependências:</span><span class="sxs-lookup"><span data-stu-id="b3094-200">Install hello Azure Linux Agent and dependencies:</span></span>

        # sudo yum install python-pyasn1 WALinuxAgent
        # sudo systemctl enable waagent

12. <span data-ttu-id="b3094-201">Não crie espaço de permuta em disco do sistema operacional hello.</span><span class="sxs-lookup"><span data-stu-id="b3094-201">Do not create swap space on hello OS disk.</span></span>
   
   <span data-ttu-id="b3094-202">Olá agente Linux do Azure pode configurar automaticamente o espaço de permuta usando Olá disco de recurso local que é anexado toohello VM após a configuração no Azure.</span><span class="sxs-lookup"><span data-stu-id="b3094-202">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="b3094-203">Observe que esse disco de recurso local Olá é um *temporário* disco e pode ser esvaziada quando Olá VM for desprovisionada.</span><span class="sxs-lookup"><span data-stu-id="b3094-203">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="b3094-204">Depois de instalar o hello agente Linux do Azure (consulte a etapa anterior), modifique Olá parâmetros a seguir `/etc/waagent.conf` adequadamente:</span><span class="sxs-lookup"><span data-stu-id="b3094-204">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>
   
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. <span data-ttu-id="b3094-205">Execute Olá seguindo a máquina virtual do comandos toodeprovision hello e prepará-la para provisionamento no Azure:</span><span class="sxs-lookup"><span data-stu-id="b3094-205">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

14. <span data-ttu-id="b3094-206">Clique em **Ação -> Desligar** no Gerenciador do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="b3094-206">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="b3094-207">O VHD Linux está agora pronto toobe carregado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b3094-207">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3094-208">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b3094-208">Next steps</span></span>
<span data-ttu-id="b3094-209">Você está agora pronto toouse seu CentOS Linux disco rígido virtual toocreate novas máquinas virtuais no Azure.</span><span class="sxs-lookup"><span data-stu-id="b3094-209">You're now ready toouse your CentOS Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="b3094-210">Se isso for Olá primeira vez que você está carregando tooAzure de arquivo. vhd hello, consulte as etapas 2 e 3 em [criando e carregando um disco rígido virtual que contém o sistema de operacional Linux Olá](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b3094-210">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

