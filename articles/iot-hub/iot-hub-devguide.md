---
title: Guia de aaaDeveloper do Azure IoT Hub | Microsoft Docs
description: "Guia do desenvolvedor do Azure IoT Hub Olá inclui discussões de pontos de extremidade, segurança, registro de identidade hello, gerenciamento de dispositivos, métodos diretos, twins do dispositivo, carregamentos de arquivos, trabalhos, Olá linguagem de consulta de IoT Hub e mensagens."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: d534ff9d-2de5-4995-bb2d-84a02693cb2e
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: 2d3f18399e4cef6f9c4850a5caeb170a2d091a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-developer-guide"></a>Guia do desenvolvedor do Hub IoT do Azure

O Hub IoT do Azure é um serviço totalmente gerenciado que ajuda a permitir comunicações bidirecionais confiáveis e seguras entre milhões de dispositivos e um back-end de solução.

O Hub IoT do Azure oferece:

* Proteja as comunicações usando as credenciais de segurança e o controle de acesso por dispositivo.
* Várias opções de comunicação em larga escala do dispositivo para a nuvem e da nuvem para o dispositivo.
* Armazenamento que podem ser consultado com informações de estado por dispositivo e metadados.
* Conectividade do dispositivo fácil com bibliotecas de dispositivo para plataformas e idiomas mais populares de saudação.

Este guia do desenvolvedor de IoT Hub inclui Olá artigos a seguir:

* [Orientação de comunicação do dispositivo para a nuvem][lnk-d2c-guidance] ajuda você a escolher entre mensagens do dispositivo para a nuvem, propriedades reportadas do dispositivo gêmeo ou carregamento do arquivo.
* [Orientação de comunicação da nuvem para o dispositivo][lnk-c2d-guidance] ajuda você a escolher entre os métodos diretos, as propriedades desejadas do dispositivo gêmeo e as mensagens da nuvem para o dispositivo.
* [Dispositivo para nuvem e nuvem para dispositivo de mensagens com o IoT Hub] [ devguide-messaging] descreve Olá recursos de mensagens (dispositivo para nuvem e nuvem para dispositivo) que expõe IoT Hub.
  * [Enviar mensagens de dispositivo para nuvem tooIoT Hub][devguide-messages-d2c].
  * [Ler mensagens de dispositivo para a nuvem de ponto de extremidade internos Olá][devguide-builtin].
  * [Utilizar pontos de extremidade personalizados e regras de roteamento para mensagens de dispositivo para a nuvem][devguide-custom].
  * [Enviar mensagens de nuvem para o dispositivo do Hub IoT][devguide-messages-c2d].
  * [Criar e ler mensagens do Hub IoT][devguide-format].
