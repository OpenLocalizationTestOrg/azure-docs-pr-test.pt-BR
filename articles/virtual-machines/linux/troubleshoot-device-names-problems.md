---
title: "os nomes de dispositivo VM aaaLinux são alterados no Azure | Microsoft Docs"
description: "Explica Olá por nomes de dispositivo são alterados e fornecem uma solução para esse problema."
services: virtual-machines-linux
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: 
ms.service: virtual-machines-linux
ms.topic: article
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.date: 07/12/2017
ms.author: genli
ms.openlocfilehash: 4d3a5853d61edd2c8e8b85ab69e5ed3b3bc00bb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-linux-vm-device-names-are-changed"></a><span data-ttu-id="81790-103">Solução de problemas: os nomes de dispositivo de VM do Linux são alterados</span><span class="sxs-lookup"><span data-stu-id="81790-103">Troubleshooting: Linux VM device names are changed</span></span>

<span data-ttu-id="81790-104">artigo Olá explica por que os nomes do dispositivo são alterados depois de reiniciar uma máquina virtual do Linux (VM), ou anexar novamente os discos de saudação.</span><span class="sxs-lookup"><span data-stu-id="81790-104">hello article explains why device names are changed after you restart a Linux virtual machine (VM), or reattach hello disks.</span></span> <span data-ttu-id="81790-105">Ele também fornece uma solução de saudação para esse problema.</span><span class="sxs-lookup"><span data-stu-id="81790-105">It also provides hello solution for this problem.</span></span>

## <a name="symptom"></a><span data-ttu-id="81790-106">Sintoma</span><span class="sxs-lookup"><span data-stu-id="81790-106">Symptom</span></span>

<span data-ttu-id="81790-107">Você pode enfrentar Olá os problemas a seguir ao executar VMs do Linux no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="81790-107">You may experience hello following problems when running Linux VMs in Microsoft Azure.</span></span>

- <span data-ttu-id="81790-108">Olá VM falha tooboot após uma reinicialização.</span><span class="sxs-lookup"><span data-stu-id="81790-108">hello VM fails tooboot after a restart.</span></span>

- <span data-ttu-id="81790-109">Se os discos de dados for desanexados e reanexados, nomes de dispositivos de saudação para discos são alterados.</span><span class="sxs-lookup"><span data-stu-id="81790-109">If data disks are detached and reattached, hello devices names for disks are changed.</span></span>

- <span data-ttu-id="81790-110">Um aplicativo ou script que faz referência a um disco usando o nome do dispositivo falha.</span><span class="sxs-lookup"><span data-stu-id="81790-110">An application or script that references a disk by using device name fails.</span></span> <span data-ttu-id="81790-111">Localizar esse Olá nome do dispositivo de disco de saudação é alterado.</span><span class="sxs-lookup"><span data-stu-id="81790-111">You find that hello device name of hello disk is changed.</span></span>

## <a name="cause"></a><span data-ttu-id="81790-112">Causa</span><span class="sxs-lookup"><span data-stu-id="81790-112">Cause</span></span>

<span data-ttu-id="81790-113">Caminhos de dispositivo no Linux não há garantia toobe consistente entre as reinicializações.</span><span class="sxs-lookup"><span data-stu-id="81790-113">Device paths in Linux are not guaranteed toobe consistent across restarts.</span></span> <span data-ttu-id="81790-114">Nomes de dispositivo consistem em números principais (letra) e secundários.</span><span class="sxs-lookup"><span data-stu-id="81790-114">Device names consist of major (letter) and minor numbers.</span></span>  <span data-ttu-id="81790-115">Quando o driver de dispositivo de armazenamento de Linux Olá detecta um novo dispositivo, ele atribui tooit de números de dispositivo principais e secundárias do intervalo de saudação disponíveis.</span><span class="sxs-lookup"><span data-stu-id="81790-115">When hello Linux storage device driver detects a new device, it assigns major and minor device numbers tooit from hello available range.</span></span> <span data-ttu-id="81790-116">Quando um dispositivo é removido, números de saudação do dispositivo são liberada toobe reutilizado posteriormente.</span><span class="sxs-lookup"><span data-stu-id="81790-116">When a device is removed, hello device numbers are freed toobe reused later.</span></span>

