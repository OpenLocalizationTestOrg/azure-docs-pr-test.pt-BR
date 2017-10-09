---
title: "aaaAzure Service Fabric visão geral do gerenciamento de API | Microsoft Docs"
description: "Este artigo é uma introdução toousing gerenciamento de API do Azure como um aplicativo de malha do serviço do gateway tooyour."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/22/2017
ms.author: vturecek
ms.openlocfilehash: f01dc570a11e68cd4a2d878abbe6019e209e2f5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-with-azure-api-management-overview"></a>Service Fabric com visão geral de Gerenciamento de API do Azure

Aplicativos de nuvem normalmente necessário um gateway de front-end de tooprovide um único ponto de entrada para os usuários, dispositivos ou outros aplicativos. No Service Fabric, um gateway pode ser qualquer serviço sem estado, como um [aplicativo ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md), ou outro serviço projetado para entrada de tráfego, como [Hubs de Evento](https://docs.microsoft.com/azure/event-hubs/), [Hub IoT](https://docs.microsoft.com/azure/iot-hub/) ou [Gerenciamento de API do Azure](https://docs.microsoft.com/azure/api-management/).

Este artigo é uma introdução toousing gerenciamento de API do Azure como um aplicativo de malha do serviço do gateway tooyour. Gerenciamento de API se integra diretamente com o Service Fabric, permitindo que você toopublish APIs com um amplo conjunto de regras tooyour back-end do Service Fabric de serviços de roteamento. 

## <a name="architecture"></a>Arquitetura
Uma arquitetura comum de malha do serviço usa um aplicativo web de página única que faz chamadas HTTP serviços tooback-end que expõem APIs do HTTP. Olá [aplicativo de exemplo de Introdução do Service Fabric](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started) mostra um exemplo dessa arquitetura.

Nesse cenário, um serviço web sem monitoração de estado funciona como gateway de saudação em Olá aplicativo do Service Fabric. Essa abordagem requer toowrite um serviço web que pode proxy HTTP solicita serviços tooback-end, conforme mostrado no diagrama a seguir de saudação:

![Service Fabric com visão geral da topologia do Gerenciamento de API do Azure][sf-web-app-stateless-gateway]

Conforme os aplicativos crescem em complexidade, portanto Olá gateways que devem apresentar uma API na frente de uma infinidade de serviços de back-end. Gerenciamento de API do Azure é projetado toohandle APIs complexas com regras de roteamento e controle de acesso, a limitação de taxa, monitoramento, o log de eventos, o cache de resposta com um mínimo de trabalho de sua parte. Gerenciamento de API do Azure oferece suporte à descoberta de serviço do Service Fabric, resolução de partição e rota de toointelligently seleção réplica diretamente solicita serviços tooback-end no Service Fabric para não ter toowrite seu próprio gateway API sem monitoração de estado. 

Nesse cenário, Olá web que interface do usuário ainda é atendida por meio de um serviço web, enquanto as chamadas da API HTTP são gerenciadas e roteadas por meio do gerenciamento de API do Azure, conforme mostrado no diagrama a seguir de saudação:

![Service Fabric com visão geral da topologia do Gerenciamento de API do Azure][sf-apim-web-app]

## <a name="application-scenarios"></a>Cenários de aplicativos

Os serviços em Service Fabric podem ser sem estado ou com estado e podem ser particionados usando um dos três esquemas: singleton, intervalo int-64 e nomeado. A resolução do ponto de extremidade de serviço requer a identificação de uma partição específica de uma instância de serviço específica. Durante a resolução de um ponto de extremidade de serviço, ambos Olá nome da instância de serviço (por exemplo, `fabric:/myapp/myservice`), bem como a partição específica de saudação do serviço Olá deve ser especificada, exceto no caso de saudação de partição singleton.

O Gerenciamento de API do Azure pode ser usado com qualquer combinação de serviços sem estado, serviços com estado e qualquer esquema de particionamento.

## <a name="send-traffic-tooa-stateless-service"></a>Enviar serviço sem monitoração de estado do tráfego tooa

No caso mais simples de saudação, o tráfego é encaminhado tooa instância de serviço sem monitoração de estado. tooachieve isso, uma operação de gerenciamento de API contém uma diretiva de processamento de entrada com um back-end do Service Fabric que mapeia a instância de serviço sem monitoração de estado específico de tooa Olá Service Fabric back-end. Solicitações enviadas toothat serviço são enviadas a réplica aleatório tooa da instância de serviço sem monitoração de estado de saudação.

#### <a name="example"></a>Exemplo
Olá cenário a seguir, um aplicativo de malha do serviço contém um serviço sem monitoração de estado chamado `fabric:/app/fooservice`, que expõe uma API HTTP interno. nome de instância do serviço de saudação é bem conhecida e pode ser embutida em código diretamente na Olá diretiva de processamento de entrada de gerenciamento de API. 

![Service Fabric com visão geral da topologia do Gerenciamento de API do Azure][sf-apim-static-stateless]

## <a name="send-traffic-tooa-stateful-service"></a>Enviar o serviço com monitoração de estado do tráfego tooa

Cenário de serviço sem monitoração de estado toohello semelhante, o tráfego pode ser encaminhado tooa instância de serviço com monitoração de estado. Nesse caso, uma operação de gerenciamento de API contém uma diretiva de processamento de entrada com um back-end do Service Fabric que mapeia uma partição específica de tooa de solicitação de um determinado *com monitoração de estado* instância de serviço. partição de saudação toomap toois cada solicitação computados através de um método de lambda usando uma entrada de solicitação HTTP entrada hello, como um valor no caminho de URL hello. política de saudação pode ser configurado toosend solicitações toohello réplica primária apenas, ou tooa aleatória para operações de leitura.

#### <a name="example"></a>Exemplo

Olá cenário a seguir, um aplicativo de malha do serviço contém um serviço com monitoração de estado particionado chamado `fabric:/app/userservice` que expõe uma API HTTP interno. nome de instância do serviço de saudação é bem conhecida e pode ser embutida em código diretamente na Olá diretiva de processamento de entrada de gerenciamento de API.  

Olá serviço for particionado usando o esquema de partição Olá Int64 com duas partições e um intervalo de chave que abrange `Int64.MinValue` muito`Int64.MaxValue`. diretiva de back-end Olá computa uma chave de partição dentro desse intervalo convertendo Olá `id` valor fornecido em inteiro de 64 bits do tooa caminho do hello URL solicitação, embora qualquer algoritmo pode ser uma chave de partição Olá usado toocompute aqui. 

![Service Fabric com visão geral da topologia do Gerenciamento de API do Azure][sf-apim-static-stateful]

## <a name="send-traffic-toomultiple-stateless-services"></a>Enviar tráfego serviços sem estado toomultiple

Em cenários mais avançados, você pode definir uma operação de gerenciamento de API que mapeia solicitações toomore de instância de um serviço. Nesse caso, cada operação contém uma política que mapeia as solicitações de instância de serviço específico tooa com base nos valores de saudação solicitação HTTP de entrada, como cadeia de consulta ou caminho de URL hello e, no caso de saudação do services com monitoração de estado, uma partição na instância do serviço Olá . 

tooachieve isso, uma API de gerenciamento de operação contém uma diretiva de processamento de entrada com um back-end do Service Fabric que mapeia a instância de serviço sem monitoração de estado tooa Olá Service Fabric back-end com base nos valores recuperados de solicitação HTTP de entrada hello. Instância do serviço tooa solicitações são enviadas a réplica aleatório tooa da instância de serviço hello.

#### <a name="example"></a>Exemplo

Neste exemplo, uma nova instância de serviço sem monitoração de estado é criada para cada usuário de um aplicativo com um nome gerado dinamicamente usando Olá seguinte fórmula:
 
 - `fabric:/app/users/<username>`

 Cada serviço tem um nome exclusivo, mas os nomes de saudação não são conhecidos inicial porque Olá serviços são criados em resposta toouser ou admin de entrada e, portanto, não pode ser codificado em políticas APIM ou regras de roteamento. Em vez disso, o nome de saudação do hello serviço toowhich toosend uma solicitação é gerado na definição de política de back-end de saudação do hello `name` valor fornecido no caminho de solicitação de URL hello. Por exemplo:

  - A solicitação muito`/api/users/foo` é roteado tooservice instância`fabric:/app/users/foo`
  - A solicitação muito`/api/users/bar` é roteado tooservice instância`fabric:/app/users/bar`

![Service Fabric com visão geral da topologia do Gerenciamento de API do Azure][sf-apim-dynamic-stateless]

## <a name="send-traffic-toomultiple-stateful-services"></a>Enviar o tráfego de serviços com monitoração de estado toomultiple

Exemplo de serviço sem monitoração de estado toohello semelhante, uma API de gerenciamento pode mapear operação solicitações toomore que um **com monitoração de estado** instância de serviço, caso em que você também pode precisar de resolução de partição tooperform para cada serviço com monitoração de estado instância.

tooachieve isso, uma API de gerenciamento de operação contém uma diretiva de processamento de entrada com um back-end do Service Fabric que mapeia a instância de serviço com monitoração de estado tooa Olá Service Fabric back-end com base nos valores recuperados de solicitação HTTP de entrada hello. Além disso toomapping uma instância de serviço de toospecific de solicitação, solicitação Olá também pode ser mapeado tooa a partição específica dentro de instância de serviço hello e, opcionalmente, réplica primária do tooeither Olá ou uma réplica secundária aleatória dentro de partição de saudação.

#### <a name="example"></a>Exemplo

Neste exemplo, uma nova instância de serviço com monitoração de estado é criada para cada usuário do aplicativo hello com um nome gerado dinamicamente usando Olá seguinte fórmula:
 
 - `fabric:/app/users/<username>`

 Cada serviço tem um nome exclusivo, mas os nomes de saudação não são conhecidos inicial porque Olá serviços são criados em resposta toouser ou admin de entrada e, portanto, não pode ser codificado em políticas APIM ou regras de roteamento. Em vez disso, o nome de saudação do hello serviço toowhich toosend uma solicitação é gerado na definição de política de back-end de saudação do hello `name` caminho de solicitação de URL de saudação do valor fornecido. Por exemplo:

  - A solicitação muito`/api/users/foo` é roteado tooservice instância`fabric:/app/users/foo`
  - A solicitação muito`/api/users/bar` é roteado tooservice instância`fabric:/app/users/bar`

Cada instância de serviço também é particionada usando o esquema de partição Olá Int64 com duas partições e um intervalo de chave que abrange `Int64.MinValue` muito`Int64.MaxValue`. diretiva de back-end Olá computa uma chave de partição dentro desse intervalo convertendo Olá `id` valor fornecido em inteiro de 64 bits do tooa caminho do hello URL solicitação, embora qualquer algoritmo pode ser uma chave de partição Olá usado toocompute aqui. 

![Service Fabric com visão geral da topologia do Gerenciamento de API do Azure][sf-apim-dynamic-stateful]

## <a name="next-steps"></a>Próximas etapas

Siga Olá [guia de início rápido](service-fabric-api-management-quick-start.md) tooset a sua primeira malha do serviço de cluster com gerenciamento de API e o fluxo de solicitações por meio de serviços de tooyour de gerenciamento de API.

<!-- links -->

<!-- pics -->
[sf-apim-web-app]: ./media/service-fabric-api-management-overview/sf-apim-web-app.png
[sf-web-app-stateless-gateway]: ./media/service-fabric-api-management-overview/sf-web-app-stateless-gateway.png
[sf-apim-static-stateless]: ./media/service-fabric-api-management-overview/sf-apim-static-stateless.png
[sf-apim-static-stateful]: ./media/service-fabric-api-management-overview/sf-apim-static-stateful.png
[sf-apim-dynamic-stateless]: ./media/service-fabric-api-management-overview/sf-apim-dynamic-stateless.png
[sf-apim-dynamic-stateful]: ./media/service-fabric-api-management-overview/sf-apim-dynamic-stateful.png