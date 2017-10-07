---
title: "Visão geral de IoT Hub de aaaAzure | Microsoft Docs"
description: "Visão geral da saudação serviço Azure IoT Hub: o que é o IoT Hub, conectividade de dispositivo, internet de padrões de comunicação de coisas, gateways e padrão de comunicação auxiliadas por serviço Olá"
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 24376318-5344-4a81-a1e6-0003ed587d53
ms.service: iot-hub
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0b46868a1ec9e13c8f107b90269c5307f4ba27c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-hello-azure-iot-hub-service"></a>Visão geral da saudação serviço Azure IoT Hub

Bem-vindo tooAzure IoT Hub. Este artigo fornece uma visão geral do Azure IoT Hub e descreve por que você deve usar esse serviço tooimplement uma solução de Internet das coisas (IoT). O Hub IoT do Azure é um serviço totalmente gerenciado que permite comunicações bidirecionais confiáveis e seguras entre milhões de dispositivos IoT e um back-end da solução. Hub IoT do Azure:

* Fornece várias opções de comunicação do dispositivo para a nuvem e da nuvem para o dispositivo incluindo: mensagens unidirecionais, transferência de arquivos e métodos de solicitação de resposta.
* Fornece tooother de roteamento de mensagem declarativa interna serviços do Azure.
* Fornece um armazenamento consultável para metadados de dispositivo e informações de estado sincronizado.
* Habilita comunicações seguras e controle de acesso usando chaves de segurança por dispositivo ou certificados X.509.
* Fornece monitoramento abrangente para eventos de gerenciamento de identidade do dispositivo e de conectividade do dispositivo.
* Inclui bibliotecas de dispositivo para plataformas e idiomas de hello mais populares.

artigo Olá [comparação de IoT Hub e Hubs de eventos] [ lnk-compare] descreve Olá principais diferenças entre esses dois serviços e destaca Olá vantagens de usar o IoT Hub em suas soluções de IoT.

Para obter mais informações sobre como do Azure e o IoT Hub ajudam a proteger sua solução de IoT, consulte [segurança de Internet das coisas de saudação de plano de fundo para cima][lnk-security-ground-up].

![Hub IoT do Azure como gateway de nuvem em solução de Internet das coisas][img-architecture]

> [!NOTE]
> Para obter uma discussão detalhada da arquitetura do IoT, consulte Olá [arquitetura de referência do Microsoft Azure IoT][lnk-refarch].

## <a name="iot-device-connectivity-challenges"></a>Desafios de conectividade do dispositivo IoT

Bibliotecas de dispositivo do IoT Hub e hello ajudarão-lo a desafios de saudação toomeet como tooreliably e se conectar com segurança dispositivos toohello solução back-end. Dispositivos IoT:

* Com frequência, são sistemas internos sem operadores humanos.
* Podem estar em locais remotos, onde o acesso físico é caro.
* Só podem ser alcançadas por meio de back-end de solução hello.
* Podem ter recursos de energia e de processamento limitados.
* Podem ter conectividade de rede intermitente, lenta ou cara.
* Talvez seja necessário toouse protocolos de aplicativo proprietárias, personalizados ou específicos do setor.
* Podem ser criados usando um grande conjunto de plataformas de hardware e de software conhecidas.

Além disso requisitos toohello acima, qualquer solução de IoT deve também fornecer dimensionamento, segurança e confiabilidade. o conjunto de requisitos de conectividade resultante Olá é difícil e demorado tooimplement quando você usar tecnologias tradicionais, como contêineres de web e agentes de mensagens.

## <a name="why-use-azure-iot-hub"></a>Por que usar o Hub IoT do Azure?

Além disso tooa avançado conjunto de [dispositivo para nuvem] [ lnk-d2c-guidance] e [nuvem para dispositivo] [ lnk-c2d-guidance] opções de comunicação, incluindo mensagens, arquivos endereços de Azure IoT Hub transferências e métodos de solicitação-resposta, Olá desafios de conectividade do dispositivo em Olá maneiras a seguir:

* **Gêmeos de dispositivo**. Usando os [Gêmeos de dispositivo][lnk-twins] você pode armazenar, sincronizar e consultar informações de metadados e o estado do dispositivo. Dispositivos gêmeos são documentos JSON que armazenam informações do estado do dispositivo (metadados, configurações e condições). IoT Hub mantém duas um dispositivo de cada dispositivo que você se conecte tooIoT Hub.