<span data-ttu-id="81790-117">Olá problema ocorre porque hello dispositivo varredura no Linux agendada pelo subsistema de SCSI Olá ocorre de maneira assíncrona.</span><span class="sxs-lookup"><span data-stu-id="81790-117">hello problem occurs because hello device scanning in Linux scheduled by hello SCSI subsystem happens asynchronously.</span></span> <span data-ttu-id="81790-118">nomes de caminho de dispositivo final Olá podem variar entre as reinicializações.</span><span class="sxs-lookup"><span data-stu-id="81790-118">hello final device path naming may vary across restarts.</span></span> 

## <a name="solution"></a><span data-ttu-id="81790-119">Solução</span><span class="sxs-lookup"><span data-stu-id="81790-119">Solution</span></span>

<span data-ttu-id="81790-120">tooresolve esse problema, use a nomenclatura persistente.</span><span class="sxs-lookup"><span data-stu-id="81790-120">tooresolve this problem, use persistent naming.</span></span> <span data-ttu-id="81790-121">Há quatro toopersistent de métodos de nomenclatura - por rótulo de sistema de arquivos, uuid, por id e pelo caminho.</span><span class="sxs-lookup"><span data-stu-id="81790-121">There are four methods toopersistent naming - by filesystem label, by uuid, by id and by path.</span></span> <span data-ttu-id="81790-122">É recomendável o rótulo do sistema de arquivos de saudação e métodos UUID para VMs do Linux do Azure.</span><span class="sxs-lookup"><span data-stu-id="81790-122">We recommend hello filesystem label and UUID methods for Azure Linux VMs.</span></span> 

<span data-ttu-id="81790-123">A maioria das distribuições também fornecem a saudação **nofail** ou **nobootwait** fstab opções.</span><span class="sxs-lookup"><span data-stu-id="81790-123">Most distributions also provide either hello **nofail** or **nobootwait** fstab options.</span></span> <span data-ttu-id="81790-124">Essas opções permitem tooboot um sistema, mesmo se o disco de saudação falhar toomount na inicialização.</span><span class="sxs-lookup"><span data-stu-id="81790-124">These options enable a system tooboot even if hello disk fails toomount at startup.</span></span> <span data-ttu-id="81790-125">Verifique a documentação da distribuição Olá para obter mais informações sobre esses parâmetros.</span><span class="sxs-lookup"><span data-stu-id="81790-125">Check hello distribution's documentation for more information about these parameters.</span></span> <span data-ttu-id="81790-126">Para obter mais informações sobre como tooconfigure toouse uma VM do Linux um UUID quando você adiciona um disco de dados, consulte [conectar toohello novo disco de VM do Linux toomount Olá](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="81790-126">For more information about how tooconfigure a Linux VM toouse a UUID when you add a data disk, see [Connect toohello Linux VM toomount hello new disk](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> 

<span data-ttu-id="81790-127">Quando hello Azure Linux é instalado em uma máquina virtual, ele usa Udev regras tooconstruct um conjunto de links simbólicos em **/dev/disk/azure**.</span><span class="sxs-lookup"><span data-stu-id="81790-127">When hello Azure Linux agent is installed on a VM, it uses Udev rules tooconstruct a set of symbolic links under **/dev/disk/azure**.</span></span> <span data-ttu-id="81790-128">Essas regras Udev podem ser usadas por aplicativos e discos de tooidentify scripts são anexado toohello VM, seu tipo, Olá LUN.</span><span class="sxs-lookup"><span data-stu-id="81790-128">These Udev rules can be used by applications and scripts tooidentify disks are attached toohello VM, their type, and hello LUN.</span></span>

## <a name="more-information"></a><span data-ttu-id="81790-129">Mais informações</span><span class="sxs-lookup"><span data-stu-id="81790-129">More information</span></span>

### <a name="identify-disk-luns"></a><span data-ttu-id="81790-130">Identificar LUNs de disco</span><span class="sxs-lookup"><span data-stu-id="81790-130">Identify disk LUNs</span></span>

