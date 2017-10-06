---
title: aaaOverview da borda do IoT do Azure | Microsoft Docs
description: "Descreve os conceitos arquitetura no Azure IoT Edge Olá chave como agentes, módulos e gateways."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dobett
ms.openlocfilehash: 32debc0d4f40cfd7f2cce7cf8c76b12ec18ee2dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-edge-architectural-concepts"></a>Conceitos de arquitetura do Azure IoT Edge

Antes de examinar um código de exemplo ou criar seu próprio gateway de campo usando borda IoT, você deve entender os conceitos de chave de saudação que são a base de arquitetura de saudação da borda de IoT.

## <a name="iot-edge-modules"></a>Módulos do IoT Edge

Você cria um gateway com o Azure IoT Edge criando e montando *módulos do IoT Edge*. Os módulos usam *mensagens* tooexchange dados entre si. Um módulo recebe uma mensagem, executa alguma ação nele, opcionalmente o transforma em uma nova mensagem e, em seguida, publica para outros módulos tooprocess. Alguns módulos poderão gerar apenas novas mensagens e nunca processar as mensagens de entrada. Uma cadeia de módulos cria um pipeline de processamento de dados com cada módulo executar uma transformação nos dados de saudação em um ponto em que o pipeline.

![Uma cadeia de módulos no gateway, compilada com o IoT Edge do Azure][1]

Borda de IoT contém Olá componentes a seguir:

* Módulos pré-gravados que executam funções comuns de gateway.
* interfaces de saudação um desenvolvedor podem usar módulos personalizados toowrite.
* Olá toodeploy necessário de infraestrutura e executar um conjunto de módulos.

Olá SDK fornece uma camada de abstração que permite que você toobuild gateways toorun em vários sistemas operacionais e plataformas.

![Camada de abstração do IoT Edge do Azure][2]

## <a name="messages"></a>Mensagens

Embora pensar módulos transmitindo mensagens tooeach outros é uma maneira conveniente de tooconceptualize como funções um gateway, ele não refletir precisamente o que acontece. Módulos de borda IoT usam toocommunicate um agente com o outro. Módulos publicar broker toohello de mensagens (usando padrões de mensagens, como de barramento ou a publicação/assinatura) e deixe Olá broker rota Olá mensagem toohello módulos conectados tooit.

Um módulo usa Olá **Broker_Publish** toopublish um agente de mensagens toohello de função. broker Olá oferece módulo de tooa de mensagens, chamando uma função de retorno de chamada. Uma mensagem consiste em um conjunto de propriedades de chave/valor e no conteúdo transmitido como um bloco de memória.

![função Hello de saudação do Broker no Azure IoT Edge][3]

## <a name="message-routing-and-filtering"></a>Roteamento e filtragem de mensagens

Há duas maneiras de módulos toohello IoT borda corretos mensagens toodirect:

* Você pode passar um conjunto de links podem ser passados toohello agente para agente Olá Saiba fonte hello e coletor para cada módulo.
* Um módulo pode filtrar em Propriedades de saudação de mensagem de saudação.

Um módulo só deve agir sobre uma mensagem se a mensagem de saudação é destinada. Os links e a filtragem de mensagens criam efetivamente um pipeline de mensagem.

## <a name="next-steps"></a>Próximas etapas

toosee esses conceitos aplicados em um exemplo que você pode executar, consulte [arquitetura de explorar o Azure IoT borda][lnk-hello-world].

<!-- Images -->
[1]: media/iot-hub-iot-edge-overview/modules.png
[2]: media/iot-hub-iot-edge-overview/modules_2.png
[3]: media/iot-hub-iot-edge-overview/messages_1.png

<!-- Links -->
[lnk-hello-world]: ./iot-hub-linux-iot-edge-get-started.md