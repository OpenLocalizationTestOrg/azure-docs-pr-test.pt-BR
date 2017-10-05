---
title: Adicionar uma VM Linux usando a CLI do Azure | Microsoft Docs
description: "Saiba como adicionar um disco persistente à sua VM Linux com a CLI do Azure 1.0 e 2.0."
keywords: "máquina virtual do Linux, adicionar disco de recurso"
services: virtual-machines-linux
documentationcenter: 
author: rickstercdn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 3005a066-7a84-4dc5-bdaa-574c75e6e411
ms.service: virtual-machines-linux
ms.topic: article
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.date: 02/02/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 185dd276cd79cb7053605d651e8ecdc7fd1e7636
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="add-a-disk-to-a-linux-vm"></a><span data-ttu-id="14fd7-104">Adicionar um disco a uma VM do Linux</span><span class="sxs-lookup"><span data-stu-id="14fd7-104">Add a disk to a Linux VM</span></span>
<span data-ttu-id="14fd7-105">Este artigo mostra como anexar um disco persistente à sua VM para que você possa preservar dados, mesmo que sua VM seja provisionada novamente devido à manutenção ou ao redimensionamento.</span><span class="sxs-lookup"><span data-stu-id="14fd7-105">This article shows how to attach a persistent disk to your VM so that you can preserve your data - even if your VM is reprovisioned due to maintenance or resizing.</span></span> 

## <a name="quick-commands"></a><span data-ttu-id="14fd7-106">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="14fd7-106">Quick Commands</span></span>
<span data-ttu-id="14fd7-107">O exemplo a seguir anexa um disco de `50` GB à VM denominada `myVM` no grupo de recursos denominado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="14fd7-107">The following example attaches a `50`GB disk to the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

<span data-ttu-id="14fd7-108">Para usar os discos gerenciados:</span><span class="sxs-lookup"><span data-stu-id="14fd7-108">To use managed disks:</span></span>

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

<span data-ttu-id="14fd7-109">Para usar os discos não gerenciados:</span><span class="sxs-lookup"><span data-stu-id="14fd7-109">To use unmanaged disks:</span></span>

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="attach-a-managed-disk"></a><span data-ttu-id="14fd7-110">Anexar um disco gerenciado</span><span class="sxs-lookup"><span data-stu-id="14fd7-110">Attach a managed disk</span></span>

<span data-ttu-id="14fd7-111">O uso de discos gerenciados permite que você se concentre em suas VMs e nos discos sem se preocupar com as contas de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="14fd7-111">Using managed disks enables you to focus on your VMs and their disks without worrying about Azure Storage accounts.</span></span> <span data-ttu-id="14fd7-112">Você pode criar e anexar rapidamente um disco gerenciado a uma VM usando o mesmo grupo de recursos do Azure, ou pode criar qualquer quantidade de discos e anexá-los.</span><span class="sxs-lookup"><span data-stu-id="14fd7-112">You can quickly create and attach a managed disk to a VM using the same Azure resource group, or you can create any number of disks and then attach them.</span></span>


### <a name="attach-a-new-disk-to-a-vm"></a><span data-ttu-id="14fd7-113">Anexar um novo disco a uma VM</span><span class="sxs-lookup"><span data-stu-id="14fd7-113">Attach a new disk to a VM</span></span>

<span data-ttu-id="14fd7-114">Se você precisar apenas de um novo disco em sua VM, você pode usar o comando `az vm disk attach`.</span><span class="sxs-lookup"><span data-stu-id="14fd7-114">If you just need a new disk on your VM, you can use the `az vm disk attach` command.</span></span>

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

### <a name="attach-an-existing-disk"></a><span data-ttu-id="14fd7-115">Anexar um disco existente</span><span class="sxs-lookup"><span data-stu-id="14fd7-115">Attach an existing disk</span></span> 

