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
# <a name="configure-lvm-on-a-linux-vm-in-azure"></a>Configurar o LVM em uma VM Linux no Azure
Este documento descreverá como tooconfigure Gerenciador de Volume lógico (LVM) em sua máquina virtual do Azure. Embora seja possível tooconfigure que LVM em qualquer disco anexado máquina virtual de toohello, por padrão nuvem a maioria das imagens não terá LVM configurado no hello disco do sistema operacional. Isso é tooprevent problemas com grupos de volumes duplicados se Olá disco do sistema operacional já está anexado tooanother VM de saudação mesmo distribuição e o tipo, por exemplo, durante um cenário de recuperação. Portanto, é recomendável somente toouse LVM em discos de dados de saudação.

## <a name="linear-vs-striped-logical-volumes"></a>Volumes lógicos lineares versus lógicos distribuídos
LVM pode ser usado toocombine um número de discos físicos em um único volume de armazenamento. Por padrão LVM geralmente cria volumes lógicos lineares, o que significa que armazenamento físico de saudação é concatenado. Nesse caso as operações de leitura/gravação normalmente só funcionará tooa único disco. Em contrapartida, também podemos criar volumes lógicos distribuídos onde leituras e gravações estão distribuídas toomultiple discos contidos no grupo de volumes hello (ou seja, tooRAID0 semelhante). Por motivos de desempenho, é provável que você desejará toostripe seus volumes lógicos para que as leituras e gravações utilizam todos os discos de dados anexado.

Este documento descrevem como toocombine vários discos de dados em um único grupo de volumes e, em seguida, criar um volume lógico distribuído. Olá etapas a seguir são um pouco generalizado toowork com a maioria das distribuições. Na saudação de casos a maioria dos utilitários e fluxos de trabalho para gerenciar LVM no Azure não são fundamentalmente diferentes de outros ambientes. Como de costume, também consulte o fornecedor do Linux para obter documentação e práticas recomendadas para usar o LVM com sua distribuição específica.

