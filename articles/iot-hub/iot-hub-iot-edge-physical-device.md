---
title: "aaaUse um dispositivo físico com borda de IoT do Azure | Microsoft Docs"
description: "Como toouse um hub de IoT Texas instrumentos SensorTag dispositivo toosend dados tooan por meio de um gateway de borda IoT em execução em um dispositivo de framboesa Pi 3. gateway de saudação é criado usando o Azure IoT borda."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 212dacbf-e5e9-48b2-9c8a-1c14d9e7b913
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: andbuc
ms.openlocfilehash: a2385accdbd99012ad094232653ee47d4e5c7839
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-on-a-raspberry-pi-tooforward-device-to-cloud-messages-tooiot-hub"></a>Usar o Azure IoT borda em um tooIoT de mensagens de dispositivo para nuvem framboesa Pi tooforward Hub

Este passo a passo de saudação [exemplo de baixa energia Bluetooth] [ lnk-ble-samplecode] mostra como toouse [Azure IoT borda] [ lnk-sdk] para:

* Encaminhe telemetria do dispositivo para nuvem tooIoT Hub de um dispositivo físico.
* Comandos de rota do dispositivo físico do IoT Hub tooa.

Este passo a passo aborda:

* **Arquitetura**: importantes informações arquitetônicas sobre Olá Bluetooth baixo consumo de energia de exemplo.
* **Compilar e executar**: Olá etapas necessárias toobuild e exemplo hello execução.

## <a name="architecture"></a>Arquitetura

Olá passo a passo mostra como toobuild e execute um gateway de extremidade IoT em um framboesa Pi 3 que executa Raspbian Linux. gateway de saudação é criado usando a borda de IoT. exemplo Hello usa um Texas instrumentos SensorTag Bluetooth baixa energia (var) dispositivo toocollect temperatura de dados.

Quando você executa Olá gateway de borda IoT-lo:

* Conecta tooa SensorTag dispositivo usando o protocolo do hello Bluetooth baixa energia (var).
* Conecta-se tooIoT Hub usando o protocolo de saudação HTTP.
* Encaminha a telemetria de saudação SensorTag dispositivo tooIoT Hub.
* Rotas de comandos de dispositivo do IoT Hub toohello SensorTag.

gateway Olá contém Olá módulos de borda IoT a seguir:

* Um *módulo Bilitar* que interage com um dado de temperatura Bilitar dispositivo tooreceive de saudação dispositivo e enviar comandos toohello.
* Um *módulo do Bilitar nuvem toodevice* que converte mensagens JSON enviadas do IoT Hub em instruções Bilitar para Olá *módulo Bilitar*.
* Um *módulo agente* que registra todos os gateway mensagens tooa arquivo local.
* Um *módulo de mapeamento de identidade* que faz a conversão entre endereços MAC dos dispositivos BLE e identidades de dispositivos do Hub IoT do Azure.
* Um *módulo de IoT Hub* que carrega o hub IoT do telemetria dados tooan e recebe comandos de dispositivo de um hub IoT.
* Um *módulo de impressora Bilitar* que interprete a telemetria de dispositivo de Bilitar hello e imprime os dados formatados toohello console tooenable solução de problemas e depuração.

### <a name="how-data-flows-through-hello-gateway"></a>Como os dados fluem por meio do gateway de saudação

Olá bloco diagrama a seguir ilustra o pipeline de fluxo de dados de carregamento do hello telemetria:

![Pipeline de gateway de upload de telemetria](media/iot-hub-iot-edge-physical-device/gateway_ble_upload_data_flow.png)

etapas de saudação que viajam de um tooIoT de dispositivo Bilitar entra em um item de telemetria Hub são:

