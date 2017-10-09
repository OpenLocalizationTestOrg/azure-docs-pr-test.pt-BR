---
title: "aaaUse uma VM de solução de problemas no portal do Azure de saudação do Linux | Microsoft Docs"
description: "Saiba como problemas de máquinas virtuais Linux tootroubleshoot usando conexão Olá OS disco tooa recuperação VM Olá portal do Azure"
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
ms.date: 11/14/2016
ms.author: iainfou
ms.openlocfilehash: 794daa06d7436215af84a61ab9088524254c47df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-portal"></a>Solucionar problemas de uma VM do Linux, anexando a VM de recuperação do hello OS disco tooa usando Olá portal do Azure
Se sua máquina virtual do Linux (VM) encontra um erro de inicialização ou do disco, talvez seja necessário tooperform etapas no disco rígido virtual Olá própria solução de problemas. Um exemplo comum seria uma entrada inválida na `/etc/fstab` que impede que Olá VM seja capaz de tooboot com êxito. Este artigo detalha como toouse Olá tooconnect portal do Azure seu virtual rígida disco tooanother VM Linux toofix quaisquer erros e crie novamente sua VM original.

## <a name="recovery-process-overview"></a>Visão geral do processo de recuperação
Olá Solucionando problemas do processo é o seguinte:

1. Exclua Olá VM encontrar problemas, mantendo os discos rígidos virtuais hello.
2. Anexar e monte tooanother de disco rígido virtual Olá VM Linux para fins de solução de problemas.
3. Conecte-se toohello VM de solução de problemas. Editar arquivos ou execute qualquer ferramenta toofix problemas em Olá original do disco rígido virtual.
4. Desmonte e desanexar o disco rígido virtual de saudação do hello VM de solução de problemas.
5. Crie uma VM usando Olá original do disco rígido virtual.


## <a name="determine-boot-issues"></a>Determinar problemas de inicialização
Examine o diagnóstico de inicialização hello e toodetermine de captura de tela VM por que a VM não é capaz de tooboot corretamente. Um exemplo comum seria uma entrada inválida em `/etc/fstab` ou a exclusão ou movimentação do disco rígido virtual subjacente.

Selecione a VM no portal de saudação e, em seguida, role para baixo toohello **suporte + solução de problemas** seção. Clique em **diagnósticos de inicialização** mensagens do console Olá tooview transmitido de sua VM. Revisão Olá logs do console toosee se você pode determinar por que hello VM estiver apresentando um problema. Olá exemplo a seguir mostra que uma VM presa no modo de manutenção que requer interação manual:

![Exibindo os logs do console do diagnóstico de inicialização da VM](./media/troubleshoot-recovery-disks-portal/boot-diagnostics-error.png)

Você também pode clicar em **captura de tela de** na superior Olá Olá inicialização diagnostics log toodownload uma captura de captura de tela VM hello.


## <a name="view-existing-virtual-hard-disk-details"></a>Exibir detalhes do disco rígido virtual existente
Antes que você pode anexar o disco rígido virtual de tooanother VM, é necessário tooidentify nome de saudação do hello virtual VHD (disco rígido). 

Selecione o grupo de recursos do portal de saudação e selecione sua conta de armazenamento. Clique em **Blobs**, conforme mostrado no exemplo a seguir de saudação:

![Selecionar os blobs de armazenamento](./media/troubleshoot-recovery-disks-portal/storage-account-overview.png)

Normalmente, você tem um contêiner chamado **vhds** que armazena os discos rígidos virtuais. Selecione Olá contêiner tooview uma lista de discos rígidos virtuais. Nome de saudação de observação do seu VHD (prefixo Olá geralmente é Olá nome da VM):

![Identificar o VHD no contêiner de armazenamento](./media/troubleshoot-recovery-disks-portal/storage-container.png)

Selecione o disco rígido virtual existente na lista de saudação e copie a URL de saudação para uso em Olá etapas a seguir:

![Copiar a URL do disco rígido virtual existente](./media/troubleshoot-recovery-disks-portal/copy-vhd-url.png)


## <a name="delete-existing-vm"></a>Excluir VM existente
Discos rígidos virtuais e VMs são dois recursos distintos no Azure. Um disco rígido virtual é onde são armazenadas Olá sistema operacional, aplicativos e configurações. Olá própria máquina virtual é os metadados que definem Olá tamanho ou local e faz referência a recursos, como um disco rígido virtual ou placa de interface de rede virtual (NIC). Cada disco rígido virtual tem uma concessão atribuída quando anexado tooa VM. Embora os discos de dados podem ser anexados e desanexados mesmo enquanto Olá VM está em execução, disco de SO Olá não pode ser desanexado, a menos que Olá recursos de máquina virtual é excluída. concessão de saudação continua tooassociate disco de saudação SO com uma VM mesmo quando a VM está em um estado parado e desalocado.

Olá primeiro toorecover de etapa sua VM é toodelete Olá VM próprio recurso. Excluindo Olá VM deixa Olá os discos rígidos virtuais em sua conta de armazenamento. Após Olá que VM é excluída, você anexar Olá disco rígido virtual tooanother VM tootroubleshoot e resolver erros de saudação.

Selecione a VM no portal de saudação, clique **excluir**:

![Captura de tela do diagnóstico de inicialização da VM mostrando um erro de inicialização](./media/troubleshoot-recovery-disks-portal/stop-delete-vm.png)

