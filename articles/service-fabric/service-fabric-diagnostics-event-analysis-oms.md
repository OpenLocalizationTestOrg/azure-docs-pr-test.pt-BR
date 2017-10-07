---
title: "Análise de eventos do serviço de malha com o OMS do aaaAzure | Microsoft Docs"
description: "Saiba mais sobre visualização e análise de eventos utilizando o OMS para o monitoramento e diagnóstico de clusters do Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/26/2017
ms.author: dekapur
ms.openlocfilehash: 526519293e70982c95e31241465b87f190096f74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="event-analysis-and-visualization-with-oms"></a>Análise de eventos e visualização com OMS

Operations Management Suite (OMS) é uma coleção de serviços de gerenciamento que ajudam com monitoramento e diagnóstico para aplicativos e serviços hospedados na nuvem hello. ler tooget uma visão mais detalhada do OMS e que ele oferece [o que é o OMS?](../operations-management-suite/operations-management-suite-overview.md)

## <a name="log-analytics-and-hello-oms-workspace"></a>Log de análise e hello espaço de trabalho do OMS

O Log Analytics coleta dados de recursos gerenciados, incluindo uma tabela de armazenamento do Azure ou um agente, e os mantém em um repositório central. dados de saudação, em seguida, podem ser usado para análise, alertas e visualização ou exportação ainda mais. O Log Analytics dá suporte a eventos, dados de desempenho ou outros dados personalizados.

Quando o OMS é configurado, você terá acesso tooa específico *espaço de trabalho do OMS*, de onde os dados poderão ser consultados ou visualizados em painéis.

Depois que dados são recebidos pela análise de Log, o OMS tem várias *soluções de gerenciamento* que são soluções predefinida toomonitor os dados de entrada, cenários de tooseveral personalizado. Isso inclui um *análise de malha do serviço* solução e um *contêineres* solução, que são toodiagnostics Olá dois aqueles mais relevantes e ao usar clusters de malha do serviço de monitoramento. Há vários outros também que vale a pena explorar e OMS também permite a criação de saudação de soluções personalizadas, que você pode ler mais sobre [aqui](../operations-management-suite/operations-management-suite-solutions.md). Cada solução que você escolhe toouse para um cluster será configurado na Olá mesmo espaço de trabalho do OMS, juntamente com a análise de Log. Espaços de trabalho permitem painéis personalizados e visualização de dados e modificações toohello dados toocollect, processar e analisar.

## <a name="setting-up-an-oms-workspace-with-hello-service-fabric-solution"></a>Configurar um espaço de trabalho do OMS com hello solução de malha do serviço

É recomendável que você incluir Olá solução de malha do serviço em seu espaço de trabalho do OMS, como ele fornece um painel útil que mostra Olá vários canais de log de entrada do nível de plataforma e o aplicativo hello e tooquery capaz de saudação do Service Fabric específicas logs. Aqui está uma solução de malha do serviço relativamente simples aparência, com um único aplicativo implantado em um cluster de saudação:

![Solução de OMS SF](media/service-fabric-diagnostics-event-analysis-oms/service-fabric-solution.png)

Há dois tooprovision de maneiras e configurar um espaço de trabalho do OMS, por meio de um modelo do Gerenciador de recursos ou diretamente do Azure Marketplace. Use antigo hello quando você estiver implantando um cluster e habilitado Olá última opção se você já tiver um cluster implantado com o diagnóstico.

### <a name="deploying-oms-using-a-resource-management-template"></a>Implantação do OMS usando um modelo de Gerenciamento de Recursos

Isso ocorre no estágio de criação de cluster Olá - ao implantar um cluster usando um modelo de Gerenciador de recursos, o modelo de saudação também pode criar um novo espaço de trabalho do OMS, adicionar Olá tooit de solução de malha do serviço e configurá-lo tooread dados de armazenamento apropriado Olá tabelas.

>[!NOTE]
>Para este toowork diagnóstico tem toobe habilitado para Olá tooexist de tabelas de armazenamento do Azure para OMS / análise de Log tooread informações do.

