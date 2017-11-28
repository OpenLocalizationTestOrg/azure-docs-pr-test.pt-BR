---
title: "Conectar o Arduino (C) ao IoT do Azure - Lição 4: modificar aplicativo | Microsoft Docs"
description: Personalize as mensagens para alterar o comportamento liga e desliga do LED.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: controlar led com arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: d7a25430-450e-43c4-a3ed-1eed995b8b7e
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5009a0466f2c5689b8ab426049f4c4f02272512b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-on-and-off-behavior-of-the-led"></a><span data-ttu-id="16e6b-104">Alterar o comportamento de ativar e desativar do LED</span><span class="sxs-lookup"><span data-stu-id="16e6b-104">Change the on and off behavior of the LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="16e6b-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="16e6b-105">What you will do</span></span>
<span data-ttu-id="16e6b-106">Personalize as mensagens para alterar o comportamento liga e desliga do LED.</span><span class="sxs-lookup"><span data-stu-id="16e6b-106">Customize the messages to change the LED’s on and off behavior.</span></span> <span data-ttu-id="16e6b-107">Se tiver problemas, procure por soluções na [página de solução de problemas](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) de sua placa Adafruit Feather M0 WiFi Arduino.</span><span class="sxs-lookup"><span data-stu-id="16e6b-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) for your Adafruit Feather M0 WiFi Arduino board.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="16e6b-108">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="16e6b-108">What you will learn</span></span>
<span data-ttu-id="16e6b-109">Utilizar funções adicionais do Arduino para alterar o comportamento liga e desliga do LED.</span><span class="sxs-lookup"><span data-stu-id="16e6b-109">Use additional Arduino functions to change the LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="16e6b-110">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="16e6b-110">What you need</span></span>
<span data-ttu-id="16e6b-111">Você deve ter concluído com sucesso [Executar um aplicativo de exemplo em sua placa do Arduino para receber mensagens de nuvem para o dispositivo][receive-cloud-to-device-messages].</span><span class="sxs-lookup"><span data-stu-id="16e6b-111">You must have successfully completed [Run a sample application on your Arduino board to receive cloud to device messages][receive-cloud-to-device-messages].</span></span>

## <a name="add-functions-to-mainc-and-gulpfilejs"></a><span data-ttu-id="16e6b-112">Adicionar funções ao main.c e ao gulpfile.js</span><span class="sxs-lookup"><span data-stu-id="16e6b-112">Add functions to main.c and gulpfile.js</span></span>
1. <span data-ttu-id="16e6b-113">Abra o aplicativo de exemplo no Visual Studio Code, executando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="16e6b-113">Open the sample application in Visual Studio code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="16e6b-114">Abra o arquivo `app.ino` e, em seguida, adicione as seguintes funções após a função blinkLED():</span><span class="sxs-lookup"><span data-stu-id="16e6b-114">Open the `app.ino` file, and then add the following functions after blinkLED() function:</span></span>

   ```arduino
   static void turnOnLED()
   {
     digitalWrite(LED_PIN, HIGH);
   }

   static void turnOffLED()
   {
     digitalWrite(LED_PIN, LOW);
   }
   ```

   ![Arquivo app.ino com funções adicionais][app-ino-file]
3. <span data-ttu-id="16e6b-116">Adicione as seguintes condições antes do bloco `else if` da função `receiveMessageCallback`:</span><span class="sxs-lookup"><span data-stu-id="16e6b-116">Add the following conditions before the `else if` block of the `receiveMessageCallback` function:</span></span>

   ```arduino
   else if (strcmp((const char*)value, "\"on\"") == 0)
   {
       turnOnLED();
   }
   else if (0 == strcmp((const char*)value, "\"off\"") == 0)
   {
       turnOffLED();
   }
   ```

   <span data-ttu-id="16e6b-117">Agora você configurou o aplicativo de exemplo para responder a mais instruções por meio de mensagens.</span><span class="sxs-lookup"><span data-stu-id="16e6b-117">Now you’ve configured the sample application to respond to more instructions through messages.</span></span> <span data-ttu-id="16e6b-118">A instrução "on" ativa o LED e a instrução "off" desativa o LED.</span><span class="sxs-lookup"><span data-stu-id="16e6b-118">The "on" instruction turns on the LED, and the "off" instruction turns off the LED.</span></span>
4. <span data-ttu-id="16e6b-119">Abra o arquivo gulpfile.js e, em seguida, adicione uma nova função antes da função `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="16e6b-119">Open the gulpfile.js file, and then add a new function before the function `sendMessage`:</span></span>

   ```javascript
   var buildCustomMessage = function (messageId) {
     if ((messageId & 1) && (messageId < MAX_MESSAGE_COUNT)) {
       return new Message(JSON.stringify({ command: 'on', messageId: messageId }));
     } else if (messageId < MAX_MESSAGE_COUNT) {
       return new Message(JSON.stringify({ command: 'off', messageId: messageId }));
     } else {
       return new Message(JSON.stringify({ command: 'stop', messageId: messageId }));
     }
   };
   ```

   ![Arquivo Gulpfile.js com funções adicionais][gulp-file-js]
5. <span data-ttu-id="16e6b-121">Na função `sendMessage`, substitua a linha `var message = buildMessage(sentMessageCount);` com a nova linha mostrada no trecho a seguir:</span><span class="sxs-lookup"><span data-stu-id="16e6b-121">In the `sendMessage` function, replace the line `var message = buildMessage(sentMessageCount);` with the new line shown in the following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="16e6b-122">Salve todas as alterações.</span><span class="sxs-lookup"><span data-stu-id="16e6b-122">Save all the changes.</span></span>

### <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="16e6b-123">Implantar e executar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="16e6b-123">Deploy and run the sample application</span></span>
<span data-ttu-id="16e6b-124">Implante e execute o aplicativo de exemplo na sua placa do Arduino executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="16e6b-124">Deploy and run the sample application on your Arduino board by running the following command:</span></span>

```bash
gulp run
# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

<span data-ttu-id="16e6b-125">Você deve ver o LED ativar por dois segundos e, em seguida, desativar por outros dois segundos.</span><span class="sxs-lookup"><span data-stu-id="16e6b-125">You should see the LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="16e6b-126">A última mensagem "stop" interrompe a execução do aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="16e6b-126">The last "stop" message stops the sample application from running.</span></span>

![liga e desliga][on-and-off]

<span data-ttu-id="16e6b-128">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="16e6b-128">Congratulations!</span></span> <span data-ttu-id="16e6b-129">Você personalizou com sucesso as mensagens que são enviadas à sua placa do Arduino do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="16e6b-129">You’ve successfully customized the messages that are sent to your Arduino board from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="16e6b-130">Resumo</span><span class="sxs-lookup"><span data-stu-id="16e6b-130">Summary</span></span>
<span data-ttu-id="16e6b-131">Essa seção opcional demonstra como personalizar as mensagens para que o aplicativo de exemplo controle o comportamento liga e desliga do LED de maneira diferente.</span><span class="sxs-lookup"><span data-stu-id="16e6b-131">This optional section demonstrates how to customize messages so that the sample application can control the on and off behavior of the LED in a different way.</span></span>

<!-- Images and links -->

[receive-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md
[app-ino-file]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_app_ino.png
[gulp-file-js]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_gulpfile_js.png
[on-and-off]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_on_and_off_arduino.png