* [Carregar arquivos de um dispositivo][devguide-upload] descreve como você pode carregar arquivos de um dispositivo. Olá também inclui informações sobre tópicos como Olá pode enviar o processo de carregamento de saudação notificações.
* [Gerenciar identidades do dispositivo no Hub IoT][devguide-identities] descreve as informações são armazenadas pelo registro de identidade de cada Hub IoT, e como elas podem ser acessadas e modificadas.
* [Controlar acesso tooIoT Hub] [ devguide-security] descreve Olá segurança modelo usado toogrant tooIoT Hub funcionalidade de acesso para dispositivos e componentes de nuvem. artigo de Olá inclui informações sobre como usar tokens e certificados x. 509 e detalhes de permissões de saudação, que você pode conceder.
* [Usar configurações e estado do dispositivo twins toosynchronize] [ devguide-device-twins] descreve Olá *duas dispositivo* conceito e hello como sincronizar um dispositivo com o seu dispositivo, ele expõe a funcionalidade duas. artigo de saudação inclui informações sobre dados de saudação armazenados em duas um dispositivo.
* [Invocar um método direto em um dispositivo] [ devguide-directmethods] descreve saudação do ciclo de vida de um método direto, obter informações sobre como tooinvoke métodos em um dispositivo de sua saudação de aplicativo e o identificador de back-end método direcionam no seu dispositivo.
* [Agendar trabalhos em vários dispositivos][devguide-jobs] descreve como você pode agendar trabalhos em vários dispositivos. Olá artigo descreve como toosubmit trabalhos que realizar tarefas como executar um método direto, atualizando um dispositivo usando duas um dispositivo. Ele também descreve como tooquery Olá status de um trabalho.
* [Referência - escolha um protocolo de comunicação] [ devguide-protocol] descreve protocolos de comunicação de saudação que IoT Hub dá suporte para a comunicação do dispositivo e listas Olá portas que devem ser abertas.
* [Referência - pontos de extremidade de IoT Hub] [ devguide-endpoints] descreve Olá vários pontos de extremidade que expõe a cada hub IoT para operações de tempo de execução e gerenciamento. Olá também descreve como você pode criar pontos de extremidade adicionais em seu hub IoT e toouse um tooyour de conectividade de dispositivos do campo gateway tooenable IoT Hub pontos de extremidade em cenários não padrão.
* [Referência - linguagem de consulta de IoT Hub para twins do dispositivo, trabalhos e roteamento de mensagens] [ devguide-query] descreve essa linguagem de consulta de IoT Hub que permite a você informações tooretrieve do seu hub sobre seus trabalhos e twins do dispositivo.
* [Referência - cotas e limitação] [ devguide-quotas] resume as cotas de saudação definidas na Olá serviço IoT Hub e hello comportamento, você pode esperar toosee ao exceder uma cota de limitação.
* [Referência - preços] [ devguide-pricing] fornece informações gerais sobre diferentes SKUs e preços para o IoT Hub e detalhes sobre como as mensagens de saudação várias funcionalidades de IoT Hub são monitoradas como pelo IoT Hub.
* [Referência - dispositivo e serviço SDKs] [ devguide-sdks] listas Olá SDKs do Azure IoT você pode usar toodevelop dispositivo e serviço de aplicativos que interagem com o hub IoT. artigo de saudação inclui documentação de API de tooonline links.
* [Referência - suporte de IoT Hub MQTT] [ devguide-mqtt] fornece informações detalhadas sobre como o IoT Hub oferece suporte a protocolo de MQTT saudação. artigo Olá descreve suporte Olá Olá MQTT protocolo interno toohello SDKs IoT do Azure e fornece informações sobre como usar o protocolo de MQTT saudação diretamente.
* [Glossário][devguide-glossary] uma lista de termos comuns relacionados ao Hub IoT.

[devguide-messaging]: iot-hub-devguide-messaging.md
[devguide-upload]: iot-hub-devguide-file-upload.md
[devguide-identities]: iot-hub-devguide-identity-registry.md
[devguide-security]: iot-hub-devguide-security.md
[devguide-device-twins]: iot-hub-devguide-device-twins.md
[devguide-directmethods]: iot-hub-devguide-direct-methods.md
[devguide-jobs]: iot-hub-devguide-jobs.md
[devguide-endpoints]: iot-hub-devguide-endpoints.md
[devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[devguide-query]: iot-hub-devguide-query-language.md
[devguide-sdks]: iot-hub-devguide-sdks.md
[devguide-mqtt]: iot-hub-mqtt-support.md
[devguide-glossary]: iot-hub-devguide-glossary.md
[devguide-pricing]: iot-hub-devguide-pricing.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[devguide-messages-d2c]: iot-hub-devguide-messages-d2c.md
[devguide-builtin]: iot-hub-devguide-messages-read-builtin.md
[devguide-custom]: iot-hub-devguide-messages-read-custom.md
[devguide-messages-c2d]: iot-hub-devguide-messages-c2d.md
[devguide-format]: iot-hub-devguide-messages-construct.md
[devguide-protocol]: iot-hub-devguide-protocols.md
