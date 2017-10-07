---
title: "aaaAttach tooa um disco clássico VM do Azure | Microsoft Docs"
description: "Anexar dados disco tooa máquina virtual do Windows criada com o modelo de implantação clássico hello e inicializá-lo."
services: virtual-machines-windows, storage
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: be4e3e74-05bc-4527-969f-84f10a1d66a7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: cynthn
ms.openlocfilehash: bfe1b0fa066277d28d3862a18da4b1023cb4452d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="attach-a-data-disk-tooa-windows-virtual-machine-created-with-hello-classic-deployment-model"></a>Anexar dados disco tooa máquina virtual do Windows criada com o modelo de implantação clássico Olá
<!--
Refernce article:
    If you want toouse hello new portal, see [How tooattach a data disk tooa Windows VM in hello Azure portal](../../virtual-machines-windows-attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

Este artigo mostra como discos de tooattach novos e existentes criados com hello clássico implantação modelo tooa máquina virtual do Windows usando Olá portal do Azure.

Você também pode [anexar tooa um disco de dados VM do Linux no portal do Azure de saudação](../../linux/attach-disk-portal.md).

Antes de anexar um disco, leia estas dicas:

* tamanho de saudação da máquina virtual de saudação controla quantos discos de dados, você pode anexar. Para obter detalhes, consulte [Tamanhos das máquinas virtuais](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

* toouse armazenamento Premium, você precisa de uma máquina virtual da série DS ou série GS. Você pode usar discos de contas de armazenamento Premium e Standard com essas máquinas virtuais. O armazenamento Premium está disponível em determinadas regiões. Para obter detalhes, confira [Armazenamento Premium: armazenamento de alto desempenho para as cargas de trabalho das máquinas virtuais do Azure](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

* Para um novo disco, você não precisa toocreate-lo primeiro porque o Azure cria quando anexá-lo.

Você também pode [anexar um disco de dados usando o Powershell](../../virtual-machines-windows-attach-disk-ps.md).

> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).

## <a name="find-hello-virtual-machine"></a>Localizar a máquina virtual de saudação
1. Entrar toohello [portal do Azure](https://portal.azure.com/).
2. Olá selecione máquina de virtual do recurso Olá listado no painel de saudação.
3. No painel esquerdo, Olá em **configurações**, clique em **discos**.

    ![Abrir configurações de disco](./media/attach-disk/virtualmachinedisks.png)

Continue seguindo as instruções para anexar um [novo disco](#option-1-attach-a-new-disk) ou um [disco existente](#option-2-attach-an-existing-disk).

## <a name="option-1-attach-and-initialize-a-new-disk"></a>Opção 1: Anexar e inicializar um novo disco

1. Em Olá **discos** folha, clique em **anexar novos**.
2. Examine as configurações padrão de saudação, atualizar conforme necessário e, em seguida, clique em **Okey**.

   ![Analisar configurações de disco](./media/attach-disk/attach-new.png)

3. Depois do Azure cria o disco hello e anexa toohello virtual machine, novo disco de saudação é listado em configurações de disco da máquina de virtual Olá em **discos de dados**.

### <a name="initialize-a-new-data-disk"></a>Inicializar um novo disco de dados

1. Conecte-se a máquina virtual de toohello. Para obter instruções, consulte [como tooconnect e logon tooan virtuais do Azure do computador que executa o Windows](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
2. Após fazer logon na máquina virtual de toohello, abra **Gerenciador do servidor**. No painel esquerdo do hello, selecione **serviços de arquivo e armazenamento**.

    ![Abra o gerenciador de servidor.](../media/attach-disk-portal/fileandstorageservices.png)

3. Escolha **Discos**.
4. Olá **discos** seção lista os discos de saudação. Na maioria das vezes, uma máquina virtual tem disco 0, disco 1 e disco 2. Disco 0 é o disco do sistema operacional hello, disco 1 é Olá temporário e o disco 2 é o disco de dados Olá recentemente anexado toohello virtual machine. listas de disco de dados Olá Olá partição como **desconhecido**.

 Disco hello e selecione **inicializar**.

5. Você é notificado de que todos os dados serão apagados quando Olá disco é inicializado. Clique em **Sim** tooacknowledge Olá aviso e inicializar Olá em disco. Uma vez concluído, partição hello será listada como **GPT**. Disco Olá novamente e selecione **Novo Volume**.

6. Conclua o Assistente de saudação usando valores padrão de saudação. Quando termina de assistente hello, Olá **Volumes** seção lista novo volume de saudação. disco de saudação agora está online e pronto toostore dados.

    ![Volume inicializado com êxito](./media/attach-disk/newdiskafterinitialization.png)

## <a name="option-2-attach-an-existing-disk"></a>Opção 2: Anexar um disco existente
1. Em Olá **discos** folha, clique em **anexar existente**.
2. Em **Anexar disco existente**, clique em **Local**.

   ![Anexar disco existente](./media/attach-disk/attachexistingdisksettings.png)
3. Em **contas de armazenamento**, selecione conta hello e contêiner que contém o arquivo. vhd de saudação.

   ![Localização do VHD](./media/attach-disk/existdiskstorageaccountandcontainer.png)

4. Selecione o arquivo. vhd de saudação.
5. Em **anexar o disco existente**, arquivo hello você selecionou é listado em **arquivo VHD**. Clique em **OK**.
6. Após anexa Azure hello disco toohello VM, ela é listada em configurações de disco da máquina de virtual Olá em **discos de dados**.

## <a name="use-trim-with-standard-storage"></a>Usar TRIM com o armazenamento padrão

Se você usar o armazenamento padrão (HDD), será necessário habilitar o TRIM. TRIM descarta blocos não usados no disco Olá para que você é cobrado somente para o armazenamento que você está usando. Usar o TRIM pode poupar dinheiro, incluindo blocos não utilizados que resultam da exclusão de arquivos grandes.

Você pode executar essa configuração de CORTE de saudação do comando toocheck. Abra um prompt de comando na sua VM do Windows e digite:

```
fsutil behavior query DisableDeleteNotify
```

Se o comando Olá retorna 0, TRIM está habilitada corretamente. Se ele retorna 1, execute Olá comando tooenable TRIM a seguir:
```
fsutil behavior set DisableDeleteNotify 0
```

## <a name="next-steps"></a>Próximas etapas
Se seu aplicativo precisa de dados de toostore toouse saudação d: unidade, você pode [alterar Olá letra da unidade de disco temporário do Windows hello](../../virtual-machines-windows-change-drive-letter.md).

## <a name="additional-resources"></a>Recursos adicionais
[Sobre discos e VHDs para máquinas virtuais](../../virtual-machines-linux-about-disks-vhds.md)
