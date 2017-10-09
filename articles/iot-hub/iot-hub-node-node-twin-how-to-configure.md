---
title: "Propriedades de duas aaaUse Azure IoT Hub dispositivo (nó) | Microsoft Docs"
description: "Como twins dispositivo do Azure IoT Hub toouse tooconfigure dispositivos. Você pode usar hello Azure IoT SDKs para Node. js tooimplement um aplicativo de dispositivo simulado e um aplicativo de serviço que modifica uma configuração de dispositivo usando duas um dispositivo."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: d0bcec50-26e6-40f0-8096-733b2f3071ec
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/13/2016
ms.author: elioda
ms.openlocfilehash: 7ebfe2dfa0876bf04fdbaceae55db76456523e8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices-node"></a>Use desejado propriedades tooconfigure dispositivos (nó)
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

No final de saudação deste tutorial, você terá dois aplicativos de console Node. js:

* **SimulateDeviceConfiguration.js**, um aplicativo de dispositivo simulado que aguarda uma atualização de configurações desejadas e relata o status de saudação de um processo de atualização de configuração simulada.
* **SetDesiredConfigurationAndQuery.js**, um aplicativo de back-end node. js, que define a saudação da configuração em um dispositivo desejado e consultas Olá o processo de atualização de configuração.

> [!NOTE]
> artigo Olá [SDKs do Azure IoT] [ lnk-hub-sdks] fornece informações sobre Olá SDKs IoT do Azure que você pode usar toobuild aplicativos de dispositivo e de back-end.
> 
> 

toocomplete este tutorial, você precisa seguir hello:

* Node.js versão 0.10.x ou posterior.
* Uma conta ativa do Azure. (Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)

Se você seguiu Olá [Introdução ao twins dispositivo] [ lnk-twin-tutorial] tutorial, você já tem um hub IoT e uma identidade de dispositivo chamado **myDeviceId**; e você poderá ignorar toohello [ Criar aplicativo de dispositivo simulado Olá] [ lnk-how-to-configure-createapp] seção.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-simulated-device-app"></a>Criar aplicativo de dispositivo simulado Olá
Nesta seção, você cria um aplicativo de console Node. js que conecta o hub tooyour como **myDeviceId**, aguarda até que uma atualização de configurações desejadas e, em seguida, relatórios atualizações no processo de atualização de configuração Olá simulada.

1. Crie uma nova pasta vazia denominada **simulatedeviceconfiguration**. Em Olá **simulatedeviceconfiguration** pasta, crie um novo arquivo Package. JSON usando Olá comando no prompt de comando a seguir. Aceite todos os padrões de saudação:
   
    ```
    npm init
    ```
2. O prompt de comando no hello **simulatedeviceconfiguration** pasta, execute Olá Olá de tooinstall de comando a seguir **dispositivo de iot do azure**, e **azure iot dispositivo-mqtt**pacote:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Usando um editor de texto, crie um novo **SimulateDeviceConfiguration.js** arquivo hello **simulatedeviceconfiguration** pasta.
4. Adicionar Olá toohello de código a seguir **SimulateDeviceConfiguration.js** de arquivo e substituir Olá **{string de conexão do dispositivo}** espaço reservado com a cadeia de conexão do dispositivo Olá copiadas quando você criado Olá **myDeviceId** identidade do dispositivo:
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
            if (err) {
                console.error('could not open IotHub client');
            } else {
                client.getTwin(function(err, twin) {
                    if (err) {
                        console.error('could not get twin');
                    } else {
                        console.log('retrieved device twin');
                        twin.properties.reported.telemetryConfig = {
                            configId: "0",
                            sendFrequency: "24h"
                        }
                        twin.on('properties.desired', function(desiredChange) {
                            console.log("received change: "+JSON.stringify(desiredChange));
                            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
                            if (desiredChange.telemetryConfig &&desiredChange.telemetryConfig.configId !== currentTelemetryConfig.configId) {
                                initConfigChange(twin);
                            }
                        });
                    }
                });
            }
        });
   
    Olá **cliente** objeto expõe toointeract necessária do todos os métodos de saudação com twins de dispositivo do dispositivo hello. Olá código anterior, depois que ele inicializa Olá **cliente** objeto recupera Olá duas de dispositivo para **myDeviceId**e anexa um manipulador de atualização de saudação em propriedades desejadas. manipulador de saudação verifica que há é uma solicitação de alteração de configuração real comparando Olá configIds, em seguida, invoca um método que inicia a alteração de configuração de saudação.
   
    Observe que, para bem Olá de simplicidade, código anterior Olá usa um padrão embutido para a configuração inicial de saudação. Um aplicativo real provavelmente carregaria essa configuração de um armazenamento local.
   
   > [!IMPORTANT]
   > Eventos de alteração de propriedade desejados sempre são emitidos uma vez na conexão do dispositivo, certifique-se de toocheck que há uma alteração real no hello propriedades desejadas antes de executar qualquer ação.
   > 
   > 