<span data-ttu-id="81790-131">Um aplicativo pode usar LUNs toofind todos os discos de saudação anexado e criação de links simbólicos.</span><span class="sxs-lookup"><span data-stu-id="81790-131">An application can use LUNs toofind all hello attached disks and constructing symbolic links.</span></span> <span data-ttu-id="81790-132">agente do Linux Azure Olá agora inclui udev regras configuradas links simbólicos em dispositivos de toohello um LUN, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="81790-132">hello Azure Linux agent now includes udev rules that set up symbolic links from a LUN toohello devices, as follows:</span></span>

    $ tree /dev/disk/azure

    /dev/disk/azure
    ├── resource -> ../../sdb
    ├── resource-part1 -> ../../sdb1
    ├── root -> ../../sda
    ├── root-part1 -> ../../sda1
    └── scsi1
        ├── lun0 -> ../../../sdc
        ├── lun0-part1 -> ../../../sdc1
        ├── lun1 -> ../../../sdd
        ├── lun1-part1 -> ../../../sdd1
        ├── lun1-part2 -> ../../../sdd2
        └── lun1-part3 -> ../../../sdd3                                    
                                 

<span data-ttu-id="81790-133">Informações de LUN também podem ser recuperadas de convidado do Linux hello usando lsscsi ou uma ferramenta semelhante, da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="81790-133">LUN information can also be retrieved from hello Linux guest using lsscsi or similar tool as follows.</span></span>

       $ sudo lsscsi

      [1:0:0:0] cd/dvd Msft Virtual CD/ROM 1.0 /dev/sr0

      [2:0:0:0] disk Msft Virtual Disk 1.0 /dev/sda

      [3:0:1:0] disk Msft Virtual Disk 1.0 /dev/sdb

      [5:0:0:0] disk Msft Virtual Disk 1.0 /dev/sdc

      [5:0:0:1] disk Msft Virtual Disk 1.0 /dev/sdd

<span data-ttu-id="81790-134">Essas informações de LUN de convidado podem ser usadas com a assinatura do Azure metadados tooidentify Olá local no armazenamento do Azure de saudação VHD que armazena dados de partição de saudação.</span><span class="sxs-lookup"><span data-stu-id="81790-134">This guest LUN information can be used with Azure subscription metadata tooidentify hello location in Azure storage of hello VHD which stores hello partition data.</span></span> <span data-ttu-id="81790-135">Por exemplo, use Olá az cli:</span><span class="sxs-lookup"><span data-stu-id="81790-135">For example, use hello az cli:</span></span>

    $ az vm show --resource-group testVM --name testVM | jq -r .storageProfile.dataDisks                                        
    [                                                                                                                                                                  
    {                                                                                                                                                                  
    "caching": "None",                                                                                                                                              
      "createOption": "empty",                                                                                                                                         
    "diskSizeGb": 1023,                                                                                                                                             
      "image": null,                                                                                                                                                   
    "lun": 0,                                                                                                                                                        
    "managedDisk": null,                                                                                                                                             
    "name": "testVM-20170619-114353",                                                                                                                    
    "vhd": {                                                                                                                                                          
      "uri": "https://testVM.blob.core.windows.net/vhd/testVM-20170619-114353.vhd"                                                       
    }                                                                                                                                                              
    },                                                                                                                                                                
    {                                                                                                                                                                   
    "caching": "None",                                                                                                                                               
    "createOption": "empty",                                                                                                                                         
    "diskSizeGb": 512,                                                                                                                                              
    "image": null,                                                                                                                                                   
    "lun": 1,                                                                                                                                                        
    "managedDisk": null,                                                                                                                                             
    "name": "testVM-20170619-121516",                                                                                                                    
    "vhd": {                                                                                                                                                           
      "uri": "https://testVM.blob.core.windows.net/vhd/testVM-20170619-121516.vhd"                                                       
      }                                                                                                                                                             
      }                                                                                                                                                             
    ]

### <a name="discover-filesystem-uuids-by-using-blkid"></a><span data-ttu-id="81790-136">Descobrir UUIDs de sistema de arquivos usando o blkid</span><span class="sxs-lookup"><span data-stu-id="81790-136">Discover filesystem UUIDs by using blkid</span></span>

<span data-ttu-id="81790-137">Um script ou aplicativo pode ler a saída de saudação do blkid ou semelhantes fontes de informações e criar links simbólicos em **dev** para uso.</span><span class="sxs-lookup"><span data-stu-id="81790-137">A script or application can read hello output of blkid, or similar sources of information, and construct symbolic links in **/dev** for use.</span></span> <span data-ttu-id="81790-138">saída de Hello mostrará Olá UUIDs de todos os discos anexados toohello VM e hello dispositivo arquivo toowhich estão associadas:</span><span class="sxs-lookup"><span data-stu-id="81790-138">hello output will show hello UUIDs of all disks attached toohello VM and hello device file toowhich they are associated:</span></span>

    $ sudo blkid -s UUID

    /dev/sr0: UUID="120B021372645f72"
    /dev/sda1: UUID="52c6959b-79b0-4bdd-8ed6-71e0ba782fb4"
    /dev/sdb1: UUID="176250df-9c7c-436f-94e4-d13f9bdea744"
    /dev/sdc1: UUID="b0048738-4ecc-4837-9793-49ce296d2692"

