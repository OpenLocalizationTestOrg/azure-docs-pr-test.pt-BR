---
title: "aaaAutomate Azure Application Insights processa usando lógica de aplicativos."
description: "Saiba como você pode rapidamente automatizar processos repetíveis adicionando Olá Application Insights conector tooyour lógica aplicativo."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: bwren
ms.openlocfilehash: 8565aadf0644ffb10da8a0964821901907db2e27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-application-insights-processes-by-using-logic-apps"></a>Automatize os processos do Application Insights usando os Aplicativos Lógicos

Você encontra-se repetidamente Olá mesmo consultas executadas em seu toocheck de dados de telemetria se o serviço está funcionando corretamente? É buscam tooautomate essas consultas para descobrir tendências e anomalias e, em seguida, criar seus próprios fluxos de trabalho contorná-las? Hello Azure aplicativo Insights connector (visualização) para aplicativos lógicos é a ferramenta certa Olá para essa finalidade.

Com essa integração, você pode automatizar diversos processos sem a necessidade de escrever nenhuma linha de código. Você pode criar um aplicativo lógico com hello Application Insights conector tooquickly automatizar qualquer processo Application Insights. 

Adicione também outras ações. recurso de aplicativos lógicos de saudação do serviço de aplicativo do Azure torna centenas de ações disponíveis. Por exemplo, usando um aplicativo lógico, você pode enviar automaticamente uma notificação por email ou criar um bug no Visual Studio Team Services. Você também pode usar uma saudação muitas disponível [modelos](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) toohelp acelerar o processo de saudação de criação de seu aplicativo lógico. 

## <a name="create-a-logic-app-for-application-insights"></a>Criar um aplicativo lógico para o Application Insights

Neste tutorial, você aprenderá como toocreate um aplicativo de lógica que usa Olá análise autocluster algoritmo toogroup atributos nos dados Olá para um aplicativo web. fluxo de saudação envia automaticamente resultados Olá por email, apenas um exemplo de como você pode usar análise de informações do aplicativo e os aplicativos lógicos juntos. 

### <a name="step-1-create-a-logic-app"></a>Etapa 1: criar um aplicativo lógico
1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Em Olá **novo** painel, selecione **Web + móvel**e, em seguida, selecione **aplicativo lógico**.

    ![Janela Novo aplicativo lógico](./media/automate-with-logic-apps/logicapp1.png)

### <a name="step-2-create-a-trigger-for-your-logic-app"></a>Etapa 2: criar um gatilho para seu aplicativo lógico
1. Em Olá **lógica de aplicativo Designer** janela, em **começar com um gatilho comuns**, selecione **recorrência**.

    ![Janela Designer de Aplicativo Lógico](./media/automate-with-logic-apps/logicapp2.png)

2. Em Olá **frequência** selecione **dia** e, em seguida, em Olá **intervalo** , digite **1**.

    ![Janela "Recorrência" do Designer de Aplicativo Lógico](./media/automate-with-logic-apps/step2b.png)

### <a name="step-3-add-an-application-insights-action"></a>Etapa 3: adicionar uma ação do Application Insights
1. Clique na caixa **Nova etapa** e depois clique em **Adicionar uma ação**.

2. Em Olá **escolher uma ação** caixa de pesquisa, digite **Azure Application Insights**.

3. Em **Ações**, clique em **Versão Prévia do Azure Application Insights – Visualizar consulta do Analytics**.

    ![Janela "Escolha uma ação" do Designer de Aplicativo Lógico](./media/automate-with-logic-apps/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a>Etapa 4: Conectar-se o recurso do Application Insights tooan

toocomplete nesta etapa, você precisa de uma ID de aplicativo e uma chave de API para o recurso. Você pode recuperá-las de saudação portal do Azure, conforme mostrado no diagrama a seguir de saudação:

![ID do aplicativo no portal do Azure de saudação](./media/automate-with-logic-apps/appid.png) 

Forneça um nome para a conexão, a ID do aplicativo hello e a chave de API do hello.

![Janela Conexão de fluxo do Designer de Aplicativo Lógico](./media/automate-with-logic-apps/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a>Etapa 5: Especificar hello consulta de análise e o tipo de gráfico
Em Olá exemplo a seguir, consulta Olá seleciona solicitações Olá falhado no último dia do hello e correlaciona-los com exceções que ocorreram como parte da operação de saudação. Análise de correlaciona solicitações Olá falhou, com base no identificador de operation_Id hello. consulta de saudação segmentos, em seguida, resultados hello usando algoritmo de autocluster hello. 

Quando você cria suas próprias consultas, verifique se estão funcionando corretamente na análise antes de adicioná-lo tooyour fluxo.

1. Em Olá **consulta** caixa, adicione Olá consulta de análise a seguir: 

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

2. Em Olá **tipo de gráfico** selecione **tabela Html**.

    ![Janela de configuração de consulta do Analytics](./media/automate-with-logic-apps/flow4.png)

### <a name="step-6-configure-hello-logic-app-toosend-email"></a>Etapa 6: Configurar o email de toosend de aplicativo hello lógica

1. Clique em **Nova etapa** e, depois, selecione **Adicionar uma ação**.

2. Na caixa de pesquisa hello, digite **Outlook do Office 365**.

3. Clique em **Office 365 Outlook – Enviar um email**.

    ![Seleção do Office 365 Outlook](./media/automate-with-logic-apps/flow2b.png)

4. Em Olá **enviar um email** janela, Olá a seguir:

   a. Digite o endereço de email de saudação do destinatário hello.

   b. Digite o assunto do email de saudação.

   c. Clique em qualquer lugar Olá **corpo** caixa e, em seguida, em Olá conteúdo menu dinâmico que é aberto no hello direito, selecione **corpo**.

   d. Clique em **Mostrar opções avançadas**.

      ![Configuração do Office 365 Outlook](./media/automate-with-logic-apps/flow5.png)

5. No menu de conteúdo dinâmico Olá, Olá a seguir:

    a. Selecione o **Nome do Anexo**.

    b. Selecione o **Conteúdo do Anexo**.
    
    c. Em Olá **é HTML** selecione **Sim**.

      ![Tela de configuração de email do Office 365](./media/automate-with-logic-apps/flow7.png)

### <a name="step-7-save-and-test-your-logic-app"></a>Etapa 7: salvar e testar o aplicativo lógico
* Clique em **salvar** toosave suas alterações.

Você pode aguardar Olá gatilho toorun Olá lógica aplicativo ou você pode executar o aplicativo de lógica de saudação imediatamente selecionando **executar**.

![Tela de criação do aplicativo lógico](./media/automate-with-logic-apps/step7.png)

Quando sua lógica de aplicativo é executado, destinatários Olá especificado na lista de email Olá receberá um email que se parece com o seguinte hello:

![Mensagem de email do aplicativo lógico](./media/automate-with-logic-apps/flow9.png)

## <a name="next-steps"></a>Próximas etapas

- Saiba mais sobre a criação de [Consultas do Analytics](app-insights-analytics-using.md).
- Saiba mais sobre o [Aplicativos Lógicos](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).



<!--Link references-->





