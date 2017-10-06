---
title: aaaMount armazenamento de arquivo do Azure de uma VM do Windows Azure | Microsoft Docs
description: "Armazene o arquivo na nuvem Olá com armazenamento de arquivos do Azure e montar o compartilhamento de arquivos de nuvem a partir de uma máquina virtual do Azure (VM)."
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: 
ms.tgt_pltfrm: 
ms.devlang: 
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: 965f1c1b3f0d07fec6d86f9312a05e02e8ce7fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-file-shares-with-windows-vms"></a>Usar compartilhamentos de arquivos do Azure com VMs do Windows 

Você pode usar compartilhamentos de arquivos do Azure como uma maneira toostore e acessar arquivos de sua VM. Por exemplo, você pode armazenar um script ou um arquivo de configuração de aplicativo que você deseja que todos os seu tooshare de VMs. Neste tópico, mostramos como compartilhamento de arquivos de montagem do Azure e toocreate e tooupload e download de arquivos.

## <a name="connect-tooa-file-share-from-a-vm"></a>Conecte-se o compartilhamento de arquivos tooa de uma VM

Esta seção pressupõe que você já tiver um compartilhamento de arquivos que você deseja tooconnect para. Se você precisar toocreate um, consulte [criar um compartilhamento de arquivos](#create-a-file-share) mais adiante neste tópico.

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. No menu à esquerda do hello, clique em **contas de armazenamento**.
3. Escolha sua conta de armazenamento.
4. Em Olá **visão geral** página em **serviços**, selecione **arquivos**.
5. Selecione um compartilhamento de arquivos.
6. Clique em **conectar** tooopen uma página que mostra a sintaxe de linha de comando Olá montagem Olá para compartilhamento de arquivos do Windows ou Linux.
7. Realçar a sintaxe de saudação do comando hello e cole-o no bloco de notas ou em outro lugar onde você pode acessá-lo facilmente. 
8. Editar à esquerda do hello sintaxe tooremove hello * * > * * e substituir *[letra da unidade]* com a letra de unidade de saudação (por exemplo, **y:**) onde deseja que o compartilhamento de arquivos toomount hello.
8. Conecte-se tooyour VM e abra um prompt de comando.
9. Colar em Olá editado sintaxe de conexão e pressione **Enter**.
10. Quando a conexão Olá tiver sido criado, você obter mensagem de saudação **Olá comando foi concluído com êxito.**
11. Verifique a conexão Olá digitando Olá letra tooswitch toothat unidade e, em seguida, digite **dir** toosee conteúdo de saudação do compartilhamento de arquivo hello.



## <a name="create-a-file-share"></a>Criar um compartilhamento de arquivos 
1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. No menu à esquerda do hello, clique em **contas de armazenamento**.
3. Escolha sua conta de armazenamento.
4. Em Olá **visão geral** página em **serviços**, selecione **arquivos**.
5. Na página de serviço de arquivo hello, clique em **+ compartilhamento de arquivos** toocreate do primeiro arquivo compartilhar. \
6. Preencha o nome de compartilhamento de arquivo hello. Nomes de compartilhamento de arquivos podem usar letras minúsculas, números e hifens únicos. Olá nome não pode começar com um hífen e não é possível usar várias hifens consecutivos. 
7. Preencha um limite no arquivo de saudação como grande pode ser a too5120 GB.
8. Clique em **Okey** toodeploy compartilhamento de arquivos de saudação.
   
## <a name="upload-files"></a>Carregar arquivos
1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. No menu à esquerda do hello, clique em **contas de armazenamento**.
3. Escolha sua conta de armazenamento.
4. Em Olá **visão geral** página em **serviços**, selecione **arquivos**.
5. Selecione um compartilhamento de arquivos.
6. Clique em **carregar** tooopen Olá **carregar arquivos** página.
7. Clique em Olá toobrowse de ícone de pasta sistema de arquivos local para tooupload um arquivo.   
8. Clique em **carregar** tooupload Olá toohello arquivo compartilhamento.

## <a name="download-files"></a>Baixar arquivos
1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. No menu à esquerda do hello, clique em **contas de armazenamento**.
3. Escolha sua conta de armazenamento.
4. Em Olá **visão geral** página em **serviços**, selecione **arquivos**.
5. Selecione um compartilhamento de arquivos.
6. Clique com botão direito no arquivo hello e escolha **baixar** toodownload-computador local tooyour.
   

## <a name="next-steps"></a>Próximas etapas

Você também pode criar e gerenciar compartilhamentos de arquivos usando o PowerShell. Para obter mais informações, confira [Introdução ao Armazenamento de Arquivos do Azure no Windows](../../storage/files/storage-dotnet-how-to-use-files.md).
