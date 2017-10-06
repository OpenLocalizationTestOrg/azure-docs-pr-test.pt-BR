---
title: "M0 toocloud: conectar-se a difusão M0 WiFi tooAzure IoT Hub | Microsoft Docs"
description: "Saiba como tooset up e conectar Adafruit difusão M0 WiFi tooAzure plataforma de nuvem do Azure IoT Hub toosend dados toohello neste tutorial."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 51befcdb-332b-416f-a6a1-8aabdb67f283
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/16/2017
ms.author: xshi
ms.openlocfilehash: 6aabeb961a50ba5d3934f77eb1ccda4af1bf64c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-m0-wifi-tooazure-iot-hub-in-hello-cloud"></a>Conecte-se Adafruit difusão M0 WiFi tooAzure IoT Hub na nuvem Olá
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Conexão entre BME280, Feather M0 WiFi e Hub IoT](media/iot-hub-adafruit-feather-m0-wifi-get-started/1_connection-m0-feather-m0-iot-hub.png)

Neste tutorial, você começar a aprender os fundamentos de saudação do trabalho com seu quadro Arduino. Em seguida, você aprenderá como tooseamlessly se conectar a sua nuvem de toohello dispositivos usando [Azure IoT Hub](iot-hub-what-is-iot-hub.md).

## <a name="what-you-do"></a>O que fazer

Conecte-se Adafruit difusão M0 WiFi tooan IoT hub que você criar. Em seguida, execute um aplicativo de exemplo em M0 Wi-Fi toocollect Olá temperatura e umidade dados de um BME280. Por fim, você pode enviar hub IoT do hello sensor dados tooyour.


## <a name="what-you-learn"></a>O que você aprenderá

* Como toocreate um hub IoT e registrar um dispositivo para difusão M0 WiFi
* Como tooconnect difusão M0 WiFi com sensor hello e seu computador
* Como os dados do sensor toocollect executando um aplicativo de exemplo em difusão M0 Wi-Fi
* Como toosend Olá hub IoT do sensor dados tooyour

## <a name="what-you-need"></a>O que você precisa

![Partes necessárias para o tutorial Olá](media/iot-hub-adafruit-feather-m0-wifi-get-started/2_parts-needed-for-the-tutorial.png)

toocomplete essa operação, você precisa Olá seguir partes de seu difusão M0 WiFi Starter Kit:

* Olá difusão M0 WiFi board
* Um tooType Micro USB um cabo

Você também precisa Olá coisas para seu ambiente de desenvolvimento a seguir:

