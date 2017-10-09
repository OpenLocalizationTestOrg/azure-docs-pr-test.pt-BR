---
title: "Telemetria dinâmico aaaUse | Microsoft Docs"
description: "Siga este tutorial toolearn como toouse a telemetria dinâmico com monitoramento remoto hello Azure IoT Suite pré-configurado solução."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 562799dc-06ea-4cdd-b822-80d1f70d2f09
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 06cb2a370b67b4950efdfa4c7d906ac92106f4a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-dynamic-telemetry-with-hello-remote-monitoring-preconfigured-solution"></a>Usar a telemetria dinâmica com hello solução pré-configurada de monitoramento remoto

Telemetria dinâmica permite que você toovisualize qualquer toohello telemetria enviada solução pré-configurada de monitoramento remoto. dispositivos Olá simulada que implantar solução Olá pré-configurado enviam telemetria de temperatura e umidade, que você pode visualizar no painel de saudação. Se você personalizar dispositivos simulados existentes, criar novos dispositivos simulados ou conectar dispositivos físicos toohello pré-configurado solução pode enviar outros valores de telemetria como temperatura externa hello, RPM ou windspeed. Em seguida, você pode visualizar essa telemetria adicional no painel de saudação.

Este tutorial usa um dispositivo simulado Node. js simples que você pode modificar facilmente tooexperiment com a telemetria dinâmica.

toocomplete neste tutorial, você precisará de:

* Uma assinatura ativa do Azure. Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação gratuita do Azure][lnk_free_trial].
* [Node.js][lnk-node] versão 0.12.x ou posterior.

Você pode concluir este tutorial em qualquer sistema operacional, como Windows ou Linux, onde é possível instalar o Node.js.

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

## <a name="add-a-telemetry-type"></a>Adicionar um tipo de telemetria

Olá próxima etapa é a telemetria de saudação tooreplace gerada pelo dispositivo simulado do Node. js Olá com um novo conjunto de valores:

1. Parar Olá Node. js dispositivo simulado digitando **Ctrl + C** no prompt de comando ou o shell.
2. No arquivo de remote_monitoring.js Olá, você pode ver os valores de base de dados de saudação de temperatura existente hello, umidade e telemetria temperatura externa. Adicione um valor de dados base para **rpm** da seguinte maneira:

    ```nodejs
    // Sensors data
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    var rpm = 200;
    ```

3. dispositivo simulado do Node. js Olá usa Olá **generateRandomIncrement** funcionar em Olá remote_monitoring.js arquivo tooadd toohello um incremento aleatório valores de base de dados. Tornar aleatório Olá **rpm** valor, adicionando uma linha de código após randomizations existente Olá da seguinte maneira:

    ```nodejs
    temperature += generateRandomIncrement();
    externalTemperature += generateRandomIncrement();
    humidity += generateRandomIncrement();
    rpm += generateRandomIncrement();
    ```

4. Adicione Olá novo rpm valor toohello JSON carga Olá dispositivo envia tooIoT Hub:

    ```nodejs
    var data = JSON.stringify({
      'DeviceID': deviceId,
      'Temperature': temperature,
      'Humidity': humidity,
      'ExternalTemperature': externalTemperature,
      'RPM': rpm
    });
    ```

5. Execute o dispositivo simulado do Node. js hello usando Olá comando a seguir:

    `node remote_monitoring.js`

6. Observe Olá novo RPM telemetria tipo que será exibido no gráfico de saudação no painel de saudação:

![Adicionar RPM toohello painel][image3]

> [!NOTE]
> Você pode precisar toodisable e, em seguida, habilitar o dispositivo Node. js Olá Olá **dispositivos** página na alteração de saudação do hello painel toosee imediatamente.

## <a name="customize-hello-dashboard-display"></a>Personalizar a exibição de painel Olá

Olá **informações do dispositivo** mensagem pode incluir metadados sobre a telemetria Olá dispositivo Olá pode enviar tooIoT Hub. Esses metadados podem especificar os tipos de telemetria Olá Olá dispositivo envia. Modificar Olá **deviceMetaData** valor Olá remote_monitoring.js arquivo tooinclude um **telemetria** definição após Olá **comandos** definição. Olá, trecho de código a seguir mostra Olá **comandos** definição (ser tooadd se um `,` após Olá **comandos** definição):

