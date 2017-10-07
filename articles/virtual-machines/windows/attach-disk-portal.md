---
title: "aaaAttach um tooa de disco de dados não gerenciados Windows VM - Azure | Microsoft Docs"
description: "Como tooattach não gerenciada de dados novo ou existente disco tooa VM do Windows no hello usando o portal do Azure Olá modelo de implantação do Gerenciador de recursos."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3790fc59-7264-41df-b7a3-8d1226799885
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: 923a6663974143bf359970f9b0eb0d36cabcba9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-an-unmanaged-data-disk-tooa-windows-vm-in-hello-azure-portal"></a>Como tooattach um dados não gerenciados disco tooa VM do Windows no hello portal do Azure

Este artigo mostra como tooattach novo e existente não gerenciado discos tooWindows máquinas de virtuais por meio de saudação portal do Azure. Você também pode [anexar um disco de dados usando o PowerShell](./attach-disk-ps.md). Antes de fazer isso, revise estas dicas:

* tamanho de saudação da máquina virtual de saudação controla quantos discos de dados, você pode anexar. Para obter detalhes, consulte [Tamanhos das máquinas virtuais](sizes.md).
* toouse armazenamento Premium, você precisa de uma máquina virtual da série DS ou série GS. Você pode usar discos de contas de armazenamento Premium e Standard com essas máquinas virtuais. O armazenamento Premium está disponível em determinadas regiões. Para obter detalhes, confira [Armazenamento Premium: armazenamento de alto desempenho para as cargas de trabalho das máquinas virtuais do Azure](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Para um novo disco, você não precisa toocreate-lo primeiro porque o Azure cria quando anexá-lo.


Você também pode [anexar um disco de dados usando o Powershell](attach-disk-ps.md).


## <a name="find-hello-virtual-machine"></a>Localizar a máquina virtual de saudação
1. Entrar toohello [portal do Azure](https://portal.azure.com/).
2. No menu Olá Olá esquerda, clique em **máquinas virtuais**.
3. Selecione máquina virtual de Olá Olá lista.
4. Na folha de máquinas virtuais de saudação, clique em **discos**.
   
Continue seguindo as instruções para anexar um [novo disco](#option-1-attach-a-new-disk) ou um [disco existente](#option-2-attach-an-existing-disk).

## <a name="option-1-attach-and-initialize-a-new-disk"></a>Opção 1: Anexar e inicializar um novo disco
1. Em Olá **discos** folha, clique em **+ adicionar disco de dados**.
2. Em Olá **anexar disco gerenciado** folha, digite um nome para o disco de saudação em **nome** e, em seguida, selecione **New (disco vazio)** na **tipo de fonte**.
3. Em **contêiner de armazenamento**, clique em Olá **procurar** botão e procurar toohello conta de armazenamento e contêiner qual seria Olá novo VHD toobe armazenado e, em seguida, clique em **selecione**. 
  
   ![Analisar configurações de disco](./media/attach-disk-portal/attach-empty-unmanaged.png)
   
3. Quando tiver terminado com as configurações de saudação de disco de dados hello, clique em **Okey**.
4. Em Olá **discos** folha, clique em **salvar** configuração da VM toohello tooadd Olá disco.


### <a name="initialize-a-new-data-disk"></a>Inicializar um novo disco de dados

1. Conecte-se a máquina virtual de toohello. Para obter instruções, consulte [como tooconnect e logon tooan virtuais do Azure do computador que executa o Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
1. Clique em Olá **iniciar** menu dentro Olá VM e digite **diskmgmt.msc** e clique em **Enter**. Isso inicia o snap-in de gerenciamento de disco de saudação.
2. Gerenciamento de disco reconhece que você tenha um disco novo e não inicializado e Olá inicializar disco janela será exibida.
3. Verifique se o novo disco de saudação é selecionado e clique em **Okey** tooinitialize-lo.
4. Olá novo disco agora aparece como **não alocado**. Clique em qualquer lugar no disco hello e selecione **novo volume simples**. Olá **Assistente de novo Volume simples** inicia.
5. Vá pelo assistente hello, mantendo todos os padrões de hello quando você terminar de selecionar **concluir**.
6. Feche Gerenciamento de Disco.
7. Você receberá um pop-up que você precisa novo disco de saudação tooformat antes de você pode usá-lo. Clique em **Formatar disco**.
8. Em Olá **disco no novo formato** caixa de diálogo, verifique as configurações de saudação e depois clique em **iniciar**.
9. Você receberá um aviso de que a formatação de discos Olá apaga todos os dados de saudação, clique em **Okey**.
10. Quando o formato de saudação for concluído, clique em **Okey**.


## <a name="option-2-attach-an-existing-disk"></a>Opção 2: Anexar um disco existente
1. Em Olá **discos** folha, clique em **+ adicionar disco de dados**.
2. Em Olá **anexar o disco não gerenciado** folha, na **tipo de fonte** selecione **blob existente**.

    ![Analisar configurações de disco](./media/attach-disk-portal/attach-existing-unmanaged.png)

    3. Clique em **procurar** toonavigate toohello conta de armazenamento e o contêiner onde hello VHD existente está localizado. Clique em e Olá VHD e, em seguida, clique em **selecione**.
4. Clique em **Okey** em Olá **anexar o disco não gerenciado** folha.
5. Em Olá **discos** folha, clique em **salvar** tooadd Olá toohello da configuração de disco Olá VM.
   


## <a name="use-trim-with-standard-storage"></a>Usar TRIM com o armazenamento padrão

Se você usar o armazenamento padrão (HDD), será necessário habilitar o TRIM. TRIM descarta blocos não usados no disco Olá para que você é cobrado somente para o armazenamento que você está usando. Isso poderá representar uma economia dos custos se você criar arquivos grandes e, em seguida, excluí-los. 

Você pode executar essa configuração de CORTE de saudação do comando toocheck. Abra um prompt de comando na sua VM do Windows e digite:

```
fsutil behavior query DisableDeleteNotify
```

Se o comando Olá retorna 0, TRIM está habilitada corretamente. Se ele retorna 1, execute Olá comando tooenable TRIM a seguir:
```
fsutil behavior set DisableDeleteNotify 0
```

Depois de excluir dados do disco, você pode garantir operações de CORTE de saudação liberação corretamente executando desfragmentação com TRIM:

```
defrag.exe <volume:> -l
```

Você também pode garantir a todo o volume Olá é cortado ao formatar o volume de saudação.


## <a name="next-steps"></a>Próximas etapas
Se seu aplicativo precisa de dados de toostore toouse saudação d: unidade, você pode [alterar Olá letra da unidade de disco temporário do Windows hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

