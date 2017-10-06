---
title: "conector do Outlook do Office 365 aaaAdd Olá em seus aplicativos lógicos | Microsoft Docs"
description: "Crie aplicativos lógicos interação de tooenable de conector do Office 365 com o Office 365. Por exemplo: criação, edição e atualização de itens de calendário e contatos."
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b2f6cc2c-bba2-493a-b0ba-841785462a80
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 86a573c9c54701de3d3f0500d19eaf545e0710ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-office-365-outlook-connector"></a>Introdução ao conector do Outlook do Office 365 Olá
conector do Outlook do Office 365 Olá permite interação com o Outlook no Office 365. Usar este conector toocreate, editar, contatos de atualização e itens de calendário e também obter, enviar e responder tooemail.

Com o Outlook do Office 365, você pode:

* Crie o fluxo de trabalho usando recursos de email e calendário Olá no Office 365. 
* Use gatilhos toostart seu fluxo de trabalho quando há um novo email, quando um item de calendário é atualizado e muito mais.
* Use ações toosend um email, criar um novo evento de calendário e muito mais. Por exemplo, quando há um novo objeto no Salesforce (um gatilho), envie um email tooyour Outlook do Office 365 (uma ação). 

Este tópico mostra como toouse Olá conector do Outlook do Office 365 em um aplicativo lógico e também lista Olá gatilhos e ações.

> [!NOTE]
> Esta versão do artigo Olá aplica tooLogic aplicativos GA (disponibilidade geral).
> 
> 

toolearn mais sobre aplicativos lógicos, consulte [quais são os aplicativos lógicos](../logic-apps/logic-apps-what-are-logic-apps.md) e [criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-toooffice-365"></a>Conecte-se tooOffice 365
Antes de sua lógica de aplicativo pode acessar qualquer serviço, você primeiro crie um *conexão* toohello service. Uma conexão fornece uma conectividade entre um aplicativo lógico e outro serviço. Por exemplo, tooconnect tooOffice 365 Outlook, primeiro é necessário um Office 365 *conexão*. toocreate uma conexão, insira as credenciais de saudação você normalmente usa o serviço de saudação tooaccess desejar tooconnect para. Portanto com o Outlook do Office 365, digite Olá credenciais tooyour conexão de saudação do Office 365 conta toocreate.

## <a name="create-hello-connection"></a>Criar conexão Olá
> [!INCLUDE [Steps toocreate a connection tooOffice 365](../../includes/connectors-create-api-office365-outlook.md)]
> 
> 

## <a name="use-a-trigger"></a>Usar um gatilho
Um gatilho é um evento que pode ser o fluxo de trabalho do hello toostart usado definido em um aplicativo lógico. Gatilhos "sondagem" hello serviço em um intervalo e a frequência com que você deseja. [Saiba mais sobre gatilhos](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. No aplicativo de lógica de hello, digite "office 365" tooget uma lista dos gatilhos hello:  
   
    ![](./media/connectors-create-api-office365-outlook/office365-trigger.png)
2. Escolha **Outlook do Office 365 – quando um evento futuro for iniciado em breve**. Se uma conexão já existir, selecione um calendário na lista suspensa de saudação.
   
    ![](./media/connectors-create-api-office365-outlook/sample-calendar.png)
   
    Se você é solicitada toosign em, digite Olá logon na conexão de saudação toocreate detalhes. [Criar conexão Olá](connectors-create-api-office365-outlook.md#create-the-connection) neste tópico lista as etapas de saudação. 
   
   > [!NOTE]
   > Neste exemplo, o aplicativo de lógica de saudação é executado quando um evento de calendário é atualizado. resultados de saudação toosee deste gatilho, adicione outra ação que envia uma mensagem de texto. Por exemplo, adicionar Olá Twilio *enviar mensagem* ação textos quando hello evento de calendário está iniciando em 15 minutos. 
   > 
   > 
3. Selecione Olá **editar** botão e defina Olá **frequência** e **intervalo** valores. Por exemplo, se você quiser Olá gatilho toopoll a cada 15 minutos, em seguida, definir Olá **frequência** muito**minuto**e conjunto hello **intervalo** muito**15**. 
   
    ![](./media/connectors-create-api-office365-outlook/calendar-settings.png)
4. **Salvar** as alterações (canto superior esquerdo da barra de ferramentas de saudação). Seu aplicativo lógico é salvo e pode ser habilitado automaticamente.

## <a name="use-an-action"></a>Usar uma ação
Uma ação é uma operação executada pelo fluxo de trabalho Olá definido em um aplicativo lógico. [Saiba mais sobre ações](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. Selecione o sinal de adição hello. Consulte várias opções: **adicionar uma ação**, **adicionar uma condição**, ou uma saudação **mais** opções.
   
    ![](./media/connectors-create-api-office365-outlook/add-action.png)
2. Escolha **Adicionar uma ação**.
3. Na caixa de texto de saudação, digite "office 365" tooget uma lista de todas as ações disponíveis de saudação.
   
    ![](./media/connectors-create-api-office365-outlook/office365-actions.png) 
4. Em nosso exemplo, escolha **Outlook do Office 365 – Criar contato**. Se uma conexão já existir, escolha Olá **ID da pasta**, **nome**e outras propriedades:  
   
    ![](./media/connectors-create-api-office365-outlook/office365-sampleaction.png)
   
    Se você for solicitado para obter informações de conexão do hello, digite conexão de Olá Olá detalhes toocreate. [Criar conexão Olá](connectors-create-api-office365-outlook.md#create-the-connection) neste tópico descreve essas propriedades. 
   
   > [!NOTE]
   > Neste exemplo, criamos um novo contato no Outlook do Office 365. Você pode usar a saída de outro disparador toocreate Olá entre em contato com. Por exemplo, adicionar Olá SalesForce *quando um objeto é criado* gatilho. Em seguida, adicione Olá Outlook do Office 365 *criar contato* ação que usa Olá SalesForce campos toocreate Olá novo novo contato no Office 365. 
   > 
   > 
5. **Salvar** as alterações (canto superior esquerdo da barra de ferramentas de saudação). Seu aplicativo lógico é salvo e pode ser habilitado automaticamente.

## <a name="connector-specific-details"></a>Detalhes específicos do conector

Exibir quaisquer gatilhos e ações definidas em swagger Olá e também os limites de saudação [detalhes conector](/connectors/office365connector/). 

## <a name="next-steps"></a>Próximas etapas
[Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md). Explorar Olá outros conectores disponíveis na lógica de aplicativos no nosso [lista APIs](apis-list.md).

