---
title: Alertas de aaaSet no Azure Application Insights | Microsoft Docs
description: "Seja notificado sobre os tempos de resposta lentos, as exceções e outras alterações de desempenho ou de uso em seu aplicativo Web."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: f8ebde72-f819-4ba5-afa2-31dbd49509a5
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: e160cb173e68fda2e6d97f29da342c46b7ac4f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-alerts-in-application-insights"></a>Definir alertas no Application Insights
[Informações de aplicativo do Azure] [ start] pode alertá-lo toochanges em métricas de desempenho ou de uso em seu aplicativo web. 

Application Insights monitora seu aplicativo em tempo real em um [ampla variedade de plataformas] [ platforms] toohelp diagnosticar problemas de desempenho e entender os padrões de uso.

Há três tipos de alerta:

* Os **alertas de métrica** informam quando uma métrica ultrapassa um valor limite durante determinado período – como tempos de resposta, contagens de exceção, uso da CPU ou exibições de página. 
* [**Testes na Web** ] [ availability] informam quando seu site não está disponível no hello internet ou respondendo lentamente. [Saiba mais][availability].
* [**O diagnóstico proativo** ](app-insights-proactive-diagnostics.md) são configurados automaticamente toonotify sobre padrões de desempenho incomuns.

Vamos nos concentrar nos alertas de métricas deste artigo.

## <a name="set-a-metric-alert"></a>Definir um alerta de Métrica
Folha de regras de alerta Olá aberto e, em seguida, use Olá adicionar botão. 

![Na folha de regras de alerta hello, escolha Adicionar alerta. Configure seu aplicativo como Olá toomeasure de recursos, forneça um nome para o alerta hello e escolha uma métrica.](./media/app-insights-alerts/01-set-metric.png)

* Defina outras propriedades do recurso de saudação antes de saudação. **Escolha o recurso hello "(componentes)"** se você quiser tooset alertas em métricas de desempenho ou de uso.
* nome de saudação que você forneça toohello alerta deve ser exclusivo dentro do grupo de recursos de saudação (não apenas o aplicativo).
* Ser unidades de saudação toonote cuidado em que você for questionado tooenter valor de limite de saudação.
* Se você marcar a caixa de Olá "... para proprietários de Email", os alertas são enviados por tooeveryone de email que possui o grupo de recursos de toothis de acesso. tooexpand esse conjunto de pessoas, adicioná-las toohello [grupo de recursos ou assinatura](app-insights-resources-roles-access-control.md) (não Olá recursos).
* Se você especificar "Emails adicionais", os alertas são enviados toothose indivíduos ou grupos (se você tiver marcado a caixa de "email proprietários …" de saudação). 
* Definir um [webhook endereço](../monitoring-and-diagnostics/insights-webhooks-alerts.md) se você tiver configurado um aplicativo web que responde tooalerts. Ele é chamado quando Olá alerta for ativado e quando ele está resolvido. (Mas observe que, no momento, os parâmetros de consulta não são passados como propriedades de webhook)
* Você pode desabilitar ou habilitar Olá alerta: consulte Olá botões na parte superior de saudação da folha de saudação.

*Não vejo o botão de alerta de adicionar hello.* 

* Você está usando uma conta organizacional? Você pode definir alertas, se você tiver o recurso de aplicativo de toothis acesso proprietário ou colaborador. Dê uma olhada na folha de controle de acesso de saudação. [Saiba mais sobre o controle de acesso][roles].

> [!NOTE]
> Na folha de alertas hello, verá que já existe um conjunto de alerta para cima: [diagnóstico proativo](app-insights-proactive-failure-diagnostics.md). alerta automática Olá monitora uma determinada métrica, taxa de falhas. A menos que você decida alerta pró-ativo do toodisable hello, você não precisa tooset seu próprio alerta na taxa de falha de solicitação. 
> 
> 

## <a name="see-your-alerts"></a>Ver seus alertas
Você recebe um email quando o estado de um alerta é mudado de inativo para ativo. 

estado atual de saudação de cada alerta é mostrado na folha de regras de alerta de saudação.

Há um resumo da atividade recente em alertas Olá suspensa:

![Lista suspensa Alertas](./media/app-insights-alerts/010-alert-drop.png)

histórico de saudação de alterações de estado está em Olá Log de atividades:

