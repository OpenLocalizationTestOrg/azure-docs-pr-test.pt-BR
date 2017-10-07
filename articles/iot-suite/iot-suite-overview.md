---
title: "Visão geral do Azure IoT Suite aaaMicrosoft | Microsoft Docs"
description: "Visão geral de como o Azure IoT Suite agrega internet das coisas soluções pré-configuradas toocollect, analisar, armazenar dados, fornecer visualizações e integrar com outros sistemas."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 2d38d08a-4133-4e5c-8b28-f93cadb5df05
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 385025c5ec0d37c74689a928bc09e85b33439634
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-iot-suite"></a>Visão geral do Azure IoT Suite

Hello Azure internet dos serviços de coisas (IoT) oferecem uma ampla variedade de recursos. Esses serviços de nível corporativo permitem que você:

* Colete dados de dispositivos
* Analise fluxos de dados em movimento
* Armazene e consulte grandes conjuntos de dados
* Visualize dados históricos e em tempo real
* Realize a integração com sistemas de back-office
* Gerenciar seus dispositivos

toodeliver, esses recursos, o Azure IoT Suite pacotes juntos em vários serviços do Azure com extensões personalizadas como *soluções pré-configuradas*. Essas soluções pré-configuradas são as implementações básicas dos padrões comuns de solução de IoT que ajudam a tooreduce Olá tempo você toodeliver suas soluções de IoT. Usando Olá [kits de desenvolvimento de software IoT][lnk-sdks], você pode personalizar e estender essas soluções toomeet seus próprios requisitos. Você também pode usar essas soluções como exemplos ou modelos no desenvolvimento de novas soluções de IoT.

Olá vídeo a seguir fornece uma introdução tooAzure IoT Suite:

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON309/player]
> 
> 

## <a name="azure-iot-services-in-azure-iot-suite"></a>Serviços do Azure IoT no Azure IoT Suite
as soluções de saudação pré-configurado geralmente usam Olá serviços a seguir:

* Núcleo tooAzure IoT Suite é hello [Azure IoT Hub] [ lnk-iot-hub] service. Esse serviço fornece Olá dispositivo para nuvem e recursos de nuvem para dispositivo mensagens e age como Olá toohello de gateway de nuvem e Olá outros serviços importantes do IoT Suite. Olá serviço permite que as mensagens de tooreceive de seus dispositivos em grande escala e enviar comandos tooyour dispositivos. Olá serviço também permite que você muito[gerenciar seus dispositivos][lnk-device-management]. Por exemplo, configurar, reinicializar ou executar uma redefinição de fábrica em um ou mais hub de toohello conectado de dispositivos.
* O [Stream Analytics do Azure][lnk-asa] fornece análise de dados em movimento. IoT Suite usa essa telemetria de entrada de tooprocess de serviço, executar agregação e detecção de eventos. soluções de Olá pré-configurado também usam o stream analytics tooprocess mensagens informativas que contêm dados como metadados ou comando respostas de dispositivos. soluções de saudação usam mensagens de saudação do Stream Analytics tooprocess de dispositivos e entregar as mensagens tooother serviços.
* [Armazenamento do Azure] [ lnk-azure-storage] e [o banco de dados do Azure Cosmos] [ lnk-document-db] fornecer recursos de armazenamento de dados de saudação. Olá soluções pré-configuradas usam telemetria de toostore de armazenamento de blob e toomake-las disponíveis para análise. soluções de saudação usam metadados do banco de dados do Cosmos toostore dispositivo e habilitam os recursos de gerenciamento de dispositivo Olá das soluções de saudação.
* [Os aplicativos Web do Azure] [ lnk-web-apps] e [Microsoft Power BI] [ lnk-power-bi] fornecer Olá recursos de visualização de dados. flexibilidade de saudação do Power BI permite que você tooquickly criar seus próprios painéis interativos que usam dados do IoT Suite.

Para obter uma visão geral da arquitetura de saudação de uma solução de IoT típica, consulte [Microsoft Azure e hello Internet das coisas (IoT)][iot-suite-what-is-azure-iot].

## <a name="preconfigured-solutions"></a>Soluções pré-configuradas

IoT Suite inclui soluções pré-configuradas que habilitar tooquickly você começar a usar e tooexplore Olá cenários IoT comuns, como:

* Monitoramento remoto
* Manutenção preditiva
* Fábrica conectada

Você pode implantar essas soluções tooyour assinatura do Azure e, em seguida, executar um cenário IoT completo, de ponta a ponta.

## <a name="next-steps"></a>Próximas etapas

Agora que você tem uma visão geral do IoT Suite que pode fazer e quais são seus principais componentes, você pode aprender mais sobre as soluções de saudação pré-configurados em IoT Suite. Para obter mais informações, consulte [quais são hello Azure IoT soluções pré-configuradas?][lnk-what-are-preconfig]

[lnk-sdks]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-azure-storage]: https://azure.microsoft.com/documentation/services/storage/
[lnk-document-db]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-power-bi]: https://powerbi.microsoft.com/
[lnk-web-apps]: https://azure.microsoft.com/documentation/services/app-service/web/
[iot-suite-what-is-azure-iot]: iot-suite-what-is-azure-iot.md
[lnk-what-are-preconfig]: iot-suite-what-are-preconfigured-solutions.md
[lnk-device-management]: ../iot-hub/iot-hub-device-management-overview.md
