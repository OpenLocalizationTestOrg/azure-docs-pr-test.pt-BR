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
# <a name="add-a-disk-tooa-linux-vm"></a>Adicionar um disco tooa VM do Linux
Este artigo mostra como tooattach um persistente disco tooyour VM para que você pode preservar os dados - mesmo se sua VM for reprovisionada devido toomaintenance ou redimensionamento. 

## <a name="quick-commands"></a>Comandos rápidos
Olá seguindo o exemplo anexa um `50`GB disco toohello VM denominada `myVM` no grupo de recursos de saudação chamado `myResourceGroup`:

toouse discos gerenciado:

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

discos toouse não gerenciado:

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="attach-a-managed-disk"></a>Anexar um disco gerenciado

Usando discos gerenciados permite que você toofocus em suas VMs e seus discos sem se preocupar sobre contas de armazenamento do Azure. Você pode criar rapidamente e anexar um disco gerenciado tooa VM usando Olá mesmo grupo de recursos do Azure, ou você pode criar qualquer número de discos e, em seguida, anexá-los.


### <a name="attach-a-new-disk-tooa-vm"></a>Anexar um novo tooa de disco VM

Se você precisar apenas de um novo disco na sua VM, você pode usar o hello `az vm disk attach` comando.

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

### <a name="attach-an-existing-disk"></a>Anexar um disco existente 

Em muitos casos, você anexa discos que já foram criados. Você primeiro localizar a id do disco hello e, em seguida, passar esse toohello `az vm disk attach` comando. Olá, exemplo a seguir usa um disco criado com `az disk create -g myResourceGroup -n myDataDisk --size-gb 50`.

```azurecli
# find hello disk id
diskId=$(az disk show -g myResourceGroup -n myDataDisk --query 'id' -o tsv)
az vm disk attach -g myResourceGroup --vm-name myVM --disk $diskId
```

Olá saída parecida com hello seguinte (você pode usar o hello `-o table` opção tooany tooformat Olá saída do comando):

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


## <a name="attach-an-unmanaged-disk"></a>Anexar um disco não gerenciado

