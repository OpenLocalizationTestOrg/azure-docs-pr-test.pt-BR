---
title: aaaAttach tooa um disco VM do Linux no Azure | Microsoft Docs
description: "Saiba como tooattach dados de um disco tooa VM Linux usando Olá clássico implantação de modelo e inicializar disco Olá para que esteja pronta para uso"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4901384d-2a6f-4f46-bba0-337a348b7f87
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: c76d8479ac2b522d2b6df658cd28f242473f30ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-virtual-machine"></a>Como tooAttach tooa um disco de dados Máquina Virtual do Linux
> [!IMPORTANT] 
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. Consulte como muito[anexar um disco de dados usando o modelo de implantação do Gerenciador de recursos de saudação](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Você pode anexar discos vazios e discos que contêm dados tooyour VMs do Azure. Ambos os tipos de discos são arquivos .vhd que residem em uma conta de armazenamento do Azure. Como com a adição de qualquer computador Linux de tooa de disco, depois que você anexar o disco Olá você precisa tooinitialize e formatá-lo para que ele está pronto para uso. Este artigo detalha anexar discos vazios e discos que já contém dados tooyour VMs, bem como toothen inicializar e formatar um novo disco.

> [!NOTE]
> É um toouse de prática recomendada, uma ou mais separados discos toostore dados de uma máquina virtual. Quando você cria uma máquina virtual Azure, há um disco do sistema operacional e um disco temporário. **Não use dados persistentes do toostore Olá disco temporário.** Como Olá nome sugere, ele fornece armazenamento temporário apenas. Não oferece redundância nem backup porque eles não residem no armazenamento do Azure.
> disco temporário Olá é normalmente gerenciado pelo Olá agente Linux do Azure e montado automaticamente muito**/mnt/Retention/ recurso** (ou **/mnt** no Ubuntu imagens). Em Olá outro lado, um disco de dados pode ser chamado pelo kernel do Linux Olá algo como `/dev/sdc`, e você precisa toopartition, formatar e montar este recurso. Consulte Olá [guia do usuário do Azure Linux Agent] [ Agent] para obter detalhes.
> 
> 

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-linux.md)]

## <a name="initialize-a-new-data-disk-in-linux"></a>Inicializar um novo disco de dados no Linux
1. SSH tooyour VM. Para obter mais informações, consulte [como toolog na máquina virtual de tooa executando o Linux][Logon].
2. Em seguida, você precisa identificador de dispositivo toofind Olá para Olá tooinitialize de disco de dados. Há dois toodo de maneiras que:
   
    a) logs de Grep para dispositivos SCSI hello, como Olá comando a seguir:
   
    ```bash
    sudo grep SCSI /var/log/messages
    ```
   
    Para distribuições Ubuntu recentes, talvez seja necessário toouse `sudo grep SCSI /var/log/syslog` porque o registro em log muito`/var/log/messages` pode ser desabilitado por padrão.
   
    Você pode encontrar o identificador Olá Olá última do disco de dados que foi adicionado em mensagens de saudação que são exibidas.
   
    ![Obter mensagens de saudação do disco](./media/attach-disk/scsidisklog.png)
   
    OU
   
    b) Olá usar `lsscsi` toofind comando out id do dispositivo hello. `lsscsi` pode ser instalado pelo `yum install lsscsi` (no Red Hat com base em distribuições) ou `apt-get install lsscsi` (no Debian distribuições de base). Você pode localizar o disco Olá procurando pelo seu *lun* ou **número de unidade lógica**. Por exemplo, Olá *lun* para discos Olá anexado podem ser vistos facilmente em `azure vm disk list <virtual-machine>` como:

    ```azurecli
    azure vm disk list myVM
    ```

    saída de Hello é a seguir toohello semelhante:

    ```azurecli
    info:    Executing command vm disk list
    + Fetching disk images
    + Getting virtual machines
    + Getting VM disks
    data:    Lun  Size(GB)  Blob-Name                         OS
    data:    ---  --------  --------------------------------  -----
    data:         30        myVM-2645b8030676c8f8.vhd  Linux
    data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
    info:    vm disk list command OK
    ```
   
    Comparar esses dados com saída Olá `lsscsi` para Olá mesma máquina virtual de amostra:
   
    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```
   
    último número Olá Olá tupla em cada linha é hello *lun*. Veja `man lsscsi` para obter mais informações.
3. No prompt de hello, digite Olá toocreate de comando a seguir seu dispositivo:
   
    ```bash
    sudo fdisk /dev/sdc
    ```

4. Quando solicitado, digite  **n**  toocreate uma partição.

    ![Criar dispositivo](./media/attach-disk/fdisknewpartition.png)

5. Quando solicitado, digite **p** partição primária do hello toomake Olá partição. Tipo **1** toomake Olá primeira partição e, em seguida, digite insira o valor de padrão de saudação do tooaccept para cilindro hello. Em alguns sistemas, pode mostrar valores padrão Olá Olá primeiro e Olá última setores, em vez de cilindro hello. Você pode escolher tooaccept esses padrões.

    ![Criar partição](./media/attach-disk/fdisknewpartdetails.png)


6. Tipo **p** toosee detalhes Olá disco Olá que estiver sendo particionado.

    ![Listar informações de disco](./media/attach-disk/fdiskpartitiondetails.png)


7. Tipo **w** toowrite configurações Olá disco hello.

    ![Gravar alterações de disco Olá](./media/attach-disk/fdiskwritedisk.png)

8. Agora você pode criar o sistema de arquivos de saudação na nova partição de saudação. Acrescentar Olá partição número toohello dispositivo ID (no exemplo a seguir de saudação `/dev/sdc1`). Olá exemplo a seguir cria uma partição de ext4 em /dev/sdc1:
   
    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```
   
    ![Criar sistema de arquivos](./media/attach-disk/mkfsext4.png)
   
   > [!NOTE]
   > Sistemas SuSE Linux Enterprise 11 dão suporte apenas a acesso somente leitura para sistemas de arquivos ext4. Para esses sistemas, é recomendável tooformat Olá novo sistema de arquivos como ext3 em vez de ext4.

