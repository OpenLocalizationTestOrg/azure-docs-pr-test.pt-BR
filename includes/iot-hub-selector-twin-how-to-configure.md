> [!div class="op_single_selector"]
> * [Node.js](../articles/iot-hub/iot-hub-node-node-twin-how-to-configure.md)
> * [C#/Node.js](../articles/iot-hub/iot-hub-csharp-node-twin-how-to-configure.md)
> * [C#](../articles/iot-hub/iot-hub-csharp-csharp-twin-how-to-configure.md)
> 
> 

## <a name="introduction"></a>Introdução

Em [começar com twins de dispositivo do IoT Hub][lnk-twin-tutorial], você aprendeu como tooset metadados do dispositivo de volta a sua solução final usando *marcas*, reporte as condições de dispositivo de um aplicativo de dispositivo usando *relatado propriedades*e consultar essas informações usando uma linguagem SQL.

Neste tutorial, você aprenderá como toouse Olá do duas do dispositivo Olá *propriedades desejadas* juntamente com *relatado propriedades*, tooremotely configurar aplicativos de dispositivo. Mais especificamente, este tutorial mostra como uma duas de dispositivo relatado e propriedades desejadas habilite uma configuração de várias etapa de um aplicativo de dispositivo e fornecem Olá visibilidade toohello solução back-end de status Olá dessa operação em todos os dispositivos. Você pode encontrar mais informações sobre a função hello das configurações de dispositivo em [visão geral do gerenciamento de dispositivos com o IoT Hub][lnk-dm-overview].

Em um nível alto, usar twins dispositivo habilita Olá solução back-end toospecify Olá desejado configuração para dispositivos Olá gerenciado, em vez de enviar comandos específicos. Isso coloca o dispositivo Olá responsável por configurar Olá melhor maneira tooupdate sua configuração (muito importante em cenários de IoT onde as condições de dispositivo específico afetam Olá capacidade tooimmediately executadas comandos específicos), ao relatar continuamente toohello solução novamente terminar o estado atual da saudação e possíveis condições de erro do processo de atualização de saudação. Esse padrão é toohello fundamental para o gerenciamento de grandes conjuntos de dispositivos, pois permite Olá solução back-end toohave visibilidade total do estado de saudação do processo de configuração de saudação em todos os dispositivos.

> [!NOTE]
> Em cenários em que os dispositivos são controlados de forma mais interativa (ativar um ventilador por meio de um aplicativo controlado pelo usuário), considere usar [métodos diretos][lnk-methods].
> 
> 

Neste tutorial, alterações de back-end de solução de saudação configuração de telemetria de saudação de um dispositivo de destino e, como resultado que, o aplicativo de dispositivo Olá segue um processo de várias etapas de tooapply uma configuração de atualização (por exemplo, que requerem a reinicialização de módulo de software, que esse tutorial simula com um atraso simple).

back-end de solução Olá armazena a configuração de saudação nas propriedades desejada do duas do dispositivo Olá Olá maneira a seguir:

        {
            ...
            "properties": {
                ...
                "desired": {
                    "telemetryConfig": {
                        "configId": "{id of hello configuration}",
                        "sendFrequency": "{config}"
                    }
                }
                ...
            }
            ...
        }

> [!NOTE]
> Como as configurações podem ser objetos complexos, elas geralmente são atribuídas ids exclusivas (hashes ou [GUIDs][lnk-guid]) toosimplify seus comparações.
> 
> 

aplicativo de dispositivo Hello relatórios sua configuração atual de espelhamento propriedade Olá desejado **telemetryConfig** no hello reportada propriedades:

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of hello current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Success",
                    }
                }
                ...
            }
        }

Observe como Olá relatadas **telemetryConfig** tem uma propriedade adicional **status**, usado tooreport estado de saudação do processo de atualização de configuração de saudação.

Quando uma nova configuração desejada é recebida, aplicativo de dispositivo Olá relata uma configuração pendente alterando Olá informações:

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of hello current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Pending",
                        "pendingConfig": {
                            "changeId": "{id of hello pending configuration}",
                            "sendFrequency": "{pending configuration}"
                        }
                    }
                }
                ...
            }
        }

Em seguida, posteriormente, Olá dispositivo aplicativo será relatar Olá êxito ou falha dessa operação atualizando Olá acima de propriedade.
Observe como solução Olá back-end é a capacidade, a qualquer momento, o status de saudação tooquery do processo de configuração de saudação em todos os dispositivos de saudação.

Este tutorial mostra como:

* Criar um aplicativo de dispositivo simulado que recebe atualizações de configuração de back-end de solução hello e relatórios de várias atualizações como *relatado propriedades* na configuração de saudação o processo de atualização.
* Crie um aplicativo de back-end que atualizações Olá configuração desejada de um dispositivo e, em seguida, consultas Olá o processo de atualização de configuração.

<!-- links -->

[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: ../articles/iot-hub/iot-hub-device-management-overview.md
[lnk-twin-tutorial]: ../articles/iot-hub/iot-hub-node-node-twin-getstarted.md
[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier
