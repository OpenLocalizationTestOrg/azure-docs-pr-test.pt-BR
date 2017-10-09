---
title: "Olá aaaUse conector de margem de atraso em seus aplicativos lógicos do Azure | Microsoft Docs"
description: "Conecte-se tooSlack em seus aplicativos lógicos"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 234cad64-b13d-4494-ae78-18b17119ba24
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 6599d7b69d2147425c9fab978c5d0f93e5605f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-slack-connector"></a>Introdução ao conector de margem de atraso de saudação
O Slack é uma ferramenta de comunicação da equipe que reúne todas as comunicações de equipe em um só lugar, que pode ser pesquisado instantaneamente e está disponível onde você estiver. 

Comece pela criação de um aplicativo lógico; veja [Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="create-a-connection-tooslack"></a>Criar uma conexão tooSlack
conector de margem de atraso de saudação toouse, primeiro você cria um **conexão** Forneça detalhes de saudação para essas propriedades: 

| Propriedade | Obrigatório | Descrição |
| --- | --- | --- |
| A criptografia do token |Sim |Fornecer credenciais do Slack |

Siga essas etapas toosign em atraso e configuração Olá completa de saudação atraso **conexão** em seu aplicativo lógica:

1. Selecione **Recorrência**
2. Selecione uma **Frequência** e insira um **Intervalo**
3. Selecione **Adicionar uma ação**  
   ![Configurar a Margem de atraso][1]  
4. Insira o atraso na caixa de pesquisa hello e aguarde Olá pesquisa tooreturn todas as entradas com atraso no nome da saudação
5. Selecione **Margem de atraso – Postar mensagem**
6. Selecione **entrar tooSlack**:  
   ![Configurar a Margem de atraso][2]
7. Forneça seu toosign margem de atraso de credenciais no aplicativo de hello tooauthorize    
   ![Configurar a Margem de atraso][3]  
8. Você será Log redirecionado tooyour organização na página. **Autorizar** toointeract Slack com seu aplicativo lógico:      
   ![Configurar a Margem de atraso][5] 
9. Após a conclusão da autorização Olá você será redirecionado tooyour lógica aplicativo toocomplete-Configurando Olá **atraso - obter todas as mensagens** seção. Adicione outros gatilhos e outras ações necessárias.  
   ![Configurar a Margem de atraso][6]
10. Salve seu trabalho selecionando **salvar** na barra de menus do hello acima.

## <a name="connector-specific-details"></a>Detalhes específicos do conector

Exibir quaisquer gatilhos e ações definidas em swagger Olá e também os limites de saudação [detalhes conector](/connectors/slack/).

## <a name="more-connectors"></a>Mais conectores
Voltar toohello [lista APIs](apis-list.md).

[1]: ./media/connectors-create-api-slack/connectionconfig1.png
[2]: ./media/connectors-create-api-slack/connectionconfig2.png 
[3]: ./media/connectors-create-api-slack/connectionconfig3.png
[4]: ./media/connectors-create-api-slack/connectionconfig4.png
[5]: ./media/connectors-create-api-slack/connectionconfig5.png
[6]: ./media/connectors-create-api-slack/connectionconfig6.png
