---
title: aaaIntel Edison toocloud (Node. js) - conectar Intel Edison tooAzure IoT Hub | Microsoft Docs
description: Saiba como toosetup e conecte-se a Intel Edison tooAzure IoT Hub para a plataforma de nuvem do Azure Edison Intel toosend dados toohello neste tutorial.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: Azure iot intel edison, intel hub iot de edison, intel edison enviar dados toocloud, intel toocloud edison
ms.assetid: a7c9cf2d-c102-41b0-aa45-41285c6877eb
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 6/15/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bfc3387efc532b4b83f0626a9cf61d12c2952af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-intel-edison-tooazure-iot-hub-nodejs"></a>Conecte-se Intel Edison tooAzure IoT Hub (Node. js)

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

Neste tutorial, você começar a aprender os fundamentos de saudação do trabalho com Intel Edison. Em seguida, você aprenderá como tooseamlessly se conectar a sua nuvem de toohello dispositivos usando [Azure IoT Hub](iot-hub-what-is-iot-hub.md).

Não tem um dispositivo ainda? Comece [aqui](https://azure.microsoft.com/develop/iot/starter-kits)

## <a name="what-you-do"></a>O que fazer

* Configure os módulos do Intel Edison e do Grove.
* Crie um Hub IoT.
* Registre um dispositivo para o Edison em seu Hub IoT.
* Execute um aplicativo de exemplo no hub IoT tooyour de dados do Edison toosend sensor.

Conecte-se o hub IoT do Intel Edison tooan que você criar. Em seguida, você executar um aplicativo de exemplo em Edison toocollect temperatura e umidade dados de um sensor de temperatura Grove. Por fim, você pode enviar hub IoT do hello sensor dados tooyour.

## <a name="what-you-learn"></a>O que você aprenderá

* Como toocreate um hub IoT do Azure e obter sua nova cadeia de caracteres de conexão do dispositivo.
* Como tooconnect Edison com um sensor de temperatura Grove.
* Como os dados do sensor toocollect executando um aplicativo de exemplo no Edison.
* Como hub IoT do toosend sensor dados tooyour.

## <a name="what-you-need"></a>O que você precisa

![O que você precisa](media/iot-hub-intel-edison-kit-node-get-started/0_kit.png)

* Olá placa Edison Intel
* Placa de expansão Arduino
* Uma assinatura ativa do Azure. Se não tiver uma conta do Azure, [crie uma conta de avaliação gratuita do Azure](https://azure.microsoft.com/free/) em apenas alguns minutos.
* Um Mac ou PC que esteja executando Windows ou Linux.
* Uma conexão com a Internet.
* Um tooType Micro B um cabo
* Uma fonte de alimentação CC (corrente contínua). A fonte de alimentação deve ser classificada da seguinte maneira:
  - 7-15V CC
  - Pelo menos 1500 mA
  - pin do Hello center/interna deve ser Olá positivo polos Olá de fonte de alimentação

Olá itens a seguir é opcional:

* Grove Base Shield V2
* Grove - Sensor de temperatura
* Cabo do Grove
* Qualquer barras espaçador ou parafusos incluídos no pacote hello, incluindo a placa de expansão dois parafusos toofasten Olá módulo toohello e quatro conjuntos de parafusos e espaçadores plásticos.

> [!NOTE] 
Esses itens são opcionais, porque o suporte de exemplo de código Olá simulados dados do sensor.

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-intel-edison"></a>Configurar o Intel Edison

### <a name="assemble-your-board"></a>Montar sua placa

Esta seção contém etapas tooattach sua placa de expansão Intel® Edison tooyour de módulo.

1. Coloque o módulo de Intel® Edison de saudação dentro da estrutura de tópicos Olá branca em seu quadro de expansão, alinhado buracos Olá no módulo Olá com parafusos Olá na placa de expansão de saudação.

2. Pressione módulo Olá logo abaixo palavras Olá `What will you make?` até que você se sentir um snapshot.

   ![montar a placa 2](media/iot-hub-intel-edison-kit-node-get-started/1_assemble_board2.jpg)

3. Use Olá dois porcas hexadecimal (incluídos no pacote de saudação) toosecure Olá módulo toohello expansão quadro.

   ![montar a placa 3](media/iot-hub-intel-edison-kit-node-get-started/2_assemble_board3.jpg)

4. Insira um parafuso de uma das quatro furos de canto Olá na placa de expansão de saudação. Gire e reforçar uma espaçadores de plástico Olá branca em parafuso de saudação.

   ![montar a placa 4](media/iot-hub-intel-edison-kit-node-get-started/3_assemble_board4.jpg)

5. Repita para Olá espaçadores outros três canto.

   ![montar a placa 5](media/iot-hub-intel-edison-kit-node-get-started/4_assemble_board5.jpg)

Agora, sua placa está montada.

   ![montar a placa](media/iot-hub-intel-edison-kit-node-get-started/5_assembled_board.jpg)

### <a name="connect-hello-grove-base-shield-and-hello-temperature-sensor"></a>Conecte-se hello Grove base de dados de blindagem e sensor de temperatura Olá

1. Coloque Olá Grove base de dados de blindagem na placa tooyour. Verifique se todos os pinos estão totalmente conectados à sua placa.
   
   ![Grove Base Shield](media/iot-hub-intel-edison-kit-node-get-started/6_grove_base_sheild.jpg)

2. Sensor de temperatura Use Grove cabo tooconnect Grove em Olá Grove base de dados de blindagem **A0** porta.

   ![Conecte-se sensor tootemperature](media/iot-hub-intel-edison-kit-node-get-started/7_temperature_sensor.jpg)

   ![Conexão do Edison e do sensor](media/iot-hub-intel-edison-kit-node-get-started/16_edion_sensor.png)

Agora seu sensor está pronto.

### <a name="power-up-edison"></a>Ligar o Edison

1. Conecte-se na fonte de alimentação hello.

   ![Conectar à fonte de alimentação](media/iot-hub-intel-edison-kit-node-get-started/8_plug_power.jpg)

2. Um LED verde (DS1 em Olá placa de expansão Arduino *) deve acende e permanecer aceso.

3. Aguarde um minuto para Olá quadro toofinish inicialização.

   > [!NOTE]
   > Se você não tiver uma fonte de energia do controlador de domínio, você ainda pode placa de saudação de energia por meio de uma porta USB. Confira a seção `Connect Edison tooyour computer` para obter detalhes. Ligar sua placa dessa maneira pode resultar em um comportamento imprevisível da placa, especialmente ao usar Wi-Fi ou motores de acionamento.

### <a name="connect-edison-tooyour-computer"></a>Conectar o computador de tooyour Edison

1. Alternar para baixo microcomutador Olá até dois o portas USB micro hello, para que Edison está no modo de dispositivo. Veja [aqui](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode) as diferenças entre o modo de dispositivo e o modo de host.

   ![Alternar a saudação microcomutador](media/iot-hub-intel-edison-kit-node-get-started/9_toggle_down_microswitch.jpg)

2. Conecte cabo micro Olá Olá superior micro porta.

   ![Porta micro USB superior](media/iot-hub-intel-edison-kit-node-get-started/10_top_usbport.jpg)

3. Plug Olá outra extremidade do cabo USB em seu computador.

   ![USB do computador](media/iot-hub-intel-edison-kit-node-get-started/11_computer_usb.jpg)

4. Você saberá que a placa foi inicializada completamente quando o computador montar uma nova unidade (muito semelhante a inserir um cartão SD no computador).

## <a name="download-and-run-hello-configuration-tool"></a>Baixe e execute a ferramenta de configuração de saudação
Obter a ferramenta de configuração mais recente saudação do [este link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listado em Olá `Installers` título. Execute a ferramenta hello e execute seu na tela instruções, clicar em próximo, quando necessário

### <a name="flash-firmware"></a>Atualizar o firmware
1. Em Olá `Set up options` , clique em `Flash Firmware`.
2. Selecione Olá tooflash de imagem em seu quadro seguindo um destes procedimentos hello:
   - flash e toodownload seu quadro com hello mais recente firmware imagem disponível da Intel, selecione `Download hello latest image version xxxx`.
   - tooflash seu quadro com uma imagem que você já tiver salvo em seu computador, selecione `Select hello local image`. Procure tooand Olá selecione imagem tooflash tooyour quadro.
3. ferramenta de configuração de saudação tentará tooflash seu quadro. todo o processo de intermitente Olá pode levar too10 minutos.

### <a name="set-password"></a>Definir senha
1. Em Olá `Set up options` , clique em `Enable Security`.
2. É possível definir um nome personalizado para sua placa Intel® Edison. Isso é opcional.
3. Digite uma senha para a placa e clique em `Set password`.
4. Marca uma senha hello, que é usada posteriormente.

### <a name="connect-wi-fi"></a>Conectar ao Wi-Fi
1. Em Olá `Set up options` , clique em `Connect Wi-Fi`. Aguarde o minuto tooone como verificações de seu computador para redes Wi-Fi disponíveis.
2. De saudação `Detected Networks` lista suspensa, selecione sua rede.
3. De saudação `Security` lista suspensa, o tipo de segurança da rede Olá select.
4. Forneça suas informações de logon e senha e clique em `Configure Wi-Fi`.
5. Marca Olá endereço IP, que é usado posteriormente.

> [!NOTE]
> Certifique-se de Edison é conectado toohello mesmo de rede do computador. O computador se conecta a tooyour Edison usando o endereço IP de saudação.

   ![Conecte-se sensor tootemperature](media/iot-hub-intel-edison-kit-node-get-started/12_configuration_tool.png)

Parabéns! Você configurou o Edison com êxito.

## <a name="run-a-sample-application-on-intel-edison"></a>Executar um exemplo de aplicativo no Intel Edison

### <a name="prepare-hello-azure-iot-device-sdk"></a>Preparar Olá SDK de dispositivo IoT do Azure

1. Use um dos Olá seguir SSH clientes de sua tooyour de tooconnect do computador host Edison Intel. endereço IP de saudação é da ferramenta de configuração de saudação e senha de saudação é Olá um que você definiu nessa ferramenta.
    - [PuTTY](http://www.putty.org/) para Windows.
    - Olá SSH do cliente interno Ubuntu ou macOS.

2. Dispositivo de tooyour do aplicativo cliente do clone Olá exemplo. 
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-intel-edison-client-app
   ```

3. Navegue todos os pacotes de saudação do toohello repositório pasta toorun tooinstall de comando a seguir, pode levar serval toocomplete de minutos.
   
   ```bash
   cd iot-hub-node-intel-edison-client-app
   npm install
   ```


### <a name="configure-and-run-hello-sample-application"></a>Configurar e executar o aplicativo de exemplo hello

1. Abra o arquivo de configuração de saudação executando Olá comandos a seguir:

   ```bash
   nano config.json
   ```

   ![Arquivo de configuração](media/iot-hub-intel-edison-kit-node-get-started/13_configure_file.png)

   Há duas macros que você pode configurar nesse arquivo. Olá primeiro um é `INTERVAL`, que define o intervalo de tempo de saudação entre duas mensagens que enviar toocloud. Olá segunda `simulatedData`, que é um valor booleano para se toouse simulados dados do sensor ou não.

   Se você **não tem o sensor Olá**, defina hello `simulatedData` valor muito`true` aplicativo de exemplo hello toomake criar e usar dados de sensor simulada.

1. Salve e saia pressionando CTRL+O > ENTER > CTRL+X.


1. Execute o aplicativo de exemplo hello executando Olá comando a seguir:

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   Verifique se você copiar e colar cadeia de caracteres de conexão de dispositivo Olá em aspas hello.

Você verá a seguinte Olá saída mostra Olá sensor dados e hello mensagens enviadas tooyour IoT hub.

![Saída - dados de sensor enviadas do Intel Edison tooyour hub IoT](media/iot-hub-intel-edison-kit-node-get-started/15_message_sent.png)

## <a name="next-steps"></a>Próximas etapas

Executar dados de sensor de toocollect do aplicativo de exemplo e enviá-lo tooyour IoT hub.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
