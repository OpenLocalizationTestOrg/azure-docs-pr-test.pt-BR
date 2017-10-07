---
title: "aaaOverview de métricas no Microsoft Azure | Microsoft Docs"
description: "Saiba como gráficos de monitoramento de toocustomize no Azure."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c36031eb-4df5-4cd5-9479-311d493a40d2
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: robb
ms.openlocfilehash: 4196b2e9bda713e9a0abc349eed78685abcaf194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-metrics-in-microsoft-azure"></a>Visão Geral das métricas no Microsoft Azure
Todos os serviços do Azure acompanham métricas-chave que permitem o uso de seus serviços, desempenho, disponibilidade e integridade de saudação toomonitor. Você pode exibir essas métricas em Olá portal do Azure, e você também pode usar o hello [API REST](https://msdn.microsoft.com/library/azure/dn931930.aspx) ou [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooaccess Olá conjunto completo de métricas de forma programática.

Para alguns serviços, talvez seja necessário tooturn diagnósticos em ordem toosee métricas. Para outras pessoas, como máquinas virtuais, você receberá um conjunto básico de métricas, mas precisa tooenable Olá conjunto completo de métricas de alta frequência. Consulte [habilitar o monitoramento e diagnóstico](insights-how-to-use-diagnostics.md) toolearn mais.

## <a name="using-monitoring-charts"></a>Usando gráficos de monitoramento
Você pode conter qualquer uma das métricas de saudação-los em qualquer período de tempo que você escolher.

1. Em Olá [Portal do Azure](https://portal.azure.com/), clique em **procurar**, e, em seguida, um recurso estiver interessado no monitoramento.
2. Olá **monitoramento** seção contém métricas mais importantes de saudação para cada recurso do Azure. Por exemplo, um aplicativo Web tem **Solicitações e erros**, enquanto que uma máquina virtual teria **Percentual de CPU** e **Leitura e gravação de disco**: ![Lente de monitoramento](./media/insights-how-to-customize-monitoring/Insights_MonitoringChart.png)
3. Clicar em qualquer gráfico mostrará a você Olá **métrica** folha. Na folha de hello, além disso toohello gráfico, é uma tabela que mostra as agregações de métricas de saudação (como média, mínima e máxima, pelo intervalo de tempo de saudação escolhido). Abaixo está Olá regras de alerta para o recurso de saudação.
    ![Folha Métrica](./media/insights-how-to-customize-monitoring/Insights_MetricBlade.png)
4. linhas de saudação toocustomize que aparecerem, clique em Olá **editar** botão gráfico hello, ou, Olá **Editar gráfico** comando na folha de métricas de saudação.
5. Na folha de editar consulta hello, você pode fazer três coisas:
   
   * Alterar o intervalo de tempo de saudação
   * Alternar a aparência de saudação entre barras e linha
   * Escolher métricas diferentes ![Editar consulta](./media/insights-how-to-customize-monitoring/Insights_EditQuery.png)
6. Alterar o intervalo de tempo de saudação é tão fácil quanto selecionar um intervalo diferente (como **última hora**) e clicando em **salvar** na parte inferior da saudação da folha de saudação. Você também pode escolher **personalizado**, que permite que você toochoose qualquer período de tempo sobre Olá últimas duas semanas. Por exemplo, você pode ver Olá duas semanas inteiras ou apenas 1 hora do dia anterior. Digite tooenter de caixa de texto de saudação outra hora.
    ![Intervalo de tempo personalizado](./media/insights-how-to-customize-monitoring/Insights_CustomTime.png)
7. Abaixo do intervalo de tempo de saudação canal você escolher qualquer número de tooshow de métricas no gráfico de saudação.
8. Quando você clica em Salvar, suas alterações serão salvas para esse recurso em particular. Por exemplo, se você tem duas máquinas virtuais, e você alterar um gráfico em um, ele não afetará Olá outros.

## <a name="creating-side-by-side-charts"></a>Criando gráficos lado a lado
Com a personalização avançada Olá no portal de saudação, você pode adicionar tantos gráficos quantos desejar.

1. Em Olá **...**  menu na parte superior de saudação do hello folha, clique em **adicionar blocos**:  
    ![Adicionar menu](./media/insights-how-to-customize-monitoring/Insights_AddMenu.png)
2. Em seguida, você pode selecionar selecionar um gráfico de saudação **galeria** Olá direita da tela: ![Galeria](./media/insights-how-to-customize-monitoring/Insights_Gallery.png)
3. Se você não vir a métrica de saudação desejado, você pode adicionar um dos sempre Olá predefinição métricas, e **editar** Olá métrica de saudação do gráfico tooshow que você precisa.

## <a name="monitoring-usage-quotas"></a>Monitorando cotas de uso
A maioria das métricas mostra tendências ao longo do tempo, mas determinados dados, como cotas de uso, são informações específicas com um limite.

Você também pode ver as cotas de uso na folha de saudação para recursos que têm cotas:

![Uso](./media/insights-how-to-customize-monitoring/Insights_UsageChart.png)

Como com métricas, você pode usar o hello [API REST](https://msdn.microsoft.com/library/azure/dn931963.aspx) ou [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooaccess Olá conjunto completo de cotas de uso por meio de programação.

## <a name="next-steps"></a>Próximas etapas
* [Receba notificações de alerta](insights-receive-alert-notifications.md) sempre que uma métrica cruzar um limite.
* [Habilitar o monitoramento e diagnóstico](insights-how-to-use-diagnostics.md) toocollect detalhadas métricas de alta frequência em seu serviço.
* [Dimensionar automaticamente a contagem de instância](insights-how-to-scale.md) toomake-se de que o serviço está disponível e respondendo.
* [Monitorar o desempenho do aplicativo](../application-insights/app-insights-azure-web-apps.md) se você quiser toounderstand exatamente como o código está sendo executado na nuvem hello.
* Use [Application Insights para páginas da web e aplicativos JavaScript](../application-insights/app-insights-web-track-usage.md) tooget análise de cliente sobre os navegadores Olá que visita uma página da web.
* [Monitore a disponibilidade e a capacidade de resposta de qualquer página da Web](../application-insights/app-insights-monitor-web-app-availability.md) com o Application Insights para que você possa descobrir se a página está inativa.

