---
title: "Contagem de instâncias aaaScale manualmente ou com o dimensionamento automático com o Portal do Azure | Microsoft Docs"
description: "Saiba como tooscale seus serviços do Azure."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 2397596a-071f-4d49-8893-bec5f735bd7b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: ancav
ms.openlocfilehash: 8cb78f18416bd3caecce52702a8d630aa434d776
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-instance-count-manually-or-automatically"></a>Dimensionar a contagem de instância manualmente ou automaticamente
Em Olá [Portal do Azure](https://portal.azure.com/), você pode definir manualmente a contagem de instâncias de saudação do seu serviço ou, você pode definir parâmetros toohave dimensionar automaticamente com base na demanda. Isso é geralmente chamado tooas *expansão* ou *ampliar*.

Antes de dimensionamento com base na contagem de instância, você deve considerar que o dimensionamento é afetado pelos **preço** na contagem de tooinstance de adição. Diferentes camadas de preços podem ter diferentes números núcleos e memória, e assim, eles terão melhor desempenho para hello mesmo número de instâncias (que é *expandir* ou *reduzir*). Este artigo aborda especificamente a *redução horizontal* e a *escala horizontal*.

Você pode dimensionar no portal de Olá, e você também pode usar o hello [API REST](https://msdn.microsoft.com/library/azure/dn931953.aspx) ou [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooadjust dimensionar automaticamente ou manualmente.

> [!NOTE]
> Este artigo descreve como toocreate uma configuração no portal de saudação em de dimensionamento automático [http://portal.azure.com](http://portal.azure.com). Configurações de AutoEscala criadas nesse portal não podem ser editada portal clássico do hello ([http://manage.windowsazure.com](http://manage.windowsazure.com)).
> 
> 

## <a name="scaling-manually"></a>Dimensionando manualmente
1. Em Olá [Portal do Azure](https://portal.azure.com/), clique em **procurar**, navegue toohello recursos você deseja tooscale, como um **plano de serviço de aplicativo**.
2. Clique em **Configurações > Escalar horizontalmente (Plano do Serviço de Aplicativo).**
3. Na parte superior de saudação do hello **escala** folha que você pode ver um histórico das ações de dimensionamento automático do serviço de saudação.
   
    ![Lâmina Escala](./media/insights-how-to-scale/Insights_ScaleBladeDayZero.png)
   
   > [!NOTE]
   > Apenas as ações executadas pelo dimensionamento automático aparecerão neste gráfico. Se você ajustar a contagem de instâncias Olá manualmente, Olá alteração não será refletida no gráfico.
   > 
   > 
4. Você pode ajustar manualmente o número de saudação **instâncias** com o controle deslizante.
5. Clique em Olá **salvar** comando e você será dimensionado toothat número de instâncias de quase imediatamente.

## <a name="scaling-based-on-a-pre-set-metric"></a>Dimensionamento com base em uma métrica predefinida
Se você quiser Olá número de instâncias tooautomatically ajustar com base em uma métrica, selecione Olá métrica desejada na Olá **o dimensionamento por** lista suspensa. Por exemplo, para um **plano do Serviço de Aplicativo**, você pode dimensionar de acordo com a **porcentagem de CPU**.

1. Quando você seleciona uma métrica você obterá um controle deslizante, e/ou, número de saudação de tooenter de caixas de texto de instâncias que você deseja tooscale entre:
   
    ![Lâmina Escala com a porcentagem de CPU](./media/insights-how-to-scale/Insights_ScaleBladeCPU.png)
   
    Dimensionamento automático nunca terão seu serviço abaixo ou acima limites Olá definidas, independentemente de sua carga.
2. Em segundo lugar, você pode escolher intervalo-alvo de métrica Olá Olá. Por exemplo, se você escolheu **percentual de CPU**, você pode definir um destino para Olá média de CPU em todas as instâncias de saudação em seu serviço. Uma expansão ocorrerá quando Olá média de CPU excede o máximo de saudação que você definir, da mesma forma, uma escala no ocorrerá sempre que Olá média de CPU cai abaixo Olá mínimo.
3. Clique em Olá **salvar** comando. Dimensionamento automático verificará cada alguns toomake minutos se você está no intervalo de instância hello e de destino para a métrica. Quando o serviço receber tráfego adicional, você obterá mais instâncias sem fazer nada.

## <a name="scale-based-on-other-metrics"></a>Dimensionamento com base em outras métricas
Você pode dimensionar com base nas métricas diferente de predefinições de saudação que aparecem no hello **o dimensionamento por** suspenso e ainda pode ter um conjunto complexo de expansão e dimensionar nas regras.

### <a name="adding-or-changing-a-rule"></a>Adicionar ou alterar uma regra
1. Escolha Olá **regras de agendamento e desempenho** em Olá **o dimensionamento por** suspenso: ![regras de desempenho](./media/insights-how-to-scale/Insights_PerformanceRules.png)
2. Se você já tinha o dimensionamento automático, você verá uma exibição de regras de saudação exato que você tinha no.
3. tooscale com base em outro Olá de métrica clique **Adicionar regra** linha. Você também pode clicar em um de saudação toochange de linhas existentes da métrica de saudação você tinha anteriormente métrica toohello deseja tooscale por.
   ![Add rule](./media/insights-how-to-scale/Insights_AddRule.png)
4. Agora, é necessário tooselect qual métrica que você deseja tooscale por. Quando escolher uma métrica existe tooconsider de duas coisas:
   
   * Olá *recurso* métrica hello proveniente. Normalmente, isso será ser Olá mesmo que o recurso de saudação dimensionará. No entanto, se você desejar tooscale por profundidade de saudação de uma fila de armazenamento, o recurso de saudação é fila Olá que você deseja tooscale por.
   * Olá *nome da métrica* em si.
   * Olá *tempo agregação* da métrica de saudação. Isso é como dados de saudação são combinar sobre Olá *duração*.
5. Depois de escolher sua métrica você escolher limite Olá Olá métrica e operador hello. Por exemplo, você poderia dizer **Maior que** **80%**.
6. Escolha Olá ação que você deseja tootake. Há alguns tipos de ações diferentes:
   
   * Aumenta ou diminui - isso adicionará ou removerá Olá **valor** número de instâncias que você definir
   * Aumentar ou diminuir a porcentagem - isso alterará a contagem de instâncias de saudação por uma porcentagem. Por exemplo, você pode colocar 25 no hello **valor** campo, e se você tiver atualmente 8 instâncias, 2 deve ser adicionado.
   * Aumentar ou diminuir muito - isso definirá Olá instância contagem toohello **valor** você definir.
7. Por fim, você pode escolher de resfriamento - quanto tempo essa regra deve esperar após Olá anterior escala ação tooscale novamente.
8. Depois de configurar a regra, pressione **OK**.
9. Depois de configurar todas as regras de saudação desejado de, ser Olá-se de toohit **salvar** comando.

### <a name="scaling-with-multiple-steps"></a>Dimensionamento com várias etapas
exemplos de saudação acima são muito básicos. No entanto, se você quiser toobe mais agressiva sobre dimensionamento para cima (ou para baixo), você pode até mesmo adicionar escala várias regras para Olá mesmo métrica. Por exemplo, você pode definir duas regras de dimensionamento de acordo com um percentual de CPU:

1. Escalar horizontalmente em uma instância se o percentual de CPU estiver acima de 60%
2. Escalar horizontalmente em três instâncias se o percentual de CPU estiver acima de 85%

![Várias regras de escala](./media/insights-how-to-scale/Insights_MultipleScaleRules.png)

Com essa regra adicional, se sua carga exceder 85% antes de uma ação de escala, você terá duas instâncias adicionais em vez de uma.

## <a name="scale-based-on-a-schedule"></a>Dimensionamento com base em um planejamento
Por padrão, quando você criar uma regra de dimensionamento, ela será sempre aplicada. Você pode ver que, quando você clicar no cabeçalho de perfil hello:

![Perfil](./media/insights-how-to-scale/Insights_Profile.png)

No entanto, talvez você queira toohave mais agressiva dimensionamento durante a saudação dia ou semana hello, que nos finais de semana de saudação. Você pode até mesmo desligar o serviço totalmente fora do horário de trabalho.

1. toodo isso, no perfil Olá tiver, selecione **recorrência** em vez de **sempre,** e escolha Olá o tempo que você deseja Olá tooapply de perfil.
2. Toohave por exemplo, um perfil que é aplicada durante a semana hello, Olá **dias** suspensa desmarque **sábado** e **domingo**.
3. toohave um perfil que se aplica durante Olá Olá comercial, defina **hora de início** toohello hora do dia em que você deseja toostart no.
   
    ![Recorrência padrão](./media/insights-how-to-scale/Insights_ProfileRecurrence.png)
4. Clique em **OK**.
5. Em seguida, você precisará de perfil de saudação tooadd que você deseja tooapply em outros momentos. Clique em Olá **adicionar perfil** linha.
    ![Dia livre](./media/insights-how-to-scale/Insights_ProfileOffWork.png)
6. Nomeie o segundo novo perfil. Por exemplo, você poderia chamá-lo de **Dias livres**.
7. Em seguida, selecione **recorrência** novamente e escolha o intervalo de contagem de instância Olá deseja durante esse tempo.
8. Como com hello perfil padrão, escolha Olá **dias** deseja tooapply esse perfil para e hello **hora de início** durante o dia de saudação.
   
   > [!NOTE]
   > Dimensionamento automático usará as regras de horário de verão economia Olá para aquele que **fuso horário** você selecionar. No entanto, durante o horário de verão deslocamento UTC do hello mostrará o deslocamento de fuso horário base hello, não Olá verão economia UTC deslocamento.
   > 
   > 
9. Clique em **OK**.
10. Agora, você precisará tooadd qualquer regras que você deseja tooapply durante seu perfil de segundo. Clique em **Adicionar regra**, e, em seguida, você pode construir Olá mesma regra durante o perfil de padrão de saudação.
    
    ![Adicionar regra toooff](./media/insights-how-to-scale/Insights_RuleOffWork.png)
11. Ser toocreate-se de que ambos os uma regra de expansão e dimensionamento em, ou se encontram durante a saudação contagem de instâncias de saudação do perfil será apenas crescimento (ou diminuir).
12. Por fim, clique em **Salvar**.

## <a name="next-steps"></a>Próximas etapas
* [Monitorar as métricas de serviço](insights-how-to-customize-monitoring.md) toomake-se de que o serviço está disponível e respondendo.
* [Habilitar o monitoramento e diagnóstico](insights-how-to-use-diagnostics.md) toocollect detalhadas métricas de alta frequência em seu serviço.
* [Receba notificações de alerta](insights-receive-alert-notifications.md) sempre que ocorrerem eventos operacionais ou métricas ultrapassarem um limite.
* [Monitorar o desempenho do aplicativo](../application-insights/app-insights-azure-web-apps.md) se você quiser toounderstand exatamente como o código está sendo executado na nuvem hello.
* [Exibir eventos e log de atividades](insights-debugging-with-events.md) toolearn tudo o que aconteceu em seu serviço.
* [Monitore a disponibilidade e a capacidade de resposta de qualquer página da Web](../application-insights/app-insights-monitor-web-app-availability.md) com o Application Insights para que você possa descobrir se a página está inativa.

