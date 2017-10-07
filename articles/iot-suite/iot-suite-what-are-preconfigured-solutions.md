---
title: "soluções pré-configuradas de aaaAzure IoT | Microsoft Docs"
description: "Uma descrição do hello Azure IoT pré-configurado soluções e sua arquitetura com recursos de tooadditional links."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 59009f37-9ba0-4e17-a189-7ea354a858a2
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: bd059d08ab458fdb0b6f49b3ac469db930dab09e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-hello-azure-iot-suite-preconfigured-solutions"></a>Quais são as soluções do Azure IoT Suite pré-configurado Olá?

soluções do Azure IoT Suite pré-configurado Olá são implementações dos padrões de solução de IoT comuns que você pode implantar tooAzure usando sua assinatura. Você pode usar soluções de saudação pré-configurados:

* Como ponto de partida para suas próprias soluções de IoT.
* toolearn sobre padrões comuns no desenvolvimento e design de solução de IoT.

Cada solução pré-configurada é uma implementação completa, de ponta a ponta que usa simulados telemetria de toogenerate de dispositivos.

Você pode baixar toocustomize de código fonte completo hello e estender Olá solução toomeet seus requisitos específicos de IoT.

> [!NOTE]
> soluções pré-configuradas de toodeploy de saudação, visite [Microsoft Azure IoT Suite][lnk-azureiotsuite]. artigo Olá [começar com soluções de IoT pré-configurado Olá] [ lnk-getstarted-preconfigured] fornece mais informações sobre como toodeploy e execute uma das Olá soluções.

Olá tabela a seguir mostra como as soluções de saudação mapeiam toospecific IoT recursos:

| Solução | Ingestão de dados | Identidade do dispositivo | Gerenciamento de dispositivos | Comando e controle | Regras e ações | Análise preditiva |
| --- | --- | --- | --- | --- | --- | --- |
| [Monitoramento remoto][lnk-getstarted-preconfigured] |Sim |Sim |Sim |Sim |Sim |- |
| [Manutenção preditiva][lnk-predictive-maintenance] |Sim |Sim |- |Sim |Sim |Sim |
| [Fábrica conectada][lnk-getstarted-factory] |Sim |Sim |Sim |Sim |Sim |- |

* *Ingestão de dados*: entrada de dados em nuvem de toohello de escala.
* *Identidade do dispositivo*: gerenciar identidades de dispositivo exclusivo e controlar a solução de toohello de acesso do dispositivo.
* *Gerenciamento de dispositivo*: gerenciar metadados de dispositivo e executar operações como atualizações de firmware e reinicializações do dispositivo.
* *Comando e controle*: toocause Olá dispositivo tootake uma ação, enviar o dispositivo de tooa mensagens da nuvem de saudação.
* *Regras e ações*: tooact em dados específicos do dispositivo para nuvem, back-end de solução Olá usa regras.
* *Análise preditiva*: back-end de solução Olá analisa dados de dispositivo para nuvem toopredict quando ações específicas devem ocorrer. Por exemplo, analisando aeronave mecanismo telemetria toodetermine quando manutenção mecanismo está vencida.

## <a name="remote-monitoring-preconfigured-solution-overview"></a>Visão geral da solução pré-configurada de Monitoramento Remoto

Escolhemos toodiscuss Olá solução pré-configurada monitoramento remoto neste artigo porque ele ilustra vários elementos comuns de design que Olá outro compartilhamento de soluções.

Olá diagrama a seguir ilustra os principais elementos do hello da saudação remota de solução de monitoramento. Olá seções a seguir fornecem mais informações sobre esses elementos.

![Arquitetura da solução pré-configurada de monitoramento remoto][img-remote-monitoring-arch]

## <a name="devices"></a>Dispositivos

Quando você implanta a solução pré-configurada de monitoramento remoto de saudação, quatro dispositivos simulados são pré-provisionado na solução de saudação que simula um dispositivo de resfriamento. Esses dispositivos simulados têm um modelo interno de temperatura interna e de umidade que emite a telemetria. Esses dispositivos simulados estão incluídos para:

- Ilustra o fluxo de ponta a ponta de saudação de dados por meio da solução de saudação.
- Fornecer uma fonte conveniente de telemetria.
- Forneça um destino para comandos ou métodos se você for um desenvolvedor de back-end usando a solução hello como ponto de partida para uma implementação personalizada.

dispositivos Olá simulado na solução Olá podem responder toohello comunicações de nuvem para dispositivo a seguir:

- *Métodos ([direto métodos][lnk-direct-methods])*: um método de comunicação bidirecional em que um dispositivo conectado é esperado toorespond imediatamente.
- *Comandos (mensagens de nuvem para dispositivo)*: um método de comunicação unidirecional em que um dispositivo recupera o comando saudação de uma fila durável.

Para uma comparação dessas diferentes abordagens, consulte [Orientação sobre comunicações da nuvem para o dispositivo][lnk-c2d-guidance].