* Uma assinatura ativa do Azure. Se não tiver uma conta do Azure, [crie uma conta de avaliação gratuita do Azure](https://azure.microsoft.com/free/) em apenas alguns minutos.
* Um Mac ou PC que esteja executando Windows ou Ubuntu.
* Uma rede sem fio para difusão M0 WiFi tooconnect para.
* Uma ferramenta de configuração do Internet conexão toodownload hello.
* [IDE do Arduino](https://www.arduino.cc/en/main/software) versão 1.6.8 ou posterior. Versões anteriores não funcionam com a biblioteca do hello Azure IoT Hub.

Se você não tiver um sensor, Olá itens a seguir é opcional. Você também tem a opção de saudação do uso de dados de sensor simulada:

* Um sensor de temperatura e umidade BME280
* Uma placa universal
* Cabos de jumper de M/M

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-m0-wifi-with-hello-sensor-and-your-computer"></a>Conexão Wi-Fi M0 de difusão com sensor hello e seu computador
Nesta seção, você se conectar a placa de tooyour sensores hello. Em seguida, você conecta o computador tooyour de dispositivo para uso posterior.

### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-m0-wifi"></a>Conecte-se um DHT22 temperatura e umidade sensor tooFeather M0 Wi-Fi

Use Olá breadboard e jumper fios toomake Olá conexão. Se você não tiver um sensor, ignore esta seção porque você pode usar dados de sensor simulado em vez disso.

![Referência de conexões](media/iot-hub-adafruit-feather-m0-wifi-get-started/3_connections_on_breadboard.png)


Pinos do sensor, use Olá fiação a seguir:


| Início (sensor)           | Fim (placa)            | Cor do cabo   |
| -----------------------  | ---------------------- | ------------: |
| VDD (pino 27A)            | 3V (pino 3A)            | Cabo vermelho     |
| GND (pino 29A)            | GND (pino 6A)           | Cabo preto   |
| SCK (pino 30A)            | SCK (pino 12A)          | Cabo amarelo  |
| SDO (pino 31A)            | MI (pino 14A)           | Cabo branco   |
| SDI (pino 32A)            | M0 (pino 13A)           | Cabo azul    |
| CS (pino 33A)             | GPIO 5 (pino 15J)       | Cabo laranja  |

Para obter mais informações, consulte [Saídas do sensor de umidade, pressão barométrica e temperatura Adafruit BME280](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) e [Pinagem do Adafruit Feather M0 WiFi](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts).



Agora seu Feather M0 WiFi deve estar conectado a um sensor ativo.

![Conectar o DHT22 ao Feather Huzzah](media/iot-hub-adafruit-feather-m0-wifi-get-started/4_connect-bme280-feather-m0-wifi.png)

### <a name="connect-feather-m0-wifi-tooyour-computer"></a>Conectar o computador de tooyour difusão M0 WiFi

Use Olá Micro USB tooType USB um cabo tooconnect difusão M0 WiFi tooyour computador, conforme mostrado:

![Conectar o computador de tooyour Huzzah de difusão](media/iot-hub-adafruit-feather-m0-wifi-get-started/5_connect-feather-m0-wifi-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a>Adicionar permissões de porta serial (somente Ubuntu)

Se você usar Ubuntu, verifique se que você tem Olá permissões toooperate em Olá USB porta da difusão M0 Wi-Fi. permissões de porta serial tooadd, siga estas etapas:


1. Em um terminal, execute Olá comandos a seguir:

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   Você obtém uma saudação saídas a seguir:

   * crw-rw---- 1 root uucp xxxxxxxx
   * crw-rw---- 1 root dialout xxxxxxxx

   Na saída de hello, observe que `uucp` ou `dialout` é o nome de proprietário do grupo de saudação do hello porta USB.

2. tooadd Olá toohello grupo de usuários, execute Olá comando a seguir:

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   Na etapa anterior de saudação, você obteve o nome do proprietário do grupo Olá `<group-owner-name>`. Seu nome de usuário do Ubuntu é `<username>`.

3. Para Olá alteração tooappear, saia do Ubuntu e entrar novamente.

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a>Coletar dados de sensor e enviá-lo tooyour IoT hub

Nesta seção, você implanta e executa um aplicativo de exemplo no Feather M0 WiFi. aplicativo de exemplo Hello torna Olá intermitência de LED em difusão M0 Wi-Fi. Em seguida, envia temperatura hello e umidade os dados coletados de saudação BME280 sensor tooyour hub IoT.

### <a name="get-hello-sample-application-from-github-and-prepare-hello-arduino-ide"></a>Obter o aplicativo de exemplo hello do GitHub e preparar Olá Arduino IDE

aplicativo de exemplo Hello está hospedado no GitHub. Clone o repositório de exemplo hello que contém o aplicativo de exemplo de saudação do GitHub. repositório de exemplo hello tooclone, siga estas etapas:

1. Abra um prompt de comando ou uma janela de terminal.

2. Vá tooa pasta onde você deseja toobe de aplicativo de exemplo hello armazenado.
3. Execute Olá comando a seguir:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-Feather-M0-WiFi-client-app.git
   ```

### <a name="install-hello-package-for-feather-m0-wifi-in-hello-arduino-ide"></a>Instalar o pacote de saudação para difusão M0 WiFi no hello Arduino IDE

1. Abra a pasta de saudação onde o aplicativo de exemplo hello está armazenado.

2. Abra o arquivo de app.ino de saudação na pasta de aplicativo Olá Olá Arduino IDE.

   ![Abra o aplicativo de exemplo hello Arduino IDE](media/iot-hub-adafruit-feather-m0-wifi-get-started/6_arduino-ide-open-sample-app.png)


1. Clique em **arquivo** > **preferências** (Windows/Linux) ou **Arduino** > **preferências** (Mac) e copie e Colar vínculo Olá abaixo em Olá **URLs adicionais do Gerenciador de quadros** opção Olá preferências Arduino IDE.
   
   ```
   https://adafruit.github.io/arduino-board-index/package_adafruit_index.json, https://adafruit.github.io/arduino-board-index/package_adafruit_index.json
   ```

1. Clique em **ferramentas** > **placa** > **Manager quadros**e, em seguida, instalar Olá `Arduino SAMD Boards` versão `1.6.2` ou posterior. 

1. Em seguida, em Olá mesma janela, instale o `Adafruit SAMD Boards` tooadd definições de arquivos de quadro de saudação do pacote.

   ![Olá esp8266 pacote está instalado](media/iot-hub-adafruit-feather-m0-wifi-get-started/7_arduino-ide-package-url.png)

4. Clique em **Ferramentas** > **Placa** > **Adafruit M0 WiFi**.

5. Instale os drivers (apenas para Windows). Quando você conecta Wi-Fi M0 de difusão, talvez seja necessário tooinstall um driver. Clique em [Olá link para download na página da Web de saudação](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) instalador do driver Olá toodownload. Siga os drivers de Olá Olá etapas tooinstall desejado.

### <a name="install-necessary-libraries"></a>Instalar as bibliotecas necessárias

1. No hello Arduino IDE, clique em **esboço** > **biblioteca incluem** > **gerenciar bibliotecas**.

2. Pesquisar Olá uma nomes de bibliotecas a seguir. Para cada biblioteca que você localizar, clique em **Instalar**:

   * `RTCZero`
   * `NTPClient`
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_HTTP`
   * `ArduinoJson`
   * `Adafruit BME280 Library`
   * `Adafruit Unified Sensor`

3. Instale o `Adafruit_WINC1500` manualmente. Vá muito[neste site](https://github.com/adafruit/Adafruit_WINC1500) e clique em **Clone ou download** > **baixar ZIP**. Em seu IDE Arduino, acesse muito**esboço** > **biblioteca incluem** > **adicionar. zip biblioteca** e adicione o arquivo zip de saudação.

### <a name="use-hello-sample-application-if-you-dont-have-a-real-bme280-sensor"></a>Use o aplicativo de exemplo hello se você não tiver um sensor BME280 real

Se você não tiver um sensor BME280 real, o aplicativo de exemplo hello pode simular temperatura e umidade dados. tooset backup de dados de toouse simulada de aplicativo de exemplo hello, siga estas etapas:

1. Olá abrir `config.h` arquivo hello `app` pasta.

2. Localize Olá a seguinte linha de código e altere o valor de saudação de `false` muito`true`:

   ```c
   define SIMULATED_DATA true
   ```
   ![Configurar dados de toouse simulada de aplicativo de exemplo hello](media/iot-hub-adafruit-feather-m0-wifi-get-started/8_arduino-ide-configure-app-use-simulated-data.png)

3. Salve o arquivo hello com `Control-s`.

### <a name="deploy-hello-sample-application-toofeather-m0-wifi"></a>Implantar tooFeather de aplicativo de exemplo hello M0 Wi-Fi

1. No hello Arduino IDE, clique em **ferramenta** > **porta**e, em seguida, clique em porta serial Olá para difusão M0 WiFi.

2. Clique em **esboço** > **carregar** toobuild e implantar tooFeather de aplicativo de exemplo hello M0 Wi-Fi.

### <a name="enter-your-credentials"></a>Introduza as suas credenciais

Olá após o carregamento for concluído com êxito, siga estas etapas tooenter suas credenciais:

1. No hello Arduino IDE, clique em **ferramentas** > **Serial Monitor**.

2. No canto inferior direito de saudação da janela do monitor serial hello, selecione **nenhuma final de linha** na lista suspensa de Olá Olá esquerda.
3. Selecione **115200 baud** na lista suspensa Olá Olá à direita.
4. Na caixa de entrada hello na parte superior do hello, insira Olá informações a seguir se você for solicitado tooprovide e clique em **enviar**:

   * SSID Wi-Fi
   * Senha de Wi-Fi
   * Cadeia de conexão de dispositivo

> [!Note]
> Olá credenciais são armazenadas no hello EEPROM de difusão M0 Wi-Fi. Se você clicar em um botão Redefinir Olá Olá difusão M0 WiFi quadro, aplicativo de exemplo hello pergunta se você deseja informações de saudação do tooerase. Digite `Y` tooerase informações de saudação. Você será solicitado a informações de saudação tooprovide uma segunda vez.

### <a name="verify-that-hello-sample-application-is-running-successfully"></a>Verifique se que o aplicativo de exemplo hello está sendo executado com êxito

Se você vir seguinte Olá de saída da janela do monitor serial hello e Olá piscando LED em difusão M0 WiFi, o aplicativo de exemplo hello está sendo executado com êxito:

![Saída final no IDE do Arduino](media/iot-hub-adafruit-feather-m0-wifi-get-started/9_arduino-ide-final-output.png)

## <a name="next-steps"></a>Próximas etapas

Você conectado difusão M0 WiFi tooyour IoT hub e enviados Olá capturado sensor dados tooyour IoT hub com êxito. 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

