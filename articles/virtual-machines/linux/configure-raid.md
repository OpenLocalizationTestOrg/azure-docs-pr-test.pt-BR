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
# <a name="configure-software-raid-on-linux"></a>Configurar RAID de software no Linux
É um software de toouse cenário comum RAID em máquinas virtuais Linux no Azure toopresent dados anexados vários discos como um único dispositivo RAID. Normalmente isso pode ser usado tooimprove desempenho e permitir melhor taxa de transferência em comparação com toousing apenas um único disco.

## <a name="attaching-data-disks"></a>Anexando discos de dados
Dois ou mais discos de dados vazios são necessário tooconfigure um dispositivo RAID.  Olá principal motivo para a criação de um dispositivo RAID é tooimprove o desempenho do disco e/s.  Com base em suas necessidades de e/s, você pode escolher tooattach discos que são armazenados em nosso armazenamento padrão, com a e/s too500/ps por armazenamento em disco ou nosso Premium com a e/s too5000/ps por disco. Este artigo não entrar em detalhes sobre como tooprovision e anexar a máquina de virtual do Linux de tooa de discos de dados.  Consulte o artigo do Microsoft Azure Olá [anexar um disco](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obter instruções detalhadas sobre como tooattach um dados vazios disco tooa máquina de virtual do Linux no Azure.

## <a name="install-hello-mdadm-utility"></a>Instalar Olá mdadm utility
* **Ubuntu**
```bash
sudo apt-get update
sudo apt-get install mdadm
```

* **CentOS & Oracle Linux**
```bash
sudo yum install mdadm
```

* **SLES e openSUSE**
```bash  
zypper install mdadm
```

## <a name="create-hello-disk-partitions"></a>Criar hello partições de disco
Neste exemplo, criamos uma única partição de disco em /dev/sdc. nova partição de disco Olá será chamada /dev/sdc1.

1. Iniciar `fdisk` toobegin a criação de partições

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

2. Pressione ' n' no toocreate prompt Olá um  **n** partição nova:

    ```bash
    Command (m for help): n
    ```

3. Em seguida, pressione 'p' toocreate um **p**rimário partição:

    ```bash 
    Command action
            e   extended
            p   primary partition (1-4)
    ```

4. Pressione '1' tooselect partição número 1:

    ```bash
    Partition number (1-4): 1
    ```

5. Selecione Olá ponto de partida da saudação nova partição, ou pressione `<enter>` tooaccept saudação padrão tooplace Olá partição de início de saudação do espaço livre Olá unidade hello:

    ```bash   
    First cylinder (1-1305, default 1):
    Using default value 1
    ```

6. Selecione o tamanho de saudação da partição hello, por exemplo '+10G' do tipo toocreate uma partição de 10 GB. Ou pressione `<enter>` criar uma única partição que abrange toda a unidade hello:

    ```bash   
    Last cylinder, +cylinders or +size{K,M,G} (1-1305, default 1305): 
    Using default value 1305
    ```

7. Em seguida, alterar a ID de saudação e **t**ID de tipo de partição de saudação do padrão de saudação '83' (Linux) tooID 'fd' (Linux automática de raid):

    ```bash  
    Command (m for help): t
    Selected partition 1
    Hex code (type L toolist codes): fd
    ```

8. Por fim, gravar toohello unidade da tabela de partição hello e sair do fdisk:

    ```bash   
    Command (m for help): w
    hello partition table has been altered!
    ```

## <a name="create-hello-raid-array"></a>Criar hello RAID matriz
1. Olá será de exemplo "distribuição" (nível RAID 0) três partições localizadas em três discos de dados separados (sdc1, sdd1, sde1) a seguir.  Depois da execução desse comando, um novo dispositivo RAID chamado **/dev/md127** é criado. Observe também que se esses discos de dados, anteriormente parte de outro conjunto RAID expirado pode ser necessário tooadd Olá `--force` toohello parâmetro `mdadm` comando:

    ```bash  
    sudo mdadm --create /dev/md127 --level 0 --raid-devices 3 \
        /dev/sdc1 /dev/sdd1 /dev/sde1
    ```

2. Criar o sistema de arquivos Olá no novo dispositivo RAID Olá
   
    a. **CentOS, Oracle Linux, SLES 12, openSUSE e Ubuntu**

    ```bash   
    sudo mkfs -t ext4 /dev/md127
    ```
   
    b. **SLES 11**

    ```bash
    sudo mkfs -t ext3 /dev/md127
    ```
   
    c. **SLES 11** – habilite boot.md e crie mdadm.conf

    ```bash
    sudo -i chkconfig --add boot.md
    sudo echo 'DEVICE /dev/sd*[0-9]' >> /etc/mdadm.conf
    ```
   
   > [!NOTE]
   > Pode ser necessária uma reinicialização depois de fazer essas alterações em sistemas SUSE. Esta etapa *não* é necessária no SLES 12.
   > 
   > 

## <a name="add-hello-new-file-system-tooetcfstab"></a>Adicionar Olá novo arquivo sistema muito/etc/fstab
> [!IMPORTANT]
> Edição incorretamente arquivo /etc/fstab de saudação pode resultar em um sistema não inicializável. Se não tiver certeza, consulte a documentação do toohello da distribuição para obter informações sobre como tooproperly editar esse arquivo. Também é recomendável que um backup de arquivo /etc/fstab de saudação é criado antes de editar.

1. Crie ponto de montagem de saudação desejado para o novo sistema de arquivos, por exemplo:

    ```bash
    sudo mkdir /data
    ```
2. Ao editar /etc/fstab, Olá **UUID** deve ser usado tooreference Olá sistema em vez de saudação dispositivo nome de arquivo.  Saudação de uso `blkid` Olá UUID do toodetermine utilitário para o novo sistema de arquivos hello:

    ```bash   
    sudo /sbin/blkid
    ...........
    /dev/md127: UUID="aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee" TYPE="ext4"
    ```

3. Abra /etc/fstab em um editor de texto e adicione uma entrada para o novo sistema de arquivos hello, por exemplo:

    ```bash   
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults  0  2
    ```
   
    Ou no **SLES 11**:

    ```bash
    /dev/disk/by-uuid/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext3  defaults  0  2
    ```
   
    Em seguida, salve e feche o /etc/fstab.

4. Teste se Olá /etc/fstab entrada está correta:

    ```bash  
    sudo mount -a
    ```

    Se esse comando resulta em uma mensagem de erro, verifique a sintaxe Olá no arquivo /etc/fstab de saudação.
   
    Em seguida execute Olá `mount` montado sistema de arquivos do comando tooensure hello:

    ```bash   
    mount
    .................
    /dev/md127 on /data type ext4 (rw)
    ```

5. (Opcional) Parâmetros de inicialização à prova de falhas
   
    **configuração fstab**
   
    Muitas distribuições incluem qualquer Olá `nobootwait` ou `nofail` parâmetros que podem ser adicionados toohello/etc/fstab arquivo de montagem. Esses parâmetros permitem falhas ao montar um sistema de arquivos específico e permitem Olá Linux sistema toocontinue tooboot mesmo se ele for o sistema de arquivos do tooproperly não é possível montar Olá RAID. Para obter mais informações sobre esses parâmetros, consulte a documentação do tooyour da distribuição.
   
    Exemplo (Ubuntu):

    ```bash  
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,nobootwait  0  2
    ```   

    **Parâmetros de inicialização do Linux**
   
    Em adição toohello acima parâmetros, Olá parâmetro kernel "`bootdegraded=true`" pode permitir Olá tooboot de sistema, mesmo se Olá RAID é percebido como danificado ou degradado, por exemplo, se uma unidade de dados for removida inadvertidamente da máquina virtual de saudação. Por padrão, isso também pode resultar em um sistema não inicializável.
   
    Consulte a documentação da distribuição tooyour em como tooproperly Editar parâmetros de kernel. Por exemplo, em muitas distribuições (CentOS, Oracle Linux, SLES 11) esses parâmetros podem ser adicionados manualmente toohello "`/boot/grub/menu.lst`" arquivo.  No Ubuntu esse parâmetro pode ser adicionado toohello `GRUB_CMDLINE_LINUX_DEFAULT` variável em "/ padrão/etc/grub".


## <a name="trimunmap-support"></a>Suporte a TRIM/UNMAP
Suportam a alguns kernels Linux TRIM/DESMAPEAMENTO operações toodiscard blocos não usados no disco hello. Essas operações são principalmente útil no armazenamento padrão tooinform Azure que páginas excluídas não são mais válidas e podem ser descartadas. Descartar páginas poderá representar uma economia de dinheiro se você criar arquivos grandes e, em seguida, excluí-los.

> [!NOTE]
> RAID não pode emitir comandos de descarte se o tamanho da parte Olá para matriz de saudação é definido tooless padrão hello (512KB). Isso ocorre porque Olá desmapeamento granularidade em Olá Host também é 512KB. Se você modificou o tamanho da parte da matriz Olá por meio do mdadm `--chunk=` parâmetro e TRIM/desmapeamento solicitações podem ser ignoradas pelo kernel hello.

Há duas maneiras tooenable TRIM suporte em sua VM do Linux. Como de costume, consulte a distribuição para Olá abordagem recomendada:

- Saudação de uso `discard` montar opção `/etc/fstab`, por exemplo:

    ```bash
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,discard  0  2
    ```

- Em alguns Olá casos `discard` opção pode ter implicações de desempenho. Como alternativa, você pode executar Olá `fstrim` comando manualmente da linha de comando hello, ou adicionar tooyour crontab toorun regularmente:

    **Ubuntu**

    ```bash
    # sudo apt-get install util-linux
    # sudo fstrim /data
    ```

    **RHEL/CentOS**
    ```bash
    # sudo yum install util-linux
    # sudo fstrim /data
    ```
