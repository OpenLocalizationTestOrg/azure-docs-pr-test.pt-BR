---
title: processa a Azure Application Insights aaaAutomate Microsoft Flow
description: "Saiba como você pode usar o Microsoft Flow tooquickly automatizar processos repetíveis usando o conector do Application Insights hello."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/25/2017
ms.author: bwren
ms.openlocfilehash: b34488a6b8b8b0a6add960a67f1426cbbbc13552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-azure-application-insights-processes-with-hello-connector-for-microsoft-flow"></a>Automatizar processos de informações de aplicativo do Azure com conector Olá para o Microsoft Flow

Você encontra-se repetidamente Olá mesmo consultas executadas em seu toocheck de dados de telemetria que o serviço está funcionando corretamente? É buscam tooautomate essas consultas para descobrir tendências e anomalias e, em seguida, criar seus próprios fluxos de trabalho contorná-las? Hello Azure Application Insights connector (visualização) para Microsoft Flow é a ferramenta certa Olá para esses fins.

Com essa integração, você agora pode automatizar diversos processos sem a necessidade de escrever nenhuma linha de código. Depois de criar um fluxo usando uma ação do Application Insights, o fluxo de saudação executa automaticamente a consulta de análise de informações do aplicativo. 

Adicione também outras ações. O Microsoft Flow disponibiliza centenas de ações. Por exemplo, você pode usar Microsoft Flow tooautomatically enviar uma notificação por email ou criar um bug no Visual Studio Team Services. Você também pode usar uma saudação muitas [modelos](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) que estão disponíveis para o conector Olá para o Microsoft Flow. Esses modelos acelerar o processo de saudação de criação de um fluxo. 

<!--hello Application Insights connector also works with [Azure Power Apps](https://powerapps.microsoft.com/en-us/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/?v=17.23h). --> 

## <a name="create-a-flow-for-application-insights"></a>Criar um fluxo para o Application Insights

Neste tutorial, você aprenderá como toocreate um fluxo que usa Olá análise automática cluster algoritmo toogroup atributos nos dados Olá para um aplicativo web. fluxo de saudação envia automaticamente resultados Olá por email, apenas um exemplo de como você pode usar Microsoft Flow e análises do aplicativo Insights juntos. 

### <a name="step-1-create-a-flow"></a>Etapa 1: Criar um fluxo
1. Entrar muito[Microsoft Flow](http://flow.microsoft.com)e, em seguida, selecione **flui meu**.
2. Clique em **Criar um fluxo em branco**.

### <a name="step-2-create-a-trigger-for-your-flow"></a>Etapa 2: Criar um gatilho para o fluxo
1. Selecione **Agendamento** e, depois, **Agendamento – Recorrência**.
2. Em hello **frequência** selecione **dia**e em Olá **intervalo** , digite **1**.

    ![Caixa de diálogo de gatilho do Microsoft Flow](./media/app-insights-automate-with-flow/flow1.png)


### <a name="step-3-add-an-application-insights-action"></a>Etapa 3: adicionar uma ação do Application Insights
1. Clique na caixa **Nova etapa** e depois clique em **Adicionar uma ação**.
2. Pesquise por **Azure Application Insights**.
3. Clique em **Versão Prévia do Azure Application Insights – Visualizar a versão prévia da consulta do Analytics**.

    ![Janela Executar consulta do Analytics](./media/app-insights-automate-with-flow/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a>Etapa 4: Conectar-se o recurso do Application Insights tooan

toocomplete nesta etapa, você precisa de uma ID de aplicativo e uma chave de API para o recurso. Você pode recuperá-las de saudação portal do Azure, conforme mostrado no diagrama a seguir de saudação:

![ID do aplicativo no portal do Azure de saudação](./media/app-insights-automate-with-flow/appid.png) 

- Forneça um nome para a conexão, juntamente com a chave de API e a ID do aplicativo hello.

    ![Janela de conexão do Microsoft Flow](./media/app-insights-automate-with-flow/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a>Etapa 5: Especificar hello consulta de análise e o tipo de gráfico
Este exemplo de consulta seleciona solicitações Olá falhado no último dia do hello e correlaciona-los com exceções que ocorreram como parte da operação de saudação. Análise de correlaciona-las com base no identificador de operation_Id hello. consulta de saudação segmentos, em seguida, resultados hello usando algoritmo de autocluster hello. 

Quando você cria suas próprias consultas, verifique se estão funcionando corretamente na análise antes de adicioná-lo tooyour fluxo.

- Adicionar Olá após a consulta de análise e, em seguida, selecione o tipo de gráfico de tabela HTML de saudação. 

    ```
    requests
    | where timestamp > ago(1d)
    | where success == "False"
    | project name, operation_Id
    | join ( exceptions
        | project problemId, outerMessage, operation_Id
    ) on operation_Id
    | evaluate autocluster()
    ```
    
    ![Janela de configuração de consulta do Analytics](./media/app-insights-automate-with-flow/flow4.png)

### <a name="step-6-configure-hello-flow-toosend-email"></a>Etapa 6: Configurar o email de toosend fluxo Olá

1. Clique na caixa **Nova etapa** e depois clique em **Adicionar uma ação**.
2. Pesquise por **Office 365 Outlook**.
3. Clique em **Office 365 Outlook – Enviar um email**.

    ![Janela de seleção do Office 365 Outlook](./media/app-insights-automate-with-flow/flow2b.png)

4. Em Olá **enviar um email** janela, Olá a seguir:

   a. Digite o endereço de email de saudação do destinatário hello.

   b. Digite o assunto do email de saudação.

   c. Clique em qualquer lugar Olá **corpo** caixa e, em seguida, em Olá conteúdo menu dinâmico que é aberto no hello direito, selecione **corpo**.

   d. Clique em **Mostrar opções avançadas**.

    ![Configuração do Office 365 Outlook](./media/app-insights-automate-with-flow/flow5.png)

5. No menu de conteúdo dinâmico Olá, Olá a seguir:

    a. Selecione o **Nome do Anexo**.

    b. Selecione o **Conteúdo do Anexo**.
    
    c. Em Olá **é HTML** selecione **Sim**.

    ![Janela de configuração de email do Office 365](./media/app-insights-automate-with-flow/flow7.png)

### <a name="step-7-save-and-test-your-flow"></a>Etapa 7: Salvar e testar o fluxo
- Em Olá **nome do fluxo de** caixa, adicione um nome para o fluxo e, em seguida, clique em **criar fluxo**.

    ![Janela de criação de fluxo](./media/app-insights-automate-with-flow/flow8.png)

Você pode aguardar Olá gatilho toorun essa ação ou você pode executar o fluxo de saudação imediatamente por [execução do gatilho Olá sob demanda](https://flow.microsoft.com/blog/run-now-and-six-more-services/).

Quando o fluxo de saudação é executado, destinatários de saudação especificado na lista de email Olá receber uma mensagem de email que se parece com o seguinte hello:

![Email de exemplo](./media/app-insights-automate-with-flow/flow9.png)


## <a name="next-steps"></a>Próximas etapas

- Saiba mais sobre como criar [consultas do Analytics](app-insights-analytics-using.md).
- Saiba mais sobre o [Microsoft Flow](https://ms.flow.microsoft.com).



<!--Link references-->