Quando um dispositivo conectado pela primeira tooIoT Hub na solução Olá pré-configurado, ele envia um hub de toohello de mensagem de informações de dispositivo. Esta mensagem enumera métodos Olá dispositivo Olá pode responder a. Olá solução pré-configurada de monitoramento remoto, dispositivos simulados suportam a estes métodos:

* *Iniciar a atualização do Firmware*: esse método inicia uma tarefa assíncrona em Olá dispositivo tooperform uma atualização de firmware. tarefa assíncrona Olá usa propriedades relatado toodeliver status atualizações toohello solução painel de controle.
* *Reinicialize*: este método faz Olá simulado dispositivo tooreboot.
* *FactoryReset*: este método dispara uma redefinição de fábrica no dispositivo simulado hello.

Quando um dispositivo conectado pela primeira tooIoT Hub na solução Olá pré-configurado, ele envia um hub de toohello de mensagem de informações de dispositivo. Esta mensagem enumera os comandos de Olá dispositivo Olá pode responder. Olá solução pré-configurada de monitoramento remoto, dispositivos simulados suportam a esses comandos:

* *Dispositivo de ping*: dispositivo Olá responde toothis comando com uma confirmação. Esse comando é útil para verificar o que dispositivo Olá ainda está ativo e escuta.
* *Iniciar telemetria*: instrui Olá dispositivo toostart enviar telemetria.
* *Parar telemetria*: instrui Olá dispositivo toostop enviar telemetria.
* *Alterar ponto definido temperatura*: controles Olá temperatura simulada telemetria valores hello dispositivo envia. Esse comando é útil para testar a lógica de back-end.
* *Telemetria de diagnóstico*: controla se o dispositivo Olá deve enviar temperatura externa hello como telemetria.
* *Alterar estado do dispositivo*: define a propriedade metadados de estado de dispositivo de saudação que Olá relatórios de dispositivo. Esse comando é útil para testar a lógica de back-end.

Você pode adicionar mais solução toohello dispositivos simulada que emitem Olá mesmo telemetria e responder toohello mesmos métodos e comandos.

Além disso tooresponding toocommands e os métodos, Olá solução usa [twins dispositivo][lnk-device-twin]. Dispositivos usam dispositivo twins tooreport propriedade valores toohello solução back-end. Painel de solução de saudação usa valores de propriedade do dispositivo twins tooset toonew desejado em dispositivos. Por exemplo, durante a relatórios de dispositivo Olá simulada do processo de atualização de firmware Olá status Olá Olá atualizar usando propriedades relatadas.

## <a name="iot-hub"></a>Hub IoT

Nesta solução pré-configurada, hello instância de IoT Hub corresponde toohello *Gateway de nuvem* em um típico [arquitetura de solução de IoT][lnk-what-is-azure-iot].

Um hub IoT recebe a telemetria de dispositivos de saudação em um único ponto de extremidade. Um hub IoT também mantém os pontos de extremidade específico do dispositivo em que cada dispositivo pode recuperar os comandos de saudação que são enviados tooit.

hub IoT de saudação disponibiliza telemetria Olá recebido por meio de telemetria do lado do serviço Olá ler o ponto de extremidade.

capacidade de gerenciamento de dispositivo de saudação do IoT Hub permite que você toomanage as propriedades de dispositivo de saudação solução portal e o agendamento de trabalhos que executam operações como:

- Reinicialização de dispositivos
- Alterar estados do dispositivo
- Atualizações de firmware

## <a name="azure-stream-analytics"></a>Stream Analytics do Azure

Olá solução pré-configurada usa três [Azure Stream Analytics] [ lnk-asa] fluxo de telemetria de saudação (ASA) trabalhos toofilter de dispositivos de saudação:

* *Trabalho de DeviceInfo* -saídas dados tooan hub de eventos que roteia do registro de dispositivo solução de toohello mensagens específicas do registro do dispositivo. Esse registro de dispositivo é um banco de dados do BD Cosmos do Azure. Essas mensagens são enviadas quando um dispositivo se conecta pela primeira vez ou em resposta tooa **alterar o estado do dispositivo** comando.
* *Trabalho de telemetria* - envia todos os armazenamento de blob de tooAzure brutos de telemetria para armazenamento frio e calcula agregações de telemetria que exibem no painel de solução de saudação.
* *Trabalho de regras* - filtros Olá fluxo de telemetria para valores que excedem os limites de regra e saídas Olá hub de eventos de tooan de dados. Quando uma regra é acionado, modo de exibição de painel do portal de solução Olá exibe esse evento como uma nova linha na tabela de histórico de alarme hello. Essas regras também podem disparar uma ação com base nas configurações de saudação definidas no hello **regras** e **ações** modos de exibição no portal de solução de saudação.

