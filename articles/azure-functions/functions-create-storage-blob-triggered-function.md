---
title: "uma função no Azure disparado pelo armazenamento de Blob de aaaCreate | Microsoft Docs"
description: "Use funções do Azure toocreate uma função sem servidor que é invocada por itens adicionados tooAzure armazenamento de Blob."
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: d6bff41c-a624-40c1-bbc7-80590df29ded
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: acb7d29abb07a22da11d0e65d2ed54591f8e3f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-azure-blob-storage"></a>Criar uma função disparada pelo Armazenamento de Blobs do Azure

Saiba como toocreate uma função disparada quando os arquivos são carregados tooor atualizado no armazenamento de BLOBs do Azure.

![Exibir mensagem nos logs de saudação.](./media/functions-create-storage-blob-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>Pré-requisitos

+ Baixe e instale Olá [Microsoft Azure Storage Explorer](http://storageexplorer.com/).
+ Uma assinatura do Azure. Se você não tiver uma, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Criar um Aplicativo de funções do Azure

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Aplicativo de funções criado com êxito.](./media/functions-create-first-azure-function/function-app-create-success.png)

Em seguida, crie uma função no novo aplicativo de função hello.

<a name="create-function"></a>

## <a name="create-a-blob-storage-triggered-function"></a>Criar uma função disparada pelo Armazenamento de Blobs

1. Expanda seu aplicativo de função e clique em Olá  **+**  botão Avançar muito**funções**. Se esta for a primeira função hello em seu aplicativo de função, selecione **função personalizada**. Isso exibe o conjunto completo de saudação de modelos de função.

    ![Página de início rápido de funções no hello portal do Azure](./media/functions-create-storage-blob-triggered-function/add-first-function.png)

2. Selecione Olá **BlobTrigger** modelo para o idioma desejado e usar configurações de saudação conforme especificado na tabela de saudação.

    ![Crie função de armazenamento disparado Blob hello.](./media/functions-create-storage-blob-triggered-function/functions-create-blob-storage-trigger-portal.png)

    | Configuração | Valor sugerido | Descrição |
    |---|---|---|
    | **Caminho**   | mycontainer/{name}    | Local no Armazenamento de Blobs que está sendo monitorada. nome do arquivo de saudação do blob Olá é passado na associação de saudação como Olá _nome_ parâmetro.  |
    | **Conexão da conta de armazenamento** | AzureWebJobStorage | Você pode usar a conexão de conta de armazenamento Olá já está sendo usado pelo seu aplicativo de função ou criar um novo.  |
    | **Nomeie sua função** | Exclusivo no aplicativo de funções | O nome dessa função disparada pelo blob. |

3. Clique em **criar** toocreate sua função.

Em seguida, conecte-se a conta de armazenamento do Azure tooyour e criar hello **mycontainer** contêiner.

## <a name="create-hello-container"></a>Criar contêiner Olá

1. Em sua função, clique em **Integrar**, expanda **Documentação**e copie **Nome da conta** e **Chave de conta**. Você usar a conta de armazenamento essas credenciais tooconnect toohello. Se você já se conectou a sua conta de armazenamento, ignore toostep 4.

    ![Obter credenciais de conexão de conta de armazenamento hello.](./media/functions-create-storage-blob-triggered-function/functions-storage-account-connection.png)

1. Executar Olá [Microsoft Azure Storage Explorer](http://storageexplorer.com/) ferramenta, clique em Olá conectar ícone Olá esquerda, escolha **usar um nome de conta de armazenamento e chave**e clique em **próximo**.

    ![Execute a ferramenta de Gerenciador de conta de armazenamento de saudação.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-1.png)

1. Digite hello **nome da conta** e **chave de conta** da etapa 1, clique em **próximo** e, em seguida, **conectar**. 

    ![Insira as credenciais de armazenamento hello e conecte-se.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-2.png)

1. Expanda a conta de armazenamento Olá anexado, clique no **contêineres de Blob**, clique em **criar contêiner de blob**, tipo `mycontainer`, e pressione enter.

    ![Crie uma fila de armazenamento.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-create-blob-container.png)

Agora que você tem um contêiner de blob, você pode testar a função hello carregando um contêiner de toohello do arquivo.

## <a name="test-hello-function"></a>Função de saudação do teste

1. Em Olá portal do Azure, procurar tooyour função expanda Olá **Logs** na parte inferior da saudação da página de saudação e verifique se esse fluxo de log não está em pausa.

1. No Gerenciador de Armazenamento, expanda sua conta de armazenamento, **Contêineres de blob** e **mycontainer**. Clique em **Carregar** e depois em **Carregar arquivos...**.

    ![Carregar um contêiner de blob de toohello do arquivo.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-upload-file-blob.png)

1. Em Olá **carregar arquivos** caixa de diálogo, clique em Olá **arquivos** campo. Procurar arquivo tooa no computador local, como um arquivo de imagem, selecione-o e clique em **abrir** e **carregar**.

1. Voltar tooyour função logs e verifique se que esse blob Olá foi lido.

   ![Exibir mensagem nos logs de saudação.](./media/functions-create-storage-blob-triggered-function/functions-blob-storage-trigger-view-logs.png)

    >[!NOTE]
    > Quando seu aplicativo de função é executado no plano de consumo saudação padrão, pode haver um atraso de backup tooseveral minutos entre Olá blob que está sendo adicionado ou atualizado e Olá de função que está sendo disparado. Se você precisar de baixa latência em suas funções disparadas por blob, considere executar seu aplicativo de funções em um Plano do Serviço de Aplicativo.

## <a name="clean-up-resources"></a>Limpar recursos

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Próximas etapas

Você criou uma função que é executada quando um blob é adicionado tooor atualizado no armazenamento de Blob. 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Para obter mais informações sobre gatilhos de armazenamento de blobs, consulte [Associações de Armazenamento de Blobs do Azure Functions](functions-bindings-storage-blob.md).
