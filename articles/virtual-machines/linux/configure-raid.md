---
title: "software aaaConfigure RAID em uma máquina virtual executando o Linux | Microsoft Docs"
description: Saiba como toouse mdadm tooconfigure RAID no Linux no Azure.
services: virtual-machines-linux
documentationcenter: na
author: rickstercdn
manager: timlt
editor: tysonn
tag: azure-service-management,azure-resource-manager
ms.assetid: f3cb2786-bda6-4d2c-9aaf-2db80f490feb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: rclaus
ms.openlocfilehash: f06e2679d953faf88ffee9991226cdb3cc1cbdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-software-raid-on-linux"></a><span data-ttu-id="7e125-103">Configurar RAID de software no Linux</span><span class="sxs-lookup"><span data-stu-id="7e125-103">Configure Software RAID on Linux</span></span>
<span data-ttu-id="7e125-104">É um software de toouse cenário comum RAID em máquinas virtuais Linux no Azure toopresent dados anexados vários discos como um único dispositivo RAID.</span><span class="sxs-lookup"><span data-stu-id="7e125-104">It's a common scenario toouse software RAID on Linux virtual machines in Azure toopresent multiple attached data disks as a single RAID device.</span></span> <span data-ttu-id="7e125-105">Normalmente isso pode ser usado tooimprove desempenho e permitir melhor taxa de transferência em comparação com toousing apenas um único disco.</span><span class="sxs-lookup"><span data-stu-id="7e125-105">Typically this can be used tooimprove performance and allow for improved throughput compared toousing just a single disk.</span></span>

