---
title: "conector de OneDrive aaaAdd Olá em seus aplicativos lógicos | Microsoft Docs"
description: "Visão geral do conector do OneDrive Olá com parâmetros de API REST"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 47a8582a-1b1a-4fc3-beb5-97c60c4306fe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 8303794bb3c2844de288f87f40639abb84c160fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-onedrive-connector"></a>Introdução ao conector do OneDrive Olá
Conecte tooOneDrive toomanage seus arquivos, incluindo o carregamento, get, excluir arquivos e muito mais. 

Com o OneDrive, você: 

* Compile seu fluxo de trabalho armazenando os arquivos no OneDrive ou atualize os arquivos existentes no OneDrive. 
* Use gatilhos toostart seu fluxo de trabalho quando um arquivo é criado ou atualizado no OneDrive.
* Use ações toocreate um arquivo, excluir um arquivo e muito mais. Por exemplo, quando um novo email do Office 365 for recebido com um anexo (um gatilho), crie um novo arquivo no OneDrive (uma ação).

Este tópico mostra como toouse Olá conector OneDrive em um aplicativo lógico e também lista Olá gatilhos e ações.

toolearn mais sobre aplicativos lógicos, consulte [quais são os aplicativos lógicos](../logic-apps/logic-apps-what-are-logic-apps.md) e [criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooonedrive"></a>Conecte-se tooOneDrive
Antes de sua lógica de aplicativo pode acessar qualquer serviço, você primeiro crie um *conexão* toohello service. Uma conexão fornece uma conectividade entre um aplicativo lógico e outro serviço. Por exemplo, tooconnect tooOneDrive, primeiro é necessário um OneDrive *conexão*. toocreate uma conexão, insira as credenciais de saudação você normalmente usa o serviço de saudação tooaccess desejar tooconnect para. Portanto, com o OneDrive, digite conexão de saudação do hello credenciais tooyour OneDrive conta toocreate.

### <a name="create-hello-connection"></a>Criar conexão Olá
> [!INCLUDE [Steps toocreate a connection tooOneDrive](../../includes/connectors-create-api-onedrive.md)]
> 
> 

## <a name="use-a-trigger"></a>Usar um gatilho
Um gatilho é um evento que pode ser o fluxo de trabalho do hello toostart usado definido em um aplicativo lógico. Gatilhos "sondagem" hello serviço em um intervalo e a frequência com que você deseja. [Saiba mais sobre gatilhos](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. No aplicativo de lógica de hello, digite "onedrive" tooget uma lista dos gatilhos hello:  
   
    ![](./media/connectors-create-api-onedrive/onedrive-1.png)
2. Escolha **Quando um arquivo é modificado**. Se uma conexão já existir, selecione Olá seletor Mostrar botão tooselect uma pasta.
   
    ![](./media/connectors-create-api-onedrive/sample-folder.png)
   
    Se você é solicitada toosign em, digite Olá logon na conexão de saudação toocreate detalhes. [Criar conexão Olá](connectors-create-api-onedrive.md#create-the-connection) neste tópico lista as etapas de saudação. 
   
   > [!NOTE]
   > Neste exemplo, Olá lógica aplicativo é executado quando um arquivo na pasta Olá que preferir é atualizado. resultados de saudação toosee deste gatilho, adicione outra ação que envia um email. Por exemplo, adicionar Olá Outlook do Office 365 *enviar um email* ação que envia email quando um arquivo é atualizado. 

3. Selecione Olá **editar** botão e defina Olá **frequência** e **intervalo** valores. Por exemplo, se você quiser Olá gatilho toopoll a cada 15 minutos, em seguida, definir Olá **frequência** muito**minuto**e conjunto hello **intervalo** muito**15**. 
   
    ![](./media/connectors-create-api-onedrive/trigger-properties.png)
4. **Salvar** as alterações (canto superior esquerdo da barra de ferramentas de saudação). Seu aplicativo lógico é salvo e pode ser habilitado automaticamente.

## <a name="use-an-action"></a>Usar uma ação
Uma ação é uma operação executada pelo fluxo de trabalho Olá definido em um aplicativo lógico. [Saiba mais sobre ações](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. Selecione o sinal de adição hello. Consulte várias opções: **adicionar uma ação**, **adicionar uma condição**, ou uma saudação **mais** opções.
   
    ![](./media/connectors-create-api-onedrive/add-action.png)
2. Escolha **Adicionar uma ação**.
3. Na caixa de texto de saudação, digite "onedrive" tooget uma lista de todas as ações disponíveis de saudação.
   
    ![](./media/connectors-create-api-onedrive/onedrive-actions.png) 
4. Em nosso exemplo, escolha **OneDrive – criar arquivo**. Se uma conexão já existir, selecione Olá **caminho da pasta** tooput Olá do arquivo, digite Olá **nome de arquivo**e escolha Olá **conteúdo do arquivo** desejado:  
   
    ![](./media/connectors-create-api-onedrive/sample-action.png)
   
    Se você for solicitado para obter informações de conexão do hello, digite conexão de Olá Olá detalhes toocreate. [Criar conexão Olá](connectors-create-api-onedrive.md#create-the-connection) neste tópico descreve essas propriedades. 
   
   > [!NOTE]
   > Neste exemplo, podemos criar um novo arquivo em uma pasta do OneDrive. Você pode usar a saída de outro arquivo do gatilho toocreate Olá OneDrive. Por exemplo, adicionar Olá Outlook do Office 365 *quando um novo email chega* gatilho. Em seguida, adicione Olá OneDrive *criar arquivo* ação que usa hello anexos e campos de tipo de conteúdo dentro de um arquivo ForEach toocreate Olá novo no OneDrive. 
   > 
   > ![](./media/connectors-create-api-onedrive/foreach-action.png)

5. **Salvar** as alterações (canto superior esquerdo da barra de ferramentas de saudação). Seu aplicativo lógico é salvo e pode ser habilitado automaticamente.


## <a name="connector-specific-details"></a>Detalhes específicos do conector

Exibir quaisquer gatilhos e ações definidas em swagger Olá e também os limites de saudação [detalhes conector](/connectors/onedriveconnector/).

## <a name="more-connectors"></a>Mais conectores
Voltar toohello [lista APIs](apis-list.md).
