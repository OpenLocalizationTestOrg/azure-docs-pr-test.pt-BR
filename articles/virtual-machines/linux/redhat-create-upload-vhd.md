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
# <a name="prepare-a-red-hat-based-virtual-machine-for-azure"></a><span data-ttu-id="e0cb2-103">Preparar uma máquina virtual baseada no Red Hat para o Azure</span><span class="sxs-lookup"><span data-stu-id="e0cb2-103">Prepare a Red Hat-based virtual machine for Azure</span></span>
<span data-ttu-id="e0cb2-104">Neste artigo, você aprenderá como tooprepare uma máquina virtual de Red Hat Enterprise Linux (RHEL) para uso no Azure.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-104">In this article, you will learn how tooprepare a Red Hat Enterprise Linux (RHEL) virtual machine for use in Azure.</span></span> <span data-ttu-id="e0cb2-105">versões de saudação do RHEL que são abordadas neste artigo são 6.7 + e 7.1 +.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-105">hello versions of RHEL that are covered in this article are 6.7+ and 7.1+.</span></span> <span data-ttu-id="e0cb2-106">Olá hipervisores de preparação que são abordados neste artigo são máquinas virtuais Hyper-V, baseado no kernel (KVM) e VMware.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-106">hello hypervisors for preparation that are covered in this article are Hyper-V, kernel-based virtual machine (KVM), and VMware.</span></span> <span data-ttu-id="e0cb2-107">Para saber mais informações sobre os requisitos de qualificação para participação no programa Red Hat Cloud Access, confira o [site Red Hat Cloud Access](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) e o artigo[Como executar o RHEL no Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).</span><span class="sxs-lookup"><span data-stu-id="e0cb2-107">For more information about eligibility requirements for participating in Red Hat's Cloud Access program, see [Red Hat's Cloud Access website](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) and [Running RHEL on Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).</span></span>

## <a name="prepare-a-red-hat-based-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="e0cb2-108">Preparar uma máquina virtual baseada em Red Hat a partir do Gerenciador do Hyper-V</span><span class="sxs-lookup"><span data-stu-id="e0cb2-108">Prepare a Red Hat-based virtual machine from Hyper-V Manager</span></span>

