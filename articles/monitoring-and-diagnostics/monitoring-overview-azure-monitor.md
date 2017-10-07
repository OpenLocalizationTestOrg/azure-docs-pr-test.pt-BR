---
title: "Visão geral do Monitor de aaaAzure | Microsoft Docs"
description: "O Azure Monitor coleta estatísticas para uso em alertas, webhooks, dimensionamento automático e automação. O artigo também lista outras opções de monitoramento da Microsoft."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: robb
ms.openlocfilehash: ffa304e7b158f0fceb7f60ab88fab291976aa0e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-monitor"></a>Visão geral do Azure Monitor
Este artigo fornece uma visão geral da saudação serviço do Monitor do Azure no Microsoft Azure. Ele discute o que faz Monitor do Azure e fornece ponteiros tooadditional informações sobre como toouse Monitor do Azure.  Se você preferir um vídeo de Introdução, consulte links para etapas Avançar na parte inferior da saudação deste artigo. 

## <a name="why-monitor-your-application-or-system"></a>Por que monitorar seu aplicativo ou sistema
Os aplicativos em nuvem são complexos com muitas partes móveis. O monitoramento fornece tooensure de dados que seu aplicativo permaneça ativo e em execução em um estado íntegro. Ele também ajuda você toostave off problemas potenciais ou solucionar problemas após os. Além disso, você pode usar o monitoramento dados toogain aprofundamento sobre seu aplicativo. Esse conhecimento pode ajudá-lo a facilidade de manutenção ou de desempenho do aplicativo tooimprove, ou automatizar ações que normalmente exigiriam a intervenção manual.


## <a name="azure-monitor-and-microsofts-other-monitoring-products"></a>Azure Monitor e outros produtos de monitoramento da Microsoft
O Azure Monitor fornece logs e métricas de infraestrutura de nível básico para a maioria dos serviços do Microsoft Azure. Serviços do Azure que não colocarem ainda seus dados no Monitor do Azure colocará-lo no hello futuras.

A Microsoft fornece produtos e serviços adicionais que oferecem mais recursos de monitoramento para desenvolvedores, DevOps ou operações de TI que também têm instalações locais. Para ter uma compreensão e visão geral de como esses diferentes produtos e serviços funcionam juntos, consulte [Monitoramento no Microsoft Azure](monitoring-overview.md).

## <a name="monitoring-sources---compute"></a>Fontes de monitoramento – Computação

![Modelo para o monitoramento e diagnóstico dos recursos não de computação](./media/monitoring-overview-azure-monitor/Monitoring_Azure_Resources-compute_v6.png)

Serviços de computação Olá incluem 
- Serviços de Nuvem 
- Máquinas Virtuais 
- Conjuntos de escala de Máquina Virtual 
- Service Fabric

### <a name="application---diagnostics-logs-application-logs-and-metrics"></a>Aplicativo - Logs de Diagnóstico, Logs de Aplicativo e Métrica
Aplicativos podem ser executados sobre Olá SO convidado no modelo de computação hello. Eles emitem seu próprio conjunto de métricas e logs. Monitor do Azure depende Olá diagnóstico do Azure extensão (Windows ou Linux) toocollect a maioria dos logs e as métricas de nível de aplicativo. Olá tipos incluem

* Contadores de desempenho
* Logs de aplicativo
* Logs de Eventos do Windows
* Fonte de evento do .NET
* Logs IIS
* Manifesto com base no ETW
* Despejos de Falha
* Logs de Erro do Cliente

Sem extensão de diagnóstico hello, apenas algumas métricas como uso de CPU estão disponíveis. 

### <a name="host-and-guest-vm-metrics"></a>Métricas de VM host e convidada
Olá recursos de computação listadas anteriormente tem uma VM do host dedicado e interagem com sistema operacional convidado. Olá host VM e o sistema operacional convidado são equivalente de saudação da raiz da VM e VM convidada no modelo de hipervisor Hyper-V hello. Você pode coletar métricas sobre ambos. Você também pode coletar logs de diagnóstico no sistema operacional convidado de saudação.   

### <a name="activity-log"></a>Log de Atividade
Você pode pesquisar hello (anteriormente chamado operacional ou os Logs de auditoria) do Log de atividades para obter informações sobre seu recurso como visto pelo Olá infraestrutura do Azure. log de saudação contém informações como horários quando os recursos são criados ou destruídos.  Para obter mais informações, consulte [Visão geral do log de atividades](monitoring-overview-activity-logs.md). 

## <a name="monitoring-sources---everything-else"></a>Fontes de monitoramento – todo o restante

![Modelo para o monitoramento e diagnóstico dos recursos de computação](./media/monitoring-overview-azure-monitor/Monitoring_Azure_Resources-non-compute_v6.png)


### <a name="resource---metrics-and-diagnostics-logs"></a>Recursos - Métricas e Logs de Diagnóstico
Logs de diagnóstico e métricas colecionável variam com base no tipo de recurso de saudação. Por exemplo, aplicativos Web fornece estatísticas sobre hello e/s de disco e por cento da CPU. Essas métricas não existem para uma fila do Barramento de Serviço, que, em vez disso, fornece métricas como tamanho da fila e taxa de transferência de mensagem. Uma lista de métricas que podem ser coletadas para cada recurso está disponível em [métricas com suporte](monitoring-supported-metrics.md). 

