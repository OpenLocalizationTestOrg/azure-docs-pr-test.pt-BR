---
title: "conector de aaaDropbox em aplicativos do Azure lógica | Microsoft Docs"
description: "Crie Aplicativos Lógicos com o serviço de Aplicativo do Azure. Conecte tooDropbox toomanage seus arquivos. Você pode executar várias ações, como carregar, atualizar, obter e excluir arquivos no Dropbox."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: cb0ae033-aba7-4ac9-beaa-be561a0f0cac
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 1f307477836104c0bc0008341604a1400860987f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-dropbox-connector"></a>Introdução ao conector do Dropbox Olá
Conecte tooDropbox toomanage seus arquivos. Você pode executar várias ações, como carregar, atualizar, obter e excluir arquivos no Dropbox.

toouse [qualquer conector](apis-list.md), primeiro é necessário toocreate um aplicativo lógico. Você pode começar [criando um aplicativo lógico agora](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-toodropbox"></a>Conecte-se tooDropbox
Antes de sua lógica de aplicativo pode acessar qualquer serviço, primeiro é necessário toocreate um *conexão* toohello service. Uma conexão fornece uma conectividade entre um aplicativo lógico e outro serviço. Por exemplo, em ordem tooconnect tooDropbox, primeiro é necessário um Dropbox *conexão*. toocreate uma conexão, você precisaria de credenciais de saudação tooprovide você normalmente usa o serviço de saudação tooaccess para que desejar tooconnect. Assim, no exemplo do Dropbox hello, seria necessário Olá credenciais tooyour conta do Dropbox na ordem toocreate Olá conexão tooDropbox. [Saiba mais sobre conexões]()

### <a name="create-a-connection-toodropbox"></a>Criar uma conexão tooDropbox
> [!INCLUDE [Steps toocreate a connection tooDropbox](../../includes/connectors-create-api-dropbox.md)]
> 
> 

## <a name="use-a-dropbox-trigger"></a>Usar um gatilho do Dropbox
Um gatilho é um evento que pode ser o fluxo de trabalho do hello toostart usado definido em um aplicativo lógico. [Saiba mais sobre gatilhos](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

Neste exemplo, usaremos Olá **quando um arquivo é criado** gatilho. Quando ocorre esse gatilho, chamaremos Olá **obter conteúdo do arquivo usando o caminho** ação Dropbox. 

1. Digite *dropbox* na caixa de pesquisa Olá no designer de aplicativos lógicos hello, selecione Olá **Dropbox - quando um arquivo é criado** gatilho.      
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger.PNG)  
2. Selecione a pasta de saudação no qual você deseja tootrack criação de arquivos. Selecione... (identificado na caixa Olá vermelho) e procurar toohello pasta tooselect para gatilho de saudação da entrada.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger-2.PNG)  

## <a name="use-a-dropbox-action"></a>Usar uma ação do Dropbox
Uma ação é uma operação executada pelo fluxo de trabalho Olá definido em um aplicativo lógico. [Saiba mais sobre ações](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

Agora que hello gatilho foi adicionado, siga essas etapas tooadd uma ação que receberá o conteúdo do arquivo hello novo.

1. Selecione **+ nova etapa** ação de saudação tooadd você gostaria que tootake quando um novo arquivo é criado.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action.PNG)
2. Escolha **Adicionar uma ação**. Essa caixa de pesquisa de Olá abre onde você pode procurar qualquer ação que você gostaria de tootake.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-2.PNG)
3. Digite *dropbox* toosearch para tooDropbox de ações relacionadas.  
4. Selecione **Dropbox - obter conteúdo do arquivo usando o caminho** como Olá tootake ação quando um novo arquivo é criado no hello selecionado pasta Dropbox. bloco de controle de ação de saudação é aberto. Você será solicitado tooauthorize tooaccess de aplicativo sua lógica seu Dropbox conta se você não tiver feito isso anteriormente.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-3.PNG)  
5. Selecione... (localizado no lado direito de saudação do hello **caminho do arquivo** controle) e procure o caminho do arquivo toohello você gostaria que toouse. Ou use Olá **caminho do arquivo** token toospeed a sua criação de lógica de aplicativo.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-4.PNG)  
6. Salve seu trabalho e criar um novo arquivo no Dropbox tooactivate seu fluxo de trabalho.  

## <a name="connector-specific-details"></a>Detalhes específicos do conector

Exibir quaisquer gatilhos e ações definidas em swagger Olá e também os limites de saudação [detalhes conector](/connectors/dropbox/).

## <a name="more-connectors"></a>Mais conectores
Voltar toohello [lista APIs](apis-list.md).