<span data-ttu-id="14fd7-116">Em muitos casos, você anexa discos que já foram criados.</span><span class="sxs-lookup"><span data-stu-id="14fd7-116">In many cases you attach disks that have already been created.</span></span> <span data-ttu-id="14fd7-117">Primeiro você encontrará a ID do disco e depois a passará para o comando `az vm disk attach`.</span><span class="sxs-lookup"><span data-stu-id="14fd7-117">You first find the disk id and then pass that to the `az vm disk attach` command.</span></span> <span data-ttu-id="14fd7-118">O exemplo a seguir usa um disco criado com `az disk create -g myResourceGroup -n myDataDisk --size-gb 50`.</span><span class="sxs-lookup"><span data-stu-id="14fd7-118">The following example uses a disk created with `az disk create -g myResourceGroup -n myDataDisk --size-gb 50`.</span></span>

```azurecli
# find the disk id
diskId=$(az disk show -g myResourceGroup -n myDataDisk --query 'id' -o tsv)
az vm disk attach -g myResourceGroup --vm-name myVM --disk $diskId
```

<span data-ttu-id="14fd7-119">A saída é algo semelhante ao seguinte (você pode usar a opção `-o table` para qualquer comando a fim de formatar a saída):</span><span class="sxs-lookup"><span data-stu-id="14fd7-119">The output looks something like the following (you can use the `-o table` option to any command to format the output in ):</span></span>

```json
{
  "accountType": "Standard_LRS",
  "creationData": {
    "createOption": "Empty",
    "imageReference": null,
    "sourceResourceId": null,
    "sourceUri": null,
    "storageAccountId": null
  },
  "diskSizeGb": 50,
  "encryptionSettings": null,
  "id": "/subscriptions/<guid>/resourceGroups/rasquill-script/providers/Microsoft.Compute/disks/myDataDisk",
  "location": "westus",
  "name": "myDataDisk",
  "osType": null,
  "ownerId": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "tags": null,
  "timeCreated": "2017-02-02T23:35:47.708082+00:00",
  "type": "Microsoft.Compute/disks"
}
```


## <a name="attach-an-unmanaged-disk"></a><span data-ttu-id="14fd7-120">Anexar um disco não gerenciado</span><span class="sxs-lookup"><span data-stu-id="14fd7-120">Attach an unmanaged disk</span></span>