Aguarde até que a saudação VM concluiu a exclusão antes de anexar o disco rígido virtual de saudação tooanother VM. concessão de Olá no disco rígido virtual Olá que associa a saudação VM precisa toobe liberado antes que você pode anexar tooanother de disco rígido virtual Olá VM.


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a>Anexar tooanother de disco rígido virtual existente VM
Para Avançar Olá algumas etapas, você usar outra VM para fins de solução de problemas. Anexar Olá toothis do disco rígido virtual existente VM toobe capaz de toobrowse de solução de problemas e editar o conteúdo do disco hello. Esse processo permite que você toocorrect quaisquer erros de configuração ou examinar aplicativos adicionais ou sistema de arquivos de log, por exemplo. Escolha ou crie outro toouse VM para fins de solução de problemas.

1. Selecione o grupo de recursos do portal de saudação e selecione a VM de solução de problemas. Selecione **Discos** e clique em **Anexar existente**:

    ![Anexar um disco existente no portal de saudação](./media/troubleshoot-recovery-disks-portal/attach-existing-disk.png)

2. tooselect o disco rígido virtual existente, clique em **arquivo VHD**:

    ![Procurar VHD existente](./media/troubleshoot-recovery-disks-portal/select-vhd-location.png)

3. Selecione sua conta de armazenamento e seu contêiner e clique no VHD existente. Clique em Olá **selecione** botão tooconfirm sua escolha:

    ![Selecionar o VHD existente](./media/troubleshoot-recovery-disks-portal/select-vhd.png)

4. Com o VHD selecionado agora, clique em **Okey** tooattach Olá disco rígido virtual existente:

    ![Confirmar a anexação do disco rígido virtual existente](./media/troubleshoot-recovery-disks-portal/attach-disk-confirm.png)

5. Depois de alguns segundos, Olá **discos** painel para sua VM lista o disco rígido virtual existente conectado como um disco de dados:

    ![Disco rígido virtual existente anexado como um disco de dados](./media/troubleshoot-recovery-disks-portal/attached-disk.png)


## <a name="mount-hello-attached-data-disk"></a>Montar o disco de dados anexado Olá

> [!NOTE]
> Olá exemplos a seguir detalham etapas Olá necessárias em uma VM do Ubuntu. Se você estiver usando uma distribuição diferente do Linux, como Red Hat Enterprise Linux ou SUSE, Olá locais de arquivo de log e `mount` comandos podem ser um pouco diferentes. Consulte a documentação de toohello para sua distribuição específica para as alterações apropriadas Olá em comandos.

1. SSH tooyour VM usando as credenciais apropriadas Olá de solução de problemas. Se o disco estiver Olá primeiro dados disco anexado tooyour VM de solução de problemas, ele provavelmente está conectado muito`/dev/sdc`. Use `dmseg` toolist anexou discos:

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
Depois que os erros são resolvidos, desanexe Olá disco rígido virtual existente de sua solução de problemas de VM. Você não pode usar o disco rígido virtual com qualquer outra VM até que a concessão Olá anexando toohello do disco rígido virtual Olá Solucionando problemas de VM é liberado.

1. De saudação SSH tooyour de sessão VM de solução de problemas, desmonte Olá existente do disco rígido virtual. Altere primeiro fora do diretório do pai Olá para o seu ponto de montagem:

    ```bash
    cd /
    ```

    Agora, desmonte-Olá existente do disco rígido virtual. exemplo a seguir Hello desmonta dispositivo Olá no `/dev/sdc1`:

    ```bash
    sudo umount /dev/sdc1
    ```

2. Agora Desanexe o disco rígido virtual de saudação do hello VM. Selecione a VM no portal de saudação e clique em **discos**. Selecione o disco rígido virtual existente e clique em **Desanexar**:

    ![Desanexar um disco rígido virtual existente](./media/troubleshoot-recovery-disks-portal/detach-disk.png)

    Aguarde até que a saudação VM tem disco desanexado com êxito Olá dados antes de continuar.

## <a name="create-vm-from-original-hard-disk"></a>Criar a VM com base no disco rígido original
toocreate uma VM do seu disco rígido virtual original, use [este modelo do Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet). modelo Olá implanta uma VM em uma rede virtual existente, usando Olá URL do VHD de saudação do comando anterior. Clique em Olá **implantar tooAzure** botão da seguinte maneira:

![Implantar a VM com base no modelo do GitHub](./media/troubleshoot-recovery-disks-portal/deploy-template-from-github.png)

modelo de saudação é carregado no hello portal do Azure para implantação. Digite os nomes de saudação para sua nova VM e os recursos do Azure existentes e, em seguida, cole Olá URL tooyour disco rígido virtual existente. implantação de saudação toobegin, clique em **compra**:

![Implantar a VM com base no modelo](./media/troubleshoot-recovery-disks-portal/deploy-from-image.png)


## <a name="re-enable-boot-diagnostics"></a>Habilitar o diagnóstico de inicialização novamente
Quando você cria a VM de saudação existente do disco rígido virtual, o diagnóstico de inicialização pode não ser habilitado automaticamente. toocheck Olá status de diagnóstico de inicialização e ativar se necessário, selecione a VM no portal de saudação. Em **Monitoramento**, clique em **Configurações de diagnóstico**. Verificar status de saudação é **na**, e Olá marca de seleção ao lado de muito**diagnósticos de inicialização** está selecionado. Se fizer alguma alteração, clique em **Salvar**:

![Atualizar as configurações do diagnóstico de inicialização](./media/troubleshoot-recovery-disks-portal/reenable-boot-diagnostics.png)

## <a name="next-steps"></a>Próximas etapas
Se você estiver tendo problemas para se conectar tooyour VM, consulte [solucionar problemas de SSH conexões tooan VM do Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Para ver problemas com o acesso a aplicativos executados na VM, consulte [Solucionar problemas de conectividade do aplicativo em uma VM do Linux](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Para obter mais informações sobre como usar o Resource Manager, consulte [Visão geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
