---
title: "passo a passo do aaaConnected fábrica Azure IoT Suite solução | Microsoft Docs"
description: "Uma descrição do hello Azure IoT pré-configurado solução conectados fábrica e sua arquitetura."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: dobett
ms.openlocfilehash: 7fd55c51351659401349cfde91a20fce1045b4f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connected-factory-preconfigured-solution-walkthrough"></a>Passo a passo de solução pré-configurada de fábrica conectada

Olá IoT Suite conectado fábrica [pré-configurado solução] [ lnk-preconfigured-solutions] é uma implementação de uma solução de ponta a ponta industrial que:

* Conecta-se tooboth simulado industrial dispositivos que executam o OPC UA servidores em linhas de produção de fábrica simulada e dispositivos de servidor de OPC UA reais. Para obter mais informações sobre OPC UA, consulte Olá [conectado perguntas Frequentes de fábrica](iot-suite-faq-cf.md).
* Mostra KPIs operacionais e OEE desses dispositivos e de linhas de produção.
* Demonstra como um aplicativo baseado em nuvem pode ser usado toointeract com sistemas de servidor de OPC UA.
* Permite que você tooconnect seus próprios dispositivos de servidor OPC UA.
* Permite que você toobrowse e modificar Olá dados do servidor de OPC UA.
* Integra-se com hello Azure tempo série Insights (TSI) serviço tooprovide exibições personalizadas de dados de saudação de seus servidores de OPC UA.

Você pode usar a solução hello como ponto de partida para sua própria implementação e [personalizar] [ lnk-customize] -toomeet seus próprios requisitos comerciais específicos.

Este artigo o orienta por meio de alguns dos elementos-chave Olá Olá conectado fábrica solução tooenable toounderstand como ele funciona. Esse conhecimento ajuda a:

* Solucione problemas na solução de saudação.
* Planejar como toocustomize toohello solução toomeet necessidades específicas.
* Criar sua própria solução IoT que usa os serviços do Azure.

Para obter mais informações, consulte Olá [conectado perguntas Frequentes de fábrica](iot-suite-faq-cf.md).

## <a name="logical-architecture"></a>Arquitetura lógica

Olá diagrama a seguir descreve os componentes lógicos de saudação da solução Olá pré-configurados:

![Arquitetura lógica de fábrica conectada][connected-factory-logical]

## <a name="communication-patterns"></a>Padrões de comunicação

