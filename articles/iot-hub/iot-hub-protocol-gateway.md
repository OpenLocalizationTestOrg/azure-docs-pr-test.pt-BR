---
title: gateway do protocolo IoT aaaAzure | Microsoft Docs
description: "Como toouse uma IoT do Azure protocolo capacidades tooextend Hub IoT e protocolo tooenable dispositivos tooconnect tooyour Centro de suporte usando protocolos não suportados nativamente pelo IoT Hub."
services: iot-hub
documentationcenter: 
author: kdotchkoff
manager: timlt
editor: 
ms.assetid: 555e59ae-3136-4533-8ba8-f3a3b6acf648
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: kdotchko
ms.openlocfilehash: 9cfed30149672d8f7e021a9899192105bbcdd400
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# Suporte a protocolos adicionais para Hub IoT
IoT Hub do Azure nativamente dá suporte à comunicação por meio de protocolos de saudação MQTT, AMQP e HTTP. Em alguns casos, gateways de campo ou dispositivos podem não ser capaz de toouse um desses protocolos padrão em exigirão adaptação de protocolo. Nesses casos, você pode usar um gateway personalizado. Um gateway personalizado pode habilitar adaptação de protocolo para pontos de extremidade de IoT Hub ponte tooand de tráfego de saudação do IoT Hub. Você pode usar o hello [gateway de protocolo do Azure IoT](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md) como uma adaptação de protocolo tooenable gateway personalizado para o IoT Hub.

## gateway de protocolo IoT do Azure
gateway do protocolo Hello IoT do Azure é uma estrutura para adaptação de protocolo que foi projetada para alta escala, a comunicação bidirecional de dispositivo com o IoT Hub. gateway do protocolo de saudação é um componente de passagem que aceita conexões de dispositivo por meio de um protocolo específico. Ela preenche Olá tráfego tooIoT Hub AMQP 1.0. gateway do protocolo Hello IoT do Azure está disponível como uma flexibilidade de tooprovide de projeto de software de código-fonte aberto para adicionar suporte para vários protocolos e versões de protocolo.

Você pode implantar o gateway do protocolo hello no Azure de maneira altamente dimensionável usando o Azure Service Fabric, funções de trabalho de serviços de nuvem do Azure ou máquinas virtuais do Windows. Além disso, o gateway de protocolo de saudação pode ser implantado em ambientes locais, como gateways de campo.

gateway do protocolo Hello IoT do Azure inclui um adaptador de protocolo MQTT que permite que você toocustomize Olá comportamento de protocolo MQTT se necessário. Desde que o IoT Hub fornece suporte interno para o protocolo de v 3.1.1 MQTT hello, você deve considerar apenas usando o adaptador de protocolo hello MQTT se as personalizações de protocolo ou requisitos específicos para recursos adicionais são necessários.

adaptador MQTT Olá também demonstra o modelo de programação Olá para a criação de adaptadores de protocolo para outros protocolos. Além disso, modelo de programação do hello Azure IoT protocolo gateway permite especializado você tooplug componentes personalizados para processamento, como autenticação personalizada, as transformações de mensagens, compactação/descompactação ou criptografia/descriptografia de tráfego entre os dispositivos de saudação e IoT Hub.

Para obter flexibilidade, gateway do protocolo hello e implementação MQTT são fornecidas em um projeto de software de código aberto. Isso permite a implementação de saudação toocustomize conforme necessário.

## Próximas etapas
toolearn mais sobre o gateway de protocolo do hello IoT do Azure e como toouse e implantá-lo como parte de sua solução de IoT, consulte:

* [Repositório de gateway de protocolo IoT do Azure no GitHub](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md)
* [Guia de desenvolvedor do gateway do protocolo IoT do Azure](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/docs/DeveloperGuide.md)

toolearn mais sobre como planejar sua implantação do IoT Hub, consulte:

* [Comparar com Hubs de Eventos][lnk-compare]
* [Escala, alta disponibilidade e recuperação de desastre][lnk-scaling]
* [Guia do desenvolvedor do Hub IoT][lnk-devguide]

[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