## <a name="attaching-data-disks"></a>Anexando discos de dados
Um geralmente desejará toostart com dois ou mais discos de dados vazios ao usar LVM. Com base em suas necessidades de e/s, você pode escolher tooattach discos que são armazenados em nosso armazenamento padrão, com a e/s too500/ps por armazenamento em disco ou nosso Premium com a e/s too5000/ps por disco. Este artigo não entra em detalhes sobre como tooprovision e anexar a máquina de virtual do Linux de tooa de discos de dados. Consulte artigo do Microsoft Azure Olá [anexar um disco](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obter instruções detalhadas sobre como tooattach um dados vazios disco tooa máquina de virtual do Linux no Azure.

## <a name="install-hello-lvm-utilities"></a>Instalar utilitários LVM Olá
* **Ubuntu**

    ```bash  
    sudo apt-get update
    sudo apt-get install lvm2
    ```

* **RHEL, CentOS e Oracle Linux**

    ```bash   
    sudo yum install lvm2
    ```

* **SLES 12 e openSUSE**

    ```bash   
    sudo zypper install lvm2
    ```

* **SLES 11**

    ```bash   
    sudo zypper install lvm2
    ```

    Em SLES11 também será necessário editar `/etc/sysconfig/lvm` e defina `LVM_ACTIVATED_ON_DISCOVERED` muito "Habilitar":

    ```sh   
    LVM_ACTIVATED_ON_DISCOVERED="enable" 
    ```

## <a name="configure-lvm"></a>Configurar o LVM
Este guia assumiremos você anexou três discos de dados, vamos analisar tooas `/dev/sdc`, `/dev/sdd` e `/dev/sde`. Observe que não podem ser sempre Olá mesmos nomes de caminho na sua VM. Você pode executar o '`sudo fdisk -l`' ou toolist semelhante do comando os discos disponíveis.

1. Prepare volumes físicos hello:

    ```bash    
    sudo pvcreate /dev/sd[cde]
    Physical volume "/dev/sdc" successfully created
    Physical volume "/dev/sdd" successfully created
    Physical volume "/dev/sde" successfully created
    ```

2. Crie um grupo de volumes. Neste exemplo estamos ligando para o grupo de volumes Olá `data-vg01`:

    ```bash    
    sudo vgcreate data-vg01 /dev/sd[cde]
    Volume group "data-vg01" successfully created
    ```

3. Crie volumes lógicos de saudação. Olá comando abaixo, criará um único volume lógico chamado `data-lv01` toospan Olá todo o grupo de volumes, mas observe que também é possível toocreate vários volumes lógicos em um grupo de volumes de saudação.

    ```bash   
    sudo lvcreate --extents 100%FREE --stripes 3 --name data-lv01 data-vg01
    Logical volume "data-lv01" created.
    ```

4. Formatar o volume lógico da saudação

    ```bash  
    sudo mkfs -t ext4 /dev/data-vg01/data-lv01
    ```
   
   > [!NOTE]
   > Com o SLES11, use `-t ext3` em vez de ext4. SLES11 só oferece suporte a sistemas de arquivos de tooext4 acesso somente leitura.

## <a name="add-hello-new-file-system-tooetcfstab"></a>Adicionar Olá novo arquivo sistema muito/etc/fstab
> [!IMPORTANT]
> Edição incorretamente Olá `/etc/fstab` arquivo pode resultar em um sistema não inicializável. Se não tiver certeza, consulte a documentação da distribuição toohello para obter informações sobre como tooproperly editar esse arquivo. Também é recomendável que um backup de saudação `/etc/fstab` arquivo é criado antes de editar.

1. Crie ponto de montagem de saudação desejado para o novo sistema de arquivos, por exemplo:

    ```bash  
    sudo mkdir /data
    ```

2. Localize o caminho do volume lógico Olá

    ```bash    
    lvdisplay
    --- Logical volume ---
    LV Path                /dev/data-vg01/data-lv01
    ....
    ```

3. Abra `/etc/fstab` em um editor de texto e adicione uma entrada para o novo sistema de arquivos hello, por exemplo:

    ```bash    
    /dev/data-vg01/data-lv01  /data  ext4  defaults  0  2
    ```   
    Em seguida, salve e feche o `/etc/fstab`.

4. Testar esse Olá `/etc/fstab` entrada está correta:

    ```bash    
    sudo mount -a
    ```

    Se esse comando resulta em uma mensagem de erro, verifique a sintaxe Olá Olá `/etc/fstab` arquivo.
   
    Em seguida execute Olá `mount` montado sistema de arquivos do comando tooensure hello:

    ```bash    
    mount
    ......
    /dev/mapper/data--vg01-data--lv01 on /data type ext4 (rw)
    ```

5. (Opcional) Parâmetros de inicialização à prova de falhas em `/etc/fstab`
   
    Muitas distribuições incluem qualquer Olá `nobootwait` ou `nofail` montar os parâmetros que podem ser adicionados toohello `/etc/fstab` arquivo. Esses parâmetros permitem falhas ao montar um sistema de arquivos específico e permitem Olá Linux sistema toocontinue tooboot mesmo se ele for o sistema de arquivos do tooproperly não é possível montar Olá RAID. Consulte a documentação da distribuição tooyour para obter mais informações sobre esses parâmetros.
   
    Exemplo (Ubuntu):

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,nobootwait  0  2
    ```

## <a name="trimunmap-support"></a>Suporte a TRIM/UNMAP
Suportam a alguns kernels Linux TRIM/DESMAPEAMENTO operações toodiscard blocos não usados no disco hello. Essas operações são principalmente útil no armazenamento padrão tooinform Azure que páginas excluídas não são mais válidas e podem ser descartadas. Descartar páginas poderá representar uma economia de dinheiro se você criar arquivos grandes e, em seguida, excluí-los.

Há duas maneiras tooenable TRIM suporte em sua VM do Linux. Como de costume, consulte a distribuição para Olá abordagem recomendada:

- Saudação de uso `discard` montar opção `/etc/fstab`, por exemplo:

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,discard  0  2
    ```

- Em alguns Olá casos `discard` opção pode ter implicações de desempenho. Como alternativa, você pode executar Olá `fstrim` comando manualmente da linha de comando hello, ou adicionar tooyour crontab toorun regularmente:

    **Ubuntu**

    ```bash 
    # sudo apt-get install util-linux
    # sudo fstrim /datadrive
    ```

    **RHEL/CentOS**

    ```bash 
    # sudo yum install util-linux
    # sudo fstrim /datadrive
    ```
