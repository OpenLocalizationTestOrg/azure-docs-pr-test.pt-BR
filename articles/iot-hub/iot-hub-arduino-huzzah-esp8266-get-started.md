---
title: "aaaESP8266 toocloud - conectar o difusão HUZZAH ESP8266 tooAzure IoT Hub | Microsoft Docs"
description: "Saiba como toosetup e conecte-se Adafruit difusão HUZZAH ESP8266 tooAzure IoT Hub para ele plataforma de nuvem do Azure toosend dados toohello neste tutorial."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: c505aacf-89a8-40ed-a853-493b75bec524
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: xshi
ms.openlocfilehash: 44fd47232488948d21c7aa71bdd865397e41e63e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-huzzah-esp8266-tooazure-iot-hub-in-hello-cloud"></a>Conecte-se Adafruit difusão HUZZAH ESP8266 tooAzure IoT Hub na nuvem Olá

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Conexão entre o DHT22, o Feather HUZZAH ESP8266 e o Hub IoT](media/iot-hub-arduino-huzzah-esp8266-get-started/1_connection-hdt22-feather-huzzah-iot-hub.png)

## <a name="what-you-do"></a>O que fazer


Conecte-se Adafruit difusão HUZZAH ESP8266 tooan IoT hub que você criar. Em seguida, execute um aplicativo de exemplo no ESP8266 toocollect Olá temperatura e umidade os dados de um sensor DHT22. Por fim, você pode enviar hub IoT do hello sensor dados tooyour.