1. dispositivo de Bilitar Hello gera uma amostra de temperatura e envia módulo de Bilitar toohello Bluetooth no gateway hello.
1. módulo de Bilitar Olá recebe exemplo hello e publica broker toohello junto com o endereço MAC de saudação do dispositivo hello.
1. módulo de mapeamento de identidade de saudação pega essa mensagem e usa uma saudação tootranslate de tabela interna endereço MAC do dispositivo de saudação em uma identidade de dispositivo IoT Hub. Uma identidade de dispositivo do Hub IoT consiste em uma ID de dispositivo e na chave do dispositivo.
1. módulo de mapeamento de identidade Olá publica uma nova mensagem que contém dados de exemplo hello temperatura, o endereço MAC de saudação do dispositivo de hello, ID do dispositivo hello e chave do dispositivo hello.
1. Olá módulo IoT Hub recebe essa mensagem nova (gerada pelo módulo de mapeamento de identidade de saudação) e publica tooIoT Hub.
1. módulo de agente Olá registra todas as mensagens de arquivo local da saudação broker tooa.

Olá bloco diagrama a seguir ilustra Olá pipeline de fluxo de dados de comando de dispositivo:

![Pipeline do gateway de comando do dispositivo](media/iot-hub-iot-edge-physical-device/gateway_ble_command_data_flow.png)

1. Olá IoT Hub módulo periodicamente sonda Olá hub IoT para novas mensagens de comando.
1. Quando Olá módulo IoT Hub recebe uma nova mensagem de comando, ela publica toohello broker.
1. módulo de mapeamento de identidade Olá pega a mensagem de saudação do comando e usa uma saudação tootranslate de tabela interna IoT Hub dispositivo ID tooa dispositivo endereço MAC. Em seguida, publica uma nova mensagem que inclui o endereço MAC de saudação do dispositivo de destino Olá no mapa de propriedades de saudação de mensagem de saudação.
1. módulo de nuvem para dispositivo Bilitar Olá pega essa mensagem e converte em instrução Bilitar adequada de Olá para o módulo de Bilitar Olá. Em seguida, ele publica uma nova mensagem.
1. módulo de Bilitar Olá pega essa mensagem e executa a instrução de e/s de saudação comunicando-se com o dispositivo de Bilitar hello.
1. módulo de agente Olá registra todas as mensagens do arquivo de disco Olá broker tooa.

## <a name="prerequisites"></a>Pré-requisitos

toocomplete neste tutorial, você precisa de uma assinatura ativa do Azure.

> [!NOTE]
> Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação gratuita do Azure][lnk-free-trial].

Você precisa cliente SSH no seu tooenable computador desktop você tooremotely acesso Olá linha de comando em Olá framboesa Pi.

