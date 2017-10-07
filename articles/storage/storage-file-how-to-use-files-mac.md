---
title: compartilhamento de arquivo do Azure aaaMount via SMB com macOS | Microsoft Docs
description: Saiba como toomount um arquivo Azure compartilhar em SMB com macOS.
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 7b4924cb42247470521c1ae8b9d03ab1756996e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-share-over-smb-with-macos"></a>Montagem do compartilhamento de arquivos do Azure no SMB com macOS
[Armazenamento de arquivo do Azure](storage-dotnet-how-to-use-files.md) é usando o serviço da Microsoft que permite que você toocreate e use compartilhamentos de arquivos de rede no hello Azure padrão da indústria hello. Os compartilhamentos de arquivos do Azure podem ser montados em macOS Sierra (10.12) e El Capitan (10.11). Este artigo mostra toomount de duas formas diferentes um compartilhamento de arquivos do Azure em macOS com hello localizador de interface do usuário e usando Olá Terminal.

> [!Note]  
> Antes de montar um compartilhamento de arquivos do Azure no SMB, é recomendável desabilitar a assinatura de pacote SMB. Isso pode resultar em baixo desempenho ao acessar o compartilhamento de arquivos do Azure de saudação do macOS. Sua conexão SMB sejam criptografado, para que isso não afeta a segurança de saudação da sua conexão. De Olá terminal, hello comandos a seguir desabilitará a assinatura de pacotes SMB, conforme descrito por esta [artigo do suporte da Apple ao desabilitar a assinatura de pacote SMB](https://support.apple.com/HT205926):  
>    ```
>    sudo -s
>    echo "[default]" >> /etc/nsmb.conf
>    echo "signing_required=no" >> /etc/nsmb.conf
>    exit
>    ```

## <a name="prerequisites-for-mounting-an-azure-file-share-on-macos"></a>Pré-requisitos para montar um compartilhamento de arquivos do Azure no macOS
* **Nome da conta de armazenamento**: toomount de compartilhamento de um arquivo do Azure, será necessário Olá o nome da conta de armazenamento hello.

* **Chave de conta de armazenamento**: toomount de compartilhamento de um arquivo do Azure, será necessário Olá o chave de armazenamento primária (ou secundário). Atualmente, as chaves SAS não têm suporte para montagem.

* **Certifique-se de que a porta 445 está aberta**: SMB se comunica pela porta TCP 445. No computador cliente (Olá Mac), verifique toomake se que o firewall não está bloqueando a porta TCP 445.

## <a name="mount-an-azure-file-share-via-finder"></a>Montar um compartilhamento de arquivos do Azure por meio do Localizador
1. **Abrir o localizador**: localizador é aberta no macOS por padrão, mas você pode garantir é Olá atualmente selecionada aplicativo clicando hello "macOS enfrentam ícone" no encaixe hello:  
    ![Olá macOS enfrentam ícone](media/storage-file-how-to-use-files-mac/mount-via-finder-1.png)

2. **Selecione "TooServer conectar-se" Olá "Go" Menu**: usando o caminho UNC de saudação do hello [pré-requisitos](#preq), converter barra invertida dupla de início da saudação (`\\`) muito`smb://` e todas as outras barras invertidas (`\`) barras de tooforwards (`/`). O link deve ter aparência a seguir Olá: ![caixa de diálogo de "TooServer conectar-se" Olá](./media/storage-file-how-to-use-files-mac/mount-via-finder-2.png)

3. **Use Olá compartilhamento nome e o armazenamento de chave da conta quando solicitado a fornecer um nome de usuário e senha**: quando você clica em "Conectar" na caixa de diálogo de "TooServer conectar-se" Olá, você será solicitado para Olá nome de usuário e senha (Isso será autopopulated com seu macOS nome de usuário). Você tem a opção de saudação de colocar chave de conta de nome/armazenamento de compartilhamento de saudação em seu conjunto de chaves macOS.

4. **Compartilhamento de arquivo do Azure Use Olá conforme desejado**: após substituindo Olá compartilhamento nome e o armazenamento de chave da conta para Olá username e password, compartilhamento hello será montado. Você pode usar isso como você normalmente usa um compartilhamento de arquivo/pasta local, incluindo arrastando e soltando arquivos em um compartilhamento de arquivo hello:

    ![Um instantâneo de um compartilhamento de arquivos montado do Azure](./media/storage-file-how-to-use-files-mac/mount-via-finder-3.png)

## <a name="mount-an-azure-file-share-via-terminal"></a>Montar um compartilhamento de arquivos do Azure por meio do Terminal
1. Substituir `<storage-account-name>` com nome de saudação da sua conta de armazenamento. Quando solicitado, forneça a chave da conta de armazenamento como a senha. 

    ```
    mount_smbfs //<storage-account-name>@<storage-account-name>.file.core.windows.net/<share-name> <desired-mount-point>
    ```

2. **Compartilhamento de arquivo do Azure Use Olá conforme desejado**: compartilhamento de arquivo do Azure Olá será montado no ponto de montagem de saudação especificado pelo comando anterior hello.  

    ![Um instantâneo do compartilhamento de arquivo do Azure Olá montado](./media/storage-file-how-to-use-files-mac/mount-via-terminal-1.png)

## <a name="next-steps"></a>Próximas etapas
Consulte estes links para obter mais informações sobre o armazenamento de arquivo do Azure.

* [Artigo de suporte da Apple - como tooconnect com o compartilhamento de arquivo no seu Mac](https://support.apple.com/HT204445)
* [Perguntas frequentes](storage-files-faq.md)
* [Solução de problemas](storage-troubleshoot-file-connection-problems.md)