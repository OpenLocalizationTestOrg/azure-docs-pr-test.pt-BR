---
title: "Olá aaaAdd um disco tooLinux VM usando a CLI do Azure | Microsoft Docs"
description: Saiba tooadd tooyour um disco persistente VM do Linux com hello Azure CLI 1.0 e 2.0.
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
ms.openlocfilehash: 0dc5236be62d96b70dd47a7f621f626a037e22aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-disk-tooa-linux-vm"></a><span data-ttu-id="04478-104">Adicionar um disco tooa VM do Linux</span><span class="sxs-lookup"><span data-stu-id="04478-104">Add a disk tooa Linux VM</span></span>
<span data-ttu-id="04478-105">Este artigo mostra como tooattach um persistente disco tooyour VM para que você pode preservar os dados - mesmo se sua VM for reprovisionada devido toomaintenance ou redimensionamento.</span><span class="sxs-lookup"><span data-stu-id="04478-105">This article shows how tooattach a persistent disk tooyour VM so that you can preserve your data - even if your VM is reprovisioned due toomaintenance or resizing.</span></span> 

## <a name="quick-commands"></a><span data-ttu-id="04478-106">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="04478-106">Quick Commands</span></span>
<span data-ttu-id="04478-107">Olá seguindo o exemplo anexa um `50`GB disco toohello VM denominada `myVM` no grupo de recursos de saudação chamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="04478-107">hello following example attaches a `50`GB disk toohello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

<span data-ttu-id="04478-108">toouse discos gerenciado:</span><span class="sxs-lookup"><span data-stu-id="04478-108">toouse managed disks:</span></span>

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

<span data-ttu-id="04478-109">discos toouse não gerenciado:</span><span class="sxs-lookup"><span data-stu-id="04478-109">toouse unmanaged disks:</span></span>

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="attach-a-managed-disk"></a><span data-ttu-id="04478-110">Anexar um disco gerenciado</span><span class="sxs-lookup"><span data-stu-id="04478-110">Attach a managed disk</span></span>

<span data-ttu-id="04478-111">Usando discos gerenciados permite que você toofocus em suas VMs e seus discos sem se preocupar sobre contas de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="04478-111">Using managed disks enables you toofocus on your VMs and their disks without worrying about Azure Storage accounts.</span></span> <span data-ttu-id="04478-112">Você pode criar rapidamente e anexar um disco gerenciado tooa VM usando Olá mesmo grupo de recursos do Azure, ou você pode criar qualquer número de discos e, em seguida, anexá-los.</span><span class="sxs-lookup"><span data-stu-id="04478-112">You can quickly create and attach a managed disk tooa VM using hello same Azure resource group, or you can create any number of disks and then attach them.</span></span>


### <a name="attach-a-new-disk-tooa-vm"></a><span data-ttu-id="04478-113">Anexar um novo tooa de disco VM</span><span class="sxs-lookup"><span data-stu-id="04478-113">Attach a new disk tooa VM</span></span>

<span data-ttu-id="04478-114">Se você precisar apenas de um novo disco na sua VM, você pode usar o hello `az vm disk attach` comando.</span><span class="sxs-lookup"><span data-stu-id="04478-114">If you just need a new disk on your VM, you can use hello `az vm disk attach` command.</span></span>

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

### <a name="attach-an-existing-disk"></a><span data-ttu-id="04478-115">Anexar um disco existente</span><span class="sxs-lookup"><span data-stu-id="04478-115">Attach an existing disk</span></span> 

<span data-ttu-id="04478-116">Em muitos casos, você anexa discos que já foram criados.</span><span class="sxs-lookup"><span data-stu-id="04478-116">In many cases you attach disks that have already been created.</span></span> <span data-ttu-id="04478-117">Você primeiro localizar a id do disco hello e, em seguida, passar esse toohello `az vm disk attach` comando.</span><span class="sxs-lookup"><span data-stu-id="04478-117">You first find hello disk id and then pass that toohello `az vm disk attach` command.</span></span> <span data-ttu-id="04478-118">Olá, exemplo a seguir usa um disco criado com `az disk create -g myResourceGroup -n myDataDisk --size-gb 50`.</span><span class="sxs-lookup"><span data-stu-id="04478-118">hello following example uses a disk created with `az disk create -g myResourceGroup -n myDataDisk --size-gb 50`.</span></span>

```azurecli
# find hello disk id
diskId=$(az disk show -g myResourceGroup -n myDataDisk --query 'id' -o tsv)
az vm disk attach -g myResourceGroup --vm-name myVM --disk $diskId
```

