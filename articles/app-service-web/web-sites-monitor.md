---
title: "aaaMonitor aplicativos no serviço de aplicativo do Azure | Microsoft Docs"
description: "Saiba como toomonitor aplicativos no serviço de aplicativo do Azure usando Olá Portal do Azure."
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: d273da4e-07de-48e0-b99d-4020d84a425e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/07/2016
ms.author: byvinyal
ms.openlocfilehash: 80d5a466102a894a49d04ae35aa54cc1d05a58df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-monitor-apps-in-azure-app-service"></a>Como monitorar aplicativos Web no Serviço de Aplicativo do Azure
[Serviço de aplicativo](http://go.microsoft.com/fwlink/?LinkId=529714) fornece funcionalidade interna de monitoramento no hello [Portal do Azure](https://portal.azure.com).
Isso inclui Olá capacidade tooreview **cotas** e **métricas** para um aplicativo, bem como Olá plano de serviço de aplicativo, configurando **alertas** e até mesmo **dimensionamento** automaticamente de acordo com essas métricas.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="understanding-quotas-and-metrics"></a>Noções básicas sobre cotas e métricas
### <a name="quotas"></a>Cotas
Aplicativos hospedados no serviço de aplicativo são o assunto toocertain *limites* nos recursos que eles podem usar. Olá limites são definidos por Olá **plano de serviço de aplicativo** associado ao aplicativo hello.

Se o aplicativo hello está hospedado em um **livre** ou **compartilhado** planejar, em seguida, limites de saudação em recursos Olá Olá aplicativo pode usar são definidos por **cotas**.

Se o aplicativo hello está hospedado em um **básica**, **padrão** ou **Premium** planejar, em seguida, limites de saudação em recursos Olá usarem são definidas pelas Olá **tamanho** (Pequeno, médio, grande) e **a contagem de instâncias** (1, 2, 3,...) do hello **plano de serviço de aplicativo**.

**Cotas** para aplicativos **Gratuitos** ou **Compartilhados** são:

* **CPU(Curto)**
  * Quantidade de CPU permitida para esse aplicativo em um intervalo de cinco minutos. Essa cota é definida novamente a cada cinco minutos.
* **CPU(dia)**
  * Quantidade total de CPU permitida para esse aplicativo em um dia. Essa cota é definida novamente a cada 24 horas, à meia-noite UTC.
* **Memória**
  * Quantidade total de memória permitida para esse aplicativo.
* **Largura de banda**
  * Quantidade total de largura de banda de saída permitida para esse aplicativo em um dia.
    Essa cota é definida novamente a cada 24 horas, à meia-noite UTC.
* **Sistema de arquivos**
  * Quantidade total de armazenamento permitida.

Olá somente cota aplicável tooapps hospedado em **básica**, **padrão** e **Premium** planos é **Filesystem**.

Para obter mais informações sobre cotas específicas hello, limites e recursos disponíveis para Olá diferentes SKUs do serviço de aplicativo podem ser encontradas aqui: [limites de serviço de assinatura do Azure](../azure-subscription-service-limits.md#app-service-limits)

#### <a name="quota-enforcement"></a>Aplicação de cota
Se um aplicativo em seu uso exceder Olá **CPU (curta)**, **CPU (dia)**, ou **largura de banda** cota, Olá aplicativo será interrompido até que a cota de saudação define novamente. Durante esse tempo, todas as solicitações de entrada resultarão em um **HTTP 403**.
![][http403]

Se Olá aplicativo **memória** cota for excedida, aplicativo hello será reiniciado.

Se hello **Filesystem** cota for excedida, em seguida, qualquer operação irá falhar, isso inclui gravar toologs de gravação.

As cotas podem ser aumentadas ou removidas de seu aplicativo pela atualização de seu Plano do Serviço de Aplicativo.

### <a name="metrics"></a>Métricas
**Métricas** fornecem informações sobre o aplicativo hello ou o comportamento do plano de serviço de aplicativo.

Para uma **aplicativo**, métricas de saudação disponíveis são:

* **Tempo Médio de Resposta**
  * Olá tempo médio para solicitações de tooserve aplicativo hello em ms.
* **Conjunto de trabalho de memória média**
  * tempo médio de saudação de memória em MiBs usada pelo aplicativo hello.
* **Tempo de CPU**
  * quantidade de saudação da CPU em segundos consumidos por um aplicativo hello. Para saber mais sobre essa métrica, consulte: [Tempo de CPU versus percentual de CPU](#cpu-time-vs-cpu-percentage)
* **Entrada de Dados**
  * quantidade de saudação de entrada largura de banda consumida pelo aplicativo hello em MiBs.
* **Saída de dados**
  * quantidade de saudação de saída de largura de banda consumida por um aplicativo hello MiBs.
* **Http 2xx**
  * Contagem de solicitações que resultam em um código de status http > = 200, mas < 300.
* **Http 3xx**
  * Contagem de solicitações que resultam em um código de status http > = 300, mas < 400.
* **Http 401**
  * Contagem de solicitações que resultam em um código de status HTTP 401.
* **Http 403**
  * Contagem de solicitações que resultam em um código de status HTTP 403.
* **Http 404**
  * Contagem de solicitações que resultam em um código de status HTTP 404.
* **Http 406**
  * Contagem de solicitações que resultam em um código de status HTTP 406.
* **Http 4xx**
  * Contagem de solicitações que resultam em um código de status http > = 400, mas < 500.
* **Erros do Servidor Http**
  * Contagem de solicitações que resultam em um código de status http > = 500, mas < 600.
* **Conjunto de trabalho de memória**
  * Quantidade de memória usada pelo aplicativo hello MiBs atual.
* **Solicitações**
  * Número total de solicitações, independentemente de seu código de status HTTP resultante.

Para uma **plano de serviço de aplicativo**, métricas de saudação disponíveis são:

> [!NOTE]
> As métricas do Plano do Serviço de Aplicativo só estão disponíveis para os planos no SKU **Básico**, **Standard** e **Premium**.
> 
> 

* **Porcentagem de CPU**
  * Olá média de CPU usada por todas as instâncias do plano de saudação.
* **Porcentagem de Memória**
  * Olá média da memória usada em todas as instâncias do plano de saudação.
* **Entrada de Dados**
  * Olá entrada largura de banda média usada em todas as instâncias do plano de saudação.
* **Saída de dados**
  * Média de saudação largura de banda usada em todas as instâncias do plano de saudação de saída.
* **Tamanho da fila do disco**
  * número médio de saudação de ler e gravar solicitações enfileiradas no armazenamento. Um comprimento de fila de disco alta é uma indicação de um aplicativo que pode ser lento devido a e/s de disco tooexcessive.
* **Tamanho da Fila de Http**
  * Olá média de solicitações HTTP que tinha toosit na fila de saudação antes que está sendo atendida. Um tamanho de fila HTTP alto ou crescente é um sintoma de um plano sob carga pesada.

### <a name="cpu-time-vs-cpu-percentage"></a>Tempo de CPU versus porcentagem de CPU
<!-- toodo: Fix Anchor (#CPU-time-vs.-CPU-percentage) -->

Há duas métricas que refletem o uso da CPU. **Tempo de CPU** e **Percentual de CPU**

**Tempo de CPU** é útil para aplicativos hospedados em **livre** ou **compartilhado** planos como uma das suas cotas é definida em minutos de CPU usados pelo aplicativo hello.

**Porcentagem de CPU** em Olá outro lado é útil para aplicativos hospedados em **básica**, **padrão** e **premium** planos desde que eles podem ser expandidos e essa métrica é uma boa indicação da saudação uso geral em todas as instâncias.

## <a name="metrics-granularity-and-retention-policy"></a>Granularidade de Métricas e a Política de Retenção
Métricas para um plano de serviço de aplicativo e de aplicativo são registradas e agregadas por serviço Olá com hello granularidades e políticas de retenção a seguir:

* Métricas de granularidade de **minuto** são mantidas por **48 horas**
* Métricas de granularidade de **hora** são mantidas por **30 dias**
* Métricas de granularidade de **dia** são mantidas por **90 dias**

## <a name="monitoring-quotas-and-metrics-in-hello-azure-portal"></a>Monitoramento de métricas e cotas no hello Portal do Azure.
Você pode examinar o status de saudação do hello diferente **cotas** e **métricas** afetar um aplicativo hello [Portal do Azure](https://portal.azure.com).

![][quotas]
**Cotas** podem ser encontradas em Configurações >**Cotas**. Olá UX permite que você examine: nome de cotas de saudação (1), (2) o intervalo de redefinição, (3) o limite atual e o valor atual (4).

![][metrics]
**Métricas** pode ser acessado diretamente na folha de recursos de saudação. Você também pode personalizar o gráfico do hello: (1) **clique** nele e selecione (2) **Editar gráfico**.
Aqui você pode alterar hello (3) **intervalo de tempo**, (4) **tipo de gráfico**e (5) **métricas** toodisplay.  

Saiba mais sobre métricas aqui: [Monitorar as métricas do serviço](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).

## <a name="alerts-and-autoscale"></a>Alertas e dimensionamento automático
Métricas para um plano de aplicativo ou serviço de aplicativo pode ser vinculado tooalerts, toolearn mais sobre isso, consulte [receber notificações de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

Aplicativos do Serviço de Aplicativo hospedados em Planos do Serviço de Aplicativo Básico, Standard ou Premium oferecem suporte ao **Dimensionamento Automático**. Isso permite que você regras tooconfigure que monitorar as métricas de plano de serviço de aplicativo e podem aumentar ou diminuir a contagem de instância Olá fornecer recursos adicionais conforme necessário, ou salvando money quando o aplicativo hello excesso de provisionamento. Você pode aprender mais sobre AutoEscala aqui: [como tooScale](../monitoring-and-diagnostics/insights-how-to-scale.md) e aqui [as práticas recomendadas para dimensionamento automático do Monitor do Azure](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)

> [!NOTE]
> Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo. Nenhum cartão de crédito é exigido, sem compromissos.
> 
> 

## <a name="whats-changed"></a>O que mudou
* Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

[fzilla]:http://go.microsoft.com/fwlink/?LinkId=247914
[vmsizes]:http://go.microsoft.com/fwlink/?LinkID=309169



<!-- Images. -->
[http403]: ./media/web-sites-monitor/http403.png
[quotas]: ./media/web-sites-monitor/quotas.png
[metrics]: ./media/web-sites-monitor/metrics.png