```nodejs
'Commands': [{
  'Name': 'SetTemperature',
  'Parameters': [{
    'Name': 'Temperature',
    'Type': 'double'
  }]
},
{
  'Name': 'SetHumidity',
  'Parameters': [{
    'Name': 'Humidity',
    'Type': 'double'
  }]
}],
'Telemetry': [{
  'Name': 'Temperature',
  'Type': 'double'
},
{
  'Name': 'Humidity',
  'Type': 'double'
},
{
  'Name': 'ExternalTemperature',
  'Type': 'double'
}]
```

> [!NOTE]
> solução de monitoramento remoto Olá usa uma definição de metadados de saudação do correspondência diferencia maiusculas de minúsculas toocompare com dados no fluxo de telemetria hello.


Adicionando um **telemetria** definição conforme mostrado na saudação anterior trecho de código não altera o comportamento de saudação do painel de saudação. No entanto, a saudação metadados também podem incluir um **DisplayName** toocustomize Olá exibição no painel de saudação do atributo. Saudação de atualização **telemetria** definição de metadados, como mostrado na Olá trecho de código a seguir:

```nodejs
'Telemetry': [
{
  'Name': 'Temperature',
  'Type': 'double',
  'DisplayName': 'Temperature (C*)'
},
{
  'Name': 'Humidity',
  'Type': 'double',
  'DisplayName': 'Humidity (relative)'
},
{
  'Name': 'ExternalTemperature',
  'Type': 'double',
  'DisplayName': 'Outdoor Temperature (C*)'
}
]
```

Olá seguinte captura de tela mostra como essa alteração modifica a legenda do gráfico de saudação no painel de saudação:

![Personalizar a legenda do gráfico Olá][image4]

> [!NOTE]
> Você pode precisar toodisable e, em seguida, habilitar o dispositivo Node. js Olá Olá **dispositivos** página na alteração de saudação do hello painel toosee imediatamente.

## <a name="filter-hello-telemetry-types"></a>Tipos de telemetria de saudação de filtro

Por padrão, o gráfico de saudação no painel de saudação mostra cada série de dados no fluxo de telemetria hello. Você pode usar o hello **informações do dispositivo** toosuppress metadados Olá exibição dos tipos de telemetria específica no gráfico de saudação. 

gráfico de saudação toomake Mostrar apenas telemetria de temperatura e umidade, omita **ExternalTemperature** de saudação **informações do dispositivo** **telemetria** metadados da seguinte maneira:

```nodejs
'Telemetry': [
{
  'Name': 'Temperature',
  'Type': 'double',
  'DisplayName': 'Temperature (C*)'
},
{
  'Name': 'Humidity',
  'Type': 'double',
  'DisplayName': 'Humidity (relative)'
},
//{
//  'Name': 'ExternalTemperature',
//  'Type': 'double',
//  'DisplayName': 'Outdoor Temperature (C*)'
//}
]
```

Olá **temperatura externa** não é mais exibido no gráfico de saudação:

![Telemetria de saudação de filtro no painel de saudação][image5]

Essa alteração afeta somente a exibição de gráfico de saudação. Olá **ExternalTemperature** valores de dados ainda são armazenados e disponibilizados para qualquer processamento de back-end.

> [!NOTE]
> Você pode precisar toodisable e, em seguida, habilitar o dispositivo Node. js Olá Olá **dispositivos** página na alteração de saudação do hello painel toosee imediatamente.

## <a name="handle-errors"></a>Tratar erros

Para um toodisplay de fluxo de dados no gráfico de saudação, seu **tipo** em Olá **informações do dispositivo** metadados devem corresponder o tipo de dados de saudação de valores de telemetria hello. Por exemplo, se hello metadados especificam que Olá **tipo** dos umidade estiver **int** e um **duplo** foi encontrado no fluxo de telemetria Olá então telemetria de umidade Olá não exiba no gráfico de saudação. No entanto, Olá **umidade** valores ainda são armazenados e disponibilizados para qualquer processamento de back-end.

## <a name="next-steps"></a>Próximas etapas

Agora que você viu como toouse a telemetria dinâmico, você pode aprender mais sobre como o hello soluções pré-configuradas usam informações do dispositivo: [metadados de informações de dispositivo no monitoramento remoto de saudação pré-configurado solução] [ lnk-devinfo].

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[image3]: media/iot-suite-dynamic-telemetry/image3.png
[image4]: media/iot-suite-dynamic-telemetry/image4.png
[image5]: media/iot-suite-dynamic-telemetry/image5.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