* **Autenticação por dispositivo e conectividade segura**. Você pode provisionar cada dispositivo com sua própria [chave de segurança] [ lnk-devguide-security] tooenable-tooconnect tooIoT Hub. Olá [registro de identidade de IoT Hub] [ lnk-devguide-identityregistry] armazena as identidades de dispositivo e as chaves em uma solução. Um back-end da solução pode adicionar tooallow dispositivos individuais ou negar lista tooenable total controle sobre o acesso ao dispositivo.

* **Rota de dispositivo para nuvem mensagens tooAzure serviços com base em regras declarativas**. IoT Hub permite que você toodefine mensagem rotas com base em roteamento toocontrol regras onde seu hub envia mensagens de dispositivo para a nuvem. Regras de roteamento não requer nenhum código de toowrite você e podem ocorrer Olá de distribuidores de mensagem personalizada de pós inclusão de.

* **Monitoramento das operações de conectividade do dispositivo**. Você pode receber os logs de operação detalhados sobre operações de gerenciamento de identidade do dispositivo e eventos de conectividade do dispositivo. Esse recurso de monitoramento permite que seus problemas de conectividade do IoT solução tooidentify, como dispositivos que tente tooconnect com credenciais incorretas, enviar mensagens com muita frequência ou rejeitar todas as mensagens de nuvem para dispositivo.

* **Um amplo conjunto de bibliotecas de dispositivos**. Os [SDKs do dispositivo IoT do Azure][lnk-device-sdks] estão disponíveis e têm suporte para várias linguagens e plataformas: C para muitas distribuições Linux, Windows e sistemas operacionais em tempo real. Os SDKs de dispositivo IoT do Azure também oferecem suporte a linguagens gerenciadas, como C#, Java e JavaScript.

* **Protocolos e extensibilidade do IoT**. Se sua solução não é possível usar bibliotecas de dispositivo Olá, o IoT Hub expõe um protocolo público que permite que dispositivos toonatively uso de saudação MQTT v 3.1.1, protocolos de AMQP 1.0 ou HTTP 1.1. Você também pode estender o IoT Hub toosupport para protocolos personalizados por:

  * Criar um gateway de campo com [Azure IoT borda] [ lnk-iot-edge] que converte seu tooone protocolo personalizado de saudação três protocolos entendidos pelo IoT Hub.
  * Personalizando Olá [gateway de protocolo do Azure IoT][protocol-gateway], um componente de código-fonte aberto que é executado na nuvem hello.

* **Escala**. IoT Hub do Azure pode ser dimensionado toomillions de dispositivos conectados simultaneamente e milhões de eventos por segundo.

## <a name="gateways"></a>Gateways

Um gateway em uma solução de IoT é normalmente uma [gateway do protocolo] [ lnk-iotedge] implantado na nuvem hello ou [gateway de campo] [ lnk-field-gateway] que é implantado localmente com seus dispositivos. Um gateway de protocolo executa a conversão de protocolo, por exemplo MQTT tooAMQP. Um gateway de campo pode executar análise na borda Olá, tomar decisões de detecção de hora tooreduce latência, fornecer serviços de gerenciamento de dispositivo, impor restrições de privacidade e segurança e também executar a conversão de protocolo. Ambos os tipos de gateway atuam como intermediários entre os seus dispositivos e o Hub IoT.

Um gateway de campo é diferente de um dispositivo de roteamento de tráfego simples (como um dispositivo conversão de endereços de rede ou firewall), pois geralmente ele executa uma função ativa no gerenciamento de acesso e no fluxo de informações da solução.

A mesma solução pode incluir gateways de protocolo e de campo.

## <a name="how-does-iot-hub-work"></a>Como funciona o Hub IoT?

IoT Hub do Azure implementa Olá [auxiliadas por serviço de comunicação] [ lnk-service-assisted-pattern] interações de saudação padrão toomediate entre os dispositivos e sua solução de back-end. Olá objetivo auxiliada por serviço de comunicação é aos caminhos de comunicação confiável, bidirecional de tooestablish entre um sistema de controle, como o IoT Hub e dispositivos com finalidade especial que são implantados em um espaço físico não confiável. padrão de saudação estabelece Olá princípios a seguir:

