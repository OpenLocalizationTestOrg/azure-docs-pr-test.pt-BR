---
title: "aaaConfigure LVM em uma máquina virtual executando o Linux | Microsoft Docs"
description: Saiba como tooconfigure LVM no Linux no Azure.
services: virtual-machines-linux
documentationcenter: na
author: szarkos
manager: timlt
editor: tysonn
tag: azure-service-management,azure-resource-manager
ms.assetid: 7f533725-1484-479d-9472-6b3098d0aecc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 8daf792d87c6bb3d91a2eddcd01cfab34fd28cff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-lvm-on-a-linux-vm-in-azure"></a><span data-ttu-id="41488-103">Configurar o LVM em uma VM Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="41488-103">Configure LVM on a Linux VM in Azure</span></span>
<span data-ttu-id="41488-104">Este documento descreverá como tooconfigure Gerenciador de Volume lógico (LVM) em sua máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="41488-104">This document will discuss how tooconfigure Logical Volume Manager (LVM) in your Azure virtual machine.</span></span> <span data-ttu-id="41488-105">Embora seja possível tooconfigure que LVM em qualquer disco anexado máquina virtual de toohello, por padrão nuvem a maioria das imagens não terá LVM configurado no hello disco do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="41488-105">While it is feasible tooconfigure LVM on any disk attached toohello virtual machine, by default most cloud images will not have LVM configured on hello OS disk.</span></span> <span data-ttu-id="41488-106">Isso é tooprevent problemas com grupos de volumes duplicados se Olá disco do sistema operacional já está anexado tooanother VM de saudação mesmo distribuição e o tipo, por exemplo, durante um cenário de recuperação.</span><span class="sxs-lookup"><span data-stu-id="41488-106">This is tooprevent problems with duplicate volume groups if hello OS disk is ever attached tooanother VM of hello same distribution and type, i.e. during a recovery scenario.</span></span> <span data-ttu-id="41488-107">Portanto, é recomendável somente toouse LVM em discos de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="41488-107">Therefore it is recommended only toouse LVM on hello data disks.</span></span>

## <a name="linear-vs-striped-logical-volumes"></a><span data-ttu-id="41488-108">Volumes lógicos lineares versus lógicos distribuídos</span><span class="sxs-lookup"><span data-stu-id="41488-108">Linear vs. striped logical volumes</span></span>
<span data-ttu-id="41488-109">LVM pode ser usado toocombine um número de discos físicos em um único volume de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="41488-109">LVM can be used toocombine a number of physical disks into a single storage volume.</span></span> <span data-ttu-id="41488-110">Por padrão LVM geralmente cria volumes lógicos lineares, o que significa que armazenamento físico de saudação é concatenado.</span><span class="sxs-lookup"><span data-stu-id="41488-110">By default LVM will usually create linear logical volumes, which means that hello physical storage is concatenated together.</span></span> <span data-ttu-id="41488-111">Nesse caso as operações de leitura/gravação normalmente só funcionará tooa único disco.</span><span class="sxs-lookup"><span data-stu-id="41488-111">In this case read/write operations will typically only be sent tooa single disk.</span></span> <span data-ttu-id="41488-112">Em contrapartida, também podemos criar volumes lógicos distribuídos onde leituras e gravações estão distribuídas toomultiple discos contidos no grupo de volumes hello (ou seja, tooRAID0 semelhante).</span><span class="sxs-lookup"><span data-stu-id="41488-112">In contrast, we can also create striped logical volumes where reads and writes are distributed toomultiple disks contained in hello volume group (i.e. similar tooRAID0).</span></span> <span data-ttu-id="41488-113">Por motivos de desempenho, é provável que você desejará toostripe seus volumes lógicos para que as leituras e gravações utilizam todos os discos de dados anexado.</span><span class="sxs-lookup"><span data-stu-id="41488-113">For performance reasons it is likely you will want toostripe your logical volumes so that reads and writes utilize all your attached data disks.</span></span>