<span data-ttu-id="14fd7-121">O processo de anexar um novo disco é rápido se você não se importar em criar um disco na mesma conta de armazenamento que sua VM.</span><span class="sxs-lookup"><span data-stu-id="14fd7-121">Attaching a new disk is quick if you do not mind creating a disk in the same storage account as your VM.</span></span> <span data-ttu-id="14fd7-122">Digite `azure vm disk attach-new` para criar e anexar um novo disco GB à sua VM.</span><span class="sxs-lookup"><span data-stu-id="14fd7-122">Type `azure vm disk attach-new` to create and attach a new GB disk for your VM.</span></span> <span data-ttu-id="14fd7-123">Se você não identificar explicitamente uma conta de armazenamento, qualquer disco que você criar será colocado na mesma conta de armazenamento na qual o disco do sistema operacional reside.</span><span class="sxs-lookup"><span data-stu-id="14fd7-123">If you do not explicitly identify a storage account, any disk you create is placed in the same storage account where your OS disk resides.</span></span> <span data-ttu-id="14fd7-124">O exemplo a seguir anexa um disco de `50` GB à VM denominada `myVM` no grupo de recursos denominado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="14fd7-124">The following example attaches a `50`GB disk to the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="connect-to-the-linux-vm-to-mount-the-new-disk"></a><span data-ttu-id="14fd7-125">Conectar-se à VM do Linux para montar o novo disco</span><span class="sxs-lookup"><span data-stu-id="14fd7-125">Connect to the Linux VM to mount the new disk</span></span>
> [!NOTE]
> <span data-ttu-id="14fd7-126">Este tópico faz a conexão com uma VM usando nomes de usuário e senhas.</span><span class="sxs-lookup"><span data-stu-id="14fd7-126">This topic connects to a VM using usernames and passwords.</span></span> <span data-ttu-id="14fd7-127">Para usar pares de chaves pública e privada a fim de se comunicar com a VM, confira [Como usar SSH com Linux no Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="14fd7-127">To use public and private key pairs to communicate with your VM, see [How to Use SSH with Linux on Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 
> 
> 

<span data-ttu-id="14fd7-128">Você precisa de SSH em sua VM do Azure para particionar, formatar e montar o novo disco para que sua VM do Linux possa usá-lo.</span><span class="sxs-lookup"><span data-stu-id="14fd7-128">You need to SSH into your Azure VM to partition, format, and mount your new disk so your Linux VM can use it.</span></span> <span data-ttu-id="14fd7-129">Se você não estiver familiarizado com a conexão usando **ssh**, o comando assumirá a forma `ssh <username>@<FQDNofAzureVM> -p <the ssh port>` e será semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="14fd7-129">If you're not familiar with connecting with **ssh**, the command takes the form `ssh <username>@<FQDNofAzureVM> -p <the ssh port>`, and looks like the following:</span></span>

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com -p 22
```

<span data-ttu-id="14fd7-130">Saída</span><span class="sxs-lookup"><span data-stu-id="14fd7-130">Output</span></span>

```bash
The authenticity of host 'mypublicdns.westus.cloudapp.azure.com (191.239.51.1)' can't be established.
ECDSA key fingerprint is bx:xx:xx:xx:xx:xx:xx:xx:xx:x:x:x:x:x:x:xx.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'mypublicdns.westus.cloudapp.azure.com,191.239.51.1' (ECDSA) to the list of known hosts.
ops@mypublicdns.westus.cloudapp.azure.com's password:
Welcome to Ubuntu 14.04.2 LTS (GNU/Linux 3.16.0-37-generic x86_64)

* Documentation:  https://help.ubuntu.com/

System information as of Fri May 22 21:02:32 UTC 2015

System load: 0.37              Memory usage: 2%   Processes:       207
Usage of /:  41.4% of 1.94GB   Swap usage:   0%   Users logged in: 0

Graph this data and manage this system at:
  https://landscape.canonical.com/

Get cloud support with Ubuntu Advantage Cloud Guest:
  http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

ops@myVM:~$
```

<span data-ttu-id="14fd7-131">Agora que está conectado a uma VM, você está pronto para anexar um disco.</span><span class="sxs-lookup"><span data-stu-id="14fd7-131">Now that you're connected to your VM, you're ready to attach a disk.</span></span>  <span data-ttu-id="14fd7-132">Primeiro, localize o disco usando `dmesg | grep SCSI` (o método usado para descobrir o novo disco pode variar).</span><span class="sxs-lookup"><span data-stu-id="14fd7-132">First find the disk, using `dmesg | grep SCSI` (the method you use to discover your new disk may vary).</span></span> <span data-ttu-id="14fd7-133">Nesse caso, deve ser semelhante a:</span><span class="sxs-lookup"><span data-stu-id="14fd7-133">In this case, it looks something like:</span></span>

```bash
dmesg | grep SCSI
```

<span data-ttu-id="14fd7-134">Saída</span><span class="sxs-lookup"><span data-stu-id="14fd7-134">Output</span></span>

```bash
[    0.294784] SCSI subsystem initialized
[    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
[    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
[    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
[ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
```

<span data-ttu-id="14fd7-135">e, no caso deste tópico, o disco do `sdc` é o que pretendemos.</span><span class="sxs-lookup"><span data-stu-id="14fd7-135">and in the case of this topic, the `sdc` disk is the one that we want.</span></span> <span data-ttu-id="14fd7-136">Agora, particione o disco com `sudo fdisk /dev/sdc`. Pressupondo que, no seu caso, o disco era `sdc`, torne-o um disco primário na partição 1 e aceite os outros padrões.</span><span class="sxs-lookup"><span data-stu-id="14fd7-136">Now partition the disk with `sudo fdisk /dev/sdc` -- assuming that in your case the disk was `sdc`, and make it a primary disk on partition 1, and accept the other defaults.</span></span>

```bash
sudo fdisk /dev/sdc
```

<span data-ttu-id="14fd7-137">Saída</span><span class="sxs-lookup"><span data-stu-id="14fd7-137">Output</span></span>

```bash
Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
Building a new DOS disklabel with disk identifier 0x2a59b123.
Changes will remain in memory only, until you decide to write them.
After that, of course, the previous content won't be recoverable.

Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)

Command (m for help): n
Partition type:
   p   primary (0 primary, 0 extended, 4 free)
   e   extended
Select (default p): p
Partition number (1-4, default 1): 1
First sector (2048-10485759, default 2048):
Using default value 2048
Last sector, +sectors or +size{K,M,G} (2048-10485759, default 10485759):
Using default value 10485759
```

<span data-ttu-id="14fd7-138">Para criar a partição, digite `p` no prompt:</span><span class="sxs-lookup"><span data-stu-id="14fd7-138">Create the partition by typing `p` at the prompt:</span></span>

```bash
Command (m for help): p

Disk /dev/sdc: 5368 MB, 5368709120 bytes
255 heads, 63 sectors/track, 652 cylinders, total 10485760 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x2a59b123

   Device Boot      Start         End      Blocks   Id  System
/dev/sdc1            2048    10485759     5241856   83  Linux

Command (m for help): w
The partition table has been altered!

Calling ioctl() to re-read partition table.
Syncing disks.
```

<span data-ttu-id="14fd7-139">Grave um sistema de arquivos para a partição usando o comando **mkfs** , especificando o tipo de sistema de arquivos e o nome do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="14fd7-139">And write a file system to the partition by using the **mkfs** command, specifying your filesystem type and the device name.</span></span> <span data-ttu-id="14fd7-140">Nesse tópico, estamos usando o `ext4` e o `/dev/sdc1` acima:</span><span class="sxs-lookup"><span data-stu-id="14fd7-140">In this topic, we're using `ext4` and `/dev/sdc1` from above:</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="14fd7-141">Saída</span><span class="sxs-lookup"><span data-stu-id="14fd7-141">Output</span></span>

```bash
mke2fs 1.42.9 (4-Feb-2014)
Discarding device blocks: done
Filesystem label=
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
Stride=0 blocks, Stripe width=0 blocks
327680 inodes, 1310464 blocks
65523 blocks (5.00%) reserved for the super user
First data block=0
Maximum filesystem blocks=1342177280
40 block groups
32768 blocks per group, 32768 fragments per group
8192 inodes per group
Superblock backups stored on blocks:
    32768, 98304, 163840, 229376, 294912, 819200, 884736
Allocating group tables: done
Writing inode tables: done
Creating journal (32768 blocks): done
Writing superblocks and filesystem accounting information: done
```

<span data-ttu-id="14fd7-142">Agora, crie um diretório para montar o novo sistema de arquivos usando o `mkdir`:</span><span class="sxs-lookup"><span data-stu-id="14fd7-142">Now we create a directory to mount the file system using `mkdir`:</span></span>

```bash
sudo mkdir /datadrive
```

<span data-ttu-id="14fd7-143">E monte o diretório usando o `mount`:</span><span class="sxs-lookup"><span data-stu-id="14fd7-143">And you mount the directory using `mount`:</span></span>

```bash
sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="14fd7-144">O disco de dados agora está pronto para uso como o `/datadrive`.</span><span class="sxs-lookup"><span data-stu-id="14fd7-144">The data disk is now ready to use as `/datadrive`.</span></span>

```bash
ls
```

<span data-ttu-id="14fd7-145">Saída</span><span class="sxs-lookup"><span data-stu-id="14fd7-145">Output</span></span>

```bash
bin   datadrive  etc   initrd.img  lib64       media  opt   root  sbin  sys  usr  vmlinuz
boot  dev        home  lib         lost+found  mnt    proc  run   srv   tmp  var
```

<span data-ttu-id="14fd7-146">Para garantir que a unidade seja remontada automaticamente após uma reinicialização, ela deve ser adicionada ao arquivo /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="14fd7-146">To ensure the drive is remounted automatically after a reboot it must be added to the /etc/fstab file.</span></span> <span data-ttu-id="14fd7-147">Além disso, é altamente recomendável que o UUID (Identificador Universal Exclusivo) seja usado no /etc/fstab para fazer referência à unidade, e não apenas ao nome do dispositivo (por exemplo, `/dev/sdc1`).</span><span class="sxs-lookup"><span data-stu-id="14fd7-147">In addition, it is highly recommended that the UUID (Universally Unique IDentifier) is used in /etc/fstab to refer to the drive rather than just the device name (such as, `/dev/sdc1`).</span></span> <span data-ttu-id="14fd7-148">Se o sistema operacional detectar um erro de disco durante a inicialização, usar o UUID evita que o disco incorreto seja montado em um determinado local.</span><span class="sxs-lookup"><span data-stu-id="14fd7-148">If the OS detects a disk error during boot, using the UUID avoids the incorrect disk being mounted to a given location.</span></span> <span data-ttu-id="14fd7-149">Os discos de dados restantes seriam então atribuídos a essas mesmas IDs de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="14fd7-149">Remaining data disks would then be assigned those same device IDs.</span></span> <span data-ttu-id="14fd7-150">Para localizar o UUID da nova unidade, use o utilitário **blkid** :</span><span class="sxs-lookup"><span data-stu-id="14fd7-150">To find the UUID of the new drive, use the **blkid** utility:</span></span>

```bash
sudo -i blkid
```

<span data-ttu-id="14fd7-151">A saída deve ser semelhante a esta:</span><span class="sxs-lookup"><span data-stu-id="14fd7-151">The output looks similar to the following:</span></span>

```bash
/dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
/dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

> [!NOTE]
> <span data-ttu-id="14fd7-152">A edição inadequada do arquivo **/etc/fstab** pode resultar em um sistema não inicializável.</span><span class="sxs-lookup"><span data-stu-id="14fd7-152">Improperly editing the **/etc/fstab** file could result in an unbootable system.</span></span> <span data-ttu-id="14fd7-153">Se não tiver certeza, consulte a documentação de distribuição para obter informações sobre como editá-lo corretamente.</span><span class="sxs-lookup"><span data-stu-id="14fd7-153">If unsure, refer to the distribution's documentation for information on how to properly edit this file.</span></span> <span data-ttu-id="14fd7-154">Também é recomendável que um backup do arquivo /etc/fstab seja criado antes da edição.</span><span class="sxs-lookup"><span data-stu-id="14fd7-154">It is also recommended that a backup of the /etc/fstab file is created before editing.</span></span>
> 
> 

<span data-ttu-id="14fd7-155">Em seguida, abra o arquivo **/etc/fstab** em um editor de texto:</span><span class="sxs-lookup"><span data-stu-id="14fd7-155">Next, open the **/etc/fstab** file in a text editor:</span></span>

```bash
sudo vi /etc/fstab
```

<span data-ttu-id="14fd7-156">Neste exemplo, usamos o valor UUID para o novo dispositivo **/dev/sdc1** criado nas etapas anteriores e o ponto de montagem **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="14fd7-156">In this example, we use the UUID value for the new **/dev/sdc1** device that was created in the previous steps, and the mountpoint **/datadrive**.</span></span> <span data-ttu-id="14fd7-157">Adicione a seguinte linha no final do arquivo **/etc/fstab** :</span><span class="sxs-lookup"><span data-stu-id="14fd7-157">Add the following line to the end of the **/etc/fstab** file:</span></span>

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
```

> [!NOTE]
> <span data-ttu-id="14fd7-158">Remover um disco de dados posteriormente sem editar fstab pode fazer com que a VM falhe ao ser inicializada.</span><span class="sxs-lookup"><span data-stu-id="14fd7-158">Later removing a data disk without editing fstab could cause the VM to fail to boot.</span></span> <span data-ttu-id="14fd7-159">A maioria das distribuições fornece as opções fstab `nofail` e/ou `nobootwait`.</span><span class="sxs-lookup"><span data-stu-id="14fd7-159">Most distributions provide either the `nofail` and/or `nobootwait` fstab options.</span></span> <span data-ttu-id="14fd7-160">Essas opções permitem que um sistema inicialize mesmo se o disco não for montado no momento da inicialização.</span><span class="sxs-lookup"><span data-stu-id="14fd7-160">These options allow a system to boot even if the disk fails to mount at boot time.</span></span> <span data-ttu-id="14fd7-161">Consulte a documentação da distribuição para obter mais informações sobre esses parâmetros.</span><span class="sxs-lookup"><span data-stu-id="14fd7-161">Consult your distribution's documentation for more information on these parameters.</span></span>
> 
> <span data-ttu-id="14fd7-162">A opção **nofail** garante que a VM inicie mesmo que o sistema de arquivos esteja corrompido ou que o disco não exista no momento da inicialização.</span><span class="sxs-lookup"><span data-stu-id="14fd7-162">The **nofail** option ensures that the VM starts even if the filesystem is corrupt or the disk does not exist at boot time.</span></span> <span data-ttu-id="14fd7-163">Sem essa opção, você poderá encontrar um comportamento conforme descrito em [Não é possível conectar-se a uma VM Linux via SSH devido a erros no FSTAB](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)</span><span class="sxs-lookup"><span data-stu-id="14fd7-163">Without this option, you may encounter behavior as described in [Cannot SSH to Linux VM due to FSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)</span></span>

### <a name="trimunmap-support-for-linux-in-azure"></a><span data-ttu-id="14fd7-164">Suporte a TRIM/UNMAP para Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="14fd7-164">TRIM/UNMAP support for Linux in Azure</span></span>
<span data-ttu-id="14fd7-165">Alguns kernels Linux permitem operações TRIM/UNMAP para descartar os blocos não utilizados no disco.</span><span class="sxs-lookup"><span data-stu-id="14fd7-165">Some Linux kernels support TRIM/UNMAP operations to discard unused blocks on the disk.</span></span> <span data-ttu-id="14fd7-166">Isso é útil principalmente no Armazenamento Standard, para informar o Azure de que as páginas excluídas não são mais válidas e podem ser descartadas.</span><span class="sxs-lookup"><span data-stu-id="14fd7-166">This is primarily useful in standard storage to inform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="14fd7-167">Isso poderá representar uma economia de dinheiro se você criar arquivos grandes e, em seguida, excluí-los.</span><span class="sxs-lookup"><span data-stu-id="14fd7-167">This can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="14fd7-168">Há duas maneiras de habilitar o suporte a TRIM em sua VM do Linux.</span><span class="sxs-lookup"><span data-stu-id="14fd7-168">There are two ways to enable TRIM support in your Linux VM.</span></span> <span data-ttu-id="14fd7-169">Como de costume, consulte sua distribuição para obter a abordagem recomendada:</span><span class="sxs-lookup"><span data-stu-id="14fd7-169">As usual, consult your distribution for the recommended approach:</span></span>

* <span data-ttu-id="14fd7-170">Use a opção de montagem `discard` em `/etc/fstab`, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="14fd7-170">Use the `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```
* <span data-ttu-id="14fd7-171">Em alguns casos a opção `discard` pode afetar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="14fd7-171">In some cases the `discard` option may have performance implications.</span></span> <span data-ttu-id="14fd7-172">Como alternativa, você pode executar o comando `fstrim` manualmente na linha de comando ou adicioná-lo a crontab para ser executado normalmente:</span><span class="sxs-lookup"><span data-stu-id="14fd7-172">Alternatively, you can run the `fstrim` command manually from the command line, or add it to your crontab to run regularly:</span></span>
  
    <span data-ttu-id="14fd7-173">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="14fd7-173">**Ubuntu**</span></span>
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    <span data-ttu-id="14fd7-174">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="14fd7-174">**RHEL/CentOS**</span></span>

    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a><span data-ttu-id="14fd7-175">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="14fd7-175">Troubleshooting</span></span>
[!INCLUDE [virtual-machines-linux-lunzero](../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a><span data-ttu-id="14fd7-176">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="14fd7-176">Next Steps</span></span>
* <span data-ttu-id="14fd7-177">Lembre-se de que o novo disco não está disponível para a VM, caso seja reinicializado, a menos que você grave essas informações no seu arquivo [fstab](http://en.wikipedia.org/wiki/Fstab) .</span><span class="sxs-lookup"><span data-stu-id="14fd7-177">Remember, that your new disk is not available to the VM if it reboots unless you write that information to your [fstab](http://en.wikipedia.org/wiki/Fstab) file.</span></span>
* <span data-ttu-id="14fd7-178">Para garantir que a VM Linux seja configurada corretamente, leia as recomendações em [Otimizar sua VM do Linux no Azure](optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) .</span><span class="sxs-lookup"><span data-stu-id="14fd7-178">To ensure your Linux VM is configured correctly, review the [Optimize your Linux machine performance](optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) recommendations.</span></span>
* <span data-ttu-id="14fd7-179">Expanda a capacidade de armazenamento adicionando mais discos e [configure o RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obter desempenho adicional.</span><span class="sxs-lookup"><span data-stu-id="14fd7-179">Expand your storage capacity by adding additional disks and [configure RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for additional performance.</span></span>

