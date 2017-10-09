---
title: aaaESP8266 toocloud - tooAzure de conectar o Sparkfun ESP8266 coisa Dev IoT Hub | Microsoft Docs
description: Saiba como toosetup e conecte-se tooAzure Sparkfun ESP8266 coisa Dev IoT Hub para ele plataforma de nuvem do Azure toosend dados toohello neste tutorial.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 587fe292-9602-45b4-95ee-f39bba10e716
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 19b249df23b6df516634853521c6d532f51014da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-sparkfun-esp8266-thing-dev-tooazure-iot-hub-in-hello-cloud"></a>Conecte-se tooAzure Sparkfun ESP8266 coisa Dev IoT Hub na nuvem Olá

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![conexão entre DHT22, a Thing Dev e o Hub IoT](media/iot-hub-sparkfun-thing-dev-get-started/1_connection-hdt22-thing-dev-iot-hub.png)

## <a name="what-you-will-do"></a>O que você fará

Conecte-se Sparkfun ESP8266 coisa Dev tooan IoT hub que será criado. Execute um aplicativo de exemplo em dados de temperatura e umidade toocollect ESP8266 partir de um sensor DHT22. Por fim, envie o hub IoT do hello sensor dados tooyour.

> [!NOTE]
> Se você estiver usando outras placas ESP8266, você ainda pode seguir estas etapas tooconnect-tooyour IoT hub. Dependendo da placa Olá ESP8266 que está usando, talvez seja necessário Olá tooreconfigure `LED_PIN`. Por exemplo, se você estiver usando ESP8266 do AI Thinker, você pode alterá-la de `0` muito`2`. Ainda não tem um kit?: Clique [aqui](http://azure.com/iotstarterkits)

## <a name="what-you-will-learn"></a>O que você aprenderá

* Como toocreate um hub IoT e registrar um dispositivo para propósitos de coisa de dispositivos
* Como tooconnect coisa desenvolvimento com sensor hello e seu computador.
* Como os dados do sensor toocollect executando um aplicativo de exemplo no coisa propósitos de dispositivos
* Como toosend Olá hub IoT do sensor dados tooyour.

## <a name="what-you-will-need"></a>O que será necessário

![Partes necessárias para o tutorial Olá](media/iot-hub-sparkfun-thing-dev-get-started/2_parts-needed-for-the-tutorial.png)

toocomplete essa operação, você precisa Olá seguir partes de seu Starter Kit de desenvolvimento de coisa:

* Olá Sparkfun ESP8266 coisa Dev quadro.
* Cabo USB A um tooType Micro USB.

Você também precisa seguir Olá para o seu ambiente de desenvolvimento:

* Uma assinatura ativa do Azure. Se não tiver uma conta do Azure, [crie uma conta de avaliação gratuita do Azure](https://azure.microsoft.com/free/) em apenas alguns minutos.
* Mac ou PC que esteja executando o Windows ou Ubuntu.
* Rede sem fio para tooconnect Sparkfun ESP8266 coisa desenvolvimento para.
* Ferramenta de configuração saudação do toodownload de conexão de Internet.
* [Arduino IDE](https://www.arduino.cc/en/main/software) versão 1.6.8 (ou mais recente), versões anteriores não funcionarão com a biblioteca de AzureIoT hello.

Olá itens a seguir são opcionais no caso de você não tiver um sensor. Você também tem a opção de saudação do uso de dados de sensor simulada.

* Um sensor de temperatura e umidade Adafruit DHT22.
* Uma placa universal.
* Cabos de jumper de M/M.

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-esp8266-thing-dev-with-hello-sensor-and-your-computer"></a>Conecte-se a ESP8266 coisa desenvolvimento com sensor hello e seu computador

### <a name="connect-a-dht22-temperature-and-humidity-sensor-tooesp8266-thing-dev"></a>Conecte-se de um sensor de temperatura e umidade DHT22 tooESP8266 coisa desenvolvimento

Use Olá breadboard e jumper fios toomake Olá conexão da seguinte maneira. Se você não tiver um sensor, ignore esta seção porque você pode usar dados de sensor simulado em vez disso.

![referência de conexões](media/iot-hub-sparkfun-thing-dev-get-started/15_connections_on_breadboard.png)

Pins de sensor, usaremos Olá fiação a seguir:

| Início (Sensor)           | End (quadro)           | Cor de cabo   |
| -----------------------  | ---------------------- | ------------: |
| VDD (Pin 27F)            | 3V (Pin 8A)           | Cabo vermelho     |
| DATA (Pin 28F)           | GPIO 2 (Pin 9A)       | Cabo branco    |
| GND (Pin 30F)            | GND (Pin 7J)          | Cabo preto   |


- Para obter mais informações, consulte: [Instalação do sensor DHT22](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) e [Especificação da Sparkfun ESP8266 Thing Dev](https://www.sparkfun.com/products/13711)

Agora sua Sparkfun ESP8266 Thing Dev deve estar conectada a um sensor ativo.

![conectar o dht22 à ESP8266 Thing Dev](media/iot-hub-sparkfun-thing-dev-get-started/8_connect-dht22-thing-dev.png)

### <a name="connect-sparkfun-esp8266-thing-dev-tooyour-computer"></a>Conectar o computador de tooyour Sparkfun ESP8266 coisa desenvolvimento

Use Olá Micro USB tooType USB um cabo tooconnect Sparkfun ESP8266 coisa Dev tooyour computador da seguinte maneira.

![conectar difusão huzzah tooyour computador](media/iot-hub-sparkfun-thing-dev-get-started/9_connect-thing-dev-computer.png)

### <a name="add-serial-port-permissions--ubuntu-only"></a>Adicionar permissões de porta serial - somente Ubuntu

Se você usar Ubuntu, certifique-se de que um usuário normal tem Olá permissões toooperate em Olá USB porta de Sparkfun ESP8266 coisa propósitos de dispositivos permissões de porta serial tooadd para um usuário normal, siga estas etapas:

1. Olá executar comandos em um terminal a seguir:

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   Você obtém uma saudação saídas a seguir:

   * crw-rw---- 1 root uucp xxxxxxxx
   * crw-rw---- 1 root dialout xxxxxxxx

   Na saída de hello, observe `uucp` ou `dialout` que é Olá grupo nome do proprietário da saudação porta USB.

1. Adicione grupo de toohello de usuários de saudação executando Olá comando a seguir:

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   `<group-owner-name>`é o nome de proprietário de grupo Olá que você obteve na etapa anterior hello. `<username>` é o nome de usuário do Ubuntu.

1. Saia Ubuntu e entre nele novamente para Olá alterar tootake efeito.

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a>Coletar dados de sensor e enviá-lo tooyour IoT hub

Nesta seção, implante e execute um aplicativo de exemplo em Sparkfun ESP8266 Thing Dev. aplicativo de exemplo Hello pisca Olá LED no desenvolvimento de coisa ESP8266 Sparkfun e envia a temperatura hello e umidade os dados coletados de saudação DHT22 sensor tooyour hub IoT.

### <a name="get-hello-sample-application-from-github"></a>Obter o aplicativo de exemplo hello do GitHub

aplicativo de exemplo Hello está hospedado no GitHub. Clone o repositório de exemplo hello que contém o aplicativo de exemplo de saudação do GitHub. repositório de exemplo hello tooclone, siga estas etapas:

1. Abra um prompt de comando ou uma janela de terminal.
1. Vá tooa pasta onde você deseja toobe de aplicativo de exemplo hello armazenado.
1. Execute Olá comando a seguir:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-SparkFun-ThingDev-client-app.git
   ```

Instale o pacote de saudação para Sparkfun ESP8266 coisa Dev no Arduino IDE:

1. Abra a pasta de saudação onde o aplicativo de exemplo hello está armazenado.
1. Abra o arquivo de app.ino de saudação na pasta do aplicativo hello Arduino IDE.

   ![Abra o aplicativo de exemplo hello no ide arduino](media/iot-hub-sparkfun-thing-dev-get-started/10_arduino-ide-open-sample-app.png)

1. No hello Arduino IDE, clique em **arquivo** > **preferências**.
1. Em Olá **preferências** caixa de diálogo, clique em Olá ícone próximo toohello **URLs adicionais do Gerenciador de quadros** caixa de texto.
1. Na janela pop-up do hello, digite Olá URL a seguir e, em seguida, clique em **Okey**.

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![url do pacote de ponto tooa arduino IDE](media/iot-hub-sparkfun-thing-dev-get-started/11_arduino-ide-package-url.png)

1. Em Olá **preferência** caixa de diálogo, clique em **Okey**.
1. Clique em **Ferramentas** > **Placa** > **Gerenciador de Placas** e procure esp8266.
   ESP8266 com uma versão 2.2.0 ou posterior deve ser instalado.

   ![Olá esp8266 pacote está instalado](media/iot-hub-sparkfun-thing-dev-get-started/12_arduino-ide-esp8266-installed.png)

1. Clique em **Ferramentas** > **Painel** > **Sparkfun ESP8266 Thing Dev**.

### <a name="install-necessary-libraries"></a>Instalar as bibliotecas necessárias

1. No hello Arduino IDE, clique em **esboço** > **biblioteca incluem** > **gerenciar bibliotecas**.
1. Pesquisar Olá uma nomes de bibliotecas a seguir. Para cada biblioteca Olá você localizar, clique em **instalar**.
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a>Você não tem um sensor DHT22 real?

aplicativo de exemplo Hello pode simular a temperatura e umidade dados caso você não tenha um sensor DHT22 real. dados de toouse simulada do aplicativo de exemplo de hello tooenable, siga estas etapas:

1. Olá abrir `config.h` arquivo hello `app` pasta.
1. Localize Olá a seguinte linha de código e altere o valor de saudação de `false` muito`true`:
   ```c
   define SIMULATED_DATA true
   ```
   ![Configurar dados de toouse simulada de aplicativo de exemplo hello](media/iot-hub-sparkfun-thing-dev-get-started/13_arduino-ide-configure-app-use-simulated-data.png)
   
1. Salvar com `Control-s`.

### <a name="deploy-hello-sample-application-toosparkfun-esp8266-thing-dev"></a>Implantar tooSparkfun de aplicativo de exemplo hello ESP8266 coisa desenvolvimento

1. No hello Arduino IDE, clique em **ferramenta** > **porta**e, em seguida, clique em porta serial Olá para propósitos de dispositivos Sparkfun ESP8266 coisa
1. Clique em **esboço** > **carregar** toobuild e implantar tooSparkfun de aplicativo de exemplo hello propósitos de dispositivos ESP8266 coisa

> [!Note]
> Se você estiver usando macOS provavelmente você pode ver Olá mensagens a seguir durante o carregamento. `warning: espcomm_sync failed`,`error: espcomm_open failed`. Abra a janela ternimal e concluir abaixo ações toosolve esse problema.
> ```bash
> cd /System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns
> sudo mv AppleUSBFTDI.kext AppleUSBFTDI.disabled
> sudo touch /System/Library/Extensions
> ```

### <a name="enter-your-credentials"></a>Inserir suas credenciais

Olá após o carregamento for concluído com êxito, execute Olá etapas tooenter suas credenciais:

1. No hello Arduino IDE, clique em **ferramentas** > **Serial Monitor**.
1. Na janela do monitor serial hello, observe Olá dois nas listas suspensas no hello canto inferior direito.
1. Selecione **nenhuma final de linha** para a lista suspensa da esquerda hello.
1. Selecione **115200 baud** para a lista suspensa à direita de saudação.
1. Na caixa de entrada hello localizada na parte superior de saudação da janela do monitor serial hello, digite Olá informações a seguir se você for solicitado tooprovide-los e, em seguida, clique em **enviar**.
   * SSID Wi-Fi
   * Senha de Wi-Fi
   * Cadeia de conexão de dispositivo

> [!Note]
> Olá credenciais são armazenadas no hello EEPROM de Sparkfun ESP8266 coisa propósitos de dispositivos Se você clicar em um botão redefinição Olá Olá placa Sparkfun ESP8266 coisa Dev, aplicativo de exemplo hello pergunta se você deseja informações de saudação do tooerase. Digite `Y` toohave informações de saudação apagados e você será solicitado tooprovide informações de saudação novamente.

### <a name="verify-hello-sample-application-is-running-successfully"></a>Verifique se o aplicativo de exemplo hello é executado com êxito

Se você vir seguinte Olá saída da janela do monitor serial hello e Olá piscando LED no desenvolvimento de coisa ESP8266 Sparkfun, o aplicativo de exemplo hello está em execução com êxito.

![saída final no ide arduino](media/iot-hub-sparkfun-thing-dev-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a>Próximas etapas

Você conectado a um hub de IoT tooyour Sparkfun ESP8266 coisa desenvolvimento e enviados Olá capturado sensor dados tooyour IoT hub com êxito. 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
