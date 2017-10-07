---
title: aaaRaspberry Pi toocloud (Python) - conectar framboesa Pi tooAzure IoT Hub | Microsoft Docs
description: Saiba como toosetup e conecte-se framboesa Pi tooAzure IoT Hub para a plataforma de nuvem do Azure framboesa Pi toosend dados toohello neste tutorial.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: Azure iot framboesa pi, framboesa pi iot hub, framboesa pi enviar dados toocloud, framboesa pi toocloud
ms.service: iot-hub
ms.devlang: python
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/31/2017
ms.author: xshi
ms.openlocfilehash: 86f5c91ab9dd4e23c563437827fb7d2d06916d2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-python"></a>Conecte-se framboesa Pi tooAzure IoT Hub (Python)

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

Neste tutorial, você começar a aprender Noções básicas de saudação do trabalho com Pi framboesa que está executando Raspbian. Em seguida, você aprenderá como tooseamlessly se conectar a sua nuvem de toohello dispositivos usando [Azure IoT Hub](iot-hub-what-is-iot-hub.md). Para obter exemplos do Windows 10 IoT Core, vá toohello [Centro de desenvolvimento do Windows](http://www.windowsondevices.com/).

Não tem um dispositivo ainda? Experimente [Simulador online Raspberry Pi](iot-hub-raspberry-pi-web-simulator-get-started.md). Ou compre um novo kit de [aqui](https://azure.microsoft.com/develop/iot/starter-kits).

## <a name="what-you-do"></a>O que fazer

* Crie um Hub IoT.
* Registre um dispositivo para o Pi em seu Hub IoT.
* Instale o Raspberry Pi.
* Execute um aplicativo de exemplo no hub IoT tooyour de dados do Pi toosend sensor.

Conecte-se o hub IoT do Pi framboesa tooan que você criar. Em seguida, executar um aplicativo de exemplo em dados de temperatura e umidade toocollect Pi a partir de um sensor BME280. Por fim, você pode enviar hub IoT do hello sensor dados tooyour.

## <a name="what-you-learn"></a>O que você aprenderá

* Como toocreate um hub IoT do Azure e obter sua nova cadeia de caracteres de conexão do dispositivo.
* Como tooconnect Pi com um sensor BME280.
* Como os dados do sensor toocollect executando um aplicativo de exemplo no Pi.
* Como hub IoT do toosend sensor dados tooyour.

## <a name="what-you-need"></a>O que você precisa

![O que você precisa](media/iot-hub-raspberry-pi-kit-c-get-started/0_starter_kit.jpg)

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

## <a name="set-up-raspberry-pi"></a>Configurar o Raspberry Pi

### <a name="install-hello-raspbian-operating-system-for-pi"></a>Instalar o sistema de operacional Raspbian Olá para Pi

Prepare um cartão microSD de saudação para a instalação da imagem de Raspbian hello.

1. Baixe o Raspbian.
   1. [Baixar Raspbian Jessie com área de trabalho](https://www.raspberrypi.org/downloads/raspbian/) (arquivo. zip de saudação).
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

   ![menu de preferências Raspbian Olá](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. Em Olá **Interfaces** guia, defina **I2C** e **SSH** muito**habilitar**e, em seguida, clique em **Okey**. Se você não tiver sensores físicos e deseja que os dados do sensor toouse simulada, esta etapa é opcional.

   ![Habilitar I2C e SSH no Raspberry Pi](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
tooenable SSH e I2C, você pode encontrar mais documentos de referência na [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) e [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).

### <a name="connect-hello-sensor-toopi"></a>Conecte-se Olá sensor tooPi

Use Olá breadboard e jumper fios tooconnect um LED e um tooPi BME280 da seguinte maneira. Se você não tiver um sensor Olá [ignore esta seção](#connect-pi-to-the-network).

![Olá framboesa Pi e o sensor de conexão](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

sensor de saudação BME280 pode coletar dados de temperatura e umidade. E Olá LED pisca se houver uma comunicação entre o dispositivo e hello nuvem. 

Pinos do sensor, use Olá fiação a seguir:

| Início (Sensor e LED)     | End (quadro)            | Cor de cabo   |
| -----------------------  | ---------------------- | ------------: |
| VDD (pino 5G)             | 3,3 v PWR (pino 1)       | Cabo branco   |
| GND (pino 7G)             | GND (pino 6)            | Cabo marrom   |
| SDI (pino 10G)            | I2C1 SDA (pino 3)       | Cabo vermelho     |
| SCK (pino 8G)             | I2C1 SCL (pino 5)       | Cabo laranja  |
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

### <a name="install-hello-prerequisite-packages"></a>Instalar pacotes de pré-requisito Olá

Use um dos Olá seguir SSH clientes de sua tooyour de tooconnect do computador host framboesa Pi.
   
   **Usuários do Windows**
   1. Baixe e instale o [PuTTY](http://www.putty.org/) para Windows. 
   1. Copie o endereço IP de saudação da seção Pi em nome de Host de hello (ou endereço IP) e selecione SSH como tipo de conexão de saudação.
   
   
   **Usuários de Mac e do Ubuntu**
   
   Use o cliente SSH interno de saudação no Ubuntu ou macOS. Talvez seja necessário toorun `ssh pi@<ip address of pi>` tooconnect Pi via SSH.
   > [!NOTE] 
   é o nome de usuário do saudação padrão `pi` , e a senha de saudação é `raspberry`.


### <a name="configure-hello-sample-application"></a>Configurar o aplicativo de exemplo hello

1. Aplicativo de exemplo hello executando o comando a seguir de saudação do clone:

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-python-raspberrypi-client-app.git
   ```
1. Abra o arquivo de configuração de saudação executando Olá comandos a seguir:

   ```bash
   cd iot-hub-python-raspberrypi-client-app
   nano config.py
   ```

   Há cinco macros nesse arquivo que você pode configurar. Olá primeiro um é `MESSAGE_TIMESPAN`, que define o intervalo de tempo de saudação (em milissegundos) entre duas mensagens que enviar toocloud. Olá segunda `SIMULATED_DATA`, que é um valor booleano para se toouse simulados dados do sensor ou não. `I2C_ADDRESS`é o endereço de saudação I2C que seu sensor BME280 está conectado. `GPIO_PIN_ADDRESS`é o endereço GPIO de saudação para o LED. Olá última um é `BLINK_TIMESPAN`, que definido timespan hello quando o LED estiver ativado em milissegundos.

   Se você **não tem o sensor Olá**, defina hello `SIMULATED_DATA` valor muito`True` aplicativo de exemplo hello toomake criar e usar dados de sensor simulada.

1. Salve e saia pressionando CTRL+O > ENTER > CTRL+X.

### <a name="build-and-run-hello-sample-application"></a>Compilar e executar o aplicativo de exemplo hello

1. Crie um aplicativo de exemplo hello executando o comando a seguir de saudação. Como Olá SDKs IoT do Azure para Python são wrappers sobre hello Azure IoT dispositivo C SDK, você precisará bibliotecas de saudação C toocompile se você quiser ou precisar toogenerate bibliotecas de Python de saudação do código-fonte.

   ```bash
   sudo chmod u+x setup.sh
   sudo ./setup.sh
   ```
   > [!NOTE] 
   Você também pode especificar a versão de hello deseja executando `sudo ./setup.sh [--python-version|-p] [2.7|3.4|3.5]`. Se você executar o script sem o parâmetro, o script hello detectará automaticamente versão de saudação do python instalado (sequência de pesquisa 2.7 -> 3.4 -> 3.5). Verifique se a versão do Python se mantém consistente durante a compilação e a execução. 
   
   > [!NOTE] 
   Sobre a criação de biblioteca de cliente do Python hello (iothub_client.so) em dispositivos de Linux que têm menos de 1GB de RAM, você poderá ver presas em 98% durante a compilação iothub_client_python.cpp, conforme mostrado abaixo de compilação `[ 98%] Building CXX object python/src/CMakeFiles/iothub_client_python.dir/iothub_client_python.cpp.o`. Se você tiver esse problema, verifique o consumo de memória de saudação da saudação dispositivo usando `free -m command` em outra janela de terminal durante esse período. Se você estiver executando sem memória ao compilar o arquivo iothub_client_python.cpp, você pode ter tootemporarily aumentar tooget de espaço de permuta Olá toosuccessfully de memória disponível mais criar biblioteca SDK do dispositivo de saudação do cliente do Python.
   
1. Execute o aplicativo de exemplo hello executando Olá comando a seguir:

   ```bash
   python app.py '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   Verifique se você copiar e colar cadeia de caracteres de conexão de dispositivo Olá em aspas hello. E se você usar o python Olá 3, você pode usar o comando de Olá `python3 app.py '<your Azure IoT hub device connection string>'`.


   Você verá a seguinte Olá saída mostra Olá sensor dados e hello mensagens enviadas tooyour IoT hub.

   ![Saída - dados de sensor enviadas do Pi framboesa tooyour hub IoT](media/iot-hub-raspberry-pi-kit-c-get-started/success.png
)

## <a name="next-steps"></a>Próximas etapas

Executar dados de sensor de toocollect do aplicativo de exemplo e enviá-lo tooyour IoT hub. mensagens de saudação toosee que o Pi framboesa enviou tooyour IoT hub ou enviar mensagens tooyour framboesa Pi em uma interface de linha de comando, consulte Olá [gerenciar nuvem dispositivo mensagens com o tutorial do Gerenciador de Hub IOT](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