### <a name="prerequisites"></a><span data-ttu-id="e0cb2-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e0cb2-109">Prerequisites</span></span>
<span data-ttu-id="e0cb2-110">Esta seção pressupõe que você já tiver obtido um arquivo ISO de site do Red Hat hello e Olá instalado RHEL imagem tooa disco rígido virtual (VHD).</span><span class="sxs-lookup"><span data-stu-id="e0cb2-110">This section assumes that you have already obtained an ISO file from hello Red Hat website and installed hello RHEL image tooa virtual hard disk (VHD).</span></span> <span data-ttu-id="e0cb2-111">Para obter mais detalhes sobre como toouse Gerenciador Hyper-V tooinstall uma imagem do sistema operacional, consulte [instalar Olá função Hyper-V e configurar uma máquina Virtual](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0cb2-111">For more details about how toouse Hyper-V Manager tooinstall an operating system image, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="e0cb2-112">**Notas de instalação do RHEL**</span><span class="sxs-lookup"><span data-stu-id="e0cb2-112">**RHEL installation notes**</span></span>

* <span data-ttu-id="e0cb2-113">Azure não oferece suporte a no formato VHDX hello.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-113">Azure does not support hello VHDX format.</span></span> <span data-ttu-id="e0cb2-114">O Azure suporta apenas VHD fixo.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-114">Azure supports only fixed VHD.</span></span> <span data-ttu-id="e0cb2-115">Você pode usar o formato de tooVHD do Gerenciador do Hyper-V tooconvert Olá disco, ou você pode usar o cmdlet convert-vhd de saudação.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-115">You can use Hyper-V Manager tooconvert hello disk tooVHD format, or you can use hello convert-vhd cmdlet.</span></span> <span data-ttu-id="e0cb2-116">Se você usar VirtualBox, selecione **tamanho fixo** contrário como padrão toohello alocada dinamicamente a opção ao criar o disco de saudação.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-116">If you use VirtualBox, select **Fixed size** as opposed toohello default dynamically allocated option when you create hello disk.</span></span>
* <span data-ttu-id="e0cb2-117">O Azure suporta somente as máquinas virtuais de geração 1.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-117">Azure supports only generation 1 virtual machines.</span></span> <span data-ttu-id="e0cb2-118">Você pode converter uma máquina virtual geração 1 de formato de arquivo VHD VHDX toohello em disco de tamanho fixo de tooa de expansão dinâmica.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-118">You can convert a generation 1 virtual machine from VHDX toohello VHD file format and from dynamically expanding tooa fixed-size disk.</span></span> <span data-ttu-id="e0cb2-119">Mas observe não é possível alterar a geração de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-119">You can't change a virtual machine's generation.</span></span> <span data-ttu-id="e0cb2-120">Para saber mais informações, confira [Devo criar uma máquina virtual de geração 1 ou 2 no Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span><span class="sxs-lookup"><span data-stu-id="e0cb2-120">For more information, see [Should I create a generation 1 or 2 virtual machine in Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span></span>
* <span data-ttu-id="e0cb2-121">tamanho máximo de saudação que é permitido para Olá VHD é 1.023 GB.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-121">hello maximum size that's allowed for hello VHD is 1,023 GB.</span></span>
* <span data-ttu-id="e0cb2-122">Quando você instala o sistema de operacional Linux hello, recomendamos que você use partições padrão em vez de Gerenciador de Volume lógico (LVM), que geralmente é o padrão de saudação para muitas instalações.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-122">When you install hello Linux operating system, we recommend that you use standard partitions rather than Logical Volume Manager (LVM), which is often hello default for many installations.</span></span> <span data-ttu-id="e0cb2-123">Essa prática evitará LVM nome conflita com máquinas virtuais, especialmente se você alguma vez precisar tooattach uma máquina virtual idêntica sistema operacional disco tooanother para solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-123">This practice will avoid LVM name conflicts with cloned virtual machines, particularly if you ever need tooattach an operating system disk tooanother identical virtual machine for troubleshooting.</span></span> <span data-ttu-id="e0cb2-124">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) podem ser usados nos discos de dados.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-124">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="e0cb2-125">É necessário suporte de kernel para montar sistemas de arquivos de formato de disco universal (UDF).</span><span class="sxs-lookup"><span data-stu-id="e0cb2-125">Kernel support for mounting Universal Disk Format (UDF) file systems is required.</span></span> <span data-ttu-id="e0cb2-126">Na primeira inicialização na mídia do Azure, Olá UDF formatado que é anexado toohello convidado passa Olá toohello provisionamento da configuração máquina virtual do Linux.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-126">At first boot on Azure, hello UDF-formatted media that is attached toohello guest passes hello provisioning configuration toohello Linux virtual machine.</span></span> <span data-ttu-id="e0cb2-127">Olá agente Linux do Azure deve ser capaz de toomount Olá UDF arquivo sistema tooread sua configuração e provisionar a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-127">hello Azure Linux Agent must be able toomount hello UDF file system tooread its configuration and provision hello virtual machine.</span></span>
* <span data-ttu-id="e0cb2-128">Versões do kernel do Linux Olá 2.6.37 anteriores não dão acesso não uniforme a memória (NUMA) no Hyper-V com os maiores tamanhos de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-128">Versions of hello Linux kernel that are earlier than 2.6.37 do not support non-uniform memory access (NUMA) on Hyper-V with larger virtual machine sizes.</span></span> <span data-ttu-id="e0cb2-129">Esse problema principalmente impactos distribuições mais antigas que usam Olá upstream kernel Red Hat 2.6.32 e foi corrigido em RHEL 6.6 (kernel-2.6.32-504).</span><span class="sxs-lookup"><span data-stu-id="e0cb2-129">This issue primarily impacts older distributions that use hello upstream Red Hat 2.6.32 kernel and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="e0cb2-130">Sistemas que executam kernels personalizados que são mais antigos que 2.6.37 ou kernels com base em RHEL mais antigos que 2.6.32-504 devem definir Olá `numa=off` parâmetro de inicialização na linha de comando de kernel Olá em grub.conf.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-130">Systems that run custom kernels that are older than 2.6.37 or RHEL-based kernels that are older than 2.6.32-504 must set hello `numa=off` boot parameter on hello kernel command line in grub.conf.</span></span> <span data-ttu-id="e0cb2-131">Para obter mais informações, confira o [KB 436883](https://access.redhat.com/solutions/436883) do Red Hat.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-131">For more information, see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="e0cb2-132">Não configure uma partição de troca no disco do sistema operacional hello.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-132">Do not configure a swap partition on hello operating system disk.</span></span> <span data-ttu-id="e0cb2-133">Olá agente Linux pode ser configurado toocreate um arquivo de permuta em disco de recursos temporário hello.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-133">hello Linux Agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="e0cb2-134">Para obter mais informações sobre isso podem ser encontradas no hello etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-134">More information about this can be found in hello following steps.</span></span>
* <span data-ttu-id="e0cb2-135">Todos os VHDs devem ter tamanhos que sejam múltiplos de 1 MB.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-135">All VHDs must have sizes that are multiples of 1 MB.</span></span>

### <a name="prepare-a-rhel-6-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="e0cb2-136">Preparar uma máquina virtual RHEL 6 do Gerenciador do Hyper-V</span><span class="sxs-lookup"><span data-stu-id="e0cb2-136">Prepare a RHEL 6 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="e0cb2-137">No Gerenciador do Hyper-V, selecione máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-137">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="e0cb2-138">Clique em **conectar** tooopen uma janela do console da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-138">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="e0cb2-139">RHEL 6, Gerenciador pode interferir com o agente do Linux Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-139">In RHEL 6, NetworkManager can interfere with hello Azure Linux agent.</span></span> <span data-ttu-id="e0cb2-140">Desinstale esse pacote executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-140">Uninstall this package by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

4. <span data-ttu-id="e0cb2-141">Criar ou editar Olá `/etc/sysconfig/network` de arquivo e, em seguida, adicione Olá texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-141">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="e0cb2-142">Criar ou editar Olá `/etc/sysconfig/network-scripts/ifcfg-eth0` de arquivo e, em seguida, adicione Olá texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-142">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="e0cb2-143">Mover (ou remover) Olá udev regras tooavoid gerar regras estáticas para interface de Ethernet hello.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-143">Move (or remove) hello udev rules tooavoid generating static rules for hello Ethernet interface.</span></span> <span data-ttu-id="e0cb2-144">Essas regras causam problemas ao clonar uma máquina virtual no Microsoft Azure ou no Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-144">These rules cause problems when you clone a virtual machine in Microsoft Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="e0cb2-145">Certifique-se de que o serviço de rede Olá iniciará no momento da inicialização executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-145">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

8. <span data-ttu-id="e0cb2-146">Registre a instalação de saudação Red Hat assinatura tooenable de pacotes do repositório do RHEL Olá executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-146">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

9. <span data-ttu-id="e0cb2-147">pacote de WALinuxAgent Hello, `WALinuxAgent-<version>`, foi introduzido repositório do toohello Red Hat extras.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-147">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="e0cb2-148">Habilite o repositório de extras Olá executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-148">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

10. <span data-ttu-id="e0cb2-149">Modificar a linha de inicialização de kernel de saudação em seus parâmetros de kernel adicionais tooinclude grub configuração do Azure.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-149">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="e0cb2-150">toodo essa modificação, abra `/boot/grub/menu.lst` em um editor de texto e certifique-se de que kernel de padrão de saudação inclui Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-150">toodo this modification, open `/boot/grub/menu.lst` in a text editor, and ensure that hello default kernel includes hello following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="e0cb2-151">Isso garantirá que todas as mensagens de console são enviadas toohello primeira porta serial, que pode ajudá-lo Azure suporte à depuração de problemas.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-151">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="e0cb2-152">Além disso, é recomendável que você remova Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-152">In addition, we recommended that you remove hello following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="e0cb2-153">Inicialização gráfica e silenciosa não são úteis em um ambiente de nuvem onde queremos que todos os toobe de logs de saudação enviada toohello de porta serial.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-153">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>  <span data-ttu-id="e0cb2-154">Você pode deixar Olá `crashkernel` opção de configuração, se desejado.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-154">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="e0cb2-155">Observe que esse parâmetro reduz a quantidade de saudação de memória disponível na máquina virtual Olá 128 MB ou mais.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-155">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more.</span></span> <span data-ttu-id="e0cb2-156">Essa configuração pode ser um problema em máquinas virtuais menores.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-156">This configuration might be problematic on smaller virtual machine sizes.</span></span>

    >[!Important]
    <span data-ttu-id="e0cb2-157">RHEL 6.5 e anterior também deve definir Olá `numa=off` parâmetro de kernel.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-157">RHEL 6.5 and earlier must also set hello `numa=off` kernel parameter.</span></span> <span data-ttu-id="e0cb2-158">Consulte Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="e0cb2-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

11. <span data-ttu-id="e0cb2-159">Certifique-se de servidor SSH (secure shell) hello está instalado e configurado toostart no momento da inicialização, que normalmente é o padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-159">Ensure that hello secure shell (SSH) server is installed and configured toostart at boot time, which is usually hello default.</span></span> <span data-ttu-id="e0cb2-160">Modificar /etc/ssh/sshd_config tooinclude Olá seguinte linha:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-160">Modify /etc/ssh/sshd_config tooinclude hello following line:</span></span>

        ClientAliveInterval 180

12. <span data-ttu-id="e0cb2-161">Instale Olá agente Linux do Azure executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-161">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

    <span data-ttu-id="e0cb2-162">Instalar pacote de WALinuxAgent Olá remove hello Gerenciador e pacotes de Gerenciador gnome se eles já não foram removidos na etapa 3.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-162">Installing hello WALinuxAgent package removes hello NetworkManager and NetworkManager-gnome packages if they were not already removed in step 3.</span></span>

13. <span data-ttu-id="e0cb2-163">Não crie espaço de permuta no disco do sistema operacional hello.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-163">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="e0cb2-164">Olá agente Linux do Azure pode configurar automaticamente o espaço de permuta usando Olá disco de recurso local que é anexado toohello máquina de virtual depois de máquina virtual de saudação é provisionada no Azure.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-164">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="e0cb2-165">Observe que Olá local do disco de recurso é temporária e que talvez esvaziada quando a máquina virtual de saudação desprovisionada.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-165">Note that hello local resource disk is a temporary disk and that it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="e0cb2-166">Depois de instalar o hello Azure Linux Agent na etapa anterior hello, modificar Olá seguintes parâmetros em /etc/waagent.conf adequadamente:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-166">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in /etc/waagent.conf appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

14. <span data-ttu-id="e0cb2-167">Cancelar o registro de assinatura de saudação (se necessário) executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-167">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # sudo subscription-manager unregister

15. <span data-ttu-id="e0cb2-168">Execute Olá seguindo a máquina virtual do comandos toodeprovision hello e prepará-la para provisionamento no Azure:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-168">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

16. <span data-ttu-id="e0cb2-169">Clique em **Ação** > **Desligar** no Gerenciador do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-169">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="e0cb2-170">O VHD Linux está agora pronto toobe carregado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-170">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>


### <a name="prepare-a-rhel-7-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="e0cb2-171">Preparar uma máquina virtual RHEL 7 do Gerenciador do Hyper-V</span><span class="sxs-lookup"><span data-stu-id="e0cb2-171">Prepare a RHEL 7 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="e0cb2-172">No Gerenciador do Hyper-V, selecione máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-172">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="e0cb2-173">Clique em **conectar** tooopen uma janela do console da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-173">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="e0cb2-174">Criar ou editar Olá `/etc/sysconfig/network` de arquivo e, em seguida, adicione Olá texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-174">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. <span data-ttu-id="e0cb2-175">Criar ou editar Olá `/etc/sysconfig/network-scripts/ifcfg-eth0` de arquivo e, em seguida, adicione Olá texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-175">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. <span data-ttu-id="e0cb2-176">Certifique-se de que o serviço de rede Olá iniciará no momento da inicialização executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-176">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

6. <span data-ttu-id="e0cb2-177">Registre a instalação de saudação Red Hat assinatura tooenable de pacotes do repositório do RHEL Olá executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-177">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. <span data-ttu-id="e0cb2-178">Modificar a linha de inicialização de kernel de saudação em seus parâmetros de kernel adicionais tooinclude grub configuração do Azure.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-178">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="e0cb2-179">toodo essa modificação, abra `/etc/default/grub` em um editor de texto e edição Olá `GRUB_CMDLINE_LINUX` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-179">toodo this modification, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="e0cb2-180">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-180">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="e0cb2-181">Isso garantirá que todas as mensagens de console são enviadas toohello primeira porta serial, que pode ajudá-lo Azure suporte à depuração de problemas.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-181">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="e0cb2-182">Essa configuração também desativa novas convenções de nomenclatura RHEL 7 Olá para as NICs.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-182">This configuration also turns off hello new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="e0cb2-183">Além disso, recomendamos que você remova Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-183">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="e0cb2-184">Inicialização gráfica e silenciosa não são úteis em um ambiente de nuvem onde queremos que todos os toobe de logs de saudação enviada toohello de porta serial.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-184">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="e0cb2-185">Você pode deixar Olá `crashkernel` opção de configuração, se desejado.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-185">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="e0cb2-186">Observe que esse parâmetro reduz a quantidade de saudação de memória disponível na máquina virtual Olá 128 MB ou mais, que pode ser problemático em tamanhos menores de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-186">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

8. <span data-ttu-id="e0cb2-187">Depois de terminar edição `/etc/default/grub`, execute hello toorebuild Olá grub configuração dos comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-187">After you are done editing `/etc/default/grub`, run hello following command toorebuild hello grub configuration:</span></span>

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

9. <span data-ttu-id="e0cb2-188">Certifique-se de servidor SSH hello está instalado e configurado toostart no momento da inicialização, que normalmente é o padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-188">Ensure that hello SSH server is installed and configured toostart at boot time, which is usually hello default.</span></span> <span data-ttu-id="e0cb2-189">Modificar `/etc/ssh/sshd_config` tooinclude Olá seguinte linha:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-189">Modify `/etc/ssh/sshd_config` tooinclude hello following line:</span></span>

        ClientAliveInterval 180

10. <span data-ttu-id="e0cb2-190">pacote de WALinuxAgent Hello, `WALinuxAgent-<version>`, foi introduzido repositório do toohello Red Hat extras.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-190">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="e0cb2-191">Habilite o repositório de extras Olá executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-191">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

11. <span data-ttu-id="e0cb2-192">Instale Olá agente Linux do Azure executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-192">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

12. <span data-ttu-id="e0cb2-193">Não crie espaço de permuta no disco do sistema operacional hello.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-193">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="e0cb2-194">Olá agente Linux do Azure pode configurar automaticamente o espaço de permuta usando Olá disco de recurso local que é anexado toohello máquina de virtual depois de máquina virtual de saudação é provisionada no Azure.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-194">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="e0cb2-195">Observe que hello, disco de recurso local é um disco temporário, e pode ser esvaziada quando a máquina virtual de saudação desprovisionada.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-195">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="e0cb2-196">Depois de instalar o hello Azure Linux Agent na etapa anterior Olá, modificar Olá parâmetros a seguir `/etc/waagent.conf` adequadamente:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-196">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. <span data-ttu-id="e0cb2-197">Se desejar que a assinatura de saudação toounregister, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-197">If you want toounregister hello subscription, run hello following command:</span></span>

        # sudo subscription-manager unregister

14. <span data-ttu-id="e0cb2-198">Execute Olá seguindo a máquina virtual do comandos toodeprovision hello e prepará-la para provisionamento no Azure:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-198">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. <span data-ttu-id="e0cb2-199">Clique em **Ação** > **Desligar** no Gerenciador do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-199">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="e0cb2-200">O VHD Linux está agora pronto toobe carregado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-200">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>


## <a name="prepare-a-red-hat-based-virtual-machine-from-kvm"></a><span data-ttu-id="e0cb2-201">Preparar uma máquina virtual baseada no Red Hat para KVM</span><span class="sxs-lookup"><span data-stu-id="e0cb2-201">Prepare a Red Hat-based virtual machine from KVM</span></span>
### <a name="prepare-a-rhel-6-virtual-machine-from-kvm"></a><span data-ttu-id="e0cb2-202">Preparar uma máquina virtual RHEL 6 do KVM</span><span class="sxs-lookup"><span data-stu-id="e0cb2-202">Prepare a RHEL 6 virtual machine from KVM</span></span>

1. <span data-ttu-id="e0cb2-203">Baixe imagem KVM de saudação do RHEL 6 do site do Red Hat hello.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-203">Download hello KVM image of RHEL 6 from hello Red Hat website.</span></span>

2. <span data-ttu-id="e0cb2-204">Definir uma senha raiz.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-204">Set a root password.</span></span>

    <span data-ttu-id="e0cb2-205">Gerar uma senha criptografada e copie a saída de saudação do comando hello:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-205">Generate an encrypted password, and copy hello output of hello command:</span></span>

        # openssl passwd -1 changeme

    <span data-ttu-id="e0cb2-206">Defina uma senha raiz com guestfish:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-206">Set a root password with guestfish:</span></span>
        
        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   <span data-ttu-id="e0cb2-207">Alteração Olá segundo campo de usuário raiz hello "!"</span><span class="sxs-lookup"><span data-stu-id="e0cb2-207">Change hello second field of hello root user from "!!"</span></span> <span data-ttu-id="e0cb2-208">toohello senha criptografada.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-208">toohello encrypted password.</span></span>

3. <span data-ttu-id="e0cb2-209">Crie uma máquina virtual em KVM da imagem de qcow2 hello.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-209">Create a virtual machine in KVM from hello qcow2 image.</span></span> <span data-ttu-id="e0cb2-210">Definir o tipo de disco Olá muito**qcow2**e defina o modelo de dispositivo de interface de rede virtual Olá muito**virtio**.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-210">Set hello disk type too**qcow2**, and set hello virtual network interface device model too**virtio**.</span></span> <span data-ttu-id="e0cb2-211">Em seguida, iniciar a máquina virtual de saudação e entre como raiz.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-211">Then, start hello virtual machine, and sign in as root.</span></span>

4. <span data-ttu-id="e0cb2-212">Criar ou editar Olá `/etc/sysconfig/network` de arquivo e, em seguida, adicione Olá texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-212">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="e0cb2-213">Criar ou editar Olá `/etc/sysconfig/network-scripts/ifcfg-eth0` de arquivo e, em seguida, adicione Olá texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-213">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="e0cb2-214">Mover (ou remover) Olá udev regras tooavoid gerar regras estáticas para interface de Ethernet hello.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-214">Move (or remove) hello udev rules tooavoid generating static rules for hello Ethernet interface.</span></span> <span data-ttu-id="e0cb2-215">Essas regras causam problemas ao clonar uma máquina virtual no Azure ou no Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-215">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="e0cb2-216">Certifique-se de que o serviço de rede Olá iniciará no momento da inicialização executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-216">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # chkconfig network on

8. <span data-ttu-id="e0cb2-217">Registre a instalação de saudação Red Hat assinatura tooenable de pacotes do repositório do RHEL Olá executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-217">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # subscription-manager register --auto-attach --username=XXX --password=XXX

9. <span data-ttu-id="e0cb2-218">Modificar a linha de inicialização de kernel de saudação em seus parâmetros de kernel adicionais tooinclude grub configuração do Azure.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-218">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="e0cb2-219">toodo essa configuração, abra `/boot/grub/menu.lst` em um editor de texto e certifique-se de que kernel de padrão de saudação inclui Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-219">toodo this configuration, open `/boot/grub/menu.lst` in a text editor, and ensure that hello default kernel includes hello following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="e0cb2-220">Isso garantirá que todas as mensagens de console são enviadas toohello primeira porta serial, que pode ajudá-lo Azure suporte à depuração de problemas.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-220">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="e0cb2-221">Além disso, recomendamos que você remova Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-221">In addition, we recommend that you remove hello following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="e0cb2-222">Inicialização gráfica e silenciosa não são úteis em um ambiente de nuvem onde queremos que todos os toobe de logs de saudação enviada toohello de porta serial.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-222">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="e0cb2-223">Você pode deixar Olá `crashkernel` opção de configuração, se desejado.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-223">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="e0cb2-224">Observe que esse parâmetro reduz a quantidade de saudação de memória disponível na máquina virtual Olá 128 MB ou mais, que pode ser problemático em tamanhos menores de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-224">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

    >[!Important]
    <span data-ttu-id="e0cb2-225">RHEL 6.5 e anterior também deve definir Olá `numa=off` parâmetro de kernel.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-225">RHEL 6.5 and earlier must also set hello `numa=off` kernel parameter.</span></span> <span data-ttu-id="e0cb2-226">Consulte Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="e0cb2-226">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

10. <span data-ttu-id="e0cb2-227">Adicione tooinitramfs de módulos do Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-227">Add Hyper-V modules tooinitramfs:</span></span>  

    <span data-ttu-id="e0cb2-228">Editar `/etc/dracut.conf`e adicione Olá conteúdo a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-228">Edit `/etc/dracut.conf`, and add hello following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="e0cb2-229">Recrie initramfs:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-229">Rebuild initramfs:</span></span>

        # dracut -f -v

11. <span data-ttu-id="e0cb2-230">Desinstale cloud-init:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-230">Uninstall cloud-init:</span></span>

        # yum remove cloud-init

12. <span data-ttu-id="e0cb2-231">Certifique-se de servidor SSH hello está instalado e configurado toostart durante a inicialização:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-231">Ensure that hello SSH server is installed and configured toostart at boot time:</span></span>

        # chkconfig sshd on

    <span data-ttu-id="e0cb2-232">Modificar /etc/ssh/sshd_config tooinclude Olá linhas seguintes:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-232">Modify /etc/ssh/sshd_config tooinclude hello following lines:</span></span>

        PasswordAuthentication yes
        ClientAliveInterval 180

13. <span data-ttu-id="e0cb2-233">pacote de WALinuxAgent Hello, `WALinuxAgent-<version>`, foi introduzido repositório do toohello Red Hat extras.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-233">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="e0cb2-234">Habilite o repositório de extras Olá executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-234">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

14. <span data-ttu-id="e0cb2-235">Instale Olá agente Linux do Azure executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-235">Install hello Azure Linux Agent by running hello following command:</span></span>

        # yum install WALinuxAgent

        # chkconfig waagent on

15. <span data-ttu-id="e0cb2-236">Olá agente Linux do Azure pode configurar automaticamente o espaço de permuta usando Olá disco de recurso local que é anexado toohello máquina de virtual depois de máquina virtual de saudação é provisionada no Azure.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-236">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="e0cb2-237">Observe que hello, disco de recurso local é um disco temporário, e pode ser esvaziada quando a máquina virtual de saudação desprovisionada.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-237">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="e0cb2-238">Depois de instalar o hello Azure Linux Agent na etapa anterior Olá, modificar Olá parâmetros a seguir **/etc/waagent.conf** adequadamente:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-238">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in **/etc/waagent.conf** appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. <span data-ttu-id="e0cb2-239">Cancelar o registro de assinatura de saudação (se necessário) executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-239">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # subscription-manager unregister

17. <span data-ttu-id="e0cb2-240">Execute Olá seguindo a máquina virtual do comandos toodeprovision hello e prepará-la para provisionamento no Azure:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-240">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. <span data-ttu-id="e0cb2-241">Desligar a máquina virtual Olá KVM.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-241">Shut down hello virtual machine in KVM.</span></span>

19. <span data-ttu-id="e0cb2-242">Converta o formato VHD Olá qcow2 imagem toohello.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-242">Convert hello qcow2 image toohello VHD format.</span></span>

    <span data-ttu-id="e0cb2-243">Primeiro converter o formato de tooraw Olá imagem:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-243">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f qcow2 -O raw rhel-6.8.qcow2 rhel-6.8.raw

    <span data-ttu-id="e0cb2-244">Certifique-se de que tamanho Olá da imagem brutos hello está alinhado com 1 MB.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-244">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="e0cb2-245">Caso contrário, arredonde Olá tamanho tooalign com 1 MB:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-245">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="e0cb2-246">Converter Olá disco raw tooa tamanho fixo VHD:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-246">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd


### <a name="prepare-a-rhel-7-virtual-machine-from-kvm"></a><span data-ttu-id="e0cb2-247">Preparar uma máquina virtual RHEL 7 do KVM</span><span class="sxs-lookup"><span data-stu-id="e0cb2-247">Prepare a RHEL 7 virtual machine from KVM</span></span>

1. <span data-ttu-id="e0cb2-248">Baixe imagem KVM de saudação do RHEL 7 do site do Red Hat hello.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-248">Download hello KVM image of RHEL 7 from hello Red Hat website.</span></span> <span data-ttu-id="e0cb2-249">Esse procedimento usa RHEL 7 como exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-249">This procedure uses RHEL 7 as hello example.</span></span>

2. <span data-ttu-id="e0cb2-250">Definir uma senha raiz.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-250">Set a root password.</span></span>

    <span data-ttu-id="e0cb2-251">Gerar uma senha criptografada e copie a saída de saudação do comando hello:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-251">Generate an encrypted password, and copy hello output of hello command:</span></span>

        # openssl passwd -1 changeme

    <span data-ttu-id="e0cb2-252">Defina uma senha raiz com guestfish:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-252">Set a root password with guestfish:</span></span>

        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   <span data-ttu-id="e0cb2-253">Alteração Olá segundo campo de usuário de raiz de "!"</span><span class="sxs-lookup"><span data-stu-id="e0cb2-253">Change hello second field of root user from "!!"</span></span> <span data-ttu-id="e0cb2-254">toohello senha criptografada.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-254">toohello encrypted password.</span></span>

3. <span data-ttu-id="e0cb2-255">Crie uma máquina virtual em KVM da imagem de qcow2 hello.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-255">Create a virtual machine in KVM from hello qcow2 image.</span></span> <span data-ttu-id="e0cb2-256">Definir o tipo de disco Olá muito**qcow2**e defina o modelo de dispositivo de interface de rede virtual Olá muito**virtio**.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-256">Set hello disk type too**qcow2**, and set hello virtual network interface device model too**virtio**.</span></span> <span data-ttu-id="e0cb2-257">Em seguida, iniciar a máquina virtual de saudação e entre como raiz.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-257">Then, start hello virtual machine, and sign in as root.</span></span>

4. <span data-ttu-id="e0cb2-258">Criar ou editar Olá `/etc/sysconfig/network` de arquivo e, em seguida, adicione Olá texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-258">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="e0cb2-259">Criar ou editar Olá `/etc/sysconfig/network-scripts/ifcfg-eth0` de arquivo e, em seguida, adicione Olá texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-259">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

6. <span data-ttu-id="e0cb2-260">Certifique-se de que o serviço de rede Olá iniciará no momento da inicialização executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-260">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # chkconfig network on

7. <span data-ttu-id="e0cb2-261">Registre a instalação do Red Hat assinatura tooenable de pacotes do repositório do RHEL Olá executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-261">Register your Red Hat subscription tooenable installation of packages from hello RHEL repository by running hello following command:</span></span>

        # subscription-manager register --auto-attach --username=XXX --password=XXX

8. <span data-ttu-id="e0cb2-262">Modificar a linha de inicialização de kernel de saudação em seus parâmetros de kernel adicionais tooinclude grub configuração do Azure.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-262">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="e0cb2-263">toodo essa configuração, abra `/etc/default/grub` em um editor de texto e edição Olá `GRUB_CMDLINE_LINUX` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-263">toodo this configuration, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="e0cb2-264">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-264">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="e0cb2-265">Esse comando também garante que todas as mensagens de console são enviadas toohello primeira porta serial, que pode ajudá-lo Azure suporte à depuração de problemas.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-265">This command also ensures that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="e0cb2-266">comando Olá também desativa novas convenções de nomenclatura RHEL 7 Olá para as NICs.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-266">hello command also turns off hello new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="e0cb2-267">Além disso, recomendamos que você remova Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-267">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="e0cb2-268">Inicialização gráfica e silenciosa não são úteis em um ambiente de nuvem onde queremos que todos os toobe de logs de saudação enviada toohello de porta serial.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-268">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="e0cb2-269">Você pode deixar Olá `crashkernel` opção de configuração, se desejado.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-269">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="e0cb2-270">Observe que esse parâmetro reduz a quantidade de saudação de memória disponível na máquina virtual Olá 128 MB ou mais, que pode ser problemático em tamanhos menores de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-270">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

9. <span data-ttu-id="e0cb2-271">Depois de terminar edição `/etc/default/grub`, execute hello toorebuild Olá grub configuração dos comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-271">After you are done editing `/etc/default/grub`, run hello following command toorebuild hello grub configuration:</span></span>

        # grub2-mkconfig -o /boot/grub2/grub.cfg

10. <span data-ttu-id="e0cb2-272">Adicione os módulos do Hyper-V em initramfs.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-272">Add Hyper-V modules into initramfs.</span></span>

    <span data-ttu-id="e0cb2-273">Edite `/etc/dracut.conf` e adicione o conteúdo:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-273">Edit `/etc/dracut.conf` and add content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="e0cb2-274">Recrie initramfs:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-274">Rebuild initramfs:</span></span>

        # dracut -f -v

11. <span data-ttu-id="e0cb2-275">Desinstale cloud-init:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-275">Uninstall cloud-init:</span></span>

        # yum remove cloud-init

12. <span data-ttu-id="e0cb2-276">Certifique-se de servidor SSH hello está instalado e configurado toostart durante a inicialização:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-276">Ensure that hello SSH server is installed and configured toostart at boot time:</span></span>

        # systemctl enable sshd

    <span data-ttu-id="e0cb2-277">Modificar /etc/ssh/sshd_config tooinclude Olá linhas seguintes:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-277">Modify /etc/ssh/sshd_config tooinclude hello following lines:</span></span>

        PasswordAuthentication yes
        ClientAliveInterval 180

13. <span data-ttu-id="e0cb2-278">pacote de WALinuxAgent Hello, `WALinuxAgent-<version>`, foi introduzido repositório do toohello Red Hat extras.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-278">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="e0cb2-279">Habilite o repositório de extras Olá executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-279">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

14. <span data-ttu-id="e0cb2-280">Instale Olá agente Linux do Azure executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-280">Install hello Azure Linux Agent by running hello following command:</span></span>

        # yum install WALinuxAgent

    <span data-ttu-id="e0cb2-281">Habilite o serviço de waagent hello:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-281">Enable hello waagent service:</span></span>

        # systemctl enable waagent.service

15. <span data-ttu-id="e0cb2-282">Não crie espaço de permuta no disco do sistema operacional hello.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-282">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="e0cb2-283">Olá agente Linux do Azure pode configurar automaticamente o espaço de permuta usando Olá disco de recurso local que é anexado toohello máquina de virtual depois de máquina virtual de saudação é provisionada no Azure.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-283">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="e0cb2-284">Observe que hello, disco de recurso local é um disco temporário, e pode ser esvaziada quando a máquina virtual de saudação desprovisionada.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-284">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="e0cb2-285">Depois de instalar o hello Azure Linux Agent na etapa anterior Olá, modificar Olá parâmetros a seguir `/etc/waagent.conf` adequadamente:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-285">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. <span data-ttu-id="e0cb2-286">Cancelar o registro de assinatura de saudação (se necessário) executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-286">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # subscription-manager unregister

17. <span data-ttu-id="e0cb2-287">Execute Olá seguindo a máquina virtual do comandos toodeprovision hello e prepará-la para provisionamento no Azure:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-287">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. <span data-ttu-id="e0cb2-288">Desligar a máquina virtual Olá KVM.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-288">Shut down hello virtual machine in KVM.</span></span>

19. <span data-ttu-id="e0cb2-289">Converta o formato VHD Olá qcow2 imagem toohello.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-289">Convert hello qcow2 image toohello VHD format.</span></span>

    <span data-ttu-id="e0cb2-290">Primeiro converter o formato de tooraw Olá imagem:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-290">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f qcow2 -O raw rhel-7.3.qcow2 rhel-7.3.raw

    <span data-ttu-id="e0cb2-291">Certifique-se de que tamanho Olá da imagem brutos hello está alinhado com 1 MB.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-291">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="e0cb2-292">Caso contrário, arredonde Olá tamanho tooalign com 1 MB:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-292">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="e0cb2-293">Converter Olá disco raw tooa tamanho fixo VHD:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-293">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-vmware"></a><span data-ttu-id="e0cb2-294">Preparar uma máquina virtual baseada no Red Hat do VMware</span><span class="sxs-lookup"><span data-stu-id="e0cb2-294">Prepare a Red Hat-based virtual machine from VMware</span></span>
### <a name="prerequisites"></a><span data-ttu-id="e0cb2-295">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e0cb2-295">Prerequisites</span></span>
<span data-ttu-id="e0cb2-296">Esta seção pressupõe que você já instalou uma máquina virtual RHEL no VMware.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-296">This section assumes that you have already installed a RHEL virtual machine in VMware.</span></span> <span data-ttu-id="e0cb2-297">Para obter detalhes sobre como tooinstall um sistema operacional em VMware, consulte [guia de instalação de sistema operacional de convidado do VMware](http://partnerweb.vmware.com/GOSIG/home.html).</span><span class="sxs-lookup"><span data-stu-id="e0cb2-297">For details about how tooinstall an operating system in VMware, see [VMware Guest Operating System Installation Guide](http://partnerweb.vmware.com/GOSIG/home.html).</span></span>

* <span data-ttu-id="e0cb2-298">Quando você instala o sistema de operacional Linux hello, recomendamos que você use partições padrão em vez de LVM, que geralmente é o padrão de saudação para muitas instalações.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-298">When you install hello Linux operating system, we recommend that you use standard partitions rather than LVM, which is often hello default for many installations.</span></span> <span data-ttu-id="e0cb2-299">Isso evitará LVM nome está em conflito com a máquina virtual clonada, especialmente se um disco do sistema operacional nunca precisa de máquina de virtual tooanother toobe anexado para solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-299">This will avoid LVM name conflicts with cloned virtual machine, particularly if an operating system disk ever needs toobe attached tooanother virtual machine for troubleshooting.</span></span> <span data-ttu-id="e0cb2-300">Se você preferir, é possível usar LVM ou RAID em discos de dados.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-300">LVM or RAID can be used on data disks if preferred.</span></span>
* <span data-ttu-id="e0cb2-301">Não configure uma partição de troca no disco do sistema operacional hello.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-301">Do not configure a swap partition on hello operating system disk.</span></span> <span data-ttu-id="e0cb2-302">Você pode configurar Olá Linux agent toocreate um arquivo de permuta em disco de recursos temporário hello.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-302">You can configure hello Linux agent toocreate a swap file on hello temporary resource disk.</span></span> <span data-ttu-id="e0cb2-303">Você encontrará mais informações sobre isso nas etapas Olá seguir.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-303">You can find more information about this in hello steps that follow.</span></span>
* <span data-ttu-id="e0cb2-304">Quando você cria um disco rígido virtual de saudação, selecione **disco virtual de armazenamento como um único arquivo**.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-304">When you create hello virtual hard disk, select **Store virtual disk as a single file**.</span></span>

### <a name="prepare-a-rhel-6-virtual-machine-from-vmware"></a><span data-ttu-id="e0cb2-305">Preparar uma máquina virtual RHEL 6 do VMware</span><span class="sxs-lookup"><span data-stu-id="e0cb2-305">Prepare a RHEL 6 virtual machine from VMware</span></span>
1. <span data-ttu-id="e0cb2-306">RHEL 6, Gerenciador pode interferir com o agente do Linux Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-306">In RHEL 6, NetworkManager can interfere with hello Azure Linux agent.</span></span> <span data-ttu-id="e0cb2-307">Desinstale esse pacote executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-307">Uninstall this package by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

2. <span data-ttu-id="e0cb2-308">Crie um arquivo chamado **rede** Olá Olá /etc/hosts sysconfig/diretório que contém texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-308">Create a file named **network** in hello /etc/sysconfig/ directory that contains hello following text:</span></span>

        NETWORKING=yes
        HOSTNAME=localhost.localdomain

3. <span data-ttu-id="e0cb2-309">Criar ou editar Olá `/etc/sysconfig/network-scripts/ifcfg-eth0` de arquivo e, em seguida, adicione Olá texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-309">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

4. <span data-ttu-id="e0cb2-310">Mover (ou remover) Olá udev regras tooavoid gerar regras estáticas para interface de Ethernet hello.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-310">Move (or remove) hello udev rules tooavoid generating static rules for hello Ethernet interface.</span></span> <span data-ttu-id="e0cb2-311">Essas regras causam problemas ao clonar uma máquina virtual no Azure ou no Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-311">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

5. <span data-ttu-id="e0cb2-312">Certifique-se de que o serviço de rede Olá iniciará no momento da inicialização executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-312">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

6. <span data-ttu-id="e0cb2-313">Registre a instalação de saudação Red Hat assinatura tooenable de pacotes do repositório do RHEL Olá executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-313">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. <span data-ttu-id="e0cb2-314">pacote de WALinuxAgent Hello, `WALinuxAgent-<version>`, foi introduzido repositório do toohello Red Hat extras.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-314">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="e0cb2-315">Habilite o repositório de extras Olá executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-315">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

8. <span data-ttu-id="e0cb2-316">Modificar a linha de inicialização de kernel de saudação em seus parâmetros de kernel adicionais tooinclude grub configuração do Azure.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-316">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="e0cb2-317">toodo isso, abra `/etc/default/grub` em um editor de texto e edição Olá `GRUB_CMDLINE_LINUX` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-317">toodo this, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="e0cb2-318">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-318">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0"
   
   <span data-ttu-id="e0cb2-319">Isso garantirá que todas as mensagens de console são enviadas toohello primeira porta serial, que pode ajudá-lo Azure suporte à depuração de problemas.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-319">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="e0cb2-320">Além disso, recomendamos que você remova Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-320">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="e0cb2-321">Inicialização gráfica e silenciosa não são úteis em um ambiente de nuvem onde queremos que todos os toobe de logs de saudação enviada toohello de porta serial.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-321">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="e0cb2-322">Você pode deixar Olá `crashkernel` opção de configuração, se desejado.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-322">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="e0cb2-323">Observe que esse parâmetro reduz a quantidade de saudação de memória disponível na máquina virtual Olá 128 MB ou mais, que pode ser problemático em tamanhos menores de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-323">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

9. <span data-ttu-id="e0cb2-324">Adicione tooinitramfs de módulos do Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-324">Add Hyper-V modules tooinitramfs:</span></span>

    <span data-ttu-id="e0cb2-325">Editar `/etc/dracut.conf`e adicione Olá conteúdo a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-325">Edit `/etc/dracut.conf`, and add hello following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="e0cb2-326">Recrie initramfs:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-326">Rebuild initramfs:</span></span>

        # dracut -f -v

10. <span data-ttu-id="e0cb2-327">Certifique-se de servidor SSH hello está instalado e configurado toostart no momento da inicialização, que normalmente é o padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-327">Ensure that hello SSH server is installed and configured toostart at boot time, which is usually hello default.</span></span> <span data-ttu-id="e0cb2-328">Modificar `/etc/ssh/sshd_config` tooinclude Olá seguinte linha:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-328">Modify `/etc/ssh/sshd_config` tooinclude hello following line:</span></span>

    <span data-ttu-id="e0cb2-329">ClientAliveInterval 180</span><span class="sxs-lookup"><span data-stu-id="e0cb2-329">ClientAliveInterval 180</span></span>

11. <span data-ttu-id="e0cb2-330">Instale Olá agente Linux do Azure executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-330">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

12. <span data-ttu-id="e0cb2-331">Não crie espaço de permuta no disco do sistema operacional hello.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-331">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="e0cb2-332">Olá agente Linux do Azure pode configurar automaticamente o espaço de permuta usando Olá disco de recurso local que é anexado toohello máquina de virtual depois de máquina virtual de saudação é provisionada no Azure.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-332">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="e0cb2-333">Observe que hello, disco de recurso local é um disco temporário, e pode ser esvaziada quando a máquina virtual de saudação desprovisionada.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-333">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="e0cb2-334">Depois de instalar o hello Azure Linux Agent na etapa anterior Olá, modificar Olá parâmetros a seguir `/etc/waagent.conf` adequadamente:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-334">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. <span data-ttu-id="e0cb2-335">Cancelar o registro de assinatura de saudação (se necessário) executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-335">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # sudo subscription-manager unregister

14. <span data-ttu-id="e0cb2-336">Execute Olá seguindo a máquina virtual do comandos toodeprovision hello e prepará-la para provisionamento no Azure:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-336">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. <span data-ttu-id="e0cb2-337">Desligar a máquina virtual de saudação e converter o arquivo. vhd do hello VMDK arquivo tooa.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-337">Shut down hello virtual machine, and convert hello VMDK file tooa .vhd file.</span></span>

    <span data-ttu-id="e0cb2-338">Primeiro converter o formato de tooraw Olá imagem:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-338">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f vmdk -O raw rhel-6.8.vmdk rhel-6.8.raw

    <span data-ttu-id="e0cb2-339">Certifique-se de que tamanho Olá da imagem brutos hello está alinhado com 1 MB.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-339">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="e0cb2-340">Caso contrário, arredonde Olá tamanho tooalign com 1 MB:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-340">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="e0cb2-341">Converter Olá disco raw tooa tamanho fixo VHD:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-341">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd

### <a name="prepare-a-rhel-7-virtual-machine-from-vmware"></a><span data-ttu-id="e0cb2-342">Preparar uma máquina virtual RHEL 7 do VMware</span><span class="sxs-lookup"><span data-stu-id="e0cb2-342">Prepare a RHEL 7 virtual machine from VMware</span></span>
1. <span data-ttu-id="e0cb2-343">Criar ou editar Olá `/etc/sysconfig/network` de arquivo e, em seguida, adicione Olá texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-343">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

2. <span data-ttu-id="e0cb2-344">Criar ou editar Olá `/etc/sysconfig/network-scripts/ifcfg-eth0` de arquivo e, em seguida, adicione Olá texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-344">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

3. <span data-ttu-id="e0cb2-345">Certifique-se de que o serviço de rede Olá iniciará no momento da inicialização executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-345">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

4. <span data-ttu-id="e0cb2-346">Registre a instalação de saudação Red Hat assinatura tooenable de pacotes do repositório do RHEL Olá executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-346">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

5. <span data-ttu-id="e0cb2-347">Modificar a linha de inicialização de kernel de saudação em seus parâmetros de kernel adicionais tooinclude grub configuração do Azure.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-347">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="e0cb2-348">toodo essa modificação, abra `/etc/default/grub` em um editor de texto e edição Olá `GRUB_CMDLINE_LINUX` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-348">toodo this modification, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="e0cb2-349">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-349">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="e0cb2-350">Essa configuração também garante que todas as mensagens de console são enviadas toohello primeira porta serial, que pode ajudá-lo Azure suporte à depuração de problemas.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-350">This configuration also ensures that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="e0cb2-351">Ela também desativa novas convenções de nomenclatura RHEL 7 Olá para as NICs.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-351">It also turns off hello new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="e0cb2-352">Além disso, recomendamos que você remova Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-352">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="e0cb2-353">Inicialização gráfica e silenciosa não são úteis em um ambiente de nuvem onde queremos que todos os toobe de logs de saudação enviada toohello de porta serial.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-353">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="e0cb2-354">Você pode deixar Olá `crashkernel` opção de configuração, se desejado.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-354">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="e0cb2-355">Observe que esse parâmetro reduz a quantidade de saudação de memória disponível na máquina virtual Olá 128 MB ou mais, que pode ser problemático em tamanhos menores de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-355">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

6. <span data-ttu-id="e0cb2-356">Depois de terminar edição `/etc/default/grub`, execute hello toorebuild Olá grub configuração dos comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-356">After you are done editing `/etc/default/grub`, run hello following command toorebuild hello grub configuration:</span></span>

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

7. <span data-ttu-id="e0cb2-357">Adicione tooinitramfs de módulos do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-357">Add Hyper-V modules tooinitramfs.</span></span>

    <span data-ttu-id="e0cb2-358">Edite `/etc/dracut.conf`e adicione o conteúdo:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-358">Edit `/etc/dracut.conf`, add content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="e0cb2-359">Recrie initramfs:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-359">Rebuild initramfs:</span></span>

        # dracut -f -v

8. <span data-ttu-id="e0cb2-360">Certifique-se de servidor SSH hello está instalado e configurado toostart no momento da inicialização.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-360">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span> <span data-ttu-id="e0cb2-361">Essa configuração é geralmente padrão hello.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-361">This setting is usually hello default.</span></span> <span data-ttu-id="e0cb2-362">Modificar `/etc/ssh/sshd_config` tooinclude Olá seguinte linha:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-362">Modify `/etc/ssh/sshd_config` tooinclude hello following line:</span></span>

        ClientAliveInterval 180

9. <span data-ttu-id="e0cb2-363">pacote de WALinuxAgent Hello, `WALinuxAgent-<version>`, foi introduzido repositório do toohello Red Hat extras.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-363">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="e0cb2-364">Habilite o repositório de extras Olá executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-364">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

10. <span data-ttu-id="e0cb2-365">Instale Olá agente Linux do Azure executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-365">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

11. <span data-ttu-id="e0cb2-366">Não crie espaço de permuta no disco do sistema operacional hello.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-366">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="e0cb2-367">Olá agente Linux do Azure pode configurar automaticamente o espaço de permuta usando Olá disco de recurso local que é anexado toohello máquina de virtual depois de máquina virtual de saudação é provisionada no Azure.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-367">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="e0cb2-368">Observe que hello, disco de recurso local é um disco temporário, e pode ser esvaziada quando a máquina virtual de saudação desprovisionada.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-368">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="e0cb2-369">Depois de instalar o hello Azure Linux Agent na etapa anterior Olá, modificar Olá parâmetros a seguir `/etc/waagent.conf` adequadamente:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-369">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

12. <span data-ttu-id="e0cb2-370">Se desejar que a assinatura de saudação toounregister, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-370">If you want toounregister hello subscription, run hello following command:</span></span>

        # sudo subscription-manager unregister

13. <span data-ttu-id="e0cb2-371">Execute Olá seguindo a máquina virtual do comandos toodeprovision hello e prepará-la para provisionamento no Azure:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-371">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

14. <span data-ttu-id="e0cb2-372">Desligar a máquina virtual de saudação e converter o formato de VHD do hello VMDK arquivo toohello.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-372">Shut down hello virtual machine, and convert hello VMDK file toohello VHD format.</span></span>

    <span data-ttu-id="e0cb2-373">Primeiro converter o formato de tooraw Olá imagem:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-373">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f vmdk -O raw rhel-7.3.vmdk rhel-7.3.raw

    <span data-ttu-id="e0cb2-374">Certifique-se de que tamanho Olá da imagem brutos hello está alinhado com 1 MB.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-374">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="e0cb2-375">Caso contrário, arredonde Olá tamanho tooalign com 1 MB:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-375">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="e0cb2-376">Converter Olá disco raw tooa tamanho fixo VHD:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-376">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-an-iso-by-using-a-kickstart-file-automatically"></a><span data-ttu-id="e0cb2-377">Preparar uma máquina virtual baseada em Red Hat de um arquivo ISO, usando um arquivo de início rápido automaticamente</span><span class="sxs-lookup"><span data-stu-id="e0cb2-377">Prepare a Red Hat-based virtual machine from an ISO by using a kickstart file automatically</span></span>
### <a name="prepare-a-rhel-7-virtual-machine-from-a-kickstart-file"></a><span data-ttu-id="e0cb2-378">Preparar uma máquina virtual RHEL 7 de um arquivo de início rápido</span><span class="sxs-lookup"><span data-stu-id="e0cb2-378">Prepare a RHEL 7 virtual machine from a kickstart file</span></span>

1.  <span data-ttu-id="e0cb2-379">Criar um arquivo de início rápido que inclui Olá conteúdo a seguir e salve o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-379">Create a kickstart file that includes hello following content, and save hello file.</span></span> <span data-ttu-id="e0cb2-380">Para obter detalhes sobre a instalação de início rápido, consulte Olá [guia de instalação de início rápido](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).</span><span class="sxs-lookup"><span data-stu-id="e0cb2-380">For details about kickstart installation, see hello [Kickstart Installation Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).</span></span>

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

2. <span data-ttu-id="e0cb2-381">Arquivo de início rápido de saudação local em que o sistema de instalação Olá pode acessá-lo.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-381">Place hello kickstart file where hello installation system can access it.</span></span>

3. <span data-ttu-id="e0cb2-382">Crie uma nova máquina virtual no Gerenciador do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-382">In Hyper-V Manager, create a new virtual machine.</span></span> <span data-ttu-id="e0cb2-383">Em Olá **conectar disco rígido Virtual** página, selecione **anexar um disco rígido virtual mais tarde**e hello concluir assistente de nova máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-383">On hello **Connect Virtual Hard Disk** page, select **Attach a virtual hard disk later**, and complete hello New Virtual Machine Wizard.</span></span>

4. <span data-ttu-id="e0cb2-384">Abra as configurações de máquina virtual de saudação:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-384">Open hello virtual machine settings:</span></span>

    <span data-ttu-id="e0cb2-385">a.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-385">a.</span></span>  <span data-ttu-id="e0cb2-386">Anexe uma nova máquina virtual de toohello disco rígido virtual.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-386">Attach a new virtual hard disk toohello virtual machine.</span></span> <span data-ttu-id="e0cb2-387">Certifique-se de que tooselect **formato VHD** e **tamanho fixo**.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-387">Make sure tooselect **VHD Format** and **Fixed Size**.</span></span>

    <span data-ttu-id="e0cb2-388">b.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-388">b.</span></span>  <span data-ttu-id="e0cb2-389">Anexe instalação Olá unidade de DVD toohello ISO.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-389">Attach hello installation ISO toohello DVD drive.</span></span>

    <span data-ttu-id="e0cb2-390">c.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-390">c.</span></span>  <span data-ttu-id="e0cb2-391">Olá BIOS tooboot do conjunto de CD.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-391">Set hello BIOS tooboot from CD.</span></span>

5. <span data-ttu-id="e0cb2-392">Inicie a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-392">Start hello virtual machine.</span></span> <span data-ttu-id="e0cb2-393">Guia de instalação do hello, pressione **guia** tooconfigure opções de inicialização de saudação.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-393">When hello installation guide appears, press **Tab** tooconfigure hello boot options.</span></span>

6. <span data-ttu-id="e0cb2-394">Insira `inst.ks=<hello location of hello kickstart file>` final Olá das opções de inicialização de Olá e pressione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-394">Enter `inst.ks=<hello location of hello kickstart file>` at hello end of hello boot options, and press **Enter**.</span></span>

7. <span data-ttu-id="e0cb2-395">Aguarde Olá toofinish de instalação.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-395">Wait for hello installation toofinish.</span></span> <span data-ttu-id="e0cb2-396">Quando ele for concluído, máquina virtual de saudação será desligada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-396">When it's finished, hello virtual machine will be shut down automatically.</span></span> <span data-ttu-id="e0cb2-397">O VHD Linux está agora pronto toobe carregado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-397">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="known-issues"></a><span data-ttu-id="e0cb2-398">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="e0cb2-398">Known issues</span></span>
### <a name="hello-hyper-v-driver-could-not-be-included-in-hello-initial-ram-disk-when-using-a-non-hyper-v-hypervisor"></a><span data-ttu-id="e0cb2-399">Olá Hyper-V driver não pode ser incluído no disco de RAM saudação inicial ao usar um hipervisor não Hyper-V</span><span class="sxs-lookup"><span data-stu-id="e0cb2-399">hello Hyper-V driver could not be included in hello initial RAM disk when using a non-Hyper-V hypervisor</span></span>

<span data-ttu-id="e0cb2-400">Em alguns casos, instaladores Linux podem não incluir drivers de saudação do Hyper-V no disco de RAM inicial hello (initrd ou initramfs), a menos que Linux detecta que está sendo executado em um ambiente Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-400">In some cases, Linux installers might not include hello drivers for Hyper-V in hello initial RAM disk (initrd or initramfs) unless Linux detects that it is running in a Hyper-V environment.</span></span>

<span data-ttu-id="e0cb2-401">Quando você estiver usando um tooprepare do sistema (ou seja, Virtualbox, Xen, etc.) de virtualização diferente em sua imagem do Linux, talvez seja necessário toorebuild initrd tooensure que pelo menos Olá hv_vmbus e módulos de kernel hv_storvsc estão disponíveis no disco de RAM saudação inicial.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-401">When you're using a different virtualization system (that is, Virtualbox, Xen, etc.) tooprepare your Linux image, you might need toorebuild initrd tooensure that at least hello hv_vmbus and hv_storvsc kernel modules are available on hello initial RAM disk.</span></span> <span data-ttu-id="e0cb2-402">Isso é um problema conhecido pelo menos em sistemas baseados em distribuição de Red Hat upstream hello.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-402">This is a known issue at least on systems that are based on hello upstream Red Hat distribution.</span></span>

<span data-ttu-id="e0cb2-403">tooresolve esse problema, adicione tooinitramfs de módulos do Hyper-V e recriá-lo:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-403">tooresolve this issue, add Hyper-V modules tooinitramfs and rebuild it:</span></span>

<span data-ttu-id="e0cb2-404">Editar `/etc/dracut.conf`e adicione Olá conteúdo a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-404">Edit `/etc/dracut.conf`, and add hello following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

<span data-ttu-id="e0cb2-405">Recrie initramfs:</span><span class="sxs-lookup"><span data-stu-id="e0cb2-405">Rebuild initramfs:</span></span>

        # dracut -f -v

<span data-ttu-id="e0cb2-406">Para obter mais detalhes, consulte as informações de saudação sobre [recriação initramfs](https://access.redhat.com/solutions/1958).</span><span class="sxs-lookup"><span data-stu-id="e0cb2-406">For more details, see hello information about [rebuilding initramfs](https://access.redhat.com/solutions/1958).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0cb2-407">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e0cb2-407">Next steps</span></span>
<span data-ttu-id="e0cb2-408">Você está agora pronto toouse as Red Hat Enterprise Linux disco rígido virtual toocreate novas máquinas virtuais no Azure.</span><span class="sxs-lookup"><span data-stu-id="e0cb2-408">You're now ready toouse your Red Hat Enterprise Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="e0cb2-409">Se isso for Olá primeira vez que você está carregando tooAzure de arquivo. vhd hello, consulte as etapas 2 e 3 em [criando e carregando um disco rígido virtual que contém o sistema de operacional Linux Olá](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e0cb2-409">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="e0cb2-410">Para obter mais detalhes sobre os hipervisores Olá que são certificadas toorun Red Hat Enterprise Linux, consulte [site do Red Hat Olá](https://access.redhat.com/certified-hypervisors).</span><span class="sxs-lookup"><span data-stu-id="e0cb2-410">For more details about hello hypervisors that are certified toorun Red Hat Enterprise Linux, see [hello Red Hat website](https://access.redhat.com/certified-hypervisors).</span></span>
