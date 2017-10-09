---
title: aaaUse um gateway de IoT tooconnect tooAzure um dispositivo IoT Hub | Microsoft Docs
description: "Saiba como toouse NUC Intel como um gateway de IoT tooconnect um SensorTag de TI e enviar os dados sensor tooAzure IoT Hub em Olá de nuvem."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "conexão de gateway de IOT toocloud do dispositivo"
ms.assetid: cb851648-018c-4a7e-860f-b62ed3b493a5
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: 418af34bf29992d46b76ae59ef548744808664c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-tooconnect-things-toohello-cloud---sensortag-tooazure-iot-hub"></a>Usar IoT gateway tooconnect coisas toohello nuvem - SensorTag tooAzure IoT Hub

> [!NOTE]
> Antes de iniciar este tutorial, conclua a [Configurar o Intel NUC como um gateway IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md). Em [configurar NUC Intel como um gateway IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), configurar Olá Intel NUC dispositivo como um gateway de IoT.

## <a name="what-you-will-learn"></a>O que você aprenderá

Você aprenderá como toouse um gateway de IoT tooconnect um tooAzure Texas instrumentos SensorTag (CC2650STK) IoT Hub. gateway de IoT Olá envia temperatura e umidade os dados coletados de saudação SensorTag tooAzure IoT Hub.

## <a name="what-you-will-do"></a>O que você fará

- Crie um Hub IoT.
- Registre um dispositivo no hub IoT de saudação para Olá SensorTag.
- Habilite conexão Olá entre o gateway de IoT hello e Olá SensorTag.
- Execute um Bilitar exemplo aplicativo toosend SensorTag tooyour IoT hub de dados.

## <a name="what-you-need"></a>O que você precisa