### <a name="host-and-guest-vm-metrics"></a>Métricas de VM host e convidada
Não há necessariamente um mapeamento individual entre o recurso e uma determinada VM host ou convidada, portanto, as métricas não estão disponíveis.

### <a name="activity-log"></a>Log de Atividade
log de atividades de saudação é Olá igual para recursos de computação.  

## <a name="uses-for-monitoring-data"></a>Usos dos Dados de Monitoramento
Depois de coletar os dados, você pode fazer Olá a seguir com ele no Monitor do Azure

### <a name="route"></a>Rota
Você pode transmitir locais de tooother de dados de monitoramento em tempo real.

Os exemplos incluem:

- Envie tooApplication Insights, você pode usar suas ferramentas de visualização e análise mais ricas.
- Envie Hubs tooEvent para que você possa rotear ferramentas de terceiros toothird. 

### <a name="store-and-archive"></a>Armazenar e arquivar
Alguns dados de monitoramento já ficam armazenados e disponíveis no Azure Monitor por um período determinado. 
- As métricas são armazenadas por 30 dias. 
- As entradas do log de atividades são armazenadas por 90 dias. 
- Logs de diagnóstico não são armazenados. 

Se você quiser toostore dados mais de saudação períodos de tempo listados acima, você pode usar um armazenamento do Azure. Os dados de monitoramento são mantidos em sua conta de armazenamento com base em uma política de retenção que você definir. Você tem toopay para Olá Olá de espaço dados ocupam no armazenamento do Azure. 

Alguns toouse de maneiras esses dados:

- Uma vez gravados, você pode ter outras ferramentas dentro ou fora do Azure para lê-los e processá-los.
- Baixar dados Olá localmente para um arquivo local ou alterar sua política de retenção nos dados do hello nuvem tookeep por longos períodos de tempo.  
- Você pode deixar dados saudação no armazenamento do Azure indefinidamente para fins de arquivamento. 

### <a name="query"></a>Consultar
Você pode usar o hello API REST do Monitor do Azure, comandos de Interface de linha de comando (CLI) de plataforma cruzada, cmdlets do PowerShell, ou tooaccess do SDK do .NET Olá Olá dados no sistema de saudação ou no armazenamento do Azure

Os exemplos incluem:

* Obtendo dados para um aplicativo de monitoramento personalizado escrito por você
* Criar consultas personalizadas e enviar esse aplicativo de terceiros tooa dados.

### <a name="visualize"></a>Visualizar
Visualizando seus dados em gráficos e gráficos de monitoramentos ajuda você a encontrar as tendências mais rápido do que examinar dados Olá em si.  

Alguns métodos de visualização incluem:

* Use Olá portal do Azure
* Dados de rota tooAzure Application Insights
* Dados de rota tooMicrosoft PowerBI
* Rota Olá dados tooa visualização de terceiros ferramenta usando o live streaming ou fazendo com que a ferramenta de saudação ler de um arquivo no armazenamento do Azure


### <a name="automate"></a>Automatizar
Você pode usar os alertas de monitoramento tootrigger de dados ou até mesmo processos inteiros. Os exemplos incluem:

* Use instâncias de computação tooautoscale dados para cima ou para baixo com base na carga do aplicativo.
* Envie emails quando uma métrica passar de um limite predeterminado.
* Chamar uma ação de um tooexecute de URL (webhook) da web em um sistema fora do Azure
* Iniciar um runbook na automação do Azure tooperform qualquer variedade de tarefas

## <a name="methods-of-accessing-azure-monitor"></a>Métodos para acessar o Azure Monitor
Em geral, você pode manipular o controle de dados, o roteamento e a recuperação usando um dos métodos a seguir de saudação. Nem todos os métodos estão disponíveis para todas as ações ou tipos de dados.

* [Portal do Azure](https://portal.azure.com)
* [PowerShell](insights-powershell-samples.md)  
* [CLI (Interface de linha de comando) de plataforma cruzada](insights-cli-samples.md)
* [API REST](https://docs.microsoft.com/rest/api/monitor/)
* [SDK .NET](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor)

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre
- Um passo a passo em vídeo do Azure Monitor está disponível em  
[Introdução ao Azure Monitor](https://channel9.msdn.com/Blogs/Azure-Monitoring/Get-Started-with-Azure-Monitor). Um vídeo adicional explicando um cenário no qual você pode usar o Azure Monitor está disponível em [Explore o monitoramento e diagnósticos no Microsoft Azure](https://channel9.msdn.com/events/Ignite/2016/BRK2234) e [Azure Monitor em um vídeo do Ignite 2016](https://myignite.microsoft.com/videos/4977)
- Percorra a interface do Monitor do Azure Olá no [guia de Introdução ao Monitor do Azure](monitoring-get-started.md)
- Configurar Olá [extensões de diagnóstico do Azure](../azure-diagnostics.md) se você estiver tentando toodiagnose problemas em seu serviço de nuvem, Máquina Virtual, a máquina Virtual dimensionar conjuntos ou aplicativo do Service Fabric.
- [Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) se você estiver tentando toodiagnostic problemas em seu aplicativo Web do serviço de aplicativo.
- [Solucionar de problemas no Armazenamento do Azure](../storage/common/storage-e2e-troubleshooting.md) ao usar os Blobs, Tabelas ou Filas de Armazenamento
- [Análise de log](https://azure.microsoft.com/documentation/services/log-analytics/) e hello [Operations Management Suite](https://www.microsoft.com/oms/)