<span data-ttu-id="41488-114">Este documento descrevem como toocombine vários discos de dados em um único grupo de volumes e, em seguida, criar um volume lógico distribuído.</span><span class="sxs-lookup"><span data-stu-id="41488-114">This document will describe how toocombine several data disks into a single volume group, and then create a striped logical volume.</span></span> <span data-ttu-id="41488-115">Olá etapas a seguir são um pouco generalizado toowork com a maioria das distribuições.</span><span class="sxs-lookup"><span data-stu-id="41488-115">hello steps below are somewhat generalized toowork with most distributions.</span></span> <span data-ttu-id="41488-116">Na saudação de casos a maioria dos utilitários e fluxos de trabalho para gerenciar LVM no Azure não são fundamentalmente diferentes de outros ambientes.</span><span class="sxs-lookup"><span data-stu-id="41488-116">In most cases hello utilities and workflows for managing LVM on Azure are not fundamentally different than other environments.</span></span> <span data-ttu-id="41488-117">Como de costume, também consulte o fornecedor do Linux para obter documentação e práticas recomendadas para usar o LVM com sua distribuição específica.</span><span class="sxs-lookup"><span data-stu-id="41488-117">As usual, please also consult your Linux vendor for documentation and best practices for using LVM with your particular distribution.</span></span>

