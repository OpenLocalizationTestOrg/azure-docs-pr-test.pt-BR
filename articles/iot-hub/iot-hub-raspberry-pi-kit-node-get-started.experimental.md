---
title: aaaRaspberry Pi toocloud (Node. js) - conectar framboesa Pi tooAzure IoT Hub | Microsoft Docs
description: Conecte-se framboesa Pi tooAzure IoT Hub para Pi framboesa toosend dados toohello nuvem do Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure iot framboesa pi, framboesa pi iot hub, framboesa pi enviar dados toocloud, framboesa pi toocloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: b0e14bfa-8e64-440a-a6ec-e507ca0f76ba
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/27/2017
ms.author: xshi
ms.openlocfilehash: 07bc66983c427eab8118be18d91abb25deb03ad3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-nodejs"></a>Conecte-se framboesa Pi tooAzure IoT Hub (Node. js)

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

Neste tutorial, você começar a aprender Noções básicas de saudação do trabalho com Pi framboesa que está executando Raspbian. Em seguida, você aprenderá como tooseamlessly se conectar a sua nuvem de toohello dispositivos usando [Azure IoT Hub](iot-hub-what-is-iot-hub.md). Para obter exemplos do Windows 10 IoT Core, vá toohello [Centro de desenvolvimento do Windows](http://www.windowsondevices.com/).

Não tem um dispositivo ainda? Tente Olá [emulador framboesa Pi 3](https://blogs.msdn.microsoft.com/iliast/2016/11/10/how-to-emulate-raspberry-pi/). Ou compre um novo kit de [aqui](https://azure.microsoft.com/develop/iot/starter-kits).

## <a name="what-you-do"></a>O que fazer

* Instale o Raspberry Pi.
* Crie um Hub IoT.
* Registre um dispositivo para o Pi em seu Hub IoT.
* Execute um aplicativo de exemplo no hub IoT tooyour de dados do Pi toosend sensor.

Conecte-se o hub IoT do Pi framboesa tooan que você criar. Em seguida, executar um aplicativo de exemplo em dados de temperatura e umidade toocollect Pi a partir de um sensor BME280. Por fim, você pode enviar hub IoT do hello sensor dados tooyour.

## <a name="what-you-learn"></a>O que você aprenderá

* Como toocreate um hub IoT do Azure e obter sua nova cadeia de caracteres de conexão do dispositivo.
* Como tooconnect Pi com um sensor BME280.
* Como os dados do sensor toocollect executando um aplicativo de exemplo no Pi.
* Como hub IoT do toosend sensor dados tooyour.

## <a name="what-you-need"></a>O que você precisa

![O que você precisa](media/iot-hub-raspberry-pi-kit-node-get-started/0_starter_kit.jpg)

* Olá framboesa Pi 2 ou 3 de Pi framboesa quadro.
* Uma assinatura ativa do Azure. Se não tiver uma conta do Azure, [crie uma conta de avaliação gratuita do Azure](https://azure.microsoft.com/free/) em apenas alguns minutos.
* Um monitor, um USB teclado e mouse que se conectam tooPi.
* Um Mac ou PC que esteja executando Windows ou Linux.
* Uma conexão com a Internet.
* Um cartão microSD de 16 GB ou superior.
* Um SD USB adaptador ou microSD cartão tooburn Olá imagem do sistema operacional em um cartão microSD de saudação.
* Fornecer uma potência de 2 amp volt 5 cabo micro-6 pés hello.

Olá itens a seguir é opcional:

* Um sensor de umidade, temperatura e pressão Adafruit BME280 montado.
* Uma placa universal.
* Cabos de jumper fêmea/macho de 15,2 cm.
* Um LED de 10 mm difuso.

  > [!NOTE] 
  Esses itens são opcionais, porque o suporte de exemplo de código Olá simulados dados do sensor.

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a>Instalar o Raspberry Pi

### <a name="install-hello-raspbian-operating-system-for-pi"></a>Instalar o sistema de operacional Raspbian Olá para Pi

Prepare um cartão microSD de saudação para a instalação da imagem de Raspbian hello.

1. Baixe o Raspbian.
   1. [Baixar Raspbian Jessie com Pixel](https://www.raspberrypi.org/downloads/raspbian/) (arquivo. zip de saudação).
   1. Extrai Olá Raspbian imagem tooa pasta do computador.
1. Instale Raspbian toohello microSD cartão.
   1. [Baixe e instale o utilitário de gravador Olá Etcher SD cartão](https://etcher.io/).
   1. Execute Etcher e selecione a imagem de Raspbian de saudação extraído na etapa 1.
   1. Selecione a unidade de cartão microSD hello. Observe que Etcher talvez já selecionou unidade correta hello.
   1. Clique em Flash tooinstall Raspbian toohello microSD cartão.
   1. Remova o cartão microSD de saudação do seu computador quando a instalação for concluída. É cartão de microSD tooremove seguro Olá diretamente porque Etcher automaticamente ejeta ou desmonta cartão microSD de saudação após a conclusão.
   1. Inserir cartão microSD de saudação Pi.

### <a name="enable-ssh-and-i2c"></a>Habilitar SSH e I2C

1. Conecte-se o monitor de toohello de Pi, teclado e mouse, iniciar Pi e, em seguida, faça logon em Raspbian usando `pi` como nome de usuário hello e `raspberry` como senha hello.
1. Clique em Olá ícone framboesa > **preferências** > **framboesa Pi configuração**.

   ![menu de preferências Raspbian Olá](media/iot-hub-raspberry-pi-kit-node-get-started/1_raspbian-preferences-menu.png)

1. Em Olá **Interfaces** guia, defina **I2C** e **SSH** muito**habilitar**e, em seguida, clique em **Okey**. Se você não tiver sensores físicos e deseja que os dados do sensor toouse simulada, esta etapa é opcional.

   ![Habilitar I2C e SSH no Raspberry Pi](media/iot-hub-raspberry-pi-kit-node-get-started/2_enable-i2c-ssh-on-raspberry-pi.png)

> [!NOTE] 
tooenable SSH e I2C, você pode encontrar mais documentos de referência na [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) e [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).

### <a name="connect-hello-sensor-toopi"></a>Conecte-se Olá sensor tooPi

Use Olá breadboard e jumper fios tooconnect um LED e um tooPi BME280 da seguinte maneira. Se você não tiver o sensor hello, ignore esta seção.

![Olá framboesa Pi e o sensor de conexão](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

sensor de saudação BME280 pode coletar dados de temperatura e umidade. E Olá LED pisca se houver uma comunicação entre o dispositivo e hello nuvem. 

Pinos do sensor, use Olá fiação a seguir:

| Início (Sensor e LED)     | End (quadro)            | Cor de cabo   |
| -----------------------  | ---------------------- | ------------: |
| VDD (pino 5G)             | 3,3 v PWR (pino 1)       | Cabo branco   |
| GND (pino 7G)             | GND (pino 6)            | Cabo marrom   |
| SCK (pino 8G)             | I2C1 SDA (pino 3)       | Cabo laranja  |
| SDI (pino 10G)            | I2C1 SCL (pino 5)       | Cabo vermelho     |
| LED VDD (pino 18F)        | GPIO 24 (pino 18)       | Cabo branco   |
| LED GND (pino 17F)        | GND (pino 20)           | Cabo preto   |

Clique em tooview [framboesa Pi 2 e 3 mapeamentos de Pin](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) para referência.

Depois de se conectar com êxito BME280 tooyour framboesa Pi, ele deve ser como abaixo de imagem.

![Pi e BME280 conectados](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a>Conectar a rede de toohello Pi

Ative o Pi usando cabo USB da micro hello e fonte de alimentação hello. Use Olá Ethernet cabo tooconnect Pi tooyour com fio de rede ou siga Olá [instruções de saudação framboesa Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) rede sem fio do tooyour tooconnect Pi. Após o Pi rede toohello conectado com êxito, você precisa tootake nota da saudação [endereço IP do seu Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).

![Rede toowired conectado](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> Certifique-se de Pi é conectado toohello mesmo de rede do computador. Por exemplo, se o computador estiver rede sem fio conectada tooa enquanto Pi é conectado tooa rede com fio, talvez você não veja Olá IP endereço na saída de devdisco hello.

## <a name="run-a-sample-application-on-pi"></a>Executar um aplicativo de exemplo no Pi

### <a name="clone-sample-application-and-install-hello-prerequisite-packages"></a>Clonar um aplicativo de exemplo e instalar pacotes de pré-requisito Olá

1. Use um dos Olá seguir SSH clientes de sua tooyour de tooconnect do computador host framboesa Pi.
    - [PuTTY](http://www.putty.org/) para Windows. Você precisa Olá endereço IP de seu tooconnect Pi-los por meio do SSH.
    - Olá SSH do cliente interno Ubuntu ou macOS. Você pode precisar executar `ssh pi@<ip address of pi>` tooconnect Pi via SSH.

   > [!NOTE] 
   é o nome de usuário do saudação padrão `pi` , e a senha de saudação é `raspberry`.

1. Instale o Node. js e NPM tooyour Pi.
   
   Primeiro você deve verificar a versão do Node. js com hello comando a seguir. 
   
   ```bash
   node -v
   ```

   Se Olá versão for inferior a 4. x ou não há nenhum Node. js no seu Pi, em seguida, executar Olá tooinstall de comando a seguir ou atualizar Node. js.

   ```bash
   curl -sL http://deb.nodesource.com/setup_4.x | sudo -E bash
   sudo apt-get -y install nodejs
   ```

1. Aplicativo de exemplo hello executando o comando a seguir de saudação do clone:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-client-app
   ```

1. Instale todos os pacotes de saudação comando a seguir. Ele inclui o SDK do dispositivo IoT do Azure, a biblioteca do Sensor BME280 e a biblioteca de fiação do Pi.

   ```bash
   cd iot-hub-node-raspberrypi-client-app
   sudo npm install
   ```
   > [!NOTE] 
   Pode levar vários toofinish de minutos esse denpening do processo de instalação na sua conexão de rede.

### <a name="configure-hello-sample-application"></a>Configurar o aplicativo de exemplo hello

1. Abra o arquivo de configuração de saudação executando Olá comandos a seguir:

   ```bash
   nano config.json
   ```

   ![Arquivo de configuração](media/iot-hub-raspberry-pi-kit-node-get-started/6_config-file.png)

   Há dois itens que podem ser configurados nesse arquivo. Olá primeiro um é `interval`, que define o intervalo de tempo de saudação entre duas mensagens que enviar toocloud. Olá segunda `simulatedData`, que é um valor booleano para se toouse simulados dados do sensor ou não.

   Se você **não tem o sensor Olá**, defina hello `simulatedData` valor muito`true` aplicativo de exemplo hello toomake criar e usar dados de sensor simulada.

1. Salve e saia pressionando CTRL+O > ENTER > CTRL+X.

### <a name="run-hello-sample-application"></a>Executar o aplicativo de exemplo hello

1. Execute o aplicativo de exemplo hello executando Olá comando a seguir:

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   Verifique se você copiar e colar cadeia de caracteres de conexão de dispositivo Olá em aspas hello.


Você verá a seguinte Olá saída mostra Olá sensor dados e hello mensagens enviadas tooyour IoT hub.

![Saída - dados de sensor enviadas do Pi framboesa tooyour hub IoT](media/iot-hub-raspberry-pi-kit-node-get-started/8_run-output.png)

## <a name="next-steps"></a>Próximas etapas

Executar dados de sensor de toocollect do aplicativo de exemplo e enviá-lo tooyour IoT hub.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]