> [!NOTE]
> Se você estiver usando outras placas ESP8266, você ainda pode seguir estas etapas tooconnect-tooyour IoT hub. Dependendo da placa Olá ESP8266 você está usando, talvez seja necessário Olá tooreconfigure `LED_PIN`. Por exemplo, se você estiver usando ESP8266 do AI Thinker, você pode alterá-la de `0` muito`2`. Não tem um dispositivo ainda? Obtê-lo do hello [site do Azure](http://azure.com/iotstarterkits).




## <a name="what-you-learn"></a>O que você aprenderá

* Como toocreate um hub IoT e registrar um dispositivo para difusão HUZZAH ESP8266
* Como tooconnect difusão HUZZAH ESP8266 com sensor hello e seu computador
* Como os dados do sensor toocollect executando um aplicativo de exemplo em difusão HUZZAH ESP8266
* Como toosend Olá hub IoT do sensor dados tooyour

## <a name="what-you-need"></a>O que você precisa

![Partes necessárias para o tutorial Olá](media/iot-hub-arduino-huzzah-esp8266-get-started/2_parts-needed-for-the-tutorial.png)

toocomplete essa operação, você precisa Olá seguir partes de seu difusão HUZZAH ESP8266 Starter Kit:

* Olá difusão HUZZAH ESP8266 board
* Um tooType Micro USB um cabo

Você também precisa Olá coisas para seu ambiente de desenvolvimento a seguir:

* Uma assinatura ativa do Azure. Se não tiver uma conta do Azure, [crie uma conta de avaliação gratuita do Azure](https://azure.microsoft.com/free/) em apenas alguns minutos.
* Mac ou PC que esteja executando o Windows ou Ubuntu.
* Rede sem fio para difusão HUZZAH ESP8266 tooconnect para.
* Ferramenta de configuração saudação do toodownload de conexão de Internet.
* [IDE do Arduino](https://www.arduino.cc/en/main/software) versão 1.6.8 ou posterior. Versões anteriores não funcionam com a biblioteca de AzureIoT hello.

Olá itens a seguir são opcionais no caso de você não tiver um sensor. Você também tem a opção de saudação do uso de dados de sensor simulada.

* Um sensor de temperatura e umidade Adafruit DHT22
* Uma placa universal
* Cabos de jumper de M/M


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-huzzah-esp8266-with-hello-sensor-and-your-computer"></a>Conecte-se a difusão HUZZAH ESP8266 com sensor hello e seu computador
Nesta seção, você se conectar a placa de tooyour sensores hello. Em seguida, você conecta o computador tooyour de dispositivo para uso posterior.
### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-huzzah-esp8266"></a>Conecte-se um DHT22 temperatura e umidade sensor tooFeather HUZZAH ESP8266

Use Olá breadboard e jumper fios toomake Olá conexão da seguinte maneira. Se você não tiver um sensor, ignore esta seção porque você pode usar dados de sensor simulado em vez disso.

![Referência de conexões](media/iot-hub-arduino-huzzah-esp8266-get-started/15_connections_on_breadboard.png)


Pinos do sensor, use Olá fiação a seguir:


| Início (Sensor)           | End (quadro)           | Cor de cabo   |
| -----------------------  | ---------------------- | ------------: |
| VDD (Pin 31F)            | 3V (Fixar 58H)           | Cabo vermelho     |
| DADOS de (Pin 32F)           | GPIO 2 (Pin 46A)       | Cabo azul    |
| GND (Pin 34F)            | GND (PIn 56I)          | Cabo preto   |

Para obter mais informações, consulte [Instalação do sensor Adafruit DHT22](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) e [Pinagem do Adafruit Feather HUZZAH Esp8266](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).



Agora seu Feather Huzzah ESP8266 deve estar conectado a um sensor ativo.

![Conectar o DHT22 ao Feather Huzzah](media/iot-hub-arduino-huzzah-esp8266-get-started/8_connect-dht22-feather-huzzah.png)

### <a name="connect-feather-huzzah-esp8266-tooyour-computer"></a>Conectar difusão HUZZAH ESP8266 tooyour computador

Como mostrado a seguir, use Olá Micro USB tooType USB um cabo tooconnect difusão HUZZAH ESP8266 tooyour computador.

![Conectar o computador de tooyour Huzzah de difusão](media/iot-hub-arduino-huzzah-esp8266-get-started/9_connect-feather-huzzah-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a>Adicionar permissões de porta serial (somente Ubuntu)


Se você usar Ubuntu, verifique se que você tem Olá permissões toooperate em Olá USB porta da difusão HUZZAH ESP8266. permissões de porta serial tooadd, siga estas etapas:


1. Olá executar comandos em um terminal a seguir:

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   Você obtém uma saudação saídas a seguir:

   * crw-rw---- 1 root uucp xxxxxxxx
   * crw-rw---- 1 root dialout xxxxxxxx

   Na saída de hello, observe que `uucp` ou `dialout` é o nome de proprietário do grupo de saudação do hello porta USB.

1. Adicione grupo de toohello de usuários de saudação executando Olá comando a seguir:

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   `<group-owner-name>`é o nome de proprietário de grupo Olá que você obteve na etapa anterior hello. `<username>` é o nome de usuário do Ubuntu.

1. Saia do Ubuntu e entrar novamente para Olá tooappear de alteração.

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a>Coletar dados de sensor e enviá-lo tooyour IoT hub

Nesta seção, implante e execute um aplicativo de exemplo em Feather HUZZAH ESP8266. aplicativo de exemplo Hello pisca Olá LED em difusão HUZZAH ESP8266 e envia a temperatura hello e umidade os dados coletados de saudação DHT22 sensor tooyour hub IoT.

### <a name="get-hello-sample-application-from-github"></a>Obter o aplicativo de exemplo hello do GitHub

aplicativo de exemplo Hello está hospedado no GitHub. Clone o repositório de exemplo hello que contém o aplicativo de exemplo de saudação do GitHub. repositório de exemplo hello tooclone, siga estas etapas:

1. Abra um prompt de comando ou uma janela de terminal.
1. Vá tooa pasta onde você deseja toobe de aplicativo de exemplo hello armazenado.
1. Execute Olá comando a seguir:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-feather-huzzah-client-app.git
   ```

Instale o pacote de saudação para difusão HUZZAH ESP8266 em Olá Arduino IDE:

1. Abra a pasta de saudação onde o aplicativo de exemplo hello está armazenado.
1. Abra o arquivo de app.ino de saudação na pasta de aplicativo Olá Olá Arduino IDE.

   ![Abra o aplicativo de exemplo hello Arduino IDE](media/iot-hub-arduino-huzzah-esp8266-get-started/10_arduino-ide-open-sample-app.png)

1. No hello Arduino IDE, clique em **arquivo** > **preferências**.
1. Em Olá **preferências** caixa de diálogo, clique em Olá ícone próximo toohello **URLs adicionais do Gerenciador de quadros** caixa.
1. Na janela pop-up do hello, digite Olá URL a seguir e, em seguida, clique em **Okey**.

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![Url do pacote de ponto tooa Arduino IDE](media/iot-hub-arduino-huzzah-esp8266-get-started/11_arduino-ide-package-url.png)

1. Em Olá **preferência** caixa de diálogo, clique em **Okey**.
1. Clique em **Ferramentas** > **Placa** > **Gerenciador de Placas** e procure esp8266.

   O Gerenciador de Placas indica que ESP8266 com uma versão 2.2.0 ou posterior está instalado.

   ![Olá esp8266 pacote está instalado](media/iot-hub-arduino-huzzah-esp8266-get-started/12_arduino-ide-esp8266-installed.png)

1. Clique em **ferramentas** > **placa** > **Adafruit HUZZAH ESP8266**.

### <a name="install-necessary-libraries"></a>Instalar as bibliotecas necessárias

1. No hello Arduino IDE, clique em **esboço** > **biblioteca incluem** > **gerenciar bibliotecas**.
1. Pesquisar Olá uma nomes de bibliotecas a seguir. Para cada biblioteca que você localizar, clique em **Instalar**.
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a>Você não tem um sensor DHT22 real?

aplicativo de exemplo Hello pode simular a temperatura e umidade dados caso você não tenha um sensor DHT22 real. tooset backup de dados de toouse simulada de aplicativo de exemplo hello, siga estas etapas:

1. Olá abrir `config.h` arquivo hello `app` pasta.
1. Localize Olá a seguinte linha de código e altere o valor de saudação de `false` muito`true`:
   ```c
   define SIMULATED_DATA true
   ```
   ![Configurar dados de toouse simulada de aplicativo de exemplo hello](media/iot-hub-arduino-huzzah-esp8266-get-started/13_arduino-ide-configure-app-use-simulated-data.png)

1. Salve o arquivo hello com `Control-s`.

### <a name="deploy-hello-sample-application-toofeather-huzzah-esp8266"></a>Implantar tooFeather de aplicativo de exemplo hello HUZZAH ESP8266

1. No hello Arduino IDE, clique em **ferramenta** > **porta**e, em seguida, clique em porta serial Olá para difusão HUZZAH ESP8266.
1. Clique em **esboço** > **carregar** toobuild e implantar tooFeather de aplicativo de exemplo hello HUZZAH ESP8266.

### <a name="enter-your-credentials"></a>Inserir suas credenciais

Olá após o carregamento for concluído com êxito, siga estas etapas tooenter suas credenciais:

1. No hello Arduino IDE, clique em **ferramentas** > **Serial Monitor**.
1. Na janela do monitor serial hello, observe Olá dois nas listas suspensas no canto inferior direito de saudação.
1. Selecione **nenhuma final de linha** para a lista suspensa da esquerda hello.
1. Selecione **115200 baud** para a lista suspensa à direita de saudação.
1. Na caixa de entrada hello localizada na parte superior de saudação da janela do monitor serial hello, digite Olá informações a seguir se você for solicitado tooprovide-los e, em seguida, clique em **enviar**.
   * SSID Wi-Fi
   * Senha de Wi-Fi
   * Cadeia de conexão de dispositivo

> [!Note]
> Olá credenciais são armazenadas no hello EEPROM de difusão HUZZAH ESP8266. Se você clicar em um botão Redefinir Olá Olá difusão HUZZAH ESP8266 board, aplicativo de exemplo hello pergunta se você deseja informações de saudação do tooerase. Digite `Y` toohave informações de saudação apagadas. Você será solicitado a informações de saudação tooprovide uma segunda vez.

### <a name="verify-hello-sample-application-is-running-successfully"></a>Verifique se o aplicativo de exemplo hello é executado com êxito

Se você vir seguinte Olá saída da janela do monitor serial hello e Olá piscando LED em difusão HUZZAH ESP8266, o aplicativo de exemplo hello está em execução com êxito.

![Saída final no IDE do Arduino](media/iot-hub-arduino-huzzah-esp8266-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a>Próximas etapas

E com sucesso conectado a um hub de IoT difusão HUZZAH ESP8266 tooyour, enviado Olá capturado sensor dados tooyour IoT hub. 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