- Do tutorial [Configurar o Intel NUC como um gateway IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) concluído, no qual você configura o Intel NUC como um gateway IoT.
- * Uma assinatura ativa do Azure. Se não tiver uma conta do Azure, [crie uma conta de avaliação gratuita do Azure](https://azure.microsoft.com/free/) em apenas alguns minutos.
- Um cliente SSH executado no computador host. Recomenda-se o PuTTY no Windows. O Linux e o macOS já vêm com um cliente SSH.
- Olá endereço IP e Olá username e password tooaccess Olá gateway de cliente SSH hello.
- Uma conexão com a Internet.

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

> [!NOTE]
> Aqui você registra esse novo dispositivo para o seu SensorTag

## <a name="enable-hello-connection-between-hello-iot-gateway-and-hello-sensortag"></a>Habilitar conexão Olá entre o gateway de IoT hello e Olá SensorTag

Nesta seção, você executará Olá tarefas a seguir:

- Obter endereço MAC Olá Olá SensorTag conexão Bluetooth.
- Inicie uma conexão de Bluetooth do hello IoT gateway toohello SensorTag.

### <a name="get-hello-mac-address-of-hello-sensortag-for-bluetooth-connection"></a>Obter o endereço MAC Olá Olá SensorTag para conexão de Bluetooth

1. No computador de host Olá, execute o cliente SSH hello e conecte-se toohello IoT gateway.
1. Desbloquear Bluetooth executando Olá comando a seguir:

   ```bash
   sudo rfkill unblock bluetooth
   ```

1. Iniciar serviço de Bluetooth do hello no gateway do IoT hello e insira um tooconfigure de shell Bluetooth Bluetooth executando Olá comandos a seguir:

   ```bash
   sudo systemctl start bluetooth
   bluetoothctl
   ```

1. Ligar o controlador de Bluetooth Olá executando Olá comando no hello shell Bluetooth a seguir:

   ```bash
   power on
   ```

   ![ligar o controlador de Bluetooth Olá no gateway do IoT Olá com bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/8_power-on-bluetooth-controller-at-bluetooth-shell-bluetoothctl.png)

1. Inicie a varredura para dispositivos Bluetooth próximos executando Olá comando a seguir:

   ```bash
   scan on
   ```

   ![Procurar dispositivos Bluetooth próximos com bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/9_start-scan-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

1. Pressione Olá emparelhamento botão Olá SensorTag. Olá verde LED no hello SensorTag pisca.
1. Em Olá Bluetooth shell, você deve ver Olá que sensortag foi encontrado. Anote Olá Olá SensorTag endereço MAC. Neste exemplo, Olá endereço MAC de saudação SensorTag é `24:71:89:C0:7F:82`.
1. Desative a verificação de saudação executando o comando a seguir de saudação:

   ```bash
   scan off
   ```

   ![Interromper a varredura de dispositivos Bluetooth próximos com bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/10_stop-scanning-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

### <a name="initiate-a-bluetooth-connection-from-hello-iot-gateway-toohello-sensortag"></a>Iniciar uma conexão de Bluetooth do hello IoT gateway toohello SensorTag

1. Conecte-se toohello SensorTag executando Olá comando a seguir:

   ```bash
   connect <MAC address>
   ```

   ![Conecte-se toohello SensorTag com bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/11_connect-to-sensortag-at-bluetooth-shell-bluetoothctl.png)

1. Desconectar Olá SensorTag e sair do shell de Bluetooth Olá executando Olá comandos a seguir:

   ```bash
   disconnect
   exit
   ```

   ![Desconectar Olá SensorTag com bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/12_disconnect-from-sensortag-at-bluetooth-shell-bluetoothctl.png)

Conexão Olá entre o gateway de IoT hello e Olá SensorTag estiver habilitado.

## <a name="run-a-ble-sample-application-toosend-sensortag-data-tooyour-iot-hub"></a>Executar um Bilitar exemplo aplicativo toosend SensorTag tooyour IoT hub de dados

Olá aplicativo de exemplo de Bluetooth baixa energia (var) é fornecido pelo Azure IoT borda. aplicativo de exemplo Hello coleta dados de conexão Bilitar e enviar o hub IoT do hello dados tooyou. aplicativo de exemplo hello toorun, você precisa:

1. Configure o aplicativo de exemplo hello.
1. Execute o aplicativo de exemplo hello no gateway do IoT hello.

### <a name="configure-hello-sample-application"></a>Configurar o aplicativo de exemplo hello

1. Vá toohello pasta do aplicativo de exemplo hello executando Olá comando a seguir:

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples/ble_gateway
   ```

1. Abra o arquivo de configuração de saudação executando Olá comando a seguir:

   ```bash
   vi ble_gateway.json
   ```

1. No arquivo de configuração hello, preencha Olá valores a seguir:

   **IoTHubName**: nome de saudação do seu hub IoT.

   **IoTHubSuffix**: IoTHubSuffix obter da saudação chave primária da cadeia de caracteres de conexão de dispositivo Olá que você anotou para baixo. Certifique-se de que você obter a chave primária de saudação da cadeia de caracteres de conexão de dispositivo hello, Olá não chave primária de sua cadeia de conexão de hub IoT. chave primária de saudação da cadeia de caracteres de conexão de dispositivo hello está no formato de saudação do `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.

   **Transporte**: valor de padrão de saudação é `amqp`. Esse valor mostra o protocolo de saudação durante transpotation. Ele pode ser `http`, `amqp` ou `mqtt`.

   **macAddress**: Olá endereço MAC de saudação SensorTag que você anotou para baixo.

   **deviceID**: ID do dispositivo Olá que você criou em seu hub IoT.

   **deviceKey**: chave primária de saudação da cadeia de caracteres de conexão de dispositivo hello.

   ![Arquivo de configuração de saudação completa de saudação aplicativo de exemplo Bilitar](./media/iot-hub-iot-gateway-connect-device-to-cloud/13_edit-config-file-of-ble-sample.png)

1. Pressione `ESC` e tipo `:wq` toosave arquivo de saudação.

### <a name="run-hello-sample-application"></a>Executar o aplicativo de exemplo hello

1. Verifique se Olá que sensortag está ligado.
1. Execute Olá comando a seguir:

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a>Próximas etapas

[Usar o gateway IoT para transformação dos dados de sensor com o Azure IoT Edge](iot-hub-gateway-kit-c-use-iot-gateway-for-data-conversion.md)