## <a name="attaching-data-disks"></a><span data-ttu-id="41488-118">Anexando discos de dados</span><span class="sxs-lookup"><span data-stu-id="41488-118">Attaching data disks</span></span>
<span data-ttu-id="41488-119">Um geralmente desejará toostart com dois ou mais discos de dados vazios ao usar LVM.</span><span class="sxs-lookup"><span data-stu-id="41488-119">One will usually want toostart with two or more empty data disks when using LVM.</span></span> <span data-ttu-id="41488-120">Com base em suas necessidades de e/s, você pode escolher tooattach discos que são armazenados em nosso armazenamento padrão, com a e/s too500/ps por armazenamento em disco ou nosso Premium com a e/s too5000/ps por disco.</span><span class="sxs-lookup"><span data-stu-id="41488-120">Based on your IO needs, you can choose tooattach disks that are stored in our Standard Storage, with up too500 IO/ps per disk or our Premium storage with up too5000 IO/ps per disk.</span></span> <span data-ttu-id="41488-121">Este artigo não entra em detalhes sobre como tooprovision e anexar a máquina de virtual do Linux de tooa de discos de dados.</span><span class="sxs-lookup"><span data-stu-id="41488-121">This article will not go into detail on how tooprovision and attach data disks tooa Linux virtual machine.</span></span> <span data-ttu-id="41488-122">Consulte artigo do Microsoft Azure Olá [anexar um disco](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obter instruções detalhadas sobre como tooattach um dados vazios disco tooa máquina de virtual do Linux no Azure.</span><span class="sxs-lookup"><span data-stu-id="41488-122">Please see hello Microsoft Azure article [attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for detailed instructions on how tooattach an empty data disk tooa Linux virtual machine on Azure.</span></span>

## <a name="install-hello-lvm-utilities"></a><span data-ttu-id="41488-123">Instalar utilitários LVM Olá</span><span class="sxs-lookup"><span data-stu-id="41488-123">Install hello LVM utilities</span></span>
* <span data-ttu-id="41488-124">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="41488-124">**Ubuntu**</span></span>

    ```bash  
    sudo apt-get update
    sudo apt-get install lvm2
    ```

* <span data-ttu-id="41488-125">**RHEL, CentOS e Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="41488-125">**RHEL, CentOS & Oracle Linux**</span></span>

    ```bash   
    sudo yum install lvm2
    ```

* <span data-ttu-id="41488-126">**SLES 12 e openSUSE**</span><span class="sxs-lookup"><span data-stu-id="41488-126">**SLES 12 and openSUSE**</span></span>

    ```bash   
    sudo zypper install lvm2
    ```

* <span data-ttu-id="41488-127">**SLES 11**</span><span class="sxs-lookup"><span data-stu-id="41488-127">**SLES 11**</span></span>

    ```bash   
    sudo zypper install lvm2
    ```

    <span data-ttu-id="41488-128">Em SLES11 também será necessário editar `/etc/sysconfig/lvm` e defina `LVM_ACTIVATED_ON_DISCOVERED` muito "Habilitar":</span><span class="sxs-lookup"><span data-stu-id="41488-128">On SLES11 you must also edit `/etc/sysconfig/lvm` and set `LVM_ACTIVATED_ON_DISCOVERED` too"enable":</span></span>

    ```sh   
    LVM_ACTIVATED_ON_DISCOVERED="enable" 
    ```

## <a name="configure-lvm"></a><span data-ttu-id="41488-129">Configurar o LVM</span><span class="sxs-lookup"><span data-stu-id="41488-129">Configure LVM</span></span>
<span data-ttu-id="41488-130">Este guia assumiremos você anexou três discos de dados, vamos analisar tooas `/dev/sdc`, `/dev/sdd` e `/dev/sde`.</span><span class="sxs-lookup"><span data-stu-id="41488-130">In this guide we will assume you have attached three data disks, which we'll refer tooas `/dev/sdc`, `/dev/sdd` and `/dev/sde`.</span></span> <span data-ttu-id="41488-131">Observe que não podem ser sempre Olá mesmos nomes de caminho na sua VM.</span><span class="sxs-lookup"><span data-stu-id="41488-131">Note that these may not always be hello same path names in your VM.</span></span> <span data-ttu-id="41488-132">Você pode executar o '`sudo fdisk -l`' ou toolist semelhante do comando os discos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="41488-132">You can run '`sudo fdisk -l`' or similar command toolist your available disks.</span></span>

1. <span data-ttu-id="41488-133">Prepare volumes físicos hello:</span><span class="sxs-lookup"><span data-stu-id="41488-133">Prepare hello physical volumes:</span></span>

    ```bash    
    sudo pvcreate /dev/sd[cde]
    Physical volume "/dev/sdc" successfully created
    Physical volume "/dev/sdd" successfully created
    Physical volume "/dev/sde" successfully created
    ```

2. <span data-ttu-id="41488-134">Crie um grupo de volumes.</span><span class="sxs-lookup"><span data-stu-id="41488-134">Create a volume group.</span></span> <span data-ttu-id="41488-135">Neste exemplo estamos ligando para o grupo de volumes Olá `data-vg01`:</span><span class="sxs-lookup"><span data-stu-id="41488-135">In this example we are calling hello volume group `data-vg01`:</span></span>

    ```bash    
    sudo vgcreate data-vg01 /dev/sd[cde]
    Volume group "data-vg01" successfully created
    ```

3. <span data-ttu-id="41488-136">Crie volumes lógicos de saudação.</span><span class="sxs-lookup"><span data-stu-id="41488-136">Create hello logical volume(s).</span></span> <span data-ttu-id="41488-137">Olá comando abaixo, criará um único volume lógico chamado `data-lv01` toospan Olá todo o grupo de volumes, mas observe que também é possível toocreate vários volumes lógicos em um grupo de volumes de saudação.</span><span class="sxs-lookup"><span data-stu-id="41488-137">hello command below we will create a single logical volume called `data-lv01` toospan hello entire volume group, but note that it is also feasible toocreate multiple logical volumes in hello volume group.</span></span>

    ```bash   
    sudo lvcreate --extents 100%FREE --stripes 3 --name data-lv01 data-vg01
    Logical volume "data-lv01" created.
    ```

4. <span data-ttu-id="41488-138">Formatar o volume lógico da saudação</span><span class="sxs-lookup"><span data-stu-id="41488-138">Format hello logical volume</span></span>

    ```bash  
    sudo mkfs -t ext4 /dev/data-vg01/data-lv01
    ```
   
   > [!NOTE]
   > <span data-ttu-id="41488-139">Com o SLES11, use `-t ext3` em vez de ext4.</span><span class="sxs-lookup"><span data-stu-id="41488-139">With SLES11 use `-t ext3` instead of ext4.</span></span> <span data-ttu-id="41488-140">SLES11 só oferece suporte a sistemas de arquivos de tooext4 acesso somente leitura.</span><span class="sxs-lookup"><span data-stu-id="41488-140">SLES11 only supports read-only access tooext4 filesystems.</span></span>

## <a name="add-hello-new-file-system-tooetcfstab"></a><span data-ttu-id="41488-141">Adicionar Olá novo arquivo sistema muito/etc/fstab</span><span class="sxs-lookup"><span data-stu-id="41488-141">Add hello new file system too/etc/fstab</span></span>
> [!IMPORTANT]
> <span data-ttu-id="41488-142">Edição incorretamente Olá `/etc/fstab` arquivo pode resultar em um sistema não inicializável.</span><span class="sxs-lookup"><span data-stu-id="41488-142">Improperly editing hello `/etc/fstab` file could result in an unbootable system.</span></span> <span data-ttu-id="41488-143">Se não tiver certeza, consulte a documentação da distribuição toohello para obter informações sobre como tooproperly editar esse arquivo.</span><span class="sxs-lookup"><span data-stu-id="41488-143">If unsure, please refer toohello distribution's documentation for information on how tooproperly edit this file.</span></span> <span data-ttu-id="41488-144">Também é recomendável que um backup de saudação `/etc/fstab` arquivo é criado antes de editar.</span><span class="sxs-lookup"><span data-stu-id="41488-144">It is also recommended that a backup of hello `/etc/fstab` file is created before editing.</span></span>

1. <span data-ttu-id="41488-145">Crie ponto de montagem de saudação desejado para o novo sistema de arquivos, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="41488-145">Create hello desired mount point for your new file system, for example:</span></span>

    ```bash  
    sudo mkdir /data
    ```

2. <span data-ttu-id="41488-146">Localize o caminho do volume lógico Olá</span><span class="sxs-lookup"><span data-stu-id="41488-146">Locate hello logical volume path</span></span>

    ```bash    
    lvdisplay
    --- Logical volume ---
    LV Path                /dev/data-vg01/data-lv01
    ....
    ```

3. <span data-ttu-id="41488-147">Abra `/etc/fstab` em um editor de texto e adicione uma entrada para o novo sistema de arquivos hello, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="41488-147">Open `/etc/fstab` in a text editor and add an entry for hello new file system, for example:</span></span>

    ```bash    
    /dev/data-vg01/data-lv01  /data  ext4  defaults  0  2
    ```   
    <span data-ttu-id="41488-148">Em seguida, salve e feche o `/etc/fstab`.</span><span class="sxs-lookup"><span data-stu-id="41488-148">Then, save and close `/etc/fstab`.</span></span>

4. <span data-ttu-id="41488-149">Testar esse Olá `/etc/fstab` entrada está correta:</span><span class="sxs-lookup"><span data-stu-id="41488-149">Test that hello `/etc/fstab` entry is correct:</span></span>

    ```bash    
    sudo mount -a
    ```

    <span data-ttu-id="41488-150">Se esse comando resulta em uma mensagem de erro, verifique a sintaxe Olá Olá `/etc/fstab` arquivo.</span><span class="sxs-lookup"><span data-stu-id="41488-150">If this command results in an error message please check hello syntax in hello `/etc/fstab` file.</span></span>
   
    <span data-ttu-id="41488-151">Em seguida execute Olá `mount` montado sistema de arquivos do comando tooensure hello:</span><span class="sxs-lookup"><span data-stu-id="41488-151">Next run hello `mount` command tooensure hello file system is mounted:</span></span>

    ```bash    
    mount
    ......
    /dev/mapper/data--vg01-data--lv01 on /data type ext4 (rw)
    ```

5. <span data-ttu-id="41488-152">(Opcional) Parâmetros de inicialização à prova de falhas em `/etc/fstab`</span><span class="sxs-lookup"><span data-stu-id="41488-152">(Optional) Failsafe boot parameters in `/etc/fstab`</span></span>
   
    <span data-ttu-id="41488-153">Muitas distribuições incluem qualquer Olá `nobootwait` ou `nofail` montar os parâmetros que podem ser adicionados toohello `/etc/fstab` arquivo.</span><span class="sxs-lookup"><span data-stu-id="41488-153">Many distributions include either hello `nobootwait` or `nofail` mount parameters that may be added toohello `/etc/fstab` file.</span></span> <span data-ttu-id="41488-154">Esses parâmetros permitem falhas ao montar um sistema de arquivos específico e permitem Olá Linux sistema toocontinue tooboot mesmo se ele for o sistema de arquivos do tooproperly não é possível montar Olá RAID.</span><span class="sxs-lookup"><span data-stu-id="41488-154">These parameters allow for failures when mounting a particular file system and allow hello Linux system toocontinue tooboot even if it is unable tooproperly mount hello RAID file system.</span></span> <span data-ttu-id="41488-155">Consulte a documentação da distribuição tooyour para obter mais informações sobre esses parâmetros.</span><span class="sxs-lookup"><span data-stu-id="41488-155">Please refer tooyour distribution's documentation for more information on these parameters.</span></span>
   
    <span data-ttu-id="41488-156">Exemplo (Ubuntu):</span><span class="sxs-lookup"><span data-stu-id="41488-156">Example (Ubuntu):</span></span>

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,nobootwait  0  2
    ```

## <a name="trimunmap-support"></a><span data-ttu-id="41488-157">Suporte a TRIM/UNMAP</span><span class="sxs-lookup"><span data-stu-id="41488-157">TRIM/UNMAP support</span></span>
<span data-ttu-id="41488-158">Suportam a alguns kernels Linux TRIM/DESMAPEAMENTO operações toodiscard blocos não usados no disco hello.</span><span class="sxs-lookup"><span data-stu-id="41488-158">Some Linux kernels support TRIM/UNMAP operations toodiscard unused blocks on hello disk.</span></span> <span data-ttu-id="41488-159">Essas operações são principalmente útil no armazenamento padrão tooinform Azure que páginas excluídas não são mais válidas e podem ser descartadas.</span><span class="sxs-lookup"><span data-stu-id="41488-159">These operations are primarily useful in standard storage tooinform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="41488-160">Descartar páginas poderá representar uma economia de dinheiro se você criar arquivos grandes e, em seguida, excluí-los.</span><span class="sxs-lookup"><span data-stu-id="41488-160">Discarding pages can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="41488-161">Há duas maneiras tooenable TRIM suporte em sua VM do Linux.</span><span class="sxs-lookup"><span data-stu-id="41488-161">There are two ways tooenable TRIM support in your Linux VM.</span></span> <span data-ttu-id="41488-162">Como de costume, consulte a distribuição para Olá abordagem recomendada:</span><span class="sxs-lookup"><span data-stu-id="41488-162">As usual, consult your distribution for hello recommended approach:</span></span>

- <span data-ttu-id="41488-163">Saudação de uso `discard` montar opção `/etc/fstab`, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="41488-163">Use hello `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,discard  0  2
    ```

- <span data-ttu-id="41488-164">Em alguns Olá casos `discard` opção pode ter implicações de desempenho.</span><span class="sxs-lookup"><span data-stu-id="41488-164">In some cases hello `discard` option may have performance implications.</span></span> <span data-ttu-id="41488-165">Como alternativa, você pode executar Olá `fstrim` comando manualmente da linha de comando hello, ou adicionar tooyour crontab toorun regularmente:</span><span class="sxs-lookup"><span data-stu-id="41488-165">Alternatively, you can run hello `fstrim` command manually from hello command line, or add it tooyour crontab toorun regularly:</span></span>

    <span data-ttu-id="41488-166">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="41488-166">**Ubuntu**</span></span>

    ```bash 
    # sudo apt-get install util-linux
    # sudo fstrim /datadrive
    ```

    <span data-ttu-id="41488-167">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="41488-167">**RHEL/CentOS**</span></span>

    ```bash 
    # sudo yum install util-linux
    # sudo fstrim /datadrive
    ```