- O Windows não inclui um cliente SSH. Recomendamos o uso de [PuTTY](http://www.putty.org/).
- A maioria das distribuições do Linux e Mac OS incluem o utilitário SSH de linha de comando do hello. Para obter mais informações, consulte [SSH usando o Linux ou Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).

## <a name="prepare-your-hardware"></a>Prepare seu hardware

Este tutorial presume que você está usando um [Texas instrumentos SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) dispositivo conectado tooa framboesa Pi 3 executando Raspbian.

### <a name="install-raspbian"></a>Instalar Raspbian

Você pode usar qualquer um dos Olá opções tooinstall Raspbian a seguir em seu dispositivo framboesa Pi 3.

* versão mais recente do hello tooinstall de Raspbian, use Olá [NOOBS] [ lnk-noobs] interface gráfica do usuário.
* Manualmente [baixar] [ lnk-raspbian] e gravar a imagem mais recente de saudação do cartão de saudação Raspbian sistema operacional tooan SD.

### <a name="sign-in-and-access-hello-terminal"></a>Entrar e acessar terminal Olá

Você tem um ambiente de terminal tooaccess de duas opções com seu Pi framboesa:

* Se você tiver um teclado e monitorar tooyour conectado framboesa Pi, você pode usar o hello GUI Raspbian tooaccess uma janela de terminal.

* Acesso a linha de comando do hello no seu Pi framboesa usando SSH em seu computador desktop.

#### <a name="use-a-terminal-window-in-hello-gui"></a>Use uma janela de terminal Olá GUI

credenciais de padrão de saudação para Raspbian são o nome de usuário **pi** e a senha **framboesa**. Na barra de tarefas de saudação em Olá GUI, você pode iniciar Olá **Terminal** utilitário usando o ícone de saudação que se parece com um monitor.

#### <a name="sign-in-with-ssh"></a>Entre com o SSH

Você pode usar o SSH para acesso de linha de comando tooyour framboesa Pi. artigo Olá [SSH (Secure Shell)] [ lnk-pi-ssh] descreve como tooconfigure SSH com o Pi framboesa e como tooconnect de [Windows] [ lnk-ssh-windows] ou [Sistema operacional Linux e Mac][lnk-ssh-linux].

Entre com o nome de usuário **pi** e a senha **raspberry**.

### <a name="install-bluez-537"></a>Instalar o BlueZ 5.37

módulos de Bilitar Olá falam toohello Bluetooth hardware por meio da pilha de BlueZ hello. Você precisa versão 5.37 do BlueZ para Olá módulos toowork corretamente. Essas instruções Certifique-se de saudação a versão correta do BlueZ está instalada.

1. Pare o daemon do hello atual bluetooth:

    ```sh
    sudo systemctl stop bluetooth
    ```

1. Instale dependências de BlueZ hello:

    ```sh
    sudo apt-get update
    sudo apt-get install bluetooth bluez-tools build-essential autoconf glib2.0 libglib2.0-dev libdbus-1-dev libudev-dev libical-dev libreadline-dev
    ```

1. Baixe o código-fonte Olá BlueZ do bluez.org:

    ```sh
    wget http://www.kernel.org/pub/linux/bluetooth/bluez-5.37.tar.xz
    ```

1. Descompacte o código-fonte hello:

    ```sh
    tar -xvf bluez-5.37.tar.xz
    ```

1. Alterar pasta de toohello recém-criado de diretórios:

    ```sh
    cd bluez-5.37
    ```

1. Configure Olá BlueZ código toobe criado:

    ```sh
    ./configure --disable-udev --disable-systemd --enable-experimental
    ```

1. Compile o BlueZ:

    ```sh
    make
    ```

1. Após compilar o BlueZ, instale-o:

    ```sh
    sudo make install
    ```

1. Alteração da configuração do serviço systemd para bluetooth para que ele aponte toohello novo daemon bluetooth no arquivo hello `/lib/systemd/system/bluetooth.service`. Substitua linha de 'ExecStart' hello Olá texto a seguir:

    ```conf
    ExecStart=/usr/local/libexec/bluetooth/bluetoothd -E
    ```

### <a name="enable-connectivity-toohello-sensortag-device-from-your-raspberry-pi-3-device"></a>Habilitar o dispositivo de SensorTag toohello conectividade do dispositivo framboesa Pi 3

Antes de exemplo hello em execução, é necessário tooverify seu framboesa Pi 3 pode conectar-se toohello SensorTag dispositivo.

1. Certifique-se de saudação `rfkill` utilitário é instalado:

    ```sh
    sudo apt-get install rfkill
    ```

1. Desbloquear bluetooth em Olá framboesa Pi 3 e verifique se o número de versão de saudação é **5.37**:

    ```sh
    sudo rfkill unblock bluetooth
    bluetoothctl --version
    ```

1. tooenter shell de bluetooth interativo hello, iniciar o serviço de bluetooth hello e executar Olá **bluetoothctl** comando:

    ```sh
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. Digite o comando Olá **ligado** toopower controlador do hello bluetooth. comando Olá retorna a seguir toohello semelhante saída:

    ```sh
    [NEW] Controller 98:4F:EE:04:1F:DF C3 raspberrypi [default]
    ```

1. No shell de bluetooth interativo hello, digite o comando de saudação **a varredura em** tooscan dispositivos bluetooth. comando Olá retorna a seguir toohello semelhante saída:

    ```sh
    Discovery started
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: yes
    ```

1. Torne dispositivo de SensorTag Olá detectável pressionando Olá pequeno botão (Olá piscarão LED verde). Olá framboesa Pi 3 deve descobrir dispositivos de SensorTag hello:

    ```sh
    [NEW] Device A0:E6:F8:B5:F6:00 CC2650 SensorTag
    [CHG] Device A0:E6:F8:B5:F6:00 TxPower: 0
    [CHG] Device A0:E6:F8:B5:F6:00 RSSI: -43
    ```

    Neste exemplo, você pode ver que Olá endereço MAC de saudação SensorTag dispositivo **A0:E6:F8:B5:F6:00**.

1. Desativar a verificação inserindo Olá **verificação** comando:

    ```sh
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: no
    Discovery stopped
    ```

1. Conectar tooyour SensorTag dispositivo usando seu endereço MAC inserindo **conectar \<endereço MAC\>**. saudação de saída de exemplo a seguir é abreviada para maior clareza:

    ```sh
    Attempting tooconnect tooA0:E6:F8:B5:F6:00
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: yes
    Connection successful
    [CHG] Device A0:E6:F8:B5:F6:00 UUIDs: 00001800-0000-1000-8000-00805f9b34fb
    ...
    [NEW] Primary Service
            /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
            Device Information
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 GattServices: /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 Name: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Alias: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Modalias: bluetooth:v000Dp0000d0110
    ```

    > Você pode listar Olá GATT características de saudação dispositivo novamente usando Olá **lista atributos** comando.

1. Agora você pode desconectar de dispositivo de saudação usando Olá **desconectar** de comando e, em seguida, saia do shell de bluetooth hello usando Olá **sair** comando:

    ```sh
    Attempting toodisconnect from A0:E6:F8:B5:F6:00
    Successful disconnected
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: no
    ```

Agora você está exemplo de borda de IoT Bilitar hello toorun pronto em seu framboesa Pi 3.

## <a name="run-hello-iot-edge-ble-sample"></a>Executar Olá IoT borda Bilitar exemplo

exemplo de IoT borda Bilitar hello toorun, é necessário toocomplete três tarefas:

* Configurar dois dispositivos de exemplo em seu Hub IoT.
* Crie o IoT Edge em seu dispositivo Raspberry Pi 3.
* Configurar e executar o exemplo de Bilitar hello em seu dispositivo framboesa Pi 3.

No momento da saudação de gravação, borda IoT só dá suporte a módulos Bilitar em gateways em execução no Linux.

### <a name="configure-two-sample-devices-in-your-iot-hub"></a>Configurar dois dispositivos de exemplo em seu Hub IoT

* [Criar um hub IoT] [ lnk-create-hub] na sua assinatura do Azure, você precisará Olá nome do seu hub toocomplete este passo a passo. Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.
* Adicionar um dispositivo chamado **SensorTag_01** tooyour IoT hub e anote sua chave de id e o dispositivo. Você pode usar o hello [Gerenciador de dispositivo ou Gerenciador de Hub IOT] [ lnk-explorer-tools] ferramentas tooadd este hub IoT de toohello de dispositivo criado na etapa anterior hello e tooretrieve sua chave. Você mapeia esse dispositivo toohello SensorTag dispositivo ao configurar o gateway de saudação.

### <a name="build-azure-iot-edge-on-your-raspberry-pi-3"></a>Criar o Azure IoT Edge no Raspberry Pi 3

Instalar dependências para o Azure IoT Edge:

```sh
sudo apt-get install cmake uuid-dev curl libcurl4-openssl-dev libssl-dev
```

A seguir Olá use comandos tooclone IoT borda e todos os seu submódulos tooyour diretório base:

```sh
cd ~
git clone https://github.com/Azure/iot-edge.git
```

Quando você tiver uma cópia completa de saudação repositório IoT borda em seu framboesa Pi 3, você pode criar usando Olá comando a seguir na pasta Olá contém Olá SDK:

```sh
cd ~/iot-edge
./tools/build.sh  --disable-native-remote-modules
```

### <a name="configure-and-run-hello-ble-sample-on-your-raspberry-pi-3"></a>Configurar e executar o exemplo de Bilitar de saudação em seu framboesa Pi 3

toobootstrap e exemplo hello execução, você deve configurar cada módulo de borda IoT participa no gateway hello. Essa configuração é fornecida em um arquivo JSON e você precisa configurar todos os cinco módulos IoT Edge participantes. Há um arquivo JSON de exemplo no repositório de saudação chamado **gateway\_sample.json** que você pode usar como ponto de partida para criar seu próprio arquivo de configuração de saudação. Esse arquivo está em Olá **ble_gateway/exemplos/src** pasta na cópia local do hello repositório IoT borda.

Olá seções a seguir descrevem como tooedit essa configuração do arquivo de exemplo de Bilitar hello e suponha que Olá repositório IoT borda está em Olá **/home/pi/iot-edge /** pasta no seu framboesa Pi 3. Se o repositório de saudação estiver em outro lugar, ajuste caminhos Olá adequadamente.

#### <a name="logger-configuration"></a>Configuração do agente

Supondo que o repositório de gateway hello está localizado em Olá **/home/pi/iot-edge /** pasta, configure o módulo de agente de log de saudação da seguinte maneira:

```json
{
  "name": "Logger",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path" : "build/modules/logger/liblogger.so"
    }
  },
  "args":
  {
    "filename": "<</path/to/log-file.log>>"
  }
}
```

#### <a name="ble-module-configuration"></a>Configuração do módulo BLE

configuração de exemplo Hello para dispositivo de Bilitar Olá pressupõe um dispositivo SensorTag de instrumentos Texas. Qualquer dispositivo Bilitar padrão que pode funcionar como um GATT periférico deve funcionar, mas você pode precisar característica de GATT tooupdate Olá IDs e dados. Adicione o endereço MAC de saudação do seu dispositivo SensorTag:

```json
{
  "name": "SensorTag",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble.so"
    }
  },
  "args": {
    "controller_index": 0,
    "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
    "instructions": [
      {
        "type": "read_once",
        "characteristic_uuid": "00002A24-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A25-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A26-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A27-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A28-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A29-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "write_at_init",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AQ=="
      },
      {
        "type": "read_periodic",
        "characteristic_uuid": "F000AA01-0451-4000-B000-000000000000",
        "interval_in_ms": 1000
      },
      {
        "type": "write_at_exit",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AA=="
      }
    ]
  }
}
```

Se você não estiver usando um dispositivo SensorTag, revise a documentação de saudação para sua toodetermine de dispositivo Bilitar se você precisa de característica de GATT tooupdate Olá IDs e valores de dados.

#### <a name="iot-hub-module"></a>módulo do Hub IoT

Adicione nome de saudação do seu IoT Hub. valor de sufixo de saudação é normalmente **devices.net azure**:

```json
{
  "name": "IoTHub",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/iothub/libiothub.so"
    }
  },
  "args": {
    "IoTHubName": "<<Azure IoT Hub Name>>",
    "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
    "Transport" : "amqp"
  }
}
```

#### <a name="identity-mapping-module-configuration"></a>Configuração do módulo de mapeamento de identidade

Adicione o endereço MAC de saudação do seu dispositivo de SensorTag e a ID do dispositivo Olá e a chave da saudação **SensorTag_01** dispositivo adicionado tooyour IoT Hub:

```json
{
  "name": "mapping",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/identitymap/libidentity_map.so"
    }
  },
  "args": [
    {
      "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
      "deviceId": "<<Azure IoT Hub Device ID>>",
      "deviceKey": "<<Azure IoT Hub Device Key>>"
    }
  ]
}
```

#### <a name="ble-printer-module-configuration"></a>Configuração do módulo de impressora BLE

```json
{
  "name": "BLE Printer",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/samples/ble_gateway/ble_printer/libble_printer.so"
    }
  },
  "args": null
}
```

#### <a name="blec2d-module-configuration"></a>Configuração do módulo BLEC2D

```json
{
  "name": "BLEC2D",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble_c2d.so"
    }
  },
  "args": null
}
```

#### <a name="routing-configuration"></a>Configuração de roteamento

configuração a seguir Hello assegura seguir Olá roteamento entre módulos IoT borda:

* Olá **agente** módulo recebe e registra todas as mensagens.
* Olá **SensorTag** módulo envia Olá de tooboth mensagens **mapeamento** e **Bilitar impressora** módulos.
* Olá **mapeamento** módulo envia mensagens toohello **hub IOT** toobe módulo enviado tooyour IoT Hub.
* Olá **hub IOT** módulo envia de volta toohello **mapeamento** módulo.
* Olá **mapeamento** módulo envia mensagens toohello **BLEC2D** módulo.
* Olá **BLEC2D** módulo envia de volta toohello **marca Sensor** módulo.

```json
"links" : [
    {"source" : "*", "sink" : "Logger" },
    {"source" : "SensorTag", "sink" : "mapping" },
    {"source" : "SensorTag", "sink" : "BLE Printer" },
    {"source" : "mapping", "sink" : "IoTHub" },
    {"source" : "IoTHub", "sink" : "mapping" },
    {"source" : "mapping", "sink" : "BLEC2D" },
    {"source" : "BLEC2D", "sink" : "SensorTag"}
 ]