![Na folha de visão geral de saudação, clique em configurações, logs de auditoria](./media/app-insights-alerts/09-alerts.png)

## <a name="how-alerts-work"></a>Como funcionam os alertas
* Um alerta tem três estados: “Nunca ativado”, “Ativado” e “Resolvido”. Ativada significa Olá condição especificada foi true, quando foi avaliado pela última vez.
* Uma notificação é gerada quando um alerta muda de estado. (Se condição de alerta Olá já foi true quando você criou o alerta hello, poderá não receber uma notificação até que a condição de saudação vai false.)
* Cada notificação gera um email, se você marcou Olá emails caixa fornecidos ou endereços de email. Você também pode examinar Olá notificações caixa suspensa.
* Um alerta é avaliado toda vez que uma métrica chega, mas não o contrário.
* avaliação Olá agrega métrica Olá sobre Olá que precedem o período e, em seguida, compara toohello limite toodetermine Olá novo estado.
* período Olá que você escolher Especifica o intervalo de saudação sobre quais métricas são agregadas. Isso não afetará a frequência hello alerta é avaliado: depende da frequência de saudação da chegada de métricas.
* Se nenhum dado chega para uma métrica específica por algum tempo, intervalo de saudação tem efeitos diferentes na avaliação de alerta e em gráficos de saudação no Gerenciador de métrica. Gerenciador de métrica, se nenhum dado é visto por mais de um intervalo de amostragem do gráfico Olá Olá gráfico mostra um valor de 0. Mas um alerta com base em Olá mesma métrica não é reavaliada e Olá permanece de estado do alerta inalterado. 
  
    Quando os dados chegam eventualmente, gráfico de saudação salta valor do retorno tooa diferente de zero. alerta de saudação é avaliada com base nos dados de saudação disponíveis para Olá período especificado. Se novo ponto de dados Olá Olá apenas um disponível no período de Olá Olá agregação é baseado apenas em ponto de dados.
* Um alerta pode piscar frequentemente entre os estados de alerta e íntegro, mesmo que você defina um longo período. Isso pode acontecer se o valor de métrica Olá passar em torno do limite de saudação. Não há nenhum Histerese no limite de saudação: Olá transição tooalert ocorre no Olá Olá transição toohealthy mesmo valor.

## <a name="what-are-good-alerts-tooset"></a>O que são bons alertas tooset?
Depende de seu aplicativo. toostart, ele tem melhor não tooset muitos métricas. Dedique algum tempo Examinando os gráficos de métricas enquanto seu aplicativo estiver em execução, tooget uma ideia de como ele se comporta normalmente. Essa prática ajuda a localizar maneiras tooimprove seu desempenho. Configure alertas tootell você quando métricas Olá saem da zona de saudação normal. 

Alguns alertas populares são:

* [Métricas de navegador][client], especificamente, **tempos de carregamento de página** do navegador, são adequados para aplicativos Web. Se a página tem muitos scripts, você deve procurar **exceções de navegador**. Em ordem tooget essas métricas e alertas, você ter tooset até [página da web de monitoramento][client].
* **Tempo de resposta do servidor** para o lado do servidor de saudação de aplicativos da web. Bem como configurar alertas, fique atento esta métrica toosee se desproporcionalmente varia com taxas de solicitação alto: variação pode indicar que seu aplicativo está ficando sem recursos. 
* **Exceções de servidor** -toosee-los, você tem toodo alguns [configuração adicional](app-insights-asp-net-exceptions.md).

Não se esqueça de que [diagnóstico de taxa de falha pró-ativo](app-insights-proactive-failure-diagnostics.md) automaticamente Olá taxa de monitor em que seu aplicativo responde toorequests com códigos de falha. 

## <a name="automation"></a>Automação
* [Use o PowerShell tooautomate configurar alertas](app-insights-powershell-alerts.md)
* [Use webhooks tooautomate resposta tooalerts](../monitoring-and-diagnostics/insights-webhooks-alerts.md)

## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="see-also"></a>Consulte também
* [Testes de disponibilidade na Web](app-insights-monitor-web-app-availability.md)
* [Automatizar a configuração de alertas](app-insights-powershell-alerts.md)
* [Diagnóstico proativo](app-insights-proactive-diagnostics.md) 

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[platforms]: app-insights-platforms.md
[roles]: app-insights-resources-roles-access-control.md
[start]: app-insights-overview.md