<span data-ttu-id="81790-139">regras de udev waagent Olá construir um conjunto de links simbólicos em **/dev/disk/azure**:</span><span class="sxs-lookup"><span data-stu-id="81790-139">hello waagent udev rules construct a set of symbolic links under **/dev/disk/azure**:</span></span>


    $ ls -l /dev/disk/azure

    total 0
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 resource -> ../../sdb
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 resource-part1 -> ../../sdb1
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 root -> ../../sda
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 root-part1 -> ../../sda1


<span data-ttu-id="81790-140">aplicativo Hello pode usar essas informações identificar o dispositivo de disco de inicialização de saudação e disco de recurso (efêmero) hello.</span><span class="sxs-lookup"><span data-stu-id="81790-140">hello application can use this information identify hello boot disk device and hello resource (ephemeral) disk.</span></span> <span data-ttu-id="81790-141">No Azure, aplicativos devem consultar muito**/dev/disk/azure/root-part1** ou **/dev/disk/azure-resource-part1** toodiscover essas partições.</span><span class="sxs-lookup"><span data-stu-id="81790-141">In Azure, applications should refer too**/dev/disk/azure/root-part1** or **/dev/disk/azure-resource-part1** toodiscover these partitions.</span></span>

<span data-ttu-id="81790-142">Se não houver partições adicionais na lista de blkid hello, eles residem em um disco de dados.</span><span class="sxs-lookup"><span data-stu-id="81790-142">If there are additional partitions from hello blkid list, they reside on a data disk.</span></span> <span data-ttu-id="81790-143">Aplicativos podem manter Olá UUID para essas partições e use um caminho como Olá abaixo do nome de dispositivo de saudação toodiscover em tempo de execução:</span><span class="sxs-lookup"><span data-stu-id="81790-143">Applications can maintain hello UUID for these partitions and use a path like hello below toodiscover hello device name at runtime:</span></span>

    $ ls -l /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692

    lrwxrwxrwx 1 root root 10 Jun 19 15:57 /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692 -> ../../sdc1

    
### <a name="get-hello-latest-azure-storage-rules"></a><span data-ttu-id="81790-144">Obter regras de armazenamento do Azure mais recentes Olá</span><span class="sxs-lookup"><span data-stu-id="81790-144">Get hello latest Azure storage rules</span></span>

<span data-ttu-id="81790-145">toohello regras de armazenamento do Azure mais recentes, execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="81790-145">toohello latest Azure storage rules, run th following commands:</span></span>

    # sudo curl -o /etc/udev/rules.d/66-azure-storage.rules https://raw.githubusercontent.com/Azure/WALinuxAgent/master/config/66-azure-storage.rules
    # sudo udevadm trigger --subsystem-match=block


<span data-ttu-id="81790-146">Para obter mais informações, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="81790-146">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="81790-147">Ubuntu: usando UUID</span><span class="sxs-lookup"><span data-stu-id="81790-147">Ubuntu: Using UUID</span></span>](https://help.ubuntu.com/community/UsingUUID)

- [<span data-ttu-id="81790-148">Red Hat: nomenclatura persistente</span><span class="sxs-lookup"><span data-stu-id="81790-148">Red Hat: Persistent Naming</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/persistent_naming.html)

- [<span data-ttu-id="81790-149">Linux: o que UUIDs podem fazer por você</span><span class="sxs-lookup"><span data-stu-id="81790-149">Linux: What UUIDs can do for you</span></span>](https://www.linux.com/news/what-uuids-can-do-you)

- [<span data-ttu-id="81790-150">UDev: Introdução tooDevice gerenciamento no sistema de Linux modernos</span><span class="sxs-lookup"><span data-stu-id="81790-150">Udev: Introduction tooDevice Management In Modern Linux System</span></span>](https://www.linux.com/news/udev-introduction-device-management-modern-linux-system)

