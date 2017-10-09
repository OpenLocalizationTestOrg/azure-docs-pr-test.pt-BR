---
title: aaaMove tooand de dados do armazenamento de Blob com o Azure Storage Explorer | Microsoft Docs
description: Mover dados tooand do armazenamento de BLOBs do Azure usando o Azure Storage Explorer
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 10bd283f-0875-4c67-af63-6492270b7656
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 38d3bc009950c97d8474b0acceaf74814638dac0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-azure-storage-explorer"></a>Mover dados tooand do armazenamento de BLOBs do Azure usando o Azure Storage Explorer
Azure Storage Explorer é uma ferramenta gratuita da Microsoft que permite que você toowork com dados de armazenamento do Azure no Linux, Windows e macOS. Este tópico descreve como toouse-armazenamento de blob de dados tooupload e o download do Azure. Olá ferramenta pode ser baixada do [Microsoft Azure Storage Explorer](http://storageexplorer.com/).

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> Se você estiver usando a VM que foi configurado com scripts Olá fornecidos pela [máquinas virtuais de ciência de dados no Azure](machine-learning-data-science-virtual-machines.md), em seguida, o Azure Storage Explorer já está instalado na VM de saudação.
> 
> [!NOTE]
> Para um armazenamento de blob tooAzure introdução completa, consulte muito[Noções básicas de Blob do Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) e [serviço Blob do Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).   
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
Este documento assume que você tenha uma assinatura do Azure, uma conta de armazenamento e chave de armazenamento correspondente Olá para essa conta. Antes de carregar/baixar os dados, você deve conhecer o nome e a chave da sua conta do Armazenamento do Azure. 

* tooset uma assinatura do Azure, consulte [um mês avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Para obter instruções sobre como criar uma conta de armazenamento e obter informações sobre conta e chave, consulte [Sobre contas do armazenamento do Azure](../storage/common/storage-create-storage-account.md). Verifique uma chave de acesso Observação Olá para sua conta de armazenamento conforme necessário a essa conta de toohello tooconnect chave com a ferramenta de Gerenciador de armazenamento do Azure hello.
* ferramenta do Hello Azure Storage Explorer pode ser baixada do [Microsoft Azure Storage Explorer](http://storageexplorer.com/). Aceite padrões Olá durante a instalação.

<a id="explorer"></a>

## <a name="use-azure-storage-explorer"></a>Usar o Gerenciador de Armazenamento do Azure
Olá documento as etapas a seguir como tooupload/baixar dados usando o Gerenciador de armazenamento do Azure. 

1. Inicie o Gerenciador de Armazenamento do Microsoft Azure.
2. toobring backup Olá **entrar na conta de tooyour...**  assistente, selecione **configurações de conta do Azure** ícone, **adicionar uma conta** e inserir as credenciais. ![Adicionar uma conta de armazenamento do Azure](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/add-an-azure-store-account.png)
3. toobring backup Olá **conectar tooAzure armazenamento** saudação do assistente, selecione **conectar o armazenamento tooAzure** ícone. ![Conectar o armazenamento de tooAzure](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-1.png)
4. Inserir chave de acesso de saudação de sua conta de armazenamento do Azure no hello **conectar tooAzure armazenamento** assistente e, em seguida, **próximo**. ![Conectar o armazenamento de tooAzure](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-2.png)
5. Digite o nome de conta de armazenamento no hello **nome da conta** caixa e, em seguida, selecione **próximo**. ![Anexar um armazenamento externo](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/attach-external-storage.png)
6. conta de armazenamento Olá adicionada agora deve ser listada. toocreate um contêiner de blob em uma conta de armazenamento, clique com botão direito Olá **contêineres de Blob** nó nessa conta, selecione **criar contêiner de Blob**e digite um nome.
7. contêiner de tooa tooupload dados, selecione Olá Olá de contêiner e clique em do destino **carregar** botão.![ Contas de armazenamento](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/storage-accounts.png)
8. Clique em Olá **...**  toohello direito da saudação **arquivos** caixa, selecione um ou vários tooupload de arquivos do sistema de arquivos hello e clique em **carregar** toobegin carregando arquivos hello.![ Carregar arquivos](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/upload-files-to-blob.png)
9. dados de toodownload, selecionando Olá toodownload do hello correspondente contêiner de blob e clique em **baixar**. ![Baixar arquivos](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/download-files-from-blob.png)

