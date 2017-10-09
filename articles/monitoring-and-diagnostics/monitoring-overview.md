---
title: aaaMonitoring no Microsoft Azure | Microsoft Docs
description: "Opções quando você quiser toomonitor nada no Microsoft Azure. Azure Monitor, Log Analytics do Application Insights"
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 1b962c74-8d36-4778-b816-a893f738f92d
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: robb
ms.openlocfilehash: f5a4f32525c52613f01a913e09a9fe3fbcbaeb21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-monitoring-in-microsoft-azure"></a>Visão Geral do Monitoramento no Microsoft Azure
Este artigo fornece uma visão geral das ferramentas disponíveis para monitorar o Microsoft Azure. Ela também se aplica
- monitoramento de aplicativos em execução no Microsoft Azure 
- ferramentas/serviços executados fora do Azure que podem monitorar objetos no Azure. 

Ele discute Olá vários produtos e serviços disponíveis e como eles funcionam juntos. Ele pode ajudá-lo toodetermine quais ferramentas são mais apropriadas para você em quais casos.  

## <a name="why-use-monitoring-and-diagnostics"></a>Por que usar o monitoramento e o diagnóstico?

Problemas de desempenho em seu aplicativo de nuvem podem afetar seus negócios. Com diversos componentes interconectados e frequentes lançamentos, degradações podem ocorrer a qualquer momento. E se você estiver desenvolvendo um aplicativo, seus usuários normalmente descobrirão problemas que você não encontrou durante os testes. Você deve saber sobre esses problemas imediatamente e ferramentas para diagnosticar e corrigir problemas de saudação. O Microsoft Azure tem uma variedade de ferramentas para identificar esses problemas.

## <a name="how-do-i-monitor-my-azure-cloud-apps"></a>Como posso monitorar meus aplicativos de nuvem do Azure?

Há uma variedade de ferramentas para monitorar serviços e aplicativos do Azure. Alguns de seus recursos se sobrepõem. Isso é parcialmente por razões históricas e em parte devido toohello obscurecendo entre o desenvolvimento e a operação de um aplicativo. 

Aqui estão as principais ferramentas de saudação:

-   O **Azure Monitor** é uma ferramenta básica para monitorar serviços em execução no Azure. Ele fornece dados de nível de infraestrutura sobre taxa de transferência de saudação de um serviço e uma saudação em torno de ambiente. Se você estiver gerenciando seus aplicativos tudo no Azure, decidir se tooscale para cima ou para baixo de recursos, Monitor do Azure permite que você usa toostart.

-   O **Application Insights** pode ser usado para desenvolvimento e como uma solução de monitoramento de produção. Ele funciona instalando um pacote em seu aplicativo e, assim, fornecendo uma exibição mais interna do que está acontecendo. Seus dados incluem tempos de resposta de dependências, rastreamentos de exceção, instantâneos de depuração, perfis de execução. Ele fornece ferramentas avançadas de inteligentes para analisar todos os essa telemetria ambos toohelp você depurar um aplicativo e toohelp você entender o que os usuários estão fazendo com que ele. Você pode informar se um aumento no tempo de resposta deve ser feito toosomething em um aplicativo ou algum problema de obtenção de recursos externo. Se você usa o Visual Studio e aplicativo hello está com defeito, você pode ficar certo toohello problema linha (s) de código para que possa corrigi-lo.  

-   **Análise de log** é para aqueles que precisam de manutenção de desempenho e planejar tootune nos aplicativos em execução na produção. Ele se baseia no Azure. Ele coleta e agrega dados de várias fontes, embora com um atraso de 10 minutos too15. Ele fornece uma solução holística de gerenciamento de TI para a infraestrutura baseada em nuvem de terceiros (como o Amazon Web Services), do Azure e local. Fornece ferramentas mais sofisticadas tooanalyze dados em mais de fontes, permite consultas complexas entre todos os logs e pode alertar proativamente nas condições especificadas.  Você pode até mesmo coletar dados personalizados em seu repositório central para que possa consultar e visualizá-los. 

-   O **SCOM (System Center Operations Manager)** é voltado ao gerenciamento e monitoramento de grandes instalações de nuvem. Você pode já estar familiarizado como ele como uma ferramenta de gerenciamento para nuvens baseadas em Hyper-V e Windows Server local, mas ele também pode se integrar e gerenciar aplicativos do Azure. Entre outras coisas, ele pode instalar o Application Insights em aplicativos ativos existentes.  Se um aplicativo falhar, ele lhe informa em segundos. Observe que o Log Analytics não substitui o SCOM. Eles funcionam bem em conjunto.  


## <a name="accessing-monitoring-in-hello-azure-portal"></a>Acessando o monitoramento no hello portal do Azure
Agora, todos os serviços de monitoramento do Azure estão disponíveis em um único painel de interface do usuário. Para obter mais informações sobre como tooaccess nessa área, consulte [Introdução ao Azure Monitor](monitoring-get-started.md). 

Você também pode acessar as funções de monitoramento de recursos específicos realçando esses recursos e fazendo uma busca detalhada em suas opções de monitoramento. 

## <a name="examples-of-when-toouse-which-tool"></a>Exemplos de quando toouse qual ferramenta 

Olá seções a seguir mostra alguns cenários básicos e as ferramentas devem ser usadas juntos. 