Anexar um novo disco é rápido se você não se importar a criação de um disco no hello mesma conta de armazenamento como sua VM. Tipo `azure vm disk attach-new` toocreate e anexar um novo disco GB para sua VM. Se você não identificar explicitamente uma conta de armazenamento, qualquer disco que você cria é colocado no hello mesma conta de armazenamento onde reside o disco do sistema operacional. Olá seguindo o exemplo anexa um `50`GB disco toohello VM denominada `myVM` no grupo de recursos de saudação chamado `myResourceGroup`:

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="connect-toohello-linux-vm-toomount-hello-new-disk"></a>Conecte-se toohello novo disco de VM do Linux toomount Olá
> [!NOTE]
> Este tópico se conecta tooa VM usando nomes de usuário e senhas. toouse toocommunicate de pares de chaves públicas e privadas com sua VM, consulte [como tooUse SSH com Linux no Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 
> 
> 

Você precisa tooSSH em toopartition sua VM do Azure, formatar e montar o novo disco para a VM do Linux podem usá-lo. Se você não estiver familiarizado com a conexão com **ssh**, comando Olá assume a forma de saudação `ssh <username>@<FQDNofAzureVM> -p <hello ssh port>`e Olá seguinte aparência:

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com -p 22
```

Saída

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

Agora que você está conectado tooyour VM, você está pronto tooattach um disco.  Primeiro localize Olá disco, usando `dmesg | grep SCSI` (método hello usar toodiscover o novo disco pode variar). Nesse caso, deve ser semelhante a:

```bash
dmesg | grep SCSI
```

Saída

```bash
[    0.294784] SCSI subsystem initialized
[    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
[    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
[    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
[ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
```

e no caso de Olá deste tópico, Olá `sdc` disco é hello que queremos. Agora partição Olá disco com `sudo fdisk /dev/sdc` - supondo que no seu caso Olá disco foi `sdc`e é um disco principal na partição 1 e aceitar Olá outros padrões.

```bash
sudo fdisk /dev/sdc
```

Saída

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

Criar partição Olá digitando `p` no prompt de saudação:

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

E gravar um sistema de arquivos toohello partição usando Olá **mkfs** comando, especificando o nome do dispositivo hello e de tipo de sistema de arquivos. Nesse tópico, estamos usando o `ext4` e o `/dev/sdc1` acima:

```bash
sudo mkfs -t ext4 /dev/sdc1
```

Saída

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

Agora podemos criar um diretório toomount Olá sistema de arquivos usando `mkdir`:

```bash
sudo mkdir /datadrive
```

E você montar Olá diretório usando `mount`:

```bash
sudo mount /dev/sdc1 /datadrive
```

disco de dados Olá agora está pronto toouse como `/datadrive`.

```bash
ls
```

Saída

```bash
bin   datadrive  etc   initrd.img  lib64       media  opt   root  sbin  sys  usr  vmlinuz
boot  dev        home  lib         lost+found  mnt    proc  run   srv   tmp  var
```

unidade de saudação tooensure é remontada automaticamente após uma reinicialização, que ele deve ser adicionado toohello /etc/fstab arquivo. Além disso, é altamente recomendável que Olá UUID (identificador universalmente exclusivo) é usado em /etc/hosts/unidade fstab toorefer toohello em vez do nome do dispositivo apenas hello (como `/dev/sdc1`). Se Olá SO detecta um erro de disco durante a inicialização, usar Olá UUID evita que está sendo montado tooa dado local de disco incorreta hello. Os discos de dados restantes seriam então atribuídos a essas mesmas IDs de dispositivo. toofind Olá UUID da unidade nova hello, use Olá **blkid** utilitário:

```bash
sudo -i blkid
```

saída de Hello tem a aparência a seguir toohello semelhante:

```bash
/dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
/dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

> [!NOTE]
> Edição incorretamente Olá **/etc/fstab** arquivo pode resultar em um sistema não inicializável. Se não tiver certeza, consulte a documentação do toohello da distribuição para obter informações sobre como tooproperly editar esse arquivo. Também é recomendável que um backup de arquivo /etc/fstab de saudação é criado antes de editar.
> 
> 

Em seguida, abra Olá **/etc/fstab** em um editor de texto:

```bash
sudo vi /etc/fstab
```

Neste exemplo, usamos Olá UUID valor para Olá novo **/desenvolvimento/sdc1** dispositivo que foi criado em etapas anteriores hello e ponto de montagem Olá **/datadrive**. Adicionar Olá após o final da linha toohello de saudação **/etc/fstab** arquivo:

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
```

> [!NOTE]
> Remover posteriormente um disco de dados sem editar fstab poderia causar Olá VM toofail tooboot. A maioria das distribuições fornecem qualquer Olá `nofail` e/ou `nobootwait` fstab opções. Essas opções permitem tooboot um sistema, mesmo se o disco de saudação falhar toomount no momento da inicialização. Consulte a documentação da distribuição para obter mais informações sobre esses parâmetros.
> 
> Olá **nofail** opção garante que Olá VM iniciado mesmo se Olá de sistema de arquivos está corrompido ou disco Olá não existe no momento da inicialização. Sem essa opção, você pode encontrar o comportamento conforme descrito em [não é possível SSH tooLinux VM devido a erros de tooFSTAB](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)

### <a name="trimunmap-support-for-linux-in-azure"></a>Suporte a TRIM/UNMAP para Linux no Azure
Suportam a alguns kernels Linux TRIM/DESMAPEAMENTO operações toodiscard blocos não usados no disco hello. Isso é útil principalmente no armazenamento padrão tooinform Azure que páginas excluídas não são mais válidas e podem ser descartadas. Isso poderá representar uma economia de dinheiro se você criar arquivos grandes e, em seguida, excluí-los.

Há duas maneiras tooenable TRIM suporte em sua VM do Linux. Como de costume, consulte a distribuição para Olá abordagem recomendada:

* Saudação de uso `discard` montar opção `/etc/fstab`, por exemplo:

    ```bash
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```
* Em alguns Olá casos `discard` opção pode ter implicações de desempenho. Como alternativa, você pode executar Olá `fstrim` comando manualmente da linha de comando hello, ou adicionar tooyour crontab toorun regularmente:
  
    **Ubuntu**
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    **RHEL/CentOS**

    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a>Solucionar problemas
[!INCLUDE [virtual-machines-linux-lunzero](../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a>Próximas etapas
* Lembre-se de que o novo disco não é disponível toohello VM se ele for reinicializado, a menos que você escreve que tooyour informações [fstab](http://en.wikipedia.org/wiki/Fstab) arquivo.
* tooensure sua VM do Linux é configurado corretamente, examinar Olá [otimizar o desempenho do computador Linux](optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) recomendações.
* Expanda a capacidade de armazenamento adicionando mais discos e [configure o RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obter desempenho adicional.

