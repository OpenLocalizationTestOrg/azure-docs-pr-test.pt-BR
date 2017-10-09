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
# <a name="prepare-an-oracle-linux-virtual-machine-for-azure"></a><span data-ttu-id="a341b-103">Preparar uma máquina virtual Oracle Linux para o Azure</span><span class="sxs-lookup"><span data-stu-id="a341b-103">Prepare an Oracle Linux virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="a341b-104">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a341b-104">Prerequisites</span></span>
<span data-ttu-id="a341b-105">Este artigo pressupõe que você já tiver instalado um disco rígido virtual Oracle Linux sistema operacional tooa.</span><span class="sxs-lookup"><span data-stu-id="a341b-105">This article assumes that you have already installed an Oracle Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="a341b-106">Várias ferramentas existem toocreate arquivos. vhd, por exemplo, uma solução de virtualização como o Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="a341b-106">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="a341b-107">Para obter instruções, consulte [instalar Olá função Hyper-V e configurar uma máquina Virtual](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="a341b-107">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="oracle-linux-installation-notes"></a><span data-ttu-id="a341b-108">Notas de instalação do Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="a341b-108">Oracle Linux installation notes</span></span>
* <span data-ttu-id="a341b-109">Veja também [Notas de instalação gerais do Linux](create-upload-generic.md#general-linux-installation-notes) para obter mais dicas sobre como preparar o Linux para o Azure.</span><span class="sxs-lookup"><span data-stu-id="a341b-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="a341b-110">O kernel da Oracle, compatível com Red Hat, e seu UEK3 (Unbreakable Enterprise Kernel) têm suporte no Hyper-V e no Azure.</span><span class="sxs-lookup"><span data-stu-id="a341b-110">Oracle's Red Hat compatible kernel and their UEK3 (Unbreakable Enterprise Kernel) are both supported on Hyper-V and Azure.</span></span> <span data-ttu-id="a341b-111">Para obter melhores resultados, esteja kernel mais recente do toohello tooupdate-se ao preparar o VHD do Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="a341b-111">For best results, please be sure tooupdate toohello latest kernel while preparing your Oracle Linux VHD.</span></span>
* <span data-ttu-id="a341b-112">UEK2 da Oracle não tem suporte no Hyper-V e o Azure como não inclui drivers Olá necessário.</span><span class="sxs-lookup"><span data-stu-id="a341b-112">Oracle's UEK2 is not supported on Hyper-V and Azure as it does not include hello required drivers.</span></span>
* <span data-ttu-id="a341b-113">formato do Hello VHDX não tem suporte apenas no Azure, **VHD fixo**.</span><span class="sxs-lookup"><span data-stu-id="a341b-113">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="a341b-114">Você pode converter Olá disco tooVHD formato usando o Gerenciador do Hyper-V ou Olá cmdlet convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="a341b-114">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span>
* <span data-ttu-id="a341b-115">Ao instalar o sistema de Linux Olá é recomendável que você use partições padrão em vez de LVM (geralmente padrão Olá para muitas instalações).</span><span class="sxs-lookup"><span data-stu-id="a341b-115">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="a341b-116">Isso evitará LVM nome conflita com VMs clonados, especialmente se um sistema operacional de disco nunca precisa tooanother toobe anexado VMs para solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="a341b-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="a341b-117">Se você preferir, é possível usar [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) em discos de dados.</span><span class="sxs-lookup"><span data-stu-id="a341b-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="a341b-118">Não há suporte para para tamanhos de VM maiores devido tooa bug nas versões de kernel do Linux abaixo 2.6.37.</span><span class="sxs-lookup"><span data-stu-id="a341b-118">NUMA is not supported for larger VM sizes due tooa bug in Linux kernel versions below 2.6.37.</span></span> <span data-ttu-id="a341b-119">Esse problema principalmente os impactos distribuições usando Olá vermelho upstream kernel Hat 2.6.32.</span><span class="sxs-lookup"><span data-stu-id="a341b-119">This issue primarily impacts distributions using hello upstream Red Hat 2.6.32 kernel.</span></span> <span data-ttu-id="a341b-120">Instalação manual de agente Linux do Azure de saudação (waagent) desabilitará automaticamente o na configuração de GRUB Olá para o kernel do Linux hello.</span><span class="sxs-lookup"><span data-stu-id="a341b-120">Manual installation of hello Azure Linux agent (waagent) will automatically disable NUMA in hello GRUB configuration for hello Linux kernel.</span></span> <span data-ttu-id="a341b-121">Para obter mais informações sobre isso podem ser encontradas nas etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="a341b-121">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="a341b-122">Não configure uma partição de troca no disco do sistema operacional hello.</span><span class="sxs-lookup"><span data-stu-id="a341b-122">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="a341b-123">agente do Linux Olá pode ser configurado toocreate um arquivo de permuta em disco de recursos temporário hello.</span><span class="sxs-lookup"><span data-stu-id="a341b-123">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="a341b-124">Para obter mais informações sobre isso podem ser encontradas nas etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="a341b-124">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="a341b-125">Todos os VHDs Olá devem ter tamanhos que sejam múltiplos de 1 MB.</span><span class="sxs-lookup"><span data-stu-id="a341b-125">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>
* <span data-ttu-id="a341b-126">Certifique-se de que Olá `Addons` repositório está habilitado.</span><span class="sxs-lookup"><span data-stu-id="a341b-126">Make sure that hello `Addons` repository is enabled.</span></span> <span data-ttu-id="a341b-127">Editar arquivo hello `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) ou `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux) e altere a linha hello `enabled=0` muito`enabled=1` em **[ol6_addons]** ou **[ol7_addons]** neste arquivo.</span><span class="sxs-lookup"><span data-stu-id="a341b-127">Edit hello file `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux ), and change hello line `enabled=0` too`enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span></span>

## <a name="oracle-linux-64"></a><span data-ttu-id="a341b-128">Oracle Linux 6.4+</span><span class="sxs-lookup"><span data-stu-id="a341b-128">Oracle Linux 6.4+</span></span>
<span data-ttu-id="a341b-129">Você deve concluir as etapas de configuração específico no sistema operacional Olá Olá toorun de máquina virtual no Azure.</span><span class="sxs-lookup"><span data-stu-id="a341b-129">You must complete specific configuration steps in hello operating system for hello virtual machine toorun in Azure.</span></span>

1. <span data-ttu-id="a341b-130">No painel central de saudação do Gerenciador do Hyper-V, selecione máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="a341b-130">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="a341b-131">Clique em **conectar** tooopen janela de saudação para a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="a341b-131">Click **Connect** tooopen hello window for hello virtual machine.</span></span>
3. <span data-ttu-id="a341b-132">Desinstale o Gerenciador executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="a341b-132">Uninstall NetworkManager by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager
   
    <span data-ttu-id="a341b-133">**Observação:** se o pacote de saudação já não estiver instalado, esse comando falhará com uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="a341b-133">**Note:** If hello package is not already installed, this command will fail with an error message.</span></span> <span data-ttu-id="a341b-134">Isso é esperado.</span><span class="sxs-lookup"><span data-stu-id="a341b-134">This is expected.</span></span>
4. <span data-ttu-id="a341b-135">Crie um arquivo chamado **rede** em Olá `/etc/sysconfig/` diretório que contém a saudação texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="a341b-135">Create a file named **network** in hello `/etc/sysconfig/` directory that contains hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
5. <span data-ttu-id="a341b-136">Crie um arquivo chamado **ifcfg eth0** em Olá `/etc/sysconfig/network-scripts/` diretório que contém a saudação texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="a341b-136">Create a file named **ifcfg-eth0** in hello `/etc/sysconfig/network-scripts/` directory that contains hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
6. <span data-ttu-id="a341b-137">Modificar udev regras tooavoid gerar regras estáticas para Olá interfaces Ethernet.</span><span class="sxs-lookup"><span data-stu-id="a341b-137">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="a341b-138">Essas regras podem provocar problemas ao clonar uma máquina virtual no Microsoft Azure ou no Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="a341b-138">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
7. <span data-ttu-id="a341b-139">Certifique-se de que o serviço de rede Olá será iniciado no momento da inicialização executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="a341b-139">Ensure hello network service will start at boot time by running hello following command:</span></span>
   
        # chkconfig network on
8. <span data-ttu-id="a341b-140">Instale o python pyasn1 executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="a341b-140">Install python-pyasn1 by running hello following command:</span></span>
   
        # sudo yum install python-pyasn1
9. <span data-ttu-id="a341b-141">Modificar a linha de inicialização de kernel de saudação em seus parâmetros de kernel adicionais tooinclude grub configuração do Azure.</span><span class="sxs-lookup"><span data-stu-id="a341b-141">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="a341b-142">toodo nesse abra "/ boot/grub/menu.lst" em um editor de texto e certifique-se de que kernel de padrão de saudação inclui Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="a341b-142">toodo this open "/boot/grub/menu.lst" in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300 numa=off
   
   <span data-ttu-id="a341b-143">Isso garantirá todas as mensagens de console são enviadas toohello primeira porta serial, que pode ajudá-lo Azure suporte à depuração de problemas.</span><span class="sxs-lookup"><span data-stu-id="a341b-143">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="a341b-144">Isso irá desabilitar o NUMA devido tooa bug no kernel compatível do Red Hat da Oracle.</span><span class="sxs-lookup"><span data-stu-id="a341b-144">This will disable NUMA due tooa bug in Oracle's Red Hat compatible kernel.</span></span>
   
   <span data-ttu-id="a341b-145">Além disso toohello acima, recomenda-se muito*remover* Olá seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="a341b-145">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
   <span data-ttu-id="a341b-146">Inicialização gráfica e silenciosa não são úteis em um ambiente de nuvem onde queremos que todos os toobe de logs de saudação enviada toohello de porta serial.</span><span class="sxs-lookup"><span data-stu-id="a341b-146">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>
   
   <span data-ttu-id="a341b-147">Olá `crashkernel` opção pode ser esquerda configurada, se desejado, mas observe que esse parâmetro será reduzir a quantidade de saudação de memória disponível em Olá VM em 128 MB ou mais, que pode ser problemático em tamanhos de VM menores hello.</span><span class="sxs-lookup"><span data-stu-id="a341b-147">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>
10. <span data-ttu-id="a341b-148">Certifique-se de servidor SSH hello está instalado e configurado toostart no momento da inicialização.</span><span class="sxs-lookup"><span data-stu-id="a341b-148">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="a341b-149">Geralmente, esse é o padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="a341b-149">This is usually hello default.</span></span>
11. <span data-ttu-id="a341b-150">Instale Olá agente Linux do Azure executando o comando a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="a341b-150">Install hello Azure Linux Agent by running hello following command.</span></span> <span data-ttu-id="a341b-151">versão mais recente da saudação é 2.0.15.</span><span class="sxs-lookup"><span data-stu-id="a341b-151">hello latest version is 2.0.15.</span></span>
    
        # sudo yum install WALinuxAgent
    
    <span data-ttu-id="a341b-152">Observe que instalar pacote de WALinuxAgent Olá removerá Olá Gerenciador e pacotes de Gerenciador gnome se eles já não foram removidos conforme descrito na etapa 2.</span><span class="sxs-lookup"><span data-stu-id="a341b-152">Note that installing hello WALinuxAgent package will remove hello NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 2.</span></span>
12. <span data-ttu-id="a341b-153">Não crie espaço de permuta em disco do sistema operacional hello.</span><span class="sxs-lookup"><span data-stu-id="a341b-153">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="a341b-154">Olá agente Linux do Azure pode configurar automaticamente o espaço de permuta usando Olá disco de recurso local que é anexado toohello VM após a configuração no Azure.</span><span class="sxs-lookup"><span data-stu-id="a341b-154">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="a341b-155">Observe que esse disco de recurso local Olá é um *temporário* disco e pode ser esvaziada quando Olá VM for desprovisionada.</span><span class="sxs-lookup"><span data-stu-id="a341b-155">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="a341b-156">Depois de instalar o hello agente Linux do Azure (consulte a etapa anterior), modifique Olá seguintes parâmetros em /etc/waagent.conf adequadamente:</span><span class="sxs-lookup"><span data-stu-id="a341b-156">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.
13. <span data-ttu-id="a341b-157">Execute Olá seguindo a máquina virtual do comandos toodeprovision hello e prepará-la para provisionamento no Azure:</span><span class="sxs-lookup"><span data-stu-id="a341b-157">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
14. <span data-ttu-id="a341b-158">Clique em **Ação -> Desligar** no Gerenciador do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="a341b-158">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="a341b-159">O VHD Linux está agora pronto toobe carregado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="a341b-159">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

- - -
## <a name="oracle-linux-70"></a><span data-ttu-id="a341b-160">Oracle Linux 7.0 ou posterior</span><span class="sxs-lookup"><span data-stu-id="a341b-160">Oracle Linux 7.0+</span></span>
<span data-ttu-id="a341b-161">**Alterações no Oracle Linux 7**</span><span class="sxs-lookup"><span data-stu-id="a341b-161">**Changes in Oracle Linux 7**</span></span>

<span data-ttu-id="a341b-162">Preparando uma máquina de virtual Oracle Linux 7 para o Azure é muito semelhante tooOracle Linux 6, no entanto, há várias diferenças importantes, vale a pena observar:</span><span class="sxs-lookup"><span data-stu-id="a341b-162">Preparing an Oracle Linux 7 virtual machine for Azure is very similar tooOracle Linux 6, however there are several important differences worth noting:</span></span>

* <span data-ttu-id="a341b-163">Kernel compatível do Red Hat hello e UEK3 da Oracle têm suporte no Azure.</span><span class="sxs-lookup"><span data-stu-id="a341b-163">Both hello Red Hat compatible kernel and Oracle's UEK3 are supported in Azure.</span></span>  <span data-ttu-id="a341b-164">núcleo de UEK3 Olá é recomendado.</span><span class="sxs-lookup"><span data-stu-id="a341b-164">hello UEK3 kernel is recommended.</span></span>
* <span data-ttu-id="a341b-165">Olá Gerenciador do pacote não está em conflito com o agente do Linux Azure hello.</span><span class="sxs-lookup"><span data-stu-id="a341b-165">hello NetworkManager package no longer conflicts with hello Azure Linux agent.</span></span> <span data-ttu-id="a341b-166">Esse pacote é instalado por padrão e recomendamos que você não o remova.</span><span class="sxs-lookup"><span data-stu-id="a341b-166">This package is installed by default and we recommend that it is not removed.</span></span>
* <span data-ttu-id="a341b-167">GRUB2 agora é usado como Olá carregador de inicialização padrão, para que o procedimento Olá para editar os parâmetros de kernel foi alterada (consulte abaixo).</span><span class="sxs-lookup"><span data-stu-id="a341b-167">GRUB2 is now used as hello default bootloader, so hello procedure for editing kernel parameters has changed (see below).</span></span>
* <span data-ttu-id="a341b-168">XFS agora é um sistema de arquivos padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="a341b-168">XFS is now hello default file system.</span></span> <span data-ttu-id="a341b-169">sistema de arquivos ext4 Olá ainda pode ser usado, se desejado.</span><span class="sxs-lookup"><span data-stu-id="a341b-169">hello ext4 file system can still be used if desired.</span></span>

<span data-ttu-id="a341b-170">**Etapas da configuração**</span><span class="sxs-lookup"><span data-stu-id="a341b-170">**Configuration steps**</span></span>

1. <span data-ttu-id="a341b-171">No Gerenciador do Hyper-V, selecione máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="a341b-171">In Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="a341b-172">Clique em **conectar** tooopen uma janela do console da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="a341b-172">Click **Connect** tooopen a console window for hello virtual machine.</span></span>
3. <span data-ttu-id="a341b-173">Crie um arquivo chamado **rede** em Olá `/etc/sysconfig/` diretório que contém a saudação texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="a341b-173">Create a file named **network** in hello `/etc/sysconfig/` directory that contains hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
4. <span data-ttu-id="a341b-174">Crie um arquivo chamado **ifcfg eth0** em Olá `/etc/sysconfig/network-scripts/` diretório que contém a saudação texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="a341b-174">Create a file named **ifcfg-eth0** in hello `/etc/sysconfig/network-scripts/` directory that contains hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
5. <span data-ttu-id="a341b-175">Modificar udev regras tooavoid gerar regras estáticas para Olá interfaces Ethernet.</span><span class="sxs-lookup"><span data-stu-id="a341b-175">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="a341b-176">Essas regras podem provocar problemas ao clonar uma máquina virtual no Microsoft Azure ou no Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="a341b-176">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
6. <span data-ttu-id="a341b-177">Certifique-se de que o serviço de rede Olá será iniciado no momento da inicialização executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="a341b-177">Ensure hello network service will start at boot time by running hello following command:</span></span>
   
        # sudo chkconfig network on
7. <span data-ttu-id="a341b-178">Instale o pacote de python pyasn1 de saudação executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="a341b-178">Install hello python-pyasn1 package by running hello following command:</span></span>
   
        # sudo yum install python-pyasn1
8. <span data-ttu-id="a341b-179">Execute Olá metadados Olá yum atuais tooclear comando a seguir e instale todas as atualizações:</span><span class="sxs-lookup"><span data-stu-id="a341b-179">Run hello following command tooclear hello current yum metadata and install any updates:</span></span>
   
        # sudo yum clean all
        # sudo yum -y update
9. <span data-ttu-id="a341b-180">Modificar a linha de inicialização de kernel de saudação em seus parâmetros de kernel adicionais tooinclude grub configuração do Azure.</span><span class="sxs-lookup"><span data-stu-id="a341b-180">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="a341b-181">toodo nesse abrir "/ padrão/etc/grub" em uma saudação de editor e editar texto `GRUB_CMDLINE_LINUX` parâmetro, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a341b-181">toodo this open "/etc/default/grub" in a text editor and edit hello `GRUB_CMDLINE_LINUX` parameter, for example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="a341b-182">Isso garantirá todas as mensagens de console são enviadas toohello primeira porta serial, que pode ajudá-lo Azure suporte à depuração de problemas.</span><span class="sxs-lookup"><span data-stu-id="a341b-182">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="a341b-183">Ela também desativa novas convenções de nomenclatura OEL 7 Olá para as NICs.</span><span class="sxs-lookup"><span data-stu-id="a341b-183">It also turns off hello new OEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="a341b-184">Além disso toohello acima, recomenda-se muito*remover* Olá seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="a341b-184">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
   
       rhgb quiet crashkernel=auto
   
   <span data-ttu-id="a341b-185">Inicialização gráfica e silenciosa não são úteis em um ambiente de nuvem onde queremos que todos os toobe de logs de saudação enviada toohello de porta serial.</span><span class="sxs-lookup"><span data-stu-id="a341b-185">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>
   
   <span data-ttu-id="a341b-186">Olá `crashkernel` opção pode ser esquerda configurada, se desejado, mas observe que esse parâmetro será reduzir a quantidade de saudação de memória disponível em Olá VM em 128 MB ou mais, que pode ser problemático em tamanhos de VM menores hello.</span><span class="sxs-lookup"><span data-stu-id="a341b-186">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>
10. <span data-ttu-id="a341b-187">Quando tiver terminado a edição "/ padrão/etc/grub" por acima, execute Olá seguinte comando toorebuild Olá grub configuração:</span><span class="sxs-lookup"><span data-stu-id="a341b-187">Once you are done editing "/etc/default/grub" per above, run hello following command toorebuild hello grub configuration:</span></span>
    
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg
11. <span data-ttu-id="a341b-188">Certifique-se de servidor SSH hello está instalado e configurado toostart no momento da inicialização.</span><span class="sxs-lookup"><span data-stu-id="a341b-188">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="a341b-189">Geralmente, esse é o padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="a341b-189">This is usually hello default.</span></span>
12. <span data-ttu-id="a341b-190">Instale Olá agente Linux do Azure executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="a341b-190">Install hello Azure Linux Agent by running hello following command:</span></span>
    
        # sudo yum install WALinuxAgent
        # sudo systemctl enable waagent
13. <span data-ttu-id="a341b-191">Não crie espaço de permuta em disco do sistema operacional hello.</span><span class="sxs-lookup"><span data-stu-id="a341b-191">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="a341b-192">Olá agente Linux do Azure pode configurar automaticamente o espaço de permuta usando Olá disco de recurso local que é anexado toohello VM após a configuração no Azure.</span><span class="sxs-lookup"><span data-stu-id="a341b-192">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="a341b-193">Observe que esse disco de recurso local Olá é um *temporário* disco e pode ser esvaziada quando Olá VM for desprovisionada.</span><span class="sxs-lookup"><span data-stu-id="a341b-193">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="a341b-194">Depois de instalar o hello agente Linux do Azure (consulte a etapa anterior Olá), modificar Olá seguintes parâmetros em /etc/waagent.conf adequadamente:</span><span class="sxs-lookup"><span data-stu-id="a341b-194">After installing hello Azure Linux Agent (see hello previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.
14. <span data-ttu-id="a341b-195">Execute Olá seguindo a máquina virtual do comandos toodeprovision hello e prepará-la para provisionamento no Azure:</span><span class="sxs-lookup"><span data-stu-id="a341b-195">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
15. <span data-ttu-id="a341b-196">Clique em **Ação -> Desligar** no Gerenciador do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="a341b-196">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="a341b-197">O VHD Linux está agora pronto toobe carregado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="a341b-197">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a341b-198">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a341b-198">Next steps</span></span>
<span data-ttu-id="a341b-199">Você está agora pronto toouse seu Oracle Linux. vhd toocreate novas máquinas virtuais no Azure.</span><span class="sxs-lookup"><span data-stu-id="a341b-199">You're now ready toouse your Oracle Linux .vhd toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="a341b-200">Se isso for Olá primeira vez que você está carregando tooAzure de arquivo. vhd hello, consulte as etapas 2 e 3 em [criando e carregando um disco rígido virtual que contém o sistema de operacional Linux Olá](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a341b-200">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