* A segurança tem precedência sobre todos os outros recursos.

* Os dispositivos não aceitam informações de rede não solicitadas. Um dispositivo estabelece todas as conexões e rotas de forma apenas de saída. Para um dispositivo tooreceive um comando de back-end de arquivo de solução hello, dispositivo Olá regularmente deve iniciar um toocheck de conexão para qualquer tooprocess de comandos pendentes.

* Só devem se conectar a dispositivos tooor estabelecer serviços de toowell conhecido de rotas que eles são emparelhados com, como o IoT Hub.

* caminho de comunicação Olá entre o dispositivo e o serviço ou entre o dispositivo e o gateway está protegido na camada de protocolo de aplicativo hello.

* A autenticação e a autorização no nível de sistema são baseadas nas identidades por dispositivo. Elas tornam as permissões e credenciais de acesso quase instantaneamente revogáveis.

* A comunicação bidirecional para dispositivos que se conectam esporadicamente vencimento toopower ou problemas de conectividade é facilitada mantendo comandos e notificações de dispositivo até que um dispositivo se conecta tooreceive-los. IoT Hub mantém filas específico do dispositivo para comandos Olá envia.

* Dados de carga do aplicativo são protegidos separadamente para tráfego protegido por meio do serviço tooa gateways.

Olá setor móvel usou padrão de comunicação auxiliadas por serviço Olá a serviços de notificação de push enorme escala tooimplement como [Windows Push Notification Services][lnk-wns], [Google Cloud Messaging][lnk-google-messaging], e [Apple Push Notification Service][lnk-apple-push].

O Hub IoT tem suporte no caminho público de emparelhamento do ExpressRoute.

## <a name="next-steps"></a>Próximas etapas

toolearn como toosend mensagens de um dispositivo e recebê-las de IoT Hub, bem como encaminhar mensagens tooconfigure, consulte [enviar e receber mensagens com o IoT Hub][lnk-send-messages].

toolearn como o IoT Hub permite o gerenciamento de dispositivo baseado em padrões para você tooremotely gerenciar, configurar e atualizar seus dispositivos, consulte [visão geral do gerenciamento de dispositivos com o IoT Hub][lnk-device-management].

aplicativos de cliente tooimplement em uma ampla variedade de plataformas de hardware de dispositivos e sistemas operacionais, você pode usar o dispositivo de IoT do Azure de saudação SDKs. dispositivo Olá SDKs incluem bibliotecas que facilitam a telemetria tooan IoT hub e o recebimento de nuvem para dispositivo as mensagens enviadas. Quando você usa o dispositivo de saudação SDKs, você pode escolher entre vários toocommunicate de protocolos de rede com o IoT Hub. toolearn mais, consulte Olá [informações sobre dispositivo SDKs][lnk-device-sdks].

tooget iniciado gravar um código e executar alguns exemplos, consulte Olá [começar com o IoT Hub] [ lnk-get-started] tutorial.

[img-architecture]: media/iot-hub-what-is-iot-hub/hubarchitecture.png

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[protocol-gateway]: https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md
[lnk-service-assisted-pattern]: http://blogs.msdn.com/b/clemensv/archive/2014/02/10/service-assisted-communication-for-connected-devices.aspx "Comunicação Assistida de Serviço, postagem de blog feita por Clemens Vasters"
[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-iotedge]: iot-hub-protocol-gateway.md
[lnk-field-gateway]: iot-hub-devguide-endpoints.md#field-gateways
[lnk-devguide-identityregistry]: iot-hub-devguide-identity-registry.md
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-wns]: https://msdn.microsoft.com/library/windows/apps/mt187203.aspx
[lnk-google-messaging]: https://developers.google.com/cloud-messaging/
[lnk-apple-push]: https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW9
[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-refarch]: http://download.microsoft.com/download/A/4/D/A4DAD253-BC21-41D3-B9D9-87D2AE6F0719/Microsoft_Azure_IoT_Reference_Architecture.pdf
[lnk-iot-edge]: https://github.com/Azure/iot-edge
[lnk-send-messages]: iot-hub-devguide-messaging.md
[lnk-device-management]: iot-hub-device-management-overview.md

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[lnk-security-ground-up]: iot-hub-security-ground-up.md