5. Adicionar Olá seguintes métodos antes de saudação `client.open()` invocação:
   
        var initConfigChange = function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.pendingConfig = twin.properties.desired.telemetryConfig;
            currentTelemetryConfig.status = "Pending";
   
            var patch = {
            telemetryConfig: currentTelemetryConfig
            };
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.log('Could not report properties');
                } else {
                    console.log('Reported pending config change: ' + JSON.stringify(patch));
                    setTimeout(function() {completeConfigChange(twin);}, 60000);
                }
            });
        }
   
        var completeConfigChange =  function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.configId = currentTelemetryConfig.pendingConfig.configId;
            currentTelemetryConfig.sendFrequency = currentTelemetryConfig.pendingConfig.sendFrequency;
            currentTelemetryConfig.status = "Success";
            delete currentTelemetryConfig.pendingConfig;
   
            var patch = {
                telemetryConfig: currentTelemetryConfig
            };
            patch.telemetryConfig.pendingConfig = null;
   
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.error('Error reporting properties: ' + err);
                } else {
                    console.log('Reported completed config change: ' + JSON.stringify(patch));
                }
            });
        };
   
    Olá **initConfigChange** método atualizações relatado propriedades no objeto de duas Olá dispositivo local com a solicitação de atualização de configuração hello e conjuntos de Olá status muito**pendente**, e em seguida, as atualizações Olá dispositivo duas no serviço de saudação. Depois de atualizar com êxito duas de dispositivo hello, ele simula um processo de execução demorada que termina em execução de saudação do **completeConfigChange**. Duas de dispositivo local este método atualizações saudação do relatado propriedades definindo o status de saudação muito**êxito** e removendo Olá **pendingConfig** objeto. Em seguida, atualiza as duas de dispositivo Olá no serviço de saudação.
   
    Observe que, a largura de banda toosave relatadas propriedades serão atualizadas, especificando somente o hello propriedades toobe modificado (denominado **patch** em Olá acima código), em vez de substituir todo o documento hello.
   
   > [!NOTE]
   > Este tutorial não simula nenhum comportamento para atualizações de configuração simultâneas. Alguns processos de atualização de configuração podem ser capaz de tooaccommodate alterações de configuração de destino durante a execução de atualização hello, outros podem ter tooqueue e outros podem rejeitá-las com uma condição de erro. Verifique tooconsider se Olá o comportamento desejado para o processo de configuração específica e adicionar lógica apropriada Olá antes de iniciar a alteração de configuração de saudação.
   > 
   > 
6. Execute o aplicativo de dispositivo hello:
   
        node SimulateDeviceConfiguration.js
   
    Você verá uma mensagem de saudação `retrieved device twin`. Lembre-Olá aplicativo em execução.

## <a name="create-hello-service-app"></a>Criar aplicativo de serviço Olá
Nesta seção, você criará um aplicativo de console Node. js que Olá atualizações *propriedades desejadas* em Olá dispositivo duas associada **myDeviceId** com um novo objeto de configuração de telemetria. Ele, em seguida, consulta twins de dispositivo Olá armazenadas no hub IoT de saudação e mostra diferença Olá entre hello desejado e relatado configurações de dispositivo de saudação.

1. Crie uma nova pasta vazia denominada **setdesiredandqueryapp**. Em Olá **setdesiredandqueryapp** pasta, crie um novo arquivo Package. JSON usando Olá comando no prompt de comando a seguir. Aceite todos os padrões de saudação:
   
    ```
    npm init
    ```
2. O prompt de comando no hello **setdesiredandqueryapp** pasta, execute Olá Olá de tooinstall de comando a seguir **hub IOT do azure** pacote:
   
    ```
    npm install azure-iothub node-uuid --save
    ```