### <a name="scenario-1--fix-errors-in-an-azure-application-under-development"></a>Cenário 1 – Corrigir erros em um aplicativo do Azure em desenvolvimento   

**Olá melhor opção é juntos toouse Application Insights, o Monitor do Azure e o Visual Studio**

Agora, o Azure fornece toda a capacidade do depurador do Visual Studio Olá na nuvem Olá Olá. Configure o Monitor do Azure toosend telemetria tooApplication Insights. Habilite Olá de tooinclude do Visual Studio SDK do Application Insights no seu aplicativo. Depois que o Application Insights, você pode usar toodiscover de mapa de aplicativo hello visualmente quais partes do seu aplicativo em execução não estão íntegras ou não. Para as partes que não estão íntegras, erros e exceções já estão disponíveis para exploração. Você pode usar Olá várias análises no Application Insights toogo mais profunda. Se você não tiver certeza sobre o erro hello, você pode usar tootrace de depurador do Visual Studio Olá no ponto de código e fixar um problema com mais detalhes. 

Para obter mais informações, consulte [monitoramento de aplicativos da Web](../application-insights/app-insights-azure-web-apps.md) e consulte toohello sumário Olá esquerda para obter instruções sobre vários tipos de aplicativos e idiomas.  

### <a name="scenario-2--debug-an-azure-net-web-application-for-errors-that-only-show-in-production"></a>Cenário 2 – Depurar um aplicativo Web .NET do Azure para encontrar erros que aparecem somente na produção 

> [!NOTE]
> Esses recursos estão no modo de versão prévia. 

**Olá melhor opção é toouse Application Insights e se possível, o Visual Studio para Olá completo experiência de depuração.**

Use Olá Application Insights instantâneo depurador toodebug seu aplicativo. Quando um determinado limite de erro ocorre com os componentes de produção, o sistema Olá captura automaticamente telemetria em janelas de tempo chamado "instantâneos". Olá quantidade capturada é segura para uma nuvem de produção porque é pequeno suficiente não tooaffect desempenho, mas o rastreamento tooallow significativo o suficiente.  sistema de saudação pode capturar vários instantâneos. Você pode pesquisar em um ponto no tempo no hello portal do Azure ou usar o Visual Studio para experiência completa de saudação. Com o Visual Studio, os desenvolvedores podem percorrer o instantâneo como se estivessem depurando em tempo real. Quadros, memória, parâmetros e variáveis locais estão disponíveis. Os desenvolvedores devem receber acesso toothis dados de produção por meio de uma função RBAC.  

Para obter mais informações, consulte [Depuração instantânea](../application-insights/app-insights-snapshot-debugger.md). 

### <a name="scenario-3--debug-an-azure-application-that-uses-containers-or-microservices"></a>Cenário 3 – Depurar um aplicativo do Azure que usa contêineres ou microsserviços 

**O mesmo que o cenário 1. Use o Application Insights, o Azure Monitor e o Visual Studio juntos** O Application Insights também dá suporte à coleta de telemetria de processos em execução dentro de contêineres e de microsserviços (Kubernetes, Docker, Service Fabric do Azure). Para obter mais informações, [assista a este vídeo sobre a depuração de contêineres e microsserviços](https://go.microsoft.com/fwlink/?linkid=848184). 


### <a name="scenario-4--fix-performance-issues-in-your-azure-application"></a>Cenário 4 – Solucionar problemas de desempenho em seu aplicativo do Azure

Olá [criador de perfil do Application Insights](../application-insights/app-insights-profiler.md) é projetado toohelp solucionar esses tipos de problemas. Você pode identificar e solucionar problemas de desempenho para aplicativos em execução nos Serviços de Aplicativos (Aplicativos Web, Aplicativos Lógicos, Aplicativos Móveis, Aplicativos de API) e outros recursos de computação, como Máquinas Virtuais, VMSS (conjunto de dimensionamento de máquinas virtuais), Serviços de Nuvem e Service Fabric. 

> [!NOTE]
> Capacidade tooprofile máquinas virtuais, máquinas virtuais conjuntos de escala (VMSS), os serviços de nuvem e malha de serviços está em visualização.   

Além disso, você é proativamente notificado por email sobre determinados tipos de erros, como tempos de carregamento de página lento, pela ferramenta de detecção inteligente hello.  Você não precisa toodo qualquer configuração sobre essa ferramenta. Para obter mais informações, consulte [Detecção Inteligente – anomalias de desempenho](../application-insights/app-insights-proactive-performance-diagnostics.md) e [Detecção Inteligente – anomalias de desempenho](https://azure.microsoft.com/blog/Enhancments-ApplicationInsights-SmartDetection/preview).



## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre

* [Azure Monitor em um vídeo do Ignite 2016](https://myignite.microsoft.com/videos/4977)
* [Introdução ao Azure Monitor](monitoring-get-started.md)
* [Diagnóstico do Azure](../azure-diagnostics.md) se você estiver tentando toodiagnose problemas em seu serviço de nuvem, Máquina Virtual, a máquina Virtual dimensionar aplicativo de malha definido ou serviço.
* [Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) se você estiver tentando toodiagnostic problemas em seu aplicativo Web do serviço de aplicativo.
* [Análise de log](https://azure.microsoft.com/documentation/services/log-analytics/) e hello [Operations Management Suite](https://www.microsoft.com/oms/) solução de monitoramento de produção