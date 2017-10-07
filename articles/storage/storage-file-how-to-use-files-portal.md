---
title: "aaaHow toomanage armazenamento de arquivo do Azure de saudação portal do Azure | Microsoft Docs"
description: "Saiba o armazenamento de arquivo do Azure toouse Olá toomanage portal do Azure."
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
ms.openlocfilehash: 385b99ac1c3d97ca79059ae8229afb53f1e825cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-file-storage-from-hello-azure-portal"></a>Como o armazenamento de arquivo do Azure toouse de Olá Portal do Azure
Olá [portal do Azure](https://portal.azure.com) fornece uma interface de usuário para gerenciar o armazenamento de arquivo do Azure. Você pode executar Olá ações a seguir em seu navegador da web:

* Criar um compartilhamento de arquivos
* Carregar e baixar arquivos tooand do seu compartilhamento de arquivos.
* Monitorar o uso real de cada compartilhamento de arquivo hello.
* Ajuste a cota de tamanho de compartilhamento de arquivo hello.
* Copie Olá montagem comandos toouse toomount o arquivo de compartilhamento de um cliente Windows ou Linux.

## <a name="create-file-share"></a>Criar o compartilhamento de arquivos
1. Entrar toohello portal do Azure.
2. No menu de navegação hello, clique em **contas de armazenamento** ou **contas de armazenamento (clássico)**.
    
    ![Captura de tela que mostra como compartilhamento de arquivos de toocreate no portal de saudação](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share1.png)

3. Escolha sua conta de armazenamento.

    ![Captura de tela que mostra como compartilhamento de arquivos de toocreate no portal de saudação](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share2.png)

4. Escolha o serviço "Arquivos".

    ![Captura de tela que mostra como compartilhamento de arquivos de toocreate no portal de saudação](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share3.png)

5. Clique em "Compartilhamentos de arquivos" e siga Olá link toocreate compartilhar seu primeiro arquivo.

    ![Captura de tela que mostra como compartilhamento de arquivos de toocreate no portal de saudação](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share4.png)

6. Preencha o compartilhamento de arquivos primeiro em nome de compartilhamento de arquivo hello e tamanho de saudação de toocreate de compartilhamento (até too5120 GB) de arquivo hello. Quando o compartilhamento de arquivo hello tiver sido criado, você pode montá-lo de qualquer sistema de arquivos com suporte para SMB 2.1 ou SMB 3.0. Você pode clicar em **cota** em tamanho Olá arquivo compartilhamento toochange saudação do arquivo hello a too5120 GB. Consulte também[Calculadora de preços do Azure](https://azure.microsoft.com/pricing/calculator/) tooestimate custo de armazenamento de saudação do uso de armazenamento de arquivo do Azure.

    ![Captura de tela que mostra como compartilhamento de arquivos de toocreate no portal de saudação](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share5.png)

## <a name="upload-and-download-files"></a>Carregar e baixar arquivos
1. Escolha um compartilhamento de arquivos que já tenha sido criado.

    ![Captura de tela que mostra como tooupload e baixe arquivos de Olá portal](media/storage-file-how-to-use-files-portal/use-files-portal-upload-file1.png)

2. Clique em **carregar** para abrir a interface do usuário Olá para carregamento de arquivos.

    ![Captura de tela que mostra como os arquivos de tooupload do portal de saudação](media/storage-file-how-to-use-files-portal/use-files-portal-upload-file2.png)

## <a name="connect-toofile-share"></a>Conecte-se o compartilhamento de toofile
-  Clique em **conectar** ao obter linha de comando Olá montagem Olá para compartilhamento de arquivos do Windows e Linux. Para os usuários do Linux, você também pode consultar muito[como toouse armazenamento de arquivo do Azure com Linux](storage-how-to-use-files-linux.md) para obter mais instruções de montagem para outras distribuições do Linux.

    ![Captura de tela que mostra como toomount Olá compartilhamento de arquivos](media/storage-file-how-to-use-files-portal/use-files-portal-connect.png)
-  Você pode copiar Olá comandos para montar o arquivo de compartilhamento no Windows ou Linux e execução-lo a sua máquina local ou de VM do Azure.

    ![Captura de tela que mostra os comandos de montagem de saudação para Windows e Linux](media/storage-file-how-to-use-files-portal/use-files-portal-show-mount-commands.png)

**Dica:**  
chave de acesso de conta de armazenamento da saudação do toofind para montagem, clique em **teclas de acesso de exibição para essa conta de armazenamento** final Olá Olá página de conexão.

## <a name="see-also"></a>Consulte também
Consulte estes links para obter mais informações sobre o armazenamento de arquivo do Azure.

* [Perguntas frequentes](storage-files-faq.md)
* [Solução de problemas](storage-troubleshoot-file-connection-problems.md)