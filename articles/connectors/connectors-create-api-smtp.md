---
title: "conector de aaaSMTP em aplicativos do Azure lógica | Microsoft Docs"
description: "Crie aplicativos lógicos com o serviço de Aplicativo do Azure. Conecte-se tooSMTP toosend email."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d4141c08-88d7-4e59-a757-c06d0dc74300
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 36bb836851014d24f2e069fda8376ad7a08c943b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-smtp-connector"></a>Introdução ao conector de SMTP Olá
Conecte-se tooSMTP toosend email.

toouse [qualquer conector](apis-list.md), primeiro é necessário toocreate um aplicativo lógico. Você pode começar [criando um aplicativo lógico agora mesmo](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-toosmtp"></a>Conecte-se tooSMTP
Antes de sua lógica de aplicativo pode acessar qualquer serviço, primeiro é necessário toocreate um *conexão* toohello service. Uma [conexão](connectors-overview.md) fornece uma conectividade entre um aplicativo lógico e outro serviço. Por exemplo, tooconnect tooSMTP, primeiro é necessário um SMTP *conexão*. toocreate uma conexão, insira as credenciais de saudação você normalmente usa o serviço de saudação tooaccess você se conectar ao. Assim, no exemplo hello SMTP, insira o nome de conexão de tooyour de credenciais de Olá, endereço do servidor SMTP e usuário logon informações toocreate Olá conexão tooSMTP.  

### <a name="create-a-connection-toosmtp"></a>Criar uma conexão tooSMTP
> [!INCLUDE [Steps toocreate a connection tooSMTP](../../includes/connectors-create-api-smtp.md)]
> 
> 

## <a name="use-an-smtp-trigger"></a>Usar um gatilho de SMTP
Um gatilho é um evento que pode ser o fluxo de trabalho do hello toostart usado definido em um aplicativo lógico. [Saiba mais sobre gatilhos](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

Neste exemplo, porque o SMTP não tem um gatilho de seu próprio, vamos usar Olá **Salesforce - quando um objeto é criado** gatilho. Esse gatilho é ativado quando um novo objeto é criado no Salesforce. Para nosso exemplo, vamos defini-lo, de modo que toda vez que um novo cliente potencial é criado no Salesforce, uma *enviar email* ação ocorre por meio do conector SMTP de saudação com uma notificação de saudação novo cliente potencial que está sendo criado.

1. Digite *salesforce* na caixa de pesquisa Olá no designer de aplicativos de lógica de saudação selecione Olá **Salesforce - quando um objeto é criado** gatilho.  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-1.png)  
2. Olá **quando um objeto é criado** controle é exibido.
   ![](../../includes/media/connectors-create-api-salesforce/trigger-2.png)  
3. Selecione Olá **tipo de objeto** , em seguida, selecione *levar* da lista de saudação de objetos. Nessa etapa, instruímos sobre a criação de um gatilho que notificará seu aplicativo lógico sempre que um novo cliente potencial for criado no Salesforce.  
   ![](../../includes/media/connectors-create-api-salesforce/trigger3.png)  
4. gatilho Olá foi criado.  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-4.png)  

## <a name="use-an-smtp-action"></a>Usar uma ação de SMTP
Uma ação é uma operação executada pelo fluxo de trabalho Olá definido em um aplicativo lógico. [Saiba mais sobre ações](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

Agora que hello gatilho foi adicionado, siga estes passos tooadd um SMTP ação que ocorrerá quando um novo cliente potencial é criado no Salesforce.

1. Selecione **+ nova etapa** ação de saudação tooadd você gostaria que tootake quando um novo cliente potencial é criado.  
   ![](../../includes/media/connectors-create-api-salesforce/trigger4.png)  
2. Escolha **Adicionar uma ação**. Essa caixa de pesquisa de Olá abre onde você pode procurar qualquer ação que você gostaria de tootake.  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-2.png)  
3. Digite *smtp* toosearch para tooSMTP de ações relacionadas.  
4. Selecione **SMTP - Enviar Email** como Olá tootake ação quando o cliente potencial Olá é criado. bloco de controle de ação de saudação é aberto. Você terá tooestablish sua conexão smtp em bloco designer Olá se você não tiver feito isso anteriormente.  
   ![](../../includes/media/connectors-create-api-smtp/smtp-2.png)    
5. Insira suas informações de email desejados no hello **SMTP - Enviar Email** bloco.  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-4.PNG)  
6. Salve seu trabalho na ordem tooactivate seu fluxo de trabalho.  

## <a name="connector-specific-details"></a>Detalhes específicos do conector

Exibir quaisquer gatilhos e ações definidas em swagger Olá e também os limites de saudação [detalhes conector](/connectors/smtpconnector/).

## <a name="more-connectors"></a>Mais conectores
Voltar toohello [lista APIs](apis-list.md).
