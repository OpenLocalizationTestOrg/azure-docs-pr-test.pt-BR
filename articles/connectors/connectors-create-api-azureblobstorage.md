---
title: "Olá aaaAdd Connector em seus aplicativos de lógica de armazenamento de BLOBs do Azure | Microsoft Docs"
description: "Comece a usar e configurar o conector de armazenamento de BLOBs do Azure Olá em um aplicativo de lógica"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b5dc3f75-6bea-420b-b250-183668d2848d
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/02/2017
ms.author: mandia; ladocs
ms.openlocfilehash: add61287ef1b2228ef9d3f54ce082807bad6858b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-blob-storage-connector-in-a-logic-app"></a>Usar o conector de armazenamento de BLOBs do Azure Olá em um aplicativo de lógica
Tooupload de conector do armazenamento de BLOBs do Azure de Olá usar, atualizar, obter e excluir blobs na conta de armazenamento, tudo dentro de um aplicativo lógico.  

Com o armazenamento de blobs do Azure, você:

* Crie seu fluxo de trabalho carregando novos projetos ou obtendo arquivos que foram atualizados recentemente.
* Use ações tooget metadados de arquivo, excluir um arquivo, copiar os arquivos e muito mais. Por exemplo, quando uma ferramenta é atualizada em um site do Azure (um gatilho), em seguida, um arquivo é atualizado no armazenamento de blobs (uma ação). 

Este tópico mostra como toouse Olá blob conector de armazenamento em um aplicativo de lógica.

toolearn mais sobre aplicativos lógicos, consulte [quais são os aplicativos lógicos](../logic-apps/logic-apps-what-are-logic-apps.md) e [criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).

toolearn mais sobre aplicativos lógicos, consulte [quais são os aplicativos lógicos](../logic-apps/logic-apps-what-are-logic-apps.md) e [criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooazure-blob-storage"></a>Conectar o armazenamento de blob tooAzure
Antes de sua lógica de aplicativo pode acessar qualquer serviço, você primeiro crie um *conexão* toohello service. Uma conexão fornece uma conectividade entre um aplicativo lógico e outro serviço. Por exemplo, conta de armazenamento do tooconnect tooa, você primeiro crie um armazenamento de blob *conexão*. toocreate uma conexão, insira as credenciais de saudação você normalmente usa o serviço de saudação tooaccess você está se conectando. Portanto, com o armazenamento do Azure, insira conexão de saudação do hello credenciais tooyour armazenamento conta toocreate. 

#### <a name="create-hello-connection"></a>Criar conexão Olá
> [!INCLUDE [Create a connection tooAzure blob storage](../../includes/connectors-create-api-azureblobstorage.md)]

## <a name="use-a-trigger"></a>Usar um gatilho
Esse conector não tem gatilhos. Use outros gatilhos toostart Olá lógica aplicativo, como um disparador de recorrência, um gatilho de HTTP Webhook, disparadores disponíveis com outros conectores e muito mais. [Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md) fornece um exemplo.

## <a name="use-an-action"></a>Usar uma ação
Uma ação é uma operação executada pelo fluxo de trabalho Olá definido em um aplicativo lógico.

1. Selecione o sinal de adição hello. Consulte várias opções: **adicionar uma ação**, **adicionar uma condição**, ou uma saudação **mais** opções.
   
    ![](./media/connectors-create-api-azureblobstorage/add-action.png)
2. Escolha **Adicionar uma ação**.
3. Na caixa de texto de saudação, digite "blob" tooget uma lista de todas as ações disponíveis de saudação.
   
    ![](./media/connectors-create-api-azureblobstorage/actions.png) 
4. Em nosso exemplo, escolha **AzureBlob – Obter metadados do arquivo usando o caminho**. Se uma conexão já existir, selecione Olá **...** (Mostrar seletor) botão tooselect um arquivo.
   
    ![](./media/connectors-create-api-azureblobstorage/sample-file.png)
   
    Se você for solicitado para obter informações de conexão do hello, digite conexão de Olá Olá detalhes toocreate. [Criar conexão Olá](connectors-create-api-azureblobstorage.md#create-the-connection) neste tópico descreve essas propriedades. 
   
   > [!NOTE]
   > Neste exemplo, obtemos Olá metadados de um arquivo. toosee Olá metadados, adicione outra ação que cria um novo arquivo usando outro conector. Por exemplo, adicione uma ação de OneDrive que cria um novo arquivo de "teste" com base nos metadados de saudação. 


5. **Salvar** as alterações (canto superior esquerdo da barra de ferramentas de saudação). Seu aplicativo lógico é salvo e pode ser habilitado automaticamente.

> [!TIP]
> [Gerenciador de armazenamento](http://storageexplorer.com/) é uma excelente ferramenta muito gerenciar várias contas de armazenamento.

## <a name="connector-specific-details"></a>Detalhes específicos do conector

Exibir quaisquer gatilhos e ações definidas em swagger Olá e também os limites de saudação [detalhes conector](/connectors/azureblobconnector/). 

## <a name="next-steps"></a>Próximas etapas
[Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md). Explorar Olá outros conectores disponíveis na lógica de aplicativos no nosso [lista APIs](apis-list.md).

