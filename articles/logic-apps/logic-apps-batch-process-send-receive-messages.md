---
title: "aaaBatch processar mensagens como um grupo ou uma coleção - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Enviar e receber mensagens para processamento em lotes em aplicativos lógicos"
keywords: lote, processo em lote
author: jonfancey
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/7/2017
ms.author: LADocs; estfan; jonfan
ms.openlocfilehash: 2603db71ee0659d5b6bf5ce3d32f1b0d13c34194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="send-receive-and-batch-process-messages-in-logic-apps"></a>Enviar, receber e processar mensagens em lote nos aplicativos lógicos

mensagens de tooprocess juntas em grupos, você pode enviar dados tooa de itens ou mensagens de *lote*e depois processar os itens como um lote. Essa abordagem é útil quando você deseja toomake-se de itens de dados são agrupados de forma específica e são processados em conjunto. 

Você pode criar aplicativos lógicos que recebem itens como um lote usando Olá **lote** gatilho. Você pode criar aplicativos lógicos que enviam itens tooa lote usando Olá **lote** ação.

Este tópico mostra como você pode compilar uma solução de envio em lote executando estas tarefas: 

* [Criar um aplicativo lógico que receba e colete itens como um lote](#batch-receiver). Este aplicativo de lógica de "destinatário lote" Especifica Olá lote nome e versão critérios toomeet antes Olá receptor lógica aplicativo libera e processa os itens. 

* [Criar um aplicativo de lógica que envia itens tooa lote](#batch-sender). Este aplicativo de lógica de "remetente lote" Especifica onde toosend itens, que devem ser um aplicativo de lógica de destinatário existente do lote. Você pode também especificar uma chave exclusiva, como um número de cliente, muito "partition" ou dividir o lote de destino Olá em subconjuntos com base na chave. Dessa forma, todos os itens com essa chave serão coletados e processados em conjunto. 

## <a name="requirements"></a>Requisitos

toofollow neste exemplo, você precisa dos seguintes itens:

* Uma assinatura do Azure. Se você não tiver uma assinatura, poderá [iniciar com uma conta gratuita do Azure](https://azure.microsoft.com/free/). Caso contrário, você pode [inscrever-se para uma assinatura Pré-paga](https://azure.microsoft.com/pricing/purchase-options/).

* Conhecimento básico sobre [como toocreate os aplicativos lógicos](../logic-apps/logic-apps-create-a-logic-app.md) 

* Uma conta de email com qualquer [provedor de email com suporte do Aplicativo Lógico do Azure](../connectors/apis-list.md)

<a name="batch-receiver"></a>

## <a name="create-logic-apps-that-receive-messages-as-a-batch"></a>Criar aplicativos lógicos que recebem mensagens como um lote

Antes de enviar o lote de tooa de mensagens, você primeiro deve criar um aplicativo de lógica de "destinatário lote" com hello **lote** gatilho. Dessa forma, você pode selecionar este aplicativo de lógica do destinatário ao criar aplicativo de lógica de remetente hello. Para o receptor hello, você pode especificar nome do lote hello, critérios de liberação e outras configurações. 

Aplicativos de lógica de remetente precisam saber onde toosend itens, enquanto os aplicativos lógicos receptor não precisam tooknow nada sobre remetentes hello.

1. Em Olá [portal do Azure](https://portal.azure.com), crie um aplicativo de lógica com esse nome: "BatchReceiver" 

2. No Designer de aplicativos de lógica, adicionar Olá **lote** gatilho que inicia o fluxo de trabalho do aplicativo de lógica. Na caixa de pesquisa hello, digite "lote" como filtro. Selecionar este gatilho: **Lote – Mensagens em lote**

   ![Adicionar o gatilho Lote](./media/logic-apps-batch-process-send-receive-messages/add-batch-receiver-trigger.png)

3. Forneça um nome para o lote hello e especificar critérios de liberação de lote hello, por exemplo:

   * **Nome do lote**: Olá nome usado tooidentify Olá lote, que é "TestBatch" neste exemplo.
   * **Contagem de mensagens**: Olá o número de mensagens toohold como um lote antes de liberar para processamento, o que é "5", neste exemplo.

   ![Fornecer detalhes sobre o gatilho Lote](./media/logic-apps-batch-process-send-receive-messages/receive-batch-trigger-details.png)

4. Adicione outra ação que envia um email quando Olá lote gatilho é acionado. Cada lote de saudação do tempo tiver cinco itens, Olá lógica aplicativo envia um email.

   1. Em um gatilho de lote hello, escolha **+ nova etapa** > **adicionar uma ação**.

   2. Na caixa de pesquisa hello, digite "email" como filtro.
   Com base em seu provedor de email, selecione um conector de email.
   
      Por exemplo, se você tiver uma conta corporativa ou de estudante, selecione Olá conector do Outlook do Office 365. 
      Se você tiver uma conta do Gmail, selecione o conector do Gmail hello.

   3. Selecione essa ação para o conector:  **{*provedor de email*} – Enviar um email**

      Por exemplo:

      ![Selecione a ação "Enviar um email" para o seu provedor de email](./media/logic-apps-batch-process-send-receive-messages/add-send-email-action.png)

5. Se você não tiver criado uma conexão para o seu provedor de email, forneça suas credenciais de email para autenticação quando receber a solicitação. Saiba mais sobre [como autenticar suas credenciais de email](../logic-apps/logic-apps-create-a-logic-app.md).

6. Definir propriedades de saudação para ação Olá que você acabou de adicionar.

   * Em Olá **para** , digite o endereço de email do destinatário hello. 
   Para fins de teste, você pode usar seu próprio endereço de email.

   * Em Olá **assunto** caixa quando hello **conteúdo dinâmico** é exibida na lista, selecione Olá **nome da partição** campo.

     ![Na lista de "Conteúdo dinâmico" Olá, selecione "Nome de partição"](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details.png)

     Em uma seção posterior, você pode especificar uma chave de partição exclusivo que divide Olá lote de destino em lógica define toowhere, você pode enviar mensagens. 
     Cada conjunto tem um número exclusivo que é gerado pelo aplicativo de lógica de remetente hello. 
     Esse recurso permite usar um único lote com várias subconjuntos e defina cada subconjunto com nome hello que você fornecer.

   * Em Olá **corpo** caixa quando hello **conteúdo dinâmico** é exibida na lista, selecione Olá **Id da mensagem** campo.

     ![Para "Corpo", selecione "Id de Mensagem"](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details-for-each.png)

     Como entrada Olá para ação de email de envio de saudação é uma matriz, designer de saudação adiciona automaticamente um **para cada** loop em torno de saudação **enviar um email** ação. 
     Esse loop age Olá interna em cada item no lote de saudação. 
     Assim, com hello lote gatilho conjunto toofive itens, você tem cinco emails que cada gatilho de saudação do tempo é acionado.

7.  Agora que você criou um aplicativo lógico destinatário do lote, salve-o.

    ![Salve seu aplicativo lógico](./media/logic-apps-batch-process-send-receive-messages/save-batch-receiver-logic-app.png)

<a name="batch-sender"></a>

## <a name="create-logic-apps-that-send-messages-tooa-batch"></a>Criar aplicativos lógicos que enviar mensagens tooa lote

Agora, crie um ou mais aplicativos de lógica que enviar itens toohello lote definido pelo aplicativo de lógica de receptor de saudação. Para o remetente hello, você pode especificar Olá receptor lógica aplicativo e nome do lote, conteúdo da mensagem e outras configurações. Opcionalmente, você pode fornecer um lote de saudação toodivide chave exclusiva de partição em itens de toocollect subconjuntos com essa chave.

Aplicativos de lógica de remetente precisam saber onde toosend itens, enquanto os aplicativos lógicos receptor não precisam tooknow nada sobre remetentes hello.

1. Crie outro aplicativo lógico com este nome: "RemetenteLote"

   1. Na caixa de pesquisa hello, digite "recurrence" como filtro. 
   Selecione este gatilho: **Agenda – Recorrência**

      ![Adicionar gatilho hello "Agenda de recorrência"](./media/logic-apps-batch-process-send-receive-messages/add-schedule-trigger-batch-receiver.png)

   2. Definir Olá frequência e o aplicativo lógico de remetente de saudação do intervalo toorun a cada minuto.

      ![Defina a frequência e o intervalo do gatilho de recorrência](./media/logic-apps-batch-process-send-receive-messages/recurrence-trigger-batch-receiver-details.png)

2. Adicione uma nova etapa para enviar mensagens tooa lote.

   1. Em um gatilho de recorrência hello, escolha **+ nova etapa** > **adicionar uma ação**.

   2. Na caixa de pesquisa hello, digite "lote" como filtro. 

   3. Selecione esta ação: **enviar mensagens toobatch – escolha um fluxo de trabalho de aplicativos lógicos com o gatilho de lote**

      ![Selecione "Enviar mensagens toobatch"](./media/logic-apps-batch-process-send-receive-messages/send-messages-batch-action.png)

   4. Agora, selecione seu aplicativo lógico "DestinatárioLote" que você criou anteriormente, e que agora aparece como uma ação.

      ![Selecione o aplicativo lógico "destinatário do lote"](./media/logic-apps-batch-process-send-receive-messages/send-batch-select-batch-receiver.png)

      > [!NOTE]
      > lista de saudação também mostra todos os outros aplicativos lógica que tenham um gatilho de lote.

3. Definir propriedades de lote de saudação.

   * **Nome do lote**: nome do lote Olá definido pelo aplicativo lógico receptor hello, que é "TestBatch" neste exemplo e é validado no tempo de execução.

     > [!IMPORTANT]
     > Certifique-se de que você não altere o nome do lote hello, que deve corresponder ao nome do lote Olá especificada pelo aplicativo de lógica de receptor de saudação.
     > Alterar o nome hello lote faz com que remetente Olá lógica toofail de aplicativo.

   * **Conteúdo da mensagem**: Olá conteúdo da mensagem que você deseja toosend. 
   Neste exemplo, adicione essa expressão que inserções Olá data e hora atuais em mensagem de saudação do conteúdo que você enviar lote toohello:

     1. Olá quando **conteúdo dinâmico** lista é exibida, escolha **expressão**. 
     2. Insira a expressão de saudação **utcnow()**e escolha **Okey**. 

        ![Em "Conteúdo da Mensagem", escolha "Expressão". Insira "utcnow()".](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details.png)

4. Agora, configure uma partição para o lote de saudação. No hello "BatchReceiver" ação, escolha **Mostrar opções avançadas**.

   * **Nome da partição**: um toouse de chave de partição exclusivo opcional para a divisão do lote de destino hello. Para este exemplo, adicione uma expressão que gera um número aleatório entre um e cinco.
   
     1. Olá quando **conteúdo dinâmico** lista é exibida, escolha **expressão**.
     2. Insira esta expressão: **rand(1,6)**

        ![Configurar uma partição para seu lote de destino](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-partition-advanced-options.png)

        Essa função **rand** gera um número entre um e cinco. 
        Portanto, você está dividindo esse lote em cinco partições numeradas, definidas dinamicamente por esta expressão.

   * **Id da Mensagem**: um identificador de mensagem opcional, e um GUID gerado quando estiver vazio. 
   Neste exemplo, deixe essa caixa em branco.

5. Salve seu aplicativo lógico. Seu aplicativo de lógica de remetente agora parece exemplo toothis semelhante:

   ![Salve seu aplicativo lógico remetente](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details-finished.png)

## <a name="test-your-logic-apps"></a>Testar seus aplicativos lógicos

tootest o envio em lote solução, deixe a seus aplicativos lógicos em execução por alguns minutos. Em breve, começar a receber emails em grupos de cinco, tudo com hello mesmo chave da partição.

Seu aplicativo de lógica de BatchSender é executado a cada minuto, gera um número aleatório entre um e cinco e usa esse número gerado como chave de partição de saudação de lote de destino Olá onde as mensagens são enviadas. Cada vez lote Olá tem cinco itens com hello mesma chave de partição, seu aplicativo de lógica de BatchReceiver é acionado e envia mensagens para cada mensagem.

> [!IMPORTANT]
> Quando você terminar de teste, certifique-se de que você desative Olá BatchSender lógica aplicativo toostop enviar mensagens e evitar a sobrecarga de sua caixa de entrada.

## <a name="next-steps"></a>Próximas etapas

* [Compilar definições de aplicativo lógico usando JSON](../logic-apps/logic-apps-author-definitions.md)
* [Compilar um aplicativo sem servidor no Visual Studio com o Aplicativo Lógico do Azure e o Functions](../logic-apps/logic-apps-serverless-get-started-vs.md)
* [Tratamento de exceção e registro em log de erros para aplicativos lógicos](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