9. Faça um diretório toomount Olá novo sistema de arquivos, da seguinte maneira:
   
    ```bash
    sudo mkdir /datadrive
    ```

10. Por fim, você pode montar Olá unidade, da seguinte maneira:
   
    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```
   
    disco de dados Olá agora está pronto toouse como **/datadrive**.
   
    ![Criar disco de saudação de diretório e montagem Olá](./media/attach-disk/mkdirandmount.png)

11. Adicione Olá nova unidade muito/etc/fstab:
   
    unidade de saudação tooensure é remontada automaticamente após uma reinicialização, que ele deve ser adicionado toohello /etc/fstab arquivo. Além disso, é altamente recomendável que Olá UUID (identificador universalmente exclusivo) é usado em /etc/fstab toorefer toohello unidade em vez do nome de dispositivo de saudação apenas (ou seja, /dev/sdc1). Usando Olá UUID evita que está sendo montado tooa dado local se Olá SO detecta um erro de disco durante a inicialização e discos de dados restantes, em seguida, que está sendo atribuído as identificações de dispositivo de disco incorreta hello. toofind Olá UUID da unidade nova hello, você pode usar o hello **blkid** utilitário:
   
    ```bash
    sudo -i blkid
    ```
   
    saída de Hello parece semelhante toohello exemplo a seguir:
   
    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

    > [!NOTE]
    > Edição incorretamente Olá **/etc/fstab** arquivo pode resultar em um sistema não inicializável. Se não tiver certeza, consulte a documentação do toohello da distribuição para obter informações sobre como tooproperly editar esse arquivo. Também é recomendável que um backup de arquivo /etc/fstab de saudação é criado antes de editar.

    Em seguida, abra Olá **/etc/fstab** em um editor de texto:

    ```bash
    sudo vi /etc/fstab
    ```

    Neste exemplo, usamos Olá UUID valor para Olá novo **/desenvolvimento/sdc1** dispositivo que foi criado em etapas anteriores hello e ponto de montagem Olá **/datadrive**. Adicionar Olá após o final da linha toohello de saudação **/etc/fstab** arquivo:

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
    ```

    Ou, em sistemas baseados no SuSE Linux, talvez seja necessário toouse um formato ligeiramente diferente:

    ```sh
    /dev/disk/by-uuid/33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext3   defaults,nofail   1   2
    ```

    > [!NOTE]
    > Olá `nofail` opção garante que Olá VM iniciado mesmo se Olá de sistema de arquivos está corrompido ou disco Olá não existe no momento da inicialização. Sem essa opção, você pode encontrar o comportamento conforme descrito em [não é possível SSH tooLinux VM devido a erros de tooFSTAB](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).

    Agora você pode testar se o sistema de arquivo hello está montado corretamente desmontar e remontar, em seguida, o sistema de arquivo hello, ou seja, usando o ponto de montagem do exemplo hello `/datadrive` criado no hello etapas anteriores:

    ```bash
    sudo umount /datadrive
    sudo mount /datadrive
    ```

    Se hello `mount` comando gerará um erro, verifique Olá/etc/fstab arquivo sintaxe correta. Se as partições ou unidades de dados adicionais forem criadas, insira-as separadamente em/etc/fstab também.

    Tornar gravável unidade hello usando este comando:

    ```bash
    sudo chmod go+w /datadrive
    ```

    > [!NOTE]
    > Subsequentemente, remover um disco de dados sem editar fstab poderia causar Olá VM toofail tooboot. Se esta for uma ocorrência comum, a maioria das distribuições fornecem qualquer Olá `nofail` e/ou `nobootwait` fstab opções que permitem que um sistema tooboot mesmo se o disco de saudação falhar toomount no momento da inicialização. Consulte a documentação da distribuição para obter mais informações sobre esses parâmetros.

### <a name="trimunmap-support-for-linux-in-azure"></a>Suporte a TRIM/UNMAP para Linux no Azure
Suportam a alguns kernels Linux TRIM/DESMAPEAMENTO operações toodiscard blocos não usados no disco hello. Essas operações são principalmente útil no armazenamento padrão tooinform Azure que páginas excluídas não são mais válidas e podem ser descartadas. Descartar páginas poderá representar uma economia de dinheiro se você criar arquivos grandes e, em seguida, excluí-los.

Há duas maneiras tooenable TRIM suporte em sua VM do Linux. Como de costume, consulte a distribuição para Olá abordagem recomendada:

* Saudação de uso `discard` montar opção `/etc/fstab`, por exemplo:

    ```sh
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
[!INCLUDE [virtual-machines-linux-lunzero](../../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a>Próximas etapas
Você pode ler mais sobre como usar a VM do Linux em Olá artigos a seguir:

* [Como toolog na máquina virtual de tooa executando o Linux][Logon]
* [Como toodetach um disco de uma máquina virtual Linux](detach-disk.md)
* [Usando Olá CLI do Azure com o modelo de implantação clássico Olá](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [Configurar o RAID em uma VM Linux no Azure](../configure-raid.md)
* [Configurar o LVM em uma VM Linux no Azure](../configure-lvm.md)

<!--Link references-->
[Agent]:../agent-user-guide.md
[Logon]:../mac-create-ssh-keys.md