solução de saudação usa Olá [especificação OPC UA Pub/Sub](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) toosend tooIoT de dados de telemetria OPC UA Hub no formato JSON. solução de saudação usa Olá [OPC publicador](https://github.com/Azure/iot-edge-opc-publisher) módulo IoT borda para essa finalidade.

solução de saudação também tem um cliente de OPC UA integrado a um aplicativo web que pode estabelecer conexões com servidores OPC UA locais. Olá cliente usa um [proxy reverso](https://wikipedia.org/wiki/Reverse_proxy) e receber ajuda de conexão do IoT Hub toomake Olá sem a necessidade de abrir portas no firewall de local de saudação. Esse padrão de comunicação é chamado de [comunicação auxiliada por serviço](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/). solução de saudação usa Olá [OPC Proxy](https://github.com/Azure/iot-edge-opc-proxy/) módulo IoT borda para essa finalidade.


## <a name="simulation"></a>Simulação

Olá simulados estações e execução de produção de hello simulado sistemas (MES) formam uma linha de produção de fábrica. Hello dispositivos simulados e hello OPC publicador módulo baseiam Olá [OPC UA .NET padrão] [ lnk-OPC-UA-NET-Standard] publicado por Olá OPC Foundation.

Olá OPC Proxy e o publicador de OPC são implementados como módulos com base em [Azure IoT borda][lnk-Azure-IoT-Gateway]. Cada linha de produção simulada tem um gateway designado anexado.

Todos os componentes de simulação executados em contêineres Docker hospedados em uma VM do Linux do Azure. simulação de saudação é configurado toorun oito simulada linhas de produção por padrão.

## <a name="simulated-production-line"></a>Linha de produção simulada

Uma linha de produção fabrica peças. É composto de estações diferentes: uma estação de assembly, uma de teste e uma de empacotamento.

simulação de saudação é executado e atualiza os dados de saudação que são expostos por meio de nós OPC UA hello. Todas as estações de linha de produção simulada são gerenciadas pelo Olá MES por meio de OPC UA.

## <a name="simulated-manufacturing-execution-system"></a>Sistema de execução de fabricação simulado

Olá MES monitora cada estação na linha de produção de hello por meio de alterações de status do OPC UA toodetect estação. Ele chama OPC UA estações do métodos toocontrol hello e passa um produto de uma estação toohello lado até que ela seja concluída.

## <a name="gateway-opc-publisher-module"></a>Módulo de editor de gateway OPC

Módulo de publicador OPC conecta toohello estação OPC UA servidores e assina toohello OPC nós toobe publicado. módulo de saudação converte dados de nó de saudação em formato JSON, criptografa e envia tooIoT Hub como mensagens de OPC UA Pub/Sub.

módulo de OPC publicador Olá apenas exige uma porta de saída https (443) e pode trabalhar com a infraestrutura existente do enterprise.

## <a name="gateway-opc-proxy-module"></a>Módulo de proxy de gateway OPC

Olá Gateway OPC UA Proxy módulo túneis de mensagens de comando e controle de OPC UA binárias e requer apenas uma porta de saída https (443). Pode funcionar com a infraestrutura existente da empresa, inclusive Proxies da Web.

Ele usa dados do dispositivo do Hub IoT métodos tootransfer colocadas em pacotes TCP/IP na camada de aplicativo hello e, portanto, garante a relação de confiança de ponto de extremidade, criptografia de dados e integridade usando SSL/TLS.

Olá protocolo binário de OPC UA retransmitido por meio do proxy de saudação em si usa criptografia e autenticação de assistência ao usuário.

## <a name="azure-time-series-insights"></a>Azure Time Series Insights

Olá Gateway OPC publicador módulo assina tooOPC UA servidor nós toodetect de alterações em valores de dados de saudação. Se for detectada uma alteração de dados em um de nós hello, esse módulo envia mensagens tooAzure IoT Hub.

IoT Hub fornece uma fonte de evento tooAzure TSI. Armazena dados de TSI por 30 dias, com base em carimbos de hora anexado toohello mensagens. Os dados incluem:

* ApplicationUri UA OPC
* NodeId UA OPC
* Valor do nó de saudação
* Carimbo de data/hora de origem
* DisplayName UA OPC

Atualmente, TSI não permitem que os clientes desejarem dados Olá tookeep toocustomize quanto tempo.

O TSI executa consultas em relação a dados de nó usando um SearchSpan (Time.From, Time.To) e agrega por OPC UA ApplicationUri, OPC UA NodeId ou OPC UA DisplayName.

dados de saudação tooretrieve Olá OEE e um KPI, gráficos e medidores gráficos de série de tempo de saudação, dados são agregados por contagem de eventos, Sum, Avg, Min e Max.

série de tempo de saudação é criado usando um processo diferente. OEE KPIs calculados do banco de dados de estação e são transferidos para a topologia de saudação (linhas de produção, fábricas, enterprise) no aplicativo hello.

Além disso, a série temporal para a topologia OEE e um KPI é calculado no aplicativo hello, sempre que um período de tempo exibido está pronto. Por exemplo, modo de exibição de dia de saudação é atualizado a cada hora cheia.

exibição de série de tempo de saudação de dados do nó vêm diretamente de TSI usando uma agregação para o período de tempo.

## <a name="iot-hub"></a>Hub IoT
Olá [hub IoT] [ lnk-IoT Hub] recebe os dados enviados do hello OPC publicador módulo em nuvem hello e facilita o serviço do Azure TSI toohello disponíveis. 

Olá IoT Hub na solução Olá também:
- Mantém um registro de identidade que armazena IDs Olá para todos os módulo de publicador OPC e todos os módulos de Proxy de OPC.
- É usado como o canal de transporte para a comunicação bidirecional de saudação OPC Proxy módulo.

## <a name="azure-storage"></a>Armazenamento do Azure
solução de Olá usa o armazenamento de BLOBs do Azure como o armazenamento em disco para dados de implantação de VM e toostore hello.

## <a name="web-app"></a>Aplicativo Web
aplicativo web do Hello implantado como parte da solução Olá pré-configurado consiste de um cliente integrado de OPC UA, processamento de alertas e visualização de telemetria.

## <a name="next-steps"></a>Próximas etapas

Você pode continuar a guia de Introdução com IoT Suite lendo Olá artigos a seguir:

* [Permissões no site de azureiotsuite.com Olá][lnk-permissions]
* [Implantar um gateway no Windows ou Linux para solução de fábrica pré-configurado Olá conectado](iot-suite-connected-factory-gateway-deployment.md)

[connected-factory-logical]:media/iot-suite-connected-factory-walkthrough/cf-logical-architecture.png

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-IoT Hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-OPC-UA-NET-Standard]:https://github.com/OPCFoundation/UA-.NETStandardLibrary
[lnk-Azure-IoT-Gateway]: https://github.com/azure/iot-edge
[lnk-permissions]: iot-suite-permissions.md
