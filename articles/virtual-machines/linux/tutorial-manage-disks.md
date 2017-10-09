---
title: aaaManage Azure discos com hello CLI do Azure | Microsoft Docs
description: Tutorial - gerenciar discos do Azure com hello CLI do Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: ad29cfbec5f9738f47705b19d0450c9a2f555492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-hello-azure-cli"></a>Gerenciar discos do Azure com hello CLI do Azure

Máquinas virtuais do Azure usam o sistema operacional do discos toostore Olá VMs, aplicativos e dados. Ao criar uma VM é importante toochoose um tamanho de disco e carga de trabalho de configuração apropriado toohello esperado. Este tutorial aborda a implantação e gerenciamento de discos de VM. Você saberá mais sobre:

> [!div class="checklist"]
> * Discos de sistema operacional e discos temporários
> * Discos de dados
> * Discos Standard e Premium
> * Desempenho do disco
> * Anexar e preparar os discos de dados
> * Redimensionamento de discos
> * Instantâneos de disco


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este tutorial requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="default-azure-disks"></a>Discos padrão do Azure

Quando uma máquina virtual do Azure é criada, dois discos são automaticamente anexados toohello máquina de virtual. 

**Disco do sistema operacional** - discos do sistema operacional podem ser dimensionados para cima too1 terabyte e hosts Olá sistema operacional de máquinas virtuais. Olá OS disco é chamado */desenvolvimento/sda* por padrão. configuração de disco do sistema operacional de saudação de cache de disco de saudação é otimizado para desempenho do sistema operacional. Devido a essa configuração, Olá disco do sistema operacional **não devem** hospedar aplicativos ou dados. Para aplicativos e dados, utilize um disco de dados, que é detalhado posteriormente neste artigo. 

**Disco temporário** -discos temporários usam uma unidade de estado sólido está localizada em Olá mesmo host do Azure como Olá VM. Os discos temporários são altamente eficazes e podem ser usados para operações como o processamento de dados temporário. No entanto, se Olá VM for movida tooa novo host, todos os dados armazenados em um disco temporário são removidos. tamanho de saudação do disco temporário Olá é determinado pelo Olá tamanho da VM. Os discos temporários são rotulados */dev/sdb* e têm um ponto de montagem de */mnt*.

### <a name="temporary-disk-sizes"></a>Tamanhos do disco temporário

| Tipo | Tamanho da VM | Tamanho máximo do disco temporário (GB) |
|----|----|----|
| [Propósito geral](sizes-general.md) | Série A e D | 800 |
| [Computação otimizada](sizes-compute.md) | Série F | 800 |
| [Memória otimizada](../virtual-machines-windows-sizes-memory.md) | Série D e G | 6144 |
| [Armazenamento otimizado](../virtual-machines-windows-sizes-storage.md) | Série L | 5630 |
| [GPU](sizes-gpu.md) | Série N | 1440 |
| [Alto desempenho](sizes-hpc.md) | Séries A e H | 2000 |

## <a name="azure-data-disks"></a>Discos de dados do Azure

Os discos de dados extras podem ser adicionados para instalação de aplicativos e armazenamento de dados. Os discos de dados devem ser usados em qualquer situação onde o armazenamento de dados durável e responsivo é desejado. Cada disco de dados tem uma capacidade máxima de 1 terabyte. Olá tamanho da saudação máquina virtual determina quantos discos de dados podem ser anexado tooa VM. Para cada núcleo da VM, podem ser anexados dois discos de dados. 

### <a name="max-data-disks-per-vm"></a>Máximo de discos de dados por VM

| Tipo | Tamanho da VM | Máximo de discos de dados por VM |
|----|----|----|
| [Propósito geral](sizes-general.md) | Série A e D | 32 |
| [Computação otimizada](sizes-compute.md) | Série F | 32 |
| [Memória otimizada](../virtual-machines-windows-sizes-memory.md) | Série D e G | 64 |
| [Armazenamento otimizado](../virtual-machines-windows-sizes-storage.md) | Série L | 64 |
| [GPU](sizes-gpu.md) | Série N | 48 |
| [Alto desempenho](sizes-hpc.md) | Série A e H | 32 |

