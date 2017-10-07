---
title: "Opções de aaaAzure IoT Hub de dispositivo para nuvem | Microsoft Docs"
description: "Guia do desenvolvedor - orientações sobre quando as mensagens de dispositivo para nuvem toouse, propriedades relatadas ou arquivo carrega para comunicações de nuvem para dispositivo."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 979136db-c92d-4288-870c-f305e8777bdd
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: elioda
ms.openlocfilehash: 2caefc4f59e16ad28b0d8cf4b3bb627b4cba803b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="device-to-cloud-communications-guidance"></a>Diretrizes de comunicações do dispositivo para a nuvem
Ao enviar informações de saudação dispositivo aplicativo toohello solução back-end, o IoT Hub expõe três opções:

* [Mensagens do dispositivo para a nuvem ][lnk-d2c], para telemetria de série de tempo e alertas.
* [Relatado propriedades] [ lnk-twins] para relatar informações de estado do dispositivo, como recursos disponíveis, condições ou estado de saudação de fluxos de trabalho de longa execução. Por exemplo, configuração e atualizações de software.
* [Carregamentos de arquivos] [ lnk-fileupload] para mídia de arquivos e lotes grandes telemetria carregados pelos dispositivos conectados de maneira intermitente ou compactados toosave largura de banda.

Aqui está uma comparação detalhada das Olá várias opções de comunicação do dispositivo para a nuvem.

|  | Mensagens do dispositivo para a nuvem | Propriedades reportadas | Carregamentos de arquivos |
| ---- | ------- | ---------- | ---- |
| Cenário | Série de tempo de telemetria e alertas. Por exemplo, os lotes de dados de sensor de 256 KB enviados a cada 5 minutos. | Recursos disponíveis e condições. Por exemplo, Olá atual dispositivo modo de conectividade, como o celular ou Wi-Fi. Sincronização dos fluxos de trabalho de longa duração, como atualizações de software e configuração. | Arquivos de mídia. Lotes grandes de telemetria (geralmente compactados). |
| Armazenamento e recuperação | Armazenados temporariamente pelo IoT Hub, backup too7 dias. Somente leitura sequencial. | Armazenados pelo IoT Hub em duas de dispositivo de saudação. Recuperáveis usando Olá [linguagem de consulta de IoT Hub][lnk-query]. | Armazenados na conta de Armazenamento do Azure fornecida pelo usuário. |
| Tamanho | As mensagens de too256 KB. | O tamanho máximo relatado das propriedades é de 8 KB. | Tamanho máximo de arquivo com suporte pelo Armazenamento de Blobs do Azure. |
| Frequência | Alta. Para saber mais, confira [Limites do Hub IoT][lnk-quotas]. | Média. Para saber mais, confira [Limites do Hub IoT][lnk-quotas]. | Baixa. Para saber mais, confira [Limites do Hub IoT][lnk-quotas]. |
| Protocolo | Disponível em todos os protocolos. | Disponível atualmente somente ao usar MQTT. | Disponíveis ao usar qualquer protocolo, mas requer HTTP no dispositivo de saudação. |

É possível que um aplicativo requer tooboth enviar informações como uma série de tempo de telemetria ou alerta e também toomake disponível em duas de dispositivo de saudação. Nesse cenário, você pode escolher de saudação as opções a seguir:

* Olá dispositivo aplicativo envia uma mensagem de dispositivo para nuvem e relata uma alteração de propriedade.
* back-end de solução Olá pode armazenar informações de Olá nas marcas do duas do hello dispositivo quando ele recebe a mensagem de saudação.

Como mensagens de dispositivo para nuvem permitem uma maior taxa de transferência que atualizações do dispositivo duas, às vezes é desejável tooavoid atualização duas do hello dispositivo para todas as mensagens de dispositivo para nuvem.


[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-fileupload]: iot-hub-devguide-file-upload.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
