---
title: "aaaAutomate processos de análise de logs do Azure com Microsoft Flow"
description: "Saiba como você pode usar o Microsoft Flow tooquickly automatizar processos repetíveis usando o conector do Azure Log Analytics hello."
services: log-analytics
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: log-analytics
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: bwren
ms.openlocfilehash: 52026df968682842cc9f8d55f6f9875c5f9c10b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-log-analytics-processes-with-hello-connector-for-microsoft-flow"></a>Automatizar processos de análise de Log com conector Olá para o Microsoft Flow
[Microsoft Flow](https://ms.flow.microsoft.com) permite que os fluxos de trabalho toocreate automatizada usando centenas de ações para uma variedade de serviços. Saída de uma ação pode ser usada como entrada tooanother, permitindo que você toocreate integração entre serviços diferentes.  conector do Azure Log Analytics Olá para o Microsoft Flow permitir toobuild fluxos de trabalho que incluem dados recuperados pelas pesquisas de log na análise de Log.

Por exemplo, você pode usar dados de análise de logs do Microsoft Flow toouse em uma notificação por email do Office 365, criar um bug no Visual Studio Team Services ou postar uma mensagem de margem de atraso.  Você pode disparar um fluxo de trabalho com um agendamento simples ou a partir de alguma ação em um serviço conectado, por exemplo, quando um email ou tweet é recebido.  


> [!NOTE]
> conector do Azure Log Analytics Olá para o Microsoft Flow requer seu espaço de trabalho toobe atualizado toohello nova análise de Log linguagem de consulta. Você pode saber mais sobre a nova linguagem de saudação e obter Olá procedimento tooupgrade seu espaço de trabalho em [atualizar sua pesquisa de log de toonew de espaço de trabalho do Azure Log Analytics](log-analytics-log-search-upgrade.md).  

tutorial de saudação neste artigo mostra como toocreate um fluxo que envia automaticamente Olá resultados de uma pesquisa de log de análise de Log por email, apenas um exemplo de como você pode usar a análise de Log no Microsoft Flow. 


## <a name="step-1-create-a-flow"></a>Etapa 1: Criar um fluxo
1. Entrar muito[Microsoft Flow](http://flow.microsoft.com)e selecione **flui meu**.
2. Clique em **+ Criar em branco**.

## <a name="step-2-create-a-trigger-for-your-flow"></a>Etapa 2: Criar um gatilho para o fluxo
1. Clique em **Pesquisar centenas de conectores e gatilhos**.
2. Tipo **agenda** na caixa de pesquisa de saudação.
3. Selecione **Agendamento** e, depois, **Agendamento – Recorrência**.
4. Em Olá **frequência** marque **dia** e em Olá **intervalo** , digite **1**.<br><br>![Caixa de diálogo de gatilho do Microsoft Flow](media/log-analytics-flow-tutorial/flow01.png)


## <a name="step-3-add-a-log-analytics-action"></a>Etapa 3: Adicionar uma ação do Log Analytics
1. Clique em **+ Nova etapa** e depois clique em **Adicionar uma ação**.
2. Pesquise por **Log Analytics**.
3. Clique em **Azure Log Analytics – Executar a consulta e visualizar os resultados**.<br><br>![Janela Executar consulta do Log Analytics](media/log-analytics-flow-tutorial/flow02.png)

## <a name="step-4-configure-hello-log-analytics-action"></a>Etapa 4: Configurar a ação de análise de Log Olá

1. Especifique os detalhes de saudação de seu espaço de trabalho incluindo Olá assinatura ID, grupo de recursos e o nome do espaço de trabalho.
2. Adicionar Olá toohello de consulta de análise de Log a seguir **consulta** janela.  Isso é apenas um exemplo de consulta, e você pode substituir por qualquer outra que retorne dados.
```
    Event
    | where EventLevelName == "Error" 
    | where TimeGenerated > ago(1day)
    | summarize count() by Computer
    | sort by Computerindow. 
```

2. Selecione **tabela HTML** para Olá **tipo de gráfico**.<br><br>![Ação do Log Analytics](media/log-analytics-flow-tutorial/flow03.png)

## <a name="step-5-configure-hello-flow-toosend-email"></a>Etapa 5: Configurar o email de toosend fluxo Olá

1. Clique em **Nova etapa** e depois clique em **+ Adicionar uma ação**.
2. Pesquise por **Office 365 Outlook**.
3. Clique em **Office 365 Outlook – Enviar um email**.<br><br>![Janela de seleção do Office 365 Outlook](media/log-analytics-flow-tutorial/flow04.png)

4. Especifique o endereço de email de saudação de um destinatário no hello **para** janela e o assunto do email de saudação em **assunto**.
5. Clique em qualquer lugar Olá **corpo** caixa.  Uma janela de **Conteúdo dinâmico** é aberta com valores de ações anteriores.  
6. Selecione **Corpo**.  Isso é resultados de saudação da consulta Olá Olá ação de análise de Log.
6. Clique em **Mostrar opções avançadas**.
7. Em Olá **é HTML** selecione **Sim**.<br><br>![Janela de configuração de email do Office 365](media/log-analytics-flow-tutorial/flow05.png)

## <a name="step-6-save-and-test-your-flow"></a>Etapa 6: Salvar e testar o fluxo
1. Em Olá **nome do fluxo de** caixa, adicione um nome para o fluxo e, em seguida, clique em **criar fluxo**.<br><br>![Salvar o fluxo](media/log-analytics-flow-tutorial/flow06.png)
2. fluxo de saudação é criado e será executado após um dia que é Olá agendamento especificado. 
3. tooimmediately teste Olá fluxo, clique em **executar agora** e **executar fluxo**.<br><br>![Executar fluxo](media/log-analytics-flow-tutorial/flow07.png)
3. Quando o fluxo de saudação for concluída, verifique mensagens de saudação do destinatário Olá que você especificou.  Você deve ter recebido um email com um corpo semelhante toohello a seguir:<br><br>![Email de exemplo](media/log-analytics-flow-tutorial/flow08.png)


## <a name="next-steps"></a>Próximas etapas

- Saiba mais sobre o [Pesquisas de log no Log Analytics](log-analytics-log-search-new.md).
- Saiba mais sobre o [Microsoft Flow](https://ms.flow.microsoft.com).