<span data-ttu-id="04478-119">Olá saída parecida com hello seguinte (você pode usar o hello `-o table` opção tooany tooformat Olá saída do comando):</span><span class="sxs-lookup"><span data-stu-id="04478-119">hello output looks something like hello following (you can use hello `-o table` option tooany command tooformat hello output in ):</span></span>

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


## <a name="attach-an-unmanaged-disk"></a><span data-ttu-id="04478-120">Anexar um disco não gerenciado</span><span class="sxs-lookup"><span data-stu-id="04478-120">Attach an unmanaged disk</span></span>

<span data-ttu-id="04478-121">Anexar um novo disco é rápido se você não se importar a criação de um disco no hello mesma conta de armazenamento como sua VM.</span><span class="sxs-lookup"><span data-stu-id="04478-121">Attaching a new disk is quick if you do not mind creating a disk in hello same storage account as your VM.</span></span> <span data-ttu-id="04478-122">Tipo `azure vm disk attach-new` toocreate e anexar um novo disco GB para sua VM.</span><span class="sxs-lookup"><span data-stu-id="04478-122">Type `azure vm disk attach-new` toocreate and attach a new GB disk for your VM.</span></span> <span data-ttu-id="04478-123">Se você não identificar explicitamente uma conta de armazenamento, qualquer disco que você cria é colocado no hello mesma conta de armazenamento onde reside o disco do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="04478-123">If you do not explicitly identify a storage account, any disk you create is placed in hello same storage account where your OS disk resides.</span></span> <span data-ttu-id="04478-124">Olá seguindo o exemplo anexa um `50`GB disco toohello VM denominada `myVM` no grupo de recursos de saudação chamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="04478-124">hello following example attaches a `50`GB disk toohello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="connect-toohello-linux-vm-toomount-hello-new-disk"></a><span data-ttu-id="04478-125">Conecte-se toohello novo disco de VM do Linux toomount Olá</span><span class="sxs-lookup"><span data-stu-id="04478-125">Connect toohello Linux VM toomount hello new disk</span></span>
> [!NOTE]
> <span data-ttu-id="04478-126">Este tópico se conecta tooa VM usando nomes de usuário e senhas.</span><span class="sxs-lookup"><span data-stu-id="04478-126">This topic connects tooa VM using usernames and passwords.</span></span> <span data-ttu-id="04478-127">toouse toocommunicate de pares de chaves públicas e privadas com sua VM, consulte [como tooUse SSH com Linux no Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="04478-127">toouse public and private key pairs toocommunicate with your VM, see [How tooUse SSH with Linux on Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 
> 
> 

<span data-ttu-id="04478-128">Você precisa tooSSH em toopartition sua VM do Azure, formatar e montar o novo disco para a VM do Linux podem usá-lo.</span><span class="sxs-lookup"><span data-stu-id="04478-128">You need tooSSH into your Azure VM toopartition, format, and mount your new disk so your Linux VM can use it.</span></span> <span data-ttu-id="04478-129">Se você não estiver familiarizado com a conexão com **ssh**, comando Olá assume a forma de saudação `ssh <username>@<FQDNofAzureVM> -p <hello ssh port>`e Olá seguinte aparência:</span><span class="sxs-lookup"><span data-stu-id="04478-129">If you're not familiar with connecting with **ssh**, hello command takes hello form `ssh <username>@<FQDNofAzureVM> -p <hello ssh port>`, and looks like hello following:</span></span>

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com -p 22
```

<span data-ttu-id="04478-130">Saída</span><span class="sxs-lookup"><span data-stu-id="04478-130">Output</span></span>

```bash
hello authenticity of host 'mypublicdns.westus.cloudapp.azure.com (191.239.51.1)' can't be established.
ECDSA key fingerprint is bx:xx:xx:xx:xx:xx:xx:xx:xx:x:x:x:x:x:x:xx.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added 'mypublicdns.westus.cloudapp.azure.com,191.239.51.1' (ECDSA) toohello list of known hosts.
ops@mypublicdns.westus.cloudapp.azure.com's password:
Welcome tooUbuntu 14.04.2 LTS (GNU/Linux 3.16.0-37-generic x86_64)

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

hello programs included with hello Ubuntu system are free software;
hello exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, toohello extent permitted by
applicable law.

ops@myVM:~$
```

<span data-ttu-id="04478-131">Agora que você está conectado tooyour VM, você está pronto tooattach um disco.</span><span class="sxs-lookup"><span data-stu-id="04478-131">Now that you're connected tooyour VM, you're ready tooattach a disk.</span></span>  <span data-ttu-id="04478-132">Primeiro localize Olá disco, usando `dmesg | grep SCSI` (método hello usar toodiscover o novo disco pode variar).</span><span class="sxs-lookup"><span data-stu-id="04478-132">First find hello disk, using `dmesg | grep SCSI` (hello method you use toodiscover your new disk may vary).</span></span> <span data-ttu-id="04478-133">Nesse caso, deve ser semelhante a:</span><span class="sxs-lookup"><span data-stu-id="04478-133">In this case, it looks something like:</span></span>

```bash
dmesg | grep SCSI
```

<span data-ttu-id="04478-134">Saída</span><span class="sxs-lookup"><span data-stu-id="04478-134">Output</span></span>

```bash
[    0.294784] SCSI subsystem initialized
[    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
[    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
[    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
[ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
```

<span data-ttu-id="04478-135">e no caso de Olá deste tópico, Olá `sdc` disco é hello que queremos.</span><span class="sxs-lookup"><span data-stu-id="04478-135">and in hello case of this topic, hello `sdc` disk is hello one that we want.</span></span> <span data-ttu-id="04478-136">Agora partição Olá disco com `sudo fdisk /dev/sdc` - supondo que no seu caso Olá disco foi `sdc`e é um disco principal na partição 1 e aceitar Olá outros padrões.</span><span class="sxs-lookup"><span data-stu-id="04478-136">Now partition hello disk with `sudo fdisk /dev/sdc` -- assuming that in your case hello disk was `sdc`, and make it a primary disk on partition 1, and accept hello other defaults.</span></span>

```bash
sudo fdisk /dev/sdc
```

<span data-ttu-id="04478-137">Saída</span><span class="sxs-lookup"><span data-stu-id="04478-137">Output</span></span>

```bash
Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
Building a new DOS disklabel with disk identifier 0x2a59b123.
Changes will remain in memory only, until you decide toowrite them.
After that, of course, hello previous content won't be recoverable.

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

<span data-ttu-id="04478-138">Criar partição Olá digitando `p` no prompt de saudação:</span><span class="sxs-lookup"><span data-stu-id="04478-138">Create hello partition by typing `p` at hello prompt:</span></span>

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
hello partition table has been altered!

Calling ioctl() toore-read partition table.
Syncing disks.
```

<span data-ttu-id="04478-139">E gravar um sistema de arquivos toohello partição usando Olá **mkfs** comando, especificando o nome do dispositivo hello e de tipo de sistema de arquivos.</span><span class="sxs-lookup"><span data-stu-id="04478-139">And write a file system toohello partition by using hello **mkfs** command, specifying your filesystem type and hello device name.</span></span> <span data-ttu-id="04478-140">Nesse tópico, estamos usando o `ext4` e o `/dev/sdc1` acima:</span><span class="sxs-lookup"><span data-stu-id="04478-140">In this topic, we're using `ext4` and `/dev/sdc1` from above:</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="04478-141">Saída</span><span class="sxs-lookup"><span data-stu-id="04478-141">Output</span></span>

```bash
mke2fs 1.42.9 (4-Feb-2014)
Discarding device blocks: done
Filesystem label=
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
Stride=0 blocks, Stripe width=0 blocks
327680 inodes, 1310464 blocks
65523 blocks (5.00%) reserved for hello super user
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

<span data-ttu-id="04478-142">Agora podemos criar um diretório toomount Olá sistema de arquivos usando `mkdir`:</span><span class="sxs-lookup"><span data-stu-id="04478-142">Now we create a directory toomount hello file system using `mkdir`:</span></span>

```bash
sudo mkdir /datadrive
```

<span data-ttu-id="04478-143">E você montar Olá diretório usando `mount`:</span><span class="sxs-lookup"><span data-stu-id="04478-143">And you mount hello directory using `mount`:</span></span>

```bash
sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="04478-144">disco de dados Olá agora está pronto toouse como `/datadrive`.</span><span class="sxs-lookup"><span data-stu-id="04478-144">hello data disk is now ready toouse as `/datadrive`.</span></span>

```bash
ls
```

<span data-ttu-id="04478-145">Saída</span><span class="sxs-lookup"><span data-stu-id="04478-145">Output</span></span>

```bash
bin   datadrive  etc   initrd.img  lib64       media  opt   root  sbin  sys  usr  vmlinuz
boot  dev        home  lib         lost+found  mnt    proc  run   srv   tmp  var
```

<span data-ttu-id="04478-146">unidade de saudação tooensure é remontada automaticamente após uma reinicialização, que ele deve ser adicionado toohello /etc/fstab arquivo.</span><span class="sxs-lookup"><span data-stu-id="04478-146">tooensure hello drive is remounted automatically after a reboot it must be added toohello /etc/fstab file.</span></span> <span data-ttu-id="04478-147">Além disso, é altamente recomendável que Olá UUID (identificador universalmente exclusivo) é usado em /etc/hosts/unidade fstab toorefer toohello em vez do nome do dispositivo apenas hello (como `/dev/sdc1`).</span><span class="sxs-lookup"><span data-stu-id="04478-147">In addition, it is highly recommended that hello UUID (Universally Unique IDentifier) is used in /etc/fstab toorefer toohello drive rather than just hello device name (such as, `/dev/sdc1`).</span></span> <span data-ttu-id="04478-148">Se Olá SO detecta um erro de disco durante a inicialização, usar Olá UUID evita que está sendo montado tooa dado local de disco incorreta hello.</span><span class="sxs-lookup"><span data-stu-id="04478-148">If hello OS detects a disk error during boot, using hello UUID avoids hello incorrect disk being mounted tooa given location.</span></span> <span data-ttu-id="04478-149">Os discos de dados restantes seriam então atribuídos a essas mesmas IDs de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="04478-149">Remaining data disks would then be assigned those same device IDs.</span></span> <span data-ttu-id="04478-150">toofind Olá UUID da unidade nova hello, use Olá **blkid** utilitário:</span><span class="sxs-lookup"><span data-stu-id="04478-150">toofind hello UUID of hello new drive, use hello **blkid** utility:</span></span>

```bash
sudo -i blkid
```

<span data-ttu-id="04478-151">saída de Hello tem a aparência a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="04478-151">hello output looks similar toohello following:</span></span>

```bash
/dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
/dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

> [!NOTE]
> <span data-ttu-id="04478-152">Edição incorretamente Olá **/etc/fstab** arquivo pode resultar em um sistema não inicializável.</span><span class="sxs-lookup"><span data-stu-id="04478-152">Improperly editing hello **/etc/fstab** file could result in an unbootable system.</span></span> <span data-ttu-id="04478-153">Se não tiver certeza, consulte a documentação do toohello da distribuição para obter informações sobre como tooproperly editar esse arquivo.</span><span class="sxs-lookup"><span data-stu-id="04478-153">If unsure, refer toohello distribution's documentation for information on how tooproperly edit this file.</span></span> <span data-ttu-id="04478-154">Também é recomendável que um backup de arquivo /etc/fstab de saudação é criado antes de editar.</span><span class="sxs-lookup"><span data-stu-id="04478-154">It is also recommended that a backup of hello /etc/fstab file is created before editing.</span></span>
> 
> 

<span data-ttu-id="04478-155">Em seguida, abra Olá **/etc/fstab** em um editor de texto:</span><span class="sxs-lookup"><span data-stu-id="04478-155">Next, open hello **/etc/fstab** file in a text editor:</span></span>

```bash
sudo vi /etc/fstab
```

<span data-ttu-id="04478-156">Neste exemplo, usamos Olá UUID valor para Olá novo **/desenvolvimento/sdc1** dispositivo que foi criado em etapas anteriores hello e ponto de montagem Olá **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="04478-156">In this example, we use hello UUID value for hello new **/dev/sdc1** device that was created in hello previous steps, and hello mountpoint **/datadrive**.</span></span> <span data-ttu-id="04478-157">Adicionar Olá após o final da linha toohello de saudação **/etc/fstab** arquivo:</span><span class="sxs-lookup"><span data-stu-id="04478-157">Add hello following line toohello end of hello **/etc/fstab** file:</span></span>

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
```

> [!NOTE]
> <span data-ttu-id="04478-158">Remover posteriormente um disco de dados sem editar fstab poderia causar Olá VM toofail tooboot.</span><span class="sxs-lookup"><span data-stu-id="04478-158">Later removing a data disk without editing fstab could cause hello VM toofail tooboot.</span></span> <span data-ttu-id="04478-159">A maioria das distribuições fornecem qualquer Olá `nofail` e/ou `nobootwait` fstab opções.</span><span class="sxs-lookup"><span data-stu-id="04478-159">Most distributions provide either hello `nofail` and/or `nobootwait` fstab options.</span></span> <span data-ttu-id="04478-160">Essas opções permitem tooboot um sistema, mesmo se o disco de saudação falhar toomount no momento da inicialização.</span><span class="sxs-lookup"><span data-stu-id="04478-160">These options allow a system tooboot even if hello disk fails toomount at boot time.</span></span> <span data-ttu-id="04478-161">Consulte a documentação da distribuição para obter mais informações sobre esses parâmetros.</span><span class="sxs-lookup"><span data-stu-id="04478-161">Consult your distribution's documentation for more information on these parameters.</span></span>
> 
> <span data-ttu-id="04478-162">Olá **nofail** opção garante que Olá VM iniciado mesmo se Olá de sistema de arquivos está corrompido ou disco Olá não existe no momento da inicialização.</span><span class="sxs-lookup"><span data-stu-id="04478-162">hello **nofail** option ensures that hello VM starts even if hello filesystem is corrupt or hello disk does not exist at boot time.</span></span> <span data-ttu-id="04478-163">Sem essa opção, você pode encontrar o comportamento conforme descrito em [não é possível SSH tooLinux VM devido a erros de tooFSTAB](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)</span><span class="sxs-lookup"><span data-stu-id="04478-163">Without this option, you may encounter behavior as described in [Cannot SSH tooLinux VM due tooFSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)</span></span>

### <a name="trimunmap-support-for-linux-in-azure"></a><span data-ttu-id="04478-164">Suporte a TRIM/UNMAP para Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="04478-164">TRIM/UNMAP support for Linux in Azure</span></span>
<span data-ttu-id="04478-165">Suportam a alguns kernels Linux TRIM/DESMAPEAMENTO operações toodiscard blocos não usados no disco hello.</span><span class="sxs-lookup"><span data-stu-id="04478-165">Some Linux kernels support TRIM/UNMAP operations toodiscard unused blocks on hello disk.</span></span> <span data-ttu-id="04478-166">Isso é útil principalmente no armazenamento padrão tooinform Azure que páginas excluídas não são mais válidas e podem ser descartadas.</span><span class="sxs-lookup"><span data-stu-id="04478-166">This is primarily useful in standard storage tooinform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="04478-167">Isso poderá representar uma economia de dinheiro se você criar arquivos grandes e, em seguida, excluí-los.</span><span class="sxs-lookup"><span data-stu-id="04478-167">This can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="04478-168">Há duas maneiras tooenable TRIM suporte em sua VM do Linux.</span><span class="sxs-lookup"><span data-stu-id="04478-168">There are two ways tooenable TRIM support in your Linux VM.</span></span> <span data-ttu-id="04478-169">Como de costume, consulte a distribuição para Olá abordagem recomendada:</span><span class="sxs-lookup"><span data-stu-id="04478-169">As usual, consult your distribution for hello recommended approach:</span></span>

* <span data-ttu-id="04478-170">Saudação de uso `discard` montar opção `/etc/fstab`, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="04478-170">Use hello `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```
* <span data-ttu-id="04478-171">Em alguns Olá casos `discard` opção pode ter implicações de desempenho.</span><span class="sxs-lookup"><span data-stu-id="04478-171">In some cases hello `discard` option may have performance implications.</span></span> <span data-ttu-id="04478-172">Como alternativa, você pode executar Olá `fstrim` comando manualmente da linha de comando hello, ou adicionar tooyour crontab toorun regularmente:</span><span class="sxs-lookup"><span data-stu-id="04478-172">Alternatively, you can run hello `fstrim` command manually from hello command line, or add it tooyour crontab toorun regularly:</span></span>
  
    <span data-ttu-id="04478-173">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="04478-173">**Ubuntu**</span></span>
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    <span data-ttu-id="04478-174">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="04478-174">**RHEL/CentOS**</span></span>

    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a><span data-ttu-id="04478-175">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="04478-175">Troubleshooting</span></span>
[!INCLUDE [virtual-machines-linux-lunzero](../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a><span data-ttu-id="04478-176">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="04478-176">Next Steps</span></span>
* <span data-ttu-id="04478-177">Lembre-se de que o novo disco não é disponível toohello VM se ele for reinicializado, a menos que você escreve que tooyour informações [fstab](http://en.wikipedia.org/wiki/Fstab) arquivo.</span><span class="sxs-lookup"><span data-stu-id="04478-177">Remember, that your new disk is not available toohello VM if it reboots unless you write that information tooyour [fstab](http://en.wikipedia.org/wiki/Fstab) file.</span></span>
* <span data-ttu-id="04478-178">tooensure sua VM do Linux é configurado corretamente, examinar Olá [otimizar o desempenho do computador Linux](optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) recomendações.</span><span class="sxs-lookup"><span data-stu-id="04478-178">tooensure your Linux VM is configured correctly, review hello [Optimize your Linux machine performance](optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) recommendations.</span></span>
* <span data-ttu-id="04478-179">Expanda a capacidade de armazenamento adicionando mais discos e [configure o RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obter desempenho adicional.</span><span class="sxs-lookup"><span data-stu-id="04478-179">Expand your storage capacity by adding additional disks and [configure RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for additional performance.</span></span>