## <a name="attaching-data-disks"></a><span data-ttu-id="7e125-106">Anexando discos de dados</span><span class="sxs-lookup"><span data-stu-id="7e125-106">Attaching data disks</span></span>
<span data-ttu-id="7e125-107">Dois ou mais discos de dados vazios são necessário tooconfigure um dispositivo RAID.</span><span class="sxs-lookup"><span data-stu-id="7e125-107">Two or more empty data disks are needed tooconfigure a RAID device.</span></span>  <span data-ttu-id="7e125-108">Olá principal motivo para a criação de um dispositivo RAID é tooimprove o desempenho do disco e/s.</span><span class="sxs-lookup"><span data-stu-id="7e125-108">hello primary reason for creating a RAID device is tooimprove performance of your disk IO.</span></span>  <span data-ttu-id="7e125-109">Com base em suas necessidades de e/s, você pode escolher tooattach discos que são armazenados em nosso armazenamento padrão, com a e/s too500/ps por armazenamento em disco ou nosso Premium com a e/s too5000/ps por disco.</span><span class="sxs-lookup"><span data-stu-id="7e125-109">Based on your IO needs, you can choose tooattach disks that are stored in our Standard Storage, with up too500 IO/ps per disk or our Premium storage with up too5000 IO/ps per disk.</span></span> <span data-ttu-id="7e125-110">Este artigo não entrar em detalhes sobre como tooprovision e anexar a máquina de virtual do Linux de tooa de discos de dados.</span><span class="sxs-lookup"><span data-stu-id="7e125-110">This article does not go into detail on how tooprovision and attach data disks tooa Linux virtual machine.</span></span>  <span data-ttu-id="7e125-111">Consulte o artigo do Microsoft Azure Olá [anexar um disco](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obter instruções detalhadas sobre como tooattach um dados vazios disco tooa máquina de virtual do Linux no Azure.</span><span class="sxs-lookup"><span data-stu-id="7e125-111">See hello Microsoft Azure article [attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for detailed instructions on how tooattach an empty data disk tooa Linux virtual machine on Azure.</span></span>

## <a name="install-hello-mdadm-utility"></a><span data-ttu-id="7e125-112">Instalar Olá mdadm utility</span><span class="sxs-lookup"><span data-stu-id="7e125-112">Install hello mdadm utility</span></span>
* <span data-ttu-id="7e125-113">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="7e125-113">**Ubuntu**</span></span>
```bash
sudo apt-get update
sudo apt-get install mdadm
```

* <span data-ttu-id="7e125-114">**CentOS & Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="7e125-114">**CentOS & Oracle Linux**</span></span>
```bash
sudo yum install mdadm
```

* <span data-ttu-id="7e125-115">**SLES e openSUSE**</span><span class="sxs-lookup"><span data-stu-id="7e125-115">**SLES and openSUSE**</span></span>
```bash  
zypper install mdadm
```

## <a name="create-hello-disk-partitions"></a><span data-ttu-id="7e125-116">Criar hello partições de disco</span><span class="sxs-lookup"><span data-stu-id="7e125-116">Create hello disk partitions</span></span>
<span data-ttu-id="7e125-117">Neste exemplo, criamos uma única partição de disco em /dev/sdc.</span><span class="sxs-lookup"><span data-stu-id="7e125-117">In this example, we create a single disk partition on /dev/sdc.</span></span> <span data-ttu-id="7e125-118">nova partição de disco Olá será chamada /dev/sdc1.</span><span class="sxs-lookup"><span data-stu-id="7e125-118">hello new disk partition will be called /dev/sdc1.</span></span>

1. <span data-ttu-id="7e125-119">Iniciar `fdisk` toobegin a criação de partições</span><span class="sxs-lookup"><span data-stu-id="7e125-119">Start `fdisk` toobegin creating partitions</span></span>

    ```bash
    sudo fdisk /dev/sdc
    Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
    Building a new DOS disklabel with disk identifier 0xa34cb70c.
    Changes will remain in memory only, until you decide toowrite them.
    After that, of course, hello previous content won't be recoverable.

    WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
                    switch off hello mode (command 'c') and change display units to
                    sectors (command 'u').
    ```

2. <span data-ttu-id="7e125-120">Pressione ' n' no toocreate prompt Olá um  **n** partição nova:</span><span class="sxs-lookup"><span data-stu-id="7e125-120">Press 'n' at hello prompt toocreate a **n**ew partition:</span></span>

    ```bash
    Command (m for help): n
    ```

3. <span data-ttu-id="7e125-121">Em seguida, pressione 'p' toocreate um **p**rimário partição:</span><span class="sxs-lookup"><span data-stu-id="7e125-121">Next, press 'p' toocreate a **p**rimary partition:</span></span>

    ```bash 
    Command action
            e   extended
            p   primary partition (1-4)
    ```

4. <span data-ttu-id="7e125-122">Pressione '1' tooselect partição número 1:</span><span class="sxs-lookup"><span data-stu-id="7e125-122">Press '1' tooselect partition number 1:</span></span>

    ```bash
    Partition number (1-4): 1
    ```

5. <span data-ttu-id="7e125-123">Selecione Olá ponto de partida da saudação nova partição, ou pressione `<enter>` tooaccept saudação padrão tooplace Olá partição de início de saudação do espaço livre Olá unidade hello:</span><span class="sxs-lookup"><span data-stu-id="7e125-123">Select hello starting point of hello new partition, or press `<enter>` tooaccept hello default tooplace hello partition at hello beginning of hello free space on hello drive:</span></span>

    ```bash   
    First cylinder (1-1305, default 1):
    Using default value 1
    ```

6. <span data-ttu-id="7e125-124">Selecione o tamanho de saudação da partição hello, por exemplo '+10G' do tipo toocreate uma partição de 10 GB.</span><span class="sxs-lookup"><span data-stu-id="7e125-124">Select hello size of hello partition, for example type '+10G' toocreate a 10 gigabyte partition.</span></span> <span data-ttu-id="7e125-125">Ou pressione `<enter>` criar uma única partição que abrange toda a unidade hello:</span><span class="sxs-lookup"><span data-stu-id="7e125-125">Or, press `<enter>` create a single partition that spans hello entire drive:</span></span>

    ```bash   
    Last cylinder, +cylinders or +size{K,M,G} (1-1305, default 1305): 
    Using default value 1305
    ```

7. <span data-ttu-id="7e125-126">Em seguida, alterar a ID de saudação e **t**ID de tipo de partição de saudação do padrão de saudação '83' (Linux) tooID 'fd' (Linux automática de raid):</span><span class="sxs-lookup"><span data-stu-id="7e125-126">Next, change hello ID and **t**ype of hello partition from hello default ID '83' (Linux) tooID 'fd' (Linux raid auto):</span></span>

    ```bash  
    Command (m for help): t
    Selected partition 1
    Hex code (type L toolist codes): fd
    ```

8. <span data-ttu-id="7e125-127">Por fim, gravar toohello unidade da tabela de partição hello e sair do fdisk:</span><span class="sxs-lookup"><span data-stu-id="7e125-127">Finally, write hello partition table toohello drive and exit fdisk:</span></span>

    ```bash   
    Command (m for help): w
    hello partition table has been altered!
    ```

## <a name="create-hello-raid-array"></a><span data-ttu-id="7e125-128">Criar hello RAID matriz</span><span class="sxs-lookup"><span data-stu-id="7e125-128">Create hello RAID array</span></span>
1. <span data-ttu-id="7e125-129">Olá será de exemplo "distribuição" (nível RAID 0) três partições localizadas em três discos de dados separados (sdc1, sdd1, sde1) a seguir.</span><span class="sxs-lookup"><span data-stu-id="7e125-129">hello following example will "stripe" (RAID level 0) three partitions located on three separate data disks (sdc1, sdd1, sde1).</span></span>  <span data-ttu-id="7e125-130">Depois da execução desse comando, um novo dispositivo RAID chamado **/dev/md127** é criado.</span><span class="sxs-lookup"><span data-stu-id="7e125-130">After running this command a new RAID device called **/dev/md127** is created.</span></span> <span data-ttu-id="7e125-131">Observe também que se esses discos de dados, anteriormente parte de outro conjunto RAID expirado pode ser necessário tooadd Olá `--force` toohello parâmetro `mdadm` comando:</span><span class="sxs-lookup"><span data-stu-id="7e125-131">Also note that if these data disks we previously part of another defunct RAID array it may be necessary tooadd hello `--force` parameter toohello `mdadm` command:</span></span>

    ```bash  
    sudo mdadm --create /dev/md127 --level 0 --raid-devices 3 \
        /dev/sdc1 /dev/sdd1 /dev/sde1
    ```

2. <span data-ttu-id="7e125-132">Criar o sistema de arquivos Olá no novo dispositivo RAID Olá</span><span class="sxs-lookup"><span data-stu-id="7e125-132">Create hello file system on hello new RAID device</span></span>
   
    <span data-ttu-id="7e125-133">a.</span><span class="sxs-lookup"><span data-stu-id="7e125-133">a.</span></span> <span data-ttu-id="7e125-134">**CentOS, Oracle Linux, SLES 12, openSUSE e Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="7e125-134">**CentOS, Oracle Linux, SLES 12, openSUSE, and Ubuntu**</span></span>

    ```bash   
    sudo mkfs -t ext4 /dev/md127
    ```
   
    <span data-ttu-id="7e125-135">b.</span><span class="sxs-lookup"><span data-stu-id="7e125-135">b.</span></span> <span data-ttu-id="7e125-136">**SLES 11**</span><span class="sxs-lookup"><span data-stu-id="7e125-136">**SLES 11**</span></span>

    ```bash
    sudo mkfs -t ext3 /dev/md127
    ```
   
    <span data-ttu-id="7e125-137">c.</span><span class="sxs-lookup"><span data-stu-id="7e125-137">c.</span></span> <span data-ttu-id="7e125-138">**SLES 11** – habilite boot.md e crie mdadm.conf</span><span class="sxs-lookup"><span data-stu-id="7e125-138">**SLES 11** - enable boot.md and create mdadm.conf</span></span>

    ```bash
    sudo -i chkconfig --add boot.md
    sudo echo 'DEVICE /dev/sd*[0-9]' >> /etc/mdadm.conf
    ```
   
   > [!NOTE]
   > <span data-ttu-id="7e125-139">Pode ser necessária uma reinicialização depois de fazer essas alterações em sistemas SUSE.</span><span class="sxs-lookup"><span data-stu-id="7e125-139">A reboot may be required after making these changes on SUSE systems.</span></span> <span data-ttu-id="7e125-140">Esta etapa *não* é necessária no SLES 12.</span><span class="sxs-lookup"><span data-stu-id="7e125-140">This step is *not* required on SLES 12.</span></span>
   > 
   > 

## <a name="add-hello-new-file-system-tooetcfstab"></a><span data-ttu-id="7e125-141">Adicionar Olá novo arquivo sistema muito/etc/fstab</span><span class="sxs-lookup"><span data-stu-id="7e125-141">Add hello new file system too/etc/fstab</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7e125-142">Edição incorretamente arquivo /etc/fstab de saudação pode resultar em um sistema não inicializável.</span><span class="sxs-lookup"><span data-stu-id="7e125-142">Improperly editing hello /etc/fstab file could result in an unbootable system.</span></span> <span data-ttu-id="7e125-143">Se não tiver certeza, consulte a documentação do toohello da distribuição para obter informações sobre como tooproperly editar esse arquivo.</span><span class="sxs-lookup"><span data-stu-id="7e125-143">If unsure, refer toohello distribution's documentation for information on how tooproperly edit this file.</span></span> <span data-ttu-id="7e125-144">Também é recomendável que um backup de arquivo /etc/fstab de saudação é criado antes de editar.</span><span class="sxs-lookup"><span data-stu-id="7e125-144">It is also recommended that a backup of hello /etc/fstab file is created before editing.</span></span>

1. <span data-ttu-id="7e125-145">Crie ponto de montagem de saudação desejado para o novo sistema de arquivos, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="7e125-145">Create hello desired mount point for your new file system, for example:</span></span>

    ```bash
    sudo mkdir /data
    ```
2. <span data-ttu-id="7e125-146">Ao editar /etc/fstab, Olá **UUID** deve ser usado tooreference Olá sistema em vez de saudação dispositivo nome de arquivo.</span><span class="sxs-lookup"><span data-stu-id="7e125-146">When editing /etc/fstab, hello **UUID** should be used tooreference hello file system rather than hello device name.</span></span>  <span data-ttu-id="7e125-147">Saudação de uso `blkid` Olá UUID do toodetermine utilitário para o novo sistema de arquivos hello:</span><span class="sxs-lookup"><span data-stu-id="7e125-147">Use hello `blkid` utility toodetermine hello UUID for hello new file system:</span></span>

    ```bash   
    sudo /sbin/blkid
    ...........
    /dev/md127: UUID="aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee" TYPE="ext4"
    ```

3. <span data-ttu-id="7e125-148">Abra /etc/fstab em um editor de texto e adicione uma entrada para o novo sistema de arquivos hello, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="7e125-148">Open /etc/fstab in a text editor and add an entry for hello new file system, for example:</span></span>

    ```bash   
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults  0  2
    ```
   
    <span data-ttu-id="7e125-149">Ou no **SLES 11**:</span><span class="sxs-lookup"><span data-stu-id="7e125-149">Or on **SLES 11**:</span></span>

    ```bash
    /dev/disk/by-uuid/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext3  defaults  0  2
    ```
   
    <span data-ttu-id="7e125-150">Em seguida, salve e feche o /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="7e125-150">Then, save and close /etc/fstab.</span></span>

4. <span data-ttu-id="7e125-151">Teste se Olá /etc/fstab entrada está correta:</span><span class="sxs-lookup"><span data-stu-id="7e125-151">Test that hello /etc/fstab entry is correct:</span></span>

    ```bash  
    sudo mount -a
    ```

    <span data-ttu-id="7e125-152">Se esse comando resulta em uma mensagem de erro, verifique a sintaxe Olá no arquivo /etc/fstab de saudação.</span><span class="sxs-lookup"><span data-stu-id="7e125-152">If this command results in an error message, please check hello syntax in hello /etc/fstab file.</span></span>
   
    <span data-ttu-id="7e125-153">Em seguida execute Olá `mount` montado sistema de arquivos do comando tooensure hello:</span><span class="sxs-lookup"><span data-stu-id="7e125-153">Next run hello `mount` command tooensure hello file system is mounted:</span></span>

    ```bash   
    mount
    .................
    /dev/md127 on /data type ext4 (rw)
    ```

5. <span data-ttu-id="7e125-154">(Opcional) Parâmetros de inicialização à prova de falhas</span><span class="sxs-lookup"><span data-stu-id="7e125-154">(Optional) Failsafe Boot Parameters</span></span>
   
    <span data-ttu-id="7e125-155">**configuração fstab**</span><span class="sxs-lookup"><span data-stu-id="7e125-155">**fstab configuration**</span></span>
   
    <span data-ttu-id="7e125-156">Muitas distribuições incluem qualquer Olá `nobootwait` ou `nofail` parâmetros que podem ser adicionados toohello/etc/fstab arquivo de montagem.</span><span class="sxs-lookup"><span data-stu-id="7e125-156">Many distributions include either hello `nobootwait` or `nofail` mount parameters that may be added toohello /etc/fstab file.</span></span> <span data-ttu-id="7e125-157">Esses parâmetros permitem falhas ao montar um sistema de arquivos específico e permitem Olá Linux sistema toocontinue tooboot mesmo se ele for o sistema de arquivos do tooproperly não é possível montar Olá RAID.</span><span class="sxs-lookup"><span data-stu-id="7e125-157">These parameters allow for failures when mounting a particular file system and allow hello Linux system toocontinue tooboot even if it is unable tooproperly mount hello RAID file system.</span></span> <span data-ttu-id="7e125-158">Para obter mais informações sobre esses parâmetros, consulte a documentação do tooyour da distribuição.</span><span class="sxs-lookup"><span data-stu-id="7e125-158">Refer tooyour distribution's documentation for more information on these parameters.</span></span>
   
    <span data-ttu-id="7e125-159">Exemplo (Ubuntu):</span><span class="sxs-lookup"><span data-stu-id="7e125-159">Example (Ubuntu):</span></span>

    ```bash  
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,nobootwait  0  2
    ```   

    <span data-ttu-id="7e125-160">**Parâmetros de inicialização do Linux**</span><span class="sxs-lookup"><span data-stu-id="7e125-160">**Linux boot parameters**</span></span>
   
    <span data-ttu-id="7e125-161">Em adição toohello acima parâmetros, Olá parâmetro kernel "`bootdegraded=true`" pode permitir Olá tooboot de sistema, mesmo se Olá RAID é percebido como danificado ou degradado, por exemplo, se uma unidade de dados for removida inadvertidamente da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="7e125-161">In addition toohello above parameters, hello kernel parameter "`bootdegraded=true`" can allow hello system tooboot even if hello RAID is perceived as damaged or degraded, for example if a data drive is inadvertently removed from hello virtual machine.</span></span> <span data-ttu-id="7e125-162">Por padrão, isso também pode resultar em um sistema não inicializável.</span><span class="sxs-lookup"><span data-stu-id="7e125-162">By default this could also result in a non-bootable system.</span></span>
   
    <span data-ttu-id="7e125-163">Consulte a documentação da distribuição tooyour em como tooproperly Editar parâmetros de kernel.</span><span class="sxs-lookup"><span data-stu-id="7e125-163">Please refer tooyour distribution's documentation on how tooproperly edit kernel parameters.</span></span> <span data-ttu-id="7e125-164">Por exemplo, em muitas distribuições (CentOS, Oracle Linux, SLES 11) esses parâmetros podem ser adicionados manualmente toohello "`/boot/grub/menu.lst`" arquivo.</span><span class="sxs-lookup"><span data-stu-id="7e125-164">For example, in many distributions (CentOS, Oracle Linux, SLES 11) these parameters may be added manually toohello "`/boot/grub/menu.lst`" file.</span></span>  <span data-ttu-id="7e125-165">No Ubuntu esse parâmetro pode ser adicionado toohello `GRUB_CMDLINE_LINUX_DEFAULT` variável em "/ padrão/etc/grub".</span><span class="sxs-lookup"><span data-stu-id="7e125-165">On Ubuntu this parameter can be added toohello `GRUB_CMDLINE_LINUX_DEFAULT` variable on "/etc/default/grub".</span></span>


## <a name="trimunmap-support"></a><span data-ttu-id="7e125-166">Suporte a TRIM/UNMAP</span><span class="sxs-lookup"><span data-stu-id="7e125-166">TRIM/UNMAP support</span></span>
<span data-ttu-id="7e125-167">Suportam a alguns kernels Linux TRIM/DESMAPEAMENTO operações toodiscard blocos não usados no disco hello.</span><span class="sxs-lookup"><span data-stu-id="7e125-167">Some Linux kernels support TRIM/UNMAP operations toodiscard unused blocks on hello disk.</span></span> <span data-ttu-id="7e125-168">Essas operações são principalmente útil no armazenamento padrão tooinform Azure que páginas excluídas não são mais válidas e podem ser descartadas.</span><span class="sxs-lookup"><span data-stu-id="7e125-168">These operations are primarily useful in standard storage tooinform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="7e125-169">Descartar páginas poderá representar uma economia de dinheiro se você criar arquivos grandes e, em seguida, excluí-los.</span><span class="sxs-lookup"><span data-stu-id="7e125-169">Discarding pages can save cost if you create large files and then delete them.</span></span>

> [!NOTE]
> <span data-ttu-id="7e125-170">RAID não pode emitir comandos de descarte se o tamanho da parte Olá para matriz de saudação é definido tooless padrão hello (512KB).</span><span class="sxs-lookup"><span data-stu-id="7e125-170">RAID may not issue discard commands if hello chunk size for hello array is set tooless than hello default (512KB).</span></span> <span data-ttu-id="7e125-171">Isso ocorre porque Olá desmapeamento granularidade em Olá Host também é 512KB.</span><span class="sxs-lookup"><span data-stu-id="7e125-171">This is because hello unmap granularity on hello Host is also 512KB.</span></span> <span data-ttu-id="7e125-172">Se você modificou o tamanho da parte da matriz Olá por meio do mdadm `--chunk=` parâmetro e TRIM/desmapeamento solicitações podem ser ignoradas pelo kernel hello.</span><span class="sxs-lookup"><span data-stu-id="7e125-172">If you modified hello array's chunk size via mdadm's `--chunk=` parameter, then TRIM/unmap requests may be ignored by hello kernel.</span></span>

<span data-ttu-id="7e125-173">Há duas maneiras tooenable TRIM suporte em sua VM do Linux.</span><span class="sxs-lookup"><span data-stu-id="7e125-173">There are two ways tooenable TRIM support in your Linux VM.</span></span> <span data-ttu-id="7e125-174">Como de costume, consulte a distribuição para Olá abordagem recomendada:</span><span class="sxs-lookup"><span data-stu-id="7e125-174">As usual, consult your distribution for hello recommended approach:</span></span>

- <span data-ttu-id="7e125-175">Saudação de uso `discard` montar opção `/etc/fstab`, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="7e125-175">Use hello `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,discard  0  2
    ```

- <span data-ttu-id="7e125-176">Em alguns Olá casos `discard` opção pode ter implicações de desempenho.</span><span class="sxs-lookup"><span data-stu-id="7e125-176">In some cases hello `discard` option may have performance implications.</span></span> <span data-ttu-id="7e125-177">Como alternativa, você pode executar Olá `fstrim` comando manualmente da linha de comando hello, ou adicionar tooyour crontab toorun regularmente:</span><span class="sxs-lookup"><span data-stu-id="7e125-177">Alternatively, you can run hello `fstrim` command manually from hello command line, or add it tooyour crontab toorun regularly:</span></span>

    <span data-ttu-id="7e125-178">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="7e125-178">**Ubuntu**</span></span>

    ```bash
    # sudo apt-get install util-linux
    # sudo fstrim /data
    ```

    <span data-ttu-id="7e125-179">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="7e125-179">**RHEL/CentOS**</span></span>
    ```bash
    # sudo yum install util-linux
    # sudo fstrim /data
    ```
