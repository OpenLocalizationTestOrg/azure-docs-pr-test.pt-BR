---
title: aaaSimulated framboesa Pi toocloud (Node. js) - conectar framboesa Pi web simulador tooAzure IoT Hub | Microsoft Docs
description: Conecte-se tooAzure simulador de web Pi framboesa IoT Hub para Pi framboesa toosend dados toohello nuvem do Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: pi framboesa simulador, azure iot framboesa pi, framboesa pi iot hub pi framboesa enviar dados toocloud, framboesa pi toocloud
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/28/2017
ms.author: xshi
ms.openlocfilehash: 83736caf6ce723a49001058495a780f7f51946a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-online-simulator-tooazure-iot-hub-nodejs"></a>Conecte-se framboesa Pi online simulador tooAzure IoT Hub (Node. js)

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

Neste tutorial, você começar a aprender Noções básicas de saudação de trabalhar com o simulador online framboesa Pi. Em seguida, você aprenderá como tooseamlessly se conectam a nuvem de toohello Olá Pi simulador usando [Azure IoT Hub](iot-hub-what-is-iot-hub.md). 

Se você tiver dispositivos físicos, visite [tooAzure conectar framboesa Pi IoT Hub](iot-hub-raspberry-pi-kit-node-get-started.md) tooget iniciado. 

<p>
<div id="diag" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#getstarted" target="_blank">
<img src="media/iot-hub-raspberry-pi-web-simulator/3_banner.png" alt="Connect Raspberry Pi web simulator tooAzure IoT Hub" width="400">
</div>
<p>
<div id="button" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#Getstarted" target="_blank">
<img src="media/iot-hub-raspberry-pi-web-simulator/6_button_default.png" alt="Start Raspberry Pi simulator" width="400" onmouseover="this.src='media/iot-hub-raspberry-pi-web-simulator/5_button_click.png';" onmouseout="this.src='media/iot-hub-raspberry-pi-web-simulator/6_button_default.png';">
</div>

## <a name="what-you-do"></a>O que fazer

* Conheça os fundamentos de saudação do simulator online framboesa Pi.
* Crie um Hub IoT.
* Registre um dispositivo para o Pi em seu Hub IoT.
* Execute um aplicativo de exemplo em dados de sensor do Pi toosend simulado tooyour IoT hub.

Conecte o hub de IoT simulada de tooan de framboesa Pi que você criar. Em seguida, você executar um aplicativo de exemplo com os dados do sensor toogenerate Olá simulador. Por fim, você pode enviar hub IoT do hello sensor dados tooyour.

## <a name="what-you-learn"></a>O que você aprenderá

* Como toocreate um hub IoT do Azure e obter sua nova cadeia de caracteres de conexão do dispositivo. Se não tiver uma conta do Azure, [crie uma conta de avaliação gratuita do Azure](https://azure.microsoft.com/free/) em apenas alguns minutos.
* Como toowork com o simulador online framboesa Pi.
* Como hub IoT do toosend sensor dados tooyour.

## <a name="overview-of-raspberry-pi-web-simulator"></a>Visão geral do simulador de web do Raspberry Pi

Clique em simulador on-line do hello botão toolaunch framboesa Pi.

> [!div class="button"]
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted" target="_blank">Iniciar o simulador do Raspberry Pi</a>

Há três áreas no simulador do Olá web.
1. Área do assembly - circuito do saudação padrão é que um Pi se conecta com um sensor BME280 e um LED. área de saudação é bloqueada na versão de visualização assim no momento você não pode fazer a personalização.
2. Codificação área - um editor de código online para você toocode com framboesa Pi. aplicativo de exemplo Hello padrão ajuda a toocollect os dados do sensor do sensor BME280 e envia tooyour Azure IoT Hub. aplicativo Hello é totalmente compatível com dispositivos de Pi reais. 
3. Janela de console integrado - ele mostra a saída de saudação do seu código. Na parte superior do hello desta janela, há três botões.
   * **Executar** -executar o aplicativo hello em Olá codificação área.
   * **Redefinir** -Olá de redefinição de aplicativo de exemplo área toohello padrão de codificação.
   * **Dobra/expandir** - nas Olá direita lado existe é um botão para você toofold/expanda Olá janela do console.

> [!NOTE] 
simulador de web Pi framboesa Olá agora está disponível na versão de visualização. Gostaríamos toohear sua voz Olá [Gitter Chatroom](https://gitter.im/Microsoft/raspberry-pi-web-simulator). código-fonte Olá é público no [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).

![Visão geral do simulador online de Pi](media/iot-hub-raspberry-pi-web-simulator/0_overview.png)

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]


## <a name="run-a-sample-application-on-pi-web-simulator"></a>Executar um aplicativo de exemplo no simulador de web Pi

1. Na área de codificação, verifique se que você estiver trabalhando no aplicativo de exemplo hello padrão. Substitua o espaço reservado de saudação em 15 de linha com hello cadeia de conexão de dispositivo de hub IoT do Azure.
   ![Substitua a cadeia de caracteres de conexão de dispositivo Olá](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)

2. Clique em **executar** ou tipo `npm start` toorun aplicativo de hello.


Você deve ver a saída de hello a seguir que mostra dados de sensor hello e mensagens de saudação enviadas tooyour IoT hub ![saída - dados de sensor enviados do hub de IoT tooyour framboesa Pi](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)


## <a name="next-steps"></a>Próximas etapas

Executar dados de sensor de toocollect do aplicativo de exemplo e enviá-lo tooyour IoT hub.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
