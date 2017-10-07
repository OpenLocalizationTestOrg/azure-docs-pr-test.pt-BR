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
# <a name="prepare-a-sles-or-opensuse-virtual-machine-for-azure"></a><span data-ttu-id="85030-103">Preparar uma máquina virtual do SLES ou openSUSE para o Azure</span><span class="sxs-lookup"><span data-stu-id="85030-103">Prepare a SLES or openSUSE virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="85030-104">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="85030-104">Prerequisites</span></span>
<span data-ttu-id="85030-105">Este artigo pressupõe que você já instalou um SUSE ou openSUSE Linux tooa rígido disco do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="85030-105">This article assumes that you have already installed a SUSE or openSUSE Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="85030-106">Várias ferramentas existem toocreate arquivos. vhd, por exemplo, uma solução de virtualização como o Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="85030-106">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="85030-107">Para obter instruções, consulte [instalar Olá função Hyper-V e configurar uma máquina Virtual](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="85030-107">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="sles--opensuse-installation-notes"></a><span data-ttu-id="85030-108">Notas de instalação do SLES / openSUSE</span><span class="sxs-lookup"><span data-stu-id="85030-108">SLES / openSUSE installation notes</span></span>
* <span data-ttu-id="85030-109">Veja também as [Notas de instalação gerais do Linux](create-upload-generic.md#general-linux-installation-notes) para obter mais dicas sobre como preparar o Linux para o Azure.</span><span class="sxs-lookup"><span data-stu-id="85030-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="85030-110">formato do Hello VHDX não tem suporte apenas no Azure, **VHD fixo**.</span><span class="sxs-lookup"><span data-stu-id="85030-110">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="85030-111">Você pode converter Olá disco tooVHD formato usando o Gerenciador do Hyper-V ou Olá cmdlet convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="85030-111">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span>
* <span data-ttu-id="85030-112">Ao instalar o sistema de Linux Olá é recomendável que você use partições padrão em vez de LVM (geralmente padrão Olá para muitas instalações).</span><span class="sxs-lookup"><span data-stu-id="85030-112">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="85030-113">Isso evitará LVM nome conflita com VMs clonados, especialmente se um sistema operacional de disco nunca precisa tooanother toobe anexado VMs para solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="85030-113">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="85030-114">Se você preferir, é possível usar [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) em discos de dados.</span><span class="sxs-lookup"><span data-stu-id="85030-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="85030-115">Não configure uma partição de troca no disco do sistema operacional hello.</span><span class="sxs-lookup"><span data-stu-id="85030-115">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="85030-116">agente do Linux Olá pode ser configurado toocreate um arquivo de permuta em disco de recursos temporário hello.</span><span class="sxs-lookup"><span data-stu-id="85030-116">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="85030-117">Para obter mais informações sobre isso podem ser encontradas nas etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="85030-117">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="85030-118">Todos os VHDs Olá devem ter tamanhos que sejam múltiplos de 1 MB.</span><span class="sxs-lookup"><span data-stu-id="85030-118">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="use-suse-studio"></a><span data-ttu-id="85030-119">Use o SUSE Studio</span><span class="sxs-lookup"><span data-stu-id="85030-119">Use SUSE Studio</span></span>
<span data-ttu-id="85030-120">[SUSE Studio](http://www.susestudio.com) pode criar e gerenciar facilmente suas imagens SLES e openSUSE no Azure e no Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="85030-120">[SUSE Studio](http://www.susestudio.com) can easily create and manage your SLES and openSUSE images for Azure and Hyper-V.</span></span> <span data-ttu-id="85030-121">Isso é hello abordagem para personalizar suas próprias imagens SLES e openSUSE recomendada.</span><span class="sxs-lookup"><span data-stu-id="85030-121">This is hello recommended approach for customizing your own SLES and openSUSE images.</span></span>

<span data-ttu-id="85030-122">Como uma alternativa toobuilding seu próprio VHD, SUSE também publica imagens BYOS (Traga sua própria assinatura) para SLES em [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007).</span><span class="sxs-lookup"><span data-stu-id="85030-122">As an alternative toobuilding your own VHD, SUSE also publishes BYOS (Bring Your Own Subscription) images for SLES at [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007).</span></span>

## <a name="prepare-suse-linux-enterprise-server-11-sp4"></a><span data-ttu-id="85030-123">Preparar o SUSE Linux Enterprise Server 11 SP4</span><span class="sxs-lookup"><span data-stu-id="85030-123">Prepare SUSE Linux Enterprise Server 11 SP4</span></span>
1. <span data-ttu-id="85030-124">No painel central de saudação do Gerenciador do Hyper-V, selecione máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="85030-124">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="85030-125">Clique em **conectar** tooopen janela de saudação para a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="85030-125">Click **Connect** tooopen hello window for hello virtual machine.</span></span>
3. <span data-ttu-id="85030-126">Registrar seu tooallow de sistema do SUSE Linux Enterprise-toodownload atualizações e pacotes de instalação.</span><span class="sxs-lookup"><span data-stu-id="85030-126">Register your SUSE Linux Enterprise system tooallow it toodownload updates and install packages.</span></span>
4. <span data-ttu-id="85030-127">Atualize o sistema de saudação com os patches mais recentes hello:</span><span class="sxs-lookup"><span data-stu-id="85030-127">Update hello system with hello latest patches:</span></span>
   
        # sudo zypper update
5. <span data-ttu-id="85030-128">Instale hello Azure Linux Agent do repositório SLES hello:</span><span class="sxs-lookup"><span data-stu-id="85030-128">Install hello Azure Linux Agent from hello SLES repository:</span></span>
   
        # sudo zypper install WALinuxAgent
6. <span data-ttu-id="85030-129">Verifique se waagent está definido muito "no" comando chkconfig e se não, habilitá-la para iniciar automaticamente:</span><span class="sxs-lookup"><span data-stu-id="85030-129">Check if waagent is set too"on" in chkconfig, and if not, enable it for autostart:</span></span>
   
        # sudo chkconfig waagent on
7. <span data-ttu-id="85030-130">Verifique se o serviço de waagent está sendo executado e se não, inicie-o:</span><span class="sxs-lookup"><span data-stu-id="85030-130">Check if waagent service is running, and if not, start it:</span></span> 
   
        # sudo service waagent start
8. <span data-ttu-id="85030-131">Modificar a linha de inicialização de kernel de saudação em seus parâmetros de kernel adicionais tooinclude grub configuração do Azure.</span><span class="sxs-lookup"><span data-stu-id="85030-131">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="85030-132">toodo nesse abra "/ boot/grub/menu.lst" em um editor de texto e certifique-se de que kernel de padrão de saudação inclui Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="85030-132">toodo this open "/boot/grub/menu.lst" in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
   
    <span data-ttu-id="85030-133">Isso garantirá que todas as mensagens de console são enviadas toohello primeira porta serial, que pode ajudá-lo Azure suporte à depuração de problemas.</span><span class="sxs-lookup"><span data-stu-id="85030-133">This will ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
9. <span data-ttu-id="85030-134">Confirme que fstab /boot/grub/menu.lst e/etc/ambos os disco de saudação de referência usando sua UUID (por uuid) em vez de ID do disco hello (por id).</span><span class="sxs-lookup"><span data-stu-id="85030-134">Confirm that /boot/grub/menu.lst and /etc/fstab both reference hello disk using its UUID (by-uuid) instead of hello disk ID (by-id).</span></span> 
   
    <span data-ttu-id="85030-135">Obter o UUID do disco</span><span class="sxs-lookup"><span data-stu-id="85030-135">Get disk UUID</span></span>
   
        # ls /dev/disk/by-uuid/
   
    <span data-ttu-id="85030-136">Se /dev/disk/by-id é usado, atualizar fstab /boot/grub/menu.lst e/etc/com o valor de adequado por uuid de saudação</span><span class="sxs-lookup"><span data-stu-id="85030-136">If /dev/disk/by-id/ is used, update both /boot/grub/menu.lst and /etc/fstab with hello proper by-uuid value</span></span>
   
    <span data-ttu-id="85030-137">Antes da alteração</span><span class="sxs-lookup"><span data-stu-id="85030-137">Before change</span></span>
   
        root=/dev/disk/by-id/SCSI-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxxx-part1
   
    <span data-ttu-id="85030-138">Depois da alteração</span><span class="sxs-lookup"><span data-stu-id="85030-138">After change</span></span>
   
        root=/dev/disk/by-uuid/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
10. <span data-ttu-id="85030-139">Modificar udev regras tooavoid gerar regras estáticas para Olá interfaces Ethernet.</span><span class="sxs-lookup"><span data-stu-id="85030-139">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="85030-140">Essas regras podem provocar problemas ao clonar uma máquina virtual no Microsoft Azure ou no Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="85030-140">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
    
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
11. <span data-ttu-id="85030-141">É recomendável tooedit arquivo de hello "/ etc/sysconfig/rede/dhcp" e alterar Olá `DHCLIENT_SET_HOSTNAME` a seguir toohello parâmetro:</span><span class="sxs-lookup"><span data-stu-id="85030-141">It is recommended tooedit hello file "/etc/sysconfig/network/dhcp" and change hello `DHCLIENT_SET_HOSTNAME` parameter toohello following:</span></span>
    
     <span data-ttu-id="85030-142">DHCLIENT_SET_HOSTNAME="no"</span><span class="sxs-lookup"><span data-stu-id="85030-142">DHCLIENT_SET_HOSTNAME="no"</span></span>
12. <span data-ttu-id="85030-143">Em "/ etc/sudoers", comente ou remova Olá linhas a seguir se eles existirem:</span><span class="sxs-lookup"><span data-stu-id="85030-143">In "/etc/sudoers", comment out or remove hello following lines if they exist:</span></span>
    
     <span data-ttu-id="85030-144">Padrões targetpw # solicitará a senha de saudação do usuário de destino Olá raiz ou seja, todos os ALL=(ALL) todos # aviso!</span><span class="sxs-lookup"><span data-stu-id="85030-144">Defaults targetpw   # ask for hello password of hello target user i.e. root ALL    ALL=(ALL) ALL   # WARNING!</span></span> <span data-ttu-id="85030-145">Deve ser usado somente em conjunto com 'Defaults targetpw'!</span><span class="sxs-lookup"><span data-stu-id="85030-145">Only use this together with 'Defaults targetpw'!</span></span>
13. <span data-ttu-id="85030-146">Certifique-se de servidor SSH hello está instalado e configurado toostart no momento da inicialização.</span><span class="sxs-lookup"><span data-stu-id="85030-146">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="85030-147">Geralmente, esse é o padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="85030-147">This is usually hello default.</span></span>
14. <span data-ttu-id="85030-148">Não crie espaço de permuta em disco do sistema operacional hello.</span><span class="sxs-lookup"><span data-stu-id="85030-148">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="85030-149">Olá agente Linux do Azure pode configurar automaticamente o espaço de permuta usando Olá disco de recurso local que é anexado toohello VM após a configuração no Azure.</span><span class="sxs-lookup"><span data-stu-id="85030-149">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="85030-150">Observe que esse disco de recurso local Olá é um *temporário* disco e pode ser esvaziada quando Olá VM for desprovisionada.</span><span class="sxs-lookup"><span data-stu-id="85030-150">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="85030-151">Depois de instalar o hello agente Linux do Azure (consulte a etapa anterior), modifique Olá seguintes parâmetros em /etc/waagent.conf adequadamente:</span><span class="sxs-lookup"><span data-stu-id="85030-151">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
     <span data-ttu-id="85030-152">ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048; # nota: Defina esse toowhatever precisar toobe.</span><span class="sxs-lookup"><span data-stu-id="85030-152">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.</span></span>
15. <span data-ttu-id="85030-153">Execute Olá seguindo a máquina virtual do comandos toodeprovision hello e prepará-la para provisionamento no Azure:</span><span class="sxs-lookup"><span data-stu-id="85030-153">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
    # <a name="sudo-waagent--force--deprovision"></a><span data-ttu-id="85030-154">sudo waagent -force -deprovision</span><span class="sxs-lookup"><span data-stu-id="85030-154">sudo waagent -force -deprovision</span></span>
    # <a name="export-histsize0"></a><span data-ttu-id="85030-155">export HISTSIZE=0</span><span class="sxs-lookup"><span data-stu-id="85030-155">export HISTSIZE=0</span></span>
    # <a name="logout"></a><span data-ttu-id="85030-156">logout</span><span class="sxs-lookup"><span data-stu-id="85030-156">logout</span></span>
16. <span data-ttu-id="85030-157">Clique em **Ação -> Desligar** no Gerenciador do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="85030-157">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="85030-158">O VHD Linux está agora pronto toobe carregado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="85030-158">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

- - -
## <a name="prepare-opensuse-131"></a><span data-ttu-id="85030-159">Preparar o openSUSE 13.1+</span><span class="sxs-lookup"><span data-stu-id="85030-159">Prepare openSUSE 13.1+</span></span>
1. <span data-ttu-id="85030-160">No painel central de saudação do Gerenciador do Hyper-V, selecione máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="85030-160">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="85030-161">Clique em **conectar** tooopen janela de saudação para a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="85030-161">Click **Connect** tooopen hello window for hello virtual machine.</span></span>
3. <span data-ttu-id="85030-162">Shell do hello, execute o comando de saudação '`zypper lr`'.</span><span class="sxs-lookup"><span data-stu-id="85030-162">On hello shell, run hello command '`zypper lr`'.</span></span> <span data-ttu-id="85030-163">Se esse comando retorna saída toohello semelhante a seguir, repositórios de saudação serão configurado conforme o esperado – sem ajustes são necessárias (Observe que os números de versão podem variar):</span><span class="sxs-lookup"><span data-stu-id="85030-163">If this command returns output similar toohello following, then hello repositories are configured as expected--no adjustments are necessary (note that version numbers may vary):</span></span>
   
        # | Alias                 | Name                  | Enabled | Refresh
        --+-----------------------+-----------------------+---------+--------
        1 | Cloud:Tools_13.1      | Cloud:Tools_13.1      | Yes     | Yes
        2 | openSUSE_13.1_OSS     | openSUSE_13.1_OSS     | Yes     | Yes
        3 | openSUSE_13.1_Updates | openSUSE_13.1_Updates | Yes     | Yes
   
    <span data-ttu-id="85030-164">Se o comando Olá não retorna "Nenhum repositório definido...", em seguida, use Olá tooadd comandos a seguir esses repositórios:</span><span class="sxs-lookup"><span data-stu-id="85030-164">If hello command returns "No repositories defined..." then use hello following commands tooadd these repos:</span></span>
   
        # sudo zypper ar -f http://download.opensuse.org/repositories/Cloud:Tools/openSUSE_13.1 Cloud:Tools_13.1
        # sudo zypper ar -f http://download.opensuse.org/distribution/13.1/repo/oss openSUSE_13.1_OSS
        # sudo zypper ar -f http://download.opensuse.org/update/13.1 openSUSE_13.1_Updates
   
    <span data-ttu-id="85030-165">Em seguida, você pode verificar a repositórios de saudação foram adicionados ao executar o comando de saudação '`zypper lr`' novamente.</span><span class="sxs-lookup"><span data-stu-id="85030-165">You can then verify hello repositories have been added by running hello command '`zypper lr`' again.</span></span> <span data-ttu-id="85030-166">No caso de um dos repositórios de atualização relevante Olá não estiver habilitado, habilite-o com o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="85030-166">In case one of hello relevant update repositories is not enabled, enable it with following command:</span></span>
   
        # sudo zypper mr -e [NUMBER OF REPOSITORY]
4. <span data-ttu-id="85030-167">Atualize Olá kernel toohello versão mais recente disponível:</span><span class="sxs-lookup"><span data-stu-id="85030-167">Update hello kernel toohello latest available version:</span></span>
   
        # sudo zypper up kernel-default
   
    <span data-ttu-id="85030-168">Sistema de saudação tooupdate com todos os patches mais recentes de saudação ou:</span><span class="sxs-lookup"><span data-stu-id="85030-168">Or tooupdate hello system with all hello latest patches:</span></span>
   
        # sudo zypper update
5. <span data-ttu-id="85030-169">Instale Olá agente Linux do Azure.</span><span class="sxs-lookup"><span data-stu-id="85030-169">Install hello Azure Linux Agent.</span></span>
   
   # <a name="sudo-zypper-install-walinuxagent"></a><span data-ttu-id="85030-170">sudo zypper install WALinuxAgent</span><span class="sxs-lookup"><span data-stu-id="85030-170">sudo zypper install WALinuxAgent</span></span>
6. <span data-ttu-id="85030-171">Modificar a linha de inicialização de kernel de saudação em seus parâmetros de kernel adicionais tooinclude grub configuração do Azure.</span><span class="sxs-lookup"><span data-stu-id="85030-171">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="85030-172">toodo isso, abra "/ boot/grub/menu.lst" em um editor de texto e certifique-se de que kernel de padrão de saudação inclui Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="85030-172">toodo this, open "/boot/grub/menu.lst" in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
   
     <span data-ttu-id="85030-173">console=ttyS0 earlyprintk=ttyS0 rootdelay=300</span><span class="sxs-lookup"><span data-stu-id="85030-173">console=ttyS0 earlyprintk=ttyS0 rootdelay=300</span></span>
   
   <span data-ttu-id="85030-174">Isso garantirá que todas as mensagens de console são enviadas toohello primeira porta serial, que pode ajudá-lo Azure suporte à depuração de problemas.</span><span class="sxs-lookup"><span data-stu-id="85030-174">This will ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="85030-175">Além disso, remova Olá seguir parâmetros de linha de inicialização do kernel Olá se existirem:</span><span class="sxs-lookup"><span data-stu-id="85030-175">In addition, remove hello following parameters from hello kernel boot line if they exist:</span></span>
   
     <span data-ttu-id="85030-176">libata.atapi_enabled=0 reserve=0x1f0,0x8</span><span class="sxs-lookup"><span data-stu-id="85030-176">libata.atapi_enabled=0 reserve=0x1f0,0x8</span></span>
7. <span data-ttu-id="85030-177">É recomendável tooedit arquivo de hello "/ etc/sysconfig/rede/dhcp" e alterar Olá `DHCLIENT_SET_HOSTNAME` a seguir toohello parâmetro:</span><span class="sxs-lookup"><span data-stu-id="85030-177">It is recommended tooedit hello file "/etc/sysconfig/network/dhcp" and change hello `DHCLIENT_SET_HOSTNAME` parameter toohello following:</span></span>
   
     <span data-ttu-id="85030-178">DHCLIENT_SET_HOSTNAME="no"</span><span class="sxs-lookup"><span data-stu-id="85030-178">DHCLIENT_SET_HOSTNAME="no"</span></span>
8. <span data-ttu-id="85030-179">**Importante:** em "/ etc/sudoers", comentar ou remover Olá linhas a seguir se eles existirem:</span><span class="sxs-lookup"><span data-stu-id="85030-179">**Important:** In "/etc/sudoers", comment out or remove hello following lines if they exist:</span></span>
   
     <span data-ttu-id="85030-180">Padrões targetpw # solicitará a senha de saudação do usuário de destino Olá raiz ou seja, todos os ALL=(ALL) todos # aviso!</span><span class="sxs-lookup"><span data-stu-id="85030-180">Defaults targetpw   # ask for hello password of hello target user i.e. root ALL    ALL=(ALL) ALL   # WARNING!</span></span> <span data-ttu-id="85030-181">Deve ser usado somente em conjunto com 'Defaults targetpw'!</span><span class="sxs-lookup"><span data-stu-id="85030-181">Only use this together with 'Defaults targetpw'!</span></span>
9. <span data-ttu-id="85030-182">Certifique-se de servidor SSH hello está instalado e configurado toostart no momento da inicialização.</span><span class="sxs-lookup"><span data-stu-id="85030-182">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="85030-183">Geralmente, esse é o padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="85030-183">This is usually hello default.</span></span>
10. <span data-ttu-id="85030-184">Não crie espaço de permuta em disco do sistema operacional hello.</span><span class="sxs-lookup"><span data-stu-id="85030-184">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="85030-185">Olá agente Linux do Azure pode configurar automaticamente o espaço de permuta usando Olá disco de recurso local que é anexado toohello VM após a configuração no Azure.</span><span class="sxs-lookup"><span data-stu-id="85030-185">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="85030-186">Observe que esse disco de recurso local Olá é um *temporário* disco e pode ser esvaziada quando Olá VM for desprovisionada.</span><span class="sxs-lookup"><span data-stu-id="85030-186">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="85030-187">Depois de instalar o hello agente Linux do Azure (consulte a etapa anterior), modifique Olá seguintes parâmetros em /etc/waagent.conf adequadamente:</span><span class="sxs-lookup"><span data-stu-id="85030-187">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
     <span data-ttu-id="85030-188">ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048; # nota: Defina esse toowhatever precisar toobe.</span><span class="sxs-lookup"><span data-stu-id="85030-188">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.</span></span>
11. <span data-ttu-id="85030-189">Execute Olá seguindo a máquina virtual do comandos toodeprovision hello e prepará-la para provisionamento no Azure:</span><span class="sxs-lookup"><span data-stu-id="85030-189">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
    # <a name="sudo-waagent--force--deprovision"></a><span data-ttu-id="85030-190">sudo waagent -force -deprovision</span><span class="sxs-lookup"><span data-stu-id="85030-190">sudo waagent -force -deprovision</span></span>
    # <a name="export-histsize0"></a><span data-ttu-id="85030-191">export HISTSIZE=0</span><span class="sxs-lookup"><span data-stu-id="85030-191">export HISTSIZE=0</span></span>
    # <a name="logout"></a><span data-ttu-id="85030-192">logout</span><span class="sxs-lookup"><span data-stu-id="85030-192">logout</span></span>
12. <span data-ttu-id="85030-193">Certifique-se de hello que Azure Linux Agent executa durante a inicialização:</span><span class="sxs-lookup"><span data-stu-id="85030-193">Ensure hello Azure Linux Agent runs at startup:</span></span>
    
        # sudo systemctl enable waagent.service
13. <span data-ttu-id="85030-194">Clique em **Ação -> Desligar** no Gerenciador do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="85030-194">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="85030-195">O VHD Linux está agora pronto toobe carregado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="85030-195">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="85030-196">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="85030-196">Next steps</span></span>
<span data-ttu-id="85030-197">Você está agora pronto toouse as SUSE Linux disco rígido virtual toocreate novas máquinas virtuais no Azure.</span><span class="sxs-lookup"><span data-stu-id="85030-197">You're now ready toouse your SUSE Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="85030-198">Se isso for Olá primeira vez que você está carregando tooAzure de arquivo. vhd hello, consulte as etapas 2 e 3 em [criando e carregando um disco rígido virtual que contém o sistema de operacional Linux Olá](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="85030-198">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

