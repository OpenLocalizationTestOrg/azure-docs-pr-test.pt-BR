---
title: "aaaUse uma VM de solução de problemas no portal do Azure de saudação do Windows | Microsoft Docs"
description: "Saiba como problemas de máquinas virtuais de Windows tootroubleshoot no Azure usando conexão Olá OS disco tooa recuperação VM Olá portal do Azure"
services: virtual-machines-windows
documentationCenter: 
authors: genlin
manager: timlt
editor: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 396f70338fa39f80bb9adcb9244d3c83f2a233eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-windows-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-portal"></a>Solucionar problemas de uma VM do Windows, anexando a VM de recuperação do hello OS disco tooa usando Olá portal do Azure
Se sua máquina virtual do Windows (VM) no Azure encontra um erro de inicialização ou do disco, talvez seja necessário tooperform etapas no disco rígido virtual Olá própria solução de problemas. Um exemplo comum seria uma atualização de aplicativo com falha que impede que Olá VM seja capaz de tooboot com êxito. Este artigo detalha como toouse Olá tooconnect portal do Azure seu virtual rígida disco toofix de VM do Windows tooanother quaisquer erros e crie novamente sua VM original.

## <a name="recovery-process-overview"></a>Visão geral do processo de recuperação
Olá Solucionando problemas do processo é o seguinte:

1. Exclua Olá VM encontrar problemas, mantendo os discos rígidos virtuais hello.
2. Anexar e montar o disco rígido virtual de saudação tooanother VM do Windows para fins de solução de problemas.
3. Conecte-se toohello VM de solução de problemas. Editar arquivos ou execute qualquer ferramenta toofix problemas em Olá original do disco rígido virtual.
4. Desmonte e desanexar o disco rígido virtual de saudação do hello VM de solução de problemas.
5. Crie uma VM usando Olá original do disco rígido virtual.


## <a name="determine-boot-issues"></a>Determinar problemas de inicialização
toodetermine por que a VM não é capaz de tooboot corretamente, examine o diagnóstico de inicialização Olá captura de tela de VM. Um exemplo comum seria uma atualização de aplicativo com falha ou um disco rígido virtual subjacente que está sendo excluído ou movido.

Selecione a VM no portal de saudação e, em seguida, role para baixo toohello **suporte + solução de problemas** seção. Clique em **diagnósticos de inicialização** tooview captura de tela de saudação. Observe as mensagens de erro específico ou códigos de erro toohelp determinar por que Olá VM estiver apresentando um problema. Olá, exemplo a seguir mostra uma VM aguardando Parando serviços:

![Exibindo os logs do console do diagnóstico de inicialização da VM](./media/troubleshoot-recovery-disks-portal/screenshot-error.png)

Você também pode clicar em **captura de tela de** toodownload uma captura de captura de tela VM hello.


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

1. Abra uma conexão de área de trabalho remota tooyour VM. Selecione a VM no portal de saudação e clique em **conectar**. Baixe e abra o arquivo de conexão de RDP hello. Insira sua credenciais toolog tooyour VM da seguinte maneira:

    ![Faça logon no tooyour VM usando a área de trabalho remota](./media/troubleshoot-recovery-disks-portal/open-remote-desktop.png)

2. Abra **Gerenciador do Servidor** e selecione **Serviços de Arquivo e Armazenamento**. 

    ![Selecionar Serviços de Arquivo e Armazenamento no Gerenciador do Servidor](./media/troubleshoot-recovery-disks-portal/server-manager-select-storage.png)

3. disco de dados Olá é automaticamente detectado e anexado. uma lista de saudação do toosee conectado discos, selecione **discos**. Você pode selecionar suas informações de volume em tooview dados em disco, incluindo a letra da unidade hello. Olá seguinte exemplo mostra Olá disco de dados anexado e usando **f:**:

    ![Disco anexado e informações de volume no Gerenciador do Servidor](./media/troubleshoot-recovery-disks-portal/server-manager-disk-attached.png)


## <a name="fix-issues-on-original-virtual-hard-disk"></a>Corrigir problemas no disco rígido virtual original
Com hello disco rígido virtual existente montado, agora você pode executar qualquer manutenção e etapas de solução de problemas conforme necessário. Depois que você resolveu problemas hello, continue com hello etapas a seguir.


## <a name="unmount-and-detach-original-virtual-hard-disk"></a>Desmontar e desanexar o disco rígido virtual original
Depois que os erros são resolvidos, desanexe Olá disco rígido virtual existente de sua solução de problemas de VM. Você não pode usar o disco rígido virtual com qualquer outra VM até que a concessão Olá anexando toohello do disco rígido virtual Olá Solucionando problemas de VM é liberado.

1. Na tooyour de sessão RDP Olá VM, abra **Gerenciador do servidor**, em seguida, selecione **serviços de arquivo e armazenamento**:

    ![Selecionar Serviços de Arquivo e Armazenamento no Gerenciador do Servidor](./media/troubleshoot-recovery-disks-portal/server-manager-select-storage.png)

2. Selecione **Discos** e, em seguida, o disco de dados. Clique com o botão direito do mouse no disco de dados e selecione **Colocar Offline**:

    ![Disco de dados do conjunto hello como offline no Gerenciador do servidor](./media/troubleshoot-recovery-disks-portal/server-manager-set-disk-offline.png)

3. Agora Desanexe o disco rígido virtual de saudação do hello VM. Selecione a VM no portal do Azure de saudação e clique em **discos**. Selecione o disco rígido virtual existente e clique em **Desanexar**:

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
Se você estiver tendo problemas para se conectar tooyour VM, consulte [tooan de conexões RDP de solucionar problemas de VM do Azure](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Para problemas com o acesso a aplicativos executados na VM, consulte [Solucionar problemas de conectividade do aplicativo em uma VM do Windows](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Para obter mais informações sobre como usar o Resource Manager, consulte [Visão geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).