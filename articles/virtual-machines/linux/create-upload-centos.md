---
title: Criar e carregar um VHD Linux baseado em CentOS no Azure
description: "Saiba como criar e carregar um VHD (disco rígido virtual) do Azure que contenha um sistema operacional Linux baseado em CentOS."
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
ms.openlocfilehash: 010f4b05b35fa1f31c14f34a5fae9298fcd831e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-a-centos-based-virtual-machine-for-azure"></a><span data-ttu-id="d9172-103">Preparar uma máquina virtual baseada em CentOS para o Azure</span><span class="sxs-lookup"><span data-stu-id="d9172-103">Prepare a CentOS-based virtual machine for Azure</span></span>
* [<span data-ttu-id="d9172-104">Preparar uma máquina virtual CentOS 6.x para o Azure</span><span class="sxs-lookup"><span data-stu-id="d9172-104">Prepare a CentOS 6.x virtual machine for Azure</span></span>](#centos-6x)
* [<span data-ttu-id="d9172-105">Preparar uma máquina virtual CentOS 7.0 ou posterior para o Azure</span><span class="sxs-lookup"><span data-stu-id="d9172-105">Prepare a CentOS 7.0+ virtual machine for Azure</span></span>](#centos-70)

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="d9172-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d9172-106">Prerequisites</span></span>
<span data-ttu-id="d9172-107">Este artigo pressupõe que você já instalou um sistema operacional Linux CentOS (ou derivado similar) em um disco rígido virtual.</span><span class="sxs-lookup"><span data-stu-id="d9172-107">This article assumes that you have already installed a CentOS (or similar derivative) Linux operating system to a virtual hard disk.</span></span> <span data-ttu-id="d9172-108">Existem várias ferramentas para criar arquivos .vhd, por exemplo, uma solução de virtualização como o Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="d9172-108">Multiple tools exist to create .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="d9172-109">Para obter instruções, consulte [Instalar a função Hyper-V e configurar uma máquina Virtual](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="d9172-109">For instructions, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="d9172-110">**Notas de instalação do CentOS**</span><span class="sxs-lookup"><span data-stu-id="d9172-110">**CentOS installation notes**</span></span>

* <span data-ttu-id="d9172-111">Veja também [Notas de instalação gerais do Linux](create-upload-generic.md#general-linux-installation-notes) para obter mais dicas sobre como preparar o Linux para o Azure.</span><span class="sxs-lookup"><span data-stu-id="d9172-111">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="d9172-112">O formato VHDX não tem suporte no Azure, somente o **VHD fixo**.</span><span class="sxs-lookup"><span data-stu-id="d9172-112">The VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="d9172-113">Você pode converter o disco em formato VHD usando o Gerenciador do Hyper-V ou o cmdlet convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="d9172-113">You can convert the disk to VHD format using Hyper-V Manager or the convert-vhd cmdlet.</span></span> <span data-ttu-id="d9172-114">Se você estiver usando o VirtualBox, isso significará selecionar **Tamanho fixo** em vez do padrão alocado dinamicamente durante a criação do disco.</span><span class="sxs-lookup"><span data-stu-id="d9172-114">If you are using VirtualBox this means selecting **Fixed size** as opposed to the default dynamically allocated when creating the disk.</span></span>
* <span data-ttu-id="d9172-115">Ao instalar o sistema Linux, é *recomendável* que você use partições padrão em vez de LVM (geralmente o padrão para muitas instalações).</span><span class="sxs-lookup"><span data-stu-id="d9172-115">When installing the Linux system it is *recommended* that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="d9172-116">Isso irá evitar conflitos de nome LVM com VMs clonadas, especialmente se um disco do sistema operacional precisar ser anexado a outra VM idêntica para solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="d9172-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another identical VM for troubleshooting.</span></span> <span data-ttu-id="d9172-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) podem ser usados nos discos de dados.</span><span class="sxs-lookup"><span data-stu-id="d9172-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="d9172-118">É necessário suporte a kernel para montar sistemas de arquivos UDF.</span><span class="sxs-lookup"><span data-stu-id="d9172-118">Kernel support for mounting UDF file systems is required.</span></span> <span data-ttu-id="d9172-119">Na primeira inicialização no Azure, a configuração de provisionamento é transmitida à VM do Linux por meio de mídia formatada para UDF, a qual é anexada ao convidado.</span><span class="sxs-lookup"><span data-stu-id="d9172-119">At first boot on Azure the provisioning configuration is passed to the Linux VM via UDF-formatted media that is attached to the guest.</span></span> <span data-ttu-id="d9172-120">O agente de Linux do Azure deve ser capaz de montar o sistema de arquivos UDF para ler sua configuração e provisionar a VM.</span><span class="sxs-lookup"><span data-stu-id="d9172-120">The Azure Linux agent must be able to mount the UDF file system to read its configuration and provision the VM.</span></span>
* <span data-ttu-id="d9172-121">Versões de kernel do Linux abaixo de 2.6.37 não dão suporte ao NUMA no Hyper-V com tamanhos maiores de VM.</span><span class="sxs-lookup"><span data-stu-id="d9172-121">Linux kernel versions below 2.6.37 do not support NUMA on Hyper-V with larger VM sizes.</span></span> <span data-ttu-id="d9172-122">Esse problema afeta principalmente distribuições mais antigas usando kernel Red Hat 2.6.32 upstream e foi corrigido no RHEL 6.6 (kernel-2.6.32-504).</span><span class="sxs-lookup"><span data-stu-id="d9172-122">This issue primarily impacts older distributions using the upstream Red Hat 2.6.32 kernel, and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="d9172-123">Sistemas que executam kernels personalizados anteriores a 2.6.37 ou com base em RHEL anteriores a 2.6.32-504 devem definir o parâmetro de inicialização `numa=off` na linha de comando do kernel em grub.conf.</span><span class="sxs-lookup"><span data-stu-id="d9172-123">Systems running custom kernels older than 2.6.37, or RHEL-based kernels older than 2.6.32-504 must set the boot parameter `numa=off` on the kernel command-line in grub.conf.</span></span> <span data-ttu-id="d9172-124">Para obter mais informações, confira o [KB 436883](https://access.redhat.com/solutions/436883) do Red Hat.</span><span class="sxs-lookup"><span data-stu-id="d9172-124">For more information see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="d9172-125">Não configure uma partição de permuta no disco do SO.</span><span class="sxs-lookup"><span data-stu-id="d9172-125">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="d9172-126">O agente Linux pode ser configurado para criar um arquivo de permuta no disco de recursos temporários.</span><span class="sxs-lookup"><span data-stu-id="d9172-126">The Linux agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="d9172-127">Verifique as etapas a seguir para obter mais informações a esse respeito.</span><span class="sxs-lookup"><span data-stu-id="d9172-127">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="d9172-128">Todos os VHDs devem ter tamanhos que sejam múltiplos de 1 MB.</span><span class="sxs-lookup"><span data-stu-id="d9172-128">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="centos-6x"></a><span data-ttu-id="d9172-129">CentOS 6.x</span><span class="sxs-lookup"><span data-stu-id="d9172-129">CentOS 6.x</span></span>

1. <span data-ttu-id="d9172-130">No Gerenciador do Hyper-V, selecione a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d9172-130">In Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="d9172-131">Clique em **Conectar** para abrir a janela do console para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d9172-131">Click **Connect** to open a console window for the virtual machine.</span></span>

3. <span data-ttu-id="d9172-132">No CentOS 6, NetworkManager pode interferir com o agente Linux do Azure.</span><span class="sxs-lookup"><span data-stu-id="d9172-132">In CentOS 6, NetworkManager can interfere with the Azure Linux agent.</span></span> <span data-ttu-id="d9172-133">Desinstale este pacote ao executar o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="d9172-133">Uninstall this package by running the following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

4. <span data-ttu-id="d9172-134">Crie ou edite o arquivo `/etc/sysconfig/network` e adicione o texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="d9172-134">Create or edit the file `/etc/sysconfig/network` and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="d9172-135">Crie ou edite o arquivo `/etc/sysconfig/network-scripts/ifcfg-eth0` e adicione o texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="d9172-135">Create or edit the file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="d9172-136">Modifique as regras de udev para evitar a geração de regras estáticas das interfaces Ethernet.</span><span class="sxs-lookup"><span data-stu-id="d9172-136">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span></span> <span data-ttu-id="d9172-137">Essas regras podem provocar problemas ao clonar uma máquina virtual no Microsoft Azure ou no Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="d9172-137">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="d9172-138">Certifique-se de que o serviço de rede será iniciado na inicialização executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="d9172-138">Ensure the network service will start at boot time by running the following command:</span></span>
   
        # sudo chkconfig network on

8. <span data-ttu-id="d9172-139">Se quiser usar os espelhos OpenLogic hospedados em datacenters do Azure, substitua o arquivo `/etc/yum.repos.d/CentOS-Base.repo` pelos repositórios a seguir.</span><span class="sxs-lookup"><span data-stu-id="d9172-139">If you would like to use the OpenLogic mirrors that are hosted within the Azure datacenters, then replace the `/etc/yum.repos.d/CentOS-Base.repo` file with the following repositories.</span></span>  <span data-ttu-id="d9172-140">Isso também adicionará o repositório **[openlogic]**, que inclui pacotes adicionais como o agente Linux do Azure:</span><span class="sxs-lookup"><span data-stu-id="d9172-140">This will also add the **[openlogic]** repository that includes additional packages such as the Azure Linux agent:</span></span>

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
    <span data-ttu-id="d9172-141">O restante deste guia parte do pressuposto de que você esteja usando, no mínimo, o repositório `[openlogic]`, que será usado para instalar o agente Linux do Azure abaixo.</span><span class="sxs-lookup"><span data-stu-id="d9172-141">The rest of this guide will assume you are using at least the `[openlogic]` repo, which will be used to install the Azure Linux agent below.</span></span>


9. <span data-ttu-id="d9172-142">Adicione a seguinte linha a /etc/yum.conf:</span><span class="sxs-lookup"><span data-stu-id="d9172-142">Add the following line to /etc/yum.conf:</span></span>
    
        http_caching=packages

10. <span data-ttu-id="d9172-143">Execute o seguinte comando para limpar os metadados atuais do yum e atualizar o sistema com os pacotes mais recentes:</span><span class="sxs-lookup"><span data-stu-id="d9172-143">Run the following command to clear the current yum metadata and update the system with the latest packages:</span></span>
    
        # yum clean all

    <span data-ttu-id="d9172-144">A menos que você esteja criando uma imagem para uma versão anterior do CentOS, é recomendável atualizar todos os pacotes para a versão mais recente:</span><span class="sxs-lookup"><span data-stu-id="d9172-144">Unless you are creating an image for an older version of CentOS, it is recommended to update all the packages to the latest:</span></span>

        # sudo yum -y update

    <span data-ttu-id="d9172-145">Pode ser necessária uma reinicialização depois de executar esse comando.</span><span class="sxs-lookup"><span data-stu-id="d9172-145">A reboot may be required after running this command.</span></span>

11. <span data-ttu-id="d9172-146">(Opcional) Instale os drivers dos LIS (Serviços de Integração do Linux).</span><span class="sxs-lookup"><span data-stu-id="d9172-146">(Optional) Install the drivers for the Linux Integration Services (LIS).</span></span>
   
    >[!IMPORTANT]
    <span data-ttu-id="d9172-147">A etapa é **necessária** para CentOS 6.3 e anteriores e opcionais para versões posteriores.</span><span class="sxs-lookup"><span data-stu-id="d9172-147">The step is **required** for CentOS 6.3 and earlier, and optional for later releases.</span></span>

        # sudo rpm -e hypervkvpd  ## (may return error if not installed, that's OK)
        # sudo yum install microsoft-hyper-v

    <span data-ttu-id="d9172-148">Como alternativa, você pode seguir as instruções de instalação manual [página de download do LIS](https://go.microsoft.com/fwlink/?linkid=403033) para instalar o RPM para sua VM.</span><span class="sxs-lookup"><span data-stu-id="d9172-148">Alternatively, you can follow the manual installation instructions on the [LIS download page](https://go.microsoft.com/fwlink/?linkid=403033) to install the RPM onto your VM.</span></span>
 
12. <span data-ttu-id="d9172-149">Instale o agente Linux do Azure e as dependências:</span><span class="sxs-lookup"><span data-stu-id="d9172-149">Install the Azure Linux Agent and dependencies:</span></span>
    
        # sudo yum install python-pyasn1 WALinuxAgent
    
    <span data-ttu-id="d9172-150">A instalação do pacote WALinuxAgent removerá o NetworkManager e os pacotes NetworkManager-gnome se eles já não tiverem sido removidos conforme descrito na etapa 3.</span><span class="sxs-lookup"><span data-stu-id="d9172-150">The WALinuxAgent package will remove the NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 3.</span></span>


13. <span data-ttu-id="d9172-151">Modifique a linha de inicialização do kernel em sua configuração de grub para incluir parâmetros adicionais de kernel para o Azure.</span><span class="sxs-lookup"><span data-stu-id="d9172-151">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="d9172-152">Para fazer isso, abra `/boot/grub/menu.lst` em um editor de texto e verifique se o kernel padrão inclui os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="d9172-152">To do this, open `/boot/grub/menu.lst` in a text editor and ensure that the default kernel includes the following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="d9172-153">Isso garantirá que todas as mensagens do console sejam enviadas para a primeira porta serial, que pode auxiliar o suporte do Azure com problemas de depuração.</span><span class="sxs-lookup"><span data-stu-id="d9172-153">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="d9172-154">Além disso, recomendamos que você *remova* os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="d9172-154">In addition to the above, it is recommended to *remove* the following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="d9172-155">As inicializações gráfica e silenciosa não são úteis em ambientes de rede, quando queremos que todos os logs sejam enviados para a porta serial.</span><span class="sxs-lookup"><span data-stu-id="d9172-155">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span>  <span data-ttu-id="d9172-156">Você pode deixar configurada a opção `crashkernel` , mas esse parâmetro reduz a memória disponível na máquina virtual em 128 MB ou mais, o que pode ser um problema em máquinas virtuais menores.</span><span class="sxs-lookup"><span data-stu-id="d9172-156">The `crashkernel` option may be left configured if desired, but note that this parameter will reduce the amount of available memory in the VM by 128MB or more, which may be problematic on the smaller VM sizes.</span></span>

    >[!Important]
    <span data-ttu-id="d9172-157">CentOS 6.5 e anteriores também devem definir o parâmetro de kernel `numa=off`.</span><span class="sxs-lookup"><span data-stu-id="d9172-157">CentOS 6.5 and earlier must also set the kernel parameter `numa=off`.</span></span> <span data-ttu-id="d9172-158">Consulte Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="d9172-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

14. <span data-ttu-id="d9172-159">Confira se o servidor SSH está instalado e configurado para iniciar no tempo de inicialização.</span><span class="sxs-lookup"><span data-stu-id="d9172-159">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="d9172-160">Geralmente, esse é o padrão.</span><span class="sxs-lookup"><span data-stu-id="d9172-160">This is usually the default.</span></span>

15. <span data-ttu-id="d9172-161">Não crie espaço de permuta no disco do SO.</span><span class="sxs-lookup"><span data-stu-id="d9172-161">Do not create swap space on the OS disk.</span></span>
    
    <span data-ttu-id="d9172-162">O Agente Linux do Azure pode configurar automaticamente o espaço de permuta usando o disco de recurso local que é anexado à VM após o provisionamento no Azure.</span><span class="sxs-lookup"><span data-stu-id="d9172-162">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="d9172-163">Observe que o disco de recurso local é um disco *temporário* e pode ser esvaziado quando a VM é desprovisionada.</span><span class="sxs-lookup"><span data-stu-id="d9172-163">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="d9172-164">Depois de instalar o Agente Linux do Azure (confira a etapa anterior), modifique adequadamente os seguintes parâmetros em `/etc/waagent.conf` :</span><span class="sxs-lookup"><span data-stu-id="d9172-164">After installing the Azure Linux Agent (see previous step), modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

16. <span data-ttu-id="d9172-165">Execute os comandos a seguir para desprovisionar a máquina virtual e prepará-la para provisionamento no Azure:</span><span class="sxs-lookup"><span data-stu-id="d9172-165">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

17. <span data-ttu-id="d9172-166">Clique em **Ação -> Desligar** no Gerenciador do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="d9172-166">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="d9172-167">Agora, seu VHD Linux está pronto para ser carregado no Azure.</span><span class="sxs-lookup"><span data-stu-id="d9172-167">Your Linux VHD is now ready to be uploaded to Azure.</span></span>


- - -
## <a name="centos-70"></a><span data-ttu-id="d9172-168">CentOS 7.0+</span><span class="sxs-lookup"><span data-stu-id="d9172-168">CentOS 7.0+</span></span>
<span data-ttu-id="d9172-169">**Alterações no CentOS 7 (e em derivativos similares)**</span><span class="sxs-lookup"><span data-stu-id="d9172-169">**Changes in CentOS 7 (and similar derivatives)**</span></span>

<span data-ttu-id="d9172-170">A preparação de uma máquina virtual CentOS 7 para o Azure é muito parecida com a preparação das máquinas virtuais CentOS 6, mas há diversas diferenças que merecem atenção:</span><span class="sxs-lookup"><span data-stu-id="d9172-170">Preparing a CentOS 7 virtual machine for Azure is very similar to CentOS 6, however there are several important differences worth noting:</span></span>

* <span data-ttu-id="d9172-171">O pacote do NetworkManager não entra mais em conflito com o agente Linux do Azure.</span><span class="sxs-lookup"><span data-stu-id="d9172-171">The NetworkManager package no longer conflicts with the Azure Linux agent.</span></span> <span data-ttu-id="d9172-172">Esse pacote é instalado por padrão e recomendamos que você não o remova.</span><span class="sxs-lookup"><span data-stu-id="d9172-172">This package is installed by default and we recommend that it is not removed.</span></span>
* <span data-ttu-id="d9172-173">O GRUB2 agora é usado como carregador de inicialização padrão. Com isso, o procedimento de edição de parâmetros do kernel mudou (confira abaixo).</span><span class="sxs-lookup"><span data-stu-id="d9172-173">GRUB2 is now used as the default bootloader, so the procedure for editing kernel parameters has changed (see below).</span></span>
* <span data-ttu-id="d9172-174">O XFS agora é o sistema de arquivos padrão.</span><span class="sxs-lookup"><span data-stu-id="d9172-174">XFS is now the default file system.</span></span> <span data-ttu-id="d9172-175">Ainda é possível usar o sistema de arquivos ext4 se você preferir.</span><span class="sxs-lookup"><span data-stu-id="d9172-175">The ext4 file system can still be used if desired.</span></span>

<span data-ttu-id="d9172-176">**Etapas da configuração**</span><span class="sxs-lookup"><span data-stu-id="d9172-176">**Configuration Steps**</span></span>

1. <span data-ttu-id="d9172-177">No Gerenciador do Hyper-V, selecione a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d9172-177">In Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="d9172-178">Clique em **Conectar** para abrir a janela do console para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d9172-178">Click **Connect** to open a console window for the virtual machine.</span></span>

3. <span data-ttu-id="d9172-179">Crie ou edite o arquivo `/etc/sysconfig/network` e adicione o texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="d9172-179">Create or edit the file `/etc/sysconfig/network` and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. <span data-ttu-id="d9172-180">Crie ou edite o arquivo `/etc/sysconfig/network-scripts/ifcfg-eth0` e adicione o texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="d9172-180">Create or edit the file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. <span data-ttu-id="d9172-181">Modifique as regras de udev para evitar a geração de regras estáticas das interfaces Ethernet.</span><span class="sxs-lookup"><span data-stu-id="d9172-181">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span></span> <span data-ttu-id="d9172-182">Essas regras podem provocar problemas ao clonar uma máquina virtual no Microsoft Azure ou no Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="d9172-182">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

6. <span data-ttu-id="d9172-183">Se quiser usar os espelhos OpenLogic hospedados em datacenters do Azure, substitua o arquivo `/etc/yum.repos.d/CentOS-Base.repo` pelos repositórios a seguir.</span><span class="sxs-lookup"><span data-stu-id="d9172-183">If you would like to use the OpenLogic mirrors that are hosted within the Azure datacenters, then replace the `/etc/yum.repos.d/CentOS-Base.repo` file with the following repositories.</span></span>  <span data-ttu-id="d9172-184">Essa ação adiciona o repositório **[openlogic]** que inclui pacotes para o agente Linux do Azure:</span><span class="sxs-lookup"><span data-stu-id="d9172-184">This will also add the **[openlogic]** repository that includes packages for the Azure Linux agent:</span></span>
   
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
    <span data-ttu-id="d9172-185">O restante deste guia parte do pressuposto de que você esteja usando, no mínimo, o repositório `[openlogic]`, que será usado para instalar o agente Linux do Azure abaixo.</span><span class="sxs-lookup"><span data-stu-id="d9172-185">The rest of this guide will assume you are using at least the `[openlogic]` repo, which will be used to install the Azure Linux agent below.</span></span>

7. <span data-ttu-id="d9172-186">Execute o comando a seguir para limpar os metadados atuais do yum e instalar atualizações:</span><span class="sxs-lookup"><span data-stu-id="d9172-186">Run the following command to clear the current yum metadata and install any updates:</span></span>
   
        # sudo yum clean all

    <span data-ttu-id="d9172-187">A menos que você esteja criando uma imagem para uma versão anterior do CentOS, é recomendável atualizar todos os pacotes para a versão mais recente:</span><span class="sxs-lookup"><span data-stu-id="d9172-187">Unless you are creating an image for an older version of CentOS, it is recommended to update all the packages to the latest:</span></span>

        # sudo yum -y update

    <span data-ttu-id="d9172-188">Uma reinicialização necessária talvez depois de executar esse comando.</span><span class="sxs-lookup"><span data-stu-id="d9172-188">A reboot maybe required after running this command.</span></span>

8. <span data-ttu-id="d9172-189">Modifique a linha de inicialização do kernel em sua configuração de grub para incluir parâmetros adicionais de kernel para o Azure.</span><span class="sxs-lookup"><span data-stu-id="d9172-189">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="d9172-190">Para fazer isso, abra `/etc/default/grub` em um editor de texto e edite o parâmetro `GRUB_CMDLINE_LINUX`, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="d9172-190">To do this, open `/etc/default/grub` in a text editor and edit the `GRUB_CMDLINE_LINUX` parameter, for example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="d9172-191">Isso garantirá que todas as mensagens do console sejam enviadas para a primeira porta serial, que pode auxiliar o suporte do Azure com problemas de depuração.</span><span class="sxs-lookup"><span data-stu-id="d9172-191">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="d9172-192">Ele também desativa novas convenções de nomenclatura do CentOS 7 para NICs.</span><span class="sxs-lookup"><span data-stu-id="d9172-192">It also turns off the new CentOS 7 naming conventions for NICs.</span></span> <span data-ttu-id="d9172-193">Além disso, recomendamos que você *remova* os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="d9172-193">In addition to the above, it is recommended to *remove* the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="d9172-194">As inicializações gráfica e silenciosa não são úteis em ambientes de rede, quando queremos que todos os logs sejam enviados para a porta serial.</span><span class="sxs-lookup"><span data-stu-id="d9172-194">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="d9172-195">Você pode deixar configurada a opção `crashkernel` , mas esse parâmetro reduz a memória disponível na máquina virtual em 128 MB ou mais, o que pode ser um problema em máquinas virtuais menores.</span><span class="sxs-lookup"><span data-stu-id="d9172-195">The `crashkernel` option may be left configured if desired, but note that this parameter will reduce the amount of available memory in the VM by 128MB or more, which may be problematic on the smaller VM sizes.</span></span>

9. <span data-ttu-id="d9172-196">Depois de editar `/etc/default/grub` como mostrado acima, execute o comando a seguir para recompilar a configuração do grub:</span><span class="sxs-lookup"><span data-stu-id="d9172-196">Once you are done editing `/etc/default/grub` per above, run the following command to rebuild the grub configuration:</span></span>
   
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

10. <span data-ttu-id="d9172-197">Se a criação da imagem de **VMWare, VirtualBox ou KVM:** Verifique se o Hyper-V drivers estão incluídos no initramfs:</span><span class="sxs-lookup"><span data-stu-id="d9172-197">If building the image from **VMWare, VirtualBox or KVM:** Ensure the Hyper-V drivers are included in the initramfs:</span></span>
   
   <span data-ttu-id="d9172-198">Edite `/etc/dracut.conf`e adicione o conteúdo:</span><span class="sxs-lookup"><span data-stu-id="d9172-198">Edit `/etc/dracut.conf`, add content:</span></span>
   
        add_drivers+=”hv_vmbus hv_netvsc hv_storvsc”
   
   <span data-ttu-id="d9172-199">Recompile o initramfs:</span><span class="sxs-lookup"><span data-stu-id="d9172-199">Rebuild the initramfs:</span></span>
   
        # sudo dracut –f -v

11. <span data-ttu-id="d9172-200">Instale o agente Linux do Azure e as dependências:</span><span class="sxs-lookup"><span data-stu-id="d9172-200">Install the Azure Linux Agent and dependencies:</span></span>

        # sudo yum install python-pyasn1 WALinuxAgent
        # sudo systemctl enable waagent

12. <span data-ttu-id="d9172-201">Não crie espaço de permuta no disco do SO.</span><span class="sxs-lookup"><span data-stu-id="d9172-201">Do not create swap space on the OS disk.</span></span>
   
   <span data-ttu-id="d9172-202">O Agente Linux do Azure pode configurar automaticamente o espaço de permuta usando o disco de recurso local que é anexado à VM após o provisionamento no Azure.</span><span class="sxs-lookup"><span data-stu-id="d9172-202">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="d9172-203">Observe que o disco de recurso local é um disco *temporário* e pode ser esvaziado quando a VM é desprovisionada.</span><span class="sxs-lookup"><span data-stu-id="d9172-203">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="d9172-204">Depois de instalar o Agente Linux do Azure (confira a etapa anterior), modifique adequadamente os seguintes parâmetros em `/etc/waagent.conf` :</span><span class="sxs-lookup"><span data-stu-id="d9172-204">After installing the Azure Linux Agent (see previous step), modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>
   
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

13. <span data-ttu-id="d9172-205">Execute os comandos a seguir para desprovisionar a máquina virtual e prepará-la para provisionamento no Azure:</span><span class="sxs-lookup"><span data-stu-id="d9172-205">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

14. <span data-ttu-id="d9172-206">Clique em **Ação -> Desligar** no Gerenciador do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="d9172-206">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="d9172-207">Agora, seu VHD Linux está pronto para ser carregado no Azure.</span><span class="sxs-lookup"><span data-stu-id="d9172-207">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9172-208">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d9172-208">Next steps</span></span>
<span data-ttu-id="d9172-209">Agora, você está pronto para usar o disco rígido virtual CentOS Linux para criar novas máquinas virtuais no Azure.</span><span class="sxs-lookup"><span data-stu-id="d9172-209">You're now ready to use your CentOS Linux virtual hard disk to create new virtual machines in Azure.</span></span> <span data-ttu-id="d9172-210">Se esta for a primeira vez que você estiver carregando o arquivo .vhd para o Azure, veja as etapas 2 e 3 em [Criando e carregando um disco rígido virtual que contém o sistema operacional Linux](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d9172-210">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