[Aqui](https://azure.microsoft.com/resources/templates/service-fabric-oms/) está um modelo de exemplo que você pode usar e modificar conforme a necessidade, que executa as ações acima. No caso de Olá que desejar mais opções, alguns modelos mais oferecem opções diferentes dependendo de onde no processo de saudação é configurar um espaço de trabalho do OMS – eles podem ser encontrados em [modelos de serviço de malha e o OMS](https://azure.microsoft.com/resources/templates/?term=service+fabric+OMS).

### <a name="deploying-oms-using-through-azure-marketplace"></a>Implantação com o OMS por meio do Azure Marketplace

Se você preferir tooadd um espaço de trabalho do OMS depois de implantar um cluster, vá direto tooAzure Marketplace e procure *"Análise de malha do serviço"*. Deve haver apenas um recurso que aparece, na categoria de "Gerenciamento de monitoramento de +" Olá, mostrada abaixo:

![Análise do OMS SF no Marketplace](media/service-fabric-diagnostics-event-analysis-oms/service-fabric-analytics.png)

Clicar em **Criar** solicitará um espaço de trabalho do OMS. Clique em **Selecionar um espaço de trabalho** e **Criar um novo espaço de trabalho**. Preencher as entradas de saudação necessária - Olá aqui a única exigência é que a assinatura Olá Olá malha do serviço de cluster e hello espaço de trabalho do OMS deve ser Olá mesmo. Depois que as entradas forem validadas, a área de trabalho do OMS será implantada em alguns minutos. Enquanto termina de implantação, criação de saudação da folha de solução do Service Fabric Olá ainda permanecerá aberta. Certifique-se de que Olá mesmo mostra espaço de trabalho, backup em *espaço de trabalho do OMS* e clique em **criar** na parte inferior do hello, tooadd Olá espaço de trabalho do Service Fabric solução toohello.

## <a name="using-hello-oms-agent"></a>Usando Olá agente do OMS

É recomendável toouse EventFlow WAD como soluções de agregação porque eles permitem um toodiagnostics abordagem mais modular e monitoramento. Por exemplo, não se você quiser toochange suas saídas de EventFlow, requer nenhuma alteração tooyour real instrumentação apenas um arquivo de configuração de tooyour simples modificação. Se, no entanto, você pode decidir tooinvest usando o OMS e estiver disposto toocontinue usá-lo para análise de evento (não tem toobe Olá somente plataforma que você usar, mas em vez disso, que ele será pelo menos uma das plataformas de saudação), é recomendável que você explore Configurando Olá [</C0>agentedoOMS<spanclass="notranslate">](../log-analytics/log-analytics-windows-agents.md).</span> Você também deve usar o agente do OMS Olá durante a implantação de cluster de tooyour de contêineres, conforme discutido abaixo.

processo de saudação para fazer isso é relativamente fácil, pois apenas tiver tooadd Olá agente como uma escala de máquina virtual do conjunto de modelo do Gerenciador de recursos de tooyour de extensão, garantindo que ele é instalado em cada um de seus nós. Um modelo do Gerenciador de recursos de exemplo que implanta o espaço de trabalho do hello OMS com hello solução de malha do serviço (como acima) e adiciona Olá agente tooyour nós pode ser encontrado para clusters que executam [Windows](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/SF%20OMS%20Samples/Windows) ou [Linux](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/SF%20OMS%20Samples/Linux).

Olá vantagens isso são seguinte hello:

* Dados mais avançados no lado de contadores e métricas de desempenho de saudação
* Fácil tooconfigure dados sendo coletados de saudação do cluster e fazer alterações tooit sem reimplantar seus aplicativos ou cluster hello, pois alterações toohello configurações do agente de saudação podem ser feitas no espaço de trabalho OMS hello e serão apenas redefinir agente Olá automaticamente. tooconfigure Olá OMS agente toopick backup contadores de desempenho específicos, espaço de trabalho toohello vá **página inicial > Configurações > dados > contadores de desempenho do Windows** e escolher dados Olá você gostaria que toosee coletado
* Os dados mostram mais rápido do que ele tenha toobe armazenado antes de transmitido pelo OMS / análise de Log
* Monitorar contêineres é muito mais fácil, pois é possível selecionar logs de docker (stdout, stderror) e estatísticas (métricas de desempenho nos níveis de contêiner e nó)

Olá principal consideração aqui é que como é um agente, ele será implantado em seu cluster juntamente com todos os seus aplicativos, então haverá algumas desempenho de toohello impacto mínimo de seus aplicativos em cluster hello.

## <a name="monitoring-containers"></a>Monitoramento de contêineres

Ao implantar um cluster de malha do serviço de tooa de contêineres, é recomendável que hello cluster foi configurado com o agente do OMS hello e essa solução contêineres Olá tenha sido adicionado tooyour OMS espaço de trabalho tooenable monitoramento e diagnóstico. É aqui que recipientes Olá solução parece com um espaço de trabalho:

![Painel do OMS básico](./media/service-fabric-diagnostics-event-analysis-oms/oms-containers-dashboard.png)

Agente de saudação habilita a coleta de saudação de vários logs específicos de contêineres que podem ser consultadas no OMS ou usado toovisualized indicadores de desempenho. Olá os tipos de log que são coletados são:

* ContainerInventory: mostra informações sobre imagens, nome e localização do contêiner
* ContainerImageInventory: informações sobre imagens implantadas, inclusive IDs ou tamanhos
* ContainerLog: logs de erros específicos, logs de docker (stdout etc.) e outras entradas
* ContainerServiceLog: comandos de daemon do docker que foram executados
* Desempenho: contadores de desempenho incluindo o contêiner de cpu, memória, tráfego de rede, e/s de disco e métricas personalizadas de saudação hospedam máquinas

Este artigo aborda Olá etapas necessárias tooset o contêiner de monitoramento para seu cluster. toolearn mais sobre solução de contêineres do OMS, confira seus [documentação](../log-analytics/log-analytics-containers.md).

tooset backup Olá solução de contêiner no espaço de trabalho, verifique se você tem o agente do OMS Olá implantado em nós do cluster por etapas Olá mencionados acima. Depois que o cluster Olá estiver pronta, implante tooit um contêiner. Tenha em mente que Olá a primeira vez que uma imagem de contêiner é cluster tooa implantado, ele entra em várias imagens de saudação toodownload minutos dependendo de seu tamanho.

No Azure Marketplace, procure *contêineres* e crie um recurso de contêineres (em Olá monitoramento + gerenciamento categoria).

![Adicionando a solução de Contêineres](./media/service-fabric-diagnostics-event-analysis-oms/containers-solution.png)

Na etapa de criação de hello, ele solicita um espaço de trabalho do OMS. Selecione Olá que foi criado com a implantação de saudação acima. Esta etapa adiciona uma solução de contêineres dentro de seu espaço de trabalho do OMS e será detectada automaticamente pelo agente do OMS Olá implantado pelo modelo de saudação. Agente de saudação começará a coletar dados sobre processos de contêineres Olá Olá cluster e menos de 15 minutos ou assim, você deve ver a solução de saudação destaque com dados, como na imagem de saudação do painel de saudação acima.


## <a name="next-steps"></a>Próximas etapas

Explore Olá toocustomize de ferramentas e opções de OMS que precisa tooyour um espaço de trabalho a seguir:

* Para clusters de local, o OMS oferece um Gateway (Forward Proxy HTTP) que pode ser usado toosend tooOMS de dados. Leia mais sobre isso em [conectar computadores sem tooOMS de acesso à Internet usando Olá Gateway do OMS](../log-analytics/log-analytics-oms-gateway.md)
* Configurar o OMS tooset [alerta automatizado](../log-analytics/log-analytics-alerts.md) tooaid na detecção e diagnóstico
* Obter trazido com hello [pesquisa e consulta de log](../log-analytics/log-analytics-log-searches.md) recursos oferecidos como parte da análise de Log