## <a name="vm-disk-types"></a>Tipos de disco da máquina virtual

O Azure fornece dois tipos de disco.

### <a name="standard-disk"></a>Disco Standard

Armazenamento padrão é apoiado por HDDs e oferece armazenamento econômico e eficaz. Os discos Standard são ideais para uma carga de trabalho econômica de desenvolvimento e teste.

### <a name="premium-disk"></a>Disco Premium

Os discos Premium são apoiados por disco de baixa latência e alto desempenho baseado em SSD. Perfeitos para VMs que executam carga de trabalho de produção. O Armazenamento Premium dá suporte às VMs das séries DS, DSv2, GS e FS. Discos Premium vêm em três tipos (P10, P20, P30), o tamanho de saudação do disco de saudação determina o tipo de disco de saudação. Selecionar um valor de saudação do tamanho de disco é arredondado até o próximo tipo de toohello. Por exemplo, se o tamanho do disco Olá é menos de 128 GB, o tipo de disco Olá é P10. Se o tamanho do disco Olá estiver entre 129 e 512 GB, o tamanho de saudação é um P20. Nada mais de 512 GB, o tamanho de saudação é um P30.

### <a name="premium-disk-performance"></a>Desempenho do disco Premium

|Tipo de disco de armazenamento Premium | P10 | P20 | P30 |
| --- | --- | --- | --- |
| Tamanho do disco (arredondado) | 128 GB | 512 GB | 1.024 GB (1 TB) |
| IOPS máxima por disco | 500 | 2.300 | 5.000 |
Taxa de transferência por disco | 100 MB/s | 150 MB/s | 200 MB/s |

Enquanto Olá acima tabela identifica o IOPS máximo por disco, um nível mais alto de desempenho pode ser obtido com a distribuição de vários discos de dados. Por exemplo, uma VM Standard_GS5 pode atingir o máximo de 80.000 IOPS. Para obter informações detalhadas sobre o máximo de IOPS por VM, veja [Tamanhos da VM Linux](sizes.md).

## <a name="create-and-attach-disks"></a>Criar e anexar discos

Discos de dados podem ser criados e anexados no momento da criação da VM ou tooan existente de VM.

### <a name="attach-disk-at-vm-creation"></a>Anexar disco na criação da VM

Criar um grupo de recursos com hello [criar grupo az](https://docs.microsoft.com/cli/azure/group#create) comando. 

```azurecli-interactive 
az group create --name myResourceGroupDisk --location eastus
```

Criar uma VM usando Olá [criar vm az]( /cli/azure/vm#create) comando. Olá `--datadisk-sizes-gb` argumento é usado toospecify que um disco adicional deve ser criado e anexado a máquina virtual de toohello. toocreate e anexar mais de um disco, use uma lista delimitada por espaço dos valores de tamanho de disco. Saudação de exemplo a seguir, uma máquina virtual é criada com discos de dados de dois, ambos os 128 GB. Como os tamanhos de disco Olá 128 GB, ambos esses discos são configurados como P10s, que fornecem o IOPS máximo de 500 por disco.

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupDisk \
  --name myVM \
  --image UbuntuLTS \
  --size Standard_DS2_v2 \
  --data-disk-sizes-gb 128 128 \
  --generate-ssh-keys
```

### <a name="attach-disk-tooexisting-vm"></a>Anexar disco tooexisting VM

toocreate e anexar uma novo disco tooan máquina virtual existente, use Olá [anexar disco de vm az](/cli/azure/vm/disk#attach) comando. Olá exemplo a seguir cria um disco premium, 128 gigabytes de tamanho e anexa toohello que VM criada na última etapa do hello.

```azurecli-interactive 
az vm disk attach --vm-name myVM --resource-group myResourceGroupDisk --disk myDataDisk --size-gb 128 --sku Premium_LRS --new 
```

## <a name="prepare-data-disks"></a>Preparar discos de dados

Depois que um disco tenha sido anexado toohello máquina de virtual, o sistema de operacional de saudação precisa toobe configurado toouse Olá disco. saudação de exemplo a seguir mostra como toomanually configurar um disco. Esse processo também pode ser automatizado utilizando a inicialização por nuvem, que é abordada em um [tutorial posterior](./tutorial-automate-vm-deployment.md).

### <a name="manual-configuration"></a>Configuração manual

Crie uma conexão SSH com a máquina virtual de saudação. Substitua o endereço IP de exemplo hello com IP público de saudação da máquina virtual de saudação.

```azurecli-interactive 
ssh 52.174.34.95
```

Partição de disco Olá com `fdisk`.

```bash
(echo n; echo p; echo 1; echo ; echo ; echo w) | sudo fdisk /dev/sdc
```

Gravar um sistema de arquivos toohello partição usando Olá `mkfs` comando.

```bash
sudo mkfs -t ext4 /dev/sdc1
```

Monte o novo disco de saudação para que seja acessível no sistema operacional de saudação.

```bash
sudo mkdir /datadrive && sudo mount /dev/sdc1 /datadrive
```

disco Olá agora pode ser acessado por meio de saudação *datadrive* ponto de montagem, o que pode ser verificado executando Olá `df -h` comando. 

```bash
df -h
```

saída de Hello mostra a nova unidade de saudação montada em */datadrive*.

```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        30G  1.4G   28G   5% /
/dev/sdb1       6.8G   16M  6.4G   1% /mnt
/dev/sdc1        50G   52M   47G   1% /datadrive
```

tooensure que Olá unidade é remontado após uma reinicialização, ela deve ser adicionada toohello */etc/fstab* arquivo. toodo fique saudação UUID de disco Olá Olá `blkid` utilitário.

```bash
sudo -i blkid
```

saída de Hello exibe Olá UUID da unidade hello, `/dev/sdc1` nesse caso.

```bash
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

Adicionar um toohello semelhante de linha a seguir toohello */etc/fstab* arquivo. Observe também que as barreiras de gravação podem ser desabilitadas utilizando *barrier=0*, essa configuração pode melhorar o desempenho do disco. 

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive  ext4    defaults,nofail,barrier=0   1  2
```

Agora que hello disco tiver sido configurado, feche a sessão SSH de saudação.

```bash
exit
```

## <a name="resize-vm-disk"></a>Redimensionar o disco da máquina virtual

Quando uma máquina virtual tiver sido implantada, disco de saudação do sistema operacional ou discos de dados anexados podem ser aumentados em tamanho. Aumentando o tamanho de saudação de um disco é benéfico quando precisar de mais espaço de armazenamento ou um nível mais alto de desempenho (P10, P20, P30). Observe que discos não podem ser reduzidos.

Antes de aumentar o tamanho do disco, Olá Id ou nome do disco Olá é necessária. Saudação de uso [lista de discos az](/cli/azure/vm/disk#list) comando tooreturn todos os discos em um grupo de recursos. Anote o nome do disco Olá que deseja tooresize.

```azurecli-interactive 
az disk list -g myResourceGroupDisk --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' --output table
```

Olá VM também deve ser desalocada. Saudação de uso [az vm desalocar]( /cli/azure/vm#deallocate) toostop de comando e desalocar Olá VM.

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupDisk --name myVM
```

Saudação de uso [atualização de disco az](/cli/azure/vm/disk#update) disco de saudação do comando tooresize. Este exemplo redimensiona um disco chamado *myDataDisk* too1 terabyte.

```azurecli-interactive 
az disk update --name myDataDisk --resource-group myResourceGroupDisk --size-gb 1023
```

Após a conclusão da operação de redimensionamento hello, inicie Olá VM.

```azurecli-interactive 
az vm start --resource-group myResourceGroupDisk --name myVM
```

Se você tiver redimensionado Olá operacional do disco do sistema, partição Olá automaticamente é expandido. Se você tiver redimensionado um disco de dados, todas as partições atuais necessário toobe expandido no sistema de operacional Olá VMs.

## <a name="snapshot-azure-disks"></a>Discos padrão do Azure

Tirar um instantâneo do disco cria uma cópia apenas, point-in-time leitura de disco de saudação. Instantâneos VM do Azure são úteis para salvar rapidamente o estado de saudação de uma VM antes de fazer alterações de configuração. No evento Olá Olá, alterações de configuração provam toobe maneira indesejada, estado da VM pode ser restaurado usando Olá instantâneo. Quando uma VM tem mais de um disco, um instantâneo é tirado de cada disco independentemente Olá outras pessoas. Para fazer backups consistentes com aplicativos, considere a possibilidade de interrupção Olá VM antes de tirar instantâneos de disco. Como alternativa, use Olá [serviço de Backup do Azure](/azure/backup/), que permite que você tooperform automatizada backups durante a saudação VM está em execução.

### <a name="create-snapshot"></a>Como criar um instantâneo

Antes de criar um instantâneo do disco de máquina virtual, hello Id ou nome do disco Olá é necessário. Saudação de uso [Mostrar de vm az](https://docs.microsoft.com/en-us/cli/azure/vm#show) id do disco de saudação do comando tooreturn. Neste exemplo, a id do disco Olá é armazenado em uma variável para que ele pode ser usado em uma etapa posterior.

```azurecli-interactive 
osdiskid=$(az vm show -g myResourceGroupDisk -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
```

Agora que você tem a id de saudação do disco da máquina virtual hello, hello comando a seguir cria um instantâneo do disco hello.

```azurcli
az snapshot create -g myResourceGroupDisk --source "$osdiskid" --name osDisk-backup
```

### <a name="create-disk-from-snapshot"></a>Como criar o disco a partir de um instantâneo

Esse instantâneo, em seguida, pode ser convertido em um disco, o que pode ser usado toorecreate Olá VM.

```azurecli-interactive 
az disk create --resource-group myResourceGroupDisk --name mySnapshotDisk --source osDisk-backup
```

### <a name="restore-virtual-machine-from-snapshot"></a>Como restaurar a máquina virtual a partir de um instantâneo

recuperação de máquina virtual toodemonstrate, máquina virtual existente de saudação delete. 

```azurecli-interactive 
az vm delete --resource-group myResourceGroupDisk --name myVM
```

Crie uma nova máquina virtual do disco de instantâneo hello.

```azurecli-interactive 
az vm create --resource-group myResourceGroupDisk --name myVM --attach-os-disk mySnapshotDisk --os-type linux
```

### <a name="reattach-data-disk"></a>Reanexar um disco de dados

Todos os discos de dados necessário toobe reanexado toohello VM.

Localizar primeiro nome do disco de dados hello usando Olá [lista de discos az](https://docs.microsoft.com/cli/azure/disk#list) comando. Este exemplo coloca Olá nome do disco de saudação em uma variável chamada *datadisk*, que é usada na próxima etapa do hello.

```azurecli-interactive 
datadisk=$(az disk list -g myResourceGroupDisk --query "[?contains(name,'myVM')].[name]" -o tsv)
```

Saudação de uso [anexar disco de vm az](https://docs.microsoft.com/cli/azure/vm/disk#attach) disco de saudação do comando tooattach.

```azurecli-interactive 
az vm disk attach –g myResourceGroupDisk –-vm-name myVM –-disk $datadisk
```

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu sobre tópicos de discos da VM como:

> [!div class="checklist"]
> * Discos de sistema operacional e discos temporários
> * Discos de dados
> * Discos Standard e Premium
> * Desempenho do disco
> * Anexar e preparar os discos de dados
> * Redimensionamento de discos
> * Instantâneos de disco

Avançar toohello toolearn próximo de tutorial sobre como automatizar a configuração da VM.

> [!div class="nextstepaction"]
> [Automatizar a configuração da VM](./tutorial-automate-vm-deployment.md)