```

exemplo de hello toorun, passagem Olá caminho toohello arquivo de configuração JSON como um parâmetro toohello **bilitar\_gateway** binário. Olá comando a seguir presume que você está usando Olá **gateway_sample.json** arquivo de configuração. Executar esse comando de saudação **iot borda** pasta Olá framboesa Pi:

```sh
./build/samples/ble_gateway/ble_gateway ./samples/ble_gateway/src/gateway_sample.json
```

Talvez seja necessário toopress Olá pequeno botão Olá SensorTag dispositivo toomake-lo detectável antes de executar o exemplo hello.

Quando você executar o exemplo hello, você pode usar o hello [explorer dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) ou hello [Gerenciador de Hub IOT](https://github.com/Azure/iothub-explorer) ferramenta toomonitor Olá mensagens Olá encaminha o gateway de borda de IoT de dispositivo de SensorTag hello. Por exemplo, usando o Gerenciador de Hub IOT você pode monitorar mensagens de dispositivo para nuvem usando Olá comando a seguir:

```sh
iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
```

## <a name="send-cloud-to-device-messages"></a>Envie mensagens da nuvem para o dispositivo

módulo de Bilitar Olá também oferece suporte a comandos de enviados do dispositivo do IoT Hub toohello. Você pode usar o hello [explorer dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) ou hello [Gerenciador de Hub IOT](https://github.com/Azure/iothub-explorer) mensagens JSON toosend ferramenta módulo Olá Bilitar gateway encaminha no dispositivo de Bilitar toohello.

Se você estiver usando um dispositivo de Texas instrumentos SensorTag hello, você pode ativar LED Olá vermelho, LED verde ou campainha enviando comandos de IoT Hub. Antes de enviar comandos de IoT Hub, primeiro envie Olá duas mensagens JSON em ordem a seguir. Em seguida, você pode enviar qualquer Olá comandos tooturn luzes hello ou campainha.

1. Redefina todos os LEDs e campainha hello (desativá-los):

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AA=="
    }
    ```

