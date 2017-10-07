---
title: "aaaUse uma VM de solução de problemas com hello Azure CLI 1.0 do Linux | Microsoft Docs"
description: "Saiba como tootroubleshoot problemas de VM do Linux usando conexão Olá OS disco tooa recuperação VM Olá 1.0 da CLI do Azure"
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 398f681d1149299d444fcfdab20737315db02855
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-cli-10"></a>Solucionar problemas de uma VM do Linux, anexando a VM de recuperação do hello OS disco tooa usando Olá 1.0 da CLI do Azure
Se sua máquina virtual do Linux (VM) encontra um erro de inicialização ou do disco, talvez seja necessário tooperform etapas no disco rígido virtual Olá própria solução de problemas. Um exemplo comum seria uma entrada inválida na `/etc/fstab` que impede que Olá VM seja capaz de tooboot com êxito. Este artigo detalha como toouse hello Azure CLI 1.0 tooconnect seu virtual rígida disco tooanother VM Linux toofix quaisquer erros e crie novamente sua VM original.


## <a name="cli-versions-toocomplete-hello-task"></a>Tarefa de saudação do CLI versões toocomplete
Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:

- [1.0 de CLI do Azure](#recovery-process-overview) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)
- [2.0 do CLI do Azure](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação


## <a name="recovery-process-overview"></a>Visão geral do processo de recuperação
Olá Solucionando problemas do processo é o seguinte:

1. Exclua Olá VM encontrar problemas, mantendo os discos rígidos virtuais hello.
2. Anexar e monte tooanother de disco rígido virtual Olá VM Linux para fins de solução de problemas.
3. Conecte-se toohello VM de solução de problemas. Editar arquivos ou execute qualquer ferramenta toofix problemas em Olá original do disco rígido virtual.
4. Desmonte e desanexar o disco rígido virtual de saudação do hello VM de solução de problemas.
5. Crie uma VM usando Olá original do disco rígido virtual.

Certifique-se de que você tenha [hello mais recente do Azure CLI 1.0](../../cli-install-nodejs.md) instalado e conectado e usando o modo do Gerenciador de recursos:

```azurecli
azure config mode arm
```

Em Olá exemplos a seguir, substitua os nomes de parâmetro com seus próprios valores. Os nomes de parâmetro de exemplo incluem `myResourceGroup`, `mystorageaccount` e `myVM`.


## <a name="determine-boot-issues"></a>Determinar problemas de inicialização
Examine Olá saída serial toodetermine por que a VM não é capaz de tooboot corretamente. Um exemplo comum é uma entrada inválida na `/etc/fstab`, ou Olá subjacente do disco rígido virtual que está sendo excluído ou movido.

Olá exemplo a seguir obtém Olá serial saída de hello VM denominada `myVM` no grupo de recursos de saudação chamado `myResourceGroup`:

```azurecli
azure vm get-serial-output --resource-group myResourceGroup --name myVM
```

Examine Olá saída serial toodetermine por hello VM está falhando tooboot. Se a saída serial Olá não fornece nenhuma indicação, talvez seja necessário tooreview arquivos de log em `/var/log` depois que você tiver Olá virtual disco rígido conectado tooa VM de solução de problemas.


## <a name="view-existing-virtual-hard-disk-details"></a>Exibir detalhes do disco rígido virtual existente
Antes que você pode anexar o disco rígido virtual de tooanother VM, é necessário tooidentify nome de saudação do hello virtual VHD (disco rígido). 

Olá, exemplo a seguir obtém informações de saudação VM denominada `myVM` no grupo de recursos de saudação chamado `myResourceGroup`:

```azurecli
azure vm show --resource-group myResourceGroup --name myVM
```

Procure `Vhd URI` na saída de saudação da saudação anterior de comando. Olá seguinte truncado exemplo mostra Olá `Vhd URI` na última linha de saudação:

```azurecli
info:    Executing command vm show
+ Looking up hello VM "myVM"
+ Looking up hello NIC "myNic"
+ Looking up hello public ip "myPublicIP"
...
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :myVM
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/myVM201610292712.vhd
```


## <a name="delete-existing-vm"></a>Excluir VM existente
Discos rígidos virtuais e VMs são dois recursos distintos no Azure. Um disco rígido virtual é onde são armazenadas Olá sistema operacional, aplicativos e configurações. Olá própria máquina virtual é os metadados que definem Olá tamanho ou local e faz referência a recursos, como um disco rígido virtual ou placa de interface de rede virtual (NIC). Cada disco rígido virtual tem uma concessão atribuída quando anexado tooa VM. Embora os discos de dados podem ser anexados e desanexados mesmo enquanto Olá VM está em execução, disco de SO Olá não pode ser desanexado, a menos que Olá recursos de máquina virtual é excluída. concessão de saudação continua tooassociate disco de saudação SO com uma VM mesmo quando a VM está em um estado parado e desalocado.

Olá primeiro toorecover de etapa sua VM é toodelete Olá VM próprio recurso. Excluindo Olá VM deixa Olá os discos rígidos virtuais em sua conta de armazenamento. Após Olá que VM é excluída, você anexar Olá disco rígido virtual tooanother VM tootroubleshoot e resolver erros de saudação.

Olá exclusões de exemplo a seguir Olá VM denominada `myVM` saudação do grupo de recursos denominado `myResourceGroup`:

```azurecli
azure vm delete --resource-group myResourceGroup --name myVM 
```

Aguarde até que a saudação VM concluiu a exclusão antes de anexar o disco rígido virtual de saudação tooanother VM. concessão de Olá no disco rígido virtual Olá que associa a saudação VM precisa toobe liberado antes que você pode anexar tooanother de disco rígido virtual Olá VM.


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a>Anexar tooanother de disco rígido virtual existente VM
Para Avançar Olá algumas etapas, você usar outra VM para fins de solução de problemas. Anexar Olá toothis do disco rígido virtual existente VM toobrowse de solução de problemas e editar o conteúdo do disco hello. Esse processo permite que você toocorrect quaisquer erros de configuração ou examinar aplicativos adicionais ou sistema de arquivos de log, por exemplo. Escolha ou crie outro toouse VM para fins de solução de problemas.

Quando você anexa Olá existente do disco rígido virtual, especifique o disco de toohello de URL de saudação obtido na saudação anterior `azure vm show` comando. Olá, exemplo a seguir anexa um toohello de disco rígido virtual existente Solucionando problemas de VM denominada `myVMRecovery` no grupo de recursos de saudação chamado `myResourceGroup`:

```azurecli
azure vm disk attach --resource-group myResourceGroup --name myVMRecovery \
    --vhd-url https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-hello-attached-data-disk"></a>Montar o disco de dados anexado Olá

> [!NOTE]
> Olá exemplos a seguir detalham etapas Olá necessárias em uma VM do Ubuntu. Se você estiver usando uma distribuição diferente do Linux, como Red Hat Enterprise Linux ou SUSE, Olá locais de arquivo de log e `mount` comandos podem ser um pouco diferentes. Consulte a documentação de toohello para sua distribuição específica para as alterações apropriadas Olá em comandos.

1. SSH tooyour VM usando as credenciais apropriadas Olá de solução de problemas. Se o disco estiver Olá primeiro dados disco anexado tooyour Solucionando problemas de VM, disco Olá provavelmente está conectado muito`/dev/sdc`. Use `dmseg` tooview anexou discos:

    ```bash
    dmesg | grep SCSI
    ```

    saudação de saída é similar toohello exemplo a seguir:

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    Nos Olá anterior de exemplo, disco Olá SO está em `/dev/sda` e Olá disco temporário fornecido para cada máquina virtual está em `/dev/sdb`. Se você tiver vários discos de dados, eles deverão estar em `/dev/sdd`, `/dev/sde` e assim por diante.

2. Crie um diretório toomount seu disco rígido virtual existente. Olá, exemplo a seguir cria um diretório chamado `troubleshootingdisk`:

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. Se você tiver várias partições no disco rígido virtual existente, monte partição Olá necessário. exemplo a seguir Hello monta primeira partição primária Olá em `/dev/sdc1`:

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > Prática recomendada é toomount os discos de dados em máquinas virtuais no Azure usando Olá identificador universalmente exclusivo (UUID) de disco rígido virtual de saudação. Para este cenário de solução de problemas curto, montagem Olá disco rígido virtual usando Olá UUID não é necessário. No entanto, em uso normal, edição `/etc/fstab` toomount os discos rígidos virtuais usando o nome do dispositivo, em vez de UUID pode causar Olá VM toofail tooboot.


## <a name="fix-issues-on-original-virtual-hard-disk"></a>Corrigir problemas no disco rígido virtual original
Com hello disco rígido virtual existente montado, agora você pode executar qualquer manutenção e etapas de solução de problemas conforme necessário. Depois que você resolveu problemas hello, continue com hello etapas a seguir.


## <a name="unmount-and-detach-original-virtual-hard-disk"></a>Desmontar e desanexar o disco rígido virtual original
Depois que os erros são resolvidos, você desmontar e desanexar Olá existente do disco rígido virtual da VM sua solução de problemas. Você não pode usar o disco rígido virtual com qualquer outra VM até que a concessão Olá anexando toohello do disco rígido virtual Olá Solucionando problemas de VM é liberado.

1. De saudação SSH tooyour de sessão VM de solução de problemas, desmonte Olá existente do disco rígido virtual. Altere primeiro fora do diretório do pai Olá para o seu ponto de montagem:

    ```bash
    cd /
    ```

    Agora, desmonte-Olá existente do disco rígido virtual. exemplo a seguir Hello desmonta dispositivo Olá no `/dev/sdc1`:

    ```bash
    sudo umount /dev/sdc1
    ```

2. Agora Desanexe o disco rígido virtual de saudação do hello VM. Sair Olá SSH sessão tooyour VM de solução de problemas. No hello CLI do Azure, primeiro Olá de lista anexado tooyour de discos de dados VM de solução de problemas. Olá, exemplo a seguir lista Olá discos de dados anexado toohello VM denominada `myVMRecovery` no grupo de recursos de saudação chamado `myResourceGroup`:

    ```azurecli
    azure vm disk list --resource-group myResourceGroup --vm-name myVMRecovery
    ```

    Saudação de Observação `Lun` valor para o disco rígido virtual existente. Olá, saída de comando de exemplo a seguir mostra disco virtual existente Olá anexado ao LUN 0:

    ```azurecli
    info:    Executing command vm disk list
    + Looking up hello VM "myVMRecovery"
    data:    Name              Lun  DiskSizeGB  Caching  URI
    data:    ------            ---  ----------  -------  ------------------------------------------------------------------------
    data:    myVM              0                None     https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    info:    vm disk list command OK
    ```

    Desanexar o disco de dados Olá de sua VM usando Olá aplicável `Lun` valor:

    ```azurecli
    azure vm disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --lun 0
    ```


## <a name="create-vm-from-original-hard-disk"></a>Criar a VM com base no disco rígido original
toocreate uma VM do seu disco rígido virtual original, use [este modelo do Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd). modelo JSON real Hello está no hello link a seguir:

- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json

modelo Olá implanta uma VM em uma rede virtual existente, usando Olá URL do VHD de saudação do comando anterior. Olá exemplo a seguir implanta o grupo de recursos do hello modelo toohello chamado `myResourceGroup`:

```azurecli
azure group deployment create --resource-group myResourceGroup --name myDeployment \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

Saudação de resposta solicita modelo hello como o nome da VM (`myDeployedVM` Olá exemplo a seguir), tipo de sistema operacional (`Linux`) e o tamanho da VM (`Standard_DS1_v2`). Olá `osDiskVhdUri` é Olá mesmo usada anteriormente ao anexar Olá toohello do disco rígido virtual existente VM de solução de problemas. Um exemplo de saída do comando hello e prompts é o seguinte:

```azurecli
info:    Executing command group deployment create
info:    Supply values for hello following parameters
vmName:  myDeployedVM
osType:  Linux
osDiskVhdUri:  https://mystorageaccount.blob.core.windows.net/vhds/myVM201610292712.vhd
vmSize:  Standard_DS1_v2
existingVirtualNetworkName:  myVnet
existingVirtualNetworkResourceGroup:  myResourceGroup
subnetName:  mySubnet
dnsNameForPublicIP:  mypublicipdeployed
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "mydeployment"
+ Waiting for deployment toocomplete
+
```


## <a name="re-enable-boot-diagnostics"></a>Habilitar o diagnóstico de inicialização novamente

Quando você cria a VM de saudação existente do disco rígido virtual, o diagnóstico de inicialização pode não ser habilitado automaticamente. Olá exemplo a seguir habilita a extensão de diagnóstico Olá no hello VM denominada `myDeployedVM` no grupo de recursos de saudação chamado `myResourceGroup`:

```azurecli
azure vm enable-diag --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a>Próximas etapas
Se você estiver tendo problemas para se conectar tooyour VM, consulte [solucionar problemas de SSH conexões tooan VM do Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Para ver problemas com o acesso a aplicativos executados na VM, consulte [Solucionar problemas de conectividade do aplicativo em uma VM do Linux](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