3. Usando um editor de texto, crie um novo **SetDesiredAndQuery.js** arquivo hello **addtagsandqueryapp** pasta.
4. Adicionar Olá toohello de código a seguir **SetDesiredAndQuery.js** de arquivo e substituir Olá **{string de conexão de hub iot}** espaço reservado com hello cadeia de caracteres de conexão de IoT Hub copiadas quando você criar o hub :
   
        'use strict';
        var iothub = require('azure-iothub');
        var uuid = require('node-uuid');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var newConfigId = uuid.v4();
                var newFrequency = process.argv[2] || "5m";
                var patch = {
                    properties: {
                        desired: {
                            telemetryConfig: {
                                configId: newConfigId,
                                sendFrequency: newFrequency
                            }
                        }
                    }
                }
                twin.update(patch, function(err) {
                    if (err) {
                        console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                    } else {
                        console.log(twin.deviceId + ' twin updated successfully');
                    }
                });
                setInterval(queryTwins, 10000);
            }
        });

    Olá **registro** objeto expõe toointeract necessária do todos os métodos de saudação com twins de dispositivo do serviço de saudação. Olá código anterior, depois que ele inicializa Olá **registro** objeto recupera Olá duas de dispositivo para **myDeviceId**e atualiza as propriedades desejadas com um novo objeto de configuração de telemetria. Depois disso, ele chama Olá **queryTwins** função evento 10 segundos.

    > [!IMPORTANT]
    > Esse aplicativo consulta o Hub IoT a cada 10 segundos para fins ilustrativos. Use consultas toogenerate voltadas para o usuário relatórios em vários dispositivos e não toodetect alterações. Se sua solução exigir notificações em tempo real de eventos de dispositivo, use [notificações gêmeas][lnk-twin-notifications].
    > 
    >.

1. Adicionar Olá seguindo o direito de código antes de saudação `registry.getDeviceTwin()` saudação do invocação tooimplement **queryTwins** função:
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log();
                    results.forEach(function(twin) {
                        var desiredConfig = twin.properties.desired.telemetryConfig;
                        var reportedConfig = twin.properties.reported.telemetryConfig;
                        console.log("Config report for: " + twin.deviceId);
                        console.log("Desired: ");
                        console.log(JSON.stringify(desiredConfig, null, 2));
                        console.log("Reported: ");
                        console.log(JSON.stringify(reportedConfig, null, 2));
                    });
                }
            });
        };
   
    consultas de código anteriores Olá Olá twins dispositivo armazenadas no hub IoT de saudação e imprime Olá desejado e relatado configurações de telemetria. Consulte toohello [linguagem de consulta de IoT Hub] [ lnk-query] toolearn como toogenerate rich relatórios em todos os seus dispositivos.
2. Com **SimulateDeviceConfiguration.js** em execução, execute o aplicativo hello com:
   
        node SetDesiredAndQuery.js 5m
   
    Você deve ver a configuração relatado Olá alterar de **êxito** muito**pendente** muito**êxito** novamente com um novo ativo de saudação enviar frequência de cinco minutos, em vez de 24 horas.
   
   > [!IMPORTANT]
   > Há um atraso de backup tooa minutos entre a operação de relatório de dispositivo hello e resultado da consulta hello. Isso é tooenable Olá consulta infraestrutura toowork em escala muito alta. modos de exibição consistente de duas um único dispositivo tooretrieve usam Olá **getDeviceTwin** método hello **registro** classe.
   > 
   > 

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você definir uma configuração desejada como *propriedades desejadas* de um aplicativo de back-end e escreveu um toodetect de aplicativo do dispositivo simulado que são alterados e simular um processo de atualização de várias etapas relatar seu status como  *relatado propriedades* toohello duas de dispositivo.

Saudação de uso toolearn de recursos a seguir como a:

* Enviar telemetria de dispositivos com hello [começar com o IoT Hub] [ lnk-iothub-getstarted] tutorial,
* agendar ou executar operações em grandes conjuntos de dispositivos Consulte Olá [agenda e trabalhos de difusão] [ lnk-schedule-jobs] tutorial.
* controlar dispositivos interativamente (como ativar um ventilador de um aplicativo controlado pelo usuário), com hello [usar métodos diretos] [ lnk-methods-tutorial] tutorial.

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-twin-notifications]: iot-hub-devguide-device-twins.md#back-end-operations
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: iot-hub-device-management-overview.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-schedule-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md

[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

[lnk-how-to-configure-createapp]: iot-hub-node-node-twin-how-to-configure.md#create-the-simulated-device-app