Nesta solução pré-configurada, Olá ASA trabalhos fazem parte do toohello **back-end de solução IoT** em um típico [arquitetura de solução de IoT][lnk-what-is-azure-iot].

## <a name="event-processor"></a>Processador de eventos

Nesta solução pré-configurada, o processador de eventos Olá faz parte do hello **back-end de solução IoT** em um típico [arquitetura de solução de IoT][lnk-what-is-azure-iot].

Olá **DeviceInfo** e **regras** trabalhos ASA enviar seus hubs de tooEvent de saída para a entrega de serviços de back-end tooother. Olá solução usa um [EventProcessorHost] [ lnk-event-processor] instância, em execução em um [WebJob][lnk-web-job], mensagens de saudação tooread dos hubs de eventos. Olá **EventProcessorHost** usa:
- Olá **DeviceInfo** tooupdate Olá dispositivo dados no banco de dados de banco de dados do Cosmos hello.
- Olá **regras** dados tooinvoke Olá lógica aplicativo e atualização Olá exibe alertas no portal de solução de saudação.

## <a name="device-identity-registry-device-twin-and-cosmos-db"></a>Registro de identidade do dispositivo, dispositivo gêmeo e Cosmos DB

Cada Hub IoT inclui um [registro de identidade do dispositivo][lnk-identity-registry] que armazena as chaves do dispositivo. IoT Hub usa essas informações autenticar dispositivos – um dispositivo deve ser registrado e tiver uma chave válida antes que ele possa se conectar toohello hub.

Um [duas dispositivo] [ lnk-device-twin] é um documento JSON gerenciado pelo Olá IoT Hub. Um dispositivo gêmeo para um dispositivo contém:

- Propriedades relatadas enviadas pelo hub de toohello dispositivo hello. Você pode exibir essas propriedades no portal de solução de saudação.
- Propriedades desejadas que você deseja que o dispositivo de toohello toosend. Você pode definir essas propriedades no portal de solução de saudação.
- Marcas que existem somente em duas de dispositivo hello e não no dispositivo de saudação. Você pode usar essas listas de toofilter marcas de dispositivos no portal de solução de saudação.

Esta solução usa metadados do dispositivo do dispositivo twins toomanage. solução de saudação também usa dados de dispositivos adicionais de solução específica de toostore um Cosmos DB banco de dados como Olá comandos suportados por cada dispositivo e hello histórico de comandos.

solução de saudação também deve manter informações de Olá no registro de identidade de dispositivo Olá sincronizado com o conteúdo de saudação do banco de dados do banco de dados do Cosmos hello. Olá **EventProcessorHost** usa Olá dados de **DeviceInfo** toomanage sincronização de saudação do trabalho do stream analytics.

## <a name="solution-portal"></a>Portal de solução

![portal da solução][img-dashboard]

portal de solução de saudação é uma interface de usuário baseada na web que é implantado toohello nuvem como parte da solução Olá pré-configurado. Ele permite que você:

* Exiba o histórico de telemetria e de alarmes em um painel.
* Provisione novos dispositivos.
* Gerencie e monitore dispositivos.
* Envie comandos toospecific dispositivos.
* Invoque métodos em dispositivos específicos.
* Gerencie regras e ações.
* Agendar trabalhos toorun em um ou mais dispositivos.

Nesta solução pré-configurada, o portal de solução Olá faz parte do hello **back-end de solução IoT** e é parte da saudação **conectividade de processamento e de negócios** em Olá típico [solução de IoT arquitetura][lnk-what-is-azure-iot].

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre as arquiteturas de solução de IoT, confira [Serviços de IoT do Microsoft Azure: arquitetura de referência][lnk-refarch].

Agora você sabe que uma solução pré-configurada for, você pode começar Implantando Olá *monitoramento remoto* pré-configurado solução: [começar com soluções de saudação pré-configurado] [ lnk-getstarted-preconfigured].

[img-remote-monitoring-arch]: ./media/iot-suite-what-are-preconfigured-solutions/remote-monitoring-arch1.png
[img-dashboard]: ./media/iot-suite-what-are-preconfigured-solutions/dashboard.png
[lnk-what-is-azure-iot]: iot-suite-what-is-azure-iot.md
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-event-processor]: ../event-hubs/event-hubs-programming-guide.md#event-processor-host
[lnk-web-job]: ../app-service-web/web-sites-create-web-jobs.md
[lnk-identity-registry]: ../iot-hub/iot-hub-devguide-identity-registry.md
[lnk-predictive-maintenance]: iot-suite-predictive-overview.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-refarch]: http://download.microsoft.com/download/A/4/D/A4DAD253-BC21-41D3-B9D9-87D2AE6F0719/Microsoft_Azure_IoT_Reference_Architecture.pdf
[lnk-getstarted-preconfigured]: iot-suite-getstarted-preconfigured-solutions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-device-twin]: ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-getstarted-factory]: iot-suite-connected-factory-overview.md
