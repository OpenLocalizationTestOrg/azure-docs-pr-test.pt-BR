---
title: aaaAttach um tooa de disco de dados gerenciados VM do Windows - Azure | Microsoft Docs
description: "Como tooattach novo gerenciados tooa de disco de dados em hello usando o portal do Azure VM do Windows hello modelo de implantação do Gerenciador de recursos."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: bacc0589ad2d93e4d3d055c8f837f8db27291ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-managed-data-disk-tooa-windows-vm-in-hello-azure-portal"></a>Como tooattach um dados gerenciados disco tooa VM do Windows no hello portal do Azure

Este artigo mostra como tooattach novos dados gerenciados disco tooWindows máquinas de virtuais por meio de saudação portal do Azure. Antes de fazer isso, revise estas dicas:

* tamanho de saudação da máquina virtual de saudação controla quantos discos de dados, você pode anexar. Para obter detalhes, consulte [Tamanhos das máquinas virtuais](sizes.md).
* Para um novo disco, você não precisa toocreate-lo primeiro porque o Azure cria quando anexá-lo.

Você também pode [anexar um disco de dados usando o Powershell](attach-disk-ps.md).



## <a name="add-a-data-disk"></a>Adicionar um disco de dados
1. No menu Olá Olá esquerda, clique em **máquinas virtuais**.
2. Selecione máquina virtual de Olá Olá lista.
3. Na folha de máquina virtual de saudação, clique em **discos**.
   4. Em Olá **discos** folha, clique em **+ adicionar disco de dados**.
5. No hello suspenso para um novo disco de saudação, selecione **criar vazio**.
6. Em Olá **disco gerenciado criar** folha, digite um nome para o disco hello e ajuste Olá outras configurações conforme necessário. Quando terminar, clique em **Criar**.
7. Em Olá **discos** folha, clique em Salvar toosave Olá nova configuração de disco Olá VM.
6. Depois do Azure cria o disco hello e anexa toohello virtual machine, novo disco de saudação é listado em configurações de disco da máquina de virtual Olá em **discos de dados**.


## <a name="initialize-a-new-data-disk"></a>Inicializar um novo disco de dados

1. Conecte-se toohello VM.
1. Clique em menu de início hello dentro Olá VM e o tipo **diskmgmt.msc** e clique em **Enter**. Isso iniciará Olá snap-in Gerenciamento de disco.
2. Gerenciamento de disco reconhecerá que você tenha um novo disco não inicializado e Olá inicializar disco janela será exibida.
3. Verifique se o novo disco de saudação é selecionado e clique em **Okey** tooinitialize-lo.
4. novo disco de saudação aparecerão como **não alocado**. Clique em qualquer lugar no disco hello e selecione **novo volume simples**. Olá **Assistente de novo Volume simples** será iniciado.
5. Vá pelo assistente hello, mantendo todos os padrões de hello quando você terminar de selecionar **concluir**.
6. Feche Gerenciamento de Disco.
7. Você receberá um pop-up que você precisa novo disco de saudação tooformat antes de você pode usá-lo. Clique em **Formatar disco**.
8. Em Olá **disco no novo formato** caixa de diálogo, verifique as configurações de saudação e depois clique em **iniciar**.
9. Você receberá um aviso que formatar discos Olá irá apagar todos os dados de saudação, clique em **Okey**.
10. Quando o formato de saudação for concluído, clique em **Okey**.

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