1. Configurar a E/S como 'remota':

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA66-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

Agora você pode enviar qualquer Olá tooturn comandos a seguir em luzes hello ou campainha no dispositivo de SensorTag hello:

* Ative o LED Olá vermelho:

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

* Ative o LED verde do hello:

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "Ag=="
    }
    ```

* Ative campainha hello:

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "BA=="
    }
    ```

## <a name="next-steps"></a>Próximas etapas

Se você quiser toogain uma compreensão mais avançada de IoT borda e fazer experiências com alguns exemplos de código, visite Olá tutoriais de desenvolvedor e recursos:

* [Azure IoT Edge][lnk-sdk]

toofurther explorar recursos de saudação do IoT Hub, consulte:

* [Guia do desenvolvedor do Hub IoT][lnk-devguide]

<!-- Links -->
[lnk-ble-samplecode]: https://github.com/Azure/iot-edge/tree/master/samples/ble_gateway
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-explorer-tools]: https://github.com/Azure/azure-iot-sdks/blob/master/doc/manage_iot_hub.md
[lnk-sdk]: https://github.com/Azure/iot-edge/
[lnk-noobs]: https://www.raspberrypi.org/documentation/installation/noobs.md
[lnk-raspbian]: https://www.raspberrypi.org/downloads/raspbian/
[lnk-devguide]: iot-hub-devguide.md
[lnk-create-hub]: iot-hub-create-through-portal.md 
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
