---
title: aaaDebug microservices do Azure no Windows | Microsoft Docs
description: "Saiba como toomonitor e diagnosticar seus serviços escritos usando o Microsoft Azure Service Fabric em uma máquina de desenvolvimento local."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: edcc0631-ed2d-45a3-851d-2c4fa0f4a326
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/24/2017
ms.author: dekapur
ms.openlocfilehash: 24868aa194b8a28fa3e6de95c1de5506d912a544
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a>Monitorar e diagnosticar serviços em uma configuração de desenvolvimento do computador local
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [Linux](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
> 
> 

Monitoramento, detectar, diagnosticar e solucionar problemas permitem toocontinue de serviços com a experiência do usuário toohello mínimo de interrupção. Enquanto o monitoramento e diagnóstico é essencial em um ambiente de produção implantado real, eficiência de saudação dependem adotando um modelo semelhante durante o desenvolvimento de serviços tooensure funcionam quando você move tooa instalação do mundo real. Malha do serviço facilita para diagnóstico de tooimplement de desenvolvedores de serviço que pode funcionar perfeitamente em configurações de desenvolvimento local único computador e configurações de cluster de produção do mundo real.

## <a name="event-tracing-for-windows"></a>Rastreamento de Eventos para Windows
[Rastreamento de eventos do Windows](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) (ETW) é hello recomendado tecnologia para mensagens de rastreamento na malha do serviço. Alguns benefícios de usar ETW são:

* **O ETW é rápido.** Ele foi criado como uma tecnologia de rastreamento que tem impacto mínimo sobre os tempos de execução de código.
* **O rastreamento ETW funciona perfeitamente nos ambientes de desenvolvimento locais e também nas configurações de cluster reais.** Isso significa que você não tem toorewrite o rastreamento de código quando você estiver pronto toodeploy cluster código tooa real.
* **O código do sistema da Malha do Serviço também usa o ETW para rastreamento interno.** Isso permite que você tooview os rastreamentos de aplicativo intercalados com rastreamentos de sistema do Service Fabric. Ele também ajuda você toomore compreender facilmente sequências hello e as relações entre o código do aplicativo e os eventos no sistema subjacente hello.
* **Não há suporte interno no serviço do Fabric Visual Studio tools tooview eventos ETW.** Eventos ETW aparecem no hello exibição de eventos de diagnóstico do Visual Studio quando o Visual Studio está configurado corretamente com o Service Fabric. 

## <a name="view-service-fabric-system-events-in-visual-studio"></a>Exibir eventos do sistema da Malha do Serviço no Visual Studio
Serviço de malha emite eventos ETW de desenvolvedores de aplicativos toohelp entender o que está acontecendo na plataforma de saudação. Se você ainda não fez isso, vá em frente e siga as etapas de saudação em [criando seu primeiro aplicativo no Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md). Essas informações ajudarão você colocar um aplicativo em execução com hello Visualizador de eventos de diagnóstico mostrando Olá mensagens de rastreamento.

1. Se diagnóstico Olá janela eventos não mostram, automaticamente, vá toohello **exibição** guia no Visual Studio, escolha **outras janelas** e **Visualizador de eventos de diagnóstico**.
2. Cada evento contém informações de metadados padrão que informa ao evento de saudação nó, aplicativo e serviço Olá é proveniente. Você também pode filtrar a lista de saudação de eventos usando Olá **filtrar eventos** caixa na parte superior de Olá Olá de janela de eventos. Por exemplo, você pode filtrar por **Nome do Nó** ou **Nome do Serviço.** E quando você está olhando detalhes do evento, você também pode pausar usando Olá **pausar** botão na parte superior de Olá Olá de janela de eventos e reiniciar mais tarde sem qualquer perda de eventos.
   
   ![Visualizador de Eventos de Diagnóstico do Visual Studio](./media/service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally/DiagEventsExamples2.png)

## <a name="add-your-own-custom-traces-toohello-application-code"></a>Adicionar seu próprio código de aplicativo toohello rastreamentos personalizados
modelos de projeto de serviço do Fabric Visual Studio Olá contêm o código de exemplo. código de saudação mostra como o código de aplicativo personalizado tooadd ETW rastreia que mostram o no Visualizador de ETW do Visual Studio Olá junto com rastreamentos de sistema do Service Fabric. Olá vantagem desse método é que metadados são adicionados automaticamente tootraces e Olá Visual Studio diagnóstico Visualizador de eventos já está configurado toodisplay-los.

Para projetos criados de saudação **modelos de serviço** (com ou sem estado) apenas procurar Olá `RunAsync` implementação:

1. Olá chamada muito`ServiceEventSource.Current.ServiceMessage` em Olá `RunAsync` método mostra um exemplo de um rastreamento ETW personalizada do código do aplicativo hello.
2. Em Olá **ServiceEventSource.cs** arquivo, você encontrará uma sobrecarga para Olá `ServiceEventSource.ServiceMessage` método deve ser usado para eventos de alta frequência devido a motivos de tooperformance.

Para projetos criados de saudação **modelos de ator** (com ou sem estado):

1. Olá abrir **"ProjectName" CS** arquivo onde *ProjectName* é Olá nome escolhido para o projeto do Visual Studio.  
2. Localizar código Olá `ActorEventSource.Current.ActorMessage(this, "Doing Work");` em Olá *DoWorkAsync* método.  Este é um exemplo de um rastreamento ETW personalizado escrito a partir do código do aplicativo.  
3. No arquivo **ActorEventSource.cs**, você encontrará uma sobrecarga para Olá `ActorEventSource.ActorMessage` método deve ser usado para eventos de alta frequência devido a motivos de tooperformance.

Depois de adicionar tooyour código de serviço de rastreamento de ETW personalizado, você pode criar, implantar e executar o aplicativo hello toosee novamente o evento (s) no Visualizador de eventos de diagnóstico de saudação. Se você depurar o aplicativo hello com **F5**, Olá Visualizador de eventos de diagnóstico será aberto automaticamente.

## <a name="next-steps"></a>Próximas etapas
Olá mesmo código de rastreamento que você adicionou o aplicativo tooyour acima para diagnóstico local funcionará com ferramentas que você pode usar tooview esses eventos durante a execução de seu aplicativo em um cluster do Azure. Consulte estes artigos que abordam opções diferentes de saudação para ferramentas hello e descrevem como você pode defini-las para cima.

* [Como toocollect registra com o diagnóstico do Azure](service-fabric-diagnostics-how-to-setup-wad.md)
* [Agregação e coleta de eventos usando o EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md